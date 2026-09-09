# How to Organize a Multi-Account Social Media Inventory

Canonical: https://theorganiclub.com/en/read/field-notes/account-inventory/

Published: 2026-09-08T12:00:00Z
Updated: 2026-09-09T07:41:56.167Z
Language: en
Evidence: editorial

An AGD inventory connects each account to its role, market, owner and observed state.

![Rows of server racks and cables at the NOIRLab headquarters.](https://theorganiclub.com/images/editorial/account-inventory.jpg)

NOIRLab/NSF/AURA/T. Slovinský. Wikimedia Commons photograph. Resized and JPEG-compressed from the source photograph. Original source SHA1: f2d53536efa6a11a83ddffb4ceed3ae171f2ca92.

## The takeaway

An AGD inventory connects each account to its role, market, owner and observed state. It separates available assets from desired ones.

## The argument

An account being created, an accessible account and a publishing-ready account are different states. Record last verification time instead of keeping permanent labels. Credentials belong in an appropriate manager, not an editorial sheet. The inventory describes the system without exposing its secrets.

Distinguish active, temporarily unavailable and out-of-scope accounts. Keep status-change history for retrospectives. Otherwise a disappeared account can drop out of calculations and make the network look stronger. The inventory is therefore also a measurement tool, provided each update does not rewrite the past. Current capacity answers today’s planning question; historical membership answers what happened to the original cohort and resources committed to it.

## Treat the inventory as a current state, not a head count.

Counting accounts is easy; knowing which ones are ready for a specific job is harder. Record the account’s purpose, current operating status, owner and the source from which that status was confirmed. Keep identifiers stable so a renamed profile does not become a new row with a lost history. Separate editorial readiness from technical readiness: an accessible account can still lack an approved brief.

Review the inventory before allocating work, especially after a long pause or a change in provider. Avoid embedding credentials in an ordinary planning sheet. Link to the approved access process and retain only the information needed for coordination. When a job fails, update the relevant state rather than leaving a warning buried in a chat thread. A useful inventory answers what can happen next and who can resolve uncertainty. The number of rows matters less than whether the next operator can trust the record.

### Three states worth separating

- **Identity:** The stable account record and its editorial purpose.

- **Readiness:** Whether a specific planned action can proceed now.

- **Responsibility:** The person and evidence needed to resolve an unknown.

Editorial model: a way to reason about the process, not measured platform results.

## Story: The idea in three screens.

### Your network starts with an accurate inventory.
An AGD inventory connects each account to its role, market, owner and observed state.

### Account inventory
An AGD inventory connects each account to its role, market, owner and observed state. It separates available assets from desired ones.

### What can mislead.
An outdated inventory can make an agent plan work against unavailable capacity.

## Story: From concept to practice.

### Define unambiguous states.
Adapt this to your audience, budget and test scope.

### Record an owner and verification date.
Adapt this to your audience, budget and test scope.

## TokPortal workflow: Start with the accounts you actually have

In TokPortal, a publishing plan begins with a real destination account. This read-only request narrows the inventory to TikTok accounts in the USA. It returns accounts in the connected workspace, not a catalogue of accounts for sale.

Endpoint: GET /api/ext/accounts

```json
{
  "tool": "tokportal_list_accounts",
  "arguments": {
    "platform": "tiktok",
    "country": "USA",
    "page": 1,
    "per_page": 3
  }
}
```

Before briefing three narrators, inspect the account IDs and state returned by this request. If an existing account is suitable, choose the existing-account route instead of ordering a new one.

- **Account ID:** A delivered saved_account_id differs from the stable bundle account listing ID. Use the identifier required by the next tool.

- **Scope:** Results belong to the connected workspace. An empty list is not proof that TikTok has no relevant audience.

- **Next decision:** Match each account to a distinct audience promise before assigning an asset.

## Put it to work

1. Define unambiguous states.

2. Record an owner and verification date.

Limit: An outdated inventory can make an agent plan work against unavailable capacity.

## Sources

- https://developers.tokportal.com/mcp/

This publication is initiated by TokPortal. AI-assisted editorial production and corrections policy: https://theorganiclub.com/en/about/
