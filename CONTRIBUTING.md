# Contributing to 7T | المساهمة في مشاريع 7T

شكراً لاهتمامك بالمساهمة في مشاريع 7T! هذا الدليل يوضح كيفية إعداد بيئة التطوير والمساهمة بشكل فعال.

Thank you for your interest in contributing to 7T projects! This guide explains how to set up your development environment and contribute effectively.

---

## Table of Contents | فهرس المحتويات

- [Development Environment Setup](#development-environment-setup)
- [Branching Strategy](#branching-strategy)
- [Pull Request Workflow](#pull-request-workflow)
- [Code Review Process](#code-review-process)
- [Commit Message Conventions](#commit-message-conventions)
- [Getting Help](#getting-help)

---

## Development Environment Setup | إعداد بيئة التطوير

### Prerequisites | المتطلبات الأساسية

Ensure you have the following tools installed before starting:

| Tool | Version | Purpose |
|------|---------|---------|
| Node.js | >= 18.x LTS | JavaScript/TypeScript runtime |
| npm | >= 9.x | Package management |
| Python | >= 3.10 | Python projects and scripting |
| Docker | >= 24.x | Containerization |
| Docker Compose | >= 2.x | Multi-container orchestration |
| Git | >= 2.40 | Version control |
| kubectl | Latest stable | Kubernetes cluster management |

### Step 1: Clone the Repository | استنساخ المستودع

```bash
git clone https://github.com/7T/<repository-name>.git
cd <repository-name>
```

### Step 2: Node.js Projects Setup | إعداد مشاريع Node.js

```bash
# Install dependencies
npm install

# Run the development server
npm run dev

# Run tests
npm test

# Run linting
npm run lint
```

### Step 3: Python Projects Setup | إعداد مشاريع Python

```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Install development dependencies
pip install -r requirements-dev.txt

# Run tests
pytest

# Run linting
flake8 .
```

### Step 4: Docker Setup | إعداد Docker

```bash
# Build the Docker image
docker build -t 7t/<service-name> .

# Run with Docker Compose
docker compose up -d

# View logs
docker compose logs -f

# Stop services
docker compose down
```

### Step 5: Kubernetes (Optional) | إعداد Kubernetes

```bash
# Apply Kubernetes configurations
kubectl apply -f k8s/

# Check pod status
kubectl get pods -n 7t

# View logs
kubectl logs -f deployment/<service-name> -n 7t
```

### IDE Recommendations | التوصيات لبيئة التطوير

- **VS Code** with extensions: ESLint, Prettier, Python, Docker, Kubernetes
- **WebStorm** for full-stack JavaScript/TypeScript projects
- **PyCharm** for Python-specific projects

---

## Branching Strategy | استراتيجية الفروع

We follow a structured branching model to maintain code quality and streamline releases.

نتبع نموذج فروع منظم للحفاظ على جودة الكود وتسهيل عمليات الإصدار.

### Branch Types | أنواع الفروع

| Branch | Purpose | Base Branch | Merges Into |
|--------|---------|-------------|-------------|
| `main` | Production-ready code | - | - |
| `develop` | Integration branch for features | `main` | `main` |
| `feature/*` | New features | `develop` | `develop` |
| `bugfix/*` | Bug fixes | `develop` | `develop` |
| `release/*` | Release preparation | `develop` | `main` & `develop` |
| `hotfix/*` | Critical production fixes | `main` | `main` & `develop` |

### Branch Naming Convention | تسمية الفروع

```
feature/<issue-number>-<short-description>
bugfix/<issue-number>-<short-description>
release/<version>
hotfix/<issue-number>-<short-description>
```

**Examples:**
```
feature/42-add-server-metrics
bugfix/87-fix-health-check-timeout
release/1.2.0
hotfix/91-fix-auth-token-refresh
```

### Branch Lifecycle | دورة حياة الفرع

```
main ─────────────────────────────────────────────►
  │                                    ▲
  └─► develop ──────────────────────── │ ────────►
        │           ▲                  │
        └─► feature/42-add-metrics ────┘
```

1. Create your branch from `develop` (or `main` for hotfixes)
2. Make your changes with atomic commits
3. Push your branch and open a Pull Request
4. After review and approval, merge into the target branch
5. Delete the feature branch after merging

---

## Pull Request Workflow | سير عمل طلبات الدمج

### Creating a Pull Request | إنشاء طلب دمج

1. **Push your branch** to the remote repository
2. **Open a Pull Request** via GitHub with the following details:
   - Clear, descriptive title
   - Description of changes made
   - Reference to related issue(s) using `Closes #<issue-number>`
   - Screenshots or recordings for UI changes
3. **Ensure CI passes** — all automated checks must be green before review

### Pull Request Template | نموذج طلب الدمج

```markdown
## Description | الوصف
Brief description of the changes.

## Type of Change | نوع التغيير
- [ ] New feature (إضافة ميزة جديدة)
- [ ] Bug fix (إصلاح خلل)
- [ ] Breaking change (تغيير جذري)
- [ ] Documentation update (تحديث التوثيق)
- [ ] Infrastructure/CI change (تغيير في البنية التحتية)

## Related Issues | القضايا المرتبطة
Closes #

## Testing | الاختبارات
Describe the tests you ran and their results.

## Checklist | قائمة التحقق
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Tests added/updated and passing
- [ ] Documentation updated (if applicable)
- [ ] No new warnings or errors introduced
```

### Pull Request Requirements | متطلبات طلب الدمج

- All CI/CD checks must pass (linting, tests, type checking)
- At least **1 approving review** required for `develop`
- At least **2 approving reviews** required for `main`
- No unresolved review comments
- Branch must be up-to-date with the target branch
- All conversations must be resolved

---

## Code Review Process | عملية مراجعة الكود

### Review Guidelines for Reviewers | إرشادات للمراجعين

When reviewing code, assess the following:

عند مراجعة الكود، قيّم النقاط التالية:

1. **Correctness (الصحة):** Does the code do what it's supposed to do?
2. **Readability (القراءة):** Is the code clear and easy to understand?
3. **Performance (الأداء):** Are there potential performance issues?
4. **Security (الأمان):** Are there any security vulnerabilities?
5. **Testing (الاختبارات):** Are there adequate tests for the changes?
6. **Documentation (التوثيق):** Is the code properly documented?

### Review Standards | معايير المراجعة

- Respond to review requests within **2 business days**
- Provide constructive, specific feedback with suggestions
- Use GitHub's suggestion feature for small code changes
- Approve when satisfied, or request changes with clear explanations
- Be respectful and professional in all review comments

### Review Labels | تسميات المراجعة

| Label | Meaning |
|-------|---------|
| `nit:` | Minor suggestion, non-blocking |
| `suggestion:` | Recommended improvement |
| `question:` | Seeking clarification |
| `issue:` | Must be addressed before merge |
| `praise:` | Highlighting good work |

### Review Example

```
issue: This function doesn't handle the case where `serverId` is undefined.
Consider adding a null check before the API call.

suggestion: This could be simplified using optional chaining:
`const name = server?.name ?? 'Unknown';`
```

---

## Commit Message Conventions | اتفاقيات رسائل الالتزام

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification.

### Format | الصيغة

```
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

### Types | الأنواع

| Type | Description |
|------|-------------|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation changes only |
| `style` | Code style changes (formatting, no logic change) |
| `refactor` | Code refactoring (no feature or fix) |
| `perf` | Performance improvement |
| `test` | Adding or updating tests |
| `build` | Build system or dependency changes |
| `ci` | CI/CD configuration changes |
| `chore` | Other changes (tooling, configs) |

### Examples | أمثلة

```bash
feat(api): add server metrics endpoint
fix(health-check): correct timeout calculation for retry logic
docs(readme): update setup instructions for Docker
test(sdk): add property tests for parameter validation
ci(workflows): configure shared pipeline for Python projects
refactor(dashboard): simplify server list component
```

### Breaking Changes | التغييرات الجذرية

```bash
feat(api)!: redesign server creation endpoint

BREAKING CHANGE: The `create` endpoint now requires a `resources` object
instead of individual `cpu`, `memory`, and `disk` parameters.
```

---

## Getting Help | الحصول على المساعدة

- **Questions?** Open a [Discussion](https://github.com/orgs/7T/discussions) on GitHub
- **Found a bug?** Open an [Issue](https://github.com/7T/<repo>/issues) using the bug report template
- **Feature idea?** Open an [Issue](https://github.com/7T/<repo>/issues) using the feature request template
- **Security concern?** Email security@7t.dev directly (do not open a public issue)

---

## License | الرخصة

By contributing to 7T projects, you agree that your contributions will be licensed under the same license as the project you are contributing to.

بمساهمتك في مشاريع 7T، فإنك توافق على أن مساهماتك ستكون مرخصة بنفس رخصة المشروع الذي تساهم فيه.

---

**Thank you for contributing to 7T! Together we build better software. 🚀**

**شكراً لمساهمتك في مشاريع 7T! معاً نبني برمجيات أفضل. 🚀**
