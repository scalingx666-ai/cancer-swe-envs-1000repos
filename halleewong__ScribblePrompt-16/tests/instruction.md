# Issue

**Title:** [DEMO]: Add voxynth to "training" extras

## Description

Hi, this is a demo showcasing how to add training-only dependencies into a separated extra so that they are not install if scribbleprompt is installed for inference only.

By running :
`pip install "scribbleprompt @ git+https://github.com/halleewong/ScribblePrompt.git"`, voxynth will not be installed :
![image](https://github.com/user-attachments/assets/994062bf-0a54-4279-bda5-e5103320d3e6)

And running:
`pip install "scribbleprompt[training] @ git+https://github.com/halleewong/ScribblePrompt.git"` will result in voxynth being installed correctly:
![image](https://github.com/user-attachments/assets/1840f860-f691-4b25-b377-4c65fc1cfcf5)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `70e12c8dfeaf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.