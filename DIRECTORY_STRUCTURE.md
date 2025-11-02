# Complete Directory Structure

```
sanity-agent/
├── .claude-plugin/
│   └── marketplace.json                                # Marketplace configuration
│
├── plugins/
│   │
│   ├── sanity-schema-helper/                           # Plugin 1: Schema Architecture
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json                             # Plugin metadata
│   │   ├── commands/
│   │   │   └── create-schema.md                        # /create-schema command
│   │   ├── agents/
│   │   │   └── schema-architect.md                     # Complex schema agent
│   │   └── skills/
│   │       └── sanity-validator/
│   │           └── SKILL.md                            # Auto-validation skill
│   │
│   ├── sanity-groq-assistant/                          # Plugin 2: Query Building
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   └── build-query.md                          # /build-query command
│   │   ├── agents/
│   │   │   └── groq-optimizer.md                       # Query optimization agent
│   │   └── skills/
│   │       └── groq-optimizer/
│   │           └── SKILL.md                            # Auto-optimization skill
│   │
│   ├── sanity-migration-helper/                        # Plugin 3: Migrations
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   └── plan-migration.md                       # /plan-migration command
│   │   ├── agents/
│   │   │   └── migration-architect.md                  # Migration planning agent
│   │   └── skills/
│   │       └── migration-validator/
│   │           └── SKILL.md                            # Migration validation skill
│   │
│   ├── sanity-plugin-creator/                          # Plugin 4: Plugin Development
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   └── create-plugin.md                        # /create-plugin command
│   │   ├── agents/
│   │   │   └── plugin-architect.md                     # Plugin development agent
│   │   └── skills/
│   │       └── plugin-validator/
│   │           └── SKILL.md                            # Plugin validation skill
│   │
│   ├── sanity-structure-builder/                       # Plugin 5: Studio Structure
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   └── build-structure.md                      # /build-structure command
│   │   ├── agents/
│   │   │   └── structure-architect.md                  # Structure design agent
│   │   └── skills/
│   │       └── structure-validator/
│   │           └── SKILL.md                            # Structure validation skill
│   │
│   ├── sanity-widget-creator/                          # Plugin 6: Dashboard Widgets
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   └── create-widget.md                        # /create-widget command
│   │   ├── agents/
│   │   │   └── widget-architect.md                     # Widget development agent
│   │   └── skills/
│   │       └── widget-validator/
│   │           └── SKILL.md                            # Widget validation skill
│   │
│   └── sanity-content-actions/                         # Plugin 7: AI Actions
│       ├── .claude-plugin/
│       │   └── plugin.json
│       ├── commands/
│       │   └── create-content-action.md                # /create-content-action command
│       ├── agents/
│       │   └── action-architect.md                     # Action workflow agent
│       └── skills/
│           └── action-validator/
│               └── SKILL.md                            # Action validation skill
│
├── README.md                                           # Complete documentation
├── QUICKSTART.md                                       # 5-minute setup guide
├── STRUCTURE.md                                        # Architecture overview
├── SUMMARY.md                                          # Project summary
└── DIRECTORY_STRUCTURE.md                             # This file
```

## File Count by Type

### Configuration
- 1 marketplace manifest
- 7 plugin manifests
**Total: 8 JSON files**

### Commands
- 7 interactive command files (one per plugin)

### Agents
- 7 autonomous agent files (one per plugin)

### Skills
- 7 auto-validation skill files (one per plugin)

### Documentation
- 5 documentation files (README, QUICKSTART, STRUCTURE, SUMMARY, DIRECTORY_STRUCTURE)

## Total Files: 35

## Commands Available After Installation

```bash
/create-schema          # Schema architecture
/build-query            # GROQ query building
/plan-migration         # Content migrations
/create-plugin          # Plugin development
/build-structure        # Studio navigation
/create-widget          # Dashboard widgets
/create-content-action  # AI-powered actions
```

## Agents Available

```bash
# Use in conversation:
"Use schema-architect agent to..."
"Use groq-optimizer agent to..."
"Use migration-architect agent to..."
"Use plugin-architect agent to..."
"Use structure-architect agent to..."
"Use widget-architect agent to..."
"Use action-architect agent to..."
```

## Skills (Auto-Activate)

Skills automatically activate when reading:
- Schema files → `sanity-validator`
- Query files → `groq-optimizer`
- Migration files → `migration-validator`
- Plugin files → `plugin-validator`
- Structure files → `structure-validator`
- Widget files → `widget-validator`
- Action files → `action-validator`

## Installation Path

```
1. /plugin marketplace add git@github.com:ncklrs/sanity-agents.git
2. /plugin install [plugin-name]@sanity-marketplace
3. Restart Claude Code
4. Use commands or let skills auto-activate
```

**Alternative (HTTPS)**:
```
1. /plugin marketplace add https://github.com/ncklrs/sanity-agents.git
```

---

**Complete**: All 7 plugins ready for production use
**Architecture**: Three-tier (commands, agents, skills)
**Coverage**: Every aspect of Sanity CMS development
