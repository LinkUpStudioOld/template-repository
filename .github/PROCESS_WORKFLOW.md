[!!!][You can use one of two workflows that shared below. **Workflow 1** is for projects that should be developed as quickly as possible, it doesn't care about quality, release happens few times a week. **Workflow 2** is for stable projects, each release should be tested before merge into main. Remove this comment after project init]

# Workflow 1
![Git Workflows-workflow without develop branch drawio (1)](https://github.com/LinkUpStudioOld/template-repository/assets/7302777/49c48fa4-5e47-4ba5-95eb-59330b5b56bc)

## Overview
### Main Branch - Staging Deployment
Changes merged into the main branch are automatically deployed to the staging environment. This ensures that the staging environment reflects the latest state of the application's production codebase.

### Feature Branches - Development
Developers create feature branches from the main branch to work on specific features or tasks.

Once a feature is complete, the branch is merged back into the main branch via a pull request (PR).

### Hotfix Branches - Bug Fixes
If critical issues arise in the production environment, hotfix branches are created from the main branch.

The hotfix is developed and tested on the hotfix branch.

Once the fix is ready, it's merged back into the main branch and deployed to staging.

### Production Release
After merging changes into the main branch and deploying them to staging, create a tag in Git to mark the specific commit that will be released to production.

Draft a release using the created tag.

Automatically generate the release description from commit messages, utilizing the [commit type](/.github/PROCESS_COMMIT_MESSAGE.md) for each change.

The automated release description can provide a concise summary of the changes included in the release.

### Publish Release - Trigger Build and Deployment
When ready to release to production, publish the draft release.

Publishing the release can be set up to trigger a build and deployment process to the production environment.

## Branch Naming Convention:
- Feature Branch: `feature/{details}`
- Hotfix Branch: `hotfix/{details}`

All branches should follow the syntax of `{type}/{details}` where `{type}` is the type of branch (`hotfix`, `feature`, or one of the [commit types](/.github/PROCESS_COMMIT_MESSAGE.md)) and `{details}` is a few hyphen separated words explaining the branch. You can use other name of type, it's not forbidden. It's just rules for better understanding the process.

## Workflow Benefits:
- Provides a simplified and streamlined branching strategy.
- Direct deployment from main to staging ensures a stable staging environment.
- Feature branches allow for isolated feature development and thorough testing before merging.
- Hotfix branches facilitate quick response to critical production issues.



# Workflow 2

![Git Workflows-workflow with develop branch drawio (2)](https://github.com/LinkUpStudioOld/template-repository/assets/7302777/18307e95-ab61-4d86-a1c1-027c40f12016)


## Overview
### Main Branch - Staging Deployment
Changes merged into the main branch are automatically deployed to the staging environment. This ensures that the staging environment reflects the latest state of the application's production codebase.

### Develop Branch - Continuous Integration
The develop branch is used for ongoing integration of feature, refactor, and bug fix changes.

Developers create feature, refactor, and bug fix branches from the develop branch.

Changes from these branches are merged back into develop once complete.


### Feature Branches - New Features
Developers create feature branches from the develop branch to work on specific new features.

Once a feature is complete, the branch is merged back into the develop branch via a pull request (PR).

### Refactor Branches - Code Changes
Refactor branches are used for code improvements, text changes, dependency updates, etc.

Similar to feature branches, refactor branches are created from and merged back into the develop branch.

### Hotfix Branches - Production Fixes
If a critical issue is detected in the main branch, a hotfix branch is created from main.

The hotfix is developed and tested on the hotfix branch.

Once the fix is ready, it's merged back into both the main and develop branches.

### Fix Branches - Unstable Fixes
Similar to hotfix branches, fix branches are used to address critical issues detected on the unstable develop branch.

Fixes are developed and tested on the fix branch before merging back into develop.

### Release Branches - Semi-Stable Releases
Release branches are used for preparing semi-stable releases.

Developers create a release branch from the develop branch.

After including a few bug fixes and ensuring stability, the release branch is merged back into both the main and develop branches.

## Branch Naming Convention:

- Feature Branch: `feature/{details}`
- Refactor Branch: `refactor/{details}`
- Hotfix Branch: `hotfix/{details}`
- Fix Branch: `fix/{details}`
- Release Branch: `release/{details}`

All branches should follow the syntax of `{type}/{details}` where `{type}` is the type of branch (`hotfix`, `feature`, `release`, or one of the [commit types](/.github/PROCESS_COMMIT_MESSAGE.md)) and `{details}` is a few hyphen separated words explaining the branch. You can use other name of type, it's not forbidden. It's just rules for better understanding the process.

## Workflow Benefits:

- Provides a clear and structured branching strategy for both new features and maintenance changes.
- Separate branches for different types of changes make it easier to track and manage the codebase's evolution.
- Differentiates between critical production fixes (hotfixes) and unstable branch fixes (fixes).

# Other

## Production release

Follow [releasing process](PROCESS_RELEASING.md) instructions

## Merge branches

When you merge 2 branches, don't change commit message. Just write `git commit` in the terminal (or IDE) without `-m` flag, you will see editor like vim or nano, close it and that is all.
Sometimes you can get conflicts after merge. You need to fix conflicts in specific files, add only these files via `git add [filename]` (or IDE). And write `git commit` without message.
