---
name: diaspora-publish-a-post
description: Publish a post to diaspora* — public or scoped to specific aspects — optionally attaching photos, a poll, a location and mentions, then verify and manage it.
api: diaspora:diaspora-api
generated: '2026-07-20'
method: generated
source: >-
  Generated from openapi/diaspora-api-openapi.yml plus
  https://diaspora.github.io/api-documentation/routes/posts.html, /routes/photos.html and
  /routes/aspects.html.
operations:
  - getAspects
  - createPhotos
  - createPosts
  - getPostsByPostGuid
  - deletePostsByPostGuid
---

# Publish a post to diaspora*

Requires a valid access token — see `diaspora-connect-to-a-pod`.

The decision that matters most here is audience. In diaspora* a post is either public to the whole network or shared with a chosen set of **aspects** (the user's contact groups). This is the product's central privacy promise, so get it explicitly right rather than defaulting.

## 1. Decide the audience

**Ask the user whether the post is public or private.** Do not guess.

For a private post, list the available aspects first:

```
GET /api/v1/aspects
Authorization: Bearer <token>
```

`getAspects` requires `contacts:read` and returns `[{ "id": 1, "name": "Family", "order": 1 }, ...]`. You need the integer `id` values, not the names.

## 2. Upload any photos first

Photos are uploaded independently and then attached to the post by GUID.

```
POST /api/v1/photos
Authorization: Bearer <token>
```

`createPhotos` requires `public:modify` or `private:modify` depending on the intended visibility. Collect the returned photo GUIDs.

## 3. Publish

```
POST /api/v1/posts
Content-Type: application/json
Authorization: Bearer <token>

{
  "body": "...",
  "public": false,
  "aspects": [2, 3],
  "photos": ["<photo guid>"],
  "poll": { ... },
  "location": { "address": "...", "lat": 48.77, "lng": 9.17 }
}
```

`createPosts` requires `public:modify` for public posts or `private:modify` for private posts.

Documented parameters:

| Name | Type | Meaning |
| --- | --- | --- |
| `body` | string | Markdown, may contain mentions |
| `public` | boolean | Public or aspect-scoped |
| `aspects` | array | Aspect **ids** to share with |
| `photos` | array | GUIDs of already-uploaded photos |
| `poll` | object | A question plus two or more answers |
| `location` | object | `address`, `lat`, `lng` |

**Mentions** use the syntax `@{alice@example.com}` inside `body`. A deprecated variant `@{Display Name; alice@example.com}` still exists in older content; prefer the modern form when writing.

Setting `public: false` with an empty or omitted `aspects` array means the post reaches nobody. If the user wanted a private post, confirm you have aspect ids.

## 4. Verify

```
GET /api/v1/posts/{post_guid}
```

`getPostsByPostGuid` returns the post with `post_type`, `public`, `author`, `interaction_counters` and `own_interaction_state`. Check that `public` matches what the user asked for.

## 5. Delete if needed

```
DELETE /api/v1/posts/{post_guid}
```

`deletePostsByPostGuid` returns `204 No Content`. This is destructive and federated — the deletion propagates to other pods, but you cannot count on retracting content that has already been reshared. Confirm with the user before calling.

## Error handling

- `403` on `createPosts` — documented as "Failed to create the post". Upstream flags this as a wart: it comes from the non-API status message controller and would more sensibly be a `422` or `400`. **Do not read it as an authentication problem.** Check the request body first.
- `403` on `deletePostsByPostGuid` — not allowed to delete this post (it is not the user's).
- `404` on either — post not found, or not visible to this user.

## Notes

- **There is no idempotency mechanism.** `createPosts` is not safe to retry blindly — a retry after a timeout may produce a duplicate post. Prefer verifying with a stream or search read before retrying.
- Photos are served in four sizes (`raw`, `large`, `medium`, `small`); use the smallest that fits the surface.
- See `conventions/diaspora-conventions.yml` and `errors/diaspora-problem-types.yml`.
