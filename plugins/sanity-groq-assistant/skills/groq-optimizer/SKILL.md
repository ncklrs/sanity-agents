---
name: groq-optimizer
description: Automatically analyze GROQ queries for performance issues and suggest optimizations
trigger: When reading or analyzing GROQ query code
---

# GROQ Query Optimizer Skill

Automatically analyze GROQ queries for performance issues and optimization opportunities.

## When This Skill Activates
- Reading files containing GROQ queries (groq`` template tags)
- User asks to review or optimize queries
- Analyzing query performance issues

## Optimization Checks

### Critical Performance Issues
- Missing result limiting on list queries
- Over-fetching (resolving entire references without projection)
- Missing _type filter (unindexed queries)
- Deep reference nesting (>3 levels)
- Array mapping without slicing
- Ordering before limiting

### Best Practice Recommendations
- Use projection `{}` for all queries
- Filter by _type first for index usage
- Limit results with `[0...n]`
- Dereference selectively: `author->{name}` not `author->`
- Use parameters `$slug` for reusable queries
- Add TypeScript types for query results
- Order only when necessary

### Syntax Issues
- Invalid GROQ syntax
- Missing required operators
- Incorrect reference syntax
- Array operation errors
- Projection syntax mistakes

### Security Considerations
- Unparameterized user input (injection risk)
- Exposing sensitive fields
- Missing access control filters

## Output Format

```
GROQ Query Analysis
===================

Query: postsQuery

🔴 Critical Issues:
1. Missing result limiting - could return thousands of documents
   Impact: Large payload, slow queries, high bandwidth
   Fix: Add [0...12] after ordering

2. Over-fetching author data
   Current: author-> (resolves all 23 fields)
   Impact: 3.2KB extra per post
   Fix: author->{name, "imageUrl": image.asset->url}

🟡 Performance Optimizations:
1. Add _type filter first
   Current: *[published == true]
   Optimized: *[_type == "post" && published == true]
   Impact: 10x faster with index usage

2. Project before dereferencing
   Current: *[...] { ..., categories[]-> }
   Optimized: *[...] { ..., "categories": categories[]->title }

✅ Good Practices Found:
- Using parameters for slug lookup
- Proper projection on main query
- Selective field selection

Estimated Performance Improvement: 85% faster, 76% smaller payload

Optimized Query:
[Provide corrected version]
```

## Example Optimization

Before:
```typescript
const query = groq`*[published == true] | order(date desc) {
  ...,
  author->,
  categories[]->
}`
```

After:
```typescript
const query = groq`
  *[_type == "post" && published == true]
  | order(date desc)
  [0...12] {
    _id,
    title,
    slug,
    date,
    "author": author->{name, "imageUrl": image.asset->url},
    "categories": categories[]->title
  }
`
```

Performance Impact:
- Query time: 1.2s → 0.15s (87% faster)
- Payload size: 245KB → 18KB (93% smaller)
- Fields transferred: 450 → 84 (81% reduction)
