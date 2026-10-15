# Authority Astrology for Cursor and Grok Bot

Explore birth charts, transits and relationship charts with Swiss Ephemeris
calculations. Preserve birth-time certainty and use your saved profiles with
permission.

![Authority Astrology](assets/icon.svg)

Calculate complete raw birth charts, aspects, houses, transits and returns with
Swiss Ephemeris. Preserve birth-time uncertainty and use your own saved profiles
with permission.

Calculate from supplied birth or event details without sign-in. The server
returns complete raw Swiss Ephemeris data; your assistant provides any
explanation. Known, approximate and unknown birth times remain distinct. Large
results include a manifest and can be retrieved in pages. There is no
server-generated interpretation, score, report purchase or marketing action.

Connect an Authority Astrology account only when you ask to read saved people or
save and retrieve new raw charts. Existing account permissions apply. Older
saved website-chart formats are outside this integration. Anonymous calculations
must be repeated after connecting before they can be saved.

## Examples

- "Calculate my natal chart for 1 January 2000 at noon in Greenwich, London.
  Confirm the place first."
- "I know my birth date and city but not my birth time. Explain what can and
  cannot be calculated."
- "Compare two supplied natal charts and show all returned cross-chart aspects,
  with their source layers."
- "Use my saved birth profile and calculate my next solar return." Sign in when
  prompted and select the intended person.

## Install and connect

This repository is a standalone Cursor plugin package. Marketplace availability
depends on review; the existence of this repository does not mean it is
approved.

For local testing in Cursor, copy this repository's contents (including
`.cursor-plugin`) into `~/.cursor/plugins/local/authority-astrology`, then
restart Cursor or run **Developer: Reload Window**. Open **Customize** and
verify that the skills and MCP server appear. Local imports must be allowed by
your organization. See
[Cursor's plugin installation documentation](https://cursor.com/docs/plugins).

Grok Bot uses the same plugin ecosystem. Once available, install through its
plugin interface; follow
[Grok Bot's setup guide](https://cursor.com/docs/grok-bot/get-started) for
account and client requirements. Do not install the same MCP server twice
through both a plugin and a manual configuration.

For a client that supports a custom remote MCP server, use:

```json
{
  "mcpServers": {
    "authority-astrology": {
      "url": "https://authorityastrology.com/mcp/claude"
    }
  }
}
```

The `/claude` suffix is the existing OAuth-compatible transport endpoint, not a
restriction on the client. It supports public tools without sign-in and an HTTP
401 OAuth challenge for account tools. The original OpenAI/Muse endpoints and
packages remain separate.

When an account tool is requested, use the host's OAuth flow and sign in on
Authority Astrology. The server supports dynamic client registration, S256 PKCE
and refresh-token rotation. No API key, password, fixed client secret or
authorization header is included in this package. Disconnect using the host's
connector controls; reconnect if authorization expires or is revoked.

## Reviewer test plan

See [TESTING.md](TESTING.md) for public smoke tests, optional account workflows,
expected results and safety boundaries. Test both local component discovery and
real tool calls in each target host before attesting that the plugin works
in-app. Protocol tests alone do not establish host compatibility.

## Data and privacy

The skills invoke only the declared Authority Astrology MCP server. The package
runs no local scripts, hooks, installers or background processes. The hosted
service receives tool arguments and, after OAuth consent, the account
permissions needed for the requested action. It does not require the full
conversation. Birthplace searches use LocationIQ. Birth details and calculated
charts are personal data; saved charts follow the service retention and deletion
policy. See the
[privacy policy](https://authorityastrology.com/privacy-policy#connected-assistants),
[terms](https://authorityastrology.com/terms) and
[developer documentation](https://authorityastrology.com/developers) for
details.

## Pricing and scope

This MIT-licensed plugin is distributed free of charge. Public
searches/calculations require no account. Private workflows require an
appropriate account and remain subject to its permissions and service limits.
The plugin cannot purchase subscriptions, reports, contact unlocks or credits.
The host application may require its own subscription. Website services and
their terms are separate from this package.

## Support

Use [Authority Astrology support](https://authorityastrology.com/support). If a
tool reports a rate limit, wait for its retry interval; do not invent missing
results. Report reproducible plugin issues in this repository without including
credentials, private records or real birth details.

## License

The plugin files are MIT licensed. No hosted application code, database
contents, Swiss Ephemeris binaries or calculation datasets are distributed here.
Hosted services and their data remain subject to their own terms.
