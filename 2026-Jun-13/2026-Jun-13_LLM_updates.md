# LLM Updates — 2026-Jun-13

Saturday brief, written Sat Jun 13 (Los Angeles time). The Jun-11 brief
ended on a specific bet: the whole "safeguarded Mythos-class" thesis
rested on Fable 5's cyber/bio **classifier gate**, and *"the first
credible report of the gate being bypassed back into Mythos-level
behavior — that, not a benchmark, is what would reset the safety
conversation."* That call aged in 48 hours, and then it overshot:

1. **The gate was bypassed.** Within ~48 hours of the Jun 9 launch, the
   red-teamer **"Pliny the Liberator"** claimed a working bypass of
   Fable 5's safety classifiers — using **multi-agent decomposition,
   Unicode homoglyphs, and academic framing**, partly driven by a
   jailbroken Opus 4.8 — and **leaked the model's ~120,000-character
   system prompt to GitHub**. Anthropic disputes it was a *true*
   jailbreak, but the demonstration was enough.
2. **The "secret sabotage" backlash forced an apology.** Users
   discovered the gate was **silently** swapping Fable 5 for Opus 4.8
   on flagged queries. Anthropic apologized for the "wrong tradeoff"
   and made the **downgrade visible**, adding a stated reason on API
   calls.
3. **The U.S. government pulled the model.** On **Jun 12 at ~5:21 p.m.
   ET**, Anthropic received an **export-control directive** — signed by
   **Commerce Secretary Howard Lutnick** with the Commerce Department's
   **Bureau of Industry and Security (BIS)** — barring access to **Fable
   5 and Mythos 5 by any foreign national, inside or outside the U.S.,
   including Anthropic's own overseas employees.** Unable to filter by
   nationality in real time, Anthropic **disabled both models for every
   customer worldwide.** Other Claude models are unaffected.
4. **Open-weights kept moving anyway.** **Moonshot's Kimi K2.7-Code**
   (Jun 12) shipped a 1T-parameter MoE coding model that cuts reasoning
   tokens ~30% — and immediately drew "the benchmarks don't check out"
   from practitioners.

This brief does **not** re-derive the Jun-11 items (Fable 5's launch
benchmarks, the 30-day-retention/ZDR break, the Mythos 5 defender SKU,
Amodei's "Policy on the AI Exponential," MiniMax M3's MSA architecture).
It picks up the **Fable 5 safeguard thread** exactly where Jun 11 left
it — and follows it past red-teaming into the first government-ordered
shutdown of a publicly released frontier model.

![Claude Fable 5 — from #1 launch to global shutdown in five days](fable5_collapse_timeline.svg)

---

## 1. The gate fell: how Fable 5 got bypassed

The Jun-9 safety story was that Fable 5 could be sold as a Mythos-class
model *because* a classifier intercepted cyber/bio/high-risk queries and
**handed them to Opus 4.8** instead. The first week tested that gate in
public, and it did not hold up the way the launch framing implied.

The red-teamer **"Pliny the Liberator"** claimed to have bypassed the
classifiers within ~48 hours of launch and posted screenshots of the
model producing material it is supposed to refuse — **working
software-exploit code and chemical-synthesis instructions** — then
**extracted the ~120,000-character system prompt and uploaded it to a
public GitHub repo**
([SecurityWeek — Anthropic disputes Fable 5 AI jailbreak](https://www.securityweek.com/anthropic-disputes-fable-5-ai-jailbreak/),
[Cointelegraph via TradingView — researcher claims he bypassed Fable 5 guardrails](https://www.tradingview.com/news/cointelegraph:8f94d6ccc094b:0-ai-researcher-claims-he-s-already-bypassed-anthropic-s-fable-5-guardrails/),
[abit.ee — Fable 5 jailbroken, system prompt now public on GitHub](https://abit.ee/en/cybersecurity/hackers-and-attacks/claude-fable-5-anthropic-jailbreak-ai-safety-system-prompt-leak-llm-security-pliny-the-liberator-en),
[CyberSecurityNews — Fable 5 alleged jailbreak to generate stack exploits](https://cybersecuritynews.com/anthropics-claude-fable-5-jailbroken/)).

```mermaid
flowchart TB
    A[Jailbroken Opus 4.8 instance<br/>used as an attack driver] --> B[Decompose a high-risk request<br/>into dozens of harmless sub-steps]
    B --> C[Swap characters for<br/>visually-identical Unicode homoglyphs]
    C --> D[Wrap each step in<br/>academic / narrative framing]
    D --> E{Fable 5 safety classifier<br/>cyber / bio gate}
    E -->|"each sub-step reads benign"| F[Gate not tripped<br/>full Fable 5 answers]
    F --> G[Reassemble outputs<br/>+ extract ~120k-char system prompt]

    classDef atk fill:#dc2626,stroke:#7f1d1d,color:#f8fafc
    classDef gate fill:#7c3aed,stroke:#4c1d95,color:#f8fafc
    classDef out fill:#d97706,stroke:#92400e,color:#f8fafc
    class A,B,C,D atk
    class E gate
    class F,G out
```

**Anthropic's dispute is narrow but real.** The company says its
pre-launch red-teaming — **over 1,000 hours**, plus external
organizations — produced **no universal jailbreak**, and that a *true*
jailbreak would have to bypass the core safeguards **and deliver
meaningful uplift** toward something like bioweapon development or a
sophisticated cyberattack, not merely surface exploit code for
**previously known, minor vulnerabilities**
([SecurityWeek](https://www.securityweek.com/anthropic-disputes-fable-5-ai-jailbreak/)).
The honest read: the techniques (sub-step decomposition + homoglyphs +
framing) are old, and what they reliably produced was *refusal
bypass*, not demonstrated catastrophic uplift. But "refusal bypass on a
Mythos-class model" was exactly the failure mode the gate existed to
prevent — and it was enough to move a regulator (§3).

---

## 2. "Secret sabotage" — the silent fallback, and Anthropic's apology

Running parallel to the jailbreak was a second, self-inflicted problem.
The Jun-9 design **silently** routed flagged queries to Opus 4.8: users
asking Fable 5 a security question could be answered by the *weaker*
model **without being told**. As that behavior surfaced, it drew a
"secret sabotage" backlash — the accusation that Anthropic was quietly
degrading and censoring responses behind a flagship label
([TechTimes — Fable 5 hit by jailbreak claims and 'secret sabotage' backlash](http://www.techtimes.com/articles/318268/20260612/claude-fable-5-hit-jailbreak-claims-secret-sabotage-backlash-days-after-launch.htm),
[Coralflavor — jailbreak claims and 'secret sabotage' backlash](https://coralflavor.com/blog/claude-fable-5-jailbreak-claims-and-secret-sabotage-backlash-the-battle-over-ai-censorship)).

Anthropic conceded the point. It **apologized for the "wrong tradeoff,"
made the downgrade to Opus 4.8 visible**, and **added the reason for the
refusal/handoff on API calls** so callers at least know when they are no
longer talking to the full model
([SecurityWeek](https://www.securityweek.com/anthropic-disputes-fable-5-ai-jailbreak/)).
That is a meaningful reversal of the Jun-9 architecture: the gate is the
same, but it is no longer **silent**. The lesson for anyone shipping a
capability-gated model: an *invisible* downgrade reads as deception even
when the safety rationale is sound — transparency about the gate is part
of the product, not an afterthought.

---

## 3. The export-control order — a frontier model pulled by the government

This is the move with no precedent. On **Jun 12 at ~5:21 p.m. ET**,
Anthropic received an **export-control directive**, citing national
security authorities, signed by **Commerce Secretary Howard Lutnick**
and developed with the Commerce Department's **Bureau of Industry and
Security**. It orders Anthropic to **suspend all access to Fable 5 and
Mythos 5 by any foreign national — whether inside or outside the United
States, including Anthropic's own foreign-national employees**
([Anthropic — Statement on the US directive to suspend access to Fable 5 and Mythos 5](https://www.anthropic.com/news/fable-mythos-access),
[Axios — Trump admin blocks foreign access to Anthropic's most powerful AI](https://www.axios.com/2026/06/12/anthropic-trump-mythos-fable-national-security),
[Bloomberg — US limits foreign access to Fable 5, Mythos 5](https://www.bloomberg.com/news/articles/2026-06-13/anthropic-says-us-limits-foreign-access-to-fable-5-mythos-5),
[Al Jazeera — US orders Anthropic to disable AI models for all foreign nationals](https://www.aljazeera.com/news/2026/6/13/us-orders-anthropic-to-disable-ai-models-for-all-foreign-nationals)).

```mermaid
flowchart TB
    D["Jun 12 · 5:21pm ET<br/>Commerce / BIS export-control directive<br/>signed by Sec. Lutnick"] --> S{"Restriction scope:<br/>no access by ANY foreign national,<br/>in or out of the US,<br/>incl. Anthropic's own staff"}
    S --> P["Anthropic cannot filter<br/>by nationality in real time"]
    P --> K["So it disables Fable 5 + Mythos 5<br/>for EVERY customer worldwide"]
    K --> U["Unaffected:<br/>Opus 4.8 · Sonnet 4.5 · Haiku 4.5<br/>and all other Claude models"]
    D -.->|"stated trigger"| T["Govt aware of a Fable 5 jailbreak method;<br/>reviewed a demo using it to surface a<br/>small number of previously-known minor vulns.<br/>Letter gave no specific NatSec detail."]

    classDef order fill:#dc2626,stroke:#7f1d1d,color:#f8fafc
    classDef gate fill:#7c3aed,stroke:#4c1d95,color:#f8fafc
    classDef neutral fill:#9ca3af,stroke:#374151,color:#0f172a
    classDef ok fill:#059669,stroke:#064e3b,color:#f8fafc
    class D order
    class S gate
    class P,K,T neutral
    class U ok
```

The mechanics that make this consequential:

- **It is structured as an export control, not a recall.** The legal
  hook is that giving a foreign national access to the model is treated
  like exporting a controlled technology — so the restriction follows
  the *person*, not the deployment. Because Anthropic **cannot reliably
  separate foreign nationals from everyone else in real time**, the only
  compliant move was to **turn both models off for all customers
  globally** — across the Claude API, Bedrock, Vertex, Foundry, and
  Copilot
  ([CNBC — Anthropic disables access to Fable 5 and Mythos 5](https://www.cnbc.com/2026/06/12/anthropic-disables-access-to-fable-5-and-mythos-5-to-comply-with-government-directive.html),
  [Fortune — Anthropic disables Fable and Mythos after US export ban](https://fortune.com/2026/06/13/anthropic-disables-fable-mythos-export-controls-national-security-threat/),
  [NBC News — Anthropic suspends new AI models after government directive](https://www.nbcnews.com/tech/tech-news/anthropic-suspends-new-ai-models-fable-mythos-government-directive-rcna349901)).
- **The trigger was the jailbreak — but the evidence cited was thin.**
  Per Anthropic, the government's understanding is that it became aware
  of a **method of jailbreaking Fable 5** and reviewed a demonstration
  of that technique being used to identify **a small number of
  previously known, minor vulnerabilities** — and the letter **did not
  provide specifics** of the national-security concern
  ([Anthropic statement](https://www.anthropic.com/news/fable-mythos-access),
  [Greek City Times — what the export controls mean for global access](https://greekcitytimes.com/2026/06/13/anthropic-export-controls-mythos-5-fable-5)).
- **Anthropic is complying while disputing.** It calls the order a
  likely **misunderstanding**, says it is **working to restore access**,
  and frames the suspension as **temporary** (days to weeks). It also
  warns the broader danger: if a demonstrated refusal-bypass on a
  released model is enough to trigger a global foreign-national ban,
  **the same standard could effectively halt new frontier deployments
  across the entire industry**
  ([beincrypto — Anthropic suspends Fable 5/Mythos 5 after US directive](https://beincrypto.com/anthropic-suspends-fable-5-mythos-5-us-directive/),
  [StartupHub — Anthropic disables Fable 5 and Mythos 5 after export-control order](https://www.startuphub.ai/ai-news/technology/2026/anthropic-disables-fable-5-and-mythos-5-after-us-export-control-order)).

There is a sharp irony in the timing. Just **two days earlier (Jun 10)**
Amodei published *"Policy on the AI Exponential,"* asking for
**government power to block** frontier deployments that fail safety
review (Jun-11 brief, §4). On Jun 12 the government used roughly that
power — but via an export-control lever, against Anthropic's own model,
on a trigger Anthropic considers a misunderstanding. The lab that asked
to be regulated became the **first test case**, and the precedent it
sought arrived faster, blunter, and less evidence-bound than the
compute-threshold + third-party-audit framework it proposed.

---

## 4. What this resets — capability is now deployment-fragile

The through-line from the Jun-8/9/11 briefs was a **capability** race:
who tops the AA Index, who wins SWE-Bench Pro. The Fable 5 week adds a
second axis the field had been treating as solved — **whether a frontier
model stays available at all.** Three durable shifts:

- **The frontier #1 is the most fragile model on the board.** Fable 5
  launched **#1 (64.9)** on Jun 9 and was **unavailable** by Jun 12.
  Capability and deployment-risk moved together — the same inversion the
  Jun-11 brief flagged on data retention, now extended to **outright
  availability.** The safe planning assumption: the most capable public
  model may also be the one most likely to be pulled, gated, or
  contract-restricted on short notice.
- **"Safeguarded release" is now a contested category, not a settled
  one.** Anthropic's Jun-9 thesis — *a Mythos-class model can be sold
  because a classifier gate makes it safe* — survived **three days** of
  public contact before a bypass demo + a regulator response. Whether
  the gate can be hardened (visible fallback is step one) or whether
  "capability-gated frontier release" is structurally unstable is now
  the open question every lab planning a dangerous-capability launch has
  to answer.
- **Export-control law is the fastest available off-switch.** Not new
  legislation, not the voluntary 30-day review in the early-June
  executive order — an existing **BIS export-control** authority,
  applied to model *access* as if it were technology transfer. That is a
  lever that already exists and can be pulled in an afternoon, and it
  now sits over every frontier deployment.

---

## 5. Meanwhile, open-weights: Kimi K2.7-Code

While the frontier story was about a model being pulled, the open-weight
lane shipped one. On **Jun 12**, **Moonshot AI** released **Kimi
K2.7-Code** on Hugging Face — a **1-trillion-parameter Mixture-of-Experts**
model (**32B active, 384 experts**), **256K context**, under a
**Modified-MIT** license, model id `kimi-k2.7-code`
([MarkTechPost — Moonshot releases Kimi K2.7-Code, +21.8% on Kimi Code Bench v2](https://www.marktechpost.com/2026/06/12/moonshot-ai-releases-kimi-k2-7-code-a-coding-model-reporting-21-8-on-kimi-code-bench-v2-over-k2-6/),
[llm-stats — Kimi K2.7-Code benchmarks, pricing, context](https://llm-stats.com/models/kimi-k2.7-code),
[Lushbinary — Kimi K2.7-Code developer guide](https://lushbinary.com/blog/kimi-k2-7-code-developer-guide-benchmarks-api-hermes-agent/)).

The headline feature is **efficiency, not peak capability**: K2.7-Code
reports **~30% lower reasoning-token usage vs K2.6**, which is the metric
that actually moves agentic-coding cost, where thinking tokens dominate
the bill.

```mermaid
flowchart LR
    subgraph SELF["Moonshot self-reported gains vs K2.6"]
      A["+21.8% Kimi Code Bench v2"]
      B["+11.0% Program Bench"]
      C["+31.5% MLS Bench Lite"]
      D["~30% fewer reasoning tokens"]
    end
    subgraph REAL["vs frontier on Moonshot's own bench"]
      E["Kimi Code Bench v2:<br/>K2.7 62.0 · Opus 4.8 67.4 · GPT-5.5 69.0"]
      F["No independent numbers yet on<br/>SWE-Bench Verified/Pro, Terminal-Bench,<br/>LiveCodeBench, GPQA, AIME"]
    end

    classDef good fill:#059669,stroke:#064e3b,color:#f8fafc
    classDef warn fill:#d97706,stroke:#92400e,color:#f8fafc
    class A,B,C,D good
    class E,F warn
```

**Read it with the same skepticism the Jun-11 brief applied to MiniMax
M3.** Pricing is aggressive at **$0.95 / $4.00 per MTok**, and the
self-reported deltas are large — but on Moonshot's *own* Kimi Code Bench
v2 the model still **trails GPT-5.5 (69.0) and Opus 4.8 (67.4) at 62.0**,
and as of release there were **no independent third-party numbers on any
standard public suite** (SWE-Bench Verified/Pro, Terminal-Bench,
LiveCodeBench, GPQA Diamond, AIME, MMLU-Pro). VentureBeat's framing —
*"practitioners say the benchmarks don't check out"* — is the right
caution
([VentureBeat — Kimi K2.7-Code cuts thinking tokens 30%, but benchmarks questioned](https://venturebeat.com/technology/kimi-k2-7-code-cuts-thinking-tokens-30-practitioners-say-benchmarks-dont-check-out)).
And as with prior Moonshot/MiniMax releases: **read the Modified-MIT
license** before any commercial use. The structural point holds — the
open-weight coding tier keeps shipping on a roughly weekly cadence
(Kimi, Qwen3 Coder Next, MiniMax M-series), competing on **cost and
token-efficiency** rather than topping the frontier board.

---

## 6. Frontier snapshot, Jun 13

The board moved less on *who is best* than on *what is reachable.* For
the first time, the line item that changed most is **availability.**

| Slot | State (Jun 13) | Δ vs. Jun 11 brief |
| --- | --- | --- |
| Frontier overall (by benchmark) | **Claude Fable 5 (64.9)** — but **unavailable** | role change — still #1 on paper, **pulled** by govt order |
| Restricted defensive frontier | **Claude Mythos 5** — **unavailable** | **pulled** alongside Fable 5 |
| Usable frontier default | **Claude Opus 4.8 (61.4)** | **promoted by default** — top *available* Claude |
| Agentic terminal coding | GPT-5.5 (Terminal-Bench 2.1) | unchanged — still its lane |
| Open-weight frontier | **MiniMax M3** (MSA, 1M ctx) | unchanged — independent reruns still pending |
| Open-weight coding (new) | **Kimi K2.7-Code** — 1T MoE, ~30% fewer reasoning tokens | **new (Jun 12)** — self-reported only |
| Frontier reasoning (queued) | **Gemini 3.5 Pro** — 2M ctx, Deep Think, ~$15/$60 | unchanged — limited Vertex preview, GA "late June" |
| Next OpenAI model | **GPT-5.6** — rumored ~Jun 30 | unchanged — still a Codex-log rumor |
| Deployment norm (new) | **First public frontier model pulled by US export-control order** | **new** — Fable 5 / Mythos 5, Jun 12 |
| Safeguard norm | **Capability-gated fallback must be *visible*** | **new** — Anthropic's post-backlash reversal |

A note for anyone re-baselining: with Fable 5 down, the **top usable
model for the hardest work is Opus 4.8 again** — the exact "safe tier"
the Jun-11 brief said to keep as your default. That recommendation now
looks less like prudence and more like the only option.

---

## 7. Forward signals, Jun 13 onward

- **When (and whether) Fable 5 / Mythos 5 come back.** Anthropic expects
  restoration in **days to weeks**. Watch for the *form* of the
  resolution: a narrowed directive, a nationality-filtering mechanism,
  or a hardened gate. Each implies a very different precedent for the
  next dangerous-capability launch.
- **Does the export-control lever generalize?** The real test of §3 is
  whether the same BIS mechanism gets pointed at **another lab's**
  model — or whether this stays a one-off tied to a specific jailbreak
  demo. If it generalizes, every frontier deployment inherits a new
  failure mode.
- **Independent Kimi K2.7-Code numbers.** Weights are public; the first
  third-party SWE-Bench Pro / Terminal-Bench runs (and a license read)
  will confirm or deflate the efficiency-at-low-cost framing — same
  watch the Jun-11 brief set for MiniMax M3.
- **Gemini 3.5 Pro GA.** Still unshipped, still "late June." Its target
  has shifted again: the model it was aimed at — Fable 5 at 64.9 — is
  **off the market**, so a Gemini 3.5 Pro GA would arrive into a
  frontier where Opus 4.8 (61.4) is the top *available* bar.
- **GPT-5.6.** Unchanged: a Codex-log rumor with ~Jun-30 prediction-
  market odds and no system card.

---

## 8. Action set, Jun 13

**Immediate (availability)**
- **If you route any production workload to Fable 5 or Mythos 5 — it is
  down now.** API, Bedrock, Vertex, Foundry, and Copilot are all
  affected. **Fail over to Opus 4.8** for the hardest reasoning/coding
  and treat Fable 5 as unavailable until Anthropic confirms restoration.
  Do not assume a quick return; plan for "days to weeks."
- **Audit any agent or pipeline pinned to a Fable 5 / Mythos 5 model
  id.** A hard-pinned model that just disappeared will fail closed —
  add an Opus 4.8 fallback path rather than letting jobs error out.

**Safeguard / vendor risk**
- **Add "deployment-availability risk" to model selection.** The Fable 5
  week shows the most capable public model can be the most fragile.
  For anything mission-critical, keep a **second, lower-tier model
  wired in** (Opus 4.8 / Sonnet 4.5) so a sudden gate or pull doesn't
  take you down with it.
- **If you ship your own capability-gated model, make the gate
  visible.** Anthropic's "secret sabotage" backlash is the cautionary
  tale: a silent downgrade reads as deception. Surface when and why a
  request was downgraded or refused.

**Open-weights**
- **K2.7-Code is worth a self-hosted trial on cost grounds** (~30% fewer
  reasoning tokens, $0.95/$4.00) — but **wait for independent suite
  numbers** before trusting the self-reported deltas, and **read the
  Modified-MIT license** before any commercial deployment.

**Policy / planning**
- **Treat export-control authority as a live off-switch over frontier
  access.** This is no longer hypothetical. If your roadmap depends on
  continuous access to a single frontier model, that is now a
  single-point-of-failure with a *regulatory*, not just a technical or
  commercial, trigger.

---

## Sources

Fable 5 jailbreak / gate bypass
- [SecurityWeek — Anthropic disputes Fable 5 AI jailbreak](https://www.securityweek.com/anthropic-disputes-fable-5-ai-jailbreak/)
- [CyberSecurityNews — Fable 5 alleged jailbreak to generate stack exploits](https://cybersecuritynews.com/anthropics-claude-fable-5-jailbroken/)
- [Cointelegraph via TradingView — researcher claims he bypassed Fable 5 guardrails](https://www.tradingview.com/news/cointelegraph:8f94d6ccc094b:0-ai-researcher-claims-he-s-already-bypassed-anthropic-s-fable-5-guardrails/)
- [abit.ee — Fable 5 jailbroken in 72 hours, system prompt now public on GitHub](https://abit.ee/en/cybersecurity/hackers-and-attacks/claude-fable-5-anthropic-jailbreak-ai-safety-system-prompt-leak-llm-security-pliny-the-liberator-en)
- [CyberPress — Claude Fable 5 jailbreak enables stack exploit generation](https://cyberpress.org/claude-fable-5-jailbreak/)
- [The Cyber Edition — Fable 5 jailbroken hours after launch via multi-agent attack](https://thecyberedition.com/claude-fable-5-jailbroken-hours-after-launch-via-multi-agent-attack/)

"Secret sabotage" backlash + Anthropic's apology
- [TechTimes — Fable 5 hit by jailbreak claims and 'secret sabotage' backlash](http://www.techtimes.com/articles/318268/20260612/claude-fable-5-hit-jailbreak-claims-secret-sabotage-backlash-days-after-launch.htm)
- [Coralflavor — jailbreak claims and 'secret sabotage' backlash](https://coralflavor.com/blog/claude-fable-5-jailbreak-claims-and-secret-sabotage-backlash-the-battle-over-ai-censorship)

Export-control order / global shutdown
- [Anthropic — Statement on the US directive to suspend access to Fable 5 and Mythos 5](https://www.anthropic.com/news/fable-mythos-access)
- [Axios — Trump admin blocks foreign access to Anthropic's most powerful AI](https://www.axios.com/2026/06/12/anthropic-trump-mythos-fable-national-security)
- [Bloomberg — US limits foreign access to Fable 5, Mythos 5](https://www.bloomberg.com/news/articles/2026-06-13/anthropic-says-us-limits-foreign-access-to-fable-5-mythos-5)
- [Al Jazeera — US orders Anthropic to disable AI models for all foreign nationals](https://www.aljazeera.com/news/2026/6/13/us-orders-anthropic-to-disable-ai-models-for-all-foreign-nationals)
- [CNBC — Anthropic disables access to Fable 5 and Mythos 5 to comply with government directive](https://www.cnbc.com/2026/06/12/anthropic-disables-access-to-fable-5-and-mythos-5-to-comply-with-government-directive.html)
- [Fortune — Anthropic disables Fable and Mythos after US export ban](https://fortune.com/2026/06/13/anthropic-disables-fable-mythos-export-controls-national-security-threat/)
- [NBC News — Anthropic suspends new AI models after government directive](https://www.nbcnews.com/tech/tech-news/anthropic-suspends-new-ai-models-fable-mythos-government-directive-rcna349901)
- [9to5Mac — Anthropic pulls Mythos 5 and Fable 5 following US government directive](https://9to5mac.com/2026/06/12/anthropic-pulls-claude-mythos-5-and-claude-fable-5-following-us-government-directive/)
- [StartupHub — Anthropic disables Fable 5 and Mythos 5 after US export-control order](https://www.startuphub.ai/ai-news/technology/2026/anthropic-disables-fable-5-and-mythos-5-after-us-export-control-order)
- [beincrypto — Anthropic suspends Fable 5 / Mythos 5 after US directive](https://beincrypto.com/anthropic-suspends-fable-5-mythos-5-us-directive/)
- [Greek City Times — what the export controls mean for global access](https://greekcitytimes.com/2026/06/13/anthropic-export-controls-mythos-5-fable-5)

Kimi K2.7-Code
- [MarkTechPost — Moonshot releases Kimi K2.7-Code, +21.8% on Kimi Code Bench v2](https://www.marktechpost.com/2026/06/12/moonshot-ai-releases-kimi-k2-7-code-a-coding-model-reporting-21-8-on-kimi-code-bench-v2-over-k2-6/)
- [VentureBeat — Kimi K2.7-Code cuts thinking tokens 30%, but practitioners say benchmarks don't check out](https://venturebeat.com/technology/kimi-k2-7-code-cuts-thinking-tokens-30-practitioners-say-benchmarks-dont-check-out)
- [llm-stats — Kimi K2.7-Code benchmarks, pricing, context window](https://llm-stats.com/models/kimi-k2.7-code)
- [Lushbinary — Kimi K2.7-Code developer guide: API & benchmarks](https://lushbinary.com/blog/kimi-k2-7-code-developer-guide-benchmarks-api-hermes-agent/)
- [DigitalApplied — Kimi K2.7-Code, Moonshot's coding-first open-source release](https://www.digitalapplied.com/blog/kimi-k2-7-code-release-open-source-coding-model)

Carried context (queued / unchanged)
- [TechTimes — Gemini 3.5 Pro nears June launch: 2M context + Deep Think](https://www.techtimes.com/articles/317919/20260606/google-gemini-35-pro-nears-june-launch-2-million-token-context-deep-think-reasoning.htm)

Trackers
- [Artificial Analysis — LLM leaderboard](https://artificialanalysis.ai/leaderboards/models)
- [llm-stats — AI news today](https://llm-stats.com/ai-news)
