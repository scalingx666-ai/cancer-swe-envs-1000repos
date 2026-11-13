# Issue

**Title:** Update main.py - dose_score/dvh_score were swapped

## Description

dose_score and dvh_score were swapped, see the .get_scores() function

current:         dvh_score, dose_score = dose_evaluator.get_scores()
new:               dose_score, dvh_score = dose_evaluator.get_scores()

def get_scores(self) -> tuple[NDArray, NDArray]:
        dose_score = np.nanmean(self.dose_errors)
        dvh_errors = np.abs(self.reference_dvh_metrics_df - self.prediction_dvh_metrics_df)
        dvh_score = np.nanmean(dvh_errors.values)
        return dose_score, dvh_score

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `788512514708`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.