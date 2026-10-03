PATCH NOTES

Summary

# Fixed four issues identified during review:

1. Fixed infinite loading when the task API request fails by clearing the loading state in `finally` and resetting stale errors.
2. Fixed the status filter SQL condition by correctly grouping the search and status conditions.
3. Fixed pagination when search/filter values change by resetting the page to 1.
4. Removed the artificial `Thread.sleep()` delay from the task API to avoid unnecessary request latency and server-thread blocking.

# Assumptions / What I Did Not Change

-Tasks are intended to be displayed in the table; there is currently no task-details page or interaction to open a task as a separate card.
-The frontend does not currently expose a page-size selector, so I left the existing fixed page size of 10 unchanged.
-Search is intended to match both task titles and descriptions, based on the existing repository query and UI behavior, so I did not restrict it to titles only.

# Biggest Remaining Risk

The application still relies on in-memory H2 data, so data persistence and production database behavior were not evaluated as part of this patch.

# Tools / AI Usage

I used AI assistance to help identify and reason about potential bugs, understand unfamiliar Spring Boot/SQL behavior, and review the proposed fixes. I manually inspected, applied, tested, and verified the changes locally.