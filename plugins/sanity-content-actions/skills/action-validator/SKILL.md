---
name: action-validator
description: Validate content action code for security, reliability, and AI integration best practices
trigger: When reading Sanity document action files with AI integrations
---

# Content Action Validator Skill

Automatically validate AI-powered document actions for security, reliability, and best practices.

## When This Skill Activates
- Reading document action files with AI calls
- User asks to review action code
- Analyzing AI integration code

## Validation Checks

### Critical Security Issues
- ❌ Exposed API keys in code
- ❌ Unvalidated user input to AI
- ❌ No rate limiting
- ❌ Missing error boundaries
- ❌ PII sent to external APIs without consent
- ❌ No timeout handling
- ❌ Unencrypted credential storage

### Best Practice Recommendations
- ✅ Use environment variables for API keys
- ✅ Implement proper error handling
- ✅ Add rate limiting and cost controls
- ✅ Validate AI responses before applying
- ✅ Show preview before making changes
- ✅ Implement retry logic with exponential backoff
- ✅ Log AI usage for monitoring
- ✅ Handle timeout scenarios

### Performance & Cost Issues
- No response caching
- Using expensive models for simple tasks
- Missing batch processing
- Inefficient prompt engineering
- No token limit controls
- Synchronous blocking operations

### Reliability Concerns
- No fallback providers
- Missing timeout handling
- Inadequate error messages
- No retry logic
- Missing progress feedback
- No operation cancellation

## Output Format

```
Action Validation: translateAction
==================================

🔴 Critical Issues:
1. Exposed API key
   File: translateAction.ts:3
   Current: apiKey: 'sk-...'
   Fix: Use process.env.OPENAI_API_KEY

2. No timeout handling
   Risk: Action hangs indefinitely
   Fix: Add timeout to AI call

3. Missing input validation
   Risk: Malicious input to AI
   Fix: Validate/sanitize content before AI call

🟡 Best Practices:
1. Add retry logic
   Current: Single attempt fails entire action
   Recommended: 3 retries with exponential backoff

2. Show preview before applying
   Current: Directly updates document
   Better: Show translation, confirm before applying

3. Add cost controls
   Missing: Token limits, usage tracking
   Recommended: Set max_tokens, log usage

💰 Cost Optimization:
1. Use cheaper model for simple translations
   Current: gpt-4 ($0.03/1K tokens)
   Recommended: gpt-3.5-turbo ($0.001/1K tokens)
   Savings: 97% cost reduction

2. Cache translations
   Translate "Hello" costs $0.0003 every time
   Cache would save 99% on repeated content

✅ Good Practices:
- Using TypeScript types
- Clear error messages
- Disabled state during operation

Security Score: 3/10 - CRITICAL ISSUES FOUND
Reliability Score: 5/10
Cost Efficiency: 4/10

Must fix security issues before production use.
```

## Example Security Fix

Vulnerable:
```typescript
const openai = new OpenAI({
  apiKey: 'sk-1234567890abcdef' // ❌ Exposed key
})

export const action = () => {
  const translate = async (text: string) => {
    // ❌ No validation, no timeout, no error handling
    const response = await openai.chat.completions.create({
      model: 'gpt-4', // ❌ Expensive for simple task
      messages: [{role: 'user', content: text}] // ❌ Direct user input
    })
    return response.choices[0].message.content
  }
}
```

Secure:
```typescript
const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY // ✅ Environment variable
})

const TIMEOUT_MS = 30000
const MAX_RETRIES = 3

export const action = () => {
  const translate = async (text: string) => {
    // ✅ Input validation
    if (!text || text.length > 5000) {
      throw new Error('Invalid input length')
    }

    // ✅ Retry logic
    for (let attempt = 0; attempt < MAX_RETRIES; attempt++) {
      try {
        // ✅ Timeout handling
        const response = await Promise.race([
          openai.chat.completions.create({
            model: 'gpt-3.5-turbo', // ✅ Cost-effective model
            messages: [{
              role: 'system',
              content: 'Translate to Spanish. Return only translation.'
            }, {
              role: 'user',
              content: text
            }],
            max_tokens: 1000 // ✅ Token limit
          }),
          new Promise((_, reject) =>
            setTimeout(() => reject(new Error('Timeout')), TIMEOUT_MS)
          )
        ])

        // ✅ Response validation
        if (!response.choices[0]?.message?.content) {
          throw new Error('Invalid AI response')
        }

        // ✅ Usage logging
        logAIUsage(response.usage)

        return response.choices[0].message.content

      } catch (error) {
        if (attempt === MAX_RETRIES - 1) throw error
        // ✅ Exponential backoff
        await new Promise(r => setTimeout(r, 2 ** attempt * 1000))
      }
    }
  }
}
```

Improvements:
- Security: Environment variables, input validation
- Reliability: Retries, timeout, error handling
- Cost: Cheaper model, token limits, usage tracking
- UX: Better error messages, progress feedback
