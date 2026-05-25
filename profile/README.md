# Langclaw

**Mantle-first AI alpha, data, and strategy intelligence.**

Langclaw is a wallet-authenticated AI agent workspace for Mantle. It analyzes smart-money flow, liquidity anomalies, protocol momentum, and DEX pair history, then turns the result into source-backed alpha briefs, watchlist signals, Dune-backed strategy backtests, paper-trading orders, and on-chain proof records.

The current hackathon build is intentionally analysis-first. It does not execute live-funds trades. Strategy Lab produces backtests and deterministic paper-trade proofs so signals can be evaluated without custody or execution risk.

## Repositories

Organization: [Langclaw-AI-Mantle](https://github.com/Langclaw-AI-Mantle)

| Repository | Stack | Port | README |
| --- | --- | --- | --- |
| [frontend](https://github.com/Langclaw-AI-Mantle/frontend) | Next.js, React, RainbowKit, AI SDK | 3000 | [README](https://github.com/Langclaw-AI-Mantle/frontend/blob/main/README.md) |
| [backend](https://github.com/Langclaw-AI-Mantle/backend) | Node HTTP API, TypeScript, Supabase, OpenAI, OpenClaw | 3001 | [README](https://github.com/Langclaw-AI-Mantle/backend/blob/main/README.md) |
| [contracts](https://github.com/Langclaw-AI-Mantle/contracts) | Foundry, Solidity proof contracts | N/A | [README](https://github.com/Langclaw-AI-Mantle/contracts/blob/main/README.md) |

This workspace can be run as a monorepo with `frontend/`, `backend/`, and `contracts/` as sibling folders, or as three separate clones from the organization above.

## What Langclaw Does

| Area | What users get |
| --- | --- |
| Research (Mantle intelligence) | Smart-money and holder-flow summaries, liquidity anomaly checks, TVL/yield momentum, evidence cards, confidence, risk notes, and source gaps |
| Alpha Watchlist | Supabase-backed saved signals for follow-up monitoring |
| Strategy Lab | Dune-backed Mantle Liquidity Momentum Strategy backtests, equity curve, trade table, win rate, drawdown, latest signal, and paper-trade opening |
| Proof Center | Registry decision history and strategy proof records linked to the Langclaw ERC-8004 agent identity |
| Usage billing | Internal MNT usage ledger with optional Mantle `LangclawUsageVault` deposit verification |

## For Judges And Reviewers

Fast path:

1. Open the deployed app, or run the local stack below.
2. Connect an EVM wallet on Mantle mainnet, chain ID `5000`.
3. Select **Research** mode in chat (legacy `onchain` is aliased to Research).
4. Run one of the demo prompts below.
5. Inspect the evidence, source gaps, agent decision proof, Alpha Watchlist, Strategy Lab, and Proof Center.

Demo prompts:

```text
Analyze holder flow and smart-money signals on Mantle token 0x5d3a1Ff2b6BAb83b63cd9AD0787074081a52ef34
```

```text
Detect liquidity anomaly on Mantle pair 0xeAfc4D6d4c3391Cd4Fc10c85D2f5f972d58C0dD5
```

```text
Rank Mantle protocols by TVL and yield momentum
```

Strategy Lab demo:

```text
Open /strategy, select the sample Mantle DEX pair, provide a Dune query ID if the backend env does not set one, run a backtest, then open a paper trade from the latest signal.
```

## Deployed Proof Layer

| Item | Value |
| --- | --- |
| Mantle chain ID | `5000` |
| `LangclawRegistry` | `0xe69755e4249c4978c39fbe847ca9674ce7af3505` |
| Registry deployment tx | `0xf6f8af14295c86d2f358c32ba15d0669903b122c086dcb0b432d9df8aaec6b6c` |
| Optional `LangclawUsageVault` | `0x7e93Ef361e7b54297cF963977bA829E47E59e8E1` |
| Usage vault deployment tx | `0xb60ed9019c5c8bb4c2b32c6a3e62e1edaf3b1530528d8151dfce08c1fd8b44e0` |
| `LangclawTradingJournal` | `0xe96e9b76af8c8f32bfa2235d647186826d92fb7d` |
| ERC-8004 identity registry | `0x8004A169FB4a3325136EB29fA0ceB6D2e539a432` |
| Langclaw ERC-8004 agent ID | `94` |
| Agent owner / recorder | `0x2cA915EF6be8D2D48ccD3c5dAF715546AF873A4c` |

Live decision proof examples:

| Decision | Signal | Transaction |
| --- | --- | --- |
| `0` | `smart-money` | `0x8a598de98fac01d53e696df67a9527de280c4d8cece72ccc4ced91164efa5187` |
| `1` | `smart-money` | `0x39caaca5fe3a6792c427740342116f309ac02ee0a846c7dbe54f12c86a39a177` |
| `2` | `liquidity-anomaly` | `0x9956a7574f6144ce831deac3275305939d65503366bc11bd922bc4783eeb5faf` |

Each `LangclawRegistry` decision stores the ERC-8004 `agentId`, Langclaw `runId`, deterministic `decisionHash`, evidence URI, signal type, recorder wallet, and block timestamp.

## Mantle Data Sources

| Source | Purpose |
| --- | --- |
| Etherscan-style API | Mantle chain reads with `chainid=5000` |
| DEX Screener | Mantle DEX pair liquidity, price, and market context |
| DeFiLlama | Mantle protocol TVL and yield context |
| Surf | Mantle-scoped smart-money and web research (API + optional CLI fallback) |
| Elfa | Mantle-scoped narrative and sentiment context |
| Nansen | Mantle smart-money netflow fallback |
| Dune | Historical rows for Strategy Lab and row-level SQL fallback |
| Alchemy | Optional chain and token enrichment |
| GoPlus | Optional token and security risk checks |
| Brave, Tavily, GitHub | Public discovery fallback for broader research context |

Provider failures are shown as source gaps instead of hidden. The UI separates usable evidence from missing or unconfigured data sources.

## Quick Start

Backend:

```bash
cd backend
cp .env.example .env
npm install
npm run dev
```

Frontend:

```bash
cd frontend
cp .env.example .env.local
pnpm install
pnpm dev
```

Contracts:

```bash
cd contracts
git submodule update --init
forge build
forge test
```

Smoke check:

```bash
curl http://localhost:3001/health
# {"ok":true,"service":"langclaw-backend"}
```

Open [http://localhost:3000](http://localhost:3000), connect a wallet, and sign the Langclaw login message.

## Environment

Core backend variables:

```bash
OPENAI_API_KEY=
OPENAI_CHAT_MODEL=gpt-5-mini
OPENAI_AGENT_MODEL=gpt-5.2
SUPABASE_URL=
SUPABASE_SERVICE_ROLE_KEY=
LANGCLAW_API_KEY_PEPPER=
CORS_ORIGIN=http://localhost:3000
```

Mantle proof and data variables:

```bash
MANTLE_CHAIN_RPC_URL=https://rpc.mantle.xyz
MANTLE_CHAIN_ID=5000
MANTLE_PRIVATE_KEY=
MANTLE_ERC8004_AGENT_ID=94
LANGCLAW_REGISTRY_ADDRESS=0xe69755e4249c4978c39fbe847ca9674ce7af3505
LANGCLAW_USAGE_VAULT_ADDRESS=0x7e93Ef361e7b54297cF963977bA829E47E59e8E1
MANTLE_LANGCLAW_TRADING_JOURNAL_ADDRESS=0xe96e9b76af8c8f32bfa2235d647186826d92fb7d
MANTLE_TRADING_JOURNAL_ENABLED=true
DUNE_API_KEY=
DUNE_DEFAULT_QUERY_ID=
DUNE_STRATEGY_QUERY_ID=
ALCHEMY_API_KEY=
ETHERSCAN_API_KEY=
GOPLUS_API_KEY=
GOPLUS_API_SECRET=
```

Frontend variable:

```bash
NEXT_PUBLIC_LANGCLAW_API_URL=http://localhost:3001
```

See the repo env templates for the full list:

- [backend/.env.example](https://github.com/Langclaw-AI-Mantle/backend/blob/main/.env.example)
- [frontend/.env.example](https://github.com/Langclaw-AI-Mantle/frontend/blob/main/.env.example)
- [contracts/.env.example](https://github.com/Langclaw-AI-Mantle/contracts/blob/main/.env.example)

## Architecture

```text
User -> Frontend (:3000) -> Backend API (:3001)
                              |-> Supabase: sessions, memory, API keys, usage ledger, watchlist
                              |-> Research workflow:
                              |     runtime probe -> planner -> discovery (TS)
                              |     -> source normalizer (TS) -> trend scorer -> evidence -> verifier
                              |     -> on-chain enrichment (TS) -> final conclusion
                              |     -> evidence bundle -> LangclawRegistry proof
                              |-> OpenClaw: planner, trend scorer, evidence, verifier, final conclusion
                              |-> OpenAI Responses: direct chat and synthesis fallback
                              |-> Mantle providers: Surf, Elfa, Nansen, Dune, DEX Screener, DeFiLlama, Alchemy, Etherscan, GoPlus
                              |-> LangclawRegistry / LangclawTradingJournal / LangclawUsageVault
```

## API Surface

Backend base URL defaults to `http://localhost:3001`.

| Area | Endpoints |
| --- | --- |
| Health | `GET /health` |
| Chat | `POST /api/chat/stream`, `POST /api/chat/sessions` |
| Research | `POST /api/discover`, `POST /api/discover/stream` |
| Strategy Lab | `POST /api/strategy/backtest`, `scan-pairs`, `paper-trade`, `runs` |
| Proof | `POST /api/proofs/readiness`, `POST /api/proofs/decisions` |
| Watchlist | `POST /api/watchlist` |
| Wallet auth | `POST /api/wallet/challenge`, `POST /api/wallet/session` |
| API keys | `POST /api/api-keys` |
| Memory | `POST /api/memory`, `POST /api/memory/settings` |
| Usage | `POST /api/usage/balance`, `quote`, `vault`, `deposit/verify`, `withdraw/request` |
| Automation | `POST /api/automation/*`, `POST /api/automation/webhooks/{slug}`, Telegram webhook |

Full shapes: [API_REFERENCE.md](https://github.com/Langclaw-AI-Mantle/backend/blob/main/docs/API_REFERENCE.md).

## Smart Contracts

| Contract | Purpose |
| --- | --- |
| `LangclawRegistry` | Records Mantle AI decision proofs and signal categories |
| `LangclawTradingJournal` | Records Strategy Lab backtests and paper-trading outcomes |
| `LangclawUsageVault` | Optional MNT billing vault for deposits and authorized withdrawals |

Deploy examples and contract details: [contracts README](https://github.com/Langclaw-AI-Mantle/contracts/blob/main/README.md).

## Verification

```bash
cd backend
npm run typecheck
npm test
```

```bash
cd frontend
pnpm typecheck
pnpm build
```

```bash
cd contracts
forge build
forge test
```

## Security Notes

- Keep provider keys, Supabase service role keys, API key pepper, and private keys on the backend only.
- API keys are stored as HMAC hashes using `LANGCLAW_API_KEY_PEPPER`.
- Use a dedicated recorder wallet for proof writes.
- Use a multisig owner for production contract ownership.
- Never commit `.env` files.

## Additional Docs

| Document | Description |
| --- | --- |
| [HACKATHON_SUBMISSION.md](https://github.com/Langclaw-AI-Mantle/backend/blob/main/docs/HACKATHON_SUBMISSION.md) | Submission summary and scoring coverage |
| [DEMO_SCRIPT.md](https://github.com/Langclaw-AI-Mantle/backend/blob/main/docs/DEMO_SCRIPT.md) | 3 to 4 minute demo script |
| [API_REFERENCE.md](https://github.com/Langclaw-AI-Mantle/backend/blob/main/docs/API_REFERENCE.md) | Backend API reference |
| [LANGCLAW_BLUEPRINT.md](https://github.com/Langclaw-AI-Mantle/backend/blob/main/LANGCLAW_BLUEPRINT.md) | Mantle hackathon product blueprint |
| [openclaw/README.md](https://github.com/Langclaw-AI-Mantle/backend/blob/main/openclaw/README.md) | OpenClaw workflow workspace |

## Links

- GitHub: https://github.com/Langclaw-AI-Mantle
- Mantle: https://www.mantle.xyz/
- Mantle docs: https://docs.mantle.xyz/

## License

TBD
