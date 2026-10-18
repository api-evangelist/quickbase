---
generated: '2026-10-18'
method: generated
name: quickbase-query-records
description: Find the right table and fields in a Quickbase app, then query records
  with a where clause and page through results.
api: openapi/quickbase-openapi.yml
operations:
- getAppTables
- getFields
- runQuery
source: Grounded in openapi/quickbase-openapi.yml; operationIds verified verbatim.
  Auth/headers per https://developer.quickbase.com/auth and /headers.
---

# Query records

Find the right table and fields in a Quickbase app, then query records with a where clause and page through results.

## Auth

Every call goes to https://api.quickbase.com/v1 with headers `QB-Realm-Hostname: {realm}.quickbase.com`, `Authorization: QB-USER-TOKEN {token}` (or `QB-TEMP-TOKEN` for a temporary token) and a `User-Agent` (https://developer.quickbase.com/auth, /headers). Errors are documented at https://developer.quickbase.com/errors.

## Steps

1. `getAppTables` (GET /tables?appId=) to list the app's tables and pick the table id.
2. `getFields` (GET /fields?tableId=) to map field labels to numeric field ids — queries use ids, not labels.
3. `runQuery` (POST /records/query) with `from` (table id, required), `select` (field ids), optional `where` (Quickbase query string, e.g. `{6.EX.'Open'}`), `sortBy`, `groupBy`, and `options` (`skip`, `top`).
4. Read `metadata` in the response and keep calling `runQuery` with an increasing `options.skip` until all records are returned (https://developer.quickbase.com/pagination).
