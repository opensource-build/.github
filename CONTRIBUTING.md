<div align="center">

# 🙌 Contributing to opensource-build

<img src="https://raw.githubusercontent.com/opensource-build/.github/main/profile/assets/marquee.svg" alt="All repositories are open source" width="100%" />

<br/>

<img src="https://img.shields.io/badge/🤝_Contributions-Welcome-3DDC97?style=for-the-badge&labelColor=0d1117" alt="Contributions welcome" />
<img src="https://img.shields.io/badge/📜_Commits-Conventional-00D9FF?style=for-the-badge&labelColor=0d1117" alt="Conventional commits" />
<img src="https://img.shields.io/badge/🛡️_Security-Private_Reporting-FF6B9D?style=for-the-badge&labelColor=0d1117" alt="Private security reporting" />

**Thank you for considering a contribution.**

Every level of contribution is welcome, from correcting a typo to building a new feature.

</div>

---

## 📋 Table of Contents

- [Code of Conduct](#-code-of-conduct)
- [Getting Started](#-getting-started)
- [Making Changes](#-making-changes)
- [Commit Guidelines](#-commit-guidelines)
- [Pull Request Process](#-pull-request-process)
- [Coding Standards](#-coding-standards)
- [Testing](#-testing)
- [Documentation](#-documentation)
- [Security](#-security)
- [Reporting Bugs and Requesting Features](#-reporting-bugs-and-requesting-features)
- [License](#-license)

---

## 🤝 Code of Conduct

We are committed to a welcoming, respectful, and harassment-free community for everyone.

**Expected behavior**

- Use welcoming and inclusive language.
- Respect differing opinions, viewpoints, and experiences.
- Accept constructive criticism gracefully.
- Focus on what is best for the community.
- Show empathy towards other community members.

**Unacceptable behavior**

- Sexualized language or imagery.
- Trolling, insulting or derogatory comments, and personal or political attacks.
- Public or private harassment.
- Publishing others' private information without explicit permission.
- Other conduct that could reasonably be considered inappropriate in a professional setting.

**Enforcement.** Maintainers may edit, hide, or remove comments, commits, issues, and pull requests that violate these standards, and may restrict participation. Report conduct issues using GitHub's **Report content** feature on the offending content, or open an issue that omits sensitive details and request maintainer attention.

---

## 🚀 Getting Started

### Prerequisites

- **Git** for version control.
- The toolchain required by the target repository (for example Python, Go, Node.js, or a POSIX shell). Each repository documents its own requirements in its `README.md`.
- **Docker** is optional and recommended where a repository provides container support.

### Workflow

1. **Fork** the repository on GitHub.
2. **Clone** your fork:
   ```bash
   git clone https://github.com/<your-username>/<repository>.git
   cd <repository>
   ```
3. **Add the upstream remote**:
   ```bash
   git remote add upstream https://github.com/opensource-build/<repository>.git
   git remote -v
   ```
4. **Create a branch**:
   ```bash
   git checkout -b feature/short-description
   ```

---

## ✍️ Making Changes

### Branch Naming

```
feature/add-retry-logic       # New feature
bugfix/fix-memory-leak        # Bug fix
docs/update-readme            # Documentation
refactor/simplify-parser      # Refactoring
chore/upgrade-dependencies    # Maintenance
hotfix/patch-critical-issue   # Urgent fix
```

### Keep Commits Atomic

Each commit should have a single responsibility.

```bash
# Good
git commit -m "feat: add retry logic to the fetch client"

# Bad: unrelated changes in one commit
git commit -m "add retry, fix ui bug and update docs"
```

### Keep Your Fork Updated

```bash
git fetch upstream
git rebase upstream/main
```

---

## 📝 Commit Guidelines

This organization follows [Conventional Commits](https://www.conventionalcommits.org/).

```
<type>(<scope>): <subject>

<body>

<footer>
```

| Type | Use |
|---|---|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation only |
| `style` | Formatting changes that do not affect meaning |
| `refactor` | Neither a fix nor a feature |
| `perf` | A performance improvement |
| `test` | Adding or correcting tests |
| `chore` | Build process, dependencies, or tooling |
| `ci` | CI configuration and scripts |

**Subject rules.** Use the imperative mood, do not capitalize the first letter, omit the trailing period, and keep it within 50 characters.

**Body rules.** Explain what changed and why, not how. Wrap at 72 characters and separate the body from the subject with a blank line.

**Footer.** Reference issues and declare breaking changes.

```
feat(auth): add token refresh support

Refresh tokens are rotated on each use to limit the exposure window
of a leaked credential.

Fixes #123
BREAKING CHANGE: the session response format changed
```

---

## 🔀 Pull Request Process

### Before You Open a Pull Request

- Rebase on the latest `main`.
- Run the repository's formatter, linter, and test suite (see [Coding Standards](#-coding-standards) and [Testing](#-testing)).
- Update documentation affected by the change.
- Confirm that no secrets, credentials, or personal data are included in the diff.

### Pull Request Description

Include the following:

1. 📌 **Summary.** What the change does and which problem it solves.
2. 🏷️ **Type.** Feature, fix, documentation, performance, refactor, or breaking change.
3. 🔗 **Related issues.** For example `Fixes #123`.
4. 🧪 **Testing.** What was tested and how a reviewer can reproduce it.
5. 💥 **Breaking changes.** The impact and a migration path, if any.
6. 🖼️ **Screenshots.** For user-interface changes, before and after.

### Review

1. Automated checks run where the repository defines them.
2. A maintainer reviews functionality, quality, documentation, and performance.
3. Address feedback with follow-up commits on the same branch.
4. At least one maintainer approval is required before merging. Maintainers may squash on merge.

---

## 🎯 Coding Standards

Repositories span several languages. Follow the conventions of the language in use and the existing style of the repository. When a repository defines its own configuration, that configuration takes precedence.

| Language | Formatter | Linter | Notes |
|---|---|---|---|
| 🐍 **Python** | `black` or `ruff format` | `ruff` or `flake8` | PEP 8, type hints on public APIs. |
| 🐹 **Go** | `gofmt` | `golangci-lint` | Handle every returned error. |
| 🟩 **Node.js / TypeScript** | `prettier` | `eslint` | Prefer TypeScript for new code. |
| 🐚 **Shell** | `shfmt` | `shellcheck` | Use `set -euo pipefail` and quote all expansions. |

### General Principles

- **Modular and DRY.** Keep functions small and single-purpose. Extract repeated logic.
- **Fail loudly.** Report errors directly and concisely. Do not swallow exceptions.
- **No secrets in code.** Use environment variables or a secrets manager.
- **Naming.** Use descriptive names. Follow the idiomatic casing of the language.

### Code Comments

- Write in formal, concise English. Do not use emojis or conversational filler.
- Explain **why** (architecture decisions, edge cases), not the obvious **what**.
- Document public functions with the language's standard format (docstrings, GoDoc, JSDoc, or a header comment).
- Use inline comments only for complex or non-obvious logic.

```python
def backoff_delay(attempt: int) -> float:
    """Return the retry delay in seconds for the given attempt.

    The delay doubles per attempt and is capped to bound worst-case latency.
    """
    # Jitter prevents synchronized retries from many clients at once.
    return min(2 ** attempt, 60) * random.uniform(0.8, 1.2)
```

---

## 🧪 Testing

- Add or update tests for every behavior change and bug fix.
- Keep tests deterministic and independent of external services where possible.
- Name tests after the behavior they verify.

Use the test runner native to the language, for example:

```bash
pytest -v          # Python
go test ./...      # Go
npm test           # Node.js
bats tests/        # Shell (Bats)
```

Where a repository defines a minimum coverage threshold, new code must meet it.

---

## 📚 Documentation

- Update `README.md` when installation, usage, or configuration changes.
- Document new configuration options, environment variables, and commands.
- Record user-visible changes in `CHANGELOG.md` where the repository maintains one.
- Prefer examples that can be copied and run.

---

## 🛡️ Security

**Do not report vulnerabilities in public issues, discussions, or pull requests.**

Use GitHub **Private Vulnerability Reporting**:

1. Open the affected repository.
2. Select the **Security** tab.
3. Select **Report a vulnerability** and describe the issue, the affected version, and steps to reproduce.

Do not include real credentials or personal data in a report. Maintainers will acknowledge the report, assess it, and coordinate a fix and disclosure through the same private advisory.

---

## 🐞 Reporting Bugs and Requesting Features

Open an issue in the relevant repository after searching existing issues for duplicates.

**Bug report**

- 📝 Description of the problem.
- ✅ Expected behavior and ❌ actual behavior.
- 🔁 Minimal steps to reproduce.
- 🖥️ Environment: operating system, tool and runtime versions.
- 📎 Relevant logs, with sensitive values removed.

**Feature request**

- 🎯 The use case and the problem to be solved.
- 💡 The proposed solution.
- 🔀 Alternatives considered.

---

## ⚖️ License

Licenses are declared per repository in the `LICENSE` file at the repository root and may differ between projects. Newer repositories use the [MIT License](https://opensource.org/license/mit). By contributing to a repository, you agree that your contribution is licensed under that repository's license.

---

<div align="center">

## 🚀 Ready to Contribute?

**Fork** ➜ **Branch** ➜ **Commit** ➜ **Test** ➜ **Pull Request**

<sub>🔓 Open by default. Built in the open.</sub>

<br/>

<a href="https://github.com/opensource-build"><img src="https://img.shields.io/badge/github.com%2Fopensource--build-0d1117?style=for-the-badge&logo=github&logoColor=white" alt="github.com/opensource-build" /></a>

</div>
