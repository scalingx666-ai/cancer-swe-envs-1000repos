# Issue

**Title:** fix(core): the reader gives no value for a zero-length string element

## Description

.

## Problem

A Part 10 reader gave a zero-length string element as one empty value, `Value: [""]`. The event stream sent one `value("")` call for the element. Thus an empty VM 1-n attribute naturalized as `[""]`, and an empty VM 1 attribute naturalized as `""`. NAT-U-VAL-1 and NAT-U-VAL-2 of `docs/specs/naturalized-dataset.md` require `null` and `[]`.

## Change

- `ValueRepresentation.read` returns no value (`[]`) for a zero-length element of a string VR. The new method `isString()` is `true` for `AsciiStringRepresentation` and `EncodedStringRepresentation`.
- Every reader calls `read`: `DicomMessage.readFile`, `AsyncDicomReader`, and `decodeCore` (`fromPart10`). The reader of an explicit-VR UN element with a known string VR also calls `read`. So each reader now gives `Value: []`, and the event stream sends `startElement` and `endElement` with no `value()` call.
- The naturalize shape rules do not change. They already give `null` and `[]` for no value.
- An empty value inside a longer list stays. For example, `\ab\\c` gives `["", "ab", "", "c"]`.
- The implementation section of the spec states the reader rule. The NAT-U-RT-7 example now uses `1\\2` (`[1, null, 2]`), because an empty DS no longer reads as `[null]`.
- The user requirements do not change. The change restores NAT-U-VAL-1 and NAT-U-VAL-2.

## Effect for users

| Zero-length element | Before | After |
| --- | --- | --- |
| Dict form of a string VR, for example CS or LO | `Value: [""]` | `Value: []` |
| Dict form of an empty DS or IS | `Value: [null]` | `Value: []` |
| Dict form `_rawValue` of an empty PN | `""` | `[]` |
| Naturalized VM 1-n or 2-n, for example `ModalitiesInStudy` | `[""]` | `[]` |
| Naturalized VM 1, for example `PatientID` | `""` | `null` |
| Naturalized PN, for example `PatientName` | `null` | `null` (no change) |

Code that reads `Value[0]` of an empty string element in the dict form now gets `undefined`, not `""`. Code that reads an empty naturalized VM 1 string attribute with `.length` or a string method must now accept `null`. A write of the dict form keeps the same bytes, because `[]` and `[""]` both write a zero-length element.

## Tests

- New `test/eventStream/emptyString.test.js`, 2 tests (implicit VR and explicit VR little endian):
  - `readFile` gives `Value: []` for zero-length CS and LT elements, and keeps `["", "ab", "", "c"]`.
  - `naturalizeDataset` and `NaturalizedListener` from `fromPart10` both give `[]` and `null`.
  - The event stream sends only the two empty values of `\ab\\c`.
- Without the fix, both tests fail.
- Three existing tests expected the old shape for a zero-length element (`[""]`, `[null]`, `""`), and now expect `[]`:
  - `test/lossless-read-write.test.js`: the UT case of "changed value overwrites original value", and "0 length PN tag should be retained".
  - `test/core/nullEntries.test.js`: the DS `[null]` round trip.
- The full suite passes: 114 suites, and 1215 tests pass with 12 skipped.

## Note on the history

The first commit put the fix in the naturalize shape rules. The second commit moves the fix into the reader and removes the first approach. The diff against `1.0-beta` holds only the reader fix.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `491b04b5cb28`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.