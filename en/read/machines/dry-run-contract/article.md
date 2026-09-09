# What Does a TokPortal Dry Run Do? Preview Scope and Limits

Canonical: https://theorganiclub.com/en/read/machines/dry-run-contract/

Published: 2026-09-08T12:00:00Z
Updated: 2026-09-09T07:41:56.167Z
Language: en
Evidence: documented

A dry run validates a request without producing live effects under the service’s contract.

![Mary Jackson holds an aircraft model inside a wind tunnel at NASA Langley.](https://theorganiclub.com/images/editorial/dry-run-contract.jpg)

NASA; restoration by Adam Cuerden. Wikimedia Commons photograph. Resized and JPEG-compressed from the source photograph. Original source SHA1: 42976da6950d21d2f0ae93640659121b482a3bab.

## The takeaway

A dry run validates a request without producing live effects under the service’s contract. It does not guarantee future capacity or outcomes.

## The argument

In TokPortal MCP, dry_run belongs at the top argument level, not inside body. The local version must support that contract. Read response fields for simulated and actual charges. Preview identifiers remain synthetic: moving live requires creating and using actual resources.

Show the mode, request and reported charges in the human-readable result. Do not say account created when the service only validated a preview. That wording prevents another agent from continuing work against an imaginary resource. The boundary should be both technical and understandable in the report, especially when output is copied into another task without the full execution history attached.

## A preview should answer the expensive questions

A dry run is valuable when it shows what the live operation would target, create and cost without performing those side effects. Its contract should say which validations are real and which outcomes remain unknowable until execution. A preview that merely echoes the request can still be useful, but it must not be presented as proof that the live action will succeed. Inspect the documented response fields and retain the exact proposed inputs so the eventual approval refers to a concrete operation.

Bind the approved preview to the execution version. If the country, account, asset or quantity changes afterwards, the old preview no longer describes the new request. Recheck the fields that determine scope and cost before proceeding. Keep credentials out of logs and distinguish a preview identifier from a completed order identifier. For TokPortal, consult the current sandbox and MCP documentation for supported dry-run behaviour rather than assuming every tool has identical semantics. The point is to make consequences legible before execution and the eventual result traceable afterwards.

### A preview is a versioned proposal

- **Prepare:** Freeze the intended inputs and destination.

- **Inspect:** Review supported validation, scope and cost.

- **Execute:** Use the approved version and verify its result.

Editorial model: a way to reason about the process, not measured platform results.

## Story: The idea in three screens.

### A preview must know what it does not simulate.
A dry run validates a request without producing live effects under the service’s contract.

### Dry-run contract
A dry run validates a request without producing live effects under the service’s contract. It does not guarantee future capacity or outcomes.

### What can mislead.
A successful preview neither authorizes spending nor reserves capacity.

## Story: From concept to practice.

### Check version and preview response.
Adapt this to your audience, budget and test scope.

### Keep an explicit boundary before live execution.
Adapt this to your audience, budget and test scope.

## TokPortal workflow: What the sandbox actually guarantees

The official sandbox page makes a useful boundary explicit: real request validation and pricing, with no created task or charge. This is an operational preview, not a simulation of TikTok reach.

Endpoint: POST /api/ext/bundles + X-TokPortal-Dry-Run: true

```json
{
  "dry_run": true,
  "dry_run_notice": "<read the actual notice returned>",
  "credits_would_charge": "<workspace-specific quote>",
  "credits_charged": 0
}
```

The fields shown are an annotated response shape. No live quote was requested for this article. Use the actual response from your connected workspace and keep any synthetic identifiers out of a live workflow.

- **Validation:** Invalid inputs still return real validation errors.

- **Pricing:** The quoted cost uses the same server-side pricing logic; the preview does not charge it.

- **Distribution:** A successful preview says nothing about the reach, retention or sales a future post will generate.

## Put it to work

1. Check version and preview response.

2. Keep an explicit boundary before live execution.

Limit: A successful preview neither authorizes spending nor reserves capacity.

## Sources

[1] https://developers.tokportal.com/sandbox/

- https://developers.tokportal.com/sandbox/

This publication is initiated by TokPortal. AI-assisted editorial production and corrections policy: https://theorganiclub.com/en/about/
