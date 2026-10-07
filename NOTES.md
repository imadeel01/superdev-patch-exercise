# Patch Notes

## Summary of changes

I focused on three high-value issues across the backend and frontend.

1. Fixed the task search SQL condition by grouping the `OR` clause correctly so that `archived` and `status` filters apply to the complete search condition.

2. Removed the query-length-based `complexityScore` and `Thread.sleep()` from `TaskController`. The delay was introducing unnecessary latency and blocking the request thread before the database query.

3. Fixed the frontend loading state in `useTasks.js`. When the task API request failed, `loading` remained `true`, causing the UI to stay on "Loading tasks..." instead of displaying the error. I moved `setLoading(false)` to a `finally` block so the state is cleared for both successful and failed requests.

## What I chose not to change

I did not make broader architectural or UI changes that were outside the highest-priority bugs. I also avoided rewriting existing logic so that the patch remained focused and low-risk, also the Oracle procedure has the same AND/OR precedence bug in both queries. I didn't change it because it can't be run or tested locally.

## Biggest remaining risk

The backend currently performs pagination after retrieving all matching tasks into memory. This could become inefficient as the dataset grows. Input validation for pagination and status values could also be improved.

## Tools / AI used

I used Claude and ChatGPT to help inspect the codebase, reason through possible bugs, and review implementation approaches. I verified the relevant behavior and made the final code changes myself.
