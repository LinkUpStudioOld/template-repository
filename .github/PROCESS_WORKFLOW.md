# Workflow

## Overview

![](https://user-images.githubusercontent.com/7302777/76073858-fea83a80-5fa2-11ea-8661-ce6bf2176456.png)

Basically, we have to maintain 7 types of branches:

- `master`: Stable, direct to production.
- `develop`: Unstable, all feature changes will be pushed here. Feature, refactor, and bug fix branches are created from `develop`. When a feature, refactor, or fix is complete it is merged into `develop`.
- `feature`: Check out from `develop` branch, and push changes back to it.
- `refactor`: The same as `feature` but it's not a new features, it can be code refactor or text changes or update dependencies or something else which is not something new.
- `hotfix`:  If an issue in `master` is detected a hotfix branch is created from `master`. Once the hotfix is complete it is merged to both `master` and `develop`.
- `fix`: Similar to `hotfix` but an issue is detected on unstable branch as `develop`.
- `release`: Semi-stable, ready to release, following with a few bugfixes. Checkout from `develop` and push to both `master` and `develop` if it's done.

All branches should follow the syntax of `{type}/{details}` where `{type}` is the type of branch (`hotfix`, `release`, or one of the [commit types](/.github/PROCESS_COMMIT_MESSAGE.md)) and `{details}` is a few hyphen separated words explaining the branch. You can use other name of type, it's not forbidden. It's just rules for better understanding the process.

## Master and Develop Branches

### Master Branch

Branches created from `master`:

The following branch should be merged back to **both** `master` and `develop`:

- A `hotfix` branch (e.g. `hotfix/style-changes`): a bug fix that is fixing an issue with a published release

A `hotfix` branch should be the **only** branch that is created from `master`.

### Develop Branch

Branches created from `develop`:

The following branches should be merged back to `develop`:

1. A feature branch (e.g. `feature/oauth2-support`): an addition to the API that is not a bug fix or regression fix
1. A bug fix branch (e.g. `fix/tab-color`): a bug fix that is not fixing a regression or issue with a published release
1. All other types listed in the [commit message types](/.github/PROCESS_COMMIT_MESSAGE.md)

The following branch should be merged back to **both** `master` and `develop`:

1. A `release` branch (e.g. `release/0.1.x`): contains all fixes and (optionally) features that are tested and should go into the release


## Feature Branches

Each new feature should reside in its own branch, based on the `develop` branch. When a feature is complete, it should be merged back into `develop`. Features should never interact directly with `master`.

## Refactor Branches

Each part of refactor should reside in its own branch, based on the `develop` branch. When a refactor is complete, it should be merged back into `develop`. Refactor should never interact directly with `master`.


## Release Branches

Once `develop` has acquired enough features for a release (or a predetermined release date is approaching), fork a `release` branch off of `develop`. Creating this branch starts the next release cycle, so no new features can be added after this point - only bug fixes, documentation generation, changelog, and other release-oriented tasks should go in this branch.

Once the `release` is ready, it will get merged into `master` and `develop`, then the `release` branch will be deleted. It’s important to merge back into `develop` because critical updates may have been added to the release branch and they need to be accessible to new features. This should be done in a pull request after review. A pull request adding a feature should be approved by one team member.

## Hotfix Branches

Maintenance or “hotfix” branches are used to quickly patch production releases. This is the only branch that should fork directly off of `master`. As soon as the fix is complete, it should be merged into both `master` and `develop` (or the current release branch).

## Fix Branches

“fix” branches are used to quickly patch for develop. This branch similar to `refactor`. As soon as the fix is complete, it should be merged into `develop` (or the current release branch).

## Examples

### Making a Change

1. Create a branch from `develop`.
1. Make changes. Limit your changes to a "unit of work", meaning don't include irrelevant changes that may confuse and delay the change.
1. Push changes.
1. Create a PR with the base of `develop` or just merge into `develop`.


### Updating from `develop`

1. Pull the latest changes locally.
1. Merge the changes, fixing any conflicts.
1. Push the merged changes.


### Hotfixes

Hotfixes bypass `develop` and should only be used for urgent fixes that can't wait for the next release to be ready.

1. Create a branch from `master`.
1. Make changes.
1. Push changes.
1. Create a PR, making sure the PR will merge into `master`.
1. Click **Squash and merge**. Use the dropdown to select this option if necessary.

    <img width="192" alt="Squash and merge button" src="https://user-images.githubusercontent.com/236501/47031620-da418900-d135-11e8-91ff-e84f2478b2b3.png">


1. Confirm squash and merge into `master`.
1. Delete created branch.
1. Merge `master` into `develop`.

### Merge branches

When you merge 2 branches, don't change commit message. Just write `git commit` in the terminal (or IDE) without `-m` flag, you will see editor like vim or nano, close it and that is all.
Sometimes you can get conflicts after merge. You need to fix conflicts in specific files, add only these files via `git add [filename]` (or IDE). And write `git commit` without message.
