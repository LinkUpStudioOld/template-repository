# Release Process
This document outlines our process for releasing updates to our software. These steps ensure that we maintain a high standard of quality control, while also allowing us to deliver updates to our users in a timely manner.

## Feature or Bugfix Pull Request
The first step in our release process is to create a pull request for your feature or bugfix. Please provide a detailed description of the changes in your PR. The more information you provide, the easier it is for others to understand the purpose and impact of your changes.

Remember to follow our coding standards and include any necessary tests to verify your changes. Also, consider whether your changes require updates to the documentation.

## Merging into Main Branch
After your pull request has been reviewed and approved, it will be merged into the main branch. Please ensure all tests are passing before merging your pull request.

The main branch serves as the pre-production staging area. All changes should be thoroughly tested and vetted here before they are released to production.

## Deployment to Staging
After your changes have been merged into the main branch, our CI/CD pipeline will automatically deploy them to the staging environment.

This will also create a draft release tag. This tag is used to track the changes that are included in the upcoming release. It's important to keep an eye on the staging environment to make sure everything is working as expected.

## Release and Production Deployment
The final step in the process is to publish the release. This action triggers the CI/CD pipeline to deploy the changes to the production environment.

Remember to update the release notes to describe the changes included in the release. This will help users understand what has changed and how it might affect them.
