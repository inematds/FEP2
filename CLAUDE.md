# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

FEP2 is a **BMad Method v4.44.3** installation - a framework for AI-driven agile development. This is a configuration/orchestration project, not an application codebase. It provides specialized AI agents, workflows, templates, and tasks for structured software development.

## Key Commands

```bash
# Install/refresh BMad framework
npx bmad-method install

# Refresh for specific IDE (Claude Code is pre-configured)
npx bmad-method install -f -i claude-code
```

## Agent System

Invoke agents with slash commands in Claude Code:

| Agent | Command | Purpose |
|-------|---------|---------|
| Developer | `/dev` | Code implementation, debugging, task execution |
| Scrum Master | `/sm` | Story creation with `*draft` command |
| Product Owner | `/po` | Document validation, master checklist |
| QA (Quinn) | `/qa` | Test architecture, quality gates |
| Architect | `/architect` | System design, architecture docs |
| PM | `/pm` | PRD creation, roadmap |
| Analyst | `/analyst` | Market research, project briefs |
| BMad-Master | `/bmad-master` | Multi-role orchestrator (prefer over BMad-Orchestrator in IDE) |

## Development Workflow

### Story Cycle
1. **SM**: `*draft` - Creates story in `docs/stories/`
2. **Dev**: `*develop-story {story}` - Implements with task checklist
3. **QA**: `*review {story}` - Quality gate assessment

### QA Commands (Test Architect)
```bash
@qa *risk {story}    # Risk assessment (before dev)
@qa *design {story}  # Test strategy (before dev)
@qa *trace {story}   # Coverage verification (during dev)
@qa *nfr {story}     # Non-functional requirements (during dev)
@qa *review {story}  # Full assessment (after dev) - REQUIRED
@qa *gate {story}    # Update quality decision (post-review)
```

## Project Structure

```
.bmad-core/              # Framework core (DO NOT modify unless updating BMad)
├── agents/              # 10 AI agent definitions
├── tasks/               # 23 executable task workflows
├── templates/           # 13 YAML document templates
├── workflows/           # Greenfield/Brownfield workflow definitions
├── checklists/          # QA checklists (PO, architect, story DoD)
├── data/                # Knowledge base, technical preferences
├── core-config.yaml     # Project configuration
└── user-guide.md        # Full BMad documentation

docs/                    # Project documentation (created during development)
├── prd.md              # Product Requirements Document
├── architecture.md     # System architecture
├── prd/                # Sharded PRD sections
├── architecture/       # Sharded architecture sections
├── stories/            # Development stories
└── qa/                 # QA assessments and gates

ref/                     # Reference materials
├── MASTER_COMPLETO.md  # Course template guide (HTML/Tailwind patterns)
└── CHECKLIST_REVISAO.md # Implementation review checklist
```

## Core Configuration

Located at `.bmad-core/core-config.yaml`:

- **devLoadAlwaysFiles**: Files the dev agent loads on startup (coding-standards, tech-stack, source-tree)
- **prdShardedLocation**: `docs/prd` - Sharded PRD location
- **architectureShardedLocation**: `docs/architecture` - Sharded architecture location
- **devStoryLocation**: `docs/stories`
- **qaLocation**: `docs/qa`
- **slashPrefix**: `BMad` (for slash commands)

## Dev Agent Critical Rules

When implementing stories as the Dev agent:
1. Story file contains ALL needed information - do NOT load PRD/architecture unless explicitly directed
2. Only update Dev Agent Record sections in story files (checkboxes, Debug Log, Completion Notes, Change Log, File List)
3. Check existing folder structure before creating directories
4. Execute `*develop-story` to follow the task checklist workflow
5. Run full test suite before marking story complete
6. HALT on: unapproved dependencies, ambiguous requirements, 3+ repeated failures, failing regression

## Quality Gate Statuses

| Status | Meaning | Can Proceed? |
|--------|---------|--------------|
| PASS | All critical requirements met | Yes |
| CONCERNS | Non-critical issues found | With caution |
| FAIL | Critical issues (security, missing P0 tests) | No |
| WAIVED | Issues acknowledged and accepted | With approval |

## Course Template Reference (ref/MASTER_COMPLETO.md)

When building course pages with HTML/Tailwind:
- Buttons always left-aligned (`justify-start`)
- Topic numbers in circles, not arrows
- Each expandable topic needs 3 sections: "O que e", "Por que aprender", "Conceitos-chave"
- Include INEMA.CLUB link (`text-sky-400`) in navigation
- Include light mode CSS overrides in all pages
- Module titles use `text-2xl`
- Color system: Emerald (T1), Blue (T2), Purple (T3), Amber (T4), Teal (T5), Rose (T6)
