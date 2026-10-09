---
name: withlocals-webhooks
description: Register, inspect and remove the Withlocals booking-cancelled webhook and handle its deliveries.
api: withlocals:withlocals-partner-api
operations:
- setWebhook
- getWebhook
- deleteWebhook
---
# Withlocals webhooks

1. `setWebhook` (PUT /webhooks) returns 201 on the first registration, and that response includes a signing `secret`. Save it, because it is never returned again. Later calls update the URL and return 200.
2. `getWebhook` shows the current URL without the secret. It returns 404 when nothing is registered.
3. `deleteWebhook` stops all deliveries (204).

Event `bookingCancelled` is sent as a POST with JSON when any booking becomes CANCELLED. Delivery is at least once and retried for about 24h with backoff, so dedupe on `eventId`.
