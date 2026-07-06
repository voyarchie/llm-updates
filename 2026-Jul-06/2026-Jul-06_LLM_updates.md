# LLM Updates — 2026-Jul-06

Monday brief, written Mon Jul 6 (Los Angeles time). The **Fable 5 / Mythos 5**
export saga that dominated three weeks of these briefs has reached a stable
state — Fable 5 back globally Jul 1 behind a hardened classifier, Mythos 5
scoped to ~100 US defenders, the measured coding cost already documented
(Jul-01 §1, Jul-03 §1). With that thread settled, the frontier's attention has
moved to a different pressure: **the calendar**. Two model launches and three
regulatory deadlines now fall inside the same fortnight, Jul 10–Aug 2.

Three things are new or sharpened since Friday:

1. **The mid-July release cliff has firm dates.** Friday's brief said Gemini
   3.5 Pro was "cleared for July." It now has a day — **July 17** — with a named
   reason for the slip (extended pre-training for **math, coding, and token
   efficiency**). **DeepSeek V4-Pro / V4-Flash** are lined up for a **full public
   launch mid-July**, out of the preview they've run since April.
2. **The quiet architecture story got louder.** The models shipping this month
   aren't scaled-up 2024 transformers — they're **hybrid state-space stacks**
   (Nemotron 3 / Mamba-3) and **fine-grained sparse-attention** designs
   (DeepSeek V4). This brief spends a section on the *techniques*, which prior
   briefs — consumed by the export story — never covered in depth.
3. **Regulation stops being a debate and becomes a deadline.** China's
   **anthropomorphic-AI rules** take effect **Jul 15** (ByteDance's Doubao and
   Alibaba's Qwen are already disabling humanlike and user-created agents), and
   the **EU AI Act's** transparency and high-risk obligations become
   **enforceable Aug 2**, with fines up to €35M or 7% of global turnover.

This report does **not** re-derive the settled export thread. The Jun-12 BIS
order, the suspension arc (Jun-15 → Jul-1), the Amazon jailbreak trigger
(Jun-19 §1), the shared-weights + classifier-gate architecture that reroutes
flagged queries to Opus 4.8 (Jun-11 §2, Jun-13), Project Glasswing (Jun-24 §1),
the Jul-1 restoration and its measured coding cost (Jul-01 §1, Jul-03 §1),
**Claude Sonnet 5** and its tokenizer caveat (Jul-01 §2), the Google Gemini
brain drain (Jul-03 §2), and the open-weights ordering (GLM-5.2 > MiniMax-M3 ≈
DeepSeek V4-Pro; Jul-01 §3) are all covered earlier. Here we advance only
what's new since Friday.

![Timeline from July 6 to August 2, 2026 showing model launches (blue) and regulatory deadlines (amber) clustering in the same fortnight: Jul 10 Qwen disables humanlike and user agents; Jul 15 China's anthropomorphic-AI rules take effect and Doubao turns agents off; mid-July DeepSeek V4-Pro/Flash full public launch; Jul 17 Gemini 3.5 Pro general availability with 2M context and Deep Think; Aug 2 EU AI Act enforcement begins.](mid_july_cliff.svg)

---

## 1. The mid-July release cliff — Gemini 3.5 Pro dated, DeepSeek V4 GA nears

Friday's brief left the frontier release calendar as a shape ("cleared for a
July GA"). It now has coordinates.

**Gemini 3.5 Pro — July 17.** Google DeepMind has set the general-availability
date after pulling the model out of Vertex AI enterprise preview. The slip from
early July is attributed to **extended pre-training** to fix three things flagged
in enterprise testing: **token efficiency, coding performance, and long-task,
multi-step reasoning** — with math a specifically named target. Reported specs
are unchanged from the June preview: a **2-million-token context window** and a
**Deep Think** reasoning mode. The delay is notable in itself: a frontier lab
choosing three extra weeks of pre-training over hitting an announced window is a
signal that the "just ship it" phase of the race has cooled, at least at Google.

**DeepSeek V4-Pro / V4-Flash — full public launch mid-July.** The V4 family has
run in limited preview since **April 24**; a full public launch (open weights +
API) is now expected mid-July. Specs recap: **V4-Pro** is a 1.6T-parameter MoE
with **49B active**; **V4-Flash** is 284B total / 13B active; both carry a
**1M-token context**. The headline is efficiency, not raw score — see §2.

**Why "cliff," not "calendar."** These two launches land the same week as three
regulatory deadlines (§3). For anyone shipping on top of these models, the
practical takeaway is that **the week of Jul 13–17 changes the menu twice** —
new frontier options arrive just as new compliance constraints bind. Plan
migrations and jurisdiction checks around that window, not after it.

## 2. Architecture spotlight — the transformer is being hollowed out

The models shipping this month share a structural theme the export drama
crowded out of earlier briefs: **the dense transformer block is being replaced
piece by piece**. This matters because it decouples capability growth from the
quadratic cost that has governed context length since 2017.

![Comparison diagram: a classic dense transformer block (dense self-attention with O(L squared) compute and a full KV cache, plus a dense feed-forward layer) versus the 2026 efficient hybrid stack (Mamba-2 state-space layers running in linear O(L) time with no KV growth, interleaved sparse attention at O(L·K) using a Lightning Indexer, a Latent Mixture-of-Experts calling 4x more experts for the same FLOPs, and multi-token prediction for built-in speculative decoding). Net effect: DeepSeek V4-Pro at 1M-token context uses ~27% of the FLOPs per token and ~10% of the KV-cache memory of the prior generation.](transformer_hollowing.svg)

Four techniques, all now in shipping models:

- **Hybrid Mamba–Transformer stacks.** NVIDIA's open-weight **Nemotron 3**
  family (Nano 3B / Super 12B / Ultra 55B active) interleaves **Mamba-2
  state-space (SSM) layers** — linear-time, no KV-cache growth — with a few
  **attention layers at key depths**. The SSM layers carry most of the sequence
  processing (making a **1M-token** window practical rather than theoretical);
  the sparse attention layers preserve **associative recall** (the "needle in a
  haystack" retrieval that pure SSMs struggle with). The **Mamba-3** paper
  pushes the SSM side further.
- **Fine-grained sparse attention.** DeepSeek V4's **DSA (DeepSeek Sparse
  Attention)** uses a "coarse filter, fine compute" scheme: tokens are
  compressed into super-entries, a **Lightning Indexer** picks the most relevant
  blocks, and only those get full attention — turning O(L²) into roughly
  **O(L·K)**. Measured effect at 1M context: **~27% of the FLOPs per token and
  ~10% of the KV-cache memory** of the prior generation.
- **Latent MoE + multi-token prediction.** Nemotron 3's **Latent MoE**
  compresses tokens before they reach the experts, letting the model call **~4×
  as many expert specialists for the same inference cost**. **Multi-token
  prediction (MTP)** emits several future tokens per forward pass, giving
  **built-in speculative decoding** for faster long-sequence generation.
- **Reasoning: Chain-of-Verification.** On the inference-protocol side, a
  recurring 2026 pattern has the model generate an answer, then generate
  verification questions about it, answer those independently, and use the
  inconsistencies to revise — a structured self-check rather than a single pass.

**The through-line:** 2026's efficiency gains are coming from *architecture*, not
just bigger clusters. That's what makes a 1M-token context affordable enough to
be a default rather than a premium tier — and it's why the open-weight field
(Nemotron 3, DeepSeek V4) is competitive on *cost per useful token* even where it
trails the closed frontier on raw benchmark score.

## 3. Regulation becomes a deadline — China (Jul 15) and the EU (Aug 2)

Two regulatory regimes stop being drafts and start binding this month.

**China — anthropomorphic-AI rules, Jul 15.** The Cyberspace Administration of
China's **Interim Measures for the Administration of AI Anthropomorphic
Interactive Services** (co-issued April 2026 with four partner agencies) take
effect Jul 15. They govern services that **simulate human personality, thinking,
and communication for sustained emotional interaction**, and require
**anti-addiction systems, mandatory usage notifications, and instant-exit
mechanisms** — features the regulators frame as architecturally incompatible
with persistent-memory companion agents. The response is already visible:

- **Alibaba's Qwen** disables humanlike and user-created agents **Jul 10**, with
  broader agent functions offline by Jul 15.
- **ByteDance's Doubao** turns off agent functionality **Jul 15**; existing
  configs and histories drop to **read-only until Oct 15**, then go.

This is the first major market to force a **product retraction** — not a fine or
a disclosure — over how an LLM presents itself to users.

**EU — AI Act enforcement, Aug 2.** The AI Act becomes broadly applicable
Aug 2: **Article 50 transparency obligations** (labeling AI interactions and
synthetic content) and most **high-risk** obligations for Annex III systems
(employment, credit, etc. — conformity assessment, data governance, logging,
human oversight) become enforceable at national and EU level, with maximum fines
of **€35M or 7% of global turnover**. (GPAI-model obligations landed earlier, in
Aug 2025; models on the market before then have until Aug 2027 to fully comply.)

**Why it belongs in an LLM brief:** taken together, these deadlines change the
*deployment* surface as much as the new models change the *capability* surface.
The same fortnight adds frontier options (§1) and removes deployment freedoms —
in China immediately, in the EU three-and-a-half weeks later.

## 4. Frontier & competition watch (brief)

- **Grok 4.5 — claims, no independent numbers.** xAI's Grok 4.5 (built on the
  **1.5T-parameter V9** base, with Cursor developer data in supplemental
  training) has been in **private beta at SpaceX and Tesla since Jun 28**. There
  is **no public API and no independent benchmark** — LMArena, Artificial
  Analysis, SWE-bench, and HLE have all *not* scored it. Musk's Opus-beating
  claims are, for now, evaluated only by engineers at sibling companies. Treat as
  unverified.
- **Microsoft's MAI family — the OpenAI-independence play continues.** At Build
  2026 (early June) Microsoft expanded its in-house **MAI** lineup into reasoning
  and coding: **MAI-Thinking-1** (its first reasoning model, pitched on low token
  cost) and **MAI-Code-1-Flash** (its first coding model). The framing is
  explicit — run on Azure, avoid OpenAI royalties, pass the savings to
  developers. A structural bet on **self-sufficiency**, not a benchmark headline.
- **SWE-bench Pro standings (Jul 4).** Claude **Mythos 5** leads at **80.3%**,
  **Fable 5** at **80.0%**, **Sakana Fugu Ultra** at **73.7%** — the
  orchestration-as-a-model open-weight entry still trailing the closed frontier
  by ~6 points on the contamination-resistant suite.
- **Fable 5 classifier — still refining.** Anthropic said Jul 1 it would keep
  tuning the over-flagging classifier "over the coming weeks" to cut false
  positives on routine coding (measured cost in Jul-03 §1). No new trigger-rate
  figure has been published since; the BridgeBench data point remains the last
  independent measurement.

## Bottom line

The export saga is over as a *story*; what replaces it is a **schedule**. The
week of Jul 13–17 delivers two frontier launches (Gemini 3.5 Pro on Jul 17,
DeepSeek V4 GA mid-July) and two hard regulatory lines (China Jul 15, EU Aug 2
close behind). Underneath the launches, the real advance is quieter and more
durable: **the dense transformer is being hollowed out** — hybrid SSM stacks and
fine-grained sparse attention are making million-token context a default, and
they're doing it in *open* weights. Capability is still won at the closed
frontier; **cost-efficiency is increasingly won in the open**. Plan around the
mid-July window on both axes — new options and new constraints arrive together.

## Sources

**Fable 5 / Mythos 5 (context, settled thread)**
- [Anthropic — statement on the US directive to suspend Fable 5 / Mythos 5](https://www.anthropic.com/news/fable-mythos-access)
- [CNBC — Trump admin lifts export controls on Fable 5 and Mythos 5 (Jun 30)](https://www.cnbc.com/2026/06/30/anthropic-says-trump-admin-has-lifted-export-controls-on-claude-fable-5-and-mythos-5.html)
- [Al Jazeera — US lifts restrictions on Fable and Mythos (Jul 1)](https://www.aljazeera.com/economy/2026/7/1/us-lifts-restrictions-on-powerful-ai-models-fable-mythos-anthropic-says)

**Mid-July releases (§1)**
- [TechTimes — Gemini 3.5 Pro cleared for July; GPT-5.6 stays locked](https://www.techtimes.com/articles/319318/20260629/gemini-35-pro-cleared-july-launch-fable-5-nears-return-gpt-56-stays-locked.htm)
- [Geeky Gadgets — Google delays Gemini 3.5 Pro to July 17 to upgrade math](https://www.geeky-gadgets.com/gemini-pro-scraps-base-model/)
- [TechTimes — Gemini 3.5 Pro nears launch: 2M context and Deep Think](https://www.techtimes.com/articles/317919/20260606/google-gemini-35-pro-nears-june-launch-2-million-token-context-deep-think-reasoning.htm)
- [NVIDIA build — DeepSeek-V4-Pro model card](https://build.nvidia.com/deepseek-ai/deepseek-v4-pro/modelcard)
- [Atlas Cloud — DeepSeek-V4 preview: million-token context & agent upgrades](https://www.atlascloud.ai/blog/ai-updates/deepseek-v4-preview-launch)

**Architecture (§2)**
- [NVIDIA — Introducing Nemotron 3 Super: open hybrid Mamba-Transformer MoE](https://developer.nvidia.com/blog/introducing-nemotron-3-super-an-open-hybrid-mamba-transformer-moe-for-agentic-reasoning/)
- [VentureBeat — Nvidia debuts Nemotron 3 with hybrid MoE and Mamba-Transformer](https://venturebeat.com/technology/nvidia-debuts-nemotron-3-with-hybrid-moe-and-mamba-transformer-to-drive)
- [Mamba-3: Advanced State Space Sequence Models (EmergentMind)](https://www.emergentmind.com/papers/2603.15569)
- [TechTimes — DeepSeek V4 architecture: how sparse attention cuts inference costs](https://www.techtimes.com/articles/318725/20260619/deepseek-v4-architecture-how-sparse-attention-cuts-inference-costs-what-nist-found.htm)
- [Dr. Kaoutar El Maghraoui — DeepSeek V4, sparse attention, and open-weight AI](https://kaoutarelmaghraoui.com/blog/deepseek-v4-long-march-open-weight-ai/)

**Regulation (§3)**
- [TechTimes — China AI companion law arrives July 15: Doubao and Qwen agent data deleted](https://www.techtimes.com/articles/319703/20260704/china-ai-companion-law-arrives-july-15-doubao-qwen-agent-data-will-deleted.htm)
- [TechNode — Doubao and Qwen to shut down AI agent features on July 15](https://technode.com/2026/07/06/bytedances-doubao-and-alibabas-qwen-to-shut-down-ai-agent-features-on-july-15/)
- [SCMP — ByteDance and Alibaba disable humanlike AI custom agents as new rules loom](https://www.scmp.com/tech/big-tech/article/3359482/bytedance-and-alibaba-disable-humanlike-ai-custom-agents-new-rules-loom)
- [European Commission — AI Act regulatory framework](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)
- [Kennedys — EU AI Act implementation timeline: the next compliance deadline](https://www.kennedyslaw.com/en/thought-leadership/article/2026/the-eu-ai-act-implementation-timeline-understanding-the-next-deadline-for-compliance/)

**Competition watch (§4)**
- [DigitalApplied — Grok 4.5: SpaceX's 1.5T V9 model, private beta](https://www.digitalapplied.com/blog/grok-4-5-cursor-data-flywheel-spacex-private-beta-2026)
- [TimesofAI — Grok 4.5 enters private beta at Tesla, SpaceX](https://www.timesofai.com/news/xai-launches-grok-4-5-private-beta/)
- [Windows Central — Microsoft launches seven in-house AI models to reduce OpenAI reliance](https://www.windowscentral.com/software-apps/microsoft-launches-seven-in-house-ai-models-to-cut-developer-costs-and-reduce-reliance-on-openai)
- [CNBC — Microsoft unveils in-house AI models to lessen OpenAI reliance](https://www.cnbc.com/2026/06/02/microsoft-unveils-new-ai-models-lessen-reliance-on-openai-lower-costs.html)
- [Morph — SWE-bench Pro leaderboard (2026)](https://www.morphllm.com/swe-bench-pro)

*Compiled Mon Jul 6, 2026 (Los Angeles time). Some searches returned transient errors during compilation; the brief proceeds on the sources that resolved and flags any single-sourced claim (e.g. the DeepSeek mid-July GA window) as such.*
