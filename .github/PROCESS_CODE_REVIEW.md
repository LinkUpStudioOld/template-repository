# Code review process

## How to Prepare Code for Review:
- Keep the Pull Request small and specific to one issue
- Ensure PR has a clear title and description
- Connect PR to the related issue(s)
- Ensure PR is not too big (preferably between 200-400 lines of code)
- Remove any commented or unused code
- Follow best practices and coding standards
- Ensure all automated checks have passed and there are no merge conflicts
- Provide a recorded demo or clear instructions on how the code was tested
- Add unit or integration tests in the same PR if possible

## What NOT to do:
- Do not try to fix more than one issue in one PR
- Do not create PRs with empty descriptions or no tests/demo
- Do not start reviewing a PR with a broken build or failed tests
- Do not do shallow “cosmetic” reviews, only paying attention to code style
- Do not review for more than 60 minutes at a time
- Do not request changes only because of personal preferences
- Avoid only negative comments
- Do not take reviewer comments personally

## When and How to Review Code:
- Ensure the PR is marked as ready for review, all automated checks have passed, and you're assigned as a reviewer
- Use Code Review Checklist for thorough reviews

## Bad vs Good Comments:
- Always be respectful and kind
- Explain your reasoning
- Encourage developers to simplify code or add comments

## When and Who Should Merge the Code:
- The team lead should decide when a PR is ready to be merged
- Do not merge until all found bugs are fixed, all discussions are solved, and all tests/build failures are fixed
- If a merged PR causes failures in the dev or main branch, the developer who merged is responsible for fixing it ASAP
