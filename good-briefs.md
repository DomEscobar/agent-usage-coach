# Good briefs

Rewrite only when ASK fired. Keep the human's intent. Add file, error, bounds, and a done-criterion the agent did not invent.

## Bug

**Before:** Fix the login bug.

**After:**

```txt
In src/auth/session.ts, refreshToken() returns undefined when the
cookie is expired. Fix it so it returns null and the caller redirects.

Error: <paste the stack>

Already tried: adding await on line 42 — same error.

Done when: a failing test first (stop and show it), then that test
passes, `npm run check` is green, and no other test file was modified.
```

## Feature

**Before:** Add order editing.

**After:**

```txt
Add PATCH /orders/:id. Follow src/routes/orders.post.ts — same
validation layer, same error mapping.

Files you may change: src/routes/, src/orders/
Do not touch: src/db/migrations/, src/legacy/

Done when: `npm run check` is green and
`curl -s -X PATCH localhost:3000/orders/1 -d '{"qty":2}'` returns 200
with the updated qty.
Show a plan first.
```

## Vague performance

**Before:** Why is this slow?

**After:**

```txt
GET /orders?limit=50 p95 is 1.8s locally. v1.4.0 was fine.

Do not edit yet. Trace the handler to the slow call. List each
function with file:line. Give one falsifiable hypothesis and the
single command that would prove it wrong.
```

## Design fork

**Before:** We need caching.

**After:**

```txt
Cache product reads for 60s. Three approaches with tradeoffs, no code.
One paragraph each. I will pick. Then implement only that one.

Done when: `npm run check` is green and a second identical request
within 60s does not hit the DB (show the log line).
```

## What "done" is not

- "It works" / "looks good" / "cleaned up"
- "Tests pass" when the agent wrote the tests in the same step
- Any criterion the agent invented after it started
