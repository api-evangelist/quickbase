---
generated: '2026-10-18'
method: generated
name: quickbase-manage-group-membership
description: Add or remove users, managers and subgroups on a Quickbase group.
api: openapi/quickbase-openapi.yml
operations:
- getUsers
- addMembersToGroup
- removeMembersFromGroup
- addManagersToGroup
- addSubgroupsToGroup
source: Grounded in openapi/quickbase-openapi.yml; operationIds verified verbatim.
  Auth/headers per https://developer.quickbase.com/auth and /headers.
---

# Manage group membership

Add or remove users, managers and subgroups on a Quickbase group.

## Auth

Every call goes to https://api.quickbase.com/v1 with headers `QB-Realm-Hostname: {realm}.quickbase.com`, `Authorization: QB-USER-TOKEN {token}` (or `QB-TEMP-TOKEN` for a temporary token) and a `User-Agent` (https://developer.quickbase.com/auth, /headers). Errors are documented at https://developer.quickbase.com/errors.

## Steps

1. `getUsers` (POST /users) to look up user ids in the account.
2. `addMembersToGroup` / `removeMembersFromGroup` (POST/DELETE /groups/{gid}/members) with an array of user ids.
3. `addManagersToGroup` to grant group management; `addSubgroupsToGroup` to nest groups.
These calls require account/realm admin rights for the token's user.
