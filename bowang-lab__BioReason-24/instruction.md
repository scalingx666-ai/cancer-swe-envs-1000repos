# Issue

**Title:** Fix SFT supervision and other critical bugs across the codebase

## Description

The headline fix is for the silently-broken SFT loss path in train_dna_qwen.py: qwen_dna_collate_fn defaulted truncate_for_generation=True, which dropped the assistant span (and all real label IDs) from the batch before the loss was computed, so train/val loss was being calculated over near-empty -100 targets. Default is flipped to False so the SFT path supervises the assistant answer as intended.

Other fixes:

bioreason/models/dna_llm.py
- Call resize_token_embeddings after adding the DNA special tokens so the embedding/output matrices stay in sync with the (possibly-extended) tokenizer.
- Stop forcing torch.no_grad() on the DNA encoder unconditionally; gate it on dna_model_finetune so the flag is actually honored. Uses nullcontext() when trainable to inherit the caller's grad state.
- Drop the 2 * batch_size over-allocation in process_dna_embeddings — the trailing slots were never written and only produced zero-row tensors that contributed nothing to the downstream torch.cat. Verified bit-exact equivalent to the original (max abs diff = 0.0). Matches the existing dna_vllm.py process_dna_embeddings sibling.
- Switch the per-sequence gather from projected_states[seq_idx, :valid_length] to mask-indexed projected_states[seq_idx][attn.bool()] so Evo2 (left-padding) works correctly. Equivalent for NT and other right-padding tokenizers.
- Remove dead DNAInput import and the no-op self.dna_embedding_layer = self.dna_embedding_layer self-assign.

bioreason/trainer/grpo_trainer.py + grpo_config.py
- Derive the reference-model arch from model.text_model.config._name_or_path instead of the hardcoded "Qwen/Qwen3-4B".
- Respect args.vllm_max_model_len instead of the hardcoded max_model_len=10000.
- Remove the duplicate vllm_gpu_memory_utilization field in the config (the second declaration was silently overriding the first).

train_grpo.py
- Fix _prep_for_training call sites that passed ghost kwargs (protein_model_finetune / go_model_finetune / freeze_protein_modules) that don't exist on GRPOModelConfig and would AttributeError on any non-SFT path. Now pass dna_model_finetune / dna_projection_finetune as _prep_for_training actually expects.
- Pass map_location="cpu" to torch.load(sft_checkpoint) to avoid GPU OOM on large checkpoints.
- Drop no-op magic.replace("protein_model", "protein_model").

reason.py
- Fix zip(extracted_responses, answer[0]) in correctness_reward_func — the [0] index was iterating characters of the first answer string instead of the answer list.
- Remove the dead duplicate _get_target_modules that referenced non-existent model.text.

train_dna_only.py
- Use clean_variant_effect_non_snv_example for the non_snv branch (previously was using the SNV cleaner, leaving non_snv labels as bracketed list strings).
- sorted(set(labels)) for the KEGG label list — set() ordering is process-local, so different DDP ranks could build different label2id mappings.
- Rank-guard the final torch.save to avoid concurrent writes corrupting the file under DDP.
- Remove the unconditional os.environ["CUDA_VISIBLE_DEVICES"] = "0" that silently single-GPU'd multi-GPU runs.

train_dna_qwen.py
- on_test_epoch_end: anchor the csv path next to --ckpt_path (which is a file) via os.path.dirname() instead of joining inside the file path.
- Don't re-timestamp args.checkpoint_dir when resuming from --ckpt_path, or wandb's resume="allow" would resume into a stale, freshly-timestamped dir.

eval_kegg_dna_vllm.py
- sorted(set(all_answers)) so the chosen positive label for the binary precision/recall computation is deterministic across runs.

BUGS.md (new)
- Catalog of all findings from the audit pass with severity, file:line, and fix direction. Useful context for reviewers.

Verified end-to-end on H100 with Qwen3-1.7B + NT-500M:
- truncate_for_generation fix: 14.5% non-(-100) label coverage (was 0%).
- resize_token_embeddings: dna_token_id=151670 < vocab=151672.
- Alignment: 80 <|dna_pad|> slots ↔ 80 valid DNA tokens.
- Forward loss finite (~7.97); backbone.grad=None when frozen, dna_projection.grad.norm > 0.
- 5-step optim step: loss decreases monotonically (9.07 → 7.74).
- Full Lightning fit() on real KEGG: 2 train steps via _step complete.
- 2*B → B equivalence: max abs diff = 0.0e+00 over [140, 2048] flat output.
- Mask-indexed gather is bit-exact for right-pad and correct for left-pad (where the original code would pick padding-token embeddings).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4dd776849d92`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.