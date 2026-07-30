---
name: Macrometa streams pub/sub
description: Create and list Macrometa GDN pub/sub streams for real-time messaging across the global data network.
api: openapi/macrometa-gdn-openapi-original.json
operations:
  - CreateStream
  - ListOfStreams
---

# Macrometa streams pub/sub

Use Macrometa GDN streams for geo-distributed pub/sub messaging.

## Auth
`Authorization: apikey <key>` (or a JWT bearer token). Scope to a geo-fabric via `/_fabric/<fabric>`.

## Steps
1. **Create a stream** — `CreateStream` (`POST /_fabric/{fabric}/_api/streams`) with the stream name and whether it is local or global.
2. **List streams** — `ListOfStreams` (`GET /_fabric/{fabric}/_api/streams`) to enumerate available streams in the fabric.
3. Produce and consume messages over the stream using the pyC8 / jsc8 SDK websocket producers and consumers (see packages/macrometa-packages.yml).

## Conventions
- Streams are geo-replicated according to the fabric's regions.
- Errors follow the `{ error, code, errorNum, errorMessage }` envelope.
- See conventions/macrometa-conventions.yml.
