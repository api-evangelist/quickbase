---
generated: '2026-10-18'
method: generated
name: quickbase-upsert-records
description: Insert or update Quickbase records in one call, keyed on a merge field,
  and confirm the result.
api: openapi/quickbase-openapi.yml
operations:
- getFields
- upsert
- runQuery
source: Grounded in openapi/quickbase-openapi.yml; operationIds verified verbatim.
  Auth/headers per https://developer.quickbase.com/auth and /headers.
---

# Upsert records

Insert or update Quickbase records in one call, keyed on a merge field, and confirm the result.

## Auth

Every call goes to https://api.quickbase.com/v1 with headers `QB-Realm-Hostname: {realm}.quickbase.com`, `Authorization: QB-USER-TOKEN {token}` (or `QB-TEMP-TOKEN` for a temporary token) and a `User-Agent` (https://developer.quickbase.com/auth, /headers). Errors are documented at https://developer.quickbase.com/errors.

## Steps

1. `getFields` on the target table to find field ids and a unique field to merge on.
2. `upsert` (POST /records) with `to` (table id), `data` (array of `{fieldId: {value: ...}}` objects), optional `mergeFieldId` (a unique field — matching rows are updated, others inserted) and `fieldsToReturn`.
3. Inspect `metadata.createdRecordIds`, `updatedRecordIds`, `unchangedRecordIds` and `lineErrors` in the response; retry only failed lines.
4. Optionally verify with `runQuery`.
Idempotency: without `mergeFieldId` a retried call inserts duplicates; use a merge field when retrying is possible.
