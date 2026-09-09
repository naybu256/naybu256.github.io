# Social Publishing Webhooks: Events, Status and Recovery

Canonical: https://theorganiclub.com/en/read/machines/webhooks/

Published: 2026-09-08T12:00:00Z
Updated: 2026-09-09T07:41:56.167Z
Language: en
Evidence: editorial

A webhook sends an event to your integration.

![A vintage telegraph machine and its brass components displayed on a wooden base.](https://theorganiclub.com/images/editorial/webhooks.jpg)

Homoatrox. Wikimedia Commons photograph. Resized and JPEG-compressed from the source photograph. Original source SHA1: e87da8fd61b405505186536d68723e07cd1b94f9.

## The takeaway

A webhook sends an event to your integration. Consumers should verify authenticity, handle repetition and reconcile state under the documented contract.

## The argument

Do not assume events arrive exactly once or in the expected order. Retain identifiers when provided and allow reading current state. Signing secrets belong in appropriate storage, not client code. Users then see progress grounded in verified events.

A consumer can retain the latest confirmed state and receipt time. If an event appears contradictory, reading source state can resolve it under the available contract. Keep an incident record without exposing the signing secret. Reliability is built in these recovery paths, not merely in receiving the first demonstration event. Test duplicate and delayed delivery cases before depending on the integration for unattended decisions.

## Treat the notification as a delivery system

A webhook tells your system that an event was sent; it does not automatically guarantee that the event will arrive once, in order, or at a convenient time. Design the receiver around the provider's documented delivery contract. Verify authenticity using the supported mechanism, reject malformed payloads, and acknowledge only after the event has been safely accepted for processing. Keep the public endpoint narrow. It should not turn arbitrary event text into an instruction for an agent with publishing or spending permissions.

Deduplicate with stable event identifiers where available and make handlers safe to repeat. If two events arrive out of order, use the underlying resource state or documented sequence information to reconcile them instead of letting the last network arrival blindly win. Record processing failures and provide a replay path with bounded retries. Avoid storing more payload data than the operation needs. A webhook integration earns its keep when an operator can answer which event arrived, what it changed and how to recover if that change did not complete.

### Receive, record, reconcile

- **Verify:** Authenticate the delivery through the provider contract.

- **Persist:** Keep the event identifier and processing state.

- **Apply:** Update the operation safely, including duplicates.

Editorial model: a way to reason about the process, not measured platform results.

## Story: The idea in three screens.

### A webhook reports an event. It does not replace your state.
A webhook sends an event to your integration.

### Webhooks
A webhook sends an event to your integration. Consumers should verify authenticity, handle repetition and reconcile state under the documented contract.

### What can mislead.
A received event is trustworthy only after service-appropriate checks.

## Story: From concept to practice.

### Apply documented verification.
Adapt this to your audience, budget and test scope.

### Plan deduplication and reconciliation.
Adapt this to your audience, budget and test scope.

## Put it to work

1. Apply documented verification.

2. Plan deduplication and reconciliation.

Limit: A received event is trustworthy only after service-appropriate checks.

## Sources

This publication is initiated by TokPortal. AI-assisted editorial production and corrections policy: https://theorganiclub.com/en/about/
