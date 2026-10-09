---
name: withlocals-book-experience
description: Find a Withlocals product, check its availability and create a confirmed booking through the Partner API.
api: withlocals:withlocals-partner-api
operations:
- listProducts
- getProduct
- availabilityCalendar
- createBooking
- getBooking
---
# Book a Withlocals experience

Auth: `Authorization: Bearer <partner token>`. Test base URL: `https://test-api.withlocals.com/v1/partner`.

1. `listProducts` (page / pageSize) to find a bookable product. Then call `getProduct` for its details.
2. `availabilityCalendar` with the productId and a `from`/`to` date range. It returns one entry per day, in ascending order.
3. `createBooking` for an available day. Send an `Idempotency-Key` header so a retry is safe, and reuse the same key on every retry. Note that `getSupplier` reports `supportsIdempotencyKey: false`, so dedupe on your partnerReference as well.
4. `getBooking` to confirm that the status is `CONFIRMED`.

Errors: `400 BAD_REQUEST`, `401 UNAUTHORIZED`, `404 NOT_FOUND` (product unknown or not bookable), and `409 CONFLICT` (slot no longer available). On a 409, re-read the availability before trying again.
