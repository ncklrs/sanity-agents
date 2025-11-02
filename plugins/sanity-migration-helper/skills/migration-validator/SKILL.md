---
name: migration-validator
description: Validate migration scripts for safety, identify potential issues, and ensure proper error handling
trigger: When reading migration script files or analyzing migration code
---

# Migration Script Validator Skill

Automatically validate Sanity migration scripts for safety, completeness, and best practices.

## When This Skill Activates
- Reading migration script files
- User asks to review migration code
- Analyzing data transformation scripts

## Validation Checks

### Critical Safety Issues
- ❌ No dry-run mode (must have DRY_RUN flag)
- ❌ Missing backup verification
- ❌ No error handling (try/catch blocks)
- ❌ No transaction usage (atomic operations)
- ❌ Missing pre-migration validation
- ❌ No post-migration validation
- ❌ Missing rollback documentation
- ❌ No progress logging
- ❌ Direct deletion without safety period

### Best Practice Recommendations
- ✅ Batch processing for large datasets
- ✅ Progress tracking and logging
- ✅ Idempotent operations (safe to re-run)
- ✅ Detailed error logging
- ✅ Transaction batching for atomicity
- ✅ Validation before and after migration
- ✅ Clear migration documentation
- ✅ Migration statistics and summary
- ✅ Graceful error recovery

### Data Integrity Checks
- Validate reference integrity after changes
- Check for orphaned documents
- Verify required fields are populated
- Ensure unique constraints maintained
- Validate type conversions
- Check for data loss

### Performance Considerations
- Batch size appropriate for dataset
- Memory usage for large migrations
- Query efficiency in document fetching
- Transaction size limits
- Progress monitoring overhead

## Output Format

```
Migration Script Analysis
=========================

Script: rename-author-field.ts
Risk Level: MEDIUM

🔴 Critical Issues:
1. Missing DRY_RUN mode
   Risk: No safe testing before production
   Fix: Add DRY_RUN constant and conditional logic

2. No pre-migration validation
   Risk: Migration may fail mid-process
   Fix: Add validateBeforeMigration() function

3. Missing error handling in batch processing
   Risk: One failure stops entire migration
   Fix: Wrap transformations in try/catch

🟡 Best Practice Improvements:
1. Add transaction batching
   Current: Individual patches
   Recommended: Batch in transactions for atomicity

2. Add progress tracking
   Recommended: Log progress every N documents

3. Document rollback procedure
   Missing: How to reverse this migration

✅ Good Practices Found:
- Using batch processing
- Logging document IDs
- Client configuration correct

Recommended Changes:
[Provide improved version with fixes]

Safety Score: 4/10
Not production-ready. Address critical issues before running.
```

## Example Validation

Problematic Script:
```typescript
// ❌ UNSAFE - Missing safety features
const docs = await client.fetch('*[_type == "post"]')
for (const doc of docs) {
  await client.patch(doc._id).set({author: doc.writer}).commit()
}
```

Issues Identified:
- No dry-run mode
- No error handling
- No batch processing
- No validation
- No progress tracking
- No rollback plan
- Not idempotent

Safe Version:
```typescript
// ✅ SAFE - All safety features included
const DRY_RUN = true
const BATCH_SIZE = 100

async function validateBefore() {
  // Check all posts have 'writer' field
  const invalid = await client.fetch('*[_type == "post" && !defined(writer)]')
  if (invalid.length > 0) {
    throw new Error(`${invalid.length} posts missing 'writer' field`)
  }
}

async function migrate() {
  await validateBefore()

  const docs = await client.fetch('*[_type == "post" && !defined(author)]')
  console.log(`Migrating ${docs.length} documents`)

  for (let i = 0; i < docs.length; i += BATCH_SIZE) {
    const batch = docs.slice(i, i + BATCH_SIZE)
    let transaction = client.transaction()

    for (const doc of batch) {
      try {
        if (!DRY_RUN) {
          transaction = transaction.patch(doc._id).set({author: doc.writer})
        }
        console.log(`✅ ${doc._id}`)
      } catch (error) {
        console.error(`❌ ${doc._id}: ${error.message}`)
      }
    }

    if (!DRY_RUN) {
      await transaction.commit()
    }

    console.log(`Progress: ${Math.min(i + BATCH_SIZE, docs.length)}/${docs.length}`)
  }

  await validateAfter()
}

async function validateAfter() {
  // Verify all posts now have 'author' field
  const missing = await client.fetch('*[_type == "post" && !defined(author)]')
  if (missing.length > 0) {
    throw new Error(`Migration incomplete: ${missing.length} posts still missing 'author'`)
  }
}
```

Safety Score: 9/10
Production-ready with all safety features.
