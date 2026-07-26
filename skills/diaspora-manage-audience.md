---
name: diaspora-manage-audience
description: Manage who sees what on diaspora* — create and organize aspects, move contacts between them, block and unblock people, and follow hashtags. These calls change the audience of content the user has already shared, so they are handled with care.
api: diaspora:diaspora-api
generated: '2026-07-20'
method: generated
source: >-
  Generated from openapi/diaspora-api-openapi.yml plus
  https://diaspora.github.io/api-documentation/routes/aspects.html, /routes/contacts.html,
  /routes/users.html and /routes/tag_followings.html.
operations:
  - getAspects
  - getAspectsByAspectId
  - createAspects
  - updateAspectsByAspectId
  - deleteAspectsByAspectId
  - getAspectsByAspectIdContacts
  - createAspectsByAspectIdContacts
  - deleteAspectsByAspectIdContactsByPersonGuid
  - createUsersByPersonGuidBlock
  - deleteUsersByPersonGuidBlock
  - getTagFollowings
  - createTagFollowings
  - deleteTagFollowingsByTagName
---

# Manage audience on diaspora*

Requires a valid access token — see `diaspora-connect-to-a-pod`.

Aspects are diaspora*'s privacy primitive. A private post is shared with a set of aspects, and visibility is evaluated against **current** aspect membership. That means moving somebody into an aspect can expose previously shared private content to them, and moving them out can withdraw it. Treat every write in this skill as a privacy-affecting operation and confirm intent with the user.

## Reading the aspect structure

```
GET /api/v1/aspects
```

`getAspects` requires `contacts:read` and returns `[{ "id": 1, "name": "Family", "order": 1 }, ...]`. Aspects use pod-local **integer ids**, not GUIDs. `getAspectsByAspectId` fetches one.

## Creating and editing aspects

`createAspects` (`POST /aspects`) takes `{ "name": "..." }` and requires `contacts:modify`.

`updateAspectsByAspectId` (`PATCH /aspects/{aspect_id}`) accepts:

| Name | Type | Meaning |
| --- | --- | --- |
| `name` | string | The aspect's name |
| `order` | integer | Position in the list; other aspects are reordered to accommodate it |

`deleteAspectsByAspectId` returns `204 No Content`.

**Deleting an aspect is destructive to audience state.** Posts shared only with that aspect lose their audience. Confirm before calling.

## Managing membership

```
GET    /api/v1/aspects/{aspect_id}/contacts
POST   /api/v1/aspects/{aspect_id}/contacts
DELETE /api/v1/aspects/{aspect_id}/contacts/{person_guid}
```

Reading needs `contacts:read`; adding and removing need `contacts:modify`. Note the asymmetry in identifiers: the aspect is an **integer id**, the person is a network-wide **GUID**.

Before adding somebody to an aspect, state plainly what it implies: they will be able to see private posts shared with that aspect.

## Blocking

```
POST   /api/v1/users/{person_guid}/block
DELETE /api/v1/users/{person_guid}/block
```

Both require `contacts:modify`.

- `409` on block — already blocked.
- `410` on unblock — no block existed.

Both are convergence, not failure. Since release 0.9.1.0, blocking a person also marks related notifications as read, so notification counts may change as a side effect.

## Following hashtags

```
GET    /api/v1/tag_followings
POST   /api/v1/tag_followings
DELETE /api/v1/tag_followings/{tag_name}
```

Reading needs `tags:read`; writing needs `tags:modify`. Tag followings are the only resource in the API keyed by a **human-readable name** rather than an id or GUID — URL-encode the tag name.

- `409` on follow — the tag was already followed.
- `410` on unfollow — the tag was not followed.

Followed tags populate `getStreamsTags`.

## Scope requirements at a glance

| Scope | Grants |
| --- | --- |
| `contacts:read` | Read aspects, aspect membership, private profiles of contacts, contacts of contacts where permitted; includes contacts hidden from public search in user search |
| `contacts:modify` | Create, rename, reorder and delete aspects; add and remove people; block and unblock |
| `tags:read` | Read tag followings and the tags stream |
| `tags:modify` | Create and delete tag followings |

Remember that `private:read` and `private:modify` depend on `contacts:read` and cannot be granted without it.

## Notes

- No idempotency mechanism exists; rely on the documented `409`/`410` semantics for safe retries of block and tag-following calls.
- `404` on a person GUID may mean the person is not visible from this pod rather than that they do not exist.
- See `scopes/diaspora-scopes.yml` and `data-model/diaspora-data-model.yml`.
