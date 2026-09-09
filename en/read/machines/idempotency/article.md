# API Retry Safety: Avoid Duplicate Social Publishing Operations

Canonical: https://theorganiclub.com/en/read/machines/idempotency/

Published: 2026-09-08T12:00:00Z
Updated: 2026-09-09T07:41:56.167Z
Language: en
Evidence: documented

Idempotency prevents repeated execution of one intent from producing multiple effects when supported by the operation’s contract.

![Numbered mechanical counter wheels inside an analogue tape deck.](https://theorganiclub.com/images/editorial/idempotency.jpg)

Retired electrician. Wikimedia Commons photograph. Resized and JPEG-compressed from the source photograph. Original source SHA1: e42ad2d38f4e8621abf96d9db7464bdb61b0c686.

## The takeaway

Idempotency prevents repeated execution of one intent from producing multiple effects when supported by the operation’s contract. It does not apply indiscriminately to every tool.

## The argument

After a timeout, do not assume nothing happened. Check state or reuse the same key for the same intent when supported. TokPortal documentation excludes some secret-bearing operations from replay. A fresh key on every retry defeats the protection you wanted.

Document what the application considers the same intent. Retrying after a lost response is not a new order; changing country or content may be. Make that distinction visible in the log. It prevents both costly duplicates and ambiguous replays after parameters change. When the service’s contract is unclear, inspect state before retrying rather than treating every timeout as proof of failure.

## A timeout is not permission to duplicate the action

When a request times out, the client knows that it did not receive a timely answer. It may not know whether the server completed the operation. Retrying a purchase or publication as a brand-new action can therefore create a duplicate. Where the service supports idempotency, use a stable key for one logical operation and preserve it across retries of that same request. Read the service's documented scope and retention rules; support for a key is not a universal promise that every endpoint behaves identically.

Store the operation's inputs, key and returned identifiers in durable state. Before retrying an uncertain result, query status or reconcile against the known identifier where the API permits it. Changing the payload while reusing the same key can also be incorrect, so treat a revised action as a separate reviewed operation. Expose an unknown state instead of collapsing it into failed. The operator needs to know when investigation is safer than another click. Reliability often comes from resisting an immediate retry, not from adding more retry loops.

### Three states, not a binary guess

- **Confirmed:** The service returned a verifiable result.

- **Rejected:** The service explicitly declined the operation.

- **Unknown:** Reconcile before issuing a potentially duplicate action.

Editorial model: a way to reason about the process, not measured platform results.

## Story: The idea in three screens.

### Retry without ordering twice.
Idempotency prevents repeated execution of one intent from producing multiple effects when supported by the operation’s contract.

### Idempotency
Idempotency prevents repeated execution of one intent from producing multiple effects when supported by the operation’s contract. It does not apply indiscriminately to every tool.

### What can mislead.
Reusing a key for a different request can create contract ambiguity.

## Story: From concept to practice.

### Keep one key per logical intent.
Adapt this to your audience, budget and test scope.

### Review documented exceptions.
Adapt this to your audience, budget and test scope.

## Put it to work

1. Keep one key per logical intent.

2. Review documented exceptions.

Limit: Reusing a key for a different request can create contract ambiguity.

## Sources

[1] https://developers.tokportal.com/mcp/

This publication is initiated by TokPortal. AI-assisted editorial production and corrections policy: https://theorganiclub.com/en/about/
