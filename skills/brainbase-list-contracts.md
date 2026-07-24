---
name: List Brainbase licensing contracts
description: Retrieve the licensing/IP contracts associated with the authenticated user from the Brainbase API v1, with filtering, search and pagination.
api: openapi/brainbase-openapi-original.json
operations:
  - ApiContractController__userAssociatedContracts
---

# List Brainbase licensing contracts

Use this skill to page through the licensing, partnership and sponsorship
contracts associated with the authenticated Brainbase user.

## Authentication

Brainbase API v1 uses HTTP bearer authentication with a JWT access token. Send it
on every request:

```
Authorization: Bearer <JWT>
```

See `authentication/brainbase-authentication.yml`.

## Steps

1. Call `GET /api/user/contracts` (operationId
   `ApiContractController__userAssociatedContracts`) at base URL
   `https://api.brainbase.com`.
2. Control the result window with the `page` (page number) and `maxRows` (max
   count of rows) query parameters. Pagination is page-number style — see
   `conventions/brainbase-conventions.yml`.
3. Apply filtering/search through the endpoint's query parameters as documented at
   `https://api.brainbase.com/docs`.
4. Read the returned contract rows and advance `page` until fewer than `maxRows`
   rows are returned.

## Notes

- No idempotency contract is documented; this is a read operation so retries are
  safe.
- The public spec declares only a `200` response; handle non-200 responses
  defensively (auth failures, empty pages).
