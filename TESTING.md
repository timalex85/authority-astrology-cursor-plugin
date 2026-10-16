# Reviewer test plan

## Local discovery

Install the package following README.md, reload the client and verify that its
MCP server and all skills appear. Only the declared HTTPS endpoint should be
contacted. No local command, hook or installer should run.

## Public tools

1. Ask: "Calculate a sample birth chart for 1 January 2000 at 12:00 UTC,
   latitude 51.4779, longitude 0. The time is exact. Show the raw placements,
   houses and aspects."
2. Expect validation and a Swiss Ephemeris calculation. Follow
   manifests/pagination to retrieve the requested data. Distinguish the
   service's numerical output from the assistant's interpretation.
3. Repeat with an unknown birth time. Preserve UNKNOWN and clearly explain
   unavailable time-sensitive results; never silently assign noon or claim exact
   houses.
4. These service calls are public, but the full package may request OAuth during
   initial connection. Use synthetic inputs only.

## Optional account tools

Use a dedicated synthetic account to list its sample saved profiles. Calculate a
new raw chart after connecting, then save it only when explicitly requested.
Retrieve the saved chart and verify ownership and pagination. Previously
anonymous calculations must be repeated after authentication before saving. Do
not request purchases, deletions or legacy website chart formats.

## OAuth and failure behavior

The package uses a registered public OAuth client and S256 PKCE. Complete the
host connection prompt before testing private tools. Test successful consent,
denied consent, reconnection and refresh without placing credentials in the
conversation. An unconnected private tool must not disclose records. Report rate
limits and unavailable tools accurately.

Reviewer credentials, if separately authorized, must be supplied through the
marketplace's private review channel. They are deliberately absent from this
public repository.

## Completion record

Record client version, package commit, date, local discovery, public tool
results and optional authenticated results for each host. A completed protocol
smoke test is not an in-app test. Do not check the submission's testing
attestation until the target-host checks pass.

## Verify actual authorization

After consent, call the account-access tool and verify it succeeds. A host label
saying “Connected” or “authenticated” is not sufficient: Cursor can establish an
anonymous MCP transport without an account token. Version 1.0.1 adds explicit
public-client OAuth configuration to address this. Test URL-only anonymous
access separately when reviewing the public service endpoint.

## Recorded verification — 16 October 2026

Cursor desktop 3.24.18 for macOS, using Grok 4.6 Medium: 26 tools and one skill
discovered. Synthetic natal calculation and paged chart retrieval passed. After
browser OAuth consent, get_account_profile, list_people and list_saved_charts
returned the synthetic reviewer, two sample people (EXACT and APPROXIMATE) and
an empty chart library.

The initial URL-only configuration exposed a Cursor lazy-authentication failure.
Version 1.0.1 was verified with explicit public-client OAuth and actual private
tool calls, not just a connected indicator. No customer records, purchases,
outreach or publication were involved.

Standalone Grok Bot has not been tested: the test account is on Cursor Free with
Legacy Privacy Mode. Grok Bot requires eligible paid access and
cloud-storage-compatible privacy settings. Cursor results must not be
represented as standalone Grok Bot results.
