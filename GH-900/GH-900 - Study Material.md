# GH-900 Robust Study Material - Expanded Scenario Use-Case Guide

**Exam:** GH-900: GitHub Foundations  
**Certification:** GitHub Foundations  
**Generated:** 31 July 2026  
**Purpose:** Single Markdown study pack in the same practical scenario-focused style as the DP-800 guide. It includes concepts, decision trees, examples, scenario cheat sheets, must-memorize facts, and last-mile exam traps so you do not need to jump back to Microsoft Learn at the last moment.

> **Exam mindset:** GH-900 is foundational, but it is still scenario-based. When a question gives a business requirement, identify the keyword: version history, repository, fork, branch, commit, pull request, issue, discussion, notification, README, LICENSE, CODEOWNERS, Actions, Copilot, Codespaces, Projects, 2FA, passkeys, branch protection, roles, Marketplace, open source, InnerSource.

---

## Exam Weighting and Study Strategy

| Domain | Weight | What to master |
|---|---:|---|
| Understand Git and GitHub basics | 25-30% | Git vs GitHub, version control, repositories, commits, branches, GitHub Flow, Markdown, GitHub Desktop, GitHub Mobile |
| Work with GitHub repositories | 10-15% | Repository files, README, LICENSE, CONTRIBUTING, CODEOWNERS, SECURITY, templates, branches, insights, stars, metrics, dependency insights |
| Collaborate using GitHub | 10-15% | Issues, pull requests, discussions, templates, filters, assignments, notifications, Gists, Wikis, GitHub Pages |
| Apply modern development practices | 10-15% | GitHub Actions, workflows, jobs, runners, Copilot, Copilot plans, Codespaces, dev containers, github.dev |
| Manage projects with GitHub | 5-10% | GitHub Projects, table/board/roadmap layouts, labels, milestones, workflows, saved replies, assignees, insights |
| Understand privacy, security, and administration | 10-15% | 2FA, passkeys, roles, teams, permissions, EMUs, Copilot policy, repository visibility, branch protection, organization settings |
| Explore the GitHub community | 5-10% | Open source, Sponsors, following users/orgs, Marketplace, InnerSource, forks, templates, discoverability |

### How To Study GH-900

| If you have... | Focus on... |
|---|---|
| 1 day | Decision trees, scenario cheat sheet, repository files, GitHub Flow, roles, Actions/Copilot/Codespaces basics |
| 3 days | Domains 1-4 first, then security/admin, then community and Projects |
| 7 days | One domain per day plus practice questions and hands-on GitHub navigation |

---

# Domain 1 - Understand Git and GitHub Basics

## 1. Version Control Fundamentals

### Version Control Overview

| Concept | What it is | When to use / exam clue |
|---|---|---|
| Version control | A system for tracking changes over time | Requirement says track history, compare changes, revert mistakes, collaborate safely |
| Distributed version control | Each contributor has a local copy of repository history | Requirement says work offline, commit locally, sync later |
| Git | The distributed version control tool | Commands like clone, commit, branch, merge, push, pull |
| GitHub | A cloud platform for hosting Git repositories and collaboration | Issues, pull requests, discussions, Actions, Projects, security, community |
| Repository | Project storage containing files and history | Need a place to store code/docs/configuration |
| Commit | Snapshot of changes with metadata and message | Need record of what changed and why |
| Branch | Independent line of development | Need isolate feature/fix work from main branch |
| Merge | Combine changes from one branch into another | Need bring feature branch into main after review |
| Clone | Download full repository to local machine | Need work locally with full history |
| Fork | Personal copy of another repository under your account | Need contribute without direct write access to original repository |
| Pull | Fetch and integrate remote changes locally | Need update local branch from remote |
| Push | Upload local commits to remote | Need publish local work to GitHub |

### Git vs GitHub Decision Table

| Scenario | Best answer | Why |
|---|---|---|
| Need local version control on a laptop | Git | Git is the version control system |
| Need web-based collaboration, issues, PRs, review, hosting | GitHub | GitHub hosts Git repos and collaboration features |
| Need to commit while offline | Git | Commits are local until pushed |
| Need to run CI/CD on pull request | GitHub Actions | Platform automation feature |
| Need discussion, planning, or community contribution | GitHub | Collaboration and community platform |

**Exam trap:** Git and GitHub are related but not the same. Git is the tool; GitHub is a hosting and collaboration platform built around Git.

### Core Git Command Cheat Sheet

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

| Command | Purpose | Use when |
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

---

## 2. GitHub Accounts, Organizations, and Enterprise Options

| Option | Description | Best for |
|---|---|---|
| Personal account | Individual GitHub identity | Personal projects, contributions, learning |
| Organization | Shared account for teams and projects | Company/team repositories, teams, centralized permissions |
| Enterprise account | Top-level account for multiple organizations | Large companies needing centralized policy, billing, security, SSO, governance |
| Enterprise Managed Users (EMUs) | Enterprise-controlled user accounts | Strict identity lifecycle and enterprise-managed GitHub identities |

### Account / Organization Decision Tree

Need one person's projects?
  -> Personal account
Need shared team repositories and permissions?
  -> Organization
Need centralized control across many organizations?
  -> Enterprise account
Need enterprise-owned developer identities?
  -> Enterprise Managed Users

---

## 3. GitHub Flow

### GitHub Flow Steps

1. Create a branch from `main`.
2. Add commits to the branch.
3. Open a pull request.
4. Discuss and review changes.
5. Run checks and resolve issues.
6. Merge into `main`.
7. Deploy from `main` if that is your release strategy.

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

| Scenario | Best GitHub Flow action |
|---|---|
| Need isolate work from stable main branch | Create a branch |
| Need ask others to review proposed changes | Open a pull request |
| Need discuss a change before merge | Use PR comments/review |
| Need automatically validate changes | Configure required checks / GitHub Actions |
| Need enforce review before merging | Branch protection or ruleset |

**Exam tip:** GitHub Flow is lightweight and pull-request based. It is not the same as Git Flow with long-lived develop/release branches.

---

## 4. Markdown for GitHub Communication

| Markdown feature | Syntax | Use case |
|---|---|---|
| Heading | `# Heading` | Structure README/issues |
| Bullet list | `- item` | Requirements or tasks |
| Task list | `- [ ] task` | Track work in issues/PRs |
| Bold | `**text**` | Emphasis |
| Inline code | `` `code` `` | Commands, file names |
| Code block | Triple backticks | Multi-line examples |
| Link | `[text](url)` | Reference docs/issues |
| Image | `![alt](url)` | Diagrams/screenshots |
| Quote | `> text` | Highlight note |
| Table | Markdown table | Compare options |

### Markdown Exam Uses

| Requirement | Best answer |
|---|---|
| Create project landing page | README.md |
| Add task checklist in an issue | Markdown task list |
| Explain contribution steps | CONTRIBUTING.md |
| Format commands clearly | Code blocks |
| Link related pull request or issue | Markdown link or GitHub auto-link |

---

## 5. GitHub Desktop, GitHub Mobile, and github.dev

| Tool | What it is | Best for | Not best for |
|---|---|---|---|
| GitHub Desktop | Desktop GUI for Git and GitHub workflows | Beginners, visual commit/branch/PR flow | Cloud dev environment or heavy browser-only coding |
| GitHub Mobile | Mobile app for GitHub notifications and collaboration | Review issues/PRs, triage, comment on the go | Full development environment |
| github.dev editor | Lightweight browser editor for repositories | Quick edits in browser without full compute | Running/building server-side apps |
| GitHub Codespaces | Cloud development environment | Full development, terminal, dependencies, dev containers | Simple one-line documentation edit when no runtime needed |

---

# Domain 2 - Work with GitHub Repositories

## 6. Repository Structure and Key Files

### Key Repository Files

| File | Purpose | Exam clue |
|---|---|---|
| README.md | Project overview, setup, usage, badges, links | New user needs to understand project quickly |
| LICENSE | Defines legal permissions for using/modifying/distributing project | Need clarify open-source usage rights |
| CONTRIBUTING.md | Explains how to contribute | New contributors need contribution process |
| CODEOWNERS | Defines reviewers responsible for files/paths | Need automatic review requests from owners |
| SECURITY.md | Explains security reporting policy | Need responsible vulnerability disclosure |
| .gitignore | Files Git should ignore | Need exclude build output/secrets/local config |
| SUPPORT.md | Support channels and expectations | Need direct users to help resources |
| ISSUE_TEMPLATE | Standardize issue creation | Need collect consistent bug/feature information |
| PULL_REQUEST_TEMPLATE | Standardize PR details | Need checklist and context for reviewers |
| .github/workflows/*.yml | GitHub Actions workflows | Need automated CI/CD or repo automation |

### Repository File Decision Tree

Need project introduction?
  -> README.md
Need legal permission for reuse?
  -> LICENSE
Need contribution rules?
  -> CONTRIBUTING.md
Need automatic reviewer assignment?
  -> CODEOWNERS
Need vulnerability reporting instructions?
  -> SECURITY.md
Need standard bug report information?
  -> Issue template
Need PR review checklist?
  -> Pull request template
Need automation?
  -> GitHub Actions workflow YAML

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

**Exam trap:** `.gitignore` does not remove files already committed. It stops untracked matching files from being added in the future.

---

## 7. Repository Creation, Templates, Branches, and Maintenance

| Feature | Description | When to use |
|---|---|---|
| New repository | Create a new project container | Starting a new project |
| Repository template | Create new repos from a predefined structure | Standardize starter projects |
| Branch | Parallel development line | Feature/fix isolation |
| Default branch | Main branch used for PR base and default view | Usually `main` |
| Protected branch / ruleset | Enforces workflow requirements | Require PR review, checks, restrictions |
| Archive repository | Make repository read-only | Project is no longer maintained |
| Topics | Tags describing repository | Improve discoverability |
| Stars | Bookmark/recommend repository | Track popular or useful repos |
| Repository insights | Metrics and activity visibility | Understand contributors, traffic, commits, dependency graph |

### Repository Maintenance Best Practices

- Keep README accurate and beginner-friendly.
- Add a LICENSE if the repository is intended for public reuse.
- Use issue and PR templates for consistency.
- Use CODEOWNERS for ownership clarity.
- Protect important branches.
- Avoid committing secrets.
- Use Dependabot/dependency insights where available.
- Archive inactive repositories rather than deleting if history should remain visible.

---

## 8. Repository Insights and Visibility

| Feature | What it shows | Use case |
|---|---|---|
| Pulse | Recent repository activity | Quick health/activity check |
| Contributors | Contribution activity by people | Understand who contributed |
| Community standards | README, code of conduct, contributing, license, security files | Improve open-source readiness |
| Traffic | Views and clones | Measure repository interest |
| Dependency graph | Dependencies used by project | Understand dependency relationships and alerts |
| Security insights | Vulnerabilities and code/security alerts where enabled | Improve security posture |
| Stars | Users interested in repository | Popularity/bookmark signal |
| Forks | Copies made by users | Community contribution and experimentation signal |

---

# Domain 3 - Collaborate Using GitHub

## 9. Issues, Pull Requests, and Discussions

### Collaboration Tool Selection Matrix

| Requirement | Best tool | Why |
|---|---|---|
| Track a bug, task, or feature request | Issue | Issue is work item / conversation around work |
| Propose code or documentation changes | Pull request | PR compares branch changes and supports review/merge |
| Ask open-ended question or community topic | Discussion | Better for Q&A, ideas, announcements, community conversation |
| Announce project updates | Discussion announcement category | Good for broadcast/community updates |
| Capture repeatable bug details | Issue template | Standardizes information |
| Capture PR checklist | Pull request template | Standardizes review readiness |
| Link implementation to task | Link PR to issue | Traceability and auto-close support |

### Issues

| Feature | Purpose |
|---|---|
| Labels | Categorize issues/PRs, e.g., bug, enhancement, help wanted |
| Assignees | Show who owns work |
| Milestones | Group work towards a target/release |
| Projects | Track issues and PRs in tables/boards/roadmaps |
| Filters | Find issues by label, assignee, state, author, etc. |
| Templates | Collect standardized information |

### Pull Requests

| PR feature | Purpose | Exam clue |
|---|---|---|
| Review | Approve, comment, request changes | Need peer review |
| Draft PR | Work is not ready for review | Early feedback without merge readiness |
| Required checks | Must pass before merge | Enforce automated validation |
| Linked issue | Connect code change to work item | Traceability, may close issue on merge |
| CODEOWNERS review | Automatically request file owners | Ownership-based review |
| Merge commit | Preserve branch history with merge commit | Need explicit merge record |
| Squash merge | Combine PR commits into one | Clean main branch history |
| Rebase merge | Replay commits onto base branch | Linear history |

### Issue-to-PR Linking Keywords

| Wording | Effect |
|---|---|
| `Fixes #123` | Links PR and can close issue when PR merges |
| `Closes #123` | Same closure intent |
| `Resolves #123` | Same closure intent |
| `Related to #123` | Links but does not automatically close |

**Exam trap:** A pull request is for proposed changes. A discussion is not the right tool to merge code.

---

## 10. Notifications, Gists, Wikis, and Pages

| Feature | Description | Best for |
|---|---|---|
| Notifications | Alerts for repository/user/team activity | Managing work you are participating in or watching |
| Watch | Subscribe to repository activity | Follow all/specific repository events |
| Mention | Notify a user/team using `@` | Bring someone into conversation |
| Saved replies | Reusable responses | Common triage/support messages |
| Gist | Lightweight snippet or note sharing | Share small code/text snippets |
| Wiki | Repository documentation pages | More detailed docs linked to a repo |
| GitHub Pages | Static website hosting from repository | Publish docs, project site, portfolio |

### Pages vs Wiki vs README

| Requirement | Best answer |
|---|---|
| Quick project overview on repository home | README |
| Multi-page repo documentation maintained near project | Wiki |
| Public static website with custom pages | GitHub Pages |
| Share a short code snippet independently | Gist |

---

# Domain 4 - Apply Modern Development Practices

## 11. GitHub Actions

### GitHub Actions Core Concepts

| Concept | Description | Exam clue |
|---|---|---|
| Workflow | Automated process defined in YAML | Need build/test/deploy automation |
| Event | Trigger that starts workflow | push, pull_request, issue opened, schedule, manual |
| Job | Group of steps that run on same runner | Need organize work / parallelize |
| Step | Individual command or action inside a job | Shell command or reusable action |
| Action | Reusable automation component | Avoid writing repeated workflow logic |
| Runner | Machine that executes jobs | GitHub-hosted or self-hosted |
| Matrix | Runs same job across combinations | Test multiple OS/language versions |
| Secret | Encrypted value for workflow | Avoid hardcoding credentials |

### Workflow Example

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

### Actions Scenario Matrix

| Scenario | Best answer |
|---|---|
| Run tests on every pull request | GitHub Actions workflow triggered by `pull_request` |
| Deploy after merge to main | Workflow triggered by push to main or release |
| Run nightly scan | Scheduled workflow |
| Reuse common workflow across repos | Reusable workflow |
| Avoid exposing passwords in workflow YAML | GitHub Actions secrets |
| Need specific hardware/network | Self-hosted runner |
| Need Linux/Windows/macOS hosted VM | GitHub-hosted runner |

**Exam trap:** GitHub Actions is not only CI/CD. It can automate repository events like labeling issues or responding to pull request activity.

---

## 12. GitHub Copilot

### Copilot Capability Overview

| Capability | Description | Good scenario |
|---|---|---|
| Code suggestions | AI suggestions as you type | Speed up coding in IDE |
| Copilot Chat | Ask questions about code or repo context | Explain, debug, refactor, generate tests |
| Pull request assistance | Helps generate PR descriptions/summaries | Improve review context |
| CLI assistance | Help with command-line tasks | Generate/explain shell or Git commands |
| Agent mode / coding agent | Can plan and make changes for review | Delegate scoped coding tasks with human review |
| Multi-model support | Choose different models where available | Match task to model capability/cost/performance |

### Copilot Plans - Exam-Level Difference

| Plan | Best for | Key idea |
|---|---|---|
| Copilot for Individuals / Pro-style plans | Individual developer productivity | Personal subscription and features |
| Copilot Business | Organization-managed Copilot access | Central policy and user management for orgs |
| Copilot Enterprise | Enterprise-scale Copilot with deeper GitHub integration | Larger governance and enterprise features |

### Copilot Security Rules

- Do not paste secrets, tokens, credentials, customer data, or sensitive data into prompts.
- Review generated code before use.
- Treat AI-generated code as a draft, not an approved implementation.
- Use pull requests and security scans for generated changes.
- Use organization/enterprise Copilot policies where governance is required.

**Exam trap:** Copilot assists development. It does not remove the need for code review, testing, security scanning, or human accountability.

---

## 13. GitHub Codespaces, Dev Containers, and github.dev

### Codespaces Overview

| Feature | Description | Exam clue |
|---|---|---|
| Codespace | Cloud-hosted development environment | Need full dev environment without local setup |
| Dev container | Configuration-as-code for development environment | Need repeatable dependencies/tools/settings |
| Browser or VS Code access | Connect from browser, VS Code, or CLI | Need flexible access to environment |
| Linux container environment | Runs in a Docker container on a VM | Need consistent Linux-based runtime |
| Prebuilds | Speed up codespace startup | Large repos or slow setup |
| Secrets | Secure environment values | Need credentials inside codespace safely |

### Dev Container Example

```json
{
  "name": "Node Dev Container",
  "image": "mcr.microsoft.com/devcontainers/javascript-node:1-20-bullseye",
  "customizations": {
    "vscode": {
      "extensions": ["GitHub.copilot"]
    }
  }
}
```

### Codespaces vs github.dev Decision Table

| Requirement | Best answer | Why |
|---|---|---|
| Quick browser edit to README | github.dev | Lightweight editor, no full compute needed |
| Run app/tests/build in browser environment | Codespaces | Provides compute, terminal, dependencies |
| Standardize dev tools for team | Dev container + Codespaces | Configuration as code |
| Review small documentation change | github.dev or GitHub web editor | Fast edit pathway |
| Need full VS Code-like cloud environment | Codespaces | Full cloud development environment |

---

# Domain 5 - Manage Projects with GitHub

## 14. GitHub Projects

### Projects Feature Overview

| Feature | Description | Use when |
|---|---|---|
| Project | Flexible planning and tracking tool | Manage backlog, roadmap, sprint, triage |
| Table layout | Spreadsheet-like view | Detailed planning and metadata |
| Board layout | Kanban-style columns | Workflow/status tracking |
| Roadmap layout | Timeline planning | Time-based planning and releases |
| Custom fields | Metadata like priority, size, target date | Track information not built into issues/PRs |
| Workflows | Automations in Projects | Automatically set status or archive items |
| Insights | Charts and progress visibility | Track productivity/progress |
| Draft issue | Project item not yet formal issue | Early planning/backlog capture |

### Projects vs Issues vs Milestones

| Requirement | Best answer |
|---|---|
| Track a single bug/task | Issue |
| Group issues/PRs for a release | Milestone |
| Visualize and manage work across many issues/PRs | Project |
| Add priority/effort/custom metadata | Project custom fields |
| Show roadmap timeline | Project roadmap layout |
| Show Kanban status columns | Project board layout |

### Labels, Milestones, Assignees, Saved Replies

| Feature | Purpose | Example |
|---|---|---|
| Label | Categorize work | bug, documentation, help wanted |
| Milestone | Group work toward target | v1.0 release |
| Assignee | Assign responsibility | Person responsible for issue/PR |
| Saved reply | Reuse common response | Triage response or support guidance |

---

# Domain 6 - Privacy, Security, and Administration

## 15. Account Security

| Feature | Description | Exam clue |
|---|---|---|
| Two-factor authentication (2FA) | Requires second factor in addition to password | Need protect account login |
| Passkeys | Passwordless/authenticator-backed sign-in method | Modern sign-in resistant to phishing |
| Personal access token (PAT) | Token for API/Git operations | Need authenticate tooling without password |
| SSH key | Key-based Git authentication | Need secure Git command-line access |
| Secret scanning | Detect committed secrets where enabled | Need identify leaked credentials |

**Exam tip:** 2FA/passkeys protect identity access. Branch protection protects repository workflow. These solve different problems.

---

## 16. Repository Visibility and Access Roles

### Repository Visibility

| Visibility | Who can see it | Use when |
|---|---|---|
| Public | Everyone | Open-source or public docs/projects |
| Private | Only explicitly granted users/teams | Confidential/proprietary work |
| Internal | Enterprise members only where supported | Company-wide sharing inside enterprise |

### Repository Roles

| Role | Best for | Key access idea |
|---|---|---|
| Read | Non-code contributors who need to view/discuss | View, clone, open issues/PRs from forks |
| Triage | Manage issues/PRs without code write | Apply labels, assign, manage discussions/issues |
| Write | Active contributors | Push branches, merge PRs depending rules |
| Maintain | Project maintainers/managers | Manage repo settings except sensitive/destructive actions |
| Admin | Full repository control | Security settings, delete/transfer repo, manage access |

### Least Privilege Role Decision

| Scenario | Recommended role |
|---|---|
| Business stakeholder needs to view docs and comment | Read |
| Support lead needs to label/assign issues but not push code | Triage |
| Developer needs to push feature branches | Write |
| Project lead needs to manage labels, settings, discussions, Pages | Maintain |
| Repo owner needs branch protection/security/delete/manage access | Admin |

**Exam trap:** Give the smallest role that satisfies the requirement. Do not choose Admin when Write or Triage is enough.

---

## 17. Branch Protection and Rulesets

| Protection / rule | Purpose | Exam clue |
|---|---|---|
| Require pull request before merge | Prevent direct changes to protected branch | Need review workflow |
| Require approvals | Enforce peer review | Need one or more reviewers |
| Require status checks | Ensure CI passes before merge | Need tests/build/security checks pass |
| Require conversation resolution | Prevent unresolved comments | Need reviewers' comments addressed |
| Require signed commits | Verify commit signatures | Need commit authenticity |
| Restrict who can push | Limit direct branch updates | Need protect main/release branches |
| CODEOWNERS review | Require owners for files | Need domain owners approve changes |

### Branch Protection Decision Tree

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

---

## 18. Organization Settings, Teams, and Copilot Policy

| Feature | Purpose | Use when |
|---|---|---|
| Team | Group users for repository access and mentions | Manage access by group |
| Base permissions | Default repo access for org members | Organization-wide access baseline |
| Outside collaborator | Non-member with access to specific repo | External partner/contractor |
| Organization owner | Admin control over organization | Manage settings, teams, policies |
| Copilot policy | Control Copilot usage at org/enterprise level | Need governance of AI coding assistant |
| Enterprise Managed Users | Centralized enterprise identity model | Enterprise-owned accounts and lifecycle |

---

# Domain 7 - Explore the GitHub Community

## 19. Open Source and Community Features

| Feature | Description | Best for |
|---|---|---|
| Open source | Software/projects with source available under license | Community collaboration and reuse |
| GitHub Sponsors | Financially support maintainers | Funding maintainers/projects |
| Follow users/orgs | Stay informed about activity | Discover updates and contributors |
| GitHub Marketplace | Find apps/actions/integrations | Extend GitHub workflows |
| Fork | Copy repository to contribute or experiment | Propose changes without write access |
| Template repository | Start new project from a standard structure | Repeatable starter repositories |
| Topics/discoverability | Help people find repos | Improve project visibility |
| InnerSource | Apply open-source practices inside organization | Cross-team collaboration in private/internal repos |

### Fork vs Template vs Clone

| Requirement | Best answer | Why |
|---|---|---|
| Work locally on existing repo | Clone | Local copy of repository |
| Contribute to project without write access | Fork | Your server-side copy on GitHub |
| Start a new independent repo from a pattern | Template | New repo without original history dependency |
| Bookmark interesting repo | Star | Save/show interest |

---

# Last-Mile Exam Decision Trees

## Git vs GitHub
Need version control commands/local history?
  -> Git
Need hosted collaboration/issues/PRs/Actions/Projects/security/community?
  -> GitHub

## Branch / Fork / Clone
Need local copy?
  -> Clone
Need isolated line of work inside same repo?
  -> Branch
Need your own GitHub copy because no write access?
  -> Fork
Need start a new repo from starter structure?
  -> Template

## Collaboration Tool
Bug/task/feature tracking?
  -> Issue
Code/doc change proposal?
  -> Pull request
Open-ended Q&A or community conversation?
  -> Discussion
Full project tracking view?
  -> Project
Reusable short snippet?
  -> Gist
Static website?
  -> GitHub Pages

## Documentation File Selection
Project overview?
  -> README.md
Usage rights?
  -> LICENSE
Contribution process?
  -> CONTRIBUTING.md
Security reporting?
  -> SECURITY.md
Auto reviewer ownership?
  -> CODEOWNERS
Standard issue content?
  -> Issue template
Standard PR checklist?
  -> PR template
Automation?
  -> .github/workflows YAML

## Modern Development Tool Selection
Automate build/test/deploy or repo events?
  -> GitHub Actions
AI-powered coding help?
  -> GitHub Copilot
Full cloud dev environment?
  -> GitHub Codespaces
Quick browser edit without compute?
  -> github.dev
Standard team dev environment?
  -> Dev container

## Project Management Selection
Single work item?
  -> Issue
Group work for release?
  -> Milestone
Categorize work?
  -> Label
Assign ownership?
  -> Assignee
Visual plan/backlog/roadmap?
  -> GitHub Project
Repeated response?
  -> Saved reply

## Security and Administration Selection
Protect user login?
  -> 2FA / passkeys
Least privilege repo access?
  -> Repository roles / teams
Prevent direct changes to main?
  -> Branch protection / rulesets
Require automated tests before merge?
  -> Required status checks
Require owners to review files?
  -> CODEOWNERS + required review
Avoid committed credentials?
  -> Secrets, secret scanning, .gitignore, remove from history if committed
Enterprise-owned users?
  -> Enterprise Managed Users

---

# Scenario Cheat Sheet

| Requirement | Best answer | Why |
|---|---|---|
| Track changes and revert mistakes | Version control / Git | Maintains history |
| Host repository and collaborate online | GitHub | Cloud collaboration platform |
| Work on new feature without affecting main | Branch | Isolates work |
| Propose changes for review | Pull request | Review and merge workflow |
| Report bug or task | Issue | Tracks work item |
| Ask broad question to community | Discussion | Open-ended collaboration |
| Standardize issue details | Issue template | Consistent input |
| Add project overview | README.md | Repository landing page |
| Specify open-source terms | LICENSE | Legal usage rights |
| Explain contribution process | CONTRIBUTING.md | Contributor guidance |
| Define file experts/reviewers | CODEOWNERS | Automatic review ownership |
| Explain vulnerability reporting | SECURITY.md | Security disclosure process |
| Prevent direct push to main | Branch protection/ruleset | Protects important branch |
| Run tests on PR | GitHub Actions | CI automation |
| Store workflow secret | GitHub Actions secrets | Avoid hardcoding credentials |
| Full cloud dev environment | Codespaces | Browser/VS Code cloud container |
| Quick web edit | github.dev | Lightweight browser editor |
| AI coding assistance | GitHub Copilot | Suggestions/chat/agent support |
| Visual backlog/roadmap | GitHub Projects | Flexible project tracking |
| Group issues for release | Milestone | Release/target grouping |
| Categorize issues | Labels | Metadata and filtering |
| Non-code issue manager | Triage role | Manage issues without write access |
| Active code contributor | Write role | Push branches/contribute code |
| Manage repo without destructive actions | Maintain role | Maintenance permissions |
| Full sensitive repo control | Admin role | Manage access/security/delete |
| Protect account login | 2FA/passkeys | Strong authentication |
| Copy repo to contribute without write access | Fork | Personal server-side copy |
| Start standardized new repo | Template repository | Reusable starter structure |
| Share small snippet | Gist | Lightweight code/text sharing |
| Publish static site | GitHub Pages | Public website hosting |
| Find reusable actions/apps | GitHub Marketplace | Integrations and automations |
| Apply open-source practices internally | InnerSource | Internal collaboration model |

---

# Syntax and Configuration Pack

## Markdown Task List

```markdown
## Acceptance Criteria
- [ ] Login page displays validation messages
- [ ] Tests pass in CI
- [ ] Documentation is updated
```

## Issue Template Example

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

## Pull Request Template Example

```markdown
## Summary
Describe the change.

## Testing
- [ ] Unit tests pass
- [ ] Manual validation completed

## Linked issue
Fixes #123
```

## CODEOWNERS Example

```text
# Global owner
* @org/core-maintainers

# Documentation owners
/docs/ @org/docs-team

# Security-sensitive areas
/security/ @org/security-team
```

## Branch Workflow Commands

```bash
git checkout main
git pull origin main
git checkout -b feature/new-report
# make changes
git add .
git commit -m "Add new report documentation"
git push origin feature/new-report
```

## Basic GitHub Actions Workflow

```yaml
name: Pull Request Checks

on:
  pull_request:
    branches: [ main ]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Validate
        run: echo "Run validation here"
```

## Dependabot Configuration Example

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
```

## Dev Container Example

```json
{
  "name": "GH-900 Practice Dev Container",
  "image": "mcr.microsoft.com/devcontainers/base:ubuntu",
  "features": {
    "ghcr.io/devcontainers/features/github-cli:1": {}
  }
}
```

---

# Expanded TOP 150 Must-Memorize GH-900 Facts

## Git and GitHub Basics
1. Git is a distributed version control system.
2. GitHub is a cloud platform for hosting Git repositories and collaboration.
3. A repository stores project files and history.
4. A commit is a saved snapshot of changes.
5. A branch is an independent line of development.
6. The default branch is commonly named `main`.
7. A clone is a local copy of a repository.
8. A fork is your GitHub-hosted copy of someone else's repository.
9. A pull request proposes merging changes from one branch into another.
10. GitHub Flow is branch, commit, pull request, review, merge.
11. Use branches to isolate work.
12. Use commits to record meaningful units of change.
13. Use pull requests for review and collaboration.
14. Use Markdown for structured communication in GitHub.
15. GitHub Desktop is a GUI for Git/GitHub workflows.
16. GitHub Mobile helps with notifications, triage, and collaboration on the go.
17. github.dev is best for quick browser-based edits.
18. Codespaces is best for full cloud development.
19. Organizations manage shared repositories and teams.
20. Enterprise accounts centralize policies across organizations.

## Repository Management
21. README.md is the repository landing page.
22. LICENSE defines permissions and restrictions for reuse.
23. CONTRIBUTING.md explains how to contribute.
24. CODEOWNERS defines file/path ownership for reviews.
25. SECURITY.md explains how to report vulnerabilities.
26. .gitignore excludes local/build/secret files from being tracked.
27. Issue templates standardize bug/feature reports.
28. Pull request templates standardize review context.
29. Repository templates help create standardized new repositories.
30. Topics improve repository discoverability.
31. Stars can bookmark or signal interest in a repo.
32. Forks help users contribute or experiment without write access.
33. Repository insights show activity and health signals.
34. Dependency insights help understand project dependencies.
35. Archive inactive repositories when they should become read-only.

## Collaboration
36. Issues track bugs, tasks, and feature requests.
37. Pull requests review and merge changes.
38. Discussions support open-ended Q&A and conversations.
39. Labels categorize issues and pull requests.
40. Assignees show responsibility.
41. Milestones group issues and pull requests toward a target.
42. Filters help find issues/PRs by metadata.
43. Notifications help manage watched, mentioned, assigned, and participating activity.
44. Gists share small snippets or notes.
45. Wikis provide repository documentation pages.
46. GitHub Pages hosts static websites.
47. Linking PRs to issues improves traceability.
48. `Fixes #123` can close an issue when the PR merges.
49. Draft pull requests signal work is not ready for final review.
50. Required reviews enforce PR review workflow.

## Modern Development Practices
51. GitHub Actions automates CI/CD and repository workflows.
52. Workflows are YAML files in `.github/workflows`.
53. Events trigger workflows.
54. Jobs group steps on a runner.
55. Steps run commands or actions.
56. Actions are reusable automation components.
57. Runners execute jobs.
58. GitHub-hosted runners are managed by GitHub.
59. Self-hosted runners are managed by you.
60. Matrix builds test multiple variations.
61. Secrets should store sensitive values for workflows.
62. Copilot is an AI coding assistant.
63. Copilot suggestions must be reviewed.
64. Copilot Chat can explain, refactor, and help debug code.
65. Copilot plans differ for individuals, businesses, and enterprises.
66. Codespaces provides cloud-hosted dev environments.
67. Dev containers define repeatable development environments.
68. Codespaces can be accessed from browser, VS Code, or GitHub CLI.
69. github.dev does not provide the same compute/runtime as Codespaces.
70. Do not paste sensitive data into AI prompts.

## Projects and Planning
71. GitHub Projects tracks work across issues and pull requests.
72. Projects can use table, board, and roadmap layouts.
73. Custom fields add metadata like priority or target date.
74. Project workflows automate project item updates.
75. Project insights show charts and progress.
76. Draft issues capture planning items before formal issues.
77. Labels categorize; milestones group; projects visualize/manage.
78. Saved replies speed up repeated communication.
79. Assignees clarify ownership.
80. Roadmap view is best for timeline planning.

## Privacy, Security, and Administration
81. 2FA adds an extra login factor.
82. Passkeys provide modern passwordless authentication.
83. Repository visibility can be public, private, or internal where supported.
84. Read role is for viewing and discussion.
85. Triage role manages issues/PRs without code write access.
86. Write role allows active contribution.
87. Maintain role manages repository without sensitive/destructive actions.
88. Admin role provides full repository control.
89. Use least privilege for repository access.
90. Teams simplify permission management.
91. Outside collaborators are non-members with repo access.
92. Branch protection prevents unsafe changes to important branches.
93. Required status checks enforce tests/builds before merge.
94. CODEOWNERS can enforce ownership-based review.
95. EMUs are enterprise-managed GitHub user accounts.
96. Organization-wide Copilot policies help govern AI use.
97. Secret scanning helps detect exposed secrets where enabled.
98. Never commit secrets to a repository.
99. Use Actions secrets for workflow credentials.
100. Admin is not the answer when a smaller role satisfies the requirement.

## Community and Open Source
101. Open source depends on a license for reuse rights.
102. GitHub Sponsors supports maintainers financially.
103. Following users/orgs helps track activity.
104. GitHub Marketplace provides apps, Actions, and integrations.
105. InnerSource applies open-source practices inside organizations.
106. Forks support external contribution.
107. Templates support standardized new projects.
108. Discoverable repositories use README, topics, license, and good metadata.
109. Community standards improve open-source readiness.
110. Public repos are visible to everyone.

## Exam Traps
111. Git is not GitHub.
112. Clone is not fork.
113. Branch is not fork.
114. README is not LICENSE.
115. CONTRIBUTING is not CODEOWNERS.
116. SECURITY.md is not secret scanning.
117. Issue is not pull request.
118. Discussion is not issue when work tracking is required.
119. Wiki is not GitHub Pages.
120. github.dev is not Codespaces.
121. Actions workflow is not a single action.
122. Runner is the machine; workflow is the automation definition.
123. Job contains steps; step can run an action.
124. Secrets should not be stored in YAML or README.
125. Required checks are enforced through branch protection/rulesets.
126. Triage role does not allow pushing code.
127. Read role can view but not manage labels broadly.
128. Maintain is not full Admin.
129. GitHub Projects are not the same as classic milestones.
130. Milestones are good for releases; Projects are flexible planning views.
131. Forking creates a server-side copy under your account.
132. Template creates a new independent repository from a pattern.
133. Pull requests are for proposed changes, not just discussion.
134. Draft PR means not ready for final review.
135. CODEOWNERS requires compatible branch protection/rules to enforce required review.
136. Copilot output should be tested and reviewed.
137. Codespaces cost/quotas can matter in real usage, but exam focuses mainly on purpose.
138. Open source does not mean no license is needed.
139. InnerSource is internal, not public open source.
140. GitHub Marketplace is for integrations and apps, not repository hosting.
141. Passkeys/2FA protect account sign-in, not branch workflows.
142. Branch protection protects code workflow, not account login.
143. .gitignore is not a security boundary for already-committed secrets.
144. Repository insights are for visibility, not deployment.
145. Dependency graph shows dependencies, not Git history.
146. Use issues for trackable work, discussions for broad conversations.
147. Use PR templates to improve review quality.
148. Use issue templates to improve triage quality.
149. Use least privilege for users, teams, and collaborators.
150. GH-900 tests terminology and scenario selection more than deep coding syntax.

---

# Final 50 Practice Questions - Scenario Style

## Domain 1 - Git and GitHub Basics
1. A developer needs to save project history locally and work while offline. What tool is involved?  
   **Answer:** Git.
2. A team needs a cloud platform for pull requests, issues, and Actions. What should they use?  
   **Answer:** GitHub.
3. You need to work on a feature without affecting `main`. What should you create?  
   **Answer:** A branch.
4. You need to propose your branch changes for review. What should you open?  
   **Answer:** A pull request.
5. You do not have write access to an open-source repo but want to propose a change. What should you do first?  
   **Answer:** Fork the repository, make changes, and open a pull request.
6. You want to copy a repository locally with full history. What command/action is this?  
   **Answer:** Clone.
7. Which workflow uses branch, commit, pull request, review, merge?  
   **Answer:** GitHub Flow.

## Domain 2 - Repositories
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
14. A repo should become read-only because development stopped. What should you do?  
   **Answer:** Archive the repository.

## Domain 3 - Collaboration
15. Where should a bug be tracked?  
   **Answer:** Issue.
16. Where should a code change be reviewed before merge?  
   **Answer:** Pull request.
17. Where should a broad community Q&A topic be started?  
   **Answer:** Discussion.
18. Which feature categorizes issues as bug or enhancement?  
   **Answer:** Labels.
19. Which feature groups issues for a release target?  
   **Answer:** Milestone.
20. Which phrase can close issue 25 when a PR merges?  
   **Answer:** `Fixes #25`, `Closes #25`, or `Resolves #25`.
21. You need to publish a static documentation website from a repo. What should you use?  
   **Answer:** GitHub Pages.
22. You need to share a short code snippet. What should you use?  
   **Answer:** Gist.

## Domain 4 - Modern Development
23. You need tests to run on every pull request. What should you use?  
   **Answer:** GitHub Actions.
24. In Actions, what starts a workflow?  
   **Answer:** An event.
25. In Actions, what executes jobs?  
   **Answer:** A runner.
26. In Actions, where are workflow files stored?  
   **Answer:** `.github/workflows`.
27. You need to test on multiple operating systems. What Actions feature helps?  
   **Answer:** Matrix strategy.
28. You need AI coding suggestions and chat assistance. What should you use?  
   **Answer:** GitHub Copilot.
29. A developer needs a complete cloud dev environment with terminal and dependencies. What should they use?  
   **Answer:** GitHub Codespaces.
30. A developer only needs to quickly edit README in browser. What can they use?  
   **Answer:** github.dev or GitHub web editor.
31. A team wants consistent development environments. What should they define?  
   **Answer:** Dev container configuration.

## Domain 5 - Projects
32. A team wants a Kanban view of work. What should they use?  
   **Answer:** GitHub Projects board layout.
33. A team wants a timeline roadmap. What should they use?  
   **Answer:** GitHub Projects roadmap layout.
34. A team wants to track priority and effort fields. What Projects feature helps?  
   **Answer:** Custom fields.
35. A support user sends the same triage answer often. What should they use?  
   **Answer:** Saved replies.
36. A team wants progress charts from tracked items. What should they use?  
   **Answer:** Project insights.

## Domain 6 - Security/Admin
37. A user account needs stronger sign-in protection. What should be enabled?  
   **Answer:** 2FA or passkeys.
38. Stakeholders need to view and comment but not push code. Which repository role fits?  
   **Answer:** Read.
39. A user must manage labels and issues but not push code. Which role fits?  
   **Answer:** Triage.
40. A developer must push code. Which role fits?  
   **Answer:** Write.
41. A project manager must manage repo settings but not destructive actions. Which role fits?  
   **Answer:** Maintain.
42. Someone must manage access and security settings. Which role fits?  
   **Answer:** Admin.
43. You must prevent direct pushes to `main`. What should be configured?  
   **Answer:** Branch protection or repository ruleset.
44. You must require tests before merging. What should be configured?  
   **Answer:** Required status checks.
45. An enterprise wants centrally managed GitHub user accounts. What feature fits?  
   **Answer:** Enterprise Managed Users.

## Domain 7 - Community
46. A maintainer wants financial support from users. What feature helps?  
   **Answer:** GitHub Sponsors.
47. A team wants reusable GitHub apps/actions. Where should they look?  
   **Answer:** GitHub Marketplace.
48. A company wants open-source-style collaboration internally. What is this called?  
   **Answer:** InnerSource.
49. A user wants to follow project activity from an organization. What should they do?  
   **Answer:** Follow the organization or watch/star relevant repositories.
50. A team wants to make new repos from a standard starter repository. What should they use?  
   **Answer:** Template repository.

---

# 7-Day Last-Moment Revision Plan

| Day | Focus |
|---:|---|
| 1 | Git vs GitHub, repositories, commits, branches, clone/fork/pull/push, GitHub Flow |
| 2 | Repository files: README, LICENSE, CONTRIBUTING, CODEOWNERS, SECURITY, templates, insights |
| 3 | Issues, pull requests, discussions, notifications, Gists, Wikis, Pages |
| 4 | GitHub Actions, Copilot, Codespaces, dev containers, github.dev |
| 5 | GitHub Projects, labels, milestones, assignees, saved replies, insights |
| 6 | Security/admin: 2FA, passkeys, roles, teams, branch protection, EMUs, Copilot policy |
| 7 | Open source, Sponsors, Marketplace, InnerSource, final cheat sheet and practice questions |

---

# Final Revision Checklist

Before the exam, confirm you can explain each of these without notes:

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
- Copilot purpose and plan-level idea.
- Codespaces vs github.dev.
- Dev containers and repeatable environments.
- Project layouts: table, board, roadmap.
- Repository roles: Read, Triage, Write, Maintain, Admin.
- Public vs private vs internal repositories.
- 2FA/passkeys vs branch protection.
- Required reviews, required status checks, CODEOWNERS.
- Organizations, teams, outside collaborators, enterprise accounts, EMUs.
- Open source, Sponsors, Marketplace, InnerSource.

---

# Source and Validation Notes

This study guide was prepared from the current Microsoft Learn GH-900 study guide and supporting GitHub Docs pages covering GitHub Flow, Actions, Copilot, Codespaces, Projects, repository roles, and GitHub community/repository collaboration concepts. It is designed as a practical, exam-focused study material and not a replacement for hands-on practice in GitHub.

Primary source areas used for alignment:

- Microsoft Learn GH-900 Study Guide, skills at a glance as of January 2026.
- GitHub Docs: GitHub Flow, Actions, Copilot, Codespaces, Projects, repository roles, repositories, issues, pull requests, discussions, notifications, Gists, Wikis, Pages, and community topics.
