[!!!][You can use one of two workflows that shared below. **Workflow 1** is for projects that should be developed as quickly as possible, it doesn't care about quality, release happens few times a week. **Workflow 2** is for stable projects, each release should be tested before merge into main.]

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
- Feature Branch: feature/{details}
- Hotfix Branch: hotfix/{details}

All branches should follow the syntax of {type}/{details} where {type} is the type of branch (hotfix, feature, or one of the [commit types](/.github/PROCESS_COMMIT_MESSAGE.md)) and {details} is a few hyphen separated words explaining the branch. You can use other name of type, it's not forbidden. It's just rules for better understanding the process.

## Workflow Benefits:
- Provides a simplified and streamlined branching strategy.
- Direct deployment from main to staging ensures a stable staging environment.
- Feature branches allow for isolated feature development and thorough testing before merging.
- Hotfix branches facilitate quick response to critical production issues.



# Workflow 2

![Git Workflows-workflow with develop branch drawio](https://github.com/LinkUpStudioOld/template-repository/assets/7302777/40f730fa-9a4e-4af9-9ec0-0852fb9ccb05)


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


# Outdated
![04 Hotfix branches](https://github.com/LinkUpStudioOld/template-repository/assets/7302777/ed90fadd-373a-4249-82f5-548e0765cba8)

Basically, we have to maintain 7 types of branches:

- `main`: Stable, direct to staging.
- `develop`: Unstable, all feature changes will be pushed here. Feature, refactor, and bug fix branches are created from `develop`. When a feature, refactor, or fix is complete it is merged into `develop`.
- `feature`: Check out from `develop` branch, and push changes back to it.
- `refactor`: The same as `feature` but it's not a new features, it can be code refactor or text changes or update dependencies or something else which is not something new.
- `hotfix`:  If an issue in `main` is detected a hotfix branch is created from `main`. Once the hotfix is complete it is merged to both `main` and `develop`.
- `fix`: Similar to `hotfix` but an issue is detected on unstable branch as `develop`.
- `release`: Semi-stable, ready to release, following with a few bugfixes. Checkout from `develop` and push to both `main` and `develop` if it's done.

All branches should follow the syntax of `{type}/{details}` where `{type}` is the type of branch (`hotfix`, `release`, or one of the [commit types](/.github/PROCESS_COMMIT_MESSAGE.md)) and `{details}` is a few hyphen separated words explaining the branch. You can use other name of type, it's not forbidden. It's just rules for better understanding the process.

## Main and Develop Branches

### Main Branch

Branches created from `main`:

The following branch should be merged back to **both** `main` and `develop`:

- A `hotfix` branch (e.g. `hotfix/style-changes`): a bug fix that is fixing an issue with a published release

A `hotfix` branch should be the **only** branch that is created from `main`.

### Develop Branch

Branches created from `develop`:

The following branches should be merged back to `develop`:

1. A feature branch (e.g. `feature/oauth2-support`): an addition to the API that is not a bug fix or regression fix
1. A bug fix branch (e.g. `fix/tab-color`): a bug fix that is not fixing a regression or issue with a published release
1. All other types listed in the [commit message types](/.github/PROCESS_COMMIT_MESSAGE.md)

The following branch should be merged back to **both** `main` and `develop`:

1. A `release` branch (e.g. `release/0.1.x`): contains all fixes and (optionally) features that are tested and should go into the release


## Feature Branches

Each new feature should reside in its own branch, based on the `develop` branch. When a feature is complete, it should be merged back into `develop`. Features should never interact directly with `main`.

## Refactor Branches

Each part of refactor should reside in its own branch, based on the `develop` branch. When a refactor is complete, it should be merged back into `develop`. Refactor should never interact directly with `main`.


## Release Branches

Once `develop` has acquired enough features for a release (or a predetermined release date is approaching), fork a `release` branch off of `develop`. Creating this branch starts the next release cycle, so no new features can be added after this point - only bug fixes, documentation generation, changelog, and other release-oriented tasks should go in this branch.

Once the `release` is ready, it will get merged into `main` and `develop`, then the `release` branch will be deleted. It’s important to merge back into `develop` because critical updates may have been added to the release branch and they need to be accessible to new features. This should be done in a pull request after review. A pull request adding a feature should be approved by one team member.

### Production release

Follow [releasing process](PROCESS_RELEASING.md) instructions

## Hotfix Branches

Maintenance or “hotfix” branches are used to quickly patch production releases. This is the only branch that should fork directly off of `main`. As soon as the fix is complete, it should be merged into both `main` and `develop` (or the current release branch).

## Fix Branches

“fix” branches are used to quickly patch for develop. This branch similar to `refactor`. As soon as the fix is complete, it should be merged into `develop` (or the current release branch).

## Other

### Merge branches

When you merge 2 branches, don't change commit message. Just write `git commit` in the terminal (or IDE) without `-m` flag, you will see editor like vim or nano, close it and that is all.
Sometimes you can get conflicts after merge. You need to fix conflicts in specific files, add only these files via `git add [filename]` (or IDE). And write `git commit` without message.
