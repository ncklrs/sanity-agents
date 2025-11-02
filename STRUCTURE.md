# Marketplace Structure

Complete file structure for the Sanity CMS Plugin Marketplace.

```
sanity-agent/
│
├── .claude-plugin/
│   └── marketplace.json                    # Marketplace manifest
│
├── plugins/
│   │
│   ├── sanity-schema-helper/               # Plugin 1: Schema Architecture
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json                 # Plugin metadata
│   │   ├── commands/
│   │   │   └── create-schema.md            # /create-schema command
│   │   ├── agents/
│   │   │   └── schema-architect.md         # Deep-dive schema agent
│   │   └── skills/
│   │       └── sanity-validator/
│   │           └── SKILL.md                # Auto-validation skill
│   │
│   ├── sanity-groq-assistant/              # Plugin 2: GROQ Query Builder
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── commands/
│   │   │   └── build-query.md              # /build-query command
│   │   ├── agents/
│   │   │   └── groq-optimizer.md           # Query optimization agent
│   │   └── skills/
│   │       └── groq-optimizer/
│   │           └── SKILL.md                # Auto-optimization skill
│   │
│   └── sanity-migration-helper/            # Plugin 3: Migration Planning
│       ├── .claude-plugin/
│       │   └── plugin.json
│       ├── commands/
│       │   └── plan-migration.md           # /plan-migration command
│       ├── agents/
│       │   └── migration-architect.md      # Complex migration agent
│       └── skills/
│           └── migration-validator/
│               └── SKILL.md                # Auto-validation skill
│
├── README.md                               # Complete documentation
├── QUICKSTART.md                           # 5-minute setup guide
└── STRUCTURE.md                            # This file
```

## File Counts

- **Total Plugins**: 3
- **Commands**: 3 (`/create-schema`, `/build-query`, `/plan-migration`)
- **Agents**: 3 (schema-architect, groq-optimizer, migration-architect)
- **Skills**: 3 (sanity-validator, groq-optimizer, migration-validator)
- **Documentation**: 3 (README, QUICKSTART, STRUCTURE)

## Component Breakdown

### Marketplace Level (1 file)
- `marketplace.json` - Defines marketplace and lists all plugins

### Per Plugin (4 files each)
- `plugin.json` - Plugin metadata and capabilities
- `command.md` - Interactive user-facing command
- `agent.md` - Autonomous specialist agent
- `SKILL.md` - Auto-triggered validation skill

## Total Files

- JSON files: 4 (1 marketplace + 3 plugin manifests)
- Markdown files: 12 (3 commands + 3 agents + 3 skills + 3 docs)
- **Total**: 16 files

## Usage Patterns

### Commands (User-Invoked)
```bash
/create-schema      # Interactive schema builder
/build-query        # Interactive GROQ query builder
/plan-migration     # Interactive migration planner
```

### Agents (Task Tool)
```bash
# Use in conversation
"Use schema-architect agent to refactor my schemas"
"Use groq-optimizer agent to improve query performance"
"Use migration-architect agent to plan complex migration"
```

### Skills (Auto-Triggered)
- Open schema file → `sanity-validator` activates
- Open query file → `groq-optimizer` activates
- Open migration file → `migration-validator` activates

## Development Workflow

### Adding a New Plugin

1. Create plugin directory structure:
   ```bash
   mkdir -p plugins/new-plugin/.claude-plugin
   mkdir -p plugins/new-plugin/commands
   mkdir -p plugins/new-plugin/agents
   mkdir -p plugins/new-plugin/skills/skill-name
   ```

2. Create plugin manifest:
   ```bash
   touch plugins/new-plugin/.claude-plugin/plugin.json
   ```

3. Add components as needed:
   ```bash
   touch plugins/new-plugin/commands/command-name.md
   touch plugins/new-plugin/agents/agent-name.md
   touch plugins/new-plugin/skills/skill-name/SKILL.md
   ```

4. Update marketplace manifest:
   ```json
   // .claude-plugin/marketplace.json
   {
     "plugins": [
       {
         "name": "new-plugin",
         "source": "./plugins/new-plugin",
         "description": "Plugin description"
       }
     ]
   }
   ```

### Testing Locally

1. Add marketplace:
   ```bash
   /plugin marketplace add /Users/nickjensen/Dev/sanity-agent
   ```

2. Install plugin:
   ```bash
   /plugin install plugin-name@sanity-marketplace
   ```

3. Restart Claude Code

4. Test command:
   ```bash
   /command-name
   ```

## Plugin Design Philosophy

Each plugin follows a three-tier architecture:

1. **Commands** (Front Door)
   - User-friendly entry point
   - Interactive Q&A workflow
   - Immediate value for simple tasks

2. **Agents** (Deep Dive)
   - Complex multi-step projects
   - Autonomous research and analysis
   - For when commands aren't enough

3. **Skills** (Automatic)
   - Always-on code quality
   - Proactive suggestions
   - No user action required

This structure ensures users get help at the right level:
- Beginners → Commands (guided workflow)
- Intermediate → Commands + Skills (guidance + validation)
- Advanced → Agents + Skills (autonomous + validation)

## Extensibility

Future plugin ideas that would fit this structure:

- `sanity-studio-config` - Studio configuration generator
- `sanity-docs-generator` - Schema documentation builder
- `sanity-relationship-mapper` - Visual schema relationships
- `sanity-portable-text` - Portable text preset library
- `sanity-localization` - Multi-language setup assistant
- `sanity-performance` - Performance benchmarking tools
- `sanity-testing` - Schema and query testing utilities

Each would follow the same pattern:
- 1 command for interactive use
- 1 agent for complex projects
- 1 skill for automatic validation
