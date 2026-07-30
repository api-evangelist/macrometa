---
name: Macrometa API key management
description: Create, validate, and list Macrometa GDN API keys and set their access levels.
api: openapi/macrometa-gdn-openapi-original.json
operations:
  - CreateApiKey
  - ListAvailableApiKeys
  - ValidateApiKey
  - SetTheDatabaseAccessLevelForApiKey
---

# Macrometa API key management

Provision and scope API keys for programmatic access to the GDN.

## Auth
Authenticate as a user (JWT bearer) or with an existing API key that has key-management permissions.

## Steps
1. **Create an API key** — `CreateApiKey` (`POST /_fabric/{fabric}/_api/key`) returns the new key and its id.
2. **List keys** — `ListAvailableApiKeys` to enumerate the keys visible to the caller.
3. **Grant database access** — `SetTheDatabaseAccessLevelForApiKey` to set `rw`/`ro`/`none` on a given database for the key.
4. **Validate** — `ValidateApiKey` to confirm a key is active before using it.

## Conventions
- Access levels cascade: database, then collection, then stream — set the narrowest scope needed.
- Errors follow the `{ error, code, errorNum, errorMessage }` envelope.
- See authentication/macrometa-authentication.yml and conventions/macrometa-conventions.yml.
