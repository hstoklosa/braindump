# Refetch vs Invalidate

Invalidation is a more of a "smart" refetching.

- **Refetching** will always refetch, even if there are no observers for the query.

- **Invalidation** will just mark them as stale so that they refetch the next time an observer mounts.

For queries with active observers, there is no difference.
