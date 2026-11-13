# Issue

**Title:** Improvements for Using the SDM-RDFizer as a Library

## Description

This PR includes several changes to improve the user experience when using the SDM-RDFizer as a Python library within other projects.

1. **No more duplicated code.** It is enough if the ``__init__.py`` contains
    ```python
    from rdfizer.semantify import semantify
    ```
    There is no need to actually copy the code. Projects can still use ``from rdfizer import semantify`` or ``from rdfizer.semantify import semantify``. So this is not a breaking change. It only improves the maintainability.

2. **Passing of configuration as a Python dictionary.** It is now possible to pass a Python dictionary instead of a string representing the path of the configuration file. The SDM-RDFizer will check for the type of the passed argument to determine whether the configuration is created from a dictionary or a file. This change enables users of the SDM-RDFizer Python library to create the configuration within their own project without the need of writing it to a file. This is particularly helpful for dynamic configurations.

3. **Loggers instead of print().** There was already a logger which was used for errors. The logger is set up in a way that all messages (``logging.INFO`` and above) are printed on console while errors and exceptions are also written to a log file. The remaining print commands are now also changed to use the logger. This enables users to change the logging level of the logger named ``rdfizer`` to show more or less messages when used as a library.

Additionally, this PR removes unused imports.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b3c1a1d1427`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.