# Good briefs

Rewrite only when ASK fired. Keep the human's intent. Add file, error,
bounds, and a done-criterion the agent did not invent.

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

We're on the current major of the HTTP stack in this repo — do not
invent deprecated options from older docs.

Files you may change: src/routes/, src/orders/
Do not touch: src/db/migrations/, src/legacy/

Already tried: none yet.

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

## Subagent research

**Before:** Find where sessions are configured.

**After:**

```txt
Find where session refresh is configured.
Search: src/auth/, config/. Do not edit anything.
Return: file:line for each relevant symbol, and one sentence on
which module owns the cookie lifetime. Stop after that.
```

## Session handoff

**Before:** Continu later, context is full.

**After:**

```txt
Write a handoff: goal, knowns, assumptions, files touched, passing
commands, next single step. No narrative. I will paste this into a
new chat and kill this one.
```

## Frontend visual

**Before:** Make the card look better.

**After:**

```txt
In src/components/OrderCard.tsx the padding and title size are wrong.
Screenshot of current: <attach>
Screenshot of target: <attach>
Match spacing and font sizes in the target. Do not restyle unrelated
components. Done when a new screenshot matches the target within a
close visual diff.
```

## Signature-first implement

**Before:** Write a helper that downloads a DB.

**After:**

```txt
Implement this and nothing else:

async def download_db(url: str, max_size_bytes: int = 5_242_880) -> Path:
    """Stream the DB to a temp dir and return the path.
    Check content-length before streaming; raise if it exceeds the limit."""

Done when: unit tests cover oversize reject and happy path, and
`npm run check` / the project test command is green.
```

## Evidence-first, no edits

**Before:** Something in checkout is broken, fix it.

**After:**

```txt
Checkout fails when the cart has a discontinued SKU.
Before you change any code: trace from the HTTP handler to the error.
List each function with file:line. Then stop.
Do not fix yet.
```

## Codemod migration

**Before:** Update all the logger calls.

**After:**

```txt
Migrate ~60 call sites from oldLogger.log(x) to logger.info({ msg: x }).
Do not edit files one by one. Write a codemod, run it on 3 files, show
the diff. If right, run on the rest.
Done when: codemod is in repo, sample diff reviewed, full run clean,
`npm run check` green.
```

## Review a diff

**Before:** Look at this PR.

**After:**

```txt
Review this diff for bugs and missing edge cases. Assume the author was
in a hurry. Point at line numbers. Don't comment on style.
Flag anything that looks like it was added to make a test pass rather
than to fix the problem.
```

## Unstick a stuck run

**Before:** Keep going, you almost had it.

**After:**

```txt
Stop. Don't edit anything.
Tell me: what do you actually know is true, and what are you assuming?
What one piece of information would let you solve this?
```

## What "done" is not

- "It works" / "looks good" / "cleaned up"
- "Tests pass" when the agent wrote the tests in the same step
- Any criterion the agent invented after it started
