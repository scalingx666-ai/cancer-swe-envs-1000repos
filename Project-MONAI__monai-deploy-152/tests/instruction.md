# Issue

**Title:** MONAI Deploy 0.6.0 release

## Description

**This is NOT recommended for production environments**

Please review the [README](https://github.com/Project-MONAI/monai-deploy/tree/main/deploy/monai-deploy-express) for details about prerequisites, installation, start/stop services, running workflows with MONAI Applications (MAPs) and some tips!

---

This release is based on the following services:

### MONAI Deploy Services

   | Service                           | Version        |
   | ----------------------- | --------------------- | 
   | [Informatics Gateway (IG)](https://github.com/Project-MONAI/monai-deploy-informatics-gateway) | [0.5.0](https://github.com/Project-MONAI/monai-deploy-informatics-gateway/releases/tag/0.5.0)                     |
   | [Workflow Manager (WM)](https://github.com/Project-MONAI/monai-deploy-workflow-manager) | [0.2.0](https://github.com/Project-MONAI/monai-deploy-workflow-manager/releases/tag/0.2.0)
   | [Task Manager (TM)](https://github.com/Project-MONAI/monai-deploy-workflow-manager) - part of WM repo as of today, but designed as a standalone service | [0.2.0](https://github.com/Project-MONAI/monai-deploy-workflow-manager/releases/tag/0.2.0)


### Third-Party Services

| Service                                                         |  Version         |
| ---------------------------------------- | ------------------------ |
| MinIO (default storage service)                                 |  RELEASE.2024-06-11T03-13-30Z |
| RabbitMQ (default message broker service)                       |  3.12.7-management |
| MongoDB (default database for WM & TM) |  5.0.25 |
| Orthanc (optional)                                           |  24.6.1-full |
| Elastic Search (optional)                                           |  8.7.0 |
| Log Stash (optional)                                           |  8.7.0 |
| Kibana (optional)                                           |  8.7.0 |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8ebac515401a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.