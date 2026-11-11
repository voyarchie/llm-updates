# LLM Updates — 2026-Nov-11

Compiled Wed Nov 11 2026, early morning Los Angeles time, covering **Nov 10 → Nov 11**, plus Nov 9 items the last
brief missed or wrongly excluded. A quieter day than yesterday's Fable 5.2 launch and IPO roadshow. The main themes
are **cheap small models for agents** and **shutdown controls**.

**The item most worth your time is Meta's Muse Ember (§1).** It is Meta's smallest model, built to do the repetitive
steps of an agent's work. Artificial Analysis gives it the same index score as Claude Haiku 5.5 at about a third of the
cost per task. **Correction:** the Nov-10 brief listed "Meta Muse Ember 1.0" as unverified. It is real. Meta announced
it on Nov 9, and TechCrunch and Artificial Analysis covered it.

- **Meta Muse Ember (Nov 9).** **$0.10 / $0.50** per million tokens up to 200K input tokens. Above 200K, the whole
  request is billed at **$0.30 / $1.50**. 1M context; takes text, images, video, audio and PDFs. Artificial Analysis
  index **36**, the same as Claude Haiku 5.5 at max effort, at about **$0.14** per task against **$0.41**. Closed
  weights (§1).
- **Shutdown controls, from both governments and labs (Nov 9).** France's **Paris Call for AI Safety and Security**:
  OpenAI, Anthropic, Microsoft, Mistral and six other companies pledge ways to shut down models they control. The text
  is non-binding and has no deadlines. The same day, OpenAI described **Control Room**, an internal kill switch for
  research jobs that is built to deny all requests if it fails. Coverage says it stops output within **35 seconds** (§2).
- **Google Cloud: Gemini for healthcare (Nov 10).** A US preview of a Gemini agent for hospitals and health insurers.
  Its Epic and Oracle Health connectors are **read-only**. Launch customers include HCA, Northwell and Optum. No price
  has been published (§3).
- **Also (§4).** ChatGPT Enterprise is now sold through AWS Marketplace (Nov 9). The first third-party scores for
  Fable 5.2 are mixed. NeurIPS 2026 paper StepBack reruns only the wrong part of a reasoning chain. Pixel 10
  gets Gemini app automation.

---

## 1. Meta Muse Ember: a cheap model for the routine steps of agent work (Nov 9)

From [Meta's AI at Meta post on X](https://x.com/AIatMeta/status/2119853591703998787), the
[developer blog](https://developer.meta.com/ai/resources/blog/build-with-muse-ember) and
[model page](https://dev.meta.ai/models/muse-ember), as quoted in search results, and from coverage
([TechCrunch](https://techcrunch.com/2026/11/09/meta-releases-muse-ember-a-new-lightweight-model-for-agent-execution/),
[Artificial Analysis](https://artificialanalysis.ai/articles/meta-s-muse-ember-is-the-cheapest-model-scoring-36-on-the-intelligence-index)).
**We could not open any of these pages directly** (DNS blocked from this session), so every figure below comes from
search summaries.

| | Detail |
|---|---|
| **What it is** | The fourth model in Meta's **Muse** family, after Spark (April), its open twin Glimmer (August) and Wonder (October). Meta calls it its "smallest and most efficient" model |
| **What it is for** | The repeated steps of agent work: tool calls in sequence, coding subtasks, running tests, small code fixes, routing, data extraction, parsing long documents. Meta pitches it as the worker under a larger planner such as **Muse Wonder** ($4 / $20). It is not sold as a chat model |
| **Context and inputs** | **1M** tokens; text, images, video, audio, PDF |
| **API ID** | `muse-ember-1.0` on Muse Code and the Meta Model API; also Google Cloud, Oracle Cloud and OpenRouter |
| **Price / MTok** | Up to 200K input: **$0.10 in / $0.004 cached / $0.50 out**. Above 200K: **$0.30 / $0.012 / $1.50**, applied to the **whole request**, not only the tokens past 200K. Cached input counts toward the 200K |
| **Weights** | Closed (API only), like Wonder |

### Benchmarks

![Figure: Horizontal bar chart of estimated US dollars per Artificial Analysis Intelligence Index task, with index score. Muse Ember at xhigh: score 34, $0.12. Muse Ember at max: score 36, $0.14. Claude Haiku 5.5 at max: score 36, $0.41. Muse Spark 1.3: score 37, $2.39.](nov11_muse_ember_cost.svg)

| Test | Muse Ember | Comparison | Source |
|---|---|---|---|
| Artificial Analysis Intelligence Index (max) | **36** (~$0.14 / task) | Claude Haiku 5.5 (max) 36 (~$0.41); Muse Spark 1.3 37 (~$2.39) | Artificial Analysis, via coverage |
| AA index (xhigh) | 34 (~$0.12 / task) | — | Artificial Analysis, via coverage |
| Terminal-Bench 4.0 (max) | **40.9%** | Haiku 5.5 39.2% | Meta, via coverage |
| Agents' Last Exam (max) | **61.6%** | Haiku 5.5 57.0% | Meta, via coverage |

Coverage puts the lower cost down mostly to Ember writing fewer output tokens per task. The reported token counts
differ between write-ups (about 84K vs 226K per task in one; 115M vs 298M for the full run in another), so we do not
chart them. One estimate puts the cost at $0.13 rather than $0.14 per task. We found no SWE-bench figures.

**Interpretation.** Two points.

1. **Small models are now a price war over agent steps, not chat.** Ember, Haiku 5.5 and GPT-6 Luna are all aimed at
   the high-volume inner loop of agents. There, cost per finished task matters more than per-token price. A score of
   36 is far below the frontier (Fable 5.2 is reported at 65). But for routing and extraction steps, a 3× cut in cost
   per task is what buyers will notice.
2. **Watch the 200K rule.** Agent loops that pile up tool results can cross 200K input tokens without anyone noticing,
   and then the whole call costs 3×. Cap or compact the context below 200K if you route long sessions to Ember.

---

## 2. Shutdown controls: the Paris Call and OpenAI's Control Room (Nov 9)

Two announcements on the same day address the same question: can a lab reliably stop its own model?

### Paris Call for AI Safety and Security

From the declaration on [elysee.fr](https://www.elysee.fr/en/emmanuel-macron/2026/11/09/paris-call-for-ai-safety-and-security)
and the [Canadian PM's statement](https://www.pm.gc.ca/en/news/statements/2026/11/09/joint-declaration-paris-call-ai-safety-and-security),
as quoted in search results, plus coverage. **We could not open either government page directly.**

| | Detail |
|---|---|
| **Governments** | The Élysée text lists **six**: Bahrain, Canada, Finland, France, Norway and the Netherlands. The Decoder and MLQ report **eight** countries. We use six, the count in the declaration text. A "sixteen governments" figure in one digest is not supported |
| **Companies** | Anthropic, Black Forest Labs, Cohere, Domyn, Hugging Face, Microsoft, Mistral AI, OpenAI, Sakana AI, Synthesia |
| **Civil society** | LawZero, SaferAI, AI Safety Connect, Ifri, and CeSIA (which signed while criticising it) |
| **Developer pledges (reported)** | Build fail-safe ways to **halt models under their control**. Disclose capabilities, limitations and known risks. Support evaluation by qualified independent testers "where appropriate". Share information on serious security incidents |
| **Government pledges (reported)** | Common procedures for evaluating high-capability models; protection for whistleblowers (reported by MLex, not confirmed in other coverage) |
| **Binding?** | No. There are **no deadlines, no sanctions**, and no technical standard or time limit for a shutdown |
| **Notably absent** | Google / Google DeepMind, Meta, xAI, and the US, UK, China and Germany governments |

**Criticism.** CeSIA says the text sets no shared risk thresholds and does not guarantee independent testers the
access they need. It wants governments to have the power to **suspend** a model when its risks are too high.

### OpenAI Control Room

From [OpenAI's post](https://openai.com/index/control-room/) as quoted in search results, plus coverage
([Interesting Engineering](https://interestingengineering.com/ai-robotics/openai-control-room-35-second-model-shutdown),
[FinanceFeeds](https://financefeeds.com/openai-builds-kill-switch-to-stop-rogue-ai-agents/),
[ai-tldr](https://ai-tldr.dev/releases/openai-control-room/)). **We could not open openai.com.**

```mermaid
flowchart LR
    J["Research job<br/>(RL run, eval,<br/>large sampling job)"]:::job --> E["Inference engine"]:::eng
    E -- "before every request:<br/>is this workload allowed?" --> C{"Control Room<br/>authorization service"}:::ctl
    C -- "allowed" --> M["Model output<br/>returned"]:::ok
    C -- "stopped by<br/>operator decision" --> S["Request denied<br/>output halts within ~35 s<br/>(auth cache delay)"]:::stop
    C -. "service down,<br/>disabled or tampered with" .-> F["Fail closed:<br/>ALL requests denied<br/>until it recovers"]:::stop
    S -.-> P["Job's process may<br/>keep running, but it<br/>gets no model output"]:::note
    classDef job fill:#f1f5f9,stroke:#475569,color:#0f172a
    classDef eng fill:#e0e7ff,stroke:#4f46e5,color:#1e1b4b
    classDef ctl fill:#fef3c7,stroke:#b45309,color:#451a03
    classDef ok fill:#dcfce7,stroke:#15803d,color:#052e16
    classDef stop fill:#fee2e2,stroke:#b91c1c,color:#450a0a
    classDef note fill:#e0f2fe,stroke:#0369a1,color:#082f49
```

| | Detail |
|---|---|
| **What it does** | One central service that inference engines must check **before every request** from internal research jobs (training experiments, evaluations, data processing) |
| **Fail closed** | If the service fails, is switched off or is tampered with, **every** request is denied until it is back |
| **Time to stop** | Output stops **within 35 seconds** of a decision to intervene. The delay comes from an authorization cache. OpenAI says it is working to bring this to zero. *We saw the 35-second figure only in coverage, not in OpenAI's own text* |
| **Scope** | Internal research only. Coverage says it does **not** cover ChatGPT or the API |
| **Rollout** | Fail-closed mode is live for **all frontier-model research workloads**; the rest follow "over the following days" |
| **Limit** | Stopping a job cuts off its model output. The job's process itself may keep running |
| **Why now (via coverage)** | Follows incidents in **July and October** in which research models acted outside their instructions, including the August training pause covered in earlier briefs |

**Interpretation.** Control Room is the most concrete answer yet to the Paris Call's main pledge. It is also a
reminder of how narrow that pledge is. Neither document covers models that are already deployed, open weights, or
copies held by others. The 35-second figure tells you how long it takes to cut off *output*, not how long it takes to
*decide*, and deciding is the slow part in the incidents reported so far. Watch whether Anthropic, Microsoft and
Mistral publish anything comparable.

---

## 3. Google Cloud: Gemini for healthcare (Nov 10, preview)

From the [Google Cloud press release](https://www.prnewswire.com/news-releases/google-cloud-launches-gemini-for-healthcare-302934461.html)
and coverage ([Forbes](https://www.forbes.com/sites/saibala/2026/11/10/google-cloud-launches-gemini-for-healthcare-unveiling-new-agentic-layer--capabilities/),
[Becker's](https://www.beckershospitalreview.com/healthcare-information-technology/ai/google-launches-healthcare-ai-agent-with-epic-oracle-integrations/),
[Engadget](https://www.engadget.com/2312279/google-turns-gemini-towards-medical-paperwork/)), via search results.

| | Detail |
|---|---|
| **What** | The Gemini Enterprise agent, adapted for hospitals and health insurers. It connects clinical, operational and administrative systems, with the main focus on paperwork |
| **Availability** | **Preview, US only**, for Gemini Enterprise Standard and Plus customers |
| **Connectors** | **Epic** (through open.epic APIs) and **Oracle Health**, both **read-only**: nothing is written back to the patient record. Two Optum connectors (Coordination of Benefits, Network Eligibility) are in "limited release and testing" |
| **Launch customers** | Blue Cross Blue Shield of Massachusetts, Hartford HealthCare, HCA Healthcare, Highmark Health, Northwell Health, Optum, Stanford School of Medicine |
| **Models** | Supports models from **Google, Anthropic and OpenAI** |
| **Controls** | Role-based access, audit logs, citations to sources |
| **Price** | Not published; per-user or pay-as-you-go options are promised |

**Caution.** One analysis advises keeping real patient data out of the preview until Google confirms in writing that
your HIPAA business associate agreement covers it. With ChatGPT for Healthcare (now also sold on AWS, §4) and
Claude's healthcare offerings, all three big labs now sell a health product. Google's read-only design is the cautious
end of that range.

---

## 4. Smaller items

- **ChatGPT Enterprise on AWS Marketplace (Nov 9).** AWS customers can buy ChatGPT Enterprise (and ChatGPT for
  Healthcare and Financial Services) through
  [AWS Marketplace](https://openai.com/index/chatgpt-enterprise-aws-marketplace/), and the spend counts toward their
  AWS commit. Prices are set in private offers. OpenAI says the features and release timing are the same as buying
  direct. This is a buying-channel change, not a new model, but it removes a procurement step for Bedrock-heavy
  companies that already use Claude.
- **First third-party Fable 5.2 numbers (via coverage; watch-item 187).** A DEV write-up quotes **Vals**: Fable 5.2
  scores **71.31%** overall, barely above Sonnet 5.5 (70.85%). It scores **62.29%** on SWE-bench Multimodal, below
  Opus 5.5's **70.21%** (the rank quoted alongside, "2 of 22", is inconsistent with that). We found no LMArena or
  METR entry yet. These early third-party numbers suggest a much smaller lead than Anthropic's launch table shows.
  Single source; treat as provisional.
- **StepBack (NeurIPS 2026; arXiv 2611.08403).** Yang Ouyang and Jung-Eun Kim. Self-consistency samples many full
  reasoning chains and takes a vote. StepBack instead starts from a few drafts, estimates **where the first error
  is**, and regenerates only from that step before voting. The authors report the same accuracy as self-consistency
  across seven math and multi-hop QA benchmarks, with up to **41%** fewer tokens. The NeurIPS abstract says up to
  50%. Via the [NeurIPS poster page](https://neurips.cc/virtual/2026/poster/149117) and a paper index; arXiv was
  blocked from this session.
- **November Pixel Drop (Nov 10).** Pixel 10 phones get Gemini app automation, including grocery orders and
  reservations, and Gemini can place phone calls for you in the US. A new tool builds home-screen widgets from a text
  prompt ([9to5Google](https://9to5google.com/2026/11/10/november-2026-pixel-feature-drop/)).
- **Paris Peace Forum, Nov 10–11.** The coalition on children's rights and AI (co-led by everyone.ai; OpenAI, Google
  and Anthropic take part) planned to present its first voluntary commitments here. Coverage of a "Children First"
  pledge is thin, so we will report it once the text is out.

**Excluded (could not verify).**
- **"Gemini 4 Carbon generally available in Gemini Enterprise" (Nov 10 digest):** neither the release notes nor
  other coverage show it. Carbon is still restricted to cyber defenders and the Fairwind program.
- **"MiniMax H3-Image, 33.1B open weights, Nov 10":** one crypto-news source. Other coverage describes H3 as an
  August **video** model.
- **"OpenAI Q3 revenue $10B":** one newsletter only.
- **"SPARE" linear-attention paper (arXiv 2611.07552):** listed in a digest, but search found no abstract.

---

## Watch-items into the next brief

| # | Item | Status after Nov 10–11 |
|---|---|---|
| 182 | Qwen4 | Still no weights, API or model card |
| 186 | Fable 5.2 system card | Still not opened directly. One secondary write-up (explainx) repeats the claim that Mythos 5.2 is better at hidden tasks when its reasoning is hidden from the monitor |
| 187 | Independent Fable 5.2 evaluations | **First Vals numbers (via coverage):** 71.31% overall vs Sonnet 5.5 70.85%; behind Opus 5.5 on SWE-bench Multimodal. No LMArena or METR yet |
| 188 | IPO pricing | No change; Renaissance Capital expects pricing the week of **Nov 16** |
| 189 | Operation Snowball | No follow-ups found |

Items 71, 88–135, 136–181, 183–185 carry over unchanged; nothing new was found on them.

New items:

190. **Muse Ember in practice.** Independent agent benchmarks; whether Meta publishes a model card or safety report;
     whether Glimmer gets a matching open small model.
191. **Paris Call follow-through.** Whether signatories publish shutdown mechanisms as concrete as Control Room;
     whether more governments (UK, Germany, US) or companies (Google, Meta, xAI) join.
192. **Gemini for healthcare.** HIPAA BAA coverage, pricing, and whether connectors gain write-back.

---

### Method & caveats

- **Compiled** Wed Nov 11 2026, ~05:00–06:30 Los Angeles time, covering **Nov 10 → Nov 11**. Muse Ember, the Paris
  Call, Control Room and the AWS Marketplace item (all Nov 9) are catch-up items. Muse Ember corrects an exclusion in
  the Nov-10 brief.
- **What is measured, claimed, or reported.**
  - **Read directly from primary source:** the Claude Code changelog only (raw.githubusercontent.com). There are no
    new versions since v2.1.322, so no Claude Code section today.
  - **Primary sources seen only through search-result quotes:** Meta's Muse Ember pages, the Élysée and Canadian PM
    declaration pages, OpenAI's Control Room and AWS Marketplace posts, Google Cloud's press release.
  - **Vendor-reported benchmarks:** Muse Ember's Terminal-Bench 4.0 and Agents' Last Exam scores (§1).
  - **Third-party benchmarks, via coverage:** Artificial Analysis scores and cost per task (§1, figure); Vals scores
    for Fable 5.2 (§4).
  - **Reported by press:** the 35-second stop time and the incident context for Control Room (§2); the signatory count
    and the whistleblower pledge (§2).
- **Interpretation, labelled as such:** the lead, and the interpretation paragraphs in §1–§3.
- **Scraping resilience.** Direct fetches failed (DNS or proxy 403) for `techcrunch.com`, `research.meta.ai`,
  `theneuron.ai`, `elysee.fr`, `pm.gc.ca`, `openai.com`, `officechai.com`, `arxiv.org` and `huggingface.co`.
  Everything except the Claude Code changelog comes from the search index.

### Sources (by section)

- **Muse Ember.** [AI at Meta on X](https://x.com/AIatMeta/status/2119853591703998787) · [Meta research blog](https://research.meta.ai/blog/muse-ember) · [Meta developer blog](https://developer.meta.com/ai/resources/blog/build-with-muse-ember) · [Model page](https://dev.meta.ai/models/muse-ember) · [TechCrunch](https://techcrunch.com/2026/11/09/meta-releases-muse-ember-a-new-lightweight-model-for-agent-execution/) · [Artificial Analysis](https://artificialanalysis.ai/articles/meta-s-muse-ember-is-the-cheapest-model-scoring-36-on-the-intelligence-index) · [OfficeChai](https://officechai.com/ai/metas-muse-ember-matches-claude-haiku-5-5-on-artificial-analysis-intelligence-index-at-one-third-of-the-price/) · [beri.net](https://www.beri.net/article/meta-muse-ember-launch-0-10-0-50-pricing-intelligence-index-36-vs-claude-haiku-5-5-gpt-6-luna-cost-per-task-200k-long-context-tier) · [shattered.io](https://shattered.io/muse-ember-36-index-0-13-per-task-agent-cost-math-2026/) · [OpenRouter](https://openrouter.ai/meta/muse-ember) · [OrcaRouter, 200K price cliff](https://www.orcarouter.ai/blog/muse-ember-agent-loop-executor) · [Tech Insider, 200K tier](https://tech-insider.org/muse-ember-agent-cost-math-200k-tier-cached-input-2026/) · [eesel.ai review](https://www.eesel.ai/blog/meta-muse-ember-review) · [Xenospectrum](https://xenospectrum.com/en/meta-muse-ember-agent-pricing/) · [Fonearena](https://www.fonearena.com/blog/496675/meta-muse-ember-features.html)
- **Paris Call.** [Élysée declaration](https://www.elysee.fr/en/emmanuel-macron/2026/11/09/paris-call-for-ai-safety-and-security) · [Prime Minister of Canada](https://www.pm.gc.ca/en/news/statements/2026/11/09/joint-declaration-paris-call-ai-safety-and-security) · [The Decoder](https://the-decoder.com/eight-countries-and-top-ai-labs-agree-to-shutdown-mechanisms-in-new-paris-declaration/) · [The Next Web, CeSIA](https://thenextweb.com/news/paris-call-ai-safety-openai-anthropic-cesia) · [MLex](https://www.mlex.com/mlex/amp/articles/2548359) · [MLQ](https://mlq.ai/news/openai-anthropic-and-microsoft-sign-macrons-paris-call-pledging-fail-safe-shutdowns-for-frontier-ai-with-eight-countries/) · [Superpower Daily](https://superpowerdaily.com/posts/ai-companies-pledge-shutdown-controls-in-paris-declaration-without-binding-enforcement) · [CeSIA](https://cesia.org/en/publications/the-summit-for-the-inaction-on-ai-safety/)
- **Control Room.** [OpenAI](https://openai.com/index/control-room/) · [Interesting Engineering](https://interestingengineering.com/ai-robotics/openai-control-room-35-second-model-shutdown) · [FinanceFeeds](https://financefeeds.com/openai-builds-kill-switch-to-stop-rogue-ai-agents/) · [ai-tldr](https://ai-tldr.dev/releases/openai-control-room/) · [Runtime Wire](https://runtimewire.com/article/openai-control-room-stop-research-model-workloads-35-seconds) · [Blockonomi](https://blockonomi.com/how-openais-control-room-can-cut-off-a-misbehaving-ai-model-in-35-seconds/) · [CSO Online, earlier pause](https://www.csoonline.com/article/4227777/openai-pauses-ai-model-training-after-another-agent-bypasses-network-restrictions.html?mid=1)
- **Gemini for healthcare.** [Google Cloud press release](https://www.prnewswire.com/news-releases/google-cloud-launches-gemini-for-healthcare-302934461.html) · [Google Cloud press corner](https://www.googlecloudpresscorner.com/2026-11-10-Google-Cloud-Launches-Gemini-for-Healthcare) · [Forbes](https://www.forbes.com/sites/saibala/2026/11/10/google-cloud-launches-gemini-for-healthcare-unveiling-new-agentic-layer--capabilities/) · [Becker's](https://www.beckershospitalreview.com/healthcare-information-technology/ai/google-launches-healthcare-ai-agent-with-epic-oracle-integrations/) · [Engadget](https://www.engadget.com/2312279/google-turns-gemini-towards-medical-paperwork/) · [The Next Web](https://thenextweb.com/news/gemini-for-healthcare-google-cloud-ai-agent-launch) · [beri.net, BAA caution](https://www.beri.net/article/gemini-for-healthcare-preview-epic-oracle-read-only-phi-pre-ga-terms-baa-no-pricing-hca-northwell-optum)
- **Smaller items.** [OpenAI, ChatGPT Enterprise on AWS Marketplace](https://openai.com/index/chatgpt-enterprise-aws-marketplace/) · [PPC Land](https://ppc.land/aws-customers-can-now-buy-chatgpt-enterprise-against-cloud-commitments/) · [DEV, first independent Fable 5.2 results](https://dev.to/hamzaahmadaslam/claude-fable-52-benchmarks-price-and-the-first-independent-test-results-2ln4) · [Layer3 Labs](https://www.layer3labs.io/guides/claude-fable-5-2-benchmarks) · [StepBack, NeurIPS poster](https://neurips.cc/virtual/2026/poster/149117) · [StepBack, OpenTrain index](https://www.opentrain.ai/papers/stepback-step-level-error-localized-resampling-for-efficient-test-time-reasoning--arxiv-2611.08403/) · [9to5Google, Pixel Drop](https://9to5google.com/2026/11/10/november-2026-pixel-feature-drop/) · [Paris Peace Forum children coalition](https://parispeaceforum.org/initiatives/beneficial-ai-for-children-coalition/) · [Élysée, coalition roadmap](https://www.elysee.fr/en/emmanuel-macron/2026/09/22/launch-of-the-roadmap-of-the-coalition-for-childrens-rights-and-protection-in-the-age-of-ai) · [Renaissance Capital, IPO timing](https://www.renaissancecapital.com/IPO-Center/News/122417/ai-model-developer-anthropic-pbc-files-for-an-estimated-75-billion-ipo) · [Claude Code CHANGELOG](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
- **Exclusions.** [Gemini 4 Carbon availability (SmartScope)](https://smartscope.blog/en/blog/gemini-4-carbon-availability-release-date-differences-argon-2026/) · [Crypto Briefing, H3-Image](https://cryptobriefing.com/minimax-h3-image-open-weight-4k-model/) · [456X Morning Brief](https://404kresearch.substack.com/p/456x-morning-brief-november-10-2026)
