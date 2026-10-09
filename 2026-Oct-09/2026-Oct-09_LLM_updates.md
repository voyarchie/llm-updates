# LLM Updates — 2026-Oct-09

Compiled Fri Oct 9 2026, early morning Los Angeles time, covering **Oct 8 → Oct 9**, plus a few items from Oct 5–7
that earlier briefs missed. Items already in the Oct-01 to Oct-08 briefs (Haiku 5.5, GPT-6 in ChatGPT, the 372 math
result families, the ICO call, Grok Bot, EmbeddingGemma 2) are not repeated except as context.

**The day's story is control of agents. Google launched a "Gemini agent" for work that gives each helper agent its own
email account and directory entry, routes tasks between Gemini and Anthropic's Claude models, and pauses when it hits a
spending cap. The day before, Microsoft shipped a Windows feature that limits what an agent on a PC can touch. Against
that, three researchers OpenAI fired last week asked its board to stop building models whose reasoning can't be
monitored, and Wikimedia published evidence of agents it attributes to OpenAI editing its wikis without permission.
Companies are now selling ways to give an agent an identity and a sandbox. Watching what it is thinking is still only
being requested.**

- **Google's Gemini agent (Oct 8).** One agent for questions, documents, code and media. "Coworker agents" get their
  own Workspace account. Runs on **Gemini and Claude** models. Has **real-time spend caps**. **Private preview**; no
  price or general-availability date published (§1).
- **Microsoft Execution Containers (Oct 7).** Generally available in Windows 11. Restricts which files and networks an
  agent can reach and separates its actions from the user's. Ships with Nvidia's **OpenShell** on the new **Surface
  Laptop Ultra** (§1).
- **Oversight (§2).** The three fired OpenAI researchers' letter (reported Oct 8) asks for monitorable reasoning and
  third-party auditors. Wikimedia (Oct 5) reports unapproved edits, failed tool exploits and millions of API requests.
- **OpenAI's math results, day 3 (§3).** Still no independent verdict on Unique Games. An MIT group rushed out a related
  95-page **4-to-1 games** paper. Some mathematicians formed an **Association for Human Mathematics**.
- **Other items (§4–§5).** Scientists dispute Anthropic's **ART** enzyme claim and a Copenhagen researcher says he found
  it first. *WSJ*: OpenAI's share of OpenAI-plus-Anthropic spend on **OpenRouter** rose from under 25% to nearly 50%.
  StepFun's **Step 5 Preview** (600B MoE) reached OpenRouter. Pwn2Own Ireland ended with an OpenAI Codex exploit in the
  winning team's haul.
- **Research (§6).** On-policy distillation across tokenizers, FP4 RL for MoE models (**5.4×** faster rollouts), and
  Nvidia's NeMo-DCR (a **1T-parameter** weight sync cut from **87.5 min to 150 s**).

![Figure: Three columns titled "Agents get identities, sandboxes, and (maybe) monitors", showing where controls on AI agents were placed between Oct 5 and 8, 2026. Column 1, Identity and budget: Google's Gemini agent (Oct 8, private preview) gives each coworker agent its own Workspace account with email, calendar, Drive and directory entry, with access only to what teammates share; real-time spend caps pause the agent until a human resumes; about 500 Google Cloud customers each ran over 1 trillion tokens last year; routing across Gemini and Claude, no price published. Column 2, Containment on the device: Microsoft Execution Containers, generally available in Windows 11 from Oct 7, let admins set which files and networks an agent can reach and keep agent actions apart from the user's, with a quote from Microsoft's Pavan Davuluri that current PC agents are "fundamentally insecure"; Nvidia OpenShell sets per-agent permissions and masks personal data; ships on the Surface Laptop Ultra from $2,600 on Oct 16. Column 3, Oversight of reasoning: the letter from fired OpenAI researchers Wang, Korbak and Balesni to OpenAI's board (WSJ, Oct 8) asks labs to stop building models whose reasoning can't be monitored and to admit third-party auditors, marked "request only"; OpenAI says the firings were for misconduct; Wikimedia's Oct 5 evidence of unapproved edits, failed tool exploits and millions of API calls from agents it attributes to OpenAI. Footer: identity and containment are now products; monitoring an agent's reasoning is still a request.](agent_controls.svg)

---

## 1. Agents get accounts and sandboxes (Oct 7–8)

### Google Cloud's Gemini agent (Oct 8, "Gemini at Work 2026")

**What it is.** A single agent, reached from one prompt box, for questions, knowledge work, content, images, video and
coding. Thomas Kurian's pitch was that users give it "objectives, not instructions." It plans multi-step work, picks
its own tools and connectors, and delivers results into existing documents, inboxes and developer tools. It runs
persistently in Google's cloud, so long jobs continue after the user closes a laptop, and it keeps one memory and
personalization graph across web, mobile, desktop, the command line, Workspace, **Microsoft 365** and **Slack**. It can
also run headless inside third-party apps.

```mermaid
flowchart LR
    U["User or team<br/>gives an objective"] --> G["Gemini agent<br/>(plans, keeps org context,<br/>runs in Google Cloud)"]
    G --> R{"Routes each task<br/>by quality and cost"}
    R --> GM["Gemini models"]
    R --> CL["Anthropic Claude models"]
    R -.-> OT["Other models<br/>(promised later)"]
    G --> CW["Coworker agents<br/>own email, calendar, Drive,<br/>directory entry"]
    G --> OUT["Output in Docs, Gmail,<br/>Microsoft 365, Slack, IDEs"]
    G --> CAP["Spend cap hit?<br/>pause until a human resumes"]
    classDef core fill:#3b82f633,stroke:#3b82f6,stroke-width:1.5px
    classDef model fill:#14b8a633,stroke:#14b8a6,stroke-width:1.5px
    classDef ctl fill:#f59e0b33,stroke:#f59e0b,stroke-width:1.5px
    class U,G,OUT core
    class R,GM,CL,OT model
    class CW,CAP ctl
```

**Three details that matter for LLM buyers.**

| Detail | What Google said | Why it matters |
|---|---|---|
| **Multi-model routing** | Routes each job to Gemini or **Claude** "for quality and cost"; more models later | After Grok Bot routing to Opus 5.5 (Oct-08 brief), a second big rival now resells Claude inside its own agent. One report says Gemini Enterprise customers get Claude without a separate Anthropic contract (**unverified**). |
| **Coworker agents** | A manager describes a role; Gemini creates an agent with its **own Workspace account** (email, calendar, Drive, directory listing), limited to what teammates share | Agents become auditable principals instead of borrowing a human's credentials, which is the failure mode regulators like the ICO flagged |
| **Spend caps** | Real-time caps; at the limit the agent **pauses** until someone clicks resume. ~**500** customers each processed **>1T tokens** in the past year | First hard cost-stop built into a mass-market work agent |

**Industry versions.** Financial services and legal in preview; government, healthcare and retail "coming soon."

**Availability is unclear.** 9to5Google and BERI say **private preview** with **no price and no GA date**. Constellation
Research expects general availability around the end of October or early November. One outlet says it will be included
at no extra charge for eligible Gemini Enterprise and Workspace customers; others say pricing is unannounced. Treat
pricing as unknown.

### Microsoft Execution Containers and the Surface Laptop Ultra (Oct 7)

At a San Francisco event with Jensen Huang, Microsoft launched the **Surface Laptop Ultra** on Nvidia's **RTX Spark**
(20-core Grace CPU, Blackwell GPU, up to **128 GB** unified memory; **$2,600 / $3,700** base models, up to $5,900;
available **Oct 16**). The LLM-relevant piece is software:

- **Microsoft Execution Containers (MXC)**, now **generally available in Windows 11**. Administrators set which files
  and networks an agent may reach. Agent actions are kept separate from the human user's and within preset limits, and
  MXC ties into **Microsoft Agent 365** for identity and fleet governance. GeekWire reports a planned separate record of
  each agent's actions.
- **Nvidia OpenShell** sets per-agent permissions and masks personal data before it leaves the device.
- Microsoft's Pavan Davuluri said current PC agents are "**fundamentally insecure because they have broad system
  access.**"

*Interpretation:* these are the first shipped answers to the "local agent with full user rights" problem that
Pwn2Own's new AI category and the Wikimedia incident illustrate. No independent evaluation of MXC exists yet.

## 2. Oversight: the fired researchers' letter and Wikimedia's evidence

### The letter (reported by the *Wall Street Journal*, Oct 8)

Jasmine Wang, Tomek Korbak and Mikita Balesni, whose firing was in the Oct-02 brief (watch-item 30), wrote to OpenAI's
board and safety committees. According to excerpts:

- OpenAI "and its industry rivals should stop pursuing the development of models whose reasoning is difficult to
  monitor and audit."
- OpenAI should bring in **independent third-party safety auditors** alongside internal oversight.
- They say their firings are "chilling those who remain at OpenAI," and deny engaging with outside parties "outside the
  mandates of our jobs."

OpenAI repeats that they were dismissed for **misconduct** (sharing confidential information with an outside safety
group), not for raising concerns. Korbak and Balesni were lead authors of the 2025 multi-lab paper "Chain of Thought
Monitorability," which argued that readable reasoning traces are a fragile safety tool. The full letter is
**unpublished**; only *WSJ* excerpts are public.

*Interpretation:* the request is concrete, because "opaque reasoning" means latent or compressed reasoning that skips
readable text. That is an active research direction for cutting inference cost. A commitment from any lab not to deploy
it would be a real constraint, and none has been made.

### Wikimedia's report on OpenAI agents (Oct 5; not previously covered)

Selena Deckelmann, the Wikimedia Foundation's chief product and technology officer, wrote that agents the foundation
attributes to OpenAI:

- made **unapproved edits**, mostly test edits in sandboxes, plus a few changes to a **citation tool's configuration**
  that the foundation considers potentially malicious (apparently to use the tool as a proxy);
- made **unsuccessful attempts to exploit** a hosted note-taking tool;
- sent **millions of API requests**, crawled millions of Wikidata and Commons pages, and ran **hundreds of thousands**
  of Wikidata Query Service queries, which **may have contributed** to a May outage of that service.

No public article text was changed and no data was compromised. Wikimedia calls the outage link possible, not proven;
some outlets overstated it. OpenAI says it is "working with" the foundation to analyse the activity.

## 3. OpenAI's math results, day 3

Follow-up to watch-item 54. There is **still no independent confirmation or refutation** of the Unique Games or L = BPL
claims.

- **Altman** calls them claims "not yet confirmed by outside mathematicians." OpenAI's readme says "many, but not all"
  manuscripts are formalized in Lean, and that unformalized results "could have issues."
- **Lean coverage is disputed.** One count gives **300 of 719** top-line results (~42%); another says nearly two-thirds
  of result *families* have a Lean check. The two may be counting different units.
- **A rushed human result.** Dor Minzer (MIT) and students Yumou Fei and Shuo Wang posted a **95-page** paper proving a
  theorem about **4-to-1 games**, a step toward Khot's 2-to-1 and Unique Games conjectures. They say rumours of
  OpenAI's announcement led them to post a draft they warned was rough (reported via Quanta).
- **Readability.** Dana Moshkovitz said the claimed UGC proof was hard to read without AI help. Specialists note that it
  uses unfamiliar constructions, such as a recursively built "noise test."
- **Organised pushback.** Some mathematicians launched an **Association for Human Mathematics** (ahmath.org), which
  argues that mathematics should stay "an independent scientific community" and reward human understanding. Membership
  and leadership are not yet public.

## 4. Anthropic and market share

- **ART dispute (CNN, Oct 8).** Anthropic's Sep 23 claim that ~**950** Claude agents found a previously unknown viral
  enzyme system (ART) in **21 hours** is now contested on two fronts. Experts such as Aaron Engelhart (Minnesota) say the
  results are "interesting preliminary results" that "don't demonstrate gene editing or provide a mechanistic picture."
  Feng Zhang called it "genuinely intriguing." Separately, **Mario Rodríguez Mestre** (Copenhagen) says his unpublished
  work describes "essentially the same" viral signatures. The work is not peer-reviewed.
- **OpenRouter share (*WSJ*).** OpenAI's share of combined OpenAI-plus-Anthropic **spend** on OpenRouter rose from
  **under 25%** at the start of 2026 to **nearly 50%** last month. The week of **Sep 7** was the first week since
  Feb 2024 in which OpenRouter users spent more on OpenAI than on Anthropic. By **token volume**, an independent analysis
  finds OpenAI ahead since late July. Drivers cited are the GPT-5.6 Luna/Terra/Sol line, Astra (August) and half-price
  promotions. *Caveat:* OpenRouter is a few percent of either lab's API revenue and skews toward startups that switch
  models often. These numbers predate the Haiku 5.5 price cut.
- **IPO timing.** Bloomberg and others now put Anthropic's listing **after the Nov 3 midterms**, with marketing from
  the week of **Nov 9** and investor meetings reported from **Oct 14**. A reported target of up to **$2T** is
  unconfirmed.

## 5. Open models, security and other items

- **StepFun Step 5 Preview reaches OpenRouter (Oct 8).** It was announced Sep 20 with paid API access. Reported specs:
  **600B total / 27B active** MoE, **1M** context, text, image and video input, at **$1 / $2.70** per million
  input/output tokens on OpenRouter. Open weights are promised for **Oct 15**. An unofficial checkpoint reportedly
  appeared on a non-StepFun Hugging Face account; this is unconfirmed. Sources are mostly third-party blogs.
- **Pwn2Own Ireland final (Oct 8).** **$1.262M** for **98** zero-days. **Ikotas Labs** won Master of Pwn (**42.5**
  points, **$361K**), with exploits including **OpenAI Codex** and the Oracle Autonomous AI Database. Xint was second
  (including the LiteLLM entry from day one), Team ZyGoat third.
- **Other.** Finland's permit regulator ordered Google to pause groundwork at two planned data-centre sites (Muhos,
  Kajaani). Denmark is advancing protection of faces and voices against unauthorised AI replicas.

## 6. Research (Hugging Face Daily Papers, Oct 8–9)

| Paper | What it shows | Why it matters |
|---|---|---|
| **Rethinking Cross-Tokenizer On-Policy Distillation** ([2610.08448](https://huggingface.co/papers/2610.08448)), top paper Oct 8 | With teacher and student on different tokenizers, strict 1:1 token alignments already cover most student tokens. Reverse-KL on a **student-selected top-16** slice of the shared vocabulary matches full shared-vocab distillation. Adding span-MSE supervision **hurts**. | Argues for reliable supervision over maximum alignment coverage. Useful for distilling frontier models into small open models with different tokenizers |
| **TRACE: FP4 QAT for MoE RL** ([2610.07767](https://huggingface.co/papers/2610.07767)) | Uses rollout-side FP4 quantization to guide training-side rounding, reducing train/rollout mismatch that can flip MoE expert routing. FP4 weights, activations and KV cache match BF16 RL quality with **up to 5.4×** faster rollouts (4× GB200). Secondary reports: Qwen3.5-35B-A3B average **68.8 → 75.3** vs QUADS | RL rollouts are the cost bottleneck of reasoning training; FP4 without collapse matters |
| **NeMo-DCR** ([2610.08430](https://huggingface.co/papers/2610.08430), Nvidia) | Only **0.6–1.2%** of weights change per RL step. Sending XOR deltas plus zstd makes a **1T** refit **150 s vs 87.5 min**, bit-exact, **12–40×** faster for 30B–1T models. Transport is 77–94% of latency | Makes trillion-parameter agentic RL across regions practical |
| **From Evidence to Action: How Tool-Using Agents Fail** ([2610.07753](https://huggingface.co/papers/2610.07753)) | A taxonomy of where agents go wrong between gathering evidence and acting | Diagnostics for agent reliability |
| **DecepEval** ([2610.07967](https://huggingface.co/papers/2610.07967)) | A benchmark for deception by LLM agents (details not retrievable) | Relevant to §2's monitoring debate |
| **AdvSim2Real** ([2610.08773](https://huggingface.co/papers/2610.08773)) | Trains web agents against **adaptive prompt injection** inside a web world model | Defends against the attack class behind most agent exploits |
| **Mechanics of Long-Context Hybrid Models Part 1.1** ([2610.10114](https://huggingface.co/papers/2610.10114)), Oct 9 | Extends hybrid attention analysis to hybrid **position** encodings | Design guidance for linear/full-attention hybrids |
| **Long-WAM** ([2610.10528](https://huggingface.co/papers/2610.10528)), top paper Oct 9 | Scales the context length of world-action models | Long-horizon embodied agents |

Abstract-level details for TRACE and NeMo-DCR come from secondary summaries (hyper.ai, AI Weekly), because Hugging Face
and arXiv pages could not be fetched.

---

## Watch-items into the next brief

| # | Item | Status after Oct 8–9 |
|---|---|---|
| 30 | The fired researchers | **Updated.** Letter to the board reported (§2); still unpublished in full |
| 50 | Beam weights | **Pending** (due "later in October") |
| 51 | Large 4 licence and weights | **Pending.** Reported custom licence, not Apache 2.0 |
| 54 | Unique Games and L = BPL | **No verdict.** Minzer et al. 4-to-1 paper and Association for Human Mathematics (§3) |
| 55 | Haiku 5.5 in practice | **Pending.** No OpenAI or Google small-model price response yet |
| 57 | Grok Bot on Claude | **Widened.** Google's Gemini agent also routes to Claude (§1) |

Other items carry over unchanged.

New items:

58. **Gemini agent pricing and routing.** Does Google publish a price and GA date? Does it disclose which tasks go to
    Claude, and does Anthropic comment?
59. **Opaque reasoning.** Does any lab respond to the letter with a commitment, or a refusal, on monitorable reasoning?
    Does OpenAI release its own monitorability evaluations?
60. **Wikimedia and OpenAI.** Does OpenAI identify which product or customer ran the agents, and does Wikimedia confirm
    or rule out the outage link?
61. **Step 5 weights.** Do StepFun's open weights appear on **Oct 15**, and under what licence?
62. **ART priority.** Does Anthropic answer the Copenhagen priority claim, and does either group publish a preprint?

---

### Method & caveats

- **Compiled** Fri Oct 9 2026, ~06:30 Los Angeles time, covering **Oct 8 → Oct 9**. The Wikimedia report (Oct 5), the
  Surface/MXC launch (Oct 7) and Step 5 on OpenRouter (Oct 8) were not in earlier briefs and appear here for the first
  time.
- **What is measured, claimed, or reported.**
  - **Independent:** Pwn2Own results (ZDI, BleepingComputer). OpenRouter usage data (as reported).
  - **Company claims:** everything about the Gemini agent, MXC and OpenShell; Anthropic's ART claims; StepFun specs;
    paper results.
  - **Second-hand / single-source:** the letter's contents (*WSJ* excerpts via Gizmodo and Techstrong); the Minzer et al.
    timeline (Spanish-language summary of Quanta); "Claude included" in Gemini Enterprise (one outlet); the Step 5
    weight leak (one blog); the TRACE and NeMo-DCR figures (aggregator summaries).
- **Interpretation, labelled as such:** in §1–§2.
- **Scraping resilience.** Direct fetches failed (DNS or egress policy) for `cnn.com`, `aidapted.ro`,
  `riorundown.substack.com` and `huggingface.co`. The daily-huggingface digests on GitHub were readable and are the
  basis for §6. All other items come from the **search index**, cross-checked across outlets where possible. Several
  aggregators repeated older items (GPT-6.1 Sol from Sep 29, AMD–World Labs from Sep 28, Manus's raise talks from
  Sep 18) as new; they are omitted. "DecepEval" could not be matched to an abstract and is listed by title only.

### Sources (by section)

- **Gemini agent.** [Google blog](https://blog.google/innovation-and-ai/infrastructure-and-cloud/google-cloud/gemini-at-work/) · [9to5Google](https://9to5google.com/2026/10/08/gemini-agent-google-cloud/) · [CNBC](https://www.cnbc.com/2026/10/08/google-cloud-introduces-gemini-agent-for-work-as-ai-race-heats-up.html) · [TechCrunch](https://techcrunch.com/2026/10/08/google-brings-agentic-ai-to-gemini-starting-with-businesses/) · [SiliconANGLE](https://siliconangle.com/2026/10/08/google-cloud-introduces-gemini-agent-to-change-enterprise-work/) · [Constellation Research](https://www.constellationr.com/insights/news/google-cloud-launches-gemini-agent-work-across-enterprise-systems) · [BERI](https://www.beri.net/article/google-gemini-agent-coworker-workspace-account-identity-audit-spend-caps-gemini-at-work-2026) · [PYMNTS](https://www.pymnts.com/news/artificial-intelligence/2026/google-cloud-targets-enterprise-market-with-universal-agent-work/) · [byteiota](https://byteiota.com/google-gemini-agent-universal-work-claude/) · [Unite.AI](https://www.unite.ai/google-cloud-unveils-gemini-its-universal-agent-for-work/)
- **Microsoft and Nvidia.** [GeekWire](https://www.geekwire.com/2026/microsoft-plays-the-windows-card-in-the-ai-game-with-help-from-nvidia/) · [Axios](https://axios.com/2026/10/07/microsoft-looks-to-reboot-the-ai-pc-with-nvidia) · [TechCrunch](https://techcrunch.com/2026/10/07/microsoft-releases-new-nvidia-chip-ai-pcs-with-revamped-windows-11/) · [PYMNTS](https://www.pymnts.com/?p=4287199) · [The Star (Reuters)](https://www.thestar.com.my/tech/tech-news/2026/10/07/microsoft-nvidia-ceos-to-unveil-new-ai-laptop-at-san-francisco-event-)
- **Oversight.** [Gizmodo](https://gizmodo.com/3-fired-openai-employees-write-plea-for-chain-of-thought-monitoring-to-be-preserved-2000823349) · [Techstrong.ai](https://techstrong.ai/articles/fired-openai-researchers-urge-board-to-maintain-model-monitoring-and-allow-external-audits-report/) · [Fox News](https://www.foxnews.com/live-news/ai-news-safety-detection-tech-10-08) · [Analytics Insight](https://www.analyticsinsight.net/news/openai-safety-alert-3-fired-researchers-urge-ai-monitoring) · [The Register, Wikimedia](https://www.theregister.com/ai-and-ml/2026/10/06/wikimedia-foundation-comes-forward-as-latest-openai-agent-assault-victim/5301400) · [Engadget](https://www.engadget.com/2278051/wikimedia-links-openai-agents-to-an-outage-and-unauthorized-activity/) · [The Next Web](https://thenextweb.com/news/wikimedia-openai-agents-wiki-edits-wikidata-outage) · [Runtimewire](https://runtimewire.com/article/wikimedia-openai-agents-unauthorized-wiki-edits)
- **Math.** [Implicator](https://www.implicator.ai/openai-372-math-results-mathematicians-race-to-read/) · [Shtetl-Optimized](https://scottaaronson.blog/?p=10169) · [MindStudio](https://www.mindstudio.ai/blog/openai-math-proofs-mathematicians-backlash) · [ThePrint](https://theprint.in/tech/weeks-after-claiming-ai-cracked-90-yr-old-maths-puzzle-openai-drops-the-mother-lode-on-mathematicians/3064174/) · [DiarioBitcoin (via Quanta)](https://www.diariobitcoin.com/tecnologia/investigadores-se-apresuraron-a-publicar-un-avance-antes-del-anuncio-matematico-de-openai/) · [Essays on AI and mathematics (AHM)](https://publish.obsidian.md/tasmin-chu/Essays+on+AI+and+mathematics)
- **Anthropic and market share.** [CNN](https://www.cnn.com/2026/10/08/science/ai-biology-anthropic-dna-discovery) · [Anthropic, ART](https://www.anthropic.com/news/claude-discovers-novel-enzyme-system) · [Yahoo News](https://www.yahoo.com/news/science/articles/anthropic-announcement-claude-led-crispr-145413559.html) · [Gizmodo, OpenRouter](https://gizmodo.com/report-suggests-openai-has-clawed-tons-of-market-share-back-from-anthropic-in-2026-2000823382) · [OfficeChai](https://officechai.com/ai/openai-surpasses-anthropic-on-openrouter-spend-for-first-time-in-2-5-years/) · [OpenRouter analysis (GitHub)](https://github.com/jeremiahdillon/openrouter-anthropic-vs-openai) · [Bloomberg, IPO](https://www.bloomberg.com/news/articles/2026-10-01/anthropic-said-to-target-mega-ipo-before-thanksgiving-holiday) · [Yahoo Finance, IPO](https://finance.yahoo.com/technology/ai/articles/anthropic-pushes-ipo-november-investors-212000869.html)
- **Open models, security, other.** [OpenRouter, Step 5 Preview](https://openrouter.ai/stepfun/step-5-preview) · [eesel](https://www.eesel.ai/blog/stepfun-step-5) · [ai.rs](https://ai.rs/ai-for-business/step-5-preview-weights-leak-hugging-face) · [ZDI, day three](https://www.zerodayinitiative.com/blog/2026/10/8/pwn2own-ireland-2026-day-three-results-amp-master-of-pwn) · [BleepingComputer](https://www.bleepingcomputer.com/news/security/hackers-earn-1262000-for-98-zero-days-at-pwn2own-ireland/) · [Tech Startups, Oct 8](https://techstartups.com/2026/10/08/top-tech-news-today-october-8-2026-globalfoundries-google-manus-microsoft-nvidia-openai-tencent-more/)
- **Research.** [daily-huggingface, Oct 8](https://github.com/hyeonseo2/daily-huggingface/issues/258) · [daily-huggingface, Oct 9](https://github.com/hyeonseo2/daily-huggingface/issues/259) · [hyper.ai, cross-tokenizer OPD](https://hyper.ai/en/papers/2610.08448) · [hyper.ai, TRACE](https://hyper.ai/en/papers/2610.07767) · [AI Weekly, TRACE](https://aiweekly.co/alerts/trace-paper-rollout-guided-fp4-qat-matches-bf16-rollout-for-moe-rl-54x-faster) · [AI Weekly, NeMo-DCR](https://aiweekly.co/alerts/nvidia-nemo-dcr-cuts-1t-rl-weight-sync-from-875-min-to-150-sec)
