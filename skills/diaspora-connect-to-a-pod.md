---
name: diaspora-connect-to-a-pod
description: Connect an application to a diaspora* pod for the first time — confirm the pod supports the API, register the client dynamically, and obtain a scoped access token. Every other diaspora* skill depends on this one.
api: diaspora:diaspora-api
generated: '2026-07-20'
method: generated
source: >-
  Generated from openapi/diaspora-api-openapi.yml plus
  https://diaspora.github.io/api-documentation/authentication.html and /scopes.html.
operations:
  - getUser
---

# Connect to a diaspora* pod

diaspora* has no central API host. Before any other skill can run, you must pick a pod, prove it speaks API v1, register yourself with it, and get a token. Do not skip the discovery steps — a pod running an older release will simply 404 and give you no useful signal about why.

## 1. Establish which pod

Ask the user which pod their account is on, or read it from configuration. It is the host part of their diaspora ID: for `alice@diaspora.social` the pod is `diaspora.social`.

Never assume a default. A token from one pod is worthless on another, and the user's data exists only on their own pod.

## 2. Confirm the pod supports the API

```
GET https://{pod}/.well-known/nodeinfo
```

Follow the returned link to the NodeInfo document and check the diaspora* version. API v1 is officially supported from release 0.9.0.0 onward. The API documentation is explicit that version discovery should happen before any request; once you have seen a compatible version on a pod, you may assume it stays compatible and cache that fact.

If the pod is too old, stop and tell the user. Do not proceed and let calls fail one by one.

## 3. Discover the OpenID Connect endpoints

```
GET https://{pod}/.well-known/openid-configuration
```

Read `registration_endpoint`, `authorization_endpoint` and `token_endpoint` from the response. Also read `scopes_supported` — it tells you what this specific pod will grant.

## 4. Register the client on this pod

Because an application cannot be pre-registered on every pod in a decentralized network, diaspora* implements OpenID Connect Dynamic Client Registration 1.0.

```
POST {registration_endpoint}
Content-Type: application/json

{
  "client_name": "<your application name>",
  "redirect_uris": ["<your redirect URI>"]
}
```

Store the returned `client_id` and `client_secret` **keyed by pod host**. They are valid only for that pod. Registering again on every run creates orphan client records on the pod — persist them.

## 5. Request an access token

Run the OpenID Connect Authorization Code Flow (native and server-side apps) or Implicit Flow (browser apps) against the discovered endpoints.

Request the narrowest scope set the task needs:

- `openid` is **mandatory**. Without it authentication fails outright.
- `public:read` is granted whether you ask or not; you cannot opt out.
- `private:read` and `private:modify` are only grantable **alongside `contacts:read`**. Requesting them without it will not work.
- A read-only agent typically needs: `openid`, `profile`, `contacts:read`, `private:read`.
- Adding writes means `public:modify` and/or `private:modify`, plus `interactions` for comments, likes, reports, votes, subscribe/mute/hide.

**Granted scopes may differ from what you requested.** Inspect the granted set in the token response and degrade gracefully rather than assuming.

## 6. Verify the token

```
GET https://{pod}/api/v1/user
Accept: application/json
Authorization: Bearer <access_token>
```

`getUser` requires the `profile` scope and returns the authenticated user's `guid`, `diaspora_id`, `name` and profile fields. A successful call confirms the whole chain.

## Error handling

- `401` — no token or an invalid token. Re-authenticate.
- `403` — the token is valid but was not granted this endpoint's scope. **Do not re-authenticate blindly**; work out which scope is missing and request it explicitly. The body is empty in this case.

## Notes

- Send `Accept: application/json` on every request. JSON is the only supported media type.
- Prefer the `Authorization: Bearer` header over the `access_token` query parameter, which leaks tokens into logs and referrers.
- See `scopes/diaspora-scopes.yml` for the full scope reference and `authentication/diaspora-authentication.yml` for the endpoint details.
