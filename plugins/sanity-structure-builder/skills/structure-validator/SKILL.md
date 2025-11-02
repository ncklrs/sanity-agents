---
name: structure-validator
description: Validate Studio structure code for performance, usability, and best practices
trigger: When reading Studio structure configuration files
---

# Studio Structure Validator Skill

Automatically validate Studio structure configurations for best practices and issues.

## When This Skill Activates
- Reading structure.ts or desk structure files
- User asks to review structure configuration
- Analyzing Studio navigation setup

## Validation Checks

### Critical Issues
- ❌ Missing StructureResolver type
- ❌ Infinite loops in nested structures
- ❌ Incorrect filter syntax
- ❌ Missing document IDs for singletons
- ❌ Invalid schema type references
- ❌ Broken intent resolution

### Best Practice Recommendations
- ✅ Use descriptive titles and icons
- ✅ Add dividers for visual grouping
- ✅ Configure default ordering for lists
- ✅ Add helpful menu filters
- ✅ Use singletons for one-off documents
- ✅ Group related content logically
- ✅ Provide keyboard shortcuts
- ✅ Optimize queries for performance

### Performance Issues
- Unoptimized filters
- Missing pagination
- Heavy nested queries
- Inefficient document lookups
- No query caching

### Usability Concerns
- Unclear labels
- Deep nesting (>3 levels)
- Missing icons
- No visual separation
- Inconsistent organization

## Output Format

```
Structure Validation Results
============================

🔴 Critical Issues:
1. Missing documentId for singleton
   Item: Settings
   Fix: Add .documentId('siteSettings')

2. Infinite loop risk in nested structure
   Item: Categories
   Fix: Remove recursive child() call

🟡 Best Practices:
1. Add default ordering to lists
   Missing on: Blog Posts, Products
   Recommended: .defaultOrdering([{field: 'publishedAt', direction: 'desc'}])

2. Add visual dividers
   Recommended: Between major sections

3. Use icons for visual navigation
   Missing icons: Authors, Categories

✅ Good Practices:
- Clear descriptive titles
- Logical content grouping
- Singleton properly configured

💡 Performance Suggestions:
1. Add pagination to large lists
   Lists with >100 items should use .child() with limits

2. Optimize category filters
   Current: Loading all categories upfront
   Better: Lazy load on navigation

Structure Health: 7/10
Good foundation, implement recommendations for production.
```
