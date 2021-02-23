# Releasing

1. Create the release branch from `develop`, for example: `release/1.5.0`.

1. Verify all tests are passing, fix any bugs if needed and make sure no undesired commits are in.

1. Create pull request from the `release` branch into `master` branch.

1. Click **Squash and merge**. Use the dropdown to select this option if necessary.

    <img width="192" alt="Squash and merge button" src="https://user-images.githubusercontent.com/236501/47031620-da418900-d135-11e8-91ff-e84f2478b2b3.png">

1. Confirm squash and merge into `master`.
1. Merge `release` into `develop`.

## Tags

A Git tag is similar to a Git reference, but the Git commit that it points to never changes. Git tags are helpful when you want to point to specific releases. 

You should create tags after each release or hotfix.

Tag name should follow the syntax of `v{major}.{minor}.{patch}`, e.g. `v1.5.0`

For `major` or `minor` releases, create a version based off core changes or a new features. This version should be created after merge `release` branch into `master`.

For `patch` releases, create a version after merge `hotfix` branch into `master`.

## Changelog

Update the changelog for each release or hotfix. We use changelog structure described in [keep a changelog](https://keepachangelog.com/en/1.0.0/)
