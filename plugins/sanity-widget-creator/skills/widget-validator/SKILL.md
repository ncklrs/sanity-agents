---
name: widget-validator
description: Validate Studio widget code for performance, UX, and best practices
trigger: When reading Studio widget or dashboard component files
---

# Studio Widget Validator Skill

Automatically validate Studio dashboard widgets for best practices and issues.

## When This Skill Activates
- Reading widget component files
- User asks to review widget code
- Analyzing dashboard configurations

## Validation Checks

### Critical Issues
- ❌ Missing loading states
- ❌ No error handling
- ❌ Missing TypeScript types
- ❌ Infinite re-render loops
- ❌ Memory leaks (missing cleanup)
- ❌ Unhandled promise rejections
- ❌ Missing key props in lists

### Best Practice Recommendations
- ✅ Use Sanity UI components
- ✅ Implement loading skeletons
- ✅ Show helpful error messages
- ✅ Handle empty states gracefully
- ✅ Use React.memo for performance
- ✅ Implement proper cleanup in useEffect
- ✅ Add ARIA labels for accessibility
- ✅ Use TypeScript for type safety

### Performance Issues
- Unnecessary re-renders
- Heavy computations in render
- Missing memoization
- Unoptimized queries
- No query result caching
- Large bundle size

### UX Concerns
- No loading feedback
- Unhelpful error messages
- Missing empty states
- Poor mobile experience
- Unclear widget purpose
- No refresh capability

## Output Format

```
Widget Validation: ContentStatsWidget
====================================

🔴 Critical Issues:
1. Missing error handling
   File: ContentStatsWidget.tsx:15
   Risk: Widget crashes on query failure
   Fix: Add try/catch and error state

2. No loading state
   File: ContentStatsWidget.tsx
   Risk: Shows stale/undefined data during fetch
   Fix: Add loading state and Spinner component

🟡 Best Practices:
1. Use Sanity UI components
   Current: Custom styled divs
   Recommended: Use Card, Stack, Box from @sanity/ui

2. Add memoization
   Component re-renders unnecessarily
   Fix: Wrap in React.memo()

3. Missing empty state
   Shows nothing when count is 0
   Add: Helpful message for empty data

✅ Good Practices:
- Using useClient hook correctly
- TypeScript types defined
- Clean component structure

💡 Performance Suggestions:
1. Cache query results
   Current: Fetches on every mount
   Better: Use SWR or React Query

2. Debounce refresh actions
   Prevent rapid API calls

Widget Health: 6/10
Fix critical issues before production use.
```
