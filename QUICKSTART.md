# Quick Start Guide - Sanity CMS Plugins

Get up and running with Sanity-focused Claude Code plugins in 5 minutes.

## Installation

### Step 1: Add Marketplace
```bash
claude
/plugin marketplace add git@github.com:ncklrs/sanity-agents.git

# Or using HTTPS:
# /plugin marketplace add https://github.com/ncklrs/sanity-agents.git
```

### Step 2: Install Plugins
```bash
/plugin install sanity-schema-helper@sanity-marketplace
/plugin install sanity-groq-assistant@sanity-marketplace
/plugin install sanity-migration-helper@sanity-marketplace
```

### Step 3: Restart Claude Code
Close and reopen Claude Code to activate plugins.

### Step 4: Verify Installation
```bash
/help
# You should see: /create-schema, /build-query, /plan-migration
```

---

## Your First Schema

```bash
/create-schema
```

Example conversation:
```
You: Create a blog post schema
Assistant: I'll help you create a blog post schema. Let me ask a few questions:

1. What fields do you need? (title, content, author, etc.)
2. Should it have categories or tags?
3. Do you need SEO metadata?
4. Should posts have a featured image?

[After answering questions, you get production-ready code:]

✅ Complete TypeScript schema generated
✅ All best practices applied
✅ Preview, validation, and orderings configured
✅ Ready to add to your Sanity project
```

---

## Your First GROQ Query

```bash
/build-query
```

Example conversation:
```
You: Get all published blog posts with author names
Assistant: I'll build an optimized GROQ query for you.

[Generates query with:]
✅ Proper filtering by _type and published status
✅ Selective dereferencing of author (name only)
✅ Result limiting for pagination
✅ TypeScript types included
✅ Performance optimized (87% faster than naive approach)
```

---

## Your First Migration

```bash
/plan-migration
```

Example conversation:
```
You: Add a required 'excerpt' field to all blog posts
Assistant: I'll plan a safe migration. First, do you have a recent backup?

[After confirmation:]
✅ Migration script with DRY_RUN mode
✅ Pre and post-validation checks
✅ Batch processing with error handling
✅ Progress tracking and logging
✅ Rollback procedure documented
✅ Safe to test on development dataset
```

---

## Power Features

### Auto-Validation Skills

These skills activate automatically when you open files:

**sanity-validator** - Validates schemas
```bash
# Just open a schema file
code schemas/blogPost.ts

# Claude automatically analyzes:
✓ Critical issues (missing validation, no alt text)
⚠ Best practice recommendations
💡 Performance suggestions
📊 Schema health score: 7/10
```

**groq-optimizer** - Optimizes queries
```bash
# Just open a query file
code lib/queries.ts

# Claude automatically analyzes:
🔴 Critical: Missing result limiting
🟡 Performance: Over-fetching author data
✅ Estimated improvement: 85% faster
```

**migration-validator** - Validates migrations
```bash
# Just open a migration script
code migrations/add-category.ts

# Claude automatically checks:
🔴 Critical: Missing DRY_RUN mode
🟡 Best practice: Add error handling
📊 Safety score: 4/10 - not production ready
```

### Specialized Agents

For complex multi-step projects, use agents:

**schema-architect** - Complex schema design
```bash
# In conversation:
"Use schema-architect agent to refactor my entire content model for better performance"

# Agent will:
1. Analyze all existing schemas
2. Design coordinated improvements
3. Plan migration strategy
4. Generate all new schema code
5. Document decisions
```

**groq-optimizer** - Query performance tuning
```bash
"Use groq-optimizer agent to analyze all queries in my lib/ folder and improve performance"

# Agent will:
1. Read all query files
2. Identify bottlenecks
3. Refactor for performance
4. Add TypeScript types
5. Show before/after improvements
```

**migration-architect** - Enterprise migrations
```bash
"Use migration-architect agent to plan zero-downtime migration of 50,000 products"

# Agent will:
1. Analyze current schema and data
2. Design multi-phase migration
3. Generate all migration scripts
4. Create comprehensive runbook
5. Plan validation and rollback
```

---

## Common Workflows

### New Feature Development
```bash
# 1. Design schema
/create-schema
> "Product schema with variants"

# 2. Build queries
/build-query
> "Get products with filters"

# 3. Iterate with auto-validation
[Open files - get instant feedback]
```

### Refactoring Existing Project
```bash
# 1. Analyze schemas
[Open schema files - sanity-validator gives feedback]

# 2. Optimize queries
"Use groq-optimizer agent to improve all queries"

# 3. Plan migrations for schema changes
/plan-migration
> "Rename author to authors array"
```

### Production Migration
```bash
# 1. Plan thoroughly
"Use migration-architect agent to plan this migration"

# 2. Test on development
# Run generated migration with DRY_RUN=true

# 3. Validate results
# Run post-migration validation scripts

# 4. Execute on production
# Set DRY_RUN=false, monitor closely
```

---

## Tips & Tricks

### Get Better Results
1. **Be specific**: "Blog post with author, categories, and SEO" vs "blog schema"
2. **Ask questions**: "What's the best way to handle multi-language content?"
3. **Iterate**: Use auto-validation to improve incrementally
4. **Use agents**: For complex projects, agents do deep research

### Performance
- Always test queries in Sanity Vision first
- Use projection to reduce payload size
- Limit results for list queries
- Filter by `_type` first (indexed)

### Safety
- Always backup before migrations
- Test migrations on development dataset
- Use DRY_RUN mode first
- Validate before and after
- Document rollback procedures

---

## Next Steps

1. **Explore commands**: Try `/create-schema`, `/build-query`, `/plan-migration`
2. **Test auto-validation**: Open schema/query files and see instant feedback
3. **Use agents**: Try complex multi-step projects with specialized agents
4. **Read full README**: Comprehensive guide with all features
5. **Contribute**: Add new plugins or improve existing ones

---

## Troubleshooting

### Plugins not showing in /help
- Make sure you restarted Claude Code after installation
- Verify installation: `/plugin` → "Manage Plugins"

### Commands not working
- Check plugin is enabled: `/plugin enable plugin-name@sanity-marketplace`
- Review plugin capabilities: `/plugin` → View plugin details

### Need help
```bash
# Ask the plugins directly
/create-schema
> "How do I handle conditional fields?"

/build-query
> "What's the syntax for filtering arrays?"

/plan-migration
> "How do I safely change a field type?"
```

---

**Ready to build amazing Sanity projects!** 🚀

For complete documentation, see [README.md](./README.md)