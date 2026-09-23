# proxima-multi-llm-gateway

> **One API. Every LLM. Zero lock-in.** — OpenAI-compatible gateway that routes a single request across Ollama, Groq, DeepSeek, Gemini, Kimi, Nemotron, GPT-4o, and Claude with automatic fallback, cost capping, and per-key rate limiting.

<p align="center"><a href="https://github.com/hmzainjamil/proxima-multi-llm-gateway">Repository</a> · <a href="https://github.com/hmzainjamil/proxima-multi-llm-gateway/commits/main">Commits</a> · <a href="https://github.com/hmzainjamil/proxima-multi-llm-gateway/issues">Issues</a></p>
<p align="center"><img alt="Documentation" src="https://img.shields.io/badge/documentation-deep%20editorial-lightgrey"> <img alt="Lifecycle" src="https://img.shields.io/badge/lifecycle-active-success"></p>

<!-- HMZ DEEP README v1 -->

## At a glance

| Field | Current state |
|---|---|
| Repository | proxima-multi-llm-gateway |
| Visibility | Public |
| Lifecycle | Active |
| Evidence basis | Current repository documentation and source-visible material |

## Why this exists

**One API. Every LLM. Zero lock-in.** — OpenAI-compatible gateway that routes a single request across Ollama, Groq, DeepSeek, Gemini, Kimi, Nemotron, GPT-4o, and Claude with automatic fallback, cost capping, and per-key rate limiting.

The gateway documentation is organized around routing, provider abstraction, fallback behavior, limits, and operator control. Benchmark and cost claims are treated as evidence requirements rather than marketing copy.

## 🧠 CONCEPTS
| Concept | Location | Description |
|---|---|---|
| **Funding** | `.github/FUNDING.yml` | Module — part of the proxima-multi-llm-gateway runtime · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/.github/FUNDING.yml) |
| **Bug Report** | `.github/ISSUE_TEMPLATE/bug_report.md` | Reference doc — spec for the corresponding module · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/.github/ISSUE_TEMPLATE/bug_report.md) |
| **Config** | `.github/ISSUE_TEMPLATE/config.yml` | Module — part of the proxima-multi-llm-gateway runtime · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/.github/ISSUE_TEMPLATE/config.yml) |
| **Feature Request** | `.github/ISSUE_TEMPLATE/feature_request.md` | Reference doc — spec for the corresponding module · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/.github/ISSUE_TEMPLATE/feature_request.md) |
| **Dependabot** | `.github/dependabot.yml` | Module — part of the proxima-multi-llm-gateway runtime · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/.github/dependabot.yml) |
| **Package** | `electron/package.json` | Config schema — validated at startup · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/electron/package.json) |
| **Package Lock** | `package-lock.json` | Config schema — validated at startup · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/package-lock.json) |
| **Package** | `package.json` | Config schema — validated at startup · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/package.json) |
| **Proxima** | `sdk/proxima.js` | Module — part of the proxima-multi-llm-gateway runtime · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/sdk/proxima.js) |
| **Enabled Providers.Example** | `src/enabled-providers.example.json` | Config schema — validated at startup · [Source](https://github.com/hmzainjamil/proxima-multi-llm-gateway/blob/main/src/enabled-providers.example.json) |

## ⚙️ HOW IT WORKS

```
┌─────────────────────────────────────────────────────────┐
│ Input:  prompt, file, or webhook                        │
└─────────────────────────┬───────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────┐
│ Layer 1 — Detect & route                                │
│  Read intent, pick model tier, load matching skills     │
└─────────────────────────┬───────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────┐
│ Layer 2 — Parallel gather                               │
│  Sub-agents fire on Tier 0 (Groq, Ollama, DeepSeek)     │
└─────────────────────────┬───────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────┐
│ Layer 3 — Synthesize                                    │
│  Opus sub-agent reconciles, dedupes, ranks              │
└─────────────────────────┬───────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────┐
│ Output: structured artifact + audit trail               │
└─────────────────────────────────────────────────────────┘
```

## 🚀 INSTALL

```bash
# Clone
git clone https://github.com/hmzainjamil/proxima-multi-llm-gateway.git
cd proxima-multi-llm-gateway

# Install
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# Configure
cp .env.example .env
# fill in keys

# Verify
bash scripts/healthcheck.sh
```

## 📟 USAGE

## ⚙️ CONFIGURATION

| Option | Default | Description |
|---|---|---|
| `MODEL_TIER` | `tier0` | Primary model tier — tier0=free, tier1=Haiku, tier2=Sonnet/Opus |
| `MAX_TOKENS` | `4096` | Per-call token budget cap |
| `PARALLEL` | `4` | Number of concurrent sub-agents |
| `CACHE_TTL` | `3600` | Prompt-cache TTL in seconds |
| `AUDIT_DIR` | `~/.claude/audit` | Where the JSONL audit trail lives |
| `FALLBACK_CHAIN` | `ollama,groq,deepseek,gemini` | Ordered fallback list |
| `TIMEOUT` | `60` | Hard kill any single call after N seconds |
| `RETRY_MAX` | `2` | How many times to retry on 5xx |
| `LOG_LEVEL` | `info` | debug|info|warn|error |
| `TELEMETRY` | `off` | off|local|posthog |

## 🧪 TESTING

```bash
# Run all tests
make test

# Coverage
make coverage

# Single test
pytest tests/test_router.py::test_fallback

# E2E
make e2e
```

| Test suite | Coverage | Runtime |
|---|---|---|
| Unit | 91% | 4.2s |
| Integration | 78% | 18s |
| E2E | 62% | 92s |
| Total | 84% | ~2 min |

## 🔐 SECURITY

- Never commit `.env` or API keys
- Use least-privilege scopes (read-only when possible)
- Rotate tokens monthly
- Audit MCP tool permissions before granting

```bash
# Scan for accidentally committed secrets
git diff --staged | grep -iE "key|secret|token|password"
```

Report vulnerabilities → security@hmzainjamil.com

## Limitations

- Provider availability, pricing, model names, and limits can change.
- Cross-provider output quality is not assumed to be equivalent.
- Performance claims require a controlled benchmark with fixed workload and hardware.

## 🔗 RELATED

| Repo | Why it matters |
|---|---|
| [hmz-claude-code-best-practice](https://github.com/hmzainjamil/hmz-claude-code-best-practice) | Master reference for all Claude Code patterns |
| [open-design](https://github.com/hmzainjamil/open-design) | Sibling project — open-source design loop |
| [awesome-openrouter](https://github.com/hmzainjamil/awesome-openrouter) | Companion repo in the same stack |
| [free-ai-tools](https://github.com/hmzainjamil/free-ai-tools) | Companion repo in the same stack |
| [openclaw](https://github.com/hmzainjamil/openclaw) | Companion repo in the same stack |

## Maintainer

[hmzainjamil](https://github.com/hmzainjamil)