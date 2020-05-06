# Process

This document is to describe the internal process that the LinkUp team uses for issue management, project planning and the development workflow.

## Table of contents
 * [Project Boards](#project-boards)
 * [Managing Issues](#managing-issues)
 * [Workflow](#workflow)
 * [Releasing](#releasing)

## Project Boards

The project boards are located under the `Projects` tab in GitHub. It contains issues or pull requests related to the project. You can have many boards for different sprints/milestones. The each board includes 4 main columns.

### To Do

Contains issues that we believe we can accomplish in the current sprint. Issues should be manually moved to this column when we have our sprint planning meeting.

### In Progress

Issues and pull requests that are currently being worked on. Issues should be manually moved to this column and assigned to yourself when you begin working on them. Pull requests are automatically added to this column when added to the project board.

### Needs Review

Issues and pull requests that need review. Pull requests will automatically move here when a reviewer requests changes, or it no longer meets the minimum number of required approving reviews.

### Done

Issues and pull requests that are completed. Issues will automatically move here when they are closed. Pull requests will automatically moved here when they are merged or closed with unmerged commits.


## Managing Issues

### Issues

Issue can be created by anyone who have access to repository. When create issue you will see default template.

If the developer wants to add a new feature, or he found some bug then he creates a new issue and assigns somebody.

If QA found some bug or he suggest to add some feature to a project, he creates a new issue in GitHub repository. QA should set label and assign someone who will do it.

### Labels

We use 8 default labels which added to the repository when start developing.

- `bug` - Something isn't working
- `docs` - Improvements or additions to documentation
- `question` - Indicates that an issue or pull request needs more information
- `production` - Indicates that an issue happened on production
- `staging` - Indicates that an issue happened on staging
- `on hold` - Needs discuss or approvement
- `next phase` - Approved but will implement in the future
- `on testing` - Issue fixed but needs additional testing

### Projects

Issue can be related to GitHub projects. You can set it during issue creation.

### Milestone

We are working with small milestones for one or two or more weeks. So, when you add issue you can choose the current milestone or create a new one.

## Workflow

### Overview

![](https://user-images.githubusercontent.com/7302777/76073858-fea83a80-5fa2-11ea-8661-ce6bf2176456.png)

Basically, we have to maintain 5 types of branches:

- `master`: Stable, direct to production.
- `develop`: Unstable, all feature changes will be pushed here. Feature, refactor, and bug fix branches are created from `develop`. When a feature, refactor, or fix is complete it is merged into `develop`.
- `feature`: Check out from `develop` branch, and push changes back to it.
- `hotfix`:  If an issue in `master` is detected a hotfix branch is created from `master`. Once the hotfix is complete it is merged to both `master` and `develop`.
- `release`: Semi-stable, ready to release, following with a few bugfixes. Checkout from `develop` and push to both `master` and `develop` if it's done.

All branches should follow the syntax of `{type}/{details}` where `{type}` is the type of branch (`hotfix`, `release`, or one of the [commit types](#commit-message-format)) and `{details}` is a few hyphen separated words explaining the branch

### Master and Develop Branches

#### Master Branch

Branches created from `master`:

The following branch should be merged back to **both** `master` and `develop`:

- A `hotfix` branch (e.g. `hotfix/style-changes`): a bug fix that is fixing an issue with a published release

A `hotfix` branch should be the **only** branch that is created from `master`.

#### Develop Branch

Branches created from `develop`:

The following branches should be merged back to `develop`:

1. A feature branch (e.g. `feature/oauth2-support`): an addition to the API that is not a bug fix or regression fix
1. A bug fix branch (e.g. `fix/tab-color`): a bug fix that is not fixing a regression or issue with a published release
1. All other types listed in the [commit message types](#commit-message-format)

The following branch should be merged back to **both** `master` and `develop`:

1. A `release` branch (e.g. `release/0.1.x`): contains all fixes and (optionally) features that are tested and should go into the release


### Feature Branches

Each new feature should reside in its own branch, based on the `develop` branch. When a feature is complete, it should be merged back into `develop`. Features should never interact directly with `master`.


### Release Branches

Once `develop` has acquired enough features for a release (or a predetermined release date is approaching), fork a `release` branch off of `develop`. Creating this branch starts the next release cycle, so no new features can be added after this point - only bug fixes, documentation generation, changelog, and other release-oriented tasks should go in this branch.

Once the `release` is ready, it will get merged into `master` and `develop`, then the `release` branch will be deleted. It’s important to merge back into `develop` because critical updates may have been added to the release branch and they need to be accessible to new features. This should be done in a pull request after review. A pull request adding a feature should be approved by one team member.

### Hotfix Branches

Maintenance or “hotfix” branches are used to quickly patch production releases. This is the only branch that should fork directly off of `master`. As soon as the fix is complete, it should be merged into both `master` and `develop` (or the current release branch).

### Examples

#### Making a Change

1. Create a branch from `develop`.
1. Make changes. Limit your changes to a "unit of work", meaning don't include irrelevant changes that may confuse and delay the change.
1. Push changes.
1. Create a PR with the base of `develop` or just merge into `develop`.


#### Updating from `develop`

1. Pull the latest changes locally.
1. Merge the changes, fixing any conflicts.
1. Push the merged changes.


#### Hotfixes

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

### Commit Message Format

We follow the [Conventional Commits specification](https://www.conventionalcommits.org/). A commit message consists of a **header**, **body** and **footer**.  The header has a **type**, **scope** and **subject**:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

The **header** is mandatory and the **scope** of the header is optional.

You can use free [tools](https://www.npmjs.com/package/commitizen) to generate a commit message.


## Releasing

1. Create the release branch from `develop`, for example: `release/1.5.0`.

1. Verify all tests are passing, fix any bugs if needed and make sure no undesired commits are in.

1. Create pull request from the `release` branch into `master` branch.

1. Click **Squash and merge**. Use the dropdown to select this option if necessary.

    <img width="192" alt="Squash and merge button" src="https://user-images.githubusercontent.com/236501/47031620-da418900-d135-11e8-91ff-e84f2478b2b3.png">

1. Confirm squash and merge into `master`.
1. Merge `release` into `develop`.

### Tags

A Git tag is similar to a Git reference, but the Git commit that it points to never changes. Git tags are helpful when you want to point to specific releases. 

You should create tags after each release or hotfix.

Tag name should follow the syntax of `v{major}.{minor}.{patch}`, e.g. `v1.5.0`

For `major` or `minor` releases, create a version based off core changes or a new features. This version should be created after merge `release` branch into `master`.

For `patch` releases, create a version after merge `hotfix` branch into `master`.

### Changelog

Update the changelog for each release or hotfix. We use changelog structure described in [keep a changelog](https://keepachangelog.com/en/1.0.0/)
