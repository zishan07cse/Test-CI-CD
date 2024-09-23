# GitHub Actions CI/CD Workflow

This repository implements a CI/CD workflow using GitHub Actions. The workflow is designed to handle multiple branches: `development`, `feature/*`, and `production`. The following outlines the processes involved:

## Workflow Overview

1. **Branches**:
   - **Development**: The main integration branch where all feature branches are merged.
   - **Feature Branches**: These branches are used for developing new features. They are named with the prefix `feature/`.
   - **Production**: The stable branch that represents the production-ready code.

2. **Triggering the Workflow**:
   - The workflow is triggered on:
     - Push events to any feature branch.
     - Pull request events targeting the `development` branch.

3. **Steps in the Workflow**:
   - **Linting**: The code in the feature branch is automatically linted to ensure quality and consistency.
   - **Unit Testing**: The workflow runs unit tests to verify the functionality of the new feature.
   - **Automatic Pull Requests**:
     - If the linting and testing pass, an automatic pull request is created to merge the feature branch into the `development` branch.
     - After the pull request for the `development` branch is accepted, the same checks are performed, and an automatic pull request is created to merge into the `production` branch.
   - **Deployment**: Once the pull request for the `production` branch is accepted, the code is automatically deployed to an AWS EC2 instance.

## Detailed Steps

### 1. Workflow Configuration

The workflow is defined in the `.github/workflows/test-ci-cd.yml` file. Key configurations include:

- **Node.js Setup**: The workflow uses Node.js version 20.
- **Linting and Testing**: Custom scripts are defined for linting and running unit tests.
- **PR Creation**: The workflow uses the `poorva17/create-pr-action` to automate pull request creation.
- **SSH Setup**: The deployment process sets up an SSH agent to connect to the AWS EC2 instance.

### 2. Secrets Configuration

Ensure the following secrets are configured in your GitHub repository:

- **GIT_TOKEN**: A GitHub personal access token with repository access.
- **EC2_SSH_KEY**: The private key for SSH access to your AWS EC2 instance.
- **EC2_IP**: The public IP address or DNS of your EC2 instance.

### 3. Directory Structure

The project is expected to have the following directory structure:

