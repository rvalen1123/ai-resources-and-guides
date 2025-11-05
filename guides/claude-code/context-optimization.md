# CLAUDE.md Context Optimization Guide

> **Master context management for maximum development efficiency**

*Based on Anthropic's official best practices and real-world usage patterns*

## What is CLAUDE.md?

CLAUDE.md is a special file that Claude Code automatically reads to understand your project. Think of it as a briefing document that helps Claude work more effectively with your codebase.

> **Official Definition:** "CLAUDE.md files provide context about your project that Claude uses to better understand your codebase and development practices" - [Anthropic Documentation](https://www.anthropic.com/engineering/claude-code-best-practices)

## Why Context Optimization Matters

**Benefits of well-optimized context:**
- ✅ Faster, more accurate responses
- ✅ Better code that follows your conventions
- ✅ Reduced need for repetitive explanations
- ✅ Improved subagent performance
- ✅ Lower token usage and costs

**Costs of poor context:**
- ❌ Generic, unhelpful responses
- ❌ Code that doesn't match your style
- ❌ Constant re-explanation
- ❌ Wasted development time
- ❌ Higher API costs

## The CLAUDE.md Hierarchy

### Project Root CLAUDE.md
**Location:** `./CLAUDE.md`

**Purpose:** High-level project context
- Project overview
- Tech stack
- Architecture approach
- Global conventions
- Team guidelines

**Example:**
```markdown
# My SaaS Platform

Multi-tenant SaaS application with subscription management.

**Tech Stack:** Next.js 14, TypeScript, PostgreSQL, Redis, Stripe
**Architecture:** Monorepo with shared components

## Conventions
- Use TypeScript strict mode
- All components must have tests
- Use Prisma for database access
- Follow React Server Components patterns
```

### Directory-Level CLAUDE.md
**Location:** `./src/components/CLAUDE.md`, `./src/api/CLAUDE.md`, etc.

**Purpose:** Domain-specific context
- Module-specific patterns
- Local conventions
- Component guidelines
- API contracts

**Example for components:**
```markdown
# UI Components

All components in this directory:
- Must be React Server Components unless marked 'use client'
- Should be in separate files (one component per file)
- Must include TypeScript prop types
- Should be tested with React Testing Library

## Naming
- PascalCase for component files: `UserCard.tsx`
- kebab-case for style files: `user-card.module.css`
```

### Nested Subagent CLAUDE.md
**Location:** `./src/features/auth/CLAUDE.md`

**Purpose:** Specialized context for subagents
- Feature-specific business logic
- Security requirements
- Integration points
- Testing requirements

**Example for auth:**
```markdown
# Authentication System

Session-based auth with NextAuth.js

## Security Requirements
- All auth endpoints require CSRF tokens
- Sessions expire after 30 days of inactivity
- Use bcrypt for password hashing (cost factor: 12)
- Implement rate limiting on login attempts

## Integration
- User data stored in PostgreSQL
- Session data in Redis
- Email via SendGrid
```

## Official Best Practice: The # Key

> **Official Tip:** "Press the # key to give Claude an instruction that it will automatically incorporate into the relevant CLAUDE.md" - [Anthropic Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)

**How it works:**
1. Press `#` during development
2. Type your instruction
3. Claude adds it to the appropriate CLAUDE.md
4. Future interactions automatically use this context

**Example:**
```bash
# Press # and type:
"All API routes must validate input with Zod schemas"

# Claude adds to ./src/api/CLAUDE.md:
## Input Validation
- All API routes must validate input with Zod schemas
```

## Context Optimization Strategies

### 1. Be Specific, Not Generic

**❌ Generic (Low Value):**
```markdown
# My Project
This is a web application. Please write good code.
```

**✅ Specific (High Value):**
```markdown
# Invoice Management System
B2B invoice processing with Stripe integration.

**Critical:** All invoice amounts must be stored in cents (integer)
to avoid floating-point errors.

**Payment Flow:**
1. Create invoice → Pending
2. Send to Stripe → Processing
3. Webhook confirmation → Paid/Failed

**Error Handling:** Never auto-retry failed payments (compliance requirement)
```

### 2. Include Business Context

**❌ Technical Only:**
```markdown
Uses React and TypeScript
```

**✅ Business + Technical:**
```markdown
**Multi-tenant SaaS:** Each tenant has isolated data (tenant_id column)

**Billing:** Stripe subscriptions with metered usage
- Track API calls per tenant
- Bill monthly based on usage tiers
- Grace period: 7 days after failed payment

**Compliance:** GDPR - users can export/delete all data
```

### 3. Document the "Why"

**❌ Just the What:**
```markdown
Use error boundaries in all route components
```

**✅ What + Why:**
```markdown
Use error boundaries in all route components.

**Why:** We had a production incident where a single component error
crashed the entire app. Error boundaries isolate failures and
maintain app stability.

**Implementation:** See `./src/components/ErrorBoundary.tsx` for
our standard pattern with error reporting to Sentry.
```

### 4. Highlight Gotchas and Edge Cases

```markdown
## Database Access

**Important:** Always use transactions when updating user balance
and creating transaction records. We had a bug where network failures
left inconsistent data.

**Bad:**
```typescript
await db.user.update({ balance: newBalance })
await db.transaction.create({ amount })
```

**Good:**
```typescript
await db.$transaction([
  db.user.update({ balance: newBalance }),
  db.transaction.create({ amount })
])
```

## Critical Edge Cases
- Handle timezone differences for subscription billing dates
- Validate email format before sending (we hit SendGrid rate limits from invalid emails)
- Check user account status before all operations (suspended accounts)
```

### 5. Reference Existing Patterns

```markdown
## Code Patterns

**API Routes:** Follow the pattern in `./src/api/users/route.ts`
- Input validation with Zod
- Error handling with custom error classes
- Response formatting with ApiResponse helper

**Database Queries:** See `./src/lib/db-helpers.ts` for:
- Soft delete pattern (deleted_at instead of DELETE)
- Pagination helper (cursor-based)
- Tenant isolation (automatic tenant_id filtering)

**Testing:** Match the style in `./src/api/users/route.test.ts`
- Use test database with seed data
- Mock external services (Stripe, SendGrid)
- Test both success and error paths
```

## Context Efficiency Techniques

### Technique 1: Progressive Disclosure

Start broad, get specific as needed:

```markdown
# Project Root CLAUDE.md (Broad)
E-commerce platform with payment processing.

## Key Technologies
Next.js, Prisma, Stripe, PostgreSQL

## Critical Concepts
- Multi-currency support
- Inventory management
- Order fulfillment workflow
```

```markdown
# src/payment/CLAUDE.md (Specific)
## Payment Processing

**Stripe Integration Details:**
- Use Payment Intents API (not deprecated Charges)
- Capture manually after fraud check
- Store payment_method_id for future charges
- Handle webhook events: payment_intent.succeeded, payment_intent.failed

**Multi-currency:**
- Store prices in cents for all currencies
- Use Stripe's currency conversion
- Display prices using Intl.NumberFormat

**Refunds:**
- Partial refunds allowed
- Full refunds reverse inventory
- Refund webhook updates order status
```

### Technique 2: Link to Examples

```markdown
## Component Patterns

Instead of repeating ourselves, see working examples:

**Complex Form:** `./src/components/UserProfileForm.tsx`
- Shows form validation with React Hook Form
- Error handling and display
- Optimistic updates
- Success notifications

**Data Table:** `./src/components/OrdersTable.tsx`
- Pagination
- Sorting
- Filtering
- Export functionality

**Modal Pattern:** `./src/components/ConfirmDialog.tsx`
- Reusable modal wrapper
- Promise-based confirmation
- Keyboard navigation (ESC to close)

Copy these patterns for consistency.
```

### Technique 3: Use Sections for Scanability

```markdown
# Project Context

## 🏗️ Architecture
[Architecture details]

## 📦 Tech Stack
[Technologies used]

## 🔒 Security
[Security requirements]

## 🧪 Testing
[Testing approach]

## 🚀 Deployment
[Deployment process]

## ⚠️ Known Issues
[Current limitations]

## 🎯 Roadmap
[Upcoming changes]
```

### Technique 4: Context by User/Developer Type

```markdown
## For Frontend Work
- Use Tailwind CSS (no custom CSS files)
- Components are in `./src/components`
- State management with React Context (no Redux)
- API calls via `./src/lib/api-client.ts`

## For Backend Work
- API routes in `./src/api`
- Database models in `./prisma/schema.prisma`
- Business logic in `./src/lib/services`
- Background jobs in `./src/jobs`

## For DevOps Work
- Infrastructure as Code in `./terraform`
- CI/CD in `./.github/workflows`
- Environment config in `./config`
```

## Token Budget Management

### Understanding Token Costs

**CLAUDE.md files are loaded into every request:**
- Root CLAUDE.md: ~always loaded
- Directory CLAUDE.md: loaded when relevant
- Token cost = Length of all CLAUDE.md files in context

**Optimization Strategy:**
```markdown
# Keep root CLAUDE.md lean (< 2000 tokens)
- Essential project info only
- High-level architecture
- Critical conventions

# Move details to subdirectory CLAUDE.md files
- Specific to that module
- Only loaded when working in that area
- Can be more detailed
```

### Measuring Context Size

```bash
# Count tokens in CLAUDE.md (approximate)
wc -w CLAUDE.md  # Roughly 1 token ≈ 0.75 words

# Optimize if root CLAUDE.md > 2000 tokens
# Move details to subdirectories
```

## Subagent Context Optimization

> **Official Tip:** "Each subagent gets its own context window. Use nested CLAUDE.md files for maximum efficiency." - [Anthropic Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)

**Pattern:**
```
project/
├── CLAUDE.md                          # General project context
├── src/
│   ├── auth/
│   │   └── CLAUDE.md                  # Auth-specific context
│   ├── payment/
│   │   └── CLAUDE.md                  # Payment-specific context
│   └── admin/
│       └── CLAUDE.md                  # Admin-specific context
```

**Subagent Usage:**
```bash
> Deploy a subagent to work on the payment system

# Subagent loads:
# 1. Root CLAUDE.md (general context)
# 2. src/payment/CLAUDE.md (specific context)
# Result: Efficient, focused context
```

## Real-World Examples

### Example 1: SaaS Startup

**Root CLAUDE.md (Lean):**
```markdown
# TaskFlow - Project Management SaaS

Multi-tenant task management with team collaboration.

**Stack:** Next.js 14, Prisma, PostgreSQL, Redis
**Auth:** NextAuth with Google OAuth
**Payments:** Stripe Billing

## Core Concepts
- Workspaces (tenant isolation)
- Projects contain tasks
- Real-time updates via Pusher

## Critical Rules
- All DB queries must filter by workspace_id
- All monetary values in cents (integer)
- Use transactions for multi-table updates
```

**src/tasks/CLAUDE.md (Detailed):**
```markdown
# Task Management

## Task States
BACKLOG → TODO → IN_PROGRESS → REVIEW → DONE → ARCHIVED

## Business Rules
- Only project members can create tasks
- Task assignee must be project member
- Cannot delete tasks, only archive
- Task status changes trigger webhooks

## Database Schema
```sql
tasks {
  id uuid
  workspace_id uuid (indexed)
  project_id uuid
  title text
  description text
  status enum
  assignee_id uuid
  due_date timestamp
  created_at timestamp
  updated_at timestamp
}
```

## API Endpoints
- GET /api/tasks?project_id=xxx - List tasks
- POST /api/tasks - Create task
- PATCH /api/tasks/:id - Update task
- DELETE /api/tasks/:id - Archive (soft delete)

See ./route.ts for implementation pattern.
```

### Example 2: E-commerce Platform

**Root CLAUDE.md:**
```markdown
# ShopifyClone - E-commerce Platform

**Architecture:** Monorepo (apps/web, apps/admin, packages/shared)

**Key Principles:**
- Mobile-first design
- Accessibility (WCAG AA)
- Performance (Core Web Vitals)

## Monorepo Structure
- `apps/web` - Customer-facing storefront
- `apps/admin` - Merchant dashboard
- `packages/ui` - Shared component library
- `packages/db` - Database schema & migrations
```

**apps/web/src/checkout/CLAUDE.md:**
```markdown
# Checkout Flow

**Critical:** PCI compliance - never store raw card numbers

## Flow
1. Cart → Shipping Info → Payment → Confirmation
2. Each step validates before proceeding
3. Use Stripe Payment Element (handles PCI)
4. Order created only after payment succeeds

## Shipping Calculation
- Real-time rates from ShipStation API
- Cache rates for 5 minutes
- Fallback to flat rate if API fails

## Payment Processing
```typescript
// Standard pattern - DO NOT DEVIATE
const paymentIntent = await stripe.paymentIntents.create({
  amount: orderTotal,
  currency: 'usd',
  metadata: { orderId }
})

// After confirmation webhook
await createOrder({ paymentIntentId, items, shipping })
```

## Error Handling
- Payment failure: Allow retry (max 3 attempts)
- Out of stock: Release payment, notify customer
- Shipping error: Capture payment, fulfill manually
```

## Advanced Patterns

### Pattern 1: Environment-Specific Context

```markdown
# Production Considerations

**Development:** (current environment)
- Mock Stripe using test keys
- Use local PostgreSQL
- Email goes to Mailhog

**Production:**
- Real Stripe keys (requires PCI compliance)
- AWS RDS PostgreSQL
- Transactional email via SendGrid
- CDN: CloudFront
- Monitoring: DataDog

⚠️ Always test with production-like data before deploying
```

### Pattern 2: Migration Context

```markdown
# Active Migration: Moving from REST to GraphQL

**Status:** 50% complete (as of 2024-11-01)

**Completed:**
- User queries
- Product queries
- Order queries

**TODO:**
- Payment mutations
- Admin mutations
- File uploads

**During Migration:**
- New features: Use GraphQL
- Bug fixes: Fix in both REST and GraphQL
- Maintain REST endpoints until migration complete
- GraphQL endpoint: `/graphql`
- REST endpoint: `/api/*` (will be deprecated)
```

### Pattern 3: Team Knowledge

```markdown
# Team Conventions

## Code Review Checklist
- [ ] Tests added/updated
- [ ] Error handling comprehensive
- [ ] No console.logs in production code
- [ ] Environment variables in .env.example
- [ ] Database migrations tested
- [ ] CLAUDE.md updated if needed

## Common Gotchas
1. **Date Handling:** Always use UTC, convert to user timezone in UI
2. **Async Operations:** Use Promise.all() not sequential awaits
3. **Error Messages:** User-friendly message + technical details for logs
4. **Type Safety:** Validate API responses even with TypeScript

## Who to Ask
- Auth issues: @alice
- Payment bugs: @bob
- Performance: @charlie
- Infrastructure: @david
```

## Maintenance Best Practices

### Keep CLAUDE.md Current

```markdown
## Recent Changes

**2024-11-05:** Migrated from REST to GraphQL
- Updated API patterns below
- Old REST examples in ./legacy-api-examples.md

**2024-10-15:** Added Redis caching layer
- See ./src/lib/cache.ts for usage
- Cache keys follow pattern: `${namespace}:${id}`

**2024-09-20:** Switched from SendGrid to Resend
- Email templates in ./emails directory
- Use `sendEmail()` helper, not direct API calls
```

### Periodic Review

**Monthly:**
- Remove outdated information
- Update examples if patterns changed
- Add new conventions
- Document recent gotchas

**After Major Changes:**
- Update architecture section
- Add migration notes
- Document breaking changes
- Update examples

### Version Control

```bash
# Commit CLAUDE.md changes separately
git add CLAUDE.md
git commit -m "docs: Update CLAUDE.md with new auth patterns"

# Review CLAUDE.md changes in PRs
# They're documentation, treat them seriously
```

## Measuring Success

### Good Indicators

✅ **Claude gives accurate responses without follow-up questions**
✅ **Generated code matches your conventions**
✅ **Subagents work efficiently without re-explanation**
✅ **New team members onboard faster with Claude's help**
✅ **Fewer "I don't understand your codebase" responses**

### Warning Signs

❌ **Constant need to correct Claude's assumptions**
❌ **Generated code in wrong style**
❌ **Repetitive explanations of same concepts**
❌ **Subagents asking for context you've provided**
❌ **Generic responses that don't fit your project**

## Resources

### Official Documentation
- [Anthropic CLAUDE.md Guide](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Context Management Best Practices](https://docs.anthropic.com/en/docs/claude-code/)

### Templates
- [CLAUDE.md Template](../../templates/claude-code/CLAUDE.md-template)

### Related Guides
- [Subagent Best Practices](subagent-best-practices.md)
- [Thinking Levels Guide](thinking-levels-guide.md)

---

*Your CLAUDE.md is Claude's briefing document. Make it count.*
