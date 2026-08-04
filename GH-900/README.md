# GH-900 GitHub Foundations - One-Day Crash Study Guide

**Exam:** GH-900: GitHub Foundations  
**Purpose:** Exam-focused study material for last-day preparation. This guide is organized by official exam domains and uses a repeatable structure: definition, description, examples, syntax, exam tips, traps, and scenarios.

---

## Index

- [0. Exam Quick Facts](#0-exam-quick-facts)
- [1. How to Use This Guide in One Day](#1-how-to-use-this-guide-in-one-day)
- [2. Official Exam Domains and Weighting](#2-official-exam-domains-and-weighting)
- [Domain 1 - Understand Git and GitHub Basics](#domain-1---understand-git-and-github-basics)
  - [1.1 Version Control](#11-version-control)
  - [1.2 Git vs GitHub](#12-git-vs-github)
  - [1.3 Core Git Concepts](#13-core-git-concepts)
  - [1.4 GitHub Accounts, Organizations, and Enterprise Options](#14-github-accounts-organizations-and-enterprise-options)
  - [1.5 GitHub Flow](#15-github-flow)
  - [1.6 Markdown](#16-markdown)
  - [1.7 GitHub Desktop, GitHub Mobile, github.dev, and Codespaces](#17-github-desktop-github-mobile-githubdev-and-codespaces)
- [Domain 2 - Work with GitHub Repositories](#domain-2---work-with-github-repositories)
  - [2.1 Repository Structure](#21-repository-structure)
  - [2.2 Key Repository Files](#22-key-repository-files)
  - [2.3 Add and Manage Repository Files](#23-add-and-manage-repository-files)
  - [2.4 Repository Templates, Branches, Topics, Stars, and Archive](#24-repository-templates-branches-topics-stars-and-archive)
  - [2.5 Repository Insights, Metrics, Feature Previews, and Dependency Insights](#25-repository-insights-metrics-feature-previews-and-dependency-insights)
- [Domain 3 - Collaborate Using GitHub](#domain-3---collaborate-using-github)
  - [3.1 Issues](#31-issues)
  - [3.2 Pull Requests](#32-pull-requests)
  - [3.3 Discussions](#33-discussions)
  - [3.4 Templates, Filters, Assignments, Labels, and Milestones](#34-templates-filters-assignments-labels-and-milestones)
  - [3.5 Notifications](#35-notifications)
  - [3.6 Gists, Wikis, and GitHub Pages](#36-gists-wikis-and-github-pages)
- [Domain 4 - Apply Modern Development Practices](#domain-4---apply-modern-development-practices)
  - [4.1 GitHub Actions](#41-github-actions)
  - [4.2 GitHub Actions Syntax](#42-github-actions-syntax)
  - [4.3 Runners, Jobs, Steps, Actions, Matrix, and Secrets](#43-runners-jobs-steps-actions-matrix-and-secrets)
  - [4.4 GitHub Copilot](#44-github-copilot)
  - [4.5 Copilot Plans](#45-copilot-plans)
  - [4.6 GitHub Codespaces and Dev Containers](#46-github-codespaces-and-dev-containers)
  - [4.7 github.dev vs Codespaces](#47-githubdev-vs-codespaces)
- [Domain 5 - Manage Projects with GitHub](#domain-5---manage-projects-with-github)
  - [5.1 GitHub Projects](#51-github-projects)
  - [5.2 Project Layouts](#52-project-layouts)
  - [5.3 Project Configuration](#53-project-configuration)
  - [5.4 Labels, Milestones, Assignees, and Saved Replies](#54-labels-milestones-assignees-and-saved-replies)
  - [5.5 Project Workflows and Insights](#55-project-workflows-and-insights)
- [Domain 6 - Understand Privacy, Security, and Administration](#domain-6---understand-privacy-security-and-administration)
  - [6.1 Account Security](#61-account-security)
  - [6.2 Repository Visibility](#62-repository-visibility)
  - [6.3 Repository Roles](#63-repository-roles)
  - [6.4 Organization Settings, Teams, Roles, and Outside Collaborators](#64-organization-settings-teams-roles-and-outside-collaborators)
  - [6.5 Branch Protection and Repository Rulesets](#65-branch-protection-and-repository-rulesets)
  - [6.6 Enterprise Managed Users and Copilot Policy](#66-enterprise-managed-users-and-copilot-policy)
- [Domain 7 - Explore the GitHub Community](#domain-7---explore-the-github-community)
  - [7.1 Open Source](#71-open-source)
  - [7.2 GitHub Sponsors](#72-github-sponsors)
  - [7.3 Following Users and Organizations](#73-following-users-and-organizations)
  - [7.4 GitHub Marketplace](#74-github-marketplace)
  - [7.5 Forks, Templates, and Discoverable Repositories](#75-forks-templates-and-discoverable-repositories)
  - [7.6 InnerSource](#76-innersource)
- [Final Exam Revision](#final-exam-revision)
  - [A. Master Decision Matrix](#a-master-decision-matrix)
  - [B. Must-Memorize Facts](#b-must-memorize-facts)
  - [C. Common Exam Traps](#c-common-exam-traps)
  - [D. Scenario Practice Questions](#d-scenario-practice-questions)
  - [E. Two-Hour Final Revision Checklist](#e-two-hour-final-revision-checklist)
  - [F. Seven-Day Revision Plan](#f-seven-day-revision-plan)

---

## 0. Exam Quick Facts

- **Exam name:** GitHub Foundations
- **Exam code:** GH-900
- **Level:** Beginner
- **Product:** GitHub
- **Duration:** 100 minutes
- **Passing score:** 700 or greater
- **Audience:** GitHub users, non-developers, developers, administrators, DevOps engineers, app makers, and solution architects who need foundational GitHub knowledge
- **Question style:** Mostly conceptual and scenario-based
- **Exam mindset:** Identify the keyword in the requirement, then map it to the correct GitHub feature

---

## 1. How to Use This Guide in One Day

### If You Have 8 Hours

1. Read the domain summaries and decision tables.
2. Focus deeply on Domains 1, 2, 3, 4, and 6 because they carry more weight.
3. Practice the scenario questions.
4. Revise the Master Decision Matrix.
5. Review Common Exam Traps before the exam.

### If You Have 4 Hours

1. Read the official domain weighting.
2. Study Git vs GitHub, clone vs fork vs branch vs template, Issues vs PRs vs Discussions.
3. Study repository files, repository roles, branch protection, Actions, Copilot, Codespaces, and Projects.
4. Complete the Two-Hour Final Revision Checklist.

### If You Have 2 Hours

1. Read the Master Decision Matrix.
2. Read Common Exam Traps.
3. Attempt the Scenario Practice Questions.
4. Review syntax examples: Git commands, Markdown, Actions YAML, CODEOWNERS, devcontainer, Dependabot.

---

## 2. Official Exam Domains and Weighting

| Domain | Weight | What to Master |
|---|---:|---|
| Understand Git and GitHub basics | 25-30% | Git vs GitHub, version control, repositories, commits, branches, GitHub Flow, Markdown, GitHub Desktop, GitHub Mobile |
| Work with GitHub repositories | 10-15% | Repository files, README, LICENSE, CONTRIBUTING, CODEOWNERS, SECURITY, templates, branches, insights, stars, metrics dashboards, dependency insights |
| Collaborate using GitHub | 10-15% | Issues, pull requests, discussions, templates, filters, assignments, notifications, Gists, Wikis, GitHub Pages |
| Apply modern development practices | 10-15% | GitHub Actions, workflows, jobs, runners, Copilot, Copilot agents, Agent Mode, multi-model support, Codespaces, dev containers, github.dev |
| Manage projects with GitHub | 5-10% | GitHub Projects, table/board/roadmap layouts, labels, milestones, workflows, saved replies, assignees, insights |
| Understand privacy, security, and administration | 10-15% | 2FA, passkeys, roles, teams, permissions, EMUs, Copilot policy, visibility, branch protection, organization settings |
| Explore the GitHub community | 5-10% | Open source, Sponsors, following users/orgs, Marketplace, InnerSource, forks, templates, discoverability |

---

# Domain 1 - Understand Git and GitHub Basics

## 1.1 Version Control

### Definition

Version control is a system that tracks changes to files over time so users can view history, compare differences, collaborate safely, and revert mistakes.

### Description

Version control is important because software, documentation, infrastructure code, and configuration files change frequently. Git keeps a record of changes through commits. GitHub builds collaboration features on top of Git repositories.

### Example

A team updates a website. One developer changes the homepage, another updates the README, and another fixes a bug. Version control tracks who changed what, when, and why.

### Exam Tips

- If the requirement says **track history**, **compare changes**, or **revert mistakes**, think **version control**.
- If the requirement says **work offline and commit locally**, think **Git**.
- If the requirement says **collaborate online with pull requests, issues, and reviews**, think **GitHub**.

### Exam Trap

Git and GitHub are related, but they are not the same. Git is the version control system. GitHub is a cloud platform for hosting Git repositories and collaboration.

---

## 1.2 Git vs GitHub

### Definition

- **Git:** Distributed version control tool used to track source history.
- **GitHub:** Cloud-based platform for hosting Git repositories and enabling collaboration.

### Decision Table

| Scenario | Best Answer | Why |
|---|---|---|
| Need local version control on a laptop | Git | Git manages local repository history |
| Need to commit while offline | Git | Commits are local until pushed |
| Need hosted repository, issues, PRs, reviews | GitHub | GitHub provides cloud collaboration |
| Need CI/CD on pull request | GitHub Actions | Actions automates workflows on GitHub |
| Need discussions, community, or project planning | GitHub | GitHub includes collaboration and community features |

### Example

A developer uses Git commands locally, then pushes commits to GitHub so the team can review the work in a pull request.

### Exam Tip

When the question says **tool**, **command**, **local commit**, or **distributed version control**, the answer is usually Git. When it says **platform**, **collaboration**, **issues**, **pull requests**, or **Actions**, the answer is usually GitHub.

---

## 1.3 Core Git Concepts

### Definitions

| Concept | Definition | Exam Clue |
|---|---|---|
| Repository | Storage location for project files and history | Need a place to store code/docs/configuration |
| Commit | Snapshot of staged changes with metadata and message | Need record of what changed and why |
| Branch | Independent line of development | Need isolate feature/fix work from main |
| Merge | Combine changes from one branch into another | Need bring reviewed work into main |
| Clone | Local copy of a repository with history | Need work locally |
| Fork | GitHub-hosted copy under your account | Need contribute without write access |
| Pull | Fetch and integrate remote changes locally | Need update local branch |
| Push | Upload local commits to remote | Need publish work to GitHub |
| Remote | Hosted copy of repository, commonly on GitHub | Need sync local and hosted repo |
| Working tree | Local files you are editing | Need understand current file changes |
| Staging area | Area where changes are selected before commit | Need prepare selected files for commit |

### Core Git Command Syntax

```bash
git clone https://github.com/org/repo.git
git status
git checkout -b feature/add-login
git add README.md
git commit -m "Update README with setup steps"
git push origin feature/add-login
git pull origin main
git merge feature/add-login
```

### Command Purpose

| Command | Purpose | Use When |
|---|---|---|
| git clone | Copy remote repository locally | Starting work on an existing repo |
| git status | Show changed/staged files | Checking current local state |
| git add | Stage changes | Preparing selected changes for commit |
| git commit | Save staged snapshot locally | Recording a meaningful unit of change |
| git branch | List/create branches | Working on isolated changes |
| git checkout / switch | Move between branches | Changing active workstream |
| git push | Upload commits to remote | Sharing your branch on GitHub |
| git pull | Bring remote changes locally | Updating local branch |
| git merge | Combine branch history | Integrating changes |

### Branch vs Fork vs Clone vs Template

| Requirement | Best Answer | Why |
|---|---|---|
| Work locally on an existing repository | Clone | Creates a local copy |
| Work on a feature without affecting main | Branch | Creates an isolated line of work |
| Contribute without write access | Fork | Creates your GitHub-hosted copy |
| Start a new repo from a standard structure | Template | Creates a new independent repository |
| Bookmark or show interest | Star | Saves or signals interest |

### Exam Trap

- Clone is local.
- Fork is server-side under your GitHub account.
- Branch is an isolated development line in a repository.
- Template is for starting a new independent repository from a standard pattern.

---

## 1.4 GitHub Accounts, Organizations, and Enterprise Options

### Definitions

| Option | Description | Best For |
|---|---|---|
| Personal account | Individual GitHub identity | Personal projects, contributions, learning |
| Organization | Shared account for teams and projects | Team repositories, teams, centralized permissions |
| Enterprise account | Top-level account for multiple organizations | Large companies needing centralized policy, billing, security, and governance |
| Enterprise Managed Users | Enterprise-controlled GitHub user accounts | Strict identity lifecycle and enterprise-owned accounts |

### Decision Tree

```text
Need one person's projects?
-> Personal account

Need shared team repositories and permissions?
-> Organization

Need centralized control across many organizations?
-> Enterprise account

Need enterprise-owned developer identities?
-> Enterprise Managed Users
```

### Exam Tip

If the question says **central governance across multiple organizations**, choose enterprise account. If it says **enterprise-owned identities and lifecycle**, choose Enterprise Managed Users.

---

## 1.5 GitHub Flow

### Definition

GitHub Flow is a lightweight branch-based collaboration workflow where changes are developed on a branch, reviewed through a pull request, and merged into the main branch.

### Steps

1. Create a branch from main.
2. Add commits to the branch.
3. Open a pull request.
4. Discuss and review changes.
5. Run checks and resolve issues.
6. Merge into main.
7. Deploy from main if that is the project strategy.

### Syntax Example

```bash
git checkout main
git pull origin main
git checkout -b feature/update-docs
# edit files
git add .
git commit -m "Update docs for onboarding"
git push origin feature/update-docs
# open pull request on GitHub
```

### Scenario Mapping

| Scenario | Best GitHub Flow Action |
|---|---|
| Need isolate work from stable main branch | Create a branch |
| Need ask others to review proposed changes | Open a pull request |
| Need discuss a change before merge | Use PR comments/review |
| Need automatically validate changes | Configure required checks / GitHub Actions |
| Need enforce review before merging | Branch protection or ruleset |

### Exam Tip

GitHub Flow is pull-request based and lightweight. Do not confuse it with Git Flow, which uses long-lived develop and release branches.

---

## 1.6 Markdown

### Definition

Markdown is a lightweight markup language used in GitHub to format README files, issues, pull requests, discussions, comments, and documentation.

### Common Syntax

```markdown
# Heading

## Subheading

- Bullet item
- [ ] Task item
- [x] Completed task

**Bold text**
`inline code`

```text
code block
```

[Link text](https://example.com)
![Alt text](image.png)

> Quoted note
```

### Markdown Use Cases

| Requirement | Best Answer |
|---|---|
| Create project landing page | README.md |
| Add checklist in an issue | Markdown task list |
| Explain contribution steps | CONTRIBUTING.md |
| Format commands clearly | Code block |
| Link related PR or issue | Markdown link or GitHub auto-link |

### Exam Tip

If the question focuses on clear communication in issues and pull requests, Markdown is likely relevant.

---

## 1.7 GitHub Desktop, GitHub Mobile, github.dev, and Codespaces

### Definitions

| Tool | What It Is | Best For | Not Best For |
|---|---|---|---|
| GitHub Desktop | Desktop GUI for Git and GitHub workflows | Beginners, visual commit/branch/PR flow | Full cloud dev environment |
| GitHub Mobile | Mobile app for notifications and collaboration | Review, triage, comment on the go | Heavy coding |
| github.dev | Lightweight browser editor | Quick edits in browser without compute | Running/building server-side apps |
| GitHub Codespaces | Cloud development environment | Full development, terminal, dependencies, dev containers | Simple one-line doc edit |

### Exam Tip

- Quick browser edit: github.dev or GitHub web editor.
- Full cloud dev environment: Codespaces.
- Visual local Git workflow: GitHub Desktop.
- Triage on phone: GitHub Mobile.

---

# Domain 2 - Work with GitHub Repositories

## 2.1 Repository Structure

### Definition

A GitHub repository stores project files, history, branches, issues, pull requests, settings, security configuration, and collaboration metadata.

### Description

Repositories can contain source code, documentation, workflows, templates, configuration files, and community health files.

### Example Repository Structure

```text
repo-name/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── SECURITY.md
├── CODEOWNERS
├── .gitignore
├── .github/
│   ├── workflows/
│   │   └── ci.yml
│   ├── ISSUE_TEMPLATE/
│   └── PULL_REQUEST_TEMPLATE.md
├── docs/
├── src/
└── tests/
```

### Exam Tip

If the question asks about a project landing page, legal reuse, contribution process, security reporting, or automatic review assignment, it is usually testing repository files.

---

## 2.2 Key Repository Files

### File Selection Table

| File | Definition / Purpose | Exam Clue |
|---|---|---|
| README.md | Project overview, setup, usage, badges, links | New user needs to understand project quickly |
| LICENSE | Defines legal permissions for using, modifying, distributing project | Need clarify reuse rights |
| CONTRIBUTING.md | Explains how to contribute | New contributors need process guidance |
| CODEOWNERS | Defines reviewers responsible for files/paths | Need automatic review requests from owners |
| SECURITY.md | Explains security reporting policy | Need responsible vulnerability disclosure |
| .gitignore | Files Git should ignore | Need exclude build output, secrets, local config |
| SUPPORT.md | Support channels and expectations | Need direct users to help resources |
| ISSUE_TEMPLATE | Standardizes issue creation | Need consistent bug/feature information |
| PULL_REQUEST_TEMPLATE | Standardizes PR details | Need checklist and context for reviewers |
| .github/workflows/*.yml | GitHub Actions workflows | Need automation |

### .gitignore Example

```gitignore
# Build output
dist/
build/

# Dependencies
node_modules/

# Environment and secrets
.env
*.local

# OS/editor files
.DS_Store
.vscode/settings.json
```

### CODEOWNERS Example

```text
# Global owner
* @org/core-maintainers

# Documentation owners
/docs/ @org/docs-team

# Security-sensitive areas
/security/ @org/security-team
```

### Exam Traps

- README is not a license.
- LICENSE is not contribution guidance.
- CONTRIBUTING is not CODEOWNERS.
- SECURITY.md is not secret scanning.
- .gitignore does not remove files already committed.
- CODEOWNERS may require branch protection/ruleset configuration to enforce required owner review.

---

## 2.3 Add and Manage Repository Files

### Definition

Managing files in a repository means creating, editing, uploading, deleting, renaming, committing, and reviewing files through GitHub web UI, github.dev, GitHub Desktop, Codespaces, or Git commands.

### Common Actions

- Add a file directly in GitHub web UI.
- Edit an existing file and commit changes.
- Upload files from a local machine.
- Delete or rename files.
- Commit directly to a branch or create a new branch and pull request.
- Use Git locally for larger changes.
- Use github.dev for lightweight browser editing.
- Use Codespaces when edits require runtime, terminal, dependencies, or build/test execution.

### Git Command Example

```bash
git checkout -b docs/update-readme
echo "# Project Guide" > GUIDE.md
git add GUIDE.md
git commit -m "Add project guide"
git push origin docs/update-readme
```

### Exam Tips

- Small browser edit: GitHub web editor or github.dev.
- Full local workflow: Git commands or GitHub Desktop.
- Change needs review: branch plus pull request.
- Needs terminal/dependencies/build: Codespaces or local environment.

---

## 2.4 Repository Templates, Branches, Topics, Stars, and Archive

### Definitions

| Feature | Definition | Use When |
|---|---|---|
| New repository | New project container | Starting a new project |
| Repository template | Create new repos from predefined structure | Standardize starter projects |
| Branch | Parallel development line | Feature/fix isolation |
| Default branch | Main branch used for default view and PR base | Usually main |
| Protected branch / ruleset | Enforces workflow requirements | Require PR review, checks, restrictions |
| Archive repository | Make repository read-only | Project is no longer maintained |
| Topics | Tags describing repository | Improve discoverability |
| Stars | Bookmark/recommend repository | Track popular or useful repos |

### Repository Maintenance Best Practices

- Keep README accurate and beginner-friendly.
- Add a LICENSE if the repository is intended for public reuse.
- Use issue and PR templates for consistency.
- Use CODEOWNERS for ownership clarity.
- Protect important branches.
- Avoid committing secrets.
- Use dependency insights and Dependabot where appropriate.
- Archive inactive repositories instead of deleting if history should remain visible.

### Exam Tip

If the project should become read-only while preserving history, choose archive repository.

---

## 2.5 Repository Insights, Metrics, Feature Previews, and Dependency Insights

### Definitions

| Feature | What It Shows | Use Case |
|---|---|---|
| Pulse | Recent repository activity | Quick health/activity check |
| Contributors | Contribution activity by people | Understand who contributed |
| Community standards | README, code of conduct, contributing, license, security files | Improve open-source readiness |
| Traffic | Views and clones | Measure repository interest |
| Stars | Users interested in repository | Popularity/bookmark signal |
| Forks | Copies made by users | Contribution/experimentation signal |
| Dependency graph | Dependencies used by the project | Understand dependency relationships |
| Dependency insights | Dependency health and visibility | Improve dependency management |
| Security insights | Vulnerabilities and alerts where enabled | Improve security posture |
| Repository metrics dashboards | Activity, trends, progress, and health indicators | Understand engagement and repository health |
| Feature previews | Ability to try newer GitHub features | Evaluate upcoming or newly available capabilities |

### Dependabot Configuration Example

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
```

### Exam Tip

If the question mentions repository activity, traffic, contributors, dependency visibility, health, or engagement, look for repository insights, metrics, dependency graph, or dependency insights.

---

# Domain 3 - Collaborate Using GitHub

## 3.1 Issues

### Definition

An issue is a GitHub work item used to track bugs, tasks, feature requests, ideas, or discussions around specific work.

### Description

Issues support labels, assignees, milestones, comments, templates, links to pull requests, and project tracking.

### Example

A tester finds a login bug and creates an issue with reproduction steps, expected behavior, actual behavior, browser version, and screenshots.

### Issue Template Example

```markdown
## Description
Explain the issue or request.

## Steps to reproduce
1.
2.
3.

## Expected behavior

## Actual behavior

## Additional context
```

### Exam Tips

- Bug/task/feature tracking: Issue.
- Need standardized bug report: Issue template.
- Need categorize issue: Label.
- Need assign responsibility: Assignee.
- Need group for release: Milestone.

---

## 3.2 Pull Requests

### Definition

A pull request proposes changes from one branch into another and supports review, comments, checks, and merge.

### Description

Pull requests are central to GitHub collaboration. They allow contributors to explain changes, request reviews, run automated checks, discuss feedback, and merge only after the required criteria are met.

### Example

A developer creates a branch, commits a bug fix, pushes the branch, opens a pull request, links the issue, passes CI checks, gets approval, and merges into main.

### Pull Request Template Example

```markdown
## Summary
Describe the change.

## Testing
- [ ] Unit tests pass
- [ ] Manual validation completed

## Linked issue
Fixes #123
```

### Issue-to-PR Linking Keywords

```text
Fixes #123
Closes #123
Resolves #123
Related to #123
```

### Meaning

| Wording | Effect |
|---|---|
| Fixes #123 | Links PR and can close issue when PR merges |
| Closes #123 | Links PR and can close issue when PR merges |
| Resolves #123 | Links PR and can close issue when PR merges |
| Related to #123 | Links but does not automatically close |

### Pull Request Merge Options

| Option | Description | Use When |
|---|---|---|
| Merge commit | Preserves branch history with a merge commit | Need explicit merge record |
| Squash merge | Combines PR commits into one commit | Need clean main history |
| Rebase merge | Replays commits onto base branch | Need linear history |

### Exam Tip

If the requirement says **propose changes**, **review code**, **run checks before merge**, or **merge branch into main**, choose pull request.

### Exam Trap

A Discussion is not the right tool for reviewing and merging code changes.

---

## 3.3 Discussions

### Definition

A discussion is a GitHub collaboration feature for open-ended conversation, questions, ideas, announcements, and community engagement.

### Description

Discussions are better than issues when the topic is not a specific trackable work item. They help communities and teams collaborate without turning every conversation into a bug or task.

### Use Cases

| Requirement | Best Answer |
|---|---|
| Ask broad question | Discussion |
| Collect ideas from community | Discussion |
| Announce project updates | Discussion announcement category |
| Track bug or task | Issue |
| Review proposed code change | Pull request |

### Exam Tip

If the scenario is open-ended Q&A or community conversation, use Discussions. If it is a trackable work item, use Issues.

---

## 3.4 Templates, Filters, Assignments, Labels, and Milestones

### Definitions

| Feature | Purpose | Example |
|---|---|---|
| Issue template | Standardize issue input | Bug report template with reproduction steps |
| PR template | Standardize review context | Checklist for tests and linked issues |
| Filter | Find issues/PRs by metadata | Filter by label, assignee, author, state |
| Label | Categorize work | bug, enhancement, documentation |
| Assignee | Show responsibility | Assign issue to developer |
| Milestone | Group issues/PRs toward target | v1.0 release |

### Filter Examples

```text
is:issue is:open label:bug
is:pr is:open review-requested:@me
author:octocat label:documentation
assignee:@me milestone:"v1.0"
```

### Exam Tip

- Organize by type: label.
- Group for release: milestone.
- Assign owner: assignee.
- Search/find work: filters.

---

## 3.5 Notifications

### Definition

GitHub notifications help users track activity for repositories, issues, pull requests, discussions, teams, reviews, assignments, and mentions.

### Common Notification Sources

- Watching a repository.
- Being mentioned with @username or @team.
- Being assigned to an issue or pull request.
- Participating in a conversation.
- Being requested as a reviewer.
- Updates to subscribed issues, PRs, or discussions.

### Configuration Options

- Watch, unwatch, or ignore repositories.
- Subscribe or unsubscribe from specific issues, PRs, or discussions.
- Configure email, web, and mobile notification preferences.
- Filter notifications by reason such as assigned, participating, mentioned, review requested, or team mention.

### Exam Tips

- Too many alerts: adjust notification settings or watch settings.
- Need follow all repository activity: watch repository.
- Need bring someone into conversation: mention user/team.
- Need manage work on the go: GitHub Mobile.

---

## 3.6 Gists, Wikis, and GitHub Pages

### Definitions

| Feature | Description | Best For |
|---|---|---|
| Gist | Lightweight snippet or note sharing | Share small code/text snippets |
| Wiki | Repository documentation pages | Multi-page docs linked to a repo |
| GitHub Pages | Static website hosting from repository | Publish docs, project site, portfolio |
| README | Repository landing page | Quick project overview |

### Decision Table

| Requirement | Best Answer |
|---|---|
| Quick project overview on repository home | README |
| Multi-page repository documentation | Wiki |
| Public static website | GitHub Pages |
| Share a short code snippet independently | Gist |

### Exam Trap

Wiki is documentation inside a repository context. GitHub Pages publishes a static website.

---

# Domain 4 - Apply Modern Development Practices

## 4.1 GitHub Actions

### Definition

GitHub Actions is GitHub's automation platform for CI/CD and repository workflows.

### Description

Actions can build, test, deploy, label issues, respond to pull request events, run scheduled jobs, and automate repository tasks.

### Core Concepts

| Concept | Definition | Exam Clue |
|---|---|---|
| Workflow | Automated process defined in YAML | Need build/test/deploy automation |
| Event | Trigger that starts a workflow | push, pull_request, schedule, manual |
| Job | Group of steps that run on the same runner | Need organize or parallelize work |
| Step | Individual command or action inside a job | Shell command or reusable action |
| Action | Reusable automation component | Avoid repeated workflow logic |
| Runner | Machine that executes jobs | GitHub-hosted or self-hosted |
| Matrix | Runs job across combinations | Test multiple OS/language versions |
| Secret | Encrypted value for workflow | Avoid hardcoding credentials |

### Exam Tip

GitHub Actions is not only CI/CD. It can also automate repository events, issue triage, pull request labeling, scheduled tasks, and release workflows.

---

## 4.2 GitHub Actions Syntax

### Basic Workflow Example

```yaml
name: Pull Request Checks

on:
  pull_request:
    branches: [ main ]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Validate
        run: echo "Run validation here"
```

### Push and Pull Request Workflow

```yaml
name: CI

on:
  pull_request:
    branches: [ main ]
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Run tests
        run: echo "Run build and test commands here"
```

### Matrix Example

```yaml
name: Matrix Test

on:
  pull_request:

jobs:
  test:
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        node: [18, 20]
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/checkout@v4
      - name: Use Node.js
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}
      - run: npm test
```

### Scenario Matrix

| Scenario | Best Answer |
|---|---|
| Run tests on every pull request | Workflow triggered by pull_request |
| Deploy after merge to main | Workflow triggered by push to main or release |
| Run nightly scan | Scheduled workflow |
| Reuse common automation across repos | Reusable workflow |
| Avoid exposing passwords in YAML | GitHub Actions secrets |
| Need specific hardware/network | Self-hosted runner |
| Need Linux/Windows/macOS hosted VM | GitHub-hosted runner |

---

## 4.3 Runners, Jobs, Steps, Actions, Matrix, and Secrets

### Definitions

| Feature | What It Means | Exam Clue |
|---|---|---|
| GitHub-hosted runner | Runner managed by GitHub | Need managed Linux/Windows/macOS environment |
| Self-hosted runner | Runner managed by your organization | Need custom hardware, software, network, or compliance |
| Job | Set of steps executed on a runner | Need organize automation |
| Step | Command or action | Need run one task |
| Action | Reusable task/plugin | Need reuse existing automation |
| Matrix | Run same job across combinations | Need test multiple OS/version combinations |
| Secret | Encrypted sensitive value | Need protect token/password/API key |

### Exam Traps

- Workflow is the automation definition.
- Event starts the workflow.
- Runner executes jobs.
- Job contains steps.
- Step runs a command or action.
- Secret is not stored directly in YAML output.

---

## 4.4 GitHub Copilot

### Definition

GitHub Copilot is an AI-powered coding assistant that helps with suggestions, explanations, debugging, refactoring, test generation, pull request assistance, command-line help, and agent-based development tasks.

### Capability Overview

| Capability | Description | Good Scenario |
|---|---|---|
| Code suggestions | AI suggestions as you type | Speed up coding in IDE |
| Copilot Chat | Ask questions about code or repo context | Explain, debug, refactor, generate tests |
| Pull request assistance | Helps generate PR descriptions/summaries | Improve review context |
| CLI assistance | Help with command-line tasks | Generate/explain shell or Git commands |
| Agent Mode / Coding Agent | Helps plan and make scoped code changes for review | Delegate scoped implementation tasks |
| Multi-model support | Supports use of different models where available | Match task to model capability, policy, or availability |

### Copilot Security Rules

- Do not paste secrets, tokens, credentials, customer data, or sensitive data into prompts.
- Review generated code before use.
- Treat AI-generated output as a draft.
- Use pull requests, testing, code review, and security scanning for generated changes.
- Use organization or enterprise Copilot policies where governance is required.

### Exam Trap

Copilot assists development. It does not remove human accountability for code review, testing, security, licensing, quality, or production readiness.

---

## 4.5 Copilot Plans

### Exam-Level Difference

| Plan | Best For | Key Idea |
|---|---|---|
| Copilot for Individuals / Pro-style plans | Individual developer productivity | Personal subscription and individual features |
| Copilot Business | Organization-managed Copilot access | Central policy and user management for organizations |
| Copilot Enterprise | Enterprise-scale Copilot with deeper GitHub integration | Enterprise governance and broader integrations |

### Exam Tip

If the scenario says **organization-wide management**, choose Copilot Business or organization policy. If it says **enterprise-scale governance**, choose Copilot Enterprise or enterprise policy.

---

## 4.6 GitHub Codespaces and Dev Containers

### Definition

GitHub Codespaces provides cloud-hosted development environments. Dev containers define a repeatable development environment as configuration.

### Codespaces Features

| Feature | Description | Exam Clue |
|---|---|---|
| Codespace | Cloud-hosted development environment | Need full dev environment without local setup |
| Dev container | Configuration-as-code for dev environment | Need repeatable tools/dependencies/settings |
| Browser or VS Code access | Connect from browser, VS Code, or CLI | Need flexible access |
| Linux container environment | Runs in a container on a VM | Need consistent Linux runtime |
| Prebuilds | Speed up startup | Large repos or slow setup |
| Secrets | Secure environment values | Need credentials safely inside codespace |

### Dev Container Example

```json
{
  "name": "GH-900 Practice Dev Container",
  "image": "mcr.microsoft.com/devcontainers/base:ubuntu",
  "features": {
    "ghcr.io/devcontainers/features/github-cli:1": {}
  },
  "customizations": {
    "vscode": {
      "extensions": ["GitHub.copilot"]
    }
  }
}
```

### Exam Tip

If the scenario asks for consistent developer setup across the team, choose dev container configuration with Codespaces.

---

## 4.7 github.dev vs Codespaces

### Decision Table

| Requirement | Best Answer | Why |
|---|---|---|
| Quick browser edit to README | github.dev | Lightweight editor, no full compute needed |
| Run app/tests/build in browser environment | Codespaces | Provides compute, terminal, dependencies |
| Standardize dev tools for team | Dev container + Codespaces | Configuration as code |
| Review small documentation change | github.dev or GitHub web editor | Fast edit pathway |
| Need full VS Code-like cloud environment | Codespaces | Full cloud development environment |

### Exam Trap

The github.dev editor does not provide the same compute/runtime as Codespaces.

---

# Domain 5 - Manage Projects with GitHub

## 5.1 GitHub Projects

### Definition

GitHub Projects is a flexible planning and tracking tool for organizing issues, pull requests, draft issues, fields, views, workflows, and progress insights.

### Description

Projects help teams manage work across repositories using table, board, and roadmap layouts. They can track custom metadata such as priority, status, size, iteration, and target date.

### Example

A team creates a GitHub Project to manage sprint work. Issues and pull requests are added to the project, assigned priorities, displayed on a board, and tracked using project insights.

### Exam Tip

If the scenario asks for cross-repository planning, visual backlog, board, roadmap, custom fields, or progress tracking, choose GitHub Projects.

---

## 5.2 Project Layouts

| Layout | Description | Use When |
|---|---|---|
| Table layout | Spreadsheet-like view | Detailed planning and metadata |
| Board layout | Kanban-style columns | Workflow/status tracking |
| Roadmap layout | Timeline planning | Time-based planning and releases |

### Exam Tip

- Kanban columns: Board layout.
- Timeline view: Roadmap layout.
- Detailed metadata view: Table layout.

---

## 5.3 Project Configuration

### Project Configuration Includes

- Selecting layout: table, board, roadmap.
- Adding custom fields such as priority, status, size, iteration, and target date.
- Adding issues, pull requests, and draft issues.
- Creating project workflows to automate item status updates.
- Using project insights to track progress.
- Saving views for different audiences or workflows.

### Draft Issues

A draft issue is a planning item inside a project that is not yet a formal repository issue.

### Exam Tip

If the requirement says early backlog planning before creating a real issue, choose draft issue in GitHub Projects.

---

## 5.4 Labels, Milestones, Assignees, and Saved Replies

### Definitions

| Feature | Purpose | Example |
|---|---|---|
| Label | Categorize work | bug, documentation, help wanted |
| Milestone | Group work toward a target | v1.0 release |
| Assignee | Assign responsibility | Person responsible for issue/PR |
| Saved reply | Reuse common response | Triage or support guidance |

### Projects vs Issues vs Milestones

| Requirement | Best Answer |
|---|---|
| Track a single bug/task | Issue |
| Group issues/PRs for a release | Milestone |
| Visualize and manage work across many items | Project |
| Add priority/effort/custom metadata | Project custom fields |
| Show roadmap timeline | Project roadmap layout |
| Show Kanban status columns | Project board layout |

### Exam Tip

Labels categorize. Milestones group toward a release or target. Projects visualize and manage work.

---

## 5.5 Project Workflows and Insights

### Definition

Project workflows automate project item updates. Project insights provide charts and visibility into progress and productivity.

### Examples

- Automatically set status to **In Progress** when an issue is assigned.
- Automatically set status to **Done** when a linked pull request is merged.
- Use charts to track completed work, remaining work, and progress over time.

### Exam Tip

If the question says **automatically update project status**, choose project workflows. If it says **track progress with charts**, choose project insights.

---

# Domain 6 - Understand Privacy, Security, and Administration

## 6.1 Account Security

### Definitions

| Feature | Description | Exam Clue |
|---|---|---|
| Two-factor authentication | Requires second factor in addition to password | Need protect account login |
| Passkeys | Passwordless or authenticator-backed sign-in | Need phishing-resistant modern sign-in |
| Personal access token | Token for API/Git operations | Need authenticate tooling without password |
| SSH key | Key-based Git authentication | Need secure Git command-line access |
| Secret scanning | Detect committed secrets where enabled | Need identify leaked credentials |

### Exam Tips

- Protect user login: 2FA or passkeys.
- Authenticate Git/API automation: PAT or SSH key depending scenario.
- Detect leaked credentials: secret scanning.
- Store workflow credentials: GitHub Actions secrets.

### Exam Trap

2FA and passkeys protect account sign-in. Branch protection protects repository workflow. They solve different problems.

---

## 6.2 Repository Visibility

### Definitions

| Visibility | Who Can See It | Use When |
|---|---|---|
| Public | Everyone | Open-source or public docs/projects |
| Private | Only explicitly granted users/teams | Confidential or proprietary work |
| Internal | Enterprise members only where supported | Company-wide sharing inside enterprise |

### Exam Tip

If the repository must be visible only to members of the enterprise but not the public, choose internal repository where supported.

---

## 6.3 Repository Roles

### Repository Role Table

| Role | Best For | Key Access Idea |
|---|---|---|
| Read | Non-code contributors who need to view/discuss | View, clone, open issues/PRs from forks |
| Triage | Manage issues/PRs without code write | Apply labels, assign, manage issues/PRs |
| Write | Active contributors | Push branches and contribute code |
| Maintain | Project maintainers/managers | Manage repo settings except sensitive/destructive actions |
| Admin | Full repository control | Security settings, delete/transfer repo, manage access |

### Least Privilege Decision Table

| Scenario | Recommended Role |
|---|---|
| Business stakeholder needs to view docs and comment | Read |
| Support lead needs to label/assign issues but not push code | Triage |
| Developer needs to push feature branches | Write |
| Project lead needs to manage labels, settings, discussions, Pages | Maintain |
| Repo owner needs branch protection/security/delete/manage access | Admin |

### Exam Tip

Always choose the smallest role that satisfies the requirement.

### Exam Trap

Do not choose Admin when Write, Triage, Maintain, or Read is enough.

---

## 6.4 Organization Settings, Teams, Roles, and Outside Collaborators

### Definitions

| Feature | Purpose | Use When |
|---|---|---|
| Organization owner | Admin control over organization | Manage settings, teams, policies, billing, access |
| Organization member | User who belongs to organization | Internal user needing org access |
| Team | Group users for repository access and mentions | Manage access by group |
| Base permissions | Default repo access for org members | Organization-wide access baseline |
| Outside collaborator | Non-member with access to specific repo | External partner/contractor |
| Organization role | Permission level within organization | Delegate organization-level responsibilities |

### Exam Tips

- Use teams for scalable permission management.
- Use outside collaborators for external users who need access only to specific repositories.
- Use organization owner for organization-wide administration.
- Use base permissions carefully because they affect default access.

---

## 6.5 Branch Protection and Repository Rulesets

### Definitions

| Protection / Rule | Purpose | Exam Clue |
|---|---|---|
| Require pull request before merge | Prevent direct changes to protected branch | Need review workflow |
| Require approvals | Enforce peer review | Need one or more reviewers |
| Require status checks | Ensure CI passes before merge | Need tests/build/security checks pass |
| Require conversation resolution | Prevent unresolved comments | Need reviewers' comments addressed |
| Require signed commits | Verify commit signatures | Need commit authenticity |
| Restrict who can push | Limit direct branch updates | Need protect main/release branches |
| CODEOWNERS review | Require owners for files | Need domain owners approve changes |

### Decision Tree

```text
Need prevent direct commits to main?
-> Require pull request before merging

Need automated tests before merge?
-> Require status checks

Need specific file owners to review?
-> CODEOWNERS + required review

Need only certain people can update branch?
-> Restrict push access

Need comments addressed before merge?
-> Require conversation resolution
```

### Exam Tip

If the scenario says main branch must be protected from direct push, choose branch protection or repository rulesets.

---

## 6.6 Enterprise Managed Users and Copilot Policy

### Enterprise Managed Users

Enterprise Managed Users are GitHub accounts controlled by an enterprise. They are used when organizations need centralized identity lifecycle management.

### Copilot Policy

Organization and enterprise Copilot policies allow administrators to control Copilot availability and governance for users and teams.

### Exam Tips

- Enterprise-owned identities: Enterprise Managed Users.
- Organization-wide AI coding governance: Copilot policy.
- Central control across multiple organizations: enterprise account.

---

# Domain 7 - Explore the GitHub Community

## 7.1 Open Source

### Definition

Open source refers to projects where source code is available under a license that defines how others can use, modify, and distribute it.

### Description

GitHub supports open source through repositories, licenses, issues, pull requests, discussions, community standards, Sponsors, discoverability, and collaboration tools.

### Exam Tips

- Open source reuse requires a license.
- Public does not automatically mean open-source licensed.
- Good open-source repositories usually have README, LICENSE, CONTRIBUTING, CODE_OF_CONDUCT, and SECURITY files.

---

## 7.2 GitHub Sponsors

### Definition

GitHub Sponsors allows individuals and organizations to financially support open-source maintainers and projects.

### Exam Tip

If the scenario says a maintainer needs financial support or funding from the community, choose GitHub Sponsors.

---

## 7.3 Following Users and Organizations

### Definition

Following users or organizations helps you stay informed about their GitHub activity and discover projects and contributors.

### Related Actions

- Follow a user.
- Follow an organization.
- Watch a repository.
- Star a repository.

### Exam Tip

If the scenario says stay informed about a user or organization, choose follow. If it says track repository activity, choose watch.

---

## 7.4 GitHub Marketplace

### Definition

GitHub Marketplace is where users can find apps, Actions, and integrations to extend GitHub workflows.

### Examples

- CI/CD tools.
- Code quality tools.
- Security scanning tools.
- Project management integrations.
- Reusable GitHub Actions.

### Exam Tip

If the requirement is to find reusable apps, Actions, or integrations, choose GitHub Marketplace.

---

## 7.5 Forks, Templates, and Discoverable Repositories

### Definitions

| Feature | Definition | Use When |
|---|---|---|
| Fork | Copy of a repository under your account | Contribute without write access or experiment |
| Template repository | Starter repository used to create new repos | Standardize new projects |
| Topics | Tags that describe a repository | Improve discoverability |
| README | Project landing page | Explain project purpose and usage |
| License | Legal permissions | Clarify reuse rights |
| Star | Bookmark or signal interest | Save useful repository |

### Exam Tip

Fork for contribution without write access. Template for starting something new from a standard pattern.

---

## 7.6 InnerSource

### Definition

InnerSource applies open-source practices inside an organization, usually using private or internal repositories.

### Description

InnerSource encourages transparency, reusable components, cross-team contribution, documented contribution processes, and collaborative review practices inside a company.

### Exam Tip

If the scenario says open-source-style collaboration inside a company, choose InnerSource.

---

# Final Exam Revision

## A. Master Decision Matrix

### Git and GitHub Basics

| Requirement | Best Answer |
|---|---|
| Track changes and revert mistakes | Version control / Git |
| Hosted collaboration platform | GitHub |
| Work offline and commit locally | Git |
| Store project files and history | Repository |
| Save a snapshot of changes | Commit |
| Isolate feature work from main | Branch |
| Copy repository locally | Clone |
| Copy repository under your GitHub account | Fork |
| Upload local commits | Push |
| Bring remote changes locally | Pull |
| Lightweight PR-based workflow | GitHub Flow |

### Repository Files

| Requirement | Best Answer |
|---|---|
| Project overview | README.md |
| Legal usage rights | LICENSE |
| Contribution process | CONTRIBUTING.md |
| Vulnerability reporting | SECURITY.md |
| Automatic reviewer ownership | CODEOWNERS |
| Ignore local/build files | .gitignore |
| Standard bug report | Issue template |
| Standard PR checklist | Pull request template |
| Automation | .github/workflows YAML |

### Collaboration

| Requirement | Best Answer |
|---|---|
| Track bug/task/feature | Issue |
| Propose code/doc change | Pull request |
| Open-ended Q&A | Discussion |
| Categorize work | Label |
| Assign responsibility | Assignee |
| Group work for a release | Milestone |
| Link PR to issue and close on merge | Fixes/Closes/Resolves issue number |
| Share small snippet | Gist |
| Multi-page repo documentation | Wiki |
| Static website | GitHub Pages |
| Reusable support response | Saved reply |

### Modern Development

| Requirement | Best Answer |
|---|---|
| Automate build/test/deploy | GitHub Actions |
| Trigger automation by event | Event |
| Machine that executes jobs | Runner |
| Group of steps | Job |
| Individual command/action | Step |
| Reusable automation component | Action |
| Test multiple OS/versions | Matrix |
| Store workflow secret | Actions secrets |
| AI coding help | GitHub Copilot |
| Full cloud dev environment | Codespaces |
| Quick browser edit | github.dev |
| Repeatable team dev environment | Dev container |

### Projects

| Requirement | Best Answer |
|---|---|
| Single work item | Issue |
| Visual backlog/roadmap | GitHub Project |
| Timeline planning | Roadmap layout |
| Kanban tracking | Board layout |
| Detailed metadata | Table layout |
| Priority/effort fields | Custom fields |
| Release grouping | Milestone |
| Automatic project item updates | Project workflows |
| Charts/progress | Project insights |

### Security and Administration

| Requirement | Best Answer |
|---|---|
| Protect account login | 2FA / passkeys |
| Tool/API authentication | PAT |
| Git command-line authentication | SSH key |
| Detect leaked credentials | Secret scanning |
| Confidential repository | Private visibility |
| Company-wide enterprise-only visibility | Internal visibility |
| View/comment only | Read role |
| Manage issues/PRs but no code push | Triage role |
| Push code | Write role |
| Manage repo without destructive actions | Maintain role |
| Full repo control | Admin role |
| Group-based access | Team |
| External user with limited repo access | Outside collaborator |
| Prevent direct push to main | Branch protection / ruleset |
| Require tests before merge | Required status checks |
| Require specific file owners | CODEOWNERS + required review |
| Enterprise-owned accounts | Enterprise Managed Users |
| Govern Copilot in organization | Copilot policy |

### Community

| Requirement | Best Answer |
|---|---|
| Financially support maintainers | GitHub Sponsors |
| Find reusable apps/actions | GitHub Marketplace |
| Stay informed about user/org | Follow |
| Track repository activity | Watch |
| Open-source-style internal collaboration | InnerSource |
| Improve project discoverability | Topics, README, license, metadata |

---

## B. Must-Memorize Facts

### Git and GitHub Basics

- Git is a distributed version control system.
- GitHub is a cloud platform for Git repositories and collaboration.
- A repository stores files and history.
- A commit is a saved snapshot of changes.
- A branch is an independent line of development.
- A clone is a local copy of a repository.
- A fork is your GitHub-hosted copy of another repository.
- A pull request proposes merging changes from one branch into another.
- GitHub Flow is branch, commit, pull request, review, merge.
- Markdown is used for README files, issues, PRs, comments, and documentation.

### Repositories

- README.md is the repository landing page.
- LICENSE defines permissions and restrictions for reuse.
- CONTRIBUTING.md explains how to contribute.
- CODEOWNERS defines file/path ownership for reviews.
- SECURITY.md explains how to report vulnerabilities.
- .gitignore excludes local/build/secret files from being tracked.
- Issue templates standardize bug/feature reports.
- Pull request templates standardize review context.
- Repository templates create standardized new repositories.
- Topics improve discoverability.
- Stars bookmark or signal interest.
- Archive makes an inactive repository read-only.

### Collaboration

- Issues track bugs, tasks, and feature requests.
- Pull requests review and merge changes.
- Discussions support open-ended conversations.
- Labels categorize issues and pull requests.
- Assignees show responsibility.
- Milestones group work toward a target.
- Notifications help manage watched, mentioned, assigned, and participating activity.
- Gists share small snippets or notes.
- Wikis provide repository documentation pages.
- GitHub Pages hosts static websites.

### Modern Development

- GitHub Actions automates CI/CD and repository workflows.
- Workflows are YAML files in `.github/workflows`.
- Events trigger workflows.
- Jobs group steps on a runner.
- Steps run commands or actions.
- Runners execute jobs.
- Matrix builds test multiple combinations.
- Secrets store sensitive workflow values.
- Copilot is an AI coding assistant.
- Copilot output must be reviewed and tested.
- Codespaces provides cloud-hosted development environments.
- Dev containers define repeatable development environments.
- github.dev is best for quick browser edits.

### Projects and Planning

- GitHub Projects tracks work across issues and pull requests.
- Projects support table, board, and roadmap layouts.
- Custom fields add metadata like priority, size, iteration, and target date.
- Project workflows automate project item updates.
- Project insights show charts and progress.
- Draft issues capture planning items before formal issues.
- Labels categorize; milestones group; projects visualize/manage.

### Security and Administration

- 2FA adds an extra login factor.
- Passkeys provide modern passwordless authentication.
- Repository visibility can be public, private, or internal where supported.
- Read role is for viewing and discussion.
- Triage role manages issues/PRs without code write access.
- Write role allows active contribution.
- Maintain role manages repository without sensitive/destructive actions.
- Admin role provides full repository control.
- Teams simplify permission management.
- Outside collaborators are non-members with specific repo access.
- Branch protection prevents unsafe changes to important branches.
- Required status checks enforce tests/builds before merge.
- CODEOWNERS can enforce ownership-based review when configured with branch protection/rulesets.
- Enterprise Managed Users are enterprise-controlled GitHub accounts.
- Copilot policies help govern AI coding assistant usage.

### Community

- Open source needs a license to define reuse rights.
- Public repository does not automatically mean licensed for reuse.
- GitHub Sponsors supports maintainers financially.
- Following users/orgs helps track activity.
- GitHub Marketplace provides apps, Actions, and integrations.
- InnerSource applies open-source practices inside organizations.
- Forks support external contribution.
- Templates support standardized new projects.

---

## C. Common Exam Traps

- Git is not GitHub.
- Clone is not fork.
- Branch is not fork.
- Template is not fork.
- README is not LICENSE.
- CONTRIBUTING is not CODEOWNERS.
- SECURITY.md is not secret scanning.
- Issue is not pull request.
- Discussion is not issue when work tracking is required.
- Pull request is for proposed changes and review.
- Wiki is not GitHub Pages.
- github.dev is not Codespaces.
- Actions workflow is not a single action.
- Runner is the machine; workflow is the automation definition.
- Job contains steps; step can run an action.
- Secrets should not be stored directly in YAML or README.
- Required checks are enforced through branch protection/rulesets.
- Triage role does not allow pushing code.
- Maintain is not full Admin.
- Milestones are good for releases; Projects are flexible planning views.
- CODEOWNERS requires compatible branch protection/rulesets to enforce required review.
- Copilot output should be tested and reviewed.
- Open source does not mean no license is needed.
- InnerSource is internal, not public open source.
- GitHub Marketplace is for integrations and apps, not repository hosting.
- Passkeys/2FA protect account sign-in, not branch workflows.
- Branch protection protects code workflow, not account login.
- .gitignore is not a security boundary for already-committed secrets.
- Repository insights are for visibility, not deployment.
- Dependency graph shows dependencies, not Git history.
- Use least privilege for users, teams, and collaborators.

---

## D. Scenario Practice Questions

### Domain 1 - Git and GitHub Basics

1. A developer needs to save project history locally and work offline. What tool is involved?  
   **Answer:** Git.

2. A team needs a cloud platform for pull requests, issues, reviews, and Actions. What should they use?  
   **Answer:** GitHub.

3. You need to work on a feature without affecting main. What should you create?  
   **Answer:** A branch.

4. You need to propose your branch changes for review. What should you open?  
   **Answer:** A pull request.

5. You do not have write access to an open-source repo but want to propose a change. What should you do first?  
   **Answer:** Fork the repository, make changes, and open a pull request.

6. You want to copy a repository locally with full history. What action is this?  
   **Answer:** Clone.

7. Which workflow uses branch, commit, pull request, review, and merge?  
   **Answer:** GitHub Flow.

### Domain 2 - Repositories

8. A new contributor needs project setup instructions. Which file should they read?  
   **Answer:** README.md.

9. A public project needs to define legal reuse rights. Which file should be added?  
   **Answer:** LICENSE.

10. A team wants automatic reviewer assignment for files under `/security`. Which file helps?  
    **Answer:** CODEOWNERS.

11. A project needs a vulnerability reporting process. Which file should be added?  
    **Answer:** SECURITY.md.

12. A team wants all bug reports to include reproduction steps. What should they configure?  
    **Answer:** Issue template.

13. A team wants every PR to include testing confirmation. What should they configure?  
    **Answer:** Pull request template.

14. A repository should become read-only because development stopped. What should you do?  
    **Answer:** Archive the repository.

15. A maintainer wants to understand views, clones, contributors, and activity. What should they use?  
    **Answer:** Repository insights or metrics.

### Domain 3 - Collaboration

16. Where should a bug be tracked?  
    **Answer:** Issue.

17. Where should a code change be reviewed before merge?  
    **Answer:** Pull request.

18. Where should a broad community Q&A topic be started?  
    **Answer:** Discussion.

19. Which feature categorizes issues as bug or enhancement?  
    **Answer:** Labels.

20. Which feature groups issues for a release target?  
    **Answer:** Milestone.

21. Which phrase can close issue 25 when a PR merges?  
    **Answer:** Fixes #25, Closes #25, or Resolves #25.

22. You need to publish a static documentation website from a repo. What should you use?  
    **Answer:** GitHub Pages.

23. You need to share a short code snippet. What should you use?  
    **Answer:** Gist.

24. A user receives too many repository alerts. What should they adjust?  
    **Answer:** Notification or watch settings.

### Domain 4 - Modern Development

25. You need tests to run on every pull request. What should you use?  
    **Answer:** GitHub Actions.

26. In GitHub Actions, what starts a workflow?  
    **Answer:** An event.

27. In GitHub Actions, what executes jobs?  
    **Answer:** A runner.

28. Where are workflow files stored?  
    **Answer:** `.github/workflows`.

29. You need to test on multiple operating systems. What Actions feature helps?  
    **Answer:** Matrix strategy.

30. You need AI coding suggestions and chat assistance. What should you use?  
    **Answer:** GitHub Copilot.

31. A developer needs a complete cloud dev environment with terminal and dependencies. What should they use?  
    **Answer:** GitHub Codespaces.

32. A developer only needs to quickly edit README in browser. What can they use?  
    **Answer:** github.dev or GitHub web editor.

33. A team wants consistent development environments. What should they define?  
    **Answer:** Dev container configuration.

### Domain 5 - Projects

34. A team wants a Kanban view of work. What should they use?  
    **Answer:** GitHub Projects board layout.

35. A team wants a timeline roadmap. What should they use?  
    **Answer:** GitHub Projects roadmap layout.

36. A team wants to track priority and effort fields. What Projects feature helps?  
    **Answer:** Custom fields.

37. A support user sends the same triage answer often. What should they use?  
    **Answer:** Saved replies.

38. A team wants progress charts from tracked items. What should they use?  
    **Answer:** Project insights.

### Domain 6 - Security/Admin

39. A user account needs stronger sign-in protection. What should be enabled?  
    **Answer:** 2FA or passkeys.

40. Stakeholders need to view and comment but not push code. Which repository role fits?  
    **Answer:** Read.

41. A user must manage labels and issues but not push code. Which role fits?  
    **Answer:** Triage.

42. A developer must push code. Which role fits?  
    **Answer:** Write.

43. A project manager must manage repository settings but not destructive actions. Which role fits?  
    **Answer:** Maintain.

44. Someone must manage access and security settings. Which role fits?  
    **Answer:** Admin.

45. You must prevent direct pushes to main. What should be configured?  
    **Answer:** Branch protection or repository ruleset.

46. You must require tests before merging. What should be configured?  
    **Answer:** Required status checks.

47. An enterprise wants centrally managed GitHub user accounts. What feature fits?  
    **Answer:** Enterprise Managed Users.

### Domain 7 - Community

48. A maintainer wants financial support from users. What feature helps?  
    **Answer:** GitHub Sponsors.

49. A team wants reusable GitHub apps/actions. Where should they look?  
    **Answer:** GitHub Marketplace.

50. A company wants open-source-style collaboration internally. What is this called?  
    **Answer:** InnerSource.

---

## E. Two-Hour Final Revision Checklist

Before the exam, confirm you can explain each item without notes:

- Git vs GitHub.
- Repository vs branch vs commit.
- Clone vs fork vs template.
- GitHub Flow steps.
- README vs LICENSE vs CONTRIBUTING vs CODEOWNERS vs SECURITY.
- Issue vs pull request vs discussion.
- Labels vs milestones vs Projects.
- Wiki vs GitHub Pages vs Gist.
- GitHub Actions workflow vs event vs job vs step vs action vs runner.
- GitHub-hosted runner vs self-hosted runner.
- Actions secrets and why not to hardcode credentials.
- Copilot purpose, Copilot Chat, Agent Mode, and multi-model support.
- Copilot plans: individual, business, enterprise.
- Codespaces vs github.dev.
- Dev containers and repeatable environments.
- Project layouts: table, board, roadmap.
- Project custom fields, workflows, and insights.
- Repository roles: Read, Triage, Write, Maintain, Admin.
- Public vs private vs internal repositories.
- 2FA/passkeys vs branch protection.
- Required reviews, required status checks, CODEOWNERS.
- Organizations, teams, outside collaborators, enterprise accounts, EMUs.
- Open source, Sponsors, Marketplace, InnerSource.

---

## F. Seven-Day Revision Plan

| Day | Focus |
|---:|---|
| 1 | Git vs GitHub, repositories, commits, branches, clone/fork/pull/push, GitHub Flow |
| 2 | Repository files: README, LICENSE, CONTRIBUTING, CODEOWNERS, SECURITY, templates, insights |
| 3 | Issues, pull requests, discussions, notifications, Gists, Wikis, Pages |
| 4 | GitHub Actions, Copilot, Codespaces, dev containers, github.dev |
| 5 | GitHub Projects, labels, milestones, assignees, saved replies, insights |
| 6 | Security/admin: 2FA, passkeys, roles, teams, branch protection, EMUs, Copilot policy |
| 7 | Open source, Sponsors, Marketplace, InnerSource, final decision matrix and practice questions |

