# SOSTAC Routing

## Purpose
Route SOSTAC planning requests to the marketing-sostac skill and handle coordination.

## Important
**Do not attempt to run SOSTAC yourself.** Invoke the `marketing-sostac` skill for all strategic planning.

## Before Invoking

1. Confirm brand is loaded and `brand-context.md` has been read
2. Check SOSTAC status (see `./sostac-status.md`) to know where to resume
3. Tell user which phase comes next

## How to Invoke

When user needs SOSTAC planning (new or resuming):
1. Invoke **marketing-sostac** skill
2. Provide:
   - Brand slug (path to read/write)
   - Which phase to start at (if resuming)
   - Brand context path (point to `brand-context.md`)

## SOSTAC Phase Sequence

Phases are strictly sequential. Never skip:

| Phase | File | Focus |
|---|---|---|
| 1. Situation Analysis | `01-situation.md` | Market, competitors, current state |
| 2. Objectives | `02-objectives.md` | Goals, KPIs, targets |
| 3. Strategy | `03-strategy.md` | Big picture approach |
| 4. Tactics | `04-tactics.md` | Channel-specific activities |
| 5. Action | `05-action.md` | Implementation timeline |
| 6. Control | `06-control.md` | Measurement, review cycles |

## After SOSTAC Completes

When marketing-sostac finishes all 6 phases:
1. Read completed SOSTAC files to understand the plan
2. Summarize plan for user in concise overview
3. Ask: "Your SOSTAC plan is complete. Would you like to start implementing? I can assemble a specialist team based on your tactics."
4. If yes → proceed to Team Spawning workflow

## Handling Jump Requests

If user wants to skip ahead:
- Explain dependency chain
- Recommend completing in order
- Example: "Tactics depend on Strategy, which depends on Objectives set in context of your Situation Analysis. Let's complete these in order for the best outcome."