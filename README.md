# 🤖 AI Runner Reusable Workflows

Central, reusable GitHub Actions workflows for self-hosted AI-driven Pull Request management, automated merge conflict resolution, test safety guards, and first-pass code reviews with `@jules` tasking.

---

## 📦 Available Reusable Workflows

| Workflow | File | Description |
| :--- | :--- | :--- |
| **All-in-One Suite** | [`.github/workflows/reusable-ai-triage.yml`](.github/workflows/reusable-ai-triage.yml) | Runs both conflict resolution and first-pass review |
| **Conflict Resolver** | [`.github/workflows/reusable-conflict-resolver.yml`](.github/workflows/reusable-conflict-resolver.yml) | Auto-resolves git merge conflicts with local LLM + safety test guard |
| **AI Reviewer** | [`.github/workflows/reusable-reviewer.yml`](.github/workflows/reusable-reviewer.yml) | Analyzes diffs, generates checklists, and tasks `@jules` |

---

## 🚀 Quickstart: How to Use in Any Repository

In any of your target repositories (e.g. `SirLocke/MyProject`), create a single file:

### Option 1: All-in-One AI Suite (Recommended)

Create `.github/workflows/ai-triage.yml`:

```yaml
name: AI Triage & Review

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  ai-suite:
    uses: SirLocke/ai-runner-workflows/.github/workflows/reusable-ai-triage.yml@main
    secrets: inherit
```

---

### Option 2: Conflict Resolver Only

Create `.github/workflows/ai-conflict-resolver.yml`:

```yaml
name: Conflict Resolver

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  resolve-conflicts:
    uses: SirLocke/ai-runner-workflows/.github/workflows/reusable-conflict-resolver.yml@main
    with:
      auto_push: true
    secrets: inherit
```

---

### Option 3: AI Reviewer with Jules Tasking Only

Create `.github/workflows/ai-reviewer.yml`:

```yaml
name: AI Reviewer

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  code-review:
    uses: SirLocke/ai-runner-workflows/.github/workflows/reusable-reviewer.yml@main
    with:
      mention_jules: true
    secrets: inherit
```

---

## ⚙️ Requirements on Runner Host

These workflows execute on self-hosted runners labeled `[self-hosted, oracle-ai-runner]` where:
- The `ai-runner` CLI (`/opt/ai-runner-tools`) is installed.
- The local OpenAI-compatible LLM endpoint is active (`http://127.0.0.1:8080/v1`).
