---
name: plugin-validator
description: Validate Sanity plugin code for best practices, API usage, and common issues
trigger: When reading Sanity plugin files or plugin configuration
---

# Sanity Plugin Validator Skill

Automatically validate Sanity plugin code against best practices and identify issues.

## When This Skill Activates
- Reading plugin source files
- User asks to review plugin code
- Analyzing plugin configuration

## Validation Checks

### Critical Issues
- ❌ Missing definePlugin() wrapper
- ❌ Incorrect TypeScript types
- ❌ Invalid plugin configuration structure
- ❌ Missing peer dependencies
- ❌ Improper patch/set/unset usage
- ❌ Memory leaks in hooks
- ❌ Missing error boundaries

### Best Practice Recommendations
- ✅ Use definePlugin() for plugin definition
- ✅ Proper TypeScript typing throughout
- ✅ Export plugin types for consumers
- ✅ Follow Sanity naming conventions
- ✅ Use Sanity UI components
- ✅ Implement proper error handling
- ✅ Add accessibility attributes
- ✅ Document plugin configuration options

### Performance Issues
- Unnecessary re-renders
- Missing React.memo/useCallback
- Heavy computations in render
- Unoptimized queries
- Large bundle size

### Security Concerns
- Exposed API keys
- Unvalidated user input
- XSS vulnerabilities
- CSRF risks

## Output Format

```
Plugin Validation: my-sanity-plugin
===================================

🔴 Critical Issues:
1. Missing definePlugin() wrapper
   File: src/plugin.ts
   Fix: Wrap plugin config in definePlugin()

2. Incorrect patch usage
   File: src/components/MyInput.tsx
   Current: onChange(value)
   Fix: onChange(value ? set(value) : unset())

🟡 Best Practices:
1. Add TypeScript types for config
   Recommended: export type MyPluginConfig

2. Use Sanity UI components
   Current: <input />
   Recommended: <TextInput from @sanity/ui />

✅ Good Practices:
- Proper peer dependencies
- Clean plugin structure
- Error handling present

Plugin Health: 6/10
Address critical issues before publishing
```
