#  PayBox plugin

[PayBox](https://paybox.sh) is a non-custodial wallet for agents. This plugin connects your agent to
it: swap and transfer tokens across chains, pay x402 services, take positions on prediction markets,
and issue merchant-scoped virtual cards.

PayBox never holds your private key. Anything that spends or signs is confirmed by you — the agent
orchestrates, it does not authorize.

## Install

Add the plugin from your host's plugin marketplace, then sign in when prompted. The first sign-in
walks you through granting the connector access to specific credentials, each with its own approval
mode.

Currently packaged for **Grok**.

## What it adds

**MCP server** — `https://api.paybox.sh/mcp`, providing `list_credentials`, `get_portfolio`,
`request_swap`, `request_transfer`, `request_payment`, `request_wallet_sign`, `request_secret`,
`get_buy_link`, `discover_services`, `pay_x402`, `use_service`, `discover_plugins`, `use_plugin`,
`get_request`, and more.

**Skills**

| Skill | Use it for |
|---|---|
| `paybox-get-started` | The grant model, approval modes, what to do when access blocks you |
| `paybox-pay-and-swap` | Units, pre-spend checks, what a card authorization does not do |
| `paybox-x402-services` | Which x402 tool to reach for, cost-before-spending, failing listings |

## How access works

Access is **per-credential and revocable**, not per-account. Each granted credential carries an
approval mode: `autonomous` signs without asking, `iframe` needs an in-window confirm, and
`always_approve` needs your passkey every time. Revoke the connector any time from the app's
**Clients** screen.

A credential that exists but is not granted is invisible to the agent. That is the intended default.

## Signing

Every money operation completes in the PayBox signing window, which holds the key and signs there
and nowhere else.

Hosts differ in *when* they draw it, and PayBox tells each agent which applies to it.

**On Grok** the window appears only once the agent's reply is finished — nothing is on screen while
it is still typing, and that is expected. When the reply ends the window appears, you sign, and the
agent reports the outcome on its next turn.

## Security

- PayBox never holds your key, and no flow asks the agent for a seed phrase or passphrase.
- Spend limits and approval modes are enforced server-side, not by the agent.
- x402 calls spend real money per request. A well-behaved agent tells you the cost before paying.

## Links

- [paybox.sh](https://paybox.sh)
- [Docs](https://docs.paybox.sh)

## License

MIT — see [LICENSE](LICENSE).
