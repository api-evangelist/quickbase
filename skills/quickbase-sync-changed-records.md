---
generated: '2026-10-18'
method: generated
name: quickbase-sync-changed-records
description: Incrementally pull records modified since a timestamp and delete records
  that match a filter.
api: openapi/quickbase-openapi.yml
operations:
- recordsModifiedSince
- runQuery
- deleteRecords
source: Grounded in openapi/quickbase-openapi.yml; operationIds verified verbatim.
  Auth/headers per https://developer.quickbase.com/auth and /headers.
---

# Sync changed records

Incrementally pull records modified since a timestamp and delete records that match a filter.

## Auth

Every call goes to https://api.quickbase.com/v1 with headers `QB-Realm-Hostname: {realm}.quickbase.com`, `Authorization: QB-USER-TOKEN {token}` (or `QB-TEMP-TOKEN` for a temporary token) and a `User-Agent` (https://developer.quickbase.com/auth, /headers). Errors are documented at https://developer.quickbase.com/errors.

## Steps

1. `recordsModifiedSince` (POST /records/modifiedSince) with `from` (table id) and `after` (timestamp), optional `fieldList` and `includeDetails`, to learn what changed since the last sync.
2. `runQuery` to fetch the full changed rows by record id.
3. `deleteRecords` (DELETE /records) with `from` and `where` (both required) to remove records matching a filter — destructive; confirm the `where` clause with `runQuery` first.
