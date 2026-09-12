# TokPortal video reschedule: use PATCH for partial edits, PUT for replacement

Canonical: https://theorganiclub.com/en/read/machines/tokportal-video-reschedule-patch-or-put/

Published: 2026-09-12T11:39:50.620Z
Updated: 2026-09-12T11:39:50.620Z
Language: en
Evidence: editorial

If a TokPortal video slot already contains the right media, the safer default for caption or date changes is PATCH. The docs make PUT a full replacement, which means omitted fields are cleared rather than preserved.

![Editorial desk scene with scheduling notes and two workflow paths representing partial edit versus full replacement for a video slot.](https://theorganiclub.com/images/daily/tokportal-video-reschedule-patch-or-put.jpg)

THE ORGANIC CLUB Studio. Original AI-generated editorial illustration. Illustrative scene, not documentary evidence.

## The takeaway

Choose PATCH when you are changing lightweight metadata or the publish window on an existing slot. Reserve PUT for intentional full-slot replacement, and dry-run the write before any live execution.

## The argument

A narrow API choice can create a very practical editorial failure. Suppose a team has already configured a TokPortal video slot with the correct media, sound, and platform-specific fields. Later, someone only wants to adjust the caption or move the publishing window. At that moment, the question is not abstract REST style. It is whether the operator should resend the full slot with PUT or make a smaller change with PATCH. TokPortal’s current configuration docs answer that directly: single-slot PUT is a full-replace write, so omitted fields are cleared, while PATCH exists for lightweight metadata edits and rescheduling [1]. For an AI-assisted workflow, that distinction matters because “reconstruct the whole object from memory” is exactly where accidental field loss becomes likely.

The safest default is therefore simple: if the slot’s media configuration is already correct and you do not intend to redefine it, use PATCH. TokPortal documents PATCH /bundles/:id/videos/:position as the endpoint for updating external_ref, name, description, or schedule without re-uploading content [1]. The same page explicitly describes it as the reschedule endpoint, and the only place where the publishing window’s end day can be chosen [1]. That last detail is easy to miss. On configure PUT, target_publish_date represents a two-day window whose end is derived automatically; target_publish_end_date is not valid there [1]. So this is not only about reducing risk. It is also about choosing the endpoint that exposes the scheduling control you actually need.

PUT still has a valid role, but it is narrower than many operators assume. Use it when your intent is to define the slot’s complete configuration: media type, asset fields, caption, schedule, and any applicable extras. TokPortal warns that PUT /bundles/:id/videos/:position and batch PUT both replace the slot’s entire configuration, and a field you omit is cleared rather than preserved [1]. The docs also note a related change in validation behavior: an unrecognized field is now refused with 400 UNKNOWN_FIELD instead of being silently stripped in the full-replace flow [1]. That reduces one class of silent mistakes, but it does not solve the more ordinary one: sending a technically valid body that is incomplete for your real intent. In other words, a well-formed PUT can still be the wrong operational choice.

A reusable procedure for agents and human operators is: first classify the intended change, then choose the smallest write surface that matches it. Step 1: list the fields that truly need to change. Step 2: if the set is limited to external_ref, name, description, or scheduling fields, prefer PATCH [1]. Step 3: if the change requires redefining media or other slot-defining fields, prepare a full PUT body and treat it as authoritative replacement [1]. Step 4: run a dry run before live execution so the request goes through the same validation and pricing path but stops before the first write; TokPortal documents that a dry run creates no rows, debits no credits, and fires no webhook [2]. Step 5: only after validation passes should the operator send the real call. This sequence is a workflow choice, not a platform requirement. The platform requires valid inputs; the extra classification step is how you avoid self-inflicted configuration loss.

One more detail changes the practical rescheduling rule: PATCH is no longer a loophole around date validation. TokPortal’s docs state that rescheduling now obeys the same minimum lead time as configuration, with earlier dates rejected as INVALID_DATE and the response carrying details such as min_days_ahead and earliest_allowed [1]. The exact minimum depends on bundle state: today + 3 while an account is still being created, and today + 1 for a delivered or existing account, in UTC [1]. That means PATCH is safer for preserving slot fields, but not looser about scheduling. An agent that used to think “PATCH is just a harmless date tweak” should instead treat it as a real write subject to operational constraints.

Worked example — HYPOTHETICAL SAMPLE INPUTS. Imagine a delivered account with bundle ID bnd_example_01 and slot position 1. The slot already contains a valid video_url, an approved description, and a TikTok sound URL. Editorial review decides only two things should change: the caption needs one clarification, and the acceptable publishing window should move from a start date of 2026-09-14 to an explicit UTC window spanning 2026-09-15T00:00:00Z through 2026-09-16T00:00:00Z. Because the media and platform-specific settings should remain untouched, the safer operation is a dry-run PATCH, not a reconstructive PUT. A hypothetical MCP-style request would look like this: {"name":"tokportal_patch_bundle_video","arguments":{"dry_run":true,"id":"bnd_example_01","position":1,"body":{"description":"Clarified caption for the same video asset.","target_publish_start_date":"2026-09-15T00:00:00Z","target_publish_end_date":"2026-09-16T00:00:00Z"}}}. The important point is not this exact JSON. It is the decision logic behind it: use PATCH because the intended edit is partial, and use dry_run because the same validation can be checked without producing live side effects [1][2].

For agent design, this suggests a durable rule: do not let the endpoint be selected merely by which schema your system happens to cache. Let it be selected by intent. If intent equals “replace the whole slot,” use PUT. If intent equals “preserve the slot and alter only lightweight metadata or timing,” use PATCH [1]. Add two guardrails from the docs. First, log the API version and request ID headers returned by the server, because TokPortal treats the public API as a versioned stable contract and includes a request identifier for correlation [3]. Second, treat dry runs and live calls as separate states in your audit trail; the sandbox docs are explicit that dry-run identifiers are synthetic, do not exist live, and should not be carried into real requests [2]. That combination—intent-based endpoint choice, preview before write, and version-aware logging—is a more robust operating pattern than “always PUT the latest object.”

## A small endpoint decision becomes an editorial reliability rule

The interesting lesson here is broader than one reschedule endpoint. Many AI-assisted publishing failures do not come from dramatic bugs; they come from a mismatch between user intent and write semantics. Human operators often say “update the post,” but an API may distinguish between merge-like edits and authoritative replacement. TokPortal makes that distinction unusually explicit. PATCH is for limited metadata and schedule changes; PUT is full replacement [1]. If you are building an agent layer, that documented difference should become a routing rule rather than a note buried in a developer handbook.

That rule matters most when a slot contains platform-specific fields the reviewer is not looking at during the last-minute edit. A caption reviewer may not remember whether a TikTok sound URL, carousel assets, or other settings were already configured. Choosing PUT in that situation forces the system to restate everything correctly. Choosing PATCH lets the system preserve what is already correct while changing only the intended subset [1]. The advantage is not speed for its own sake. The advantage is narrower blast radius.

The sandbox docs strengthen this pattern because they let a team treat preview as part of the write process instead of a separate environment [2]. Dry run is not a marketing simulation and not a reach predictor; it is a contract-level rehearsal of the exact request path, with identical validation and pricing logic but no live side effects [2]. For editorial operations, that means you can check whether a reschedule is too early, whether a field combination is invalid, or whether your tool is accidentally using a synthetic ID—before any irreversible action occurs.

Finally, versioning is a quiet but useful part of the answer. TokPortal states a stable public API version and returns request IDs on every response [3]. That means a team can record not just that a slot failed to update, but under which contract version and which server-correlated request. The endpoint decision itself is editorially simple—PATCH for partial edits, PUT for replacement—but the durable practice is operational: choose by intent, preview before writing, and log enough context to explain what happened later.

### Endpoint selection for an existing video slot

- **1. Identify change:** List only the fields you actually intend to alter.

- **2. Partial fields only?:** If the change is metadata or schedule, route toward PATCH.

- **3. Need full redefinition?:** If media or full slot config changes, prepare a complete PUT body.

- **4. Dry-run validation:** Preview the exact request before any live write.

- **5. Execute live:** Send the reviewed request and log version plus request ID.

Illustrative decision flow; values show layout only, not measured data.

## Story: How to choose PATCH vs PUT

### Start with intent
Ask one question first: am I preserving this slot and changing only metadata or timing, or am I redefining the whole slot? Endpoint choice follows that answer, not habit.

### PATCH protects existing setup
TokPortal documents PATCH for lightweight metadata edits and rescheduling. That makes it the safer default when media and platform-specific fields should stay as they are [1].

### PUT is authoritative replacement
Use PUT when you want the submitted body to become the slot’s full configuration. If you omit a field, the docs say it is cleared rather than preserved [1].

## Story: Why dry run belongs in the workflow

### Validate before writing
TokPortal’s dry run uses the same validation and pricing path as the real request, then stops before the first write [2].

### Separate preview from execution
A simulated success is not a live change. No credits are debited, no row is written, and dry-run IDs are synthetic [2].

### Then execute live deliberately
After the preview passes, resend the intended live request with the same carefully reviewed body. This is a workflow choice for safety, not a platform mandate.

## TokPortal workflow: Prepare the actual video slot, not just the caption

In the archived editor capture, the interface shows Video, Carousel and Story options, plus a target publishing period. The API example below is a separate documented slot-configuration preview; the screenshot alone does not establish the API contract.

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
      "target_publish_date": "<valid future date: YYYY-MM-DD>",
      "ai_content_disclaimer": false,
      "auto_publish": false
    },
    "dry_run": true
  }
}
```

Replace the marked values with an authorized real bundle, a media URL you control and a valid future date. This is a dry-run template, not an executed campaign. The archived UI shows a two-day period for that captured example; use the current API validation response to determine the dates accepted for your own request.

- **Choose the correct media fields:** A video needs video_url and description. A TikTok carousel instead needs carousel_images and tiktok_sound_url.

- **Use a valid window:** Allow at least three days while account creation is pending, or one day for delivered/existing accounts. Check the current response and limits.

- **Read the preview result:** Check the simulation markers and date validation. If INVALID_DATE includes details.earliest_allowed, use that returned limit to revise the proposed date. Never copy preview IDs into live requests.

## Put it to work

1. Classify each requested slot edit as partial change or full replacement before choosing an endpoint.

2. Use PATCH for caption, name, external_ref, and schedule changes on an existing editable slot.

3. Use PUT only when you intend the body to become the slot’s entire authoritative configuration.

4. Dry-run every unfamiliar or consequential write, then repeat live only after reviewing validation output.

5. Store request ID, API version, and the exact request body used so later debugging is possible.

Limit: The common mistake is assuming PUT behaves like a merge. In TokPortal’s documented contract, single-slot PUT is full replacement, so an omitted valid field can be cleared even when the request itself succeeds [1].

## Sources

[1] https://developers.tokportal.com/configure-videos/

[2] https://developers.tokportal.com/sandbox/

[3] https://developers.tokportal.com/versioning/

- https://developers.tokportal.com/mcp/

- https://developers.tokportal.com/use-cases/no-code/mp4-delivered-account-preview/

This publication is initiated by TokPortal. AI-assisted editorial production and corrections policy: https://theorganiclub.com/en/about/
