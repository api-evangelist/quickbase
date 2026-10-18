---
generated: '2026-10-18'
method: generated
name: quickbase-run-a-report
description: Discover the saved reports on a Quickbase table and run one, paging with
  skip/top.
api: openapi/quickbase-openapi.yml
operations:
- getTableReports
- getReport
- runReport
source: Grounded in openapi/quickbase-openapi.yml; operationIds verified verbatim.
  Auth/headers per https://developer.quickbase.com/auth and /headers.
---

# Run a saved report

Discover the saved reports on a Quickbase table and run one, paging with skip/top.

## Auth

Every call goes to https://api.quickbase.com/v1 with headers `QB-Realm-Hostname: {realm}.quickbase.com`, `Authorization: QB-USER-TOKEN {token}` (or `QB-TEMP-TOKEN` for a temporary token) and a `User-Agent` (https://developer.quickbase.com/auth, /headers). Errors are documented at https://developer.quickbase.com/errors.

## Steps

1. `getTableReports` (GET /reports?tableId=) to list saved reports.
2. `getReport` (GET /reports/{reportId}?tableId=) to read its type, query and columns.
3. `runReport` (POST /reports/{reportId}/run?tableId=) with `skip` and `top` query parameters to page through results.
