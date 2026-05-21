# Google vs OpenAI vs Anthropic — Full Portfolio Comparison (May 2026)

**TL;DR**
- As of May 21, 2026, there is no single "winner" across the AI stack: **Anthropic Claude Opus 4.7 / Sonnet 4.6** wins complex multi-file coding (64.3% SWE-bench Pro), MCP-native agentic workloads, and enterprise governance on AWS Bedrock; **OpenAI GPT-5.5** wins terminal/computer-use agents (82.7% Terminal-Bench 2.0, 78.7% OSWorld) and consumer distribution; **Google Gemini 3.1 Pro / 3.5 Flash** wins multimodal+video, raw reasoning (94.3% GPQA Diamond), price-per-intelligence at the frontier, and the deepest data-residency footprint.


## Key Findings

1. **Model layer has trifurcated by job.** Opus 4.7 (SWE-bench Pro 64.3%, hallucination 36% on Artificial Analysis AA-Omniscience) is the most reliable model for high-stakes coding and agentic reasoning; GPT-5.5 (Terminal-Bench 2.0 82.7%, MRCR v2 @1M 74.0%, but AA-Omniscience hallucination 86%) is the strongest agentic/terminal model with the highest hallucination at the frontier; Gemini 3.1 Pro Preview (GPQA Diamond 94.1–94.3%, ARC-AGI-2 77.1%) leads pure reasoning at half the per-token price of Opus.
2. **Pricing has bifurcated.** Sonnet 4.6 and Gemini 3.1 Pro sit at $3/$15 and $2/$12 per Mtok respectively; GPT-5.5 doubled to $5/$30 with the new generation; Opus 4.7 holds $5/$25 but its new tokenizer can inflate effective cost up to 35%. Gemini 3.5 Flash (May 19, 2026) at $1.50/$9 is the new price-performance leader for high-volume production.
3. **MCP is the standard.** Anthropic invented it, but Google's Antigravity, ADK 2.0, and Managed Agents API, and OpenAI's Responses API, Codex, and AgentKit all speak MCP natively as of Q1–Q2 2026. 
4. **Agentic coding is a three-product race.** Claude Code leads weekly-active developer share with 4.2 million weekly active developer users (Presenc AI, April 2026: "Claude Code has 4.2 million weekly active developer users, with deployments at over 1,400 enterprise engineering organisations") and $2.5B run-rate revenue, with Anthropic's February 2026 Series G announcement stating "The number of weekly active Claude Code users has also doubled since January 1." Per SemiAnalysis's May 2026 analysis, Claude Code authors 4% of all public GitHub commits. The JetBrains AI Pulse Survey of January 2026 (n=10,000+ professional developers, 8 languages) found Claude Code "has the highest product loyalty metrics on the market, with a CSAT (satisfaction) of 91% and an NPS (likelihood to recommend) of 54 (on a scale from -100 to +100)." OpenAI Codex (GPT-5.5) is the agentic-terminal leader. Google Antigravity 2.0 (launched May 19, 2026 at I/O) is the late but credible challenger with multi-agent orchestration and a free preview tier.
5. **Browser/computer-use has thinned.** Project Mariner shut down May 4, 2026; OpenAI Operator shut down August 31, 2025 (its CUA tech now powers Atlas and ChatGPT Agent); Anthropic's Claude for Chrome and Claude Cowork (post-Vercept acquisition, Feb 2026) lead OSWorld at 72.5% with Sonnet 4.6.
6. **On-device mobile AI is a Google monopoly.** Gemini Nano via AICore + AI Edge SDK + ML Kit GenAI APIs is the only frontier-vendor production on-device stack. OpenAI and Anthropic have no native on-device offerings — both rely on cloud APIs from mobile apps.
7. **Video generation is a Google-OpenAI duopoly with Google ahead.** Veo 3.1 (cinematic, 1080p+native audio, scene extension, ingredients-to-video) is the editorial pick over Sora 2 — which OpenAI has *deprecated* (Videos API and Sora 2 retire September 24, 2026). Gemini Omni (announced I/O 2026) collapses text/image/audio/video into one model. Anthropic has zero video, zero raster image generation.
8. **Enterprise governance roughly at parity, with deployment-channel nuance.** Anthropic, Google, and OpenAI all hold SOC 2 Type II, ISO 27001, ISO 42001, HIPAA BAAs, and offer ZDR; Anthropic also has BAAs via AWS Bedrock (cleanest path for your stack), Google offers data residency in 10 countries on Vertex/Gemini Enterprise Agent Platform, and OpenAI offers data residency for Enterprise in 10 regions plus a 10% regional uplift on GPT-5.5 API.
9. **Significant changes since  (validation list)**: Vertex AI → Gemini Enterprise Agent Platform; Gemini CLI → Antigravity CLI (June 18, 2026 sunset); Project Mariner → shut down; OpenAI Assistants API → Responses/Conversations API (Aug 26, 2026 sunset); Sora 2 API → sunset September 24, 2026; DALL·E 2/3 → sunset May 12, 2026; "Imagine with Claude" was a 5-day September 2025 preview (Anthropic blog), now generalized as Claude's interactive visualizations (March 2026) and "Live Artifacts" (April 2026); Claude Code SDK was renamed Claude Agent SDK in early 2026.

---

## Details

### 1) Foundation Models — Flagship Comparison

| Model | Vendor | Context | Pricing $/Mtok (in/out/cached) | Headline benchmarks | Hallucination profile | Speed | Best fit |
|---|---|---|---|---|---|---|---|
| **Gemini 3.1 Pro Preview** | Google | 1M (2M practical) | $2 / $12 / $0.20 (above 200K: $4 / $18) | GPQA Diamond 94.1%, ARC-AGI-2 77.1%, SWE-bench Verified 80.6%, MMMLU 92.6%, AA Intelligence Index 57 | Moderate (50% on AA-Omniscience) | ~120 tok/s, TTFT 26s | Long-context analysis, multimodal, lowest frontier $/intelligence |
| **Gemini 3.5 Flash** (May 19, 2026) | Google | 1M | $1.50 / $9.00 / $0.15 | Terminal-Bench 2.1 76.2%, MCP Atlas 83.6%, beats 3.1 Pro on coding | Similar to 3.1 Pro | ~4× faster than 3.1 Pro | New default Flash; high-volume production |
| **GPT-5.5** | OpenAI | 1M (922K in / 128K out) | $5 / $30 / $0.50 (>272K: 2× in, 1.5× out; +10% regional) | Terminal-Bench 2.0 82.7%, OSWorld 78.7%, SWE-Bench Pro 58.6%, MRCR-v2@1M 74.0%, ARC-AGI-2 85.0%, AIME 100%, FrontierMath Tier 4 35.4% | **High** (86% AA-Omniscience hallucination) | Same per-tok latency as 5.4, ~40% fewer output tokens | Agentic coding, terminal, computer use, knowledge worker apps |
| **GPT-5.5 Pro** | OpenAI | 1M | $30 / $180 | BrowseComp 90.1%, hardest math/research | Lower than 5.5 standard | Slow (xhigh effort) | Frontier research, hard math, deep browse |
| **Claude Opus 4.7** | Anthropic | 1M (200K standard) | $5 / $25 / $0.50 (US-only +1.1×) | SWE-Bench Verified 87.6%, SWE-Bench Pro 64.3% (cat-leading), τ²-bench Telecom 98%, GDPval 80.3%, CyberGym 73.1% | **Best of frontier** (36% hallucination) | Standard; 6× "Fast Mode" beta available | Complex multi-file coding, agentic reasoning, regulated work |
| **Claude Opus 4.5** | Anthropic | 200K | $5 / $25 | SWE-bench Verified 80.9%, ARC-AGI-2 37.6%, prompt-injection robustness 4.7% (industry-best) | Excellent | Standard | Safety-critical agents; superseded by 4.7 for new builds |
| **Claude Sonnet 4.6** | Anthropic | 1M | $3 / $15 / $0.30 | SWE-bench Verified 79.6%, OSWorld 61.4%, matches Opus 4.5 on long-horizon coding | Excellent | ~2× Opus speed | **Production default for most workloads** |
| **Claude Haiku 4.5** | Anthropic | 200K | $1 / $5 | Near-frontier on routing/classification | Excellent | Fastest in family | Routing, classification, high-volume extraction |
| **Claude Mythos Preview** (Glasswing-restricted) | Anthropic | 200K | n/a | GPQA Diamond 94.6%, HLE 64.7%, CyberGym 83.1% | TBD | TBD | Cyber/research; only 40 enterprise partners |

** Gemini 3.1 Pro GPQA Diamond is 94.1–94.3% (confirmed by Price Per Token, NxCode, Google blog). Opus 4.7 SWE-Bench Pro 64.3% and Verified 87.6% (confirmed by Anthropic + Build Fast with AI). GPT-5.5 Terminal-Bench 2.0 82.7% (confirmed by OpenAI announcement and Artificial Analysis). Claude Sonnet 4.5 OSWorld 61.4% (confirmed by Anthropic blog). If `research.txt` shows Opus 4.6 SWE-bench Verified at 80.8%, that's accurate; the 87.6% number is Opus 4.7 from April 16, 2026.

### 2) Android / On-Device / Mobile

| Tool | Vendor | What it is | Speed | Accuracy | Cost | Best fit | Notes |
|---|---|---|---|---|---|---|---|
| **Gemini Nano / Gemini Nano 4** | Google | On-device SLM via AICore | Hardware-accelerated NPU (Pixel/Samsung/MediaTek/Snapdragon); ms-class | Limited context (~2–12K tok), summarization/smart reply quality on par with cloud for narrow tasks | **$0 inference** | Privacy-sensitive on-device features, offline, zero per-call cost | Gemini Nano 4 in AICore Developer Preview (April 2026), built on Gemma 4, 140+ languages, multimodal |
| **AI Edge SDK + ML Kit GenAI APIs** | Google | Android SDK for on-device GenAI | NA | NA | Free | Drop-in summarization, rewrite, smart reply | Production-eligible on AICore-enabled devices |
| **LiteRT + MediaPipe** | Google | Cross-platform on-device runtime | High | Model-dependent | Free | Custom on-device ML (vision, audio, custom LLMs) | Cross-platform incl. iOS/Web |
| **OpenAI mobile** | OpenAI | iOS/Android client apps for ChatGPT + Codex desktop apps | Cloud-bound | Cloud model quality | $20–$200/mo subscription | Consumer apps; no on-device SDK | **No native on-device SDK**; iOS/Android SDKs are thin clients to cloud |
| **Anthropic mobile** | Anthropic | Claude iOS/Android apps | Cloud-bound | Cloud model quality | $20–$200/mo | Consumer Claude apps; no on-device SDK | **No on-device strategy**; Anthropic explicitly cloud-only |

**Winner — on-device mobile inference: Google, unchallenged.** OpenAI and Anthropic have no on-device offering. For Product Mate's mobile consumers, you have one realistic path for offline/privacy: Gemini Nano via AICore.

### 3) Cloud / Enterprise AI Toolkits

| Platform | Vendor | Status May 2026 | Pricing model | Best fit |
|---|---|---|---|---|
| **Gemini Enterprise Agent Platform** (ex-Vertex AI) | Google | GA; rebranded at Cloud Next '26 | Consumption: Agent Engine $0.0864/vCPU-hr, sessions $0.25/1K events, Vertex AI Search $1.50–$6/1K queries, model tokens separate | Multi-model (200+ models incl. Claude on first-class), data-residency-heavy enterprises |
| **Gemini API / AI Studio** | Google | GA | Per-token; free tier on Flash/Flash-Lite only since April 1, 2026 | Developer prototyping, Flash production |
| **BigQuery ML + Gemini in BigQuery** | Google | GA | Per-slot/per-query | Data-warehouse-grounded analytics agents |
| **Antigravity 2.0 (Managed Agents API)** | Google | GA (May 19, 2026) | Tiered with AI Pro ($19.99), Ultra ($99.99/$200) | Multi-agent orchestration on GCP |
| **OpenAI Platform (Responses API)** | OpenAI | GA; Assistants API sunset **Aug 26, 2026** | Per-token GPT-5.5 $5/$30; regional +10%; Batch -50%; Cached -90% | OpenAI-native, agent-first apps |
| **AgentKit / Agents SDK** | OpenAI | GA | Per-token | Agent orchestration with built-in tools (web search $10/1K, file search $2.50/1K + storage) |
| **Azure OpenAI / Microsoft Foundry Agents** | Microsoft+OpenAI | GA (Azure Assistants deprecate Aug 26, 2026 → Foundry Agents) | Azure consumption | Enterprises mandating Azure; data residency in Azure regions |
| **Secure MCP Tunnel** (OpenAI) | OpenAI | GA (2026) | Enterprise add-on | Connect Atlas/Codex/Responses API to private/on-prem MCP servers without exposing them |
| **Claude API (Anthropic first-party)** | Anthropic | GA | Per-token; 1.1× US-only inference; 1M context at standard pricing on Opus 4.7/4.6 & Sonnet 4.6 | Direct first-party access |
| **Claude on AWS Bedrock** | Anthropic/AWS | GA self-serve in 27 AWS regions on Bedrock console | Bedrock matches direct API rates; +10% cross-region | **Your platform's default** — AWS BAA, VPC, IAM, Guardrails, CloudTrail |
| **Claude on Vertex AI** | Anthropic/Google | GA | Vertex matches direct rates; regional/multi-region +10% | GCP-native enterprises |
| **Claude Managed Agents** | Anthropic | Public beta (April 8, 2026); requires `managed-agents-2026-04-01` header | Per-token; Dreaming/Outcomes/MCP Tunnels in research preview | Managed agent harness with sandbox, MCP, vault credentials, webhooks |

**Verdict for an MCP-native AWS-Bedrock platform:** Claude on Bedrock is the architecturally cleanest path (Bedrock pricing matches Anthropic direct; HIPAA-eligible under AWS BAA; VPC-scoped; Guardrails for Amazon Bedrock for PII/policy enforcement). Use Bedrock cross-region inference + intelligent routing across Haiku 4.5 / Sonnet 4.6 / Opus 4.7. Note: **Claude Managed Agents is *not* HIPAA-eligible and not ZDR-eligible** because sessions are stateful and server-side; if Product Mate needs managed agents in regulated contexts, run them in a self-hosted sandbox or wait for HIPAA coverage.

### 4) Agentic Coding Toolkits

| Tool | Vendor | Backbone model | IDE / surface | Pricing | Adoption | Strengths | Weaknesses |
|---|---|---|---|---|---|---|---|
| **Claude Code + Claude Agent SDK** (formerly Claude Code SDK) | Anthropic | Opus 4.7 / Sonnet 4.6 | Terminal-first; VS Code extension (native), Cursor/Windsurf/JetBrains plugins, GitHub Action | Pro $20, Max $100/$200; or API pay-per-token; Agent SDK credits separated June 15, 2026 ($20/$100/$200 monthly pool) | 4.2M weekly active developers (Presenc AI, April 2026), $2.5B run-rate (doubled since Jan 1, 2026 per Anthropic Series G); 4% of public GitHub commits per SemiAnalysis; 91% CSAT / NPS 54 in JetBrains AI Pulse Survey January 2026 (n=10,000+ professional devs) | Best SWE-bench Pro (64.3%), long-context 1M, checkpoints, parallel "Agent Teams", MCP native, SSO/SCIM/HIPAA on Bedrock | Anthropic-only model; per-token cost can balloon with subagent fan-out |
| **OpenAI Codex** | OpenAI | GPT-5.5 (GPT-5.3-Codex specialized) | Terminal CLI, desktop apps (macOS+Windows), ChatGPT integration, Linear | Bundled in ChatGPT Plus/Pro/Business/Enterprise; pay-as-you-go Codex-only seats (Apr 2, 2026); 400K context in Codex | Strong second; NVIDIA Blog (April 23, 2026, Justin Boitano, VP Enterprise Computing): "Over 10,000 NVIDIANs — across engineering, product, legal, marketing, finance, sales, HR, operations and developer programs — are already using GPT-5.5-powered Codex." | Best Terminal-Bench 2.0 (82.7%), best computer use (78.7% OSWorld), agentic terminal | OpenAI-locked; SWE-Bench Pro trails Opus 4.7 by ~6 pts; 86% hallucination on AA-Omniscience |
| **Google Antigravity 2.0 + Antigravity CLI** | Google | Gemini 3.5 Flash default; supports Claude Sonnet 4.5 + GPT-5 | Standalone IDE (VS Code fork), CLI (Go), public SDK | Free preview; AI Pro $19.99, AI Ultra $99.99/$200 | Newest; small but growing. **Gemini CLI sunset June 18, 2026** for non-enterprise tiers | Multi-agent orchestration, parallel subagents, Artifacts for verification, model optionality | Stability issues reported; Antigravity CLI not open source (Gemini CLI was Apache 2.0); enterprise SSO/compliance documentation lighter than Claude Code |
| **Cursor / Windsurf** (3rd party) | Anysphere / Cognition | Multi-model (Claude default for many) | IDE | Cursor Pro $20, Windsurf Pro $20, Business $40 | Largest IDE share | Multi-model | Not a vendor offering |

**Verdict — by sub-use case:**
- **Multi-file production codebase work, regulated industries** → Claude Code (Opus 4.7) on Bedrock.
- **Terminal-native agentic workflows / OS-level automation** → Codex (GPT-5.5).
- **Multi-agent parallel orchestration with Google data integration** → Antigravity 2.0.
- **Cost-sensitive bulk coding (RAG, classification, simple refactor)** → Sonnet 4.6 or Gemini 3.5 Flash via Cursor or Antigravity.

### 5) Multimodal / Creative / Design

| Tool | Vendor | Capability | Pricing | Best fit | Notes |
|---|---|---|---|---|---|
| **Veo 3.1 / 3.1 Fast / 3.1 Lite** | Google | Text-to-video, image-to-video, native synced audio, scene extension, ingredients-to-video, 1080p/4K | ~$0.75/sec API; Pro $19.99 (1,000 credits/mo); Ultra $99.99/$200 | Cinematic video; ad/creator workflows | Veo 3.1 Lite launched March 31, 2026 at <50% of Fast pricing |
| **Gemini Omni** (Flash today, API "coming weeks") | Google | Unified text/image/audio/video in/out | Bundled in Gemini app + YouTube Shorts (10s clips at launch) | Single-model multimodal generation | Announced May 19, 2026 at I/O 2026 |
| **Imagen 4 / Nano Banana 2 (Gemini 3.1 Flash Image)** | Google | Image generation; speed/cost leader | API per-image | Marketing assets, mockups | Nano Banana 2 = speed/cost leader; ChatGPT Images 2.0 = layout/typography leader |
| **Flow** | Google | Veo+Imagen video editor / production app | Pro $19.99 / Ultra $99.99 | Storyboarded video production | Mobile app planned 2026; Flow rebrand of earlier video tools |
| **Stitch (stitch.withgoogle.com)** | Google | **UI-to-code design**, conversational, voice canvas, Gemini 3-powered | **Free** | Frontend mockups, design-to-HTML/CSS, exports to Antigravity via MCP | **Confirmed active and upgraded at I/O 2026** with Stitch Agent + Voice Canvas; not deprecated |
| **ChatGPT Images 2.0 (gpt-image-2)** | OpenAI | Image gen with readable typography in dense layouts, 2K output, non-Latin scripts | API + ChatGPT Plus+ | Infographics, posters, diagrams | Released April 21, 2026; **DALL·E 2 + DALL·E 3 retired May 12, 2026** |
| **Sora 2 / Videos API** | OpenAI | Text-to-video | ChatGPT Pro included | Consumer video | **API + Sora 2 model aliases scheduled for sunset Sep 24, 2026** (announced Mar 24, 2026); web/mobile app closed April 26, 2026 |
| **Canvas** | OpenAI | Inline document/code editor in ChatGPT | Plus+ | Editing workflow alongside model |  |
| **Claude Artifacts + Live Artifacts** | Anthropic | Interactive code/UI preview (React, SVG, HTML, Mermaid, .docx/.pptx/.xlsx); Live Artifacts refresh data | All paid plans | UI prototyping inside the chat | No raster image gen, no video gen |
| **Claude interactive visualizations** | Anthropic | Generalized "Imagine with Claude" — produces no-code interactive software on the fly | Default for all tiers incl. free (March 2026) | Vibe-coding demos, teaching | Successor to the 5-day Sept 2025 "Imagine" preview |

**Verdict:**
- **Video generation** → Google Veo 3.1 (Sora 2 is being sunset).
- **Image generation** → ChatGPT Images 2.0 for typography-dense layouts; Nano Banana 2 for cost/speed; Imagen 4 for photoreal.
- **Design/UI mockups → code** → Google Stitch (free, Gemini 3-powered) + export to Antigravity.
- **In-chat UI prototypes** → Claude Artifacts is best-in-class.
- **Anthropic has zero native raster image or video output.** For Product Mate, design/video must be sourced from Google or OpenAI (or third parties like FLUX via MCP).

### 6) Research / Knowledge Toolkits

| Tool | Vendor | Strengths | Pricing | Best fit |
|---|---|---|---|---|
| **NotebookLM + Deep Research / Fast Research** | Google | Source-grounded RAG, Audio/Video Overviews, Mind Maps, Data Tables, Slide Decks; 80+ language Audio Overviews | Free (50 queries/day); Plus $19.99; Ultra $99.99 | Document-grounded synthesis; lawyers, academics, analysts |
| **Notebooks in Gemini** (April 2026) | Google | NotebookLM workspace synced into Gemini | Bundled with Gemini Pro/Ultra | Multi-source research with web breadth |
| **ChatGPT Projects + File Library + Deep Research** | OpenAI | 1M-token Projects context, Deep Research 50+ sources, Connected Apps (Drive/SharePoint/GitHub/etc.) | Plus 10 DR runs/mo; Pro 250 DR/mo | Web-breadth research, agentic search |
| **Claude Projects + Claude Research + Skills** | Anthropic | Source-grounded RAG inside Projects, MCP connectors to FactSet/S&P/PitchBook/Moody's/Morningstar for finance | Pro/Max/Team/Enterprise | Domain-specific research with governed data |
| **Outcomes / Dreaming** (Claude Managed Agents) | Anthropic | Agents self-grade vs rubric; Dreaming consolidates agent memory across sessions; Anthropic's official Managed Agents blog (claude.com/blog, May 6, 2026): "Harvey uses Managed Agents to coordinate complex legal work… Completion rates went up ~6x in their tests." Wisedocs cut document review time by 50% per the same post | Per-token + research-preview headers | Long-horizon research with verification |

**Verdict:** For document-grounded synthesis with citations (legal/medical/academic), **NotebookLM** still wins for accuracy and source fidelity. For agentic web research, **ChatGPT Deep Research** has the broadest coverage. For domain-specific governed data + finance, **Claude Projects + MCP** is the only choice with Excel/PowerPoint/Word add-ins and finance-provider MCP apps (Moody's, FactSet, S&P Capital IQ, PitchBook, Morningstar, LSEG, Chronograph).

### 7) Browser / Computer-Use Toolkits

| Tool | Vendor | Status May 2026 | OSWorld | Strengths | Weaknesses |
|---|---|---|---|---|---|
| **Gemini in Chrome + Chrome Auto Browse** | Google | GA for Premium subscribers; **Project Mariner shut down May 4, 2026** | 83.5% (Mariner) | Distribution via Chrome; integrated with Gmail/Calendar/Maps | Mariner's capabilities migrating into Gemini Agent |
| **OpenAI Atlas + ChatGPT Agent** | OpenAI | GA, macOS-only (Win/iOS/Android in dev); CUA tech inherited from Operator (Operator shut down Aug 31, 2025) | ~38.1% (CUA legacy) | Tight Chrome alternative; second-largest agentic browser share (~21%) | Lower OSWorld; macOS-only; superapp consolidation in progress |
| **Claude for Chrome (extension) + Claude Cowork** | Anthropic | Claude for Chrome GA to all paid users; Cowork = OS-level agent on macOS (post-Vercept acquisition Feb 2026) | **72.5%** (Sonnet 4.6) | OS-level control, highest OSWorld of any shipped product, MCP-native | Cowork is **NOT HIPAA-eligible** under BAA; latency from screenshot loops |

**Verdict:** For browser/computer automation today, **Claude Cowork + Claude for Chrome on Sonnet 4.6** is the strongest combination (72.5% OSWorld). But for regulated workloads, Cowork is excluded from Anthropic's BAA — route those through Bedrock-hosted Claude with your own DLP layer above the model.

### 8) General Agent Frameworks / SDKs

| Framework | Vendor | What it is | MCP-native | Best fit |
|---|---|---|---|---|
| **Antigravity 2.0 + ADK 2.0 + Managed Agents API + Agent CLI** | Google | Full stack: visual builder (Agent Studio), code-first Python/Go/Java/TS (ADK), managed runtime (Agent Engine), CLI | Yes | GCP-native multi-agent; A2A inter-agent protocol |
| **Agent Garden + Model Garden** | Google | 200+ models incl. Claude/Llama/Gemma/Mistral; pre-built agent templates | Yes | Multi-model platform on GCP |
| **OpenAI Agents SDK + Responses API + AgentKit** | OpenAI | Python/TS SDK with built-in web search, file search, computer use, Secure MCP Tunnel | Yes | OpenAI-native agents |
| **Claude Agent SDK** (was Claude Code SDK) | Anthropic | Python+TS SDK; programmable agent loop, MCP, permissions, subagents | Yes (invented MCP) | Vendor-portable agents with MCP |
| **Claude Managed Agents (Outcomes, Dreaming, Multi-Agent)** | Anthropic | Hosted agent runtime with sandboxes, vault credentials, Outcomes self-grading, Dreaming memory consolidation, multi-agent orchestration on shared FS (Netflix deployed) | Yes | Managed long-running agents |
| **Advisor tool** | Anthropic | Pair a fast executor with higher-intelligence advisor mid-generation | Yes | Cost-optimized agentic workloads (`advisor-tool-2026-03-01` beta) |

**Verdict:** **MCP has won as the cross-vendor protocol.** Your Product Mate MCP investment is correctly placed. For an AWS-Bedrock platform, the cleanest agent stack is **Claude Agent SDK + MCP servers + Bedrock Claude models + (optional) Claude Managed Agents** for hosted long-running cases that don't need HIPAA. Use **OpenAI Agents SDK** as a thin secondary lane for GPT-5.5 terminal/computer-use cases.

### 9) Chat / Consumer Surfaces

| Plan | Vendor | Price (May 2026) | Models | Notable features |
|---|---|---|---|---|
| ChatGPT Free | OpenAI | $0 | GPT-5.5 Instant (since May 5, 2026) | Ads in US since Feb 9, 2026; 10 msgs/5hr |
| ChatGPT Go | OpenAI | $8/mo global | GPT-5.2 Instant | Ads even on paid; 10× Free limits |
| ChatGPT Plus | OpenAI | $20/mo | GPT-5.5, Deep Research 10/mo, Sora (until sunset), Codex, Agent | Same price since Feb 2023 |
| ChatGPT Pro $100 | OpenAI | $100/mo | GPT-5.5 Pro, 5× Plus, 10× Codex (promo through May 31, 2026) | Launched Apr 9, 2026 |
| ChatGPT Pro $200 | OpenAI | $200/mo | GPT-5.5 Pro, 20× Plus, 1M context, 250 Deep Research/mo | For daily power users |
| ChatGPT Business | OpenAI | $20–$25/seat (cut Apr 2, 2026) | GPT-5.5, SOC 2, SAML SSO, default training-data exclusion, 60+ integrations | 2+ users |
| ChatGPT Enterprise | OpenAI | Custom | + ISO 27001/27017/27018/27701, CSA STAR, SCIM, RBAC, EKM, data residency in 10 regions, 24/7 SLA | 150+ seats typical |
| Gemini app (free) | Google | $0 | Gemini 3 Flash | Workspace consumer integrations |
| Google AI Plus | Google | $7.99/mo | Gemini 3.1 Pro limited, 128K context, 200 credits | Cheapest paid tier |
| Google AI Pro | Google | $19.99/mo | Gemini 3.1 Pro full 1M context, 1,000 credits, Flow, Gemini Omni, Code Assist | Sweet spot |
| Google AI Ultra | Google | $99.99/mo (cut from $249.99 at I/O 2026) | 20× limits, 20TB storage, Antigravity 2.0 Ultra | Power users |
| Google AI Ultra Max | Google | $200/mo (former $249.99 top tier) | Same 20× ceiling with extras | Top tier |
| Claude Free | Anthropic | $0 | Sonnet 4.6 default, file creation, connectors, skills | Significantly expanded in 2026 |
| Claude Pro | Anthropic | $20/mo ($17 annual) | Opus 4.7 access, Projects, Claude for Chrome, Cowork | Best-value paid AI plan |
| Claude Max 5× / 20× | Anthropic | $100/$200 | Higher Opus 4.7 quota, fast mode | Heavy users |
| Claude Team | Anthropic | $25/seat (5+ seats) | Workspace, SSO | Teams |
| Claude Enterprise | Anthropic | Custom or self-serve (new 2026) | SAML/OIDC SSO, SCIM, audit logs, ZDR, HIPAA BAA, BYOK (H1 2026), private network via Bedrock/Vertex | Regulated industries |

**Notable consumer-side updates since `research.txt`:** Google AI Ultra base price cut from $249.99 to $99.99 at I/O 2026; OpenAI introduced the $100 Pro tier (Apr 9, 2026); ads on Free/Go in US (Feb 9, 2026); ChatGPT Plus rate-limit reductions on GPT-5.5 Thinking (initially 200/week, raised to ~3,000/week after backlash); Anthropic launched self-serve Enterprise.

### 10) Governance / Safety / Enterprise Readiness

| Control | Google | OpenAI | Anthropic |
|---|---|---|---|
| **SOC 2 Type II** | Yes (Vertex / Gemini Enterprise Agent Platform) | Yes (Business + Enterprise) | Yes (Trust Portal) |
| **ISO 27001 / 27017 / 27018 / 27701** | Yes | Enterprise tier | 27001:2022 + 42001:2023 (AI Management) |
| **HIPAA BAA** | Yes via Vertex / GCP | Yes via Enterprise | **Yes — directly + via AWS Bedrock BAA** (cleanest path) |
| **HIPAA-excluded products** | Preview models, some grounding services | Free, Plus, Pro, Go (consumer tiers) | **Claude Cowork excluded**; Managed Agents excluded |
| **Zero Data Retention** | Default behavior; configurable | Enterprise | Available (executed addendum); via Bedrock too |
| **Data residency** | 10 countries (Vertex / GAP); EU regions for Gemini under europe-west4 etc. | 10 regions (US, EU, UK, JP, CA, KR, SG, IN, AU, UAE) — Enterprise; +10% uplift on GPT-5.5 regional | US-only inference via `inference_geo` (1.1× multiplier); Bedrock per-region; Vertex per-region |
| **SAML/OIDC SSO + SCIM** | Yes | Enterprise | Enterprise |
| **Audit logs / RBAC** | Cloud Audit Logs, Security Command Center | Enterprise | Enterprise; emerging granular RBAC in 2026 |
| **Customer-Managed Encryption Keys (CMEK / BYOK)** | Yes (CMEK on Vertex) | Enterprise Key Management | **BYOK announced for H1 2026** |
| **VPC / Private Network** | VPC Service Controls, PSC | Secure MCP Tunnel, regional endpoints | Bedrock VPC, Vertex PSC, ZDR endpoints |
| **Prompt-injection robustness (best public number)** | Gemini 3 Pro: ~12.5% attack success (per Anthropic Gray Swan test) | GPT-5.1: ~21.9% | **Opus 4.5: 4.7% — industry best** |
| **Fine-tuning** | Yes (Vertex tuning, Gemini supervised tuning) | Phasing out self-serve fine-tuning (May 7, 2026 announcement); inference on FT models continues until base deprecation | Available for select enterprise partners only |
| **Content guardrails** | Model Armor (prompt injection, sensitive data, tool poisoning) | OpenAI Moderation, Trusted Access for Cyber, GPT-5.5-Cyber preview | Constitutional AI; NNSA-built safety classifiers (nuclear/bio/chem); ASL-3 deployment for Opus |

**Verdict:** The strongest enterprise readiness package today is **Anthropic on Bedrock under your existing AWS BAA**, plus a thin Vertex AI sidecar for Gemini 3.1 Pro / Veo 3.1 / NotebookLM workloads that need data residency in non-US regions and/or 1M-context multimodal. OpenAI is the third-source provider for terminal/computer-use only.

---

## Summary Positioning Matrix — Dominant Layer per Vendor

| Layer | Dominant vendor | Runner-up |
|---|---|---|
| Pure reasoning at frontier price | **Google** (Gemini 3.1 Pro) | Anthropic |
| Complex multi-file coding accuracy | **Anthropic** (Opus 4.7) | OpenAI |
| Terminal / computer-use agents | **OpenAI** (GPT-5.5 + Codex) | Anthropic (Cowork) |
| Browser automation today | **Anthropic** (Cowork, 72.5% OSWorld) | OpenAI (Atlas) |
| On-device mobile inference | **Google** (Gemini Nano + AI Edge) | — (none) |
| Video generation | **Google** (Veo 3.1 / Omni) | OpenAI (Sora 2 sunsetting) |
| Design → code | **Google** (Stitch + Antigravity 2.0) | Anthropic (Artifacts) |
| Knowledge research (grounded) | **Google** (NotebookLM) | Anthropic (Projects+MCP) |
| Knowledge research (web breadth) | **OpenAI** (Deep Research) | Google |
| Enterprise governance & compliance breadth | **Google + Anthropic** tied (data residency + Bedrock BAA) | OpenAI |
| Multi-tenant SaaS economics | **Anthropic on Bedrock** (Haiku/Sonnet routing) + **Google Gemini 3.5 Flash** | OpenAI (most expensive per Mtok at frontier) |
| Long-context (1M+) | **Google** (2M practical) | Anthropic (1M GA) and OpenAI (1M API) |
| MCP-native ecosystem maturity | **Anthropic** (inventor, deepest tooling) | Google (Antigravity), OpenAI (Secure MCP Tunnel) |
| Hallucination reliability | **Anthropic** (36% AA-Omniscience) | Google (50%); OpenAI distant (86%) |

---



### Stage 1 — Now (Q2 2026)
1. **Keep Claude on Bedrock as the production default.** Sonnet 4.6 for the 80% of workloads; Haiku 4.5 for routing/classification; Opus 4.7 selectively (gate behind cost guardrails because the new tokenizer can increase effective cost by up to 35%). Enable Bedrock Guardrails for PII and policy enforcement; route all production via VPC endpoints under your AWS BAA.
2. **Migrate any OpenAI Assistants API code by Aug 26, 2026.** If you have *any* Assistants-API usage in agents stack, plan migration to OpenAI Responses + Conversations API now. Use the OpenAI Agents SDK for the migration to gain Secure MCP Tunnel + built-in tools.
3. **Adopt the Claude Agent SDK + MCP pattern for new agentic features.** Standardize tool definitions as MCP servers; this gives you vendor portability — the same MCP servers can be consumed by Claude Agent SDK, OpenAI Agents SDK (via Secure MCP Tunnel), and Google ADK 2.0.
4. **Stand up a second source via Vertex AI** for two specific workloads: (a) document/repo workloads that need 1M+ context with grounding; (b) any video or design-to-code feature (Veo 3.1 + Stitch + Imagen 4). Use this as price/risk leverage in your Anthropic and AWS conversations.
5. **Implement a model router** for cost optimization. CloudZero's inference-cost research reports "Intelligent routing alone can reduce inference cost by 30 to 60% in mixed-workload environments." Build this in the gateway layer where Product Mate already terminates MCP.
6. **Lock down Claude Cowork** if anyone in your org is using it. It's excluded from Anthropic's HIPAA BAA. Either disable for regulated teams or front it with a DLP layer (Strac-style MCP DLP server).

### Stage 2 — Next 90 days
7. **Pilot Claude Managed Agents (Outcomes + Dreaming + Multi-Agent)** for one long-horizon research workload. Per Anthropic's official Managed Agents blog (May 6, 2026), Harvey saw ~6× task-completion lift and Wisedocs cut document review time by 50%. Run it in a self-hosted sandbox to maintain HIPAA eligibility because the managed-cloud version is not BAA-eligible.
8. **Pilot GPT-5.5 via OpenAI Responses API on a narrow terminal/computer-use surface.** Don't make it primary — use it as a third-source escape valve, gated to non-PHI workflows because of GPT-5.5's 86% AA-Omniscience hallucination rate.
9. **Eval Antigravity 2.0 + ADK 2.0 in a sandbox project** for greenfield multi-agent prototypes. Free preview, A2A protocol could be relevant if you build cross-vendor agent meshes.
10. **Migrate any Gemini CLI usage to Antigravity CLI before June 18, 2026.** Enterprise Gemini Code Assist Standard/Enterprise license holders keep Gemini CLI indefinitely; non-enterprise tiers do not.

### Stage 3 — H2 2026 watch list
11. **Watch for Claude 5 / Mythos GA.** Prediction markets price Q2–Q3 2026. Anthropic's Project Glasswing partner-only Mythos Preview (94.6% GPQA, 64.7% HLE, 83.1% CyberGym) suggests a meaningful frontier step.
12. **Watch Anthropic BYOK GA (H1 2026)** — material for your KMS/encryption posture if you require customer-managed keys.
13. **Watch Gemini 3.5 Pro and Gemini Spark** — Google announced "coming soon" at I/O 2026 but did not ship; could reshape price-performance leadership again.
14. **Watch OpenAI superapp consolidation.** Atlas + ChatGPT + Codex are merging into a single desktop superapp per March 2026 reporting; this could clarify or further fragment OpenAI's enterprise story.

### Thresholds that would change these recommendations
- If **GPT-5.5 hallucination drops below 50% on AA-Omniscience** in a future release → reconsider OpenAI as a co-primary for knowledge work.
- If **Anthropic ships HIPAA BAA coverage for Claude Cowork or Managed Agents** → expand managed-agent footprint for regulated workloads.
- If **Google's Gemini 3.5 Pro launches at <$1.50 input pricing** with frontier benchmarks → strongly evaluate as a co-primary on Bedrock-equivalent VPC pattern via Vertex.
- If **Opus 4.7 effective cost inflation exceeds 25%** on your Product Mate workloads (measure on real traffic replay) → tighten Opus gating and push more traffic to Sonnet 4.6.

---

## Caveats

- **Preview vs GA.** Gemini 3.1 Pro is still labeled "Preview" as of May 2026, despite five-month-old benchmarks; Google says GA "soon." Several Claude Managed Agents features (Dreaming, MCP Tunnels, Fast Mode) are in research preview and not BAA-eligible. Don't anchor production SLAs on preview models.
- **Hallucination rate methodology.** Artificial Analysis's AA-Omniscience benchmark deliberately rewards models that decline to answer when uncertain. GPT-5.5's 86% hallucination rate vs Opus 4.7's 36% reflects answer-or-decline behavior, not raw factual accuracy. Real-world impact depends on whether your application has citation/grounding guardrails. Test on your own data.
- **Benchmark contamination.** OpenAI and others have flagged memorization concerns on some agentic benchmarks (e.g., GPT-5.5's MCP Atlas score is from "after the latest 2026 April update"); the Tom's Guide hands-on comparison reportedly favored Opus 4.7 across all 7 categories despite GPT-5.5's leaderboard wins. Treat single benchmarks as directional, not decisive.
- **Pricing volatility.** OpenAI doubled GPT-5.5 API pricing vs GPT-5.4 (+20% effective after token-efficiency claims). Google removed Pro-tier free API access April 1, 2026 and shifted to a Flash-only free tier. Anthropic kept Opus 4.7 pricing flat but introduced a tokenizer that can inflate effective cost up to 35%. Re-validate budget assumptions quarterly.
- **Subagent token sprawl.** Claude Code Pro/Max users have reported 3–50× faster rate-limit consumption after specific version regressions (Claude Code v2.1.89 in March 2026 was one such case). Build cost telemetry into your agent layer; don't rely solely on vendor dashboards.
- **`research.txt` items that should be revalidated** (in addition to the deprecations called out above): Project Mariner / WebVoyager 83.5% is now a *historical* number — Mariner was shut down May 4, 2026. Any "OpenAI Operator" reference should be replaced with "Atlas + ChatGPT Agent". DALL·E references should be replaced with ChatGPT Images 2.0 (gpt-image-2 / gpt-image-1 / gpt-image-1-mini). Any "Vertex AI" branding should be updated to "Gemini Enterprise Agent Platform" (the SKUs and APIs are unchanged). The "Claude Code SDK" reference should be updated to "Claude Agent SDK". Sora 2 references should note the September 24, 2026 API sunset.
- **Cowork / Excel add-ins.** Claude in Excel/Word/PowerPoint via Microsoft 365 add-ins shipped in 2026 with MCP support for FactSet, S&P, LSEG, Moody's, PitchBook — relevant if Product Mate has financial-services tenants. None of these are HIPAA-eligible.
- **Vercept-acquired computer-use technology** powers Claude Cowork's OSWorld jump from 42.2% → 72.5%. This capability is fast-moving; expect another step from Anthropic or Google in H2 2026.
