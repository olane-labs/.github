<h1 align="center">Copass</h1>

<p align="center"><strong>Hosted infrastructure for production AI agents.</strong></p>

<p align="center">
  <a href="https://docs.copass.com">Docs</a> ·
  <a href="https://docs.copass.com/quickstart">Quickstart</a> ·
  <a href="https://docs.copass.com/api-reference">API Reference</a> ·
  <a href="https://github.com/olane-labs/copass">copass</a>
</p>

---

One platform, three Routers:

- **Agent Router** — one API for any agent runtime (Anthropic, Google, Hermes).
- **Context Router** — the data, integrations, memory, and end users your agent reads from.
- **Compute Router** — managed compute for self-hosted runtimes.

## Run an agent against your sandbox

```ts
// TypeScript
import { AgentRouter } from '@copass/agent-router';

const router = new AgentRouter({
  auth: { type: 'api-key', key: process.env.COPASS_API_KEY! },
  sandboxId: process.env.COPASS_SANDBOX_ID!,
});

for await (const event of router.run({
  provider: 'anthropic',
  model: 'claude-opus-4-7',
  message: 'Why is checkout breaking on Safari?',
  endUserId: 'u-123',
})) {
  if (event.type === 'text') process.stdout.write(event.text);
}
```

```python
# Python
import os
from copass_agent_router import AgentRouter

router = AgentRouter(
    auth={"type": "api-key", "key": os.environ["COPASS_API_KEY"]},
    sandbox_id=os.environ["COPASS_SANDBOX_ID"],
)

async for event in router.run(
    provider="anthropic",
    model="claude-opus-4-7",
    message="Why is checkout breaking on Safari?",
    end_user_id="u-123",
):
    if event.type == "text":
        print(event.text, end="", flush=True)
```

The same call works on `provider: 'google'` and `provider: 'hermes'`. Memory, tools, integrations, and end-user permissions stay scoped to the sandbox.

A complete setup runs in 60 seconds — see the [Quickstart](https://docs.copass.com/quickstart).

## Build with Copass

- [**Agent Router**](https://docs.copass.com/developer-tools/agent-router) — Run agents that call models, integrations, and tools.
- [**Context Router**](https://docs.copass.com/context-router/overview) — Register data sources, ingest content, query the knowledge graph.
- [**Compute Router**](https://docs.copass.com/compute-router/overview) — Managed compute for self-hosted agent runtimes.
- [**Collaboration**](https://docs.copass.com/collaboration/overview) — Share sandboxes and agents with teammates.
- [**Account**](https://docs.copass.com/account/api-keys) — API keys, billing, and your Copass ID.

## Integrate from your stack

- [**TypeScript**](https://docs.copass.com/sdk) — `@copass/agent-router`, `@copass/core`
- [**Python**](https://docs.copass.com/sdk) — `copass-agent-router`, `copass-core`
- [**CLI**](https://docs.copass.com/cli) — `copass` (Node 20+)
- [**HTTP**](https://docs.copass.com/api-reference) — REST API with full OpenAPI catalog
- [**MCP**](https://docs.copass.com/developer-tools/mcp) — `@copass/mcp` for Claude Code, Cursor, and any MCP client

## Concepts

- [**Sandboxes**](https://docs.copass.com/concepts/secure-storage) — Tenancy and isolation.
- [**Retrieval**](https://docs.copass.com/concepts/retrieval) — `discover` / `interpret` / `search`.
- [**Multi-tenancy**](https://docs.copass.com/concepts/multi-tenancy) — Per-end-user isolation via `endUserId`.
- [**ANS**](https://docs.copass.com/ans/overview) — Addressing layer.

## Repositories

- [**copass**](https://github.com/olane-labs/copass) — SDKs, adapters, MCP server, CLI.

## License

MIT.
