# Issue

**Title:** Refactoring of lib.fileio.auto_open function to work with subprocess

## Description

1. CommandFormatter Interface
Introduced the CommandFormatter interface, encapsulating file operations and validations.​
Added standard CLI response outputs to enhance user interaction.​
 2. MODES_TO_FILES_PRESET and COMMANDS Configurations (just 2 dicts)
MODES_TO_FILES_PRESET: format keys with values as lists of possible operation modes (read, write, append).
COMMANDS: format and mode keys with values as dictionaries containing:
tool: the tool's presence is verified in the system.
command: a command formatted for substituting the number of available processors (nproc).
This structure streamlines adding new formats without altering existing code.​
3. Binary File Support in CommandFormatter
Added capabilities for handling binary files.​
This feature is not currently utilized but provides flexibility for future enhancements.​
4. Integration with subprocess
Transitioned to using subprocess for file operations, improving compatibility and performance.​


P.S. The function signatures and responses of auto_open remain unchanged, ensuring backward compatibility. However, the implementation using the CommandFormatter class offers a more convenient and versatile approach, enhancing code maintainability and scalability.​

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `737a23639997`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.