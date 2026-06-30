# Contributing to Enterprise Integration Hub

First off, thank you for considering contributing to the Enterprise Integration Hub! It's people like you that make open source such a great community.

## 1. Code of Conduct
By participating in this project, you are expected to uphold our [Code of Conduct](CODE_OF_CONDUCT.md).

## 2. Branching Strategy
We use Git Flow:
- `main`: Production-ready code.
- `develop`: Integration branch for features.
- `feature/*`: New features and integrations.
- `bugfix/*`: Fixes for identified issues.

## 3. Commit Convention
We strictly follow [Conventional Commits](https://www.conventionalcommits.org/):
- `feat:` A new feature
- `fix:` A bug fix
- `docs:` Documentation only changes
- `style:` Changes that do not affect the meaning of the code
- `refactor:` A code change that neither fixes a bug nor adds a feature
- `test:` Adding missing tests or correcting existing tests
- `chore:` Changes to the build process or auxiliary tools

## 4. Pull Request Process
1. Ensure your branch is rebased against `develop`.
2. Ensure your code follows the coding standards outlined in `docs/architecture/coding_standards.md` (to be created).
3. Ensure CI checks (GitHub Actions) pass.
4. Request review from a maintainer.
