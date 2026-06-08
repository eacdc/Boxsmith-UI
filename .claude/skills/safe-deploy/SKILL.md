---
name: safe-deploy
description: >-
  Safely publish website or code changes to GitHub using a test-first workflow.
  ALWAYS send changes to the `test` branch before the live `main` branch, and
  ALWAYS show a plain-language summary and get an explicit "yes" before every
  single push. Use this skill whenever the user wants to push, publish, deploy,
  save, ship, update, or "make live" any changes to a GitHub repository, or asks
  to update the website — even if they do not say the word "deploy". This is
  especially important when the person is not a coder: they must never push
  straight to the live branch, and nothing should reach the live site without
  their confirmation.
---

# Safe Deploy

This skill keeps website/code changes safe by enforcing a **test-first, confirm-before-every-push** workflow. The person using it is **not a coder**, so speak in plain language and act as a careful guardrail.

## The golden rules (never break these)

1. **Test before live.** Changes always go to the **`test`** branch first. They only reach **`main`** (the live site) after the person has reviewed the test version and explicitly approves.
2. **Confirm before every push.** Before pushing to `test` AND before going live to `main`, show what changed in plain English and wait for a clear "yes". A quick verbal "yes" is the safeguard — never skip it, even if the person seems to be in a hurry.
3. **Never assume "push" means "go live."** If the person says "push", "save", or "publish", treat it as a push to **test** first, not to main. Going live is always a separate, second confirmation.
4. **Plain language only.** Talk about "the test version" and "the live site", not "branches", "commits", or "merges". No git jargon unless they use it first.
5. **Stay reversible.** Never force-push, never delete branches, never rewrite history. Only ordinary commits, pushes, and a simple merge from `test` into `main`.

## The workflow

### Step 1 — See what changed
Check the repository for changes (e.g. `git status` and `git diff`). Then describe them to the person in **plain, human terms** — what the change actually does, not file/line numbers.
- Good: "You changed the homepage headline to 'Luxury packaging, made in India'."
- Avoid: "Modified line 42 of index.html."

If there are **no changes** to publish, say so plainly and stop.

### Step 2 — Put it on the test version (with confirmation)
1. Make sure you're on the **`test`** branch. If it doesn't exist yet, create it from `main`. If you're on a different branch, switch to `test`.
2. Show the plain-language summary and ask:
   > "Here's what I'll put on the **test version**: [summary]. Want me to push this to test? (yes / no)"
3. Only after an explicit **yes**, commit the changes and push to **`test`**.
4. If they say no, stop and ask what they'd like to change.

### Step 3 — Invite them to review the test version
After pushing to test, tell them it's updated and where to look:
> "Done — your changes are on the **test site** now. Please open the test link and check it looks right, then tell me if you'd like to make it live."

(If you know the test URL, give it. Otherwise tell them to open their usual test/preview link.)

### Step 4 — Go live (separate confirmation)
Only when the person **explicitly approves the test version**:
1. Confirm once more, clearly, because this affects real visitors:
   > "Ready to make this live on the **main site**? This updates what visitors see. (yes / no)"
2. On an explicit **yes**, take the approved changes from `test` to `main` by **merging `test` directly into `main`** (no pull request), then push `main`.
3. Confirm it's live in plain language, and give the live URL if you know it:
   > "It's live now — visitors will see the update at [live URL]."

### Step 5 — When in doubt, ask
- If it's unclear whether they mean the test version or the live site, **ask** rather than guess.
- If a push is rejected (for example a permissions error), explain it simply and don't keep retrying blindly.
- Never take a shortcut that skips the test step or a confirmation.

## Quick reference

| Person says… | What this skill does |
| --- | --- |
| "Push / save / publish my changes" | Summarize → confirm → push to **test** only |
| "Make it live" / "Push to main" / "Publish to the live site" | Confirm again → merge **test → main** → push live |
| "Push straight to main" / "skip test" | Gently confirm they really want to bypass the test step before doing anything; default is still test-first |

## What NOT to do
- Don't push to `main` first, or without an explicit go-ahead.
- Don't push anything (test or live) without showing the summary and getting a "yes".
- Don't use technical jargon with this person.
- Don't force-push, delete branches, or rewrite history.
