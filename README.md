# Claude Code Project Scaffolder

> A meta-project for setting up new Claude Code projects with optimal CLAUDE.md files, agent configurations, and skill definitions.

## What This Project Does

This repository is a **meta-scaffolding system** for Claude Code that helps developers quickly bootstrap new projects with optimal Claude Code integration.

### Core Capabilities

#### 1. Automated Project Setup
Provides slash commands that can:
- Analyze existing codebases to understand their tech stack and structure
- Generate customized CLAUDE.md files tailored to specific project types (React, Python, full-stack)
- Create custom slash commands for common workflows
- Set up specialized subagents for delegated tasks
- Generate agent skills for domain-specific capabilities

#### 2. Template Library
Includes production-ready templates for:
- **4 CLAUDE.md templates**: Minimal, React/TypeScript, Python API, and Full-stack
- **3 slash command templates**: Code review, test-and-commit, and fix-issue workflows
- **3 subagent templates**: Code-reviewer, debugger, and researcher specialists
- **Skill templates**: Base templates for creating new agent skills

#### 3. Best Practice Documentation
Comprehensive guides covering:
- How to write effective CLAUDE.md files (keep them under 200 lines, focus on actionable instructions)
- Agent workflow patterns (explore → plan → code → verify → commit)
- Creating and using subagents for specialized tasks
- Developing agent skills with progressive disclosure
- Context management strategies

## Quick Start

### Available Commands

```bash
# Scaffolding commands
/project:scaffold         # Interactive project setup wizard
/project:scaffold-react   # Quick React/TypeScript project
/project:scaffold-python  # Quick Python API project

# CLAUDE.md commands
/project:generate-claude-md    # Generate CLAUDE.md from project analysis

# Customization commands
/project:create-subagent  # Create a specialized subagent
/project:create-skill     # Create a new agent skill
```

### Example: Setting Up a New React Project

1. Run `/project:scaffold-react`
2. System prompts for project details
3. Generates CLAUDE.md from react-typescript.md template with Vite, React, TypeScript configs
4. Sets up ESLint, Prettier, Vitest
5. Creates basic src/ structure
6. Provides verification commands and next steps

### Example: Analyzing an Existing Python Project

1. Run `/project:generate-claude-md /path/to/project`
2. Spawns project-analyzer subagent
3. Analyzer detects FastAPI project from imports and pyproject.toml
4. Maps directory structure and extracts scripts
5. Selects python-api.md template
6. Generates customized CLAUDE.md with actual project structure

## Project Structure

```
project-scaffolder/
├── CLAUDE.md                    # Main project documentation
├── .claude/
│   ├── commands/               # Custom slash commands
│   │   ├── scaffold.md
│   │   ├── scaffold-react.md
│   │   ├── scaffold-python.md
│   │   ├── generate-claude-md.md
│   │   ├── create-skill.md
│   │   └── create-subagent.md
│   └── agents/                 # Subagent definitions
│       └── project-analyzer.md
├── templates/                   # Project templates
│   ├── claude-md/              # CLAUDE.md templates by project type
│   │   ├── react-typescript.md
│   │   ├── python-api.md
│   │   ├── fullstack.md
│   │   └── minimal.md
│   ├── commands/               # Slash command templates
│   │   ├── review.md
│   │   ├── test-and-commit.md
│   │   └── fix-issue.md
│   ├── agents/                 # Subagent templates
│   │   ├── code-reviewer.md
│   │   ├── debugger.md
│   │   └── researcher.md
│   └── skills/                 # Skill templates
│       └── SKILL.template.md
├── skills/                      # This project's skills
│   └── project-setup/
│       └── SKILL.md
└── docs/
    ├── best-practices.md       # CLAUDE.md best practices
    ├── agent-patterns.md       # Common agent patterns
    ├── skill-guide.md          # How to write skills
    └── subagent-guide.md       # How to create subagents
```

## Key Components

### Slash Commands (`.claude/commands/`)

| Command | Purpose |
|---------|---------|
| `/project:scaffold` | Interactive wizard for complete project setup |
| `/project:scaffold-react` | Quick React + TypeScript + Vite setup |
| `/project:scaffold-python` | Quick Python FastAPI setup |
| `/project:generate-claude-md` | Analyze projects and generate CLAUDE.md |
| `/project:create-skill` | Create new agent skills |
| `/project:create-subagent` | Create specialized subagents |

### Custom Subagent

**project-analyzer** (Haiku-powered)
- Analyzes codebases to detect project types
- Maps directory structures
- Extracts commands from config files
- Identifies coding patterns and conventions
- Used automatically by `/project:generate-claude-md`

### CLAUDE.md Templates

#### minimal.md (~35 lines)
For simple projects or when starting fresh:
- Project name and purpose
- Essential commands only
- Key files to know about
- Basic verification steps

#### react-typescript.md (~150 lines)
For React + TypeScript projects:
- Tech stack: Vite, ESLint, Prettier, Vitest
- Component structure and naming conventions
- TypeScript patterns (props interfaces, hooks typing)
- Code patterns (components, custom hooks, data fetching)
- Verification checklist (type-check, lint, test, build)
- Common tasks walkthrough

#### python-api.md (~140 lines)
For Python FastAPI projects:
- Virtual environment setup instructions
- Project structure (app, models, schemas, API routes)
- Database configuration (SQLAlchemy, Alembic migrations)
- Code patterns (REST endpoints, Pydantic models, error handling)
- Commands for dev server, testing (pytest), linting (ruff)
- Common tasks (adding endpoints, models, background tasks)

#### fullstack.md (~180 lines)
For full-stack applications:
- Architecture overview (frontend → backend → database flow)
- Separate tech stacks for each layer
- Coordinated project structure
- Commands for both components
- Development workflow (backend first, then frontend)
- API contract management

## Design Philosophy

### 1. Progressive Disclosure
Only load what's needed when it's needed:
- CLAUDE.md contains universal instructions only
- Slash commands contain workflow-specific details
- Skills contain specialized domain knowledge
- External docs contain context-specific information
- **Result**: Reduced context window usage, faster responses

### 2. WHAT/WHY/HOW Framework
Every CLAUDE.md should answer:
- **WHAT**: Tech stack, project structure, key files
- **WHY**: Purpose, architectural decisions
- **HOW**: Commands to run, how to verify changes, file boundaries

### 3. Actionable Over Explanatory
- Tell Claude HOW to do things, not just WHAT to do
- Provide concrete commands: `npm run typecheck`, `pytest`
- Include verification steps for every action
- Define safe boundaries: safe to edit vs. never touch

### 4. Linters Over Guidelines
Never send an LLM to do a linter's job:
- Don't include style rules in CLAUDE.md
- Reference linter/formatter configs instead: "Follow ESLint rules"
- Use git hooks to run formatters automatically
- Let tools enforce standards, let CLAUDE.md guide behavior

### 5. The Agent Loop
Recommended workflow pattern for all tasks:

```
GATHER CONTEXT → PLAN → EXECUTE → VERIFY → COMMIT
```

1. **Gather**: Read relevant files, understand scope
2. **Plan**: Think through approach before coding
3. **Execute**: Implement in small, verifiable chunks
4. **Verify**: Run tests, linters, type checks
5. **Commit**: Create descriptive commit messages

## Documentation

### [best-practices.md](docs/best-practices.md)
- Optimal CLAUDE.md length: 30-200 lines depending on complexity
- What to include vs. what to avoid
- Common mistakes and anti-patterns
- Template structures (minimal and standard)

### [agent-patterns.md](docs/agent-patterns.md)
- Common workflow patterns (Explore → Plan → Code → Commit, TDD, Visual Iteration)
- Agent architectures (Simple, Orchestrator-Workers, Evaluator-Optimizer)
- Context management strategies
- Tool design principles
- Multi-agent patterns and subagent chaining

### [skill-guide.md](docs/skill-guide.md)
- What skills are and why they matter
- Skill anatomy and structure
- Creating effective skills
- Skill patterns: How-To, Integration, Quality, Template
- Security considerations

### [subagent-guide.md](docs/subagent-guide.md)
- When to use subagents
- Subagent file format and configuration
- Writing effective descriptions and system prompts
- Advanced features (chaining, resumable subagents)
- Best practices and troubleshooting

## Template Examples

### Slash Command Templates

**review.md** - Code Review Automation
- Quality checks (naming, function length, pattern adherence)
- Error handling verification
- Security analysis (secrets, input validation, SQL/XSS injection)
- Performance considerations
- Test coverage verification
- Outputs findings by severity: Critical → Important → Suggestions → Highlights

**test-and-commit.md** - Quality Gate + Git Workflow
- Runs git status and language-specific checks
- TypeScript: typecheck → lint → test → build
- Python: mypy → ruff → pytest
- Auto-generates conventional commit messages
- Shows next steps

**fix-issue.md** - GitHub Issue Resolution
- Fetches issue details via `gh` CLI
- Creates implementation plan
- Implements fix incrementally with tests
- Creates commit and PR with issue reference

### Subagent Templates

**code-reviewer.md** (Sonnet)
- Security, code quality, and best practices specialist
- Checks quality, error handling, security, performance, testing
- Outputs organized by severity with line numbers

**debugger.md** (Sonnet)
- Root cause analysis specialist
- Systematic hypothesis testing
- Output: Problem → Root Cause → Evidence → Fix → Verification → Prevention

**researcher.md** (Haiku)
- Fast, read-only codebase research
- Configurable thoroughness levels
- Output: Key Findings → Relevant Files → Patterns → Recommendations

## Current Status

### What's Complete ✅
- Full template library for common project types
- Comprehensive documentation of best practices
- Working slash commands for scaffolding
- Custom subagent for project analysis
- Skill system with project-setup skill
- Templates for common workflows

### What's Template-Only 📝
- Code reviewer/debugger/researcher subagents (templates exist, not installed)
- Review/test-and-commit/fix-issue commands (templates exist, not installed)

### What's Missing ⚠️
- MCP server configurations (.mcp.json templates)
- Git hook implementations
- Actual scaffolding scripts (commands reference them)
- Template testing/validation system

## Use Cases

This project is ideal for:
- Quickly setting up new projects with Claude Code integration
- Learning Claude Code best practices
- Creating specialized subagents for your workflow
- Building custom slash commands for repetitive tasks
- Understanding effective agent patterns
- Maintaining clean, concise CLAUDE.md files

## Bottom Line

This is a **meta-project that scaffolds the scaffolding infrastructure** for Claude Code projects. It's a comprehensive toolkit that makes it fast and easy to integrate Claude Code into any development workflow by providing templates, best practices, and automation for setting up optimal Claude Code configurations.

The repository itself demonstrates best practices by being a working example of how to structure a Claude Code project with custom commands, subagents, skills, and documentation.

## Learn More

- [CLAUDE.md](CLAUDE.md) - Full project documentation and instructions
- [docs/best-practices.md](docs/best-practices.md) - CLAUDE.md development guidelines
- [docs/agent-patterns.md](docs/agent-patterns.md) - Effective agent workflows
- [docs/skill-guide.md](docs/skill-guide.md) - Creating agent skills
- [docs/subagent-guide.md](docs/subagent-guide.md) - Creating subagents

## Reference Documentation

Before scaffolding projects, consult these authoritative sources:
- [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents)
- [Agent Skills Guide](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- [Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk)
- [Subagents Documentation](https://code.claude.com/docs/en/sub-agents)
- [CLAUDE.md Files Guide](https://www.claude.com/blog/using-claude-md-files)
