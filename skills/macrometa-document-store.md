---
name: Macrometa document store
description: Create a collection, insert and read documents, and run a C8QL query against the Macrometa GDN.
api: openapi/macrometa-gdn-openapi-original.json
operations:
  - handleCommandPost:CreateCollection
  - insertDocument
  - readDocument
  - createQueryCursor
---

# Macrometa document store

Use the Macrometa GDN REST API to store and query documents in a geo-fabric.

## Auth
Send an API key on every request: `Authorization: apikey <key>` (or a JWT: `Authorization: bearer <jwt>`).
Requests are scoped to a geo-fabric via the `/_fabric/<fabric>` path segment (default `_system`).

## Steps
1. **Create a collection** — `handleCommandPost:CreateCollection` (`POST /_fabric/{fabric}/_api/collection`) with a JSON body `{ "name": "<collection>" }`.
2. **Insert a document** — `insertDocument` (`POST /_fabric/{fabric}/_api/document/{collection}`) with the document body. The response returns the document `_key`/`_id`.
3. **Read a document** — `readDocument` (`GET /_fabric/{fabric}/_api/document/{collection}/{key}`) using the `_key` returned above.
4. **Query** — `createQueryCursor` (`POST /_fabric/{fabric}/_api/cursor`) with a C8QL query, e.g. `{ "query": "FOR d IN <collection> RETURN d" }`. Page through results using the cursor `id` while `hasMore` is true.

## Conventions
- Errors return a JSON envelope `{ error, code, errorNum, errorMessage }` — see errors/macrometa-problem-types.yml.
- No idempotency-key header is supported; treat writes as non-idempotent.
- See conventions/macrometa-conventions.yml for pagination and tenancy details.
