# Reviewer test plan

## Local discovery

Install the package following README.md, reload the client and verify that its
MCP server and all skills appear. Only the declared HTTPS endpoint should be
contacted. No local command, hook or installer should run.

## Public tools (no account required)

1. Ask: "Calculate a sample birth chart for 1 January 2000 at 12:00 UTC,
   latitude 51.4779, longitude 0. The time is exact. Show the raw placements,
   houses and aspects."
2. Expect validation and a Swiss Ephemeris calculation. Follow
   manifests/pagination to retrieve the requested data. Distinguish the
   service's numerical output from the assistant's interpretation.
3. Repeat with an unknown birth time. Preserve UNKNOWN and clearly explain
   unavailable time-sensitive results; never silently assign noon or claim exact
   houses.
4. No sign-in should be requested for public calculations. Use synthetic inputs
   only.

## Optional account tools

Use a dedicated synthetic account to list its sample saved profiles. Calculate a
new raw chart after connecting, then save it only when explicitly requested.
Retrieve the saved chart and verify ownership and pagination. Previously
anonymous calculations must be repeated after authentication before saving. Do
not request purchases, deletions or legacy website chart formats.

## OAuth and failure behavior

Account operations should trigger the host's normal OAuth connection, using
dynamic client registration and S256 PKCE. Test successful consent, denied
consent, reconnection and refresh without placing credentials in the
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
