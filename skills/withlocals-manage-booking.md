---
name: withlocals-manage-booking
description: Look up, amend or cancel an existing Withlocals booking through the Partner API.
api: withlocals:withlocals-partner-api
operations:
- listBookings
- getBooking
- amendBooking
- cancelBooking
---
# Manage a Withlocals booking

1. Find the booking with `listBookings`, filtering by `partnerReference`, `date` or `fromDate`/`toDate`. Or call `getBooking` by id. Bookings are ownership-scoped: another partner's booking returns 404.
2. `amendBooking` (PATCH) changes the date/time and/or party size. Withlocals may transfer the booking to another host internally. Errors: 400, 404, and `412 PRECONDITION_FAILED`.
3. `cancelBooking` (DELETE) with an optional `reason`. The booking persists with `status=CANCELLED` and `cancellationReason=CANCELLEDBYGUEST`. This is destructive, so confirm with the user first.
