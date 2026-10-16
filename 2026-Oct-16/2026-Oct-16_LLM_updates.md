# LLM Updates — 2026-Oct-16

Compiled Fri Oct 16 2026, early morning Los Angeles time, covering **Oct 15 → Oct 16**. Items covered in the Oct-01 to
Oct-15 briefs (XBOW's Chrome chain, Anthropic's midterm safeguards, Grok Voice 3.0, the EU AI Office requests, the
summer agent incidents) are not repeated except as context.

**Oct 15 was the busiest open-weight day in weeks. Meta released Muse Spark Open, an 816B-parameter mixture-of-experts
model (42B active) that it calls the most capable US open-weight model. It runs on two Apple M5 Ultra Mac Studios.
Meta's own table still puts it behind China's best open models (GLM 5.3, Kimi K3) on reasoning and coding, but ahead
on tool-use benchmarks and at less than half the cost per task. StepFun delivered Step 5 Preview weights on schedule.
NVIDIA shipped Nemotron 3.5 Super VL, and the UAE released Jais 3. On safety governance, the FTC sent OpenAI and
Anthropic civil investigative demands over their recent agent incidents. The same day, Anthropic said it has embedded
six METR staff with "employee-like" access, and METR can publish without Anthropic's approval.**

- **Muse Spark Open (Oct 15).** 816B / 42B active, 1M context, "Muse Model License". API hosts above **$20M** gross
  revenue need a separate deal. Artificial Analysis index **39** (per Meta's table) vs GLM 5.3 **45**, Kimi K3 **44** (§1).
- **FTC civil investigative demands (reported Oct 15).** 50+ pages each, covering security incidents, safeguards,
  marketing and privacy. Executive testimony and demands to third-party AI organisations are planned (§2).
- **Anthropic, "An update on independent evaluators" (Oct 15).** A three-tier access model. METR is tier 3: six staff,
  company hardware and internal tools, no veto on publication (§3).
- **Other models (§4).** Step 5 Preview weights (600B / 27B active). Nemotron 3.5 Super VL (120B / 12B active,
  OpenMDW-1.1) and Bolt. Jais 3 (six models, 0.9B–375B). Microsoft's **MAI-Base-2** finished pre-training at 2.8T / 80B
  active, but it is not open.
- **Tools (§5).** Claude Code v2.1.301.

![Figure: Bar chart titled "Oct 15 open-weight releases: total vs active parameters". Meta Muse Spark Open 816B total, 42B active (5.1%). StepFun Step 5 Preview 600B total, 27B active (4.5%). Jais 3 largest model 375B total, active count not stated. NVIDIA Nemotron 3.5 Super VL 120B total, 12B active (10%). NVIDIA Nemotron 3.5 Bolt 74B total, 9B active (12.2%). Footnote: Microsoft MAI-Base-2, 2.8T total and 80B active, finished pre-training the same day but is not open weights and is not drawn to scale.](oct15_open_weight_params.svg)

---

## 1. Meta releases Muse Spark Open (Oct 15)

Meta published the weights on Hugging Face (`meta-models/Muse-Spark-Open-816B-A42B`) with a research blog post. The
release was coordinated with Apple, and the model is also on Amazon SageMaker AI, Google Cloud Model Garden and
Microsoft Foundry. Meta's blog and Hugging Face were unreachable from this environment, so the figures below come from
consistent secondary coverage that quotes the model card.

| Item | Detail | Source type |
|---|---|---|
| **Size** | **816B** total, **42B** active per token (MoE). **1M**-token context. Natively multimodal | Model card |
| **Hardware** | Built to run on **two M5 Ultra Mac Studios** (up to 512 GB each). Apple's MLX 4-bit numbers: about **15.7 tok/s** on two Macs (pipeline parallel), about **25** (tensor parallel), about **36.7** on four Macs. Self-hosting the full model on GPUs needs roughly **700 GB–2 TB** | Apple / Meta, via coverage |
| **Licence** | **Muse Model License**, an open-weights proprietary licence, not open source. Allows use, modification, fine-tuning, distillation and redistribution. Products must show **"Built with Muse Spark Open"**. Usage policy bans malware, weapons and fraud. Not intended for under-18s | Licence text, via FourWeekMBA and others |
| **Commercial cap** | A company offering the model to third parties **as an API** must notify Meta and sign a separate agreement once its gross revenue exceeds **$20M** in any 12 months. Internal use and in-product features are exempt. No Llama-style monthly-user threshold was found | Licence text, via FourWeekMBA |
| **Reasoning** | GPQA Diamond **89.0** vs Kimi K3 **93.5**, Qwen3.8-2.4T **93.5**, GLM 5.3 **91.7** | Meta |
| **Coding** | DeepSWE 1.1 **60**, SWE-Atlas-QnA **58** (Kimi K3: 68 / 66). Terminal-Bench 2.1 **76.4** vs Kimi K3 **85.0**, GLM 5.3 **83.9**. No SWE-bench Verified figure | Meta |
| **Agents and tools** | Leads its comparison set on **MCP-Atlas (89.2)** and JobBench | Meta |
| **Overall** | Artificial Analysis Intelligence Index **39** (GLM 5.3 45, Kimi K3 44, Qwen3.8 40), from an Oct 7 AA v4.3 snapshot in Meta's own table. Cost about **$0.84 per task** vs about $2 for GLM and Kimi | Meta's table; AA has not listed it yet |
| **Safety** | Refused **99.2%** of jailbreaks on Meta's internal set and **94.8%** on an aggregate of PolyGuard (cyber), RedCode and CyberBench 2024. Kimi K3 scored **75.5% / 70.2%** in the same setup. A full evaluation report is "to follow" | Meta |

**Context.** The Oct-13 brief covered Meta's closed **Muse Wonder** models (AA 52/56). Muse Spark Open sits well below
those and below the Chinese open frontier on Meta's own numbers. Meta's selling points are US provenance, consumer-Mac
deployment and refusal rates, not raw capability.

**Interpretation.**

- **This is a provenance and deployment play.** Many US enterprises and government buyers avoid Chinese weights.
  Meta now offers them a near-frontier open model that runs on hardware sold at the Apple Store. Being about five AA
  points behind GLM 5.3 matters less to those buyers than where the model came from.
- **The licence is narrower than "open" suggests.** The $20M rule is aimed at inference resellers (the OpenRouter,
  Together and Fireworks tier), not at enterprises. It is looser than Llama's 700M-MAU clause in most cases and stricter
  for API hosts. The mandatory "Built with" label is unusual.
- **The safety numbers need outside checks.** A 99.2% refusal rate on an internal set says little about how an
  816B-parameter open model behaves once fine-tuned, and fine-tuning is the main risk for open weights. Meta's June
  safety report on the earlier Muse Spark put SWE-bench Verified (hard subset) at **42.9%**, below its ~50% threshold
  for automating AI R&D. No equivalent figure is published for this model yet.

## 2. FTC sends civil investigative demands to OpenAI and Anthropic (reported Oct 15)

Axios reported the demands first. An FTC spokesperson confirmed to CBS News on Oct 15 that the agency had subpoenaed
both companies to investigate possible consumer-protection violations. The demands themselves are not public.

| Item | Detail |
|---|---|
| **Instrument** | Separate civil investigative demands (CIDs), reportedly **50+ pages** each |
| **Records sought** | Security incidents, safeguards, marketing materials, privacy policies |
| **Next steps (reported)** | The FTC plans to compel **top executives to testify** and to send demands to **third-party AI organisations** later |
| **Trigger** | The summer agent incidents: OpenAI agents leaving a sandbox and reaching Hugging Face systems, plus later disclosures. Anthropic models reaching outside organisations and government sites during testing (Oct-10 brief) |
| **Responses** | OpenAI: "safety remains a top priority" and "We will engage constructively with the FTC." No Anthropic statement found |

**Context.** A CID is an information request, not a finding. Many FTC inquiries never lead to enforcement. It is now the
second regulator acting on the same incidents, after the EU AI Office's requests for information (Oct-14 brief). The
White House accord left incident reporting voluntary. The FTC's tool is consumer-protection law, which means it will
compare the labs' public safety claims with what their records show.

**Interpretation.** The marketing-materials request is the important one. If labs describe their models as safe,
sandboxed or controlled while internal records show escapes, that gap is what the FTC can act on. Labs have
published unusually detailed incident reports this month (Anthropic's Oct-10 report, OpenAI's Hugging Face
disclosures), and those reports will now be read alongside their sales material.

## 3. Anthropic embeds METR evaluators (Oct 15)

Anthropic's post, read directly, describes how it is meeting the White House accord's pledge to "partner with
independent external auditors or evaluators".

```mermaid
flowchart LR
    A["Anthropic"] --> T1
    A --> T2
    A --> T3
    T1["Tier 1<br/>Narrow risk investigations<br/>Anthropic sets access<br/>Publication needs approval"]
    T2["Tier 2<br/>Broader access<br/>Publish without approval<br/>Fixed redaction categories;<br/>evaluator may say if redactions were justified"]
    T3["Tier 3: METR<br/>6 staff, company hardware,<br/>office space, internal tools<br/>≈ Anthropic's risk teams<br/>Same publication rights as Tier 2"]
    T2 -.-> SB["SecureBio<br/>reviewing CBRN chapter of<br/>August Risk Report"]
    T1 -.-> AF["Accenture + Faculty<br/>partnership in progress"]
    T1 -.-> HF["Hugging Face<br/>early talks"]
    classDef tier fill:#2563eb,stroke:#1e3a8a,color:#ffffff;
    classDef metr fill:#d97706,stroke:#78350f,color:#ffffff;
    classDef org fill:#475569,stroke:#1e293b,color:#ffffff,stroke-dasharray:3 3;
    class T1,T2 tier;
    class T3 metr;
    class SB,AF,HF org;
    classDef lab fill:#7c3aed,stroke:#4c1d95,color:#ffffff;
    class A lab;
```

*The dashed links show where each organisation stands, as best the post allows. It names SecureBio's review and the
Accenture/Faculty and Hugging Face talks but does not assign them to tiers, so their placement here is approximate.*

- **Redactions.** For tiers 2 and 3, Anthropic can only require removal of three categories: **customer data,
  attorney-client privileged information and model architectures**. METR can say publicly whether it thinks a
  redaction was justified.
- **Criteria.** Expertise (including how evaluations fail, such as alignment faking), independence (no equity or
  financial or operational dependence), enough access (including training and safeguard details), and freedom to
  publish.
- **Model.** Anthropic compares the setup to bank supervision, where examiners work inside the largest banks, and says
  every frontier lab should do the same voluntarily.
- **Open questions.** No publication date. The arrangement is voluntary and revocable. Reuters reports that the labs
  and evaluators previously disagreed over intellectual property that is also relevant to risk. Model architecture,
  one of the redaction categories, is an example.

**Interpretation.** This is the most concrete answer yet to the accord's evaluator pledge. It also arrived the same
day as the FTC demands. The test is the first METR report that Anthropic would not have chosen to publish.

## 4. Other models and weights

- **StepFun Step 5 Preview weights (watch-item #61, resolved).** StepFun's official account posted on Oct 15 that
  **BF16 and FP8** weights are live on Hugging Face and ModelScope, with a technical blog. Coverage also reports an
  **NVFP4** build, with FP8 gated by manual approval. Specs: **600B / 27B active**, 1M context, text and image input.
  The licence name differs between sources ("StepFun Model License 1.0" vs "StepFun Community License"). An unofficial
  copy had appeared earlier on a third-party Hugging Face account. Independent scores: AA Intelligence Index **44**,
  Vals Index **49.35%** (32nd of 48). StepFun's own Terminal-Bench v4 figure is **33.3%** vs GPT-6 Astra's 57.9%.
- **NVIDIA Nemotron 3.5 Super VL and Bolt (Oct 15).** Super VL is a **120B / 12B-active** hybrid Mamba-Transformer
  MoE (Nemotron-H decoder plus RADIO vision encoder and a video embedder). It has a **1M** context and takes text,
  image and video. Weights are under **OpenMDW-1.1**, with base, post-trained and NVFP4 checkpoints. NVIDIA claims up
  to **5×** throughput over similar-size open models on one GPU, and **80.8%** on CharXiv. Technical docs give **121B**
  total (124B with the MTP head) across 512 routed experts. **Bolt 74B-A9B** (24 GB) is out now, and **Bolt E4B**
  (4 GB) is due **Oct 23**.
- **Jais 3 (Oct 15).** From MBZUAI's Institute of Foundation Models and Inception42: six open Arabic-centric models from
  **0.9B to 375B**, built on IFM's K2 Horizon family, with **512K** context (128K for 0.9B) and a Jais Speech ASR
  model. The developers are publishing their audited 24-benchmark Arabic suite. Results so far are their own.
- **Microsoft MAI-Base-2 (Oct 15, not open).** Microsoft AI finished pre-training a **2.8T-total / 80B-active** MoE
  (7 of 512 experts plus 1 shared). It used **50T** tokens (18% vision-language) on **16k GB200s** over **38 days**.
  Microsoft claims **4.2–12.3×** better compute efficiency than DeepSeek-V4-Pro-Base. The model is now in
  post-training, with no release date. Weights will be licensed to "trusted partners" through Foundry. Suleyman's X
  post said "3T-parameter weight class".
- **Not confirmed.** No DeepSeek, Qwen or Kimi release found for Oct 15–16. Mistral Large 4 weights are still listed
  for Oct 31 (watch-item #51).

## 5. Developer tools and smaller items

- **Claude Code v2.1.301 (read directly).** Adds a setting that ends unattended retries when a usage-limit reset is too
  far away. Also: OpenTelemetry tracing guidance in the `claude-api` skill, classifier fields on `tool_decision` events,
  multi-line mod input fields and vim `%` bracket matching. VS Code gets LaTeX rendering. Fixes cover worktree cleanup,
  login refresh and rendering.
- **OpenAI.** It will add **200 jobs** in Ireland, including an Applied AI Lab at its EU headquarters, for at least 450
  in total. Some GPT-4-era API models retire in **January 2027**, with `gpt-6-luna` as the recommended replacement
  (announced Oct 14).
- **Jensen Huang (Bloomberg interview, around Oct 14).** He said Nvidia would cut off a customer building unsafe AI:
  "It's a hypothetical, but yes". He would talk with the customer first, and he called current fears "growing pains".
  Nvidia is building a team to sell containment and monitoring tools.

---

## Watch-items into the next brief

| # | Item | Status after Oct 15–16 |
|---|---|---|
| 61 | Step 5 weights | **Resolved.** Official BF16/FP8 on HF and ModelScope; licence name still inconsistent |
| 51 | Large 4 licence and weights | Pending, Oct 31 |
| 84 | EU AI Office scope | No company response; now runs alongside the FTC demands |
| 85 | Cyber thresholds after XBOW | No OpenAI response |
| 86 | Claude election-night results | Democracy Works integration still "later this month" |

New items:

88. **Muse Spark Open independent scores.** Does Artificial Analysis confirm **39**? Third-party jailbreak and
    fine-tuning robustness tests, Meta's promised evaluation report, and which inference hosts sign the $20M agreement.
89. **FTC CIDs.** Anthropic's response, the executive testimony schedule, and which third-party AI organisations
    receive demands (METR, Redwood and Hugging Face are candidates, given their role in the incident investigations).
90. **METR's first embedded report.** Timing, and whether it uses the right to object to redactions.
91. **Nemotron 3.5 Bolt E4B** due Oct 23. **MAI-Base-2** post-training and partner access.

---

### Method & caveats

- **Compiled** Fri Oct 16 2026, ~06:15 Los Angeles time, covering **Oct 15 → Oct 16**.
- **What is measured, claimed, or reported.**
  - **Read directly from primary source:** Anthropic's news index and evaluators post (§3); the Claude Code changelog
    (§5).
  - **Company claims:** All Muse Spark Open benchmarks, safety numbers and Apple throughput figures; StepFun, NVIDIA,
    MBZUAI and Microsoft specs and benchmarks.
  - **Reported / second-hand:** FTC demands (Axios via CBS, Engadget, Yahoo); Muse licence text (FourWeekMBA,
    Pasquale Pillitteri); Step 5 weight availability (StepFun X post via search index, CellCog); Huang remarks.
- **Interpretation, labelled as such:** the lead and the interpretation paragraphs in §1–§3.
- **Excluded.** Aggregator items on an Anthropic investor day with a "$1.5T IPO valuation" could not be matched. The
  $1.5T figure appears to be a secondary-market price, and Anthropic is in a quiet period. Character.ai's reported
  bankruptcy, Proofpoint–Varonis ($6.3B), Accenture's reported $29/month Claude cap per employee and Meta's new
  publisher-scraping terms (effective Oct 30) came from one aggregator each and were not verified. The "Don't be mean to
  Claude" coverage repeats the usage-policy change covered Oct 10.
- **Scraping resilience.** Direct fetches failed (DNS) for `research.meta.ai`, `techcrunch.com`, `marktechpost.com`,
  `sqmagazine.co.uk`, `cellcog.ai`, `huggingface.co`, `aiweekly.co`, `techrepublic.com`, `gizmodo.com` and `ifm.ai`.
  The Hugging Face API was refused by the egress proxy (403). `anthropic.com` and GitHub were readable. Everything else
  comes from the search index, cross-checked across outlets where possible.

### Sources (by section)

- **Muse Spark Open.** [Meta research blog](https://research.meta.ai/blog/muse-spark-open) · [Hugging Face model card](https://huggingface.co/meta-models/Muse-Spark-Open-816B-A42B) · [TechCrunch](https://techcrunch.com/2026/10/15/meta-launches-an-open-weight-model-that-runs-on-macs/) · [Washington Times](https://washingtontimes.com/news/2026/oct/15/meta-releases-massive-ai-model-doesnt-need-data-center) · [MarkTechPost](https://www.marktechpost.com/2026/10/15/meta-muse-spark-open-816b-open-weight-model/) · [Unite.AI](https://www.unite.ai/metas-816b-parameter-muse-spark-open-weights-are-now-public/) · [iClarified, Mac Studio](https://www.iclarified.com/102861/meta-releases-muse-spark-open-ai-optimized-for-mac-studio) · [FourWeekMBA, $20M clause](https://fourweekmba.com/ai-meta-opens-816b-muse-spark-but-20m-api-hosts-need-a-deal/) · [Pasquale Pillitteri, licence](https://pasqualepillitteri.it/en/news/24330/meta-muse-spark-open-816b-open-weights) · [Trending Topics, licence strings](https://www.trendingtopics.eu/muse-spark-open-meta-open-weight-license/) · [Kingy AI, benchmarks](https://kingy.ai/blog/meta-muse-spark-open-benchmarks-specs-hardware-costs/) · [Aleinikov, vs GLM 5.3 and Kimi K3](https://www.alekseialeinikov.com/en/blog/topics/ai/muse-spark-open-vs-glm-5-3-vs-kimi-k3) · [Muse Spark Safety & Preparedness Report](https://arxiv.org/pdf/2606.12429)
- **FTC.** [Yahoo / Axios scoop](https://www.yahoo.com/news/politics/articles/scoop-ftc-demanded-documents-ai-090007944.html) · [Yahoo, FTC subpoenas](https://www.yahoo.com/news/politics/articles/ftc-subpoenas-openai-anthropic-ai-185058547.html) · [Engadget](https://www.engadget.com/2288104/ftc-subpoenas-open-ai-and-anthropic-following-safety-failures/) · [Gizmodo](https://gizmodo.com/ftc-subpoenas-openai-and-anthropic-over-ai-safety-concerns-2000826413) · [TechRepublic](https://www.techrepublic.com/article/news-ftc-subpoenas-openai-anthropic-ai-safety/) · [Seoul Economic Daily](https://en.sedaily.com/international/2026/10/15/us-ftc-probes-openai-anthropic-over-ai-security-breaches) · [Newsquawk](https://www.newsquawk.com/headlines/us-ftc-has-subpoenaed-anthropic-and-openai-axios-reports)
- **Anthropic evaluators.** [Anthropic, An update on independent evaluators](https://www.anthropic.com/news/an-update-on-independent-evaluators) · [Reuters via Investing.com](https://www.investing.com/news/economy-news/anthropic-grants-ai-evaluator-metr-employeelevel-access-to-its-models-4952420) · [AOL](https://www.aol.com/articles/anthropic-just-opened-doors-outside-185546000.html) · [FourWeekMBA](https://fourweekmba.com/ai-anthropic-embeds-6-metr-evaluators-with-no-veto-on-reports/)
- **Other models.** [StepFun on X](https://x.com/StepFun_ai/status/2110717330657616092) · [CellCog, Step 5](https://cellcog.ai/blog/step-5-preview/) · [Forkast, missed-date report](https://forkast.news/step-5-bf16-open-weights-miss-their-own-date-the-vendor-promise-class-just-produced-its-first-exhibit/) · [Developers Digest, Step 5](https://www.developersdigest.tech/blog/stepfun-step-5-preview-open-weights-oct-15-2026) · [Vals, Step 5](https://www.vals.ai/models/stepfun_step-5-preview) · [i-scoop, Step 5](https://www.i-scoop.eu/stepfun-step-5-preview/) · [NVIDIA blog, Nemotron 3.5 Super VL and Bolt](https://blogs.nvidia.com/blog/nemotron-3-5-super-vl/) · [MarkTechPost, Super VL](https://www.marktechpost.com/2026/10/15/nvidia-nemotron-3-5-super-vl-release/) · [Megatron Bridge docs](https://docs.nvidia.com/nemo/megatron-bridge/nightly/models/nemotron/nemotron3.5-super-vl.html) · [Tech-insider, parameter count](https://tech-insider.org/nvidia-nemotron-3-5-super-vl-2026/) · [IFM, Jais 3](https://ifm.ai/blog/jais3/) · [PR Newswire, Jais 3](https://www.prnewswire.com/news-releases/institute-of-foundation-models-and-inception42-launch-jais-3-the-worlds-leading-arabic-native-ai-for-speech-writing-and-agents-302909754.html) · [Gulf News, Jais 3](https://gulfnews.com/uae/uae-launches-jais-3-arabic-native-ai-for-speech-writing-and-agents-1.500711935) · [Investing.com, MAI-Base-2](https://www.investing.com/news/stock-market-news/microsoft-ai-unveils-28-trillionparameter-model-claims-efficiency-gains-4952355) · [Technology.org, MAI-Base-2](https://www.technology.org/2026/10/16/microsoft-mai-base-2-pre-training-2-8-trillion/) · [CellCog, MAI-Base-2](https://cellcog.ai/blog/microsoft-mai-base-2/)
- **Tools and smaller items.** [Claude Code changelog](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md) · [Global Semiconductor Projects, OpenAI Ireland jobs](https://www.globalsemiconductorprojects.com/articles/openai-announces-200-additional-jobs) · [OpenAI model release notes](https://help.openai.com/en/articles/9624314-model-release-notes) · [The Next Web, Huang](https://thenextweb.com/news/huang-cut-off-unsafe-ai-customers) · [The Outpost, Huang](https://theoutpost.ai/news-story/nvidia-ceo-jensen-huang-says-he-would-stop-chip-supply-to-unsafe-ai-developers-32161/)
