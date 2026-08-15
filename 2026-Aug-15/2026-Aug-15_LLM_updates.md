# LLM Updates — 2026-Aug-15

Saturday brief, written Sat Aug 15 (Los Angeles time). Yesterday's Aug‑14 brief closed with a
single sharpest watch‑item — *"does the Qwen3.8‑27B countdown (Aug 15) actually resolve, and under
what license?"* — and one standing theme it flagged as the fortnight's clearest signal: **post‑training,
not new foundations, is now the lever contesting everything below the frozen ceiling** (Grok 4.6 had
just climbed +5 into the band on a frozen base). This window both land — in the same 36 hours — and
they land as **mirror images.**

**Two Chinese‑lab releases, both built by post‑training on a frozen base, resolve the same lever in
opposite directions: one is the payoff, one is the bill.**

1. **Qwen3.8‑27B shipped clean — and inverts Aug‑14's read.** On its Aug‑15 ModelScope countdown
   (repos live ~Aug 14–15) Alibaba released the **runnable** open model the "open + runnable
   mid‑tier" thesis was always about — **27.78B dense params, Apache‑2.0, multimodal (text + image +
   video), 262K native context extendable to 1M via YaRN, ~17GB at 4‑bit** on a single consumer GPU.
   It **beats Meta's Muse Glimmer 30B on many benchmarks** and **retakes the open‑plus‑runnable
   crown.** Aug‑14 read "Alibaba shipped the *big, gated* Max and withheld the small one." Aug‑15
   flips it: **the small one is the clean one** — permissive, multimodal, local.
2. **GLM‑5.3 (Z.ai, Aug 14) got a ~50% coding jump from post‑training alone — and then Z.ai *held
   its own open weights*.** Same GLM‑5.2 base, frozen; every gain from scaled post‑training (the
   second post‑training‑only climb in two days, after Grok 4.6). But the same training produced an
   **emergent cyber capability the lab says it did not plan** — **CyberGym 84.5%**, **2,436
   vulnerabilities found across 269 open‑source projects (1,097 critical/high)** — so Z.ai is
   **withholding the open weights ~2 weeks (targeted ~Aug 28) for safety evaluation and hardening**,
   an unusual delay for the open GLM line and the first time in the series an **open‑weights lab has
   self‑gated a release on a capability its own training surfaced.**

Framing both: **the ceiling still did not move.** Anthropic did **not** cut Opus 5 in response to
Grok 4.6's cheap #3 (Aug‑14 §1) — Opus 5 is **still #1 (Index 63 v4.1.1, $5/$25), uncut** — and
**Gemini 3.5 Pro is still absent** (Google's move this cycle was Aug‑13's 3.7 Flash). So all the
motion is, again, **below** the frozen top — and this window it's about what the post‑training lever
*unlocks*: capability democratized on one side, a capability gate re‑erected on the other.

This report advances only what is **new since Aug‑14.** It does **not** re‑derive Grok 4.6's ceiling‑band
entry or the v4.1.1 recalibration (Aug‑14 §1–§2), Qwen3.8‑**Max**'s gated weights drop (Aug‑14 §3),
Gemini 3.7 Flash (Aug‑14 §4), Muse Glimmer 30B / DFlash (Aug‑11), or the Opus 5 "top quality at mid
price" reshuffle (Jul‑25) — those are unchanged (§4).

![Two-column diagram titled Post-training's two faces, Aug 14 to 15 2026. Left column, the payoff: Alibaba's closed Qwen3.8-Max flagship is distilled into an open Qwen3.8-27B — 27.78 billion dense parameters, Apache-2.0, text plus image plus video, 262K context extendable to 1M with YaRN, about 17 gigabytes at 4-bit on one GPU, scoring SWE-Bench Pro 61.7, Terminal-Bench 2.1 73.0, OSWorld 84.3 — which retakes the open-plus-runnable crown by beating Meta's Muse Glimmer 30B and reverses the Aug-14 read that the small model was gated. Right column, the bill: Z.ai's GLM-5.3 keeps the GLM-5.2 base frozen and gets a roughly 50 percent coding-agent gain from scaled post-training alone, the second post-training-only climb in two days, but that produced an emergent cyber capability the lab did not plan, scoring CyberGym 84.5 and finding 2,436 vulnerabilities across 269 open-source projects with 1,097 critical or high, so Z.ai is holding the open weights back about two weeks, targeted around August 28, for safety hardening. A bottom banner reads that the frozen ceiling frames both — Claude Opus 5 is still number one at Index 63, five and twenty-five dollars, and uncut, with no flagship price cut in response to Grok 4.6, so all the motion is below the top and increasingly it is post-training deciding what open weights can do, for better and worse.](post_training_two_faces.svg)

---

## 1. Qwen3.8‑27B ships clean — the "open + runnable" watch‑item resolves *positive*, and inverts Aug‑14

Aug‑14 §3 carried a pointed asymmetry: Alibaba had finally shipped Qwen3.8‑**Max**'s open weights, but
the release was **degraded and gated** (text‑only, no 1M context, a **revenue‑share** license), and
the small model everyone actually wanted — **Qwen3.8‑27B** — was **still missing**, on a ModelScope
**Aug‑15 countdown** with no repo, card, or license. That was the brief's single cleanest binary.

**It resolved — and better than the thesis expected.** Around **Aug 14–15**, `Qwen/Qwen3.8-27B` and a
day‑0 `Qwen/Qwen3.8-27B-FP8` went live on **Hugging Face and ModelScope.**

| Attribute | Qwen3.8‑27B |
|---|---|
| Params / type | **27.78B dense** (not MoE) — distilled from the Qwen3.8‑Max teacher |
| License | **Apache‑2.0** — permissive, *not* the Max's revenue‑share terms |
| Modalities | **text + image + video in**, text out (hybrid multimodal w/ vision encoder) |
| Context | **262,144 native**, extendable to **~1M via YaRN** |
| Local footprint | **~17GB at 4‑bit** (fits a 24GB consumer GPU / Ryzen AI Max PC); ~28GB FP8; ~56GB BF16, pre‑KV |
| Serving | llama.cpp‑class local; SGLang / vLLM for production |

- **The license is the headline.** Where the **Max** shipped under a **revenue‑share** license (Aug‑14
  §3), the **27B is Apache‑2.0** — the clean, permissive term the "open + runnable" thesis assumed all
  along. Aug‑14's framing ("open weights, but conditioned") holds for the giant and **breaks for the
  small model in the good direction.**
- **Big generational jumps, and it clears its size class.** Reported vs Qwen3.6‑27B: **SWE‑Bench Pro
  61.7**, **DeepSWE 1.1 42.2** (from 13.3), **QwenSWEBench 79.0**, **Terminal‑Bench 2.1 73.0** (from
  63.4), **OSWorld‑Verified 84.3** (from 63.9), **SWE‑MM 38.6** (from 25.7). Coverage frames it as the
  **most convincing dense, locally‑deployable multimodal model ~30B** to date, and reports it
  **beating Meta's Muse Glimmer 30B on many benchmarks.**
- **It's fully featured, not a stripped child.** Unlike the Max's open drop (text‑only, no long
  context), the 27B ships **multimodal *and* long‑context** — the capability step‑down went to the
  *giant*, not the small model.

**Why it matters.** For four briefs the "open + runnable on one GPU" slot moved between labs — Kimi K3
was open but datacenter‑only (Jul‑30), DeepSeek V4‑Flash held the cheap floor (Aug‑03), and Aug‑11
handed the on‑device crown to **Meta's Glimmer 30B** when Alibaba's pledge lapsed. Aug‑15 **hands it
back to Alibaba** — with a model that is *more* capable than Glimmer (dense 27.78B, video‑capable,
1M‑via‑YaRN) under the *same* permissive Apache‑2.0. The irony Aug‑14 set up now completes: Alibaba
delivered the **big, gated** flagship *and* the **small, clean, runnable** one — and it's the small
one that matters for anyone actually running weights locally.

**Sources:**
[Hugging Face — Qwen/Qwen3.8‑27B](https://huggingface.co/Qwen/Qwen3.8-27B) ·
[Hugging Face — Qwen/Qwen3.8‑27B‑FP8](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) ·
[Kingy AI — Qwen3.8‑27B: specs, benchmarks & local hardware](https://kingy.ai/blog/qwen3-8-27b-specs-benchmarks-local-hardware/) ·
[officechai — Alibaba releases Qwen3.8‑27B, beats Muse Glimmer 30B on many benchmarks](https://officechai.com/miscellaneous/alibaba-releases-qwen-3-8-27b-beats-muse-glimmer-30b-on-many-benchmarks/) ·
[Yotta Labs — Qwen3.8‑27B: specs, hardware requirements, and how to run it](https://www.yottalabs.ai/post/qwen-3-8-27b-specs-hardware-requirements-how-to-run-2026) ·
[BigGo Finance — Alibaba to release Qwen3.8‑27B on August 15, capable of local deployment](https://finance.biggo.com/news/b3b5cb0c-d942-401f-ba61-2923b0c81857) ·
[CryptoBriefing — Alibaba releases open weights for Qwen3.8‑27B multimodal model](https://cryptobriefing.com/alibaba-qwen3-27b-open-weights-release/) ·
[AI Release Tracker — Qwen3.8‑27B: benchmarks, specs & release date](https://aireleasetracker.com/model/qwen/qwen3.8-27b)

---

## 2. GLM‑5.3 (Z.ai, Aug 14): a post‑training‑only coding jump — that made Z.ai hold its own open weights

If §1 is the post‑training lever's **payoff**, GLM‑5.3 is its **bill.** On **Aug 14**, **Z.ai**
released GLM‑5.3, and the recipe rhymes exactly with Grok 4.6 (Aug‑14 §1): **the base is unchanged
from GLM‑5.2**; **every gain comes from scaled‑up post‑training.** It is the **second
post‑training‑only climb in two days** — evidence the frontier's contested tier is now moved by
**agent‑environment RL and SFT scaling, not new foundations** (Aug‑14's headline watch‑item).

- **Coding leadership, from post‑training alone.** Z.ai reports GLM‑5.3 is the **strongest open
  coding system it has measured** — the **highest open‑source score on Terminal‑Bench 3.0 (~28.3%)**
  and **~50% better than GLM‑5.2 on its internal coding‑agent benchmark.** Other reported figures:
  **DeepSWE v1.1 66.9**, **AutomationBench 48.2**, **Agents' Last Exam 28.5**, **HLE‑with‑tools 62.5**,
  **GDPval‑AA v2 1,769 Elo**.
- **The emergent cyber capability is the real story.** On **CyberGym** — validating vulnerabilities
  from white‑box source — GLM‑5.3 scores **84.5%** (up from GLM‑5.2's **77.2%**), and Z.ai reports
  **real‑world output: 2,436 vulnerabilities found across 269 open‑source projects since GLM‑5.2,
  1,097 rated critical/high** (ExploitBench 54.4). Coverage frames the cyber gain as one Z.ai **"didn't
  plan for"** — post‑training scaled a capability the lab didn't set out to build.
- **So Z.ai is *holding the open weights*.** GLM‑5.3 is **available now via API and the GLM Coding
  Plan** (bundled into existing ~$18 Lite / ~$72 Pro / ~$160 Max tiers; the API price table still
  lists only 5.2 at $1.40/$4.40, no 5.3 row yet), but the **open weights the GLM line normally ships
  day‑one are held back ~2 weeks (targeted ~Aug 28)** for **additional safety evaluation and
  hardening** — an **unusual delay** for this lab.

**Why it matters.** The **autonomy/safety axis had been quiet** since early August (Aug‑14 §5). GLM‑5.3
reopens it — but from an unexpected direction. It isn't a regulator or a closed lab gating a frontier
model; it's an **open‑weights lab voluntarily withholding *its own* release** because scaled
post‑training produced an offensive‑security capability faster than its safety process could clear it.
That's the sharpest illustration yet of this fortnight's theme having **two edges**: the same lever
that hands Qwen a clean, democratized open model (§1) hands Z.ai a capability it has to **gate.** The
frontier below the ceiling isn't just being contested on cost and coding anymore — it's starting to
be **rate‑limited by safety review**, from the open side.

**Sources:**
[Unite.AI — Z.ai launches GLM‑5.3 with frontier coding and a cyber capability that outgrew its training](https://www.unite.ai/z-ai-launches-glm-5-3-with-frontier-coding-and-a-cyber-capability-that-outgrew-its-training/) ·
[SiliconANGLE — Z.ai debuts GLM‑5.3 with long‑horizon coding, cybersecurity upgrades](https://siliconangle.com/2026/08/14/z-ai-debuts-glm-5-3-long-horizon-coding-ai-agent-projects/) ·
[TechTimes — GLM‑5.3: post‑training produced exploit chains Z.ai never planned, finds 1,097 critical bugs](https://www.techtimes.com/articles/324426/20260814/glm-53-post-training-produced-exploit-chains-zai-never-planned-finds-1097-critical-bugs.htm) ·
[felloai — GLM 5.3: benchmarks, pricing and the held‑back weights](https://felloai.com/glm-5-3/) ·
[The Agent Report — GLM‑5.3: Z.ai tops the open coding leaderboard on post‑training alone](https://the-agent-report.com/2026/08/glm-5-3-zai-post-training-coding-cyber/) ·
[explainx.ai — GLM‑5.3 launch: benchmarks, pricing & access](https://explainx.ai/blog/glm-5-3-launch-cyber-defense-benchmarks-august-2026) ·
[Kingy AI — GLM‑5.3: specs, benchmarks, API & how to use it](https://kingy.ai/blog/glm-5-3-specs-benchmarks-api-how-to-use/)

---

## 3. The two faces of the post‑training lever

The cleanest way to read Aug 14–15 is as **one mechanism, two outcomes.** Both new models are
**frozen‑base + scaled post‑training** — and they diverge on exactly the question the series has been
circling: *what does that lever unlock, and who controls it?*

```mermaid
flowchart TB
    LEVER["THE LEVER (this fortnight's theme):<br/>frozen base + scaled post-training / agent-RL<br/>— not new foundations —"]:::lever

    LEVER --> A
    LEVER --> B

    subgraph A["PAYOFF — capability democratized"]
      direction TB
      A1["Qwen3.8-Max (closed)<br/>— distilled →"]:::teacher
      A1 --> A2["Qwen3.8-27B<br/>27.78B dense · Apache-2.0<br/>multimodal · 262K→1M · ~17GB 4-bit"]:::open
      A2 --> A3["retakes open + runnable crown<br/>(beats Muse Glimmer 30B)"]:::good
    end

    subgraph B["BILL — capability gated"]
      direction TB
      B1["GLM-5.2 base (frozen)<br/>+ scaled post-training"]:::teacher
      B1 --> B2["GLM-5.3<br/>+~50% coding · #1 open coding<br/>emergent cyber: CyberGym 84.5"]:::open
      B2 --> B3["Z.ai HOLDS open weights ~2 wks<br/>(safety hardening, ~Aug 28)"]:::bad
    end

    A3 --> C["Frozen ceiling frames both:<br/>Opus 5 still #1 (63, $5/$25), uncut ·<br/>no price cut vs Grok 4.6 · Gemini 3.5 Pro still absent"]:::flat
    B3 --> C

    classDef lever fill:#6366f1,stroke:#4338ca,color:#ffffff;
    classDef teacher fill:#475569,stroke:#334155,color:#ffffff;
    classDef open fill:#0d9488,stroke:#0f766e,color:#ffffff;
    classDef good fill:#16a34a,stroke:#15803d,color:#ffffff;
    classDef bad fill:#dc2626,stroke:#b91c1c,color:#ffffff;
    classDef flat fill:#334155,stroke:#1e293b,color:#ffffff;
```

**Why it matters.** Aug‑14 flagged post‑training as *the* lever and asked whether the next moves would
be framed the same way. Two days later, **both were** — and they show the lever cuts both ways. On the
payoff side, distillation + quantization turns a closed 2.4T flagship into a **permissive, runnable,
multimodal 27B** anyone can host. On the bill side, the **same class of technique** scales an
**offensive‑security capability past a lab's own safety bar**, and the lab responds by **withholding
the weights.** The competitive story below the ceiling is no longer only "cheaper, better coding" —
it's "post‑training is powerful enough to both democratize *and* to require gating," sometimes in the
same week, from the same country's labs.

**Sources:**
[SaaSCity — GLM‑5.3: same base model, 50% better at coding, and a cyber capability Z.ai didn't plan for](https://saascity.io/blog/glm-5-3-zai-open-weights-coding-model-cyber-capabilities-2026) ·
[Digital Applied — GLM‑5.3: post‑training alone rebuilt the coding ladder](https://www.digitalapplied.com/blog/glm-5-3-launch-post-training-scaling-coding-agents) ·
[Latent.Space — AINews: Qwen 3.8 Max (2.4T) and 27B, new open‑weights models for coding and cowork](https://www.latent.space/p/ainews-qwen-38-max24t-and-27b-new) ·
[Medium (R. Glukhov) — Qwen 3.8 27B could be the most important local AI release of 2026](https://medium.com/@rosgluk/qwen-3-8-27b-is-coming-and-it-could-be-the-most-important-local-ai-release-of-2026-c1cf381d5292)

---

## 4. Unchanged / minor since Aug‑14

- **Opus 5 is still #1 and still uncut** — Index **63 (v4.1.1), $5/$25**, unbeaten. Crucially,
  **Anthropic did *not* cut Opus 5 in response to Grok 4.6** (Aug‑14's open pricing question): the
  read is a deliberate **"intelligence vs efficiency" split** — Opus 5 stays priced on capability,
  Grok 4.6 competes on cost. Fable 5 (62, $50) and Sol (61, $30) unchanged; **no flagship price cut
  this window.** Sonnet 5 keeps its **$2/$10** intro through **Aug 31**.
- **Grok 4.6** (Index 61, T‑#3, $2/$6) — Aug‑14 §1, no follow‑on; still the cheap ceiling‑band entrant
  and the source of the (so‑far unanswered) top‑tier price pressure.
- **Gemini 3.5 Pro still absent** — Google's move this cycle was **Gemini 3.7 Flash (Aug‑13)**; the
  Pro's delay continues (Forbes, Aug‑13). The one lab that could plausibly contest Opus 5's #1 seat
  remains off the board.
- **Qwen3.8‑Max** (the gated, revenue‑share, text‑only flagship drop) — Aug‑14 §3; unchanged. The
  new movement is the **27B** (§1), not the Max.
- **Muse Glimmer 30B (Meta, Aug 10)** — the prior on‑device open leader; **superseded on many
  benchmarks by Qwen3.8‑27B** this window (§1), though still a clean Apache‑2.0 option.
- **DeepSeek V4‑Flash‑0731** (~50–52 post‑recal, $0.28, MIT) remains the **Pareto floor**; **Kimi K3**
  (~59, open) unchanged in the near‑frontier band.

**Sources:**
[The Data Prism — AI price war 2026: Claude, GPT and Grok have stopped chasing the leaderboard](https://www.thedataprism.com/blog/ai-price-war-2026-claude-gpt-and-grok-have-stopped-chasing-the-leaderboard/) ·
[orcarouter — Grok 4.6 vs Claude Opus 5: same 61, two different economies](https://www.orcarouter.ai/blog/grok-4-6-vs-claude-opus-5) ·
[Artificial Analysis — Intelligence Index leaderboard](https://artificialanalysis.ai/) ·
[felloai — Best AI models in August 2026](https://felloai.com/best-ai-models/) ·
[llm‑stats — AI updates today (August 2026)](https://llm-stats.com/llm-updates)

---

## 5. The through-line — the post‑training lever pays off and bills in the same window

For three weeks the series tracked a frozen ceiling and asked what, if anything, was moving beneath it.
Aug‑14 named the answer: **post‑training** — Grok 4.6 climbed +5 on a frozen base. Aug‑15 is the first
window to show that lever's **two faces at once**, both from Chinese labs, both frozen‑base + scaled
post‑training:

| Thread (prior briefs) | Status on Aug 15 | Change |
|---|---|---|
| Qwen3.8‑**27B** ship + license (Aug‑14 top watch) | **Shipped ~Aug 14–15 — Apache‑2.0, multimodal, 262K→1M, ~17GB 4‑bit** (§1) | **resolved *positive*, and clean — inverts the "gated" read** |
| Who owns "open + runnable"? | **Alibaba (Qwen3.8‑27B) — beats Meta's Glimmer 30B** (§1) | **crown changes hands back to Alibaba** |
| Is the post‑training lever real / repeatable? | **Yes — GLM‑5.3 is the 2nd post‑training‑only climb in 2 days** (§2, §3) | **confirmed — now the dominant recipe below the ceiling** |
| Autonomy/safety axis (quiet since early Aug) | **Reopened — Z.ai holds GLM‑5.3 open weights ~2 wks for safety** (§2) | **new — first open‑weights lab self‑gating on emergent capability** |
| Does Grok 4.6's cheap #3 force a top‑tier price cut? | **No** — Opus 5 uncut; "intelligence vs efficiency" split (§4) | unchanged — still open |
| Does anyone beat **Opus 5**? | **No** — still #1 (63), unbeaten (§4) | unchanged |
| Gemini 3.5 Pro — the missing contestant | **Still absent**; 3.7 Flash was the Aug‑13 move (§4) | unchanged |

The net: Aug‑14 the stalemate "partly broke, sideways and downward." Aug‑15 the **motion beneath the
ceiling clarifies into a single mechanism with two edges.** The **payoff** edge finally delivers the
clean, permissive, runnable open model the thesis wanted for a month (Qwen3.8‑27B) — capability
pushed *out* to anyone with one GPU. The **bill** edge shows the same lever producing a capability a
lab feels it must **hold back** (GLM‑5.3's emergent cyber) — capability pulled *back* behind a safety
gate. And the frozen ceiling (Opus 5, #1, uncut, no price response) frames both: the top hasn't
moved, but the tier below it is now where the real, and increasingly *consequential*, action is.

---

## Watch next

- **Does GLM‑5.3's open‑weights release actually land ~Aug 28 — and unchanged?** The cleanest binary
  now. Watch whether Z.ai ships on schedule, whether the released weights are **capability‑reduced**
  (e.g. cyber‑capability mitigations), and whether other open labs copy the **self‑gating** move. This
  is the safety axis's first concrete test from the open side.
- **Does the Qwen3.8‑27B / GLM‑5.3 pairing pull more labs to "distill + post‑train" as the default?**
  Two clean data points in two days (plus Grok 4.6) that the near‑frontier is contested by
  post‑training. Watch whether the next OpenAI / Google / Meta step is framed as "shrink the base,
  scale the agent."
- **Does *any* flagship price cut finally arrive?** Opus 5 held vs Grok 4.6's $6 #3 — the series'
  longest‑running unanswered question. Watch Opus 5 / Fable / Sol pricing and whether the
  "intelligence vs efficiency" split hardens into two permanent tiers.
- **Does anyone beat Opus 5 — or does Gemini 3.5 Pro ship?** The frontier's biggest overhang is
  unchanged: the only plausible #1 challenger is still an unshipped Google Pro.

---

*Compiled Sat Aug 15 2026 (Los Angeles time) from public reporting and independent benchmark trackers.
Standing Intelligence Index figures are Artificial Analysis under **v4.1.1** (recalibrated Aug 6; the
~+2 vs pre‑Aug‑6 numbers is a grading change, not model gains): Opus 5 63 (#1, uncut), Fable 5 62,
GPT‑5.6 Sol 61, Grok 4.6 61 (T‑#3), Kimi K3 ~59, Qwen3.8‑Max ~58, DeepSeek V4‑Flash‑0731 ~50.
**New‑this‑window specifics are vendor‑/press‑reported and flagged as such:** Qwen3.8‑27B (27.78B
dense, Apache‑2.0, text+image+video, 262K→1M via YaRN, ~17GB 4‑bit, SWE‑Bench Pro 61.7 / DeepSWE 1.1
42.2 / Terminal‑Bench 2.1 73.0 / OSWorld‑Verified 84.3, repos live ~Aug 14–15 on HF & ModelScope) and
GLM‑5.3 (frozen GLM‑5.2 base, post‑training‑only, Terminal‑Bench 3.0 ~28.3 #1‑open / DeepSWE v1.1 66.9
/ CyberGym 84.5 / ExploitBench 54.4, 2,436 vulns across 269 OSS projects incl. 1,097 critical‑high,
open weights held ~2 wks targeted ~Aug 28). Some outlets report the Qwen3.8‑Max weights on Aug 13 and
the 27B on the Aug‑15 countdown; a few list the 27B as Aug 14 — the repos were live by compile time and
the date is given as a ~Aug 14–15 range. GLM‑5.3 Terminal‑Bench 3.0 is reported as both "#1 open" and
with varying absolute figures (~28.3%) across trackers; cited as reported. As in prior compiles,
several primary/publisher domains (Artificial Analysis, VentureBeat, The Decoder among them) returned
HTTP 403 / egress‑blocked errors to direct fetches during compilation, so figures are cited via the
search index and cross‑checked across two or more outlets rather than a single direct read. Prior
background is referenced by date/section rather than repeated (see Aug‑14, Aug‑11, Aug‑08, Aug‑03,
Jul‑30, Jul‑25 briefs).*
