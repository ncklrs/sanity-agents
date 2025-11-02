---
name: sanity-validator
description: Validate Sanity schemas against best practices and identify common issues
trigger: When examining, reviewing, or validating Sanity schema files
---

# Sanity Schema Validator Skill

Automatically validate Sanity schema definitions against best practices when working with schema files.

## When This Skill Activates
- Reading `.ts` or `.js` schema files in Sanity projects
- User asks to review or validate schema code
- Analyzing schema structure during refactoring

## Validation Checks

### Critical Issues
- Missing required fields (name, title, type)
- Invalid type references
- Missing validation on required fields
- Images without alt text fields
- Slug fields without source configuration
- References without `to` array
- Arrays without `of` property

### Best Practice Recommendations
- Use defineType/defineField for TypeScript support
- Add descriptions for editor guidance
- Configure preview with title, subtitle, media
- Use proper naming conventions (camelCase)
- Add validation rules for better data quality
- Configure initial values where appropriate
- Use field groups for complex schemas
- Add orderings for document lists

### Performance Considerations
- Warn about deeply nested references (query performance)
- Suggest denormalization opportunities for frequently queried data
- Identify missing indexes on sortable fields

### Accessibility Checks
- Images should have alt text fields
- Links should have descriptive text
- Form fields should have clear labels and descriptions

## Output Format
When validating, provide:
1. Critical issues that must be fixed
2. Best practice recommendations
3. Performance optimization suggestions
4. Code examples for recommended fixes
5. Overall schema health score (1-10)

## Example Output

```
Schema Validation Results for "blogPost"
========================================

✓ Critical Checks Passed
- All required fields present
- Valid type references
- Proper validation configured

⚠ Best Practice Recommendations
1. Add preview configuration for better Studio UX
   Suggested code:
   preview: {
     select: {
       title: 'title',
       media: 'mainImage'
     }
   }

2. Add descriptions to fields for editor guidance
   - Field 'publishedAt' missing description

3. Consider adding field groups for organization
   Suggested: content, seo, settings groups

💡 Performance Suggestions
- Consider denormalizing author name for list views
- Current: Reference requires join for every query
- Alternative: Store author name directly, reference for details

Schema Health Score: 7/10
Good foundation, implement recommendations for production readiness.
```
