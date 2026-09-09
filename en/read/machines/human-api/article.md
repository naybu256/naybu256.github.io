# TokPortal’s Human API: Briefs, Native Actions and Receipts

Canonical: https://theorganiclub.com/en/read/machines/human-api/

Published: 2026-09-08T12:00:00Z
Updated: 2026-09-09T07:41:56.167Z
Language: en
Evidence: documented

A Human API exposes a software workflow partly executed by people.

![A worker operates an antique printing press inside a working print shop.](https://theorganiclub.com/images/editorial/human-api.jpg)

Caelb375. Wikimedia Commons photograph. Resized and JPEG-compressed from the source photograph. Original source SHA1: 2aa5baf9386557b730ec488a397287c9d71e5e4b.

## The takeaway

A Human API exposes a software workflow partly executed by people. In TokPortal’s context, orchestration and native interaction are separate layers.

## The argument

A call may create a mission rather than immediately publish a post. Integrations therefore need waiting, status and correction handling. Design around the real cycle: request received, work executed, result verified. Hiding latency behind instant success misrepresents what happened.

A client interface can show request accepted before publication verified. Add handling for delays and corrections. This matters for agents: they should not analyze a mission as though it were already a visible post. The software contract should respect the actual time of human work. Clear intermediate states make integrations more useful without promising instantaneous execution the underlying operation does not provide.

## Make the handoff executable by a person

A human operator is not a magic endpoint that repairs every vague request. If the task is to publish a post, the handoff needs an account identifier, approved asset, caption, timing constraints and a definition of completion. Include the relevant rights and any feature that must be applied inside the platform. Replace instructions such as make it feel native with concrete observations the operator can act on. The human's judgement should be reserved for real ambiguity, not spent guessing which file named final is actually approved.

Ask for evidence proportional to the operation. A public URL and completion timestamp may be enough for an ordinary post; a failed task needs a clear state and reason rather than a generic done message. Do not require screenshots containing unnecessary personal or account information. Keep a route for clarification and a rule against improvising outside the authorised scope. The advantage of a human handoff is contextual judgement where interfaces remain awkward. Treating the person as invisible glue makes that judgement difficult to review and the process difficult to improve.

### A useful operator contract

- **Input:** Account, approved version and publishing constraints.

- **Decision:** Explicit room for judgement and escalation.

- **Receipt:** Result URL, time and any unresolved exception.

Editorial model: a way to reason about the process, not measured platform results.

## Story: The idea in three screens.

### Behind the API, someone actually opens the app.
A Human API exposes a software workflow partly executed by people.

### Human API
A Human API exposes a software workflow partly executed by people. In TokPortal’s context, orchestration and native interaction are separate layers.

### What can mislead.
A successful HTTP response can confirm request creation without confirming final execution.

## Story: From concept to practice.

### Separate acceptance from delivery.
Adapt this to your audience, budget and test scope.

### Plan status feedback and correction handling.
Adapt this to your audience, budget and test scope.

## TokPortal workflow: Prepare the actual video slot, not just the caption

TokPortal’s editor distinguishes Video, Carousel and Story, and asks for a target publishing period. The API follows the same operational idea: the content needs a valid format, accessible media and a usable window.

Endpoint: PUT /api/ext/bundles/{id}/videos/{position}

```json
{
  "tool": "tokportal_configure_bundle_video",
  "arguments": {
    "id": "<real-bundle-uuid>",
    "position": 1,
    "body": {
      "video_type": "video",
      "video_url": "<public_url returned by your video upload>",
      "description": "A practical example of organising freelance subscriptions.",
      "target_publish_date": "<valid future date: YYYY-MM-DD>"
    }
  }
}
```

Replace the marked values with your actual upload and bundle. This template is intentionally not a runnable campaign. target_publish_date starts a two-day publishing window; it does not request an exact minute.

- **Choose the correct media fields:** A video needs video_url and description. A TikTok carousel instead needs carousel_images and tiktok_sound_url.

- **Use a valid window:** Allow at least three days while account creation is pending, or one day for delivered/existing accounts. Check the current response and limits.

- **Inspect readiness:** GET /api/ext/bundles/{id}/publish-readiness lists blockers without a debit or mutation. Review ignored_fields and the returned start/end dates.

## Put it to work

1. Separate acceptance from delivery.

2. Plan status feedback and correction handling.

Limit: A successful HTTP response can confirm request creation without confirming final execution.

## Sources

[1] https://developers.tokportal.com/

- https://developers.tokportal.com/mcp/

This publication is initiated by TokPortal. AI-assisted editorial production and corrections policy: https://theorganiclub.com/en/about/
