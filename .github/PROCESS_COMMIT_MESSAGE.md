# Commit Message Guidelines

This project adheres to the [Conventional Commits](https://www.conventionalcommits.org/) standard to create meaningful and standardized commit messages. This leads to more readable histories and more intuitive release notes.

## Structure of a Commit Message
A commit message consists of a **header**, **body** (optional), and **footer** (optional). The header has a special format that includes a **type**, an optional **scope**, and a **description**:
```
<type>(<scope>): <description>

<body>

<footer>
```

## Type
Type must be one of the following:

* **fix**: A bug fix
* **feat**: A new feature
* **chore**: Regular code maintenance tasks
* **docs**: Documentation only changes
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **perf**: A code change that improves performance
* **test**: Adding missing or correcting existing tests

## Scope

Scope is optional and can be anything specifying the place of the commit change. For example **auth**, **model**, **view**, **controller**, etc.

## Description

The description is a short description of the change. It should be:

* written in lower case
* a succinct summary of the change, not exceeding 50 characters
* not ending with a period

## Body

The body is optional. When present, it should include a more detailed explanation of the change. You can also include rationale and context here. Each paragraph in the body should be separated by a blank line.

## Footer

The footer is optional. When present, it should contain any information about **Breaking Changes**.

Breaking Changes should start with the word `BREAKING CHANGE:` with a space or two newlines.

Here's an example of a commit message:

```
feat(user): add reset password feature

This commit introduces a new feature that allows users to reset their password. The user will receive an email with a link that redirects to the password reset page.

BREAKING CHANGE: Updates user model to include password reset token.
```

Please ensure all your commits follow this format. This greatly helps us in maintaining the project and understanding the changes.

---

Remember, a well-formed commit message can help streamline the review process and make it much easier to track down bugs or understand why a particular change was made.
