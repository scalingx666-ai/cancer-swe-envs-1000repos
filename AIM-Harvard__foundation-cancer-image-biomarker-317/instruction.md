# Issue

**Title:** Patch0001

## Description

## Description

<!-- Add a more detailed description of the changes if needed. -->

## Related Issue

<!-- If your PR refers to a related issue, link it here. -->

## Type of Change

<!-- Mark with an `x` all the checkboxes that apply (like `[x]`) -->

- [ ] 📚 Examples / docs / tutorials / dependencies update
- [ ] 🔧 Bug fix (non-breaking change which fixes an issue)
- [ ] 🥂 Improvement (non-breaking change which improves an existing feature)
- [ ] 🚀 New feature (non-breaking change which adds functionality)
- [ ] 💥 Breaking change (fix or feature that would cause existing functionality to change)
- [ ] 🔐 Security fix

## Checklist

<!-- Mark with an `x` all the checkboxes that apply (like `[x]`) -->

- [ ] I've read the [`CODE_OF_CONDUCT.md`](https://github.com/foundation_image_biomarker/foundation-image-biomarker/blob/master/CODE_OF_CONDUCT.md) document.
- [ ] I've read the [`CONTRIBUTING.md`](https://github.com/foundation_image_biomarker/foundation-image-biomarker/blob/master/CONTRIBUTING.md) guide.
- [ ] I've updated the code style using `make codestyle`.
- [ ] I've written tests for all new methods and classes that I created.
- [ ] I've written the docstring in Google format for all the methods and classes that I used.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **Chores**
  • Updated build configuration to enforce Python 3 usage consistently.
  • Updated dependencies in the project configuration file to newer versions and added new dependencies.

- **Documentation**
  • Revised command guidelines in several guides by standardizing flag usage with an equals sign for configuration file arguments.

- **Bug Fixes**
  • Enhanced error handling in image processing routines to gracefully manage missing inputs while providing compressed outputs.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `860b90b857f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.