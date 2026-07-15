# ProjectForge for Codex

## Installation

Copy the complete `projectforge` folder into your Codex skills directory.

### Personal installation

```text
~/.codex/skills/projectforge/
├── SKILL.md
└── README.md
```

Example shell command:

```bash
mkdir -p ~/.codex/skills
cp -R projectforge ~/.codex/skills/projectforge
```

Restart Codex or begin a new Codex session after installation. The registered skill name is `projectforge`.

## Use Cases

- Define maintainable code structure, feature boundaries, dependency direction, public exports, and test placement

- Compare viable technical approaches and recommend the best option before creating an implementation plan

Use `projectforge` in Codex when you need to:

- Analyze an existing repository before editing it
- Convert an application idea, issue, or PRD into an implementation plan
- Build a complete feature across frontend, backend, database, and tests
- Choose system architecture and detailed system design
- Organize a codebase using module-based, feature-based, or hybrid architecture
- Apply senior-level code-quality, readability, understandability, folder, export, and filename standards
- Optimize frontend, backend, API, database, memory, and bundle performance using profiling and before/after evidence
- Refactor a growing application without breaking public behaviour
- Add tests and implement changes using a test-first workflow
- Review the final diff and verify tests, linting, types, and builds
- Prepare an application change for review, deployment, and maintenance

### Example Codex prompts

```text
Use projectforge to inspect this repository and implement user authentication.
```

```text
Use projectforge to convert this issue into a plan, write failing tests, implement the fix, and verify it.
```

```text
Use projectforge to design and build a URL-shortener MVP in this repository.
```

```text
Use projectforge to reorganize this React project into a feature-based architecture while preserving behaviour.
```

```text
Use projectforge to review this codebase for clean-code and filename problems, then fix the highest-impact issues.
```

```text
Use projectforge to define the system architecture, API design, database model, tests, and implementation steps for this SaaS feature.
```

```text
Use projectforge as a senior programmer to review this change for correctness, readability, understandability, error handling, tests, and maintainability, then fix the problems.
```

```text
Use projectforge to inspect this repository, compare the best implementation approaches, recommend one with trade-offs, and then create the implementation plan.
```

```text
Use projectforge to profile this code, identify the real bottleneck, recommend the safest optimization, implement it, and report before-and-after evidence.
```

```text
Use projectforge to review this repository structure, recommend the best module or feature boundaries, and refactor it without changing behaviour.
```
