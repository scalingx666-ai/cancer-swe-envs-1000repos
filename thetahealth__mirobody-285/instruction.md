# Issue

**Title:** demo: add Chinese lab reports and validate walkthrough exports

## Description

## Summary

Add three synthetic historical reports for `you`, so the walkthrough can show the same lab test printed in Chinese and English, under different names and in different units, without uploading a real person's report.

| File | Date | LDL spelling | Unit |
| --- | --- | --- | --- |
| `you_lab_report_zh_2023-03.pdf` | 2023-03-21 | `LDL-C` | mmol/L |
| `you_checkup_photo_zh_2024-04.jpg` | 2024-04-16 | `低密度脂蛋白胆固醇` | mg/dL |
| `you_lab_results_en_2025-03.xlsx` | 2025-03-25 | `LDL Cholesterol` | mg/dL |

Each file has 16 invented readings and identifies itself as synthetic. All 16 analytes resolve to the same respective series across the three files. The reports remain optional uploads; they are not seeded into the initial record. The walkthrough and quickstart explain them in English, Chinese and Japanese.

## Export and regression fixes

- Export every seeded panel, including mom's older mg/dL report. The fixture now contains 2,022 seeded readings, three seed files and seven upload files, with a source file for every cited reading.
- Keep `period` at device coverage, **2025-09-15 through 2026-09-14**, even though an older lab panel predates it. The previous draft accepted the lab date as the device-window start; the restored assertion reproduced that error before the fix.
- Add an offline test of all 48 historical readings: spelling and unit variants must share each analyte's series, and the 16 analytes must remain distinct.
- Run `python demo/test_export.py` in the full-install CI job and include `demo/` in Ruff's scope. These files were outside the existing gates.
- Save workbooks with fixed timestamps and ZIP metadata. The existing mom workbook changes bytes but retains the same cells. PDF string grouping and explicit `zip(strict=True)` also pass the expanded lint scope.

The seed-export correction overlaps #288. This PR remains self-contained and includes its device-window behavior; it also adds the historical uploads and their regression checks.

## Validation

Fresh checks against this PR's source:

- `pytest -q`: **1500 passed, 169 skipped, 12 xfailed**.
- `python demo/test_export.py`: **5 passed**.
- `ruff check mirobody examples benchmarks/windows demo`: passed.
- `python -m compileall -q mirobody`: passed.
- `lint-imports`: **6 kept, 0 broken**; bare library imports passed.
- PDF and workbook extracted through `documents.extract` and the table rules without a model: **16 readings each, correct dates, zero unread rows**.
- Actual Chinese PDF and photo visually inspected. Rebuilding all seven uploads twice leaves their bytes unchanged.
- Workflow YAML, version check, comment-style gate and `git diff --check` on text files: passed.

## Limits

This review did not rerun a live model, a database ingestion or a cloud vision model. Earlier testing on released 1.6.1 with MiniCPM5-2B and GLM-OCR recorded 16 readings from each file and one LDL trend. That earlier run also observed existing model errors around choosing a sampling/report date, inventing a day in a filename and calculating a percentage; those are outside this fixture change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8087fddcbcbb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.