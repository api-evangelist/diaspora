# Diaspora

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

diaspora* is a privacy-aware, decentralized, open source social network, launched in 2010 and released under the AGPL. Rather than running on servers owned by a single company, diaspora* runs as a federated network of independently operated servers called "pods" — anyone can join an existing pod or host their own, and users own their own data. Its "aspects" model lets people organize contacts into groups and control exactly which audience sees each post, alongside hashtags, mentions, reshares, likes, polls, photos and private conversations. Pods federate with each other using the diaspora* federation protocol. Since release 0.9.0.0 the project officially supports third-party applications through a documented JSON REST API at /api/v1 on every pod, authenticated with OpenID Connect Core 1.0 including Dynamic Client Registration — a necessity in a decentralized network where an application cannot pre-register with every pod it might talk to.

**Areas:** Company · Social · Social Network · Decentralized · Federated · Open Source · Privacy · Fediverse · Messaging · OpenID Connect

## Diaspora on APIs.io

Everything profiled for Diaspora is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/diaspora/](https://apis.io/providers/diaspora/)** — or go straight to one of the APIs or properties below.

### APIs (14)

- [Diaspora Aspects API](https://apis.io/apis/diaspora/diaspora-aspects-api/) — The Aspects API from Diaspora — 2 operation(s) for aspects.
- [Diaspora Comments API](https://apis.io/apis/diaspora/diaspora-comments-api/) — The Comments API from Diaspora — 3 operation(s) for comments.
- [Diaspora Contacts API](https://apis.io/apis/diaspora/diaspora-contacts-api/) — The Contacts API from Diaspora — 2 operation(s) for contacts.
- [Diaspora Conversations API](https://apis.io/apis/diaspora/diaspora-conversations-api/) — The Conversations API from Diaspora — 3 operation(s) for conversations.
- [Diaspora Likes API](https://apis.io/apis/diaspora/diaspora-likes-api/) — The Likes API from Diaspora — 2 operation(s) for likes.
- [Diaspora Notifications API](https://apis.io/apis/diaspora/diaspora-notifications-api/) — The Notifications API from Diaspora — 2 operation(s) for notifications.
- [Diaspora Photos API](https://apis.io/apis/diaspora/diaspora-photos-api/) — The Photos API from Diaspora — 2 operation(s) for photos.
- [Diaspora Post interactions API](https://apis.io/apis/diaspora/diaspora-post-interactions-api/) — The Post interactions API from Diaspora — 5 operation(s) for post interactions.
- [Diaspora Posts API](https://apis.io/apis/diaspora/diaspora-posts-api/) — The Posts API from Diaspora — 2 operation(s) for posts.
- [Diaspora Reshares API](https://apis.io/apis/diaspora/diaspora-reshares-api/) — The Reshares API from Diaspora — 1 operation(s) for reshares.
- [Diaspora Search API](https://apis.io/apis/diaspora/diaspora-search-api/) — The Search API from Diaspora — 3 operation(s) for search.
- [Diaspora Streams API](https://apis.io/apis/diaspora/diaspora-streams-api/) — The Streams API from Diaspora — 7 operation(s) for streams.
- [Diaspora Tag followings API](https://apis.io/apis/diaspora/diaspora-tag-followings-api/) — The Tag followings API from Diaspora — 2 operation(s) for tag followings.
- [Diaspora Users API](https://apis.io/apis/diaspora/diaspora-users-api/) — The Users API from Diaspora — 5 operation(s) for users.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [diaspora-mcp.yml](https://apis.io/servers/diaspora/diaspora-mcp-yml/)

#### Collections (14)

Postman and Open Collection request collections.

- [diaspora* Aspects API](https://apis.io/collections/diaspora/open-diaspora-aspects-api/)
- [diaspora* Aspects Comments API](https://apis.io/collections/diaspora/open-diaspora-comments-api/)
- [diaspora* Aspects Contacts API](https://apis.io/collections/diaspora/open-diaspora-contacts-api/)
- [diaspora* Aspects Conversations API](https://apis.io/collections/diaspora/open-diaspora-conversations-api/)
- [diaspora* Aspects Likes API](https://apis.io/collections/diaspora/open-diaspora-likes-api/)
- [diaspora* Aspects Notifications API](https://apis.io/collections/diaspora/open-diaspora-notifications-api/)
- [diaspora* Aspects Photos API](https://apis.io/collections/diaspora/open-diaspora-photos-api/)
- [diaspora* Aspects Post interactions API](https://apis.io/collections/diaspora/open-diaspora-post-interactions-api/)
- [diaspora* Aspects Posts API](https://apis.io/collections/diaspora/open-diaspora-posts-api/)
- [diaspora* Aspects Reshares API](https://apis.io/collections/diaspora/open-diaspora-reshares-api/)
- [diaspora* Aspects Search API](https://apis.io/collections/diaspora/open-diaspora-search-api/)
- [diaspora* Aspects Streams API](https://apis.io/collections/diaspora/open-diaspora-streams-api/)
- [diaspora* Aspects Tag followings API](https://apis.io/collections/diaspora/open-diaspora-tag-followings-api/)
- [diaspora* Aspects Users API](https://apis.io/collections/diaspora/open-diaspora-users-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Diaspora Api Overlay](https://apis.io/overlays/diaspora/diaspora-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Diaspora Authentication](https://apis.io/security/diaspora/diaspora-authentication/)
- [Diaspora Domain Security](https://apis.io/security/diaspora/diaspora-domain-security/)
- [Diaspora Vulnerability Disclosure](https://apis.io/security/diaspora/diaspora-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Diaspora Scopes](https://apis.io/scopes/diaspora/diaspora-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://diasporafoundation.org/)
- [Documentation](https://diaspora.github.io/api-documentation/)
- [Getting started](https://diasporafoundation.org/tutorials)
- [API reference](https://diaspora.github.io/api-documentation/)
- [Sign up](https://diasporafoundation.org/getting_started/sign_up)
- [Support](https://discourse.diasporafoundation.org/)
- [Changelog](https://raw.githubusercontent.com/diaspora/diaspora/develop/Changelog.md)
- [Blog](https://blog.diasporafoundation.org/)
- [GitHub](https://github.com/diaspora)

## API Evangelist rating

**Kin Score 42.3** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 51.8 |
| Contract governance | 4.5 |
| Operational transparency | 39.5 |
| Developer ergonomics | 58.9 |
| Access clarity | 13.2 |

**Agent readiness 28.7** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | negotiable (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | documented (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 32.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/diaspora/](https://apis.io/providers/diaspora/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Diaspora: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/diaspora/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
