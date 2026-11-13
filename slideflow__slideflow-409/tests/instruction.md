# Issue

**Title:** Add features

## Description

# Add feature addition functionality to DatasetFeatures

This PR adds a new method `add_features()` to the `DatasetFeatures` class, allowing users to incorporate additional features from annotation files into the existing feature set. 

## Changes

- Added `add_features()` method to `DatasetFeatures` class in `features.py`
- The method allows adding both categorical and numerical features from annotations
- Categorical features are one-hot encoded
- The one-hot encoding is non redundant, there will be one fewer column than the total number of categories
- Numerical features are added directly
- Added error handling for missing columns, non-numerical values, and missing slides
- Updated feature indexing and printing feature correspondence
- The same features are appended redundantly to the end of every vector

## Usage

Users can now add features from annotations like this:

```python
features.add_features(
    annotations='path/to/annotations.csv',
    categorical_cols=['stage', 'grade'],
    numerical_cols=['age', 'tumor_size'],
    slide_col='slide_id'
)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `106190191e26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.