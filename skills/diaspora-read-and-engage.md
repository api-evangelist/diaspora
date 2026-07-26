---
name: diaspora-read-and-engage
description: Read a diaspora* timeline, search the pod, and engage with content — comment, like, reshare, subscribe, mute, hide, report and vote in polls — handling the 409/410 convergence semantics correctly.
api: diaspora:diaspora-api
generated: '2026-07-20'
method: generated
source: >-
  Generated from openapi/diaspora-api-openapi.yml plus
  https://diaspora.github.io/api-documentation/routes/streams.html, /routes/comments.html,
  /routes/likes.html, /routes/reshares.html, /routes/post_interactions.html and /routes/search.html.
operations:
  - getStreamsMain
  - getStreamsAspects
  - getStreamsActivity
  - getStreamsMentions
  - getStreamsTags
  - getStreamsLiked
  - getStreamsCommented
  - getSearchPosts
  - getSearchUsers
  - getSearchTags
  - getPostsByPostGuidComments
  - createPostsByPostGuidComments
  - createPostsByPostGuidLikes
  - deletePostsByPostGuidLikes
  - createPostsByPostGuidReshares
  - createPostsByPostGuidSubscribe
  - createPostsByPostGuidMute
  - createPostsByPostGuidHide
  - createPostsByPostGuidReport
  - createPostsByPostGuidVote
---

# Read and engage on diaspora*

Requires a valid access token — see `diaspora-connect-to-a-pod`.

## Reading a timeline

Seven streams are available, all read-only projections over posts:

| Operation | Path | Contents |
| --- | --- | --- |
| `getStreamsMain` | `/streams/main` | The user's main timeline |
| `getStreamsAspects` | `/streams/aspects` | Posts from contacts in aspects |
| `getStreamsActivity` | `/streams/activity` | Activity stream |
| `getStreamsMentions` | `/streams/mentions` | Posts mentioning the user |
| `getStreamsTags` | `/streams/tags` | Posts under followed tags |
| `getStreamsLiked` | `/streams/liked` | Posts the user liked |
| `getStreamsCommented` | `/streams/commented` | Posts the user commented on |

Most streams require `private:read`, which is only grantable alongside `contacts:read`. `getStreamsTags` relates to `tags:read`.

**A stream's contents depend on the caller's granted scopes, not only on request parameters.** A token missing `private:read` returns a materially thinner stream rather than an error. If a timeline looks suspiciously empty, check the granted scope set before concluding the user has no content.

## Pagination

Paginated responses carry a `Link` header:

```
Link: <https://example.com/api/v1/streams/main?page=2>; rel="next", <...>; rel="last"
```

`rel` values are `first`, `previous`, `next`, `last`. `per_page` defaults to 20 and is capped at 100.

**Never construct pagination URLs yourself.** The documentation is explicit: some resources — streams especially — page by timestamp or GUID rather than an increasing counter. Follow the `Link` header or you will silently get wrong results.

## Searching

`getSearchUsers`, `getSearchPosts` and `getSearchTags` all require `public:read` and hit `/search/users`, `/search/posts` and `/search/tags`. Note that user search only returns profiles that are publicly searchable — unless `contacts:read` is granted, in which case the user's own contacts are included even when hidden from public search.

## Engaging

All of these require the `interactions` scope **plus** read access to the underlying post (`public:read` for public posts, `private:read` for private ones).

| Action | Operation |
| --- | --- |
| Read comments | `getPostsByPostGuidComments` |
| Add a comment | `createPostsByPostGuidComments` |
| Like a post | `createPostsByPostGuidLikes` |
| Unlike a post | `deletePostsByPostGuidLikes` |
| Reshare | `createPostsByPostGuidReshares` (needs `public:modify`) |
| Subscribe | `createPostsByPostGuidSubscribe` |
| Mute | `createPostsByPostGuidMute` |
| Hide | `createPostsByPostGuidHide` |
| Report | `createPostsByPostGuidReport` |
| Vote in a poll | `createPostsByPostGuidVote` |

## The 409/410 convergence rule — read this before writing retry logic

diaspora* has no idempotency key. Instead, interaction endpoints express already-applied state through status codes:

- **`409 Conflict`** on a create means it is already done — already liked, already reshared, already reported, already subscribed, already hidden.
- **`410 Gone`** on a delete means it was never there — the like doesn't exist, the post wasn't subscribed to, the post isn't hidden.

**Treat both as success when your goal is convergence to a desired state.** Reporting them as failures produces confusing behavior and pointless retries. They are only genuine errors if you specifically needed to know you were the one who caused the transition.

## Other errors

- `422` — the user is not allowed to perform this action (not allowed to comment, like or reshare), or the request was invalid such as a report missing a reason.
- `404` — post or comment not found. Remember this can mean "not visible to you" rather than "does not exist", because visibility is governed by aspects and federation reach.
- `403` — the token lacks the `interactions` scope, or read access to the post.

## Notes

- Do not parse error `message` strings. Branch on status code plus the operation invoked; there is no stable machine-readable error identifier.
- No rate limiting is documented, but pods are volunteer-operated and often small. Self-limit; do not hammer a stream.
- See `errors/diaspora-problem-types.yml` for the full per-operation error table.
