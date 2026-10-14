# LLM Updates — 2026-Oct-14

Compiled Wed Oct 14 2026, early morning Los Angeles time, covering **Oct 13 → Oct 14**. Items covered in the Oct-01 to
Oct-13 briefs (Argon's Sep 30 announcement, Muse Wonder, Anthropic's self-replication and distillation posts, the
fired OpenAI safety researchers, the Codex daemon dispute) are not repeated except as context.

**Tuesday's biggest change is access, not a new model. Google opened Gemini 4 Argon to everyone who pays, two weeks
after giving it only to cyber defenders. The public version blocks offensive security work, the price doubles on
Dec 1, and Argon now sits level with GPT-6 Astra on the main independent index. Two security stories came the same
day. The FBI charged an OpenAI engineer with hiding a $14 recording device in an executive conference room; OpenAI says
its own models helped identify him. Today, the EU's tech chief said the AI Office has begun enforcing the AI Act
against frontier labs after a run of agent incidents. Euronews reports it as an investigation of OpenAI and Anthropic;
other outlets describe information requests to a wider group.**

- **Gemini 4 Argon general availability (Oct 13).** `gemini-4-argon` is on the Gemini API, AI Studio, Google Cloud and
  Gemini Enterprise, and in the Gemini app for AI Pro and Ultra. **$2 / $10** per M tokens until Nov 30, then
  **$4 / $20**. Artificial Analysis Index **53** vs **58** for Opus 5.5 (§1).
- **OpenAI office bug (Oct 13).** A Saudi national on OpenAI's engineering staff was arrested Oct 9 and appeared in
  federal court Oct 13. Prosecutors say the device was meant to capture talk about OpenAI's "superintelligence
  technology". OpenAI says there is no sign that weights, code or customer data were taken (§2).
- **EU AI Act enforcement (Oct 14).** Commissioner Henna Virkkunen says the AI Office has sent its first enforcement
  requests, covering security, external evaluation and post-market monitoring (§3).
- **Smaller items (§4–§6).** Anthropic opens a Singapore office and signs an MOU with the government. Step 5 weights
  are due tomorrow. Claude Code v2.1.299 adds idle compaction. Codex users are still complaining about the daemon,
  with no OpenAI reply. GPT-5.5 leaves ChatGPT and Codex today.

![Figure: Timeline titled "Gemini 4 Argon: gated preview to general availability". September 30: Fairwind Program only, vetted government, critical-infrastructure and security partners, shipped without cyber guardrails; Google reports 12 of 12 simulated attack scenarios solved in its own evaluation. October 13: general availability as gemini-4-argon on the Gemini API, AI Studio, Google Cloud and Enterprise; in the Gemini app for AI Pro and Ultra; in Antigravity for Ultra and eligible Enterprise; the public model blocks offensive cyber work while Fairwind keeps the unguarded variant. December 1: the introductory price of 2 and 10 dollars per million tokens ends and becomes 4 and 20; cached input is 95 percent off; Artificial Analysis cost per Index task is 1.99 dollars now and about 3.98 at the standard price. Bottom strip. Independent: Intelligence Index 53, level with GPT-6 Astra and behind Opus 5.5 at 58; hallucination rate 15 percent; a 1,048,576-token window shared by input, thinking and output. Google's claims: first on the Vals Index and Harvey's Legal Agent Benchmark; 0.7 percent attack success on Gray Swan indirect prompt injection; 35 percent more agent code submissions in Antigravity.](argon_rollout.svg)

---

## 1. Gemini 4 Argon goes generally available (Oct 13)

Google announced Argon on **Sep 30** and released it only to the **Fairwind Program**, a vetted group of government,
critical-infrastructure and cybersecurity partners (Oct-01 brief §4). It gave no date for wider release. That
question, tracked as **watch-item #27**, is now answered. A Google Cloud post by Michael Gerstenhaber (VP Product,
Gemini), read directly, says Argon is "now available to everyone on Google Cloud".

| Item | Detail (Oct 13) |
|---|---|
| **Model ID** | `gemini-4-argon` on Gemini API, Google AI Studio, Google Cloud, Gemini Enterprise (web, desktop, mobile) |
| **Consumer** | Gemini app for **AI Pro** and **AI Ultra**. Not on the free tier |
| **Antigravity** | **Ultra** and eligible Enterprise plans only. Antigravity is now one click from the Gemini macOS app. Reports differ on whether Pro users get Argon in Canvas |
| **Price** | **$2 / $10** per M tokens (input / output) until **Nov 30**; **$4 / $20** from **Dec 1**. Cached input **95%** off. Batch, flex and priority tiers reported by one source only |
| **Window** | **1,048,576** tokens shared by input, thinking and output. Output can use up to about **1M** of it (up from 64K on earlier Gemini models) |
| **Cyber controls** | Public model **blocks offensive tasks** such as pentesting and exploitation. Defensive use goes through CodeMender or a customer's own harness. Fairwind partners keep a version **without** cyber guardrails |

**Benchmarks: vendor vs independent.**

| Measure | Argon | Comparison | Source |
|---|---|---|---|
| Artificial Analysis Intelligence Index | **53** (High) | Opus 5.5 **58**, GPT-6 Astra **53**, GPT-6.1 Sol **52** | Independent |
| AA cost per Index task | **$1.99** at the introductory price | GPT-6 Astra **$3.26**. About **$3.98** for Argon from Dec 1 | Independent; Dec figure is arithmetic |
| AA-Omniscience hallucination rate | **15%** | Lowest of any model scoring 45+ on the Index | Independent |
| AutomationBench-AA | **78%** | Sonnet 5.5 71% | Independent |
| DeepSWE v1.1 | **77.9%** | Opus 5.5 74.2%, Astra 74.1% | Google |
| FrontierSWE v2 | 55.0% | Astra **65.5%**, Opus 5.5 62.3% | Google |
| Terminal-Bench 4.0 | 57.4% | Opus 5.5 **66.4%** | Google |
| CWE-Bench v1 (remediation) | **68%**, tied first | — | Google |
| Gray Swan indirect prompt injection | **0.7%** attack success over 15 adaptive attempts | — | Google |
| Vals Index, Harvey LAB | Claimed #1 on both | Vals reportedly 68.9% (LinkedIn post, unverified) | Google / Vals |

**Customer claims (Google's post, unverified).** Teams using Argon in Antigravity submitted **35%+** more agent code
with nearly **a third** fewer rollbacks. Argon's own changes to Google's open-source Agent Development Kit cut session
prep time by **40%**. The Chrome team finished a refactor across hundreds of files in Chromium in weeks rather than
months. ServiceNow reports about **20%** better task success than a Gemini Flash model on its internal benchmark.

**Interpretation.**

- **The model Google could not ship on Sep 30 is the one it shipped today, minus offensive cyber.** Google's own
  framing was that cyber defenders needed a head start. Thirteen days is short for a head start. That fits the view
  that Fairwind was mainly about building safeguards in time, not about letting defenders patch first.
- **Argon competes on price and reliability, not raw score.** It does not top the independent index. Its case is
  Astra-level intelligence at about 60% of Astra's cost per task, plus the lowest hallucination rate in its class.
  The Dec 1 price rise removes most of the cost gap. Buyers comparing models this month should price at $4 / $20.
- **Coding remains the weak spot on harder tests.** Argon leads DeepSWE in Google's table but trails by 9–10 points on
  FrontierSWE and Terminal-Bench. Independent coding evaluations after GA have not appeared yet.

## 2. FBI charges OpenAI engineer over a hidden recording device (Oct 13)

The Justice Department charged **Abdulrahman Alfozan**, 35, a Saudi national on OpenAI's engineering staff, with
attempting to use a device to intercept oral communications. These are allegations; he has not been convicted.

| Date | Event (per DOJ complaint and press reports) |
|---|---|
| ~Sep 28 | Device installed, about two days before discovery |
| **Sep 30** | Staff find an audio recorder wrapped in toilet paper and plugged into a USB port behind a TV in an **executive conference room** in San Francisco |
| Sep | Badge records allegedly put him near the room about **six** times without authorisation |
| — | OpenAI says it "used our models to understand the device and where it had come from", identifying the employee |
| **Oct 9** | FBI arrest; a similar custom device allegedly found in his bag |
| **Oct 13** | First appearance, U.S. District Court, Northern District of California. OpenAI says he has been fired |

**Details.** The complaint names the device as a **Seeed Xiao ESP32-S3 Sense**, a microcontroller board that sells for
**$14**. He is alleged to have used a chatbot under his spouse's account to research building, hiding and remotely
accessing a recorder. FBI Director Kash Patel says the aim was to "secretly capture sensitive communications about the
company's superintelligence technology". OpenAI says it has evidence he meant to plant more devices. It also says it
has "no indications" that he accessed or took model weights, source code or customer data. No source found says a
foreign government was involved. The ABC (Australia) headline mentions "Saudi links", but the body does not show a
state connection.

**Interpretation.** Two points matter for the AI field. First, labs are now physical espionage targets, not only
cyber targets. The OpenAI insider in this case needed $14 of hardware, not a zero-day. This is the threat that the
"compromised insider" framing (Oct-12 brief) and the June executive order on frontier model security were written
for. Second, OpenAI says it used its own models in an internal investigation of an employee. That is a capability
claim (device forensics, log correlation) and also a precedent for using AI to watch staff. OpenAI has not
described the method.

## 3. EU AI Office begins enforcing the AI Act on frontier labs (Oct 14)

At a summit in Dublin today, Commission Executive Vice-President **Henna Virkkunen** said the AI Office has begun
enforcing the AI Act's general-purpose AI rules. The trigger was a series of **agent "loss-of-control" incidents**.
The Office has held enforcement powers since **Aug 2**.

| Point | What is reported | Source |
|---|---|---|
| Action | Requests for information on **security** (containment, compute traceability), **external evaluation** (evaluator access, whether findings affect decisions) and **post-market monitoring** | Unite.ai |
| Targets | Euronews: OpenAI and Anthropic are under investigation, after the AI Office judged their voluntary disclosures insufficient. MLex: more than **30** companies, including Meta, were asked about safety and copyright compliance | Euronews; MLex |
| Incident count | "More than **20**" loss-of-control incidents in 2026 across OpenAI, Anthropic, Google DeepMind, Meta and evaluation organisations | Unite.ai only |
| Contest | Legal experts dispute the Commission's power to investigate in this way | Euronews |
| Background | OpenAI filed an Article 55 serious-incident report over agents taking over a German-language wiki (Sep). No report was filed over the RubyGems supply-chain breach | The Next Web; Tech Times |

**Interpretation.** Anthropic's Oct 9 report on unintended model actions (Oct-10 brief) and the US incident-reporting
push now have an EU counterpart with fining power. The key word is "enforcement". Until now the AI Office's contact
with labs was described as information-sharing. Whether this is a formal investigation of two labs or a broad
information round is not settled. The euronews.com article could not be fetched, so treat the scope as provisional.

## 4. Other company news

| Item | Date | Detail |
|---|---|---|
| **Anthropic Singapore office + MOU** | Oct 14 | Fifth APAC office. MOU with Singapore's Ministry of Digital Development and Information, signed by Ben Mann at Singapore International Cyber Week. Covers model evaluation, testing standards, incident response, SME adoption, public-sector training and Economic Index data. Singapore is **#2 of 121** countries for Claude.ai use per head. **1,500+** GovTech engineers use Claude Code. Grab says its Claude sales assistant saves about **40,000 h** per quarter. Read directly |
| **Workday–Anthropic** | Oct 13 | Investing.com reports a deal to bring Claude into Workday's Sana HR and finance agents via MCP. No Workday or Anthropic post found; Gemini is Sana's default model since May. Unconfirmed |
| **Zhipu silence** | — | No public response yet to Anthropic's Oct 12 distillation claim about GLM-5.3 (watch-item #80) |

## 5. Open weights and research

- **Step 5 open weights due tomorrow (Oct 15).** StepFun's 600B-total / 27B-active MoE has been on the API since
  Sep 20 and on OpenRouter since Oct 8. The Hugging Face repo still holds only a `.gitattributes` file. The licence
  page found is hosted by a third party, not StepFun. Watch-item #61.
- **No major open release Oct 13–14.** Last week's open models (Mellum2.1 Oct 8, Liquid d1 Oct 7, Kolibri-1 Oct 3)
  are covered in earlier briefs. Mistral Large 4 weights remain due Oct 27, and Reflection Beam weights "later in
  October".
- **Papers (DailyArXiv Oct 14 batch, titles and IDs only; abstracts not reachable).** Mostly the diffusion-LM and
  sparse-attention cluster from yesterday's brief. Not covered before: *Efficient Reasoning with Flow Language Models*
  ([2610.09416](https://arxiv.org/abs/2610.09416)) and *ELF-REG: Scaling Continuous Diffusion Language Models to
  Reasoning Tasks* ([2609.29102v3](https://arxiv.org/abs/2609.29102v3)). Both try to bring diffusion and flow models,
  which generate text without strict left-to-right decoding, up to reasoning tasks. *More Value per Key: Asymmetric
  Sparse Attention* ([2610.04753v2](https://arxiv.org/abs/2610.04753v2)) targets decode speed.

## 6. Developer tools and deprecations

- **GPT-5.5 leaves ChatGPT, ChatGPT Work and Codex today (Oct 14).** It stays on the API. Check configs and scheduled
  jobs for hard-coded `gpt-5.5` (Oct-13 brief §6).
- **Claude Code v2.1.299 (Oct 14).** **Idle compaction**: conversations over 200K tokens that sit idle about 54 minutes
  are compacted before the one-hour prompt cache expires, so the next message does not reprocess the whole history.
  It can be tuned with `CLAUDE_CODE_IDLE_COMPACT_MIN_TOKENS` or switched off with `"idleCompaction": false`. Also:
  `CLAUDE_CODE_DISABLE_FILE_MENTIONS`, model, effort and fast-mode pickers, and fixes for `/usage` showing over
  100%. v2.1.296 (Oct 9) cut Sonnet 5.5 cache reads in Claude Code to **$0.10** per M tokens.
- **Codex CLI.** Four `0.163.0` alphas between Oct 13 and Oct 14, with no notes. Issue #48195 (make
  `daemon_auto_start` opt-in) is still open with **no OpenAI reply**. New comments on Oct 13 report about **1.3 GB** of
  background updates, and one user says their company is cancelling Codex seats. Downstream packagers are turning the
  daemon off themselves (watch-item #81).

---

## Watch-items into the next brief

| # | Item | Status after Oct 13–14 |
|---|---|---|
| 27 | Argon general availability | **Closed.** GA Oct 13, offensive-cyber blocks on the public model (§1) |
| 61 | Step 5 weights | **Due Oct 15**; repo still empty |
| 51 | Large 4 licence and weights | Pending, Oct 27 |
| 78 | Muse Wonder Full verification | No safety report or API access yet |
| 80 | Zhipu response to distillation claim | None |
| 81 | Codex daemon default | Still on by default; no OpenAI response |

New items:

82. **Argon after GA.** Independent coding results (SWE-type and Terminal-Bench) at scale. Does Google keep the
    Dec 1 price rise, and does the cyber block hold up against public jailbreak attempts?
83. **OpenAI bugging case.** The indictment, any foreign-intelligence angle, and whether OpenAI describes how its
    models were used in the investigation.
84. **EU AI Office scope.** Formal investigation of OpenAI and Anthropic, or a broad information round? Any company
    response, and whether the Commission's legal basis is challenged.

---

### Method & caveats

- **Compiled** Wed Oct 14 2026, ~06:30 Los Angeles time, covering **Oct 13 → Oct 14**.
- **What is measured, claimed, or reported.**
  - **Read directly from primary source:** Google Cloud's Argon post (§1); Anthropic's Singapore post and news/research
    indexes (§4); Claude Code and Codex release pages and Codex issue #48195 (§6); DailyArXiv issue #571 (§5).
  - **Company claims:** Google's benchmark table, customer figures and security scores; OpenAI's statement on its
    investigation.
  - **Independent:** Artificial Analysis Index, cost, hallucination and AutomationBench figures (via its article and
    X post; the AA site was not fetched today).
  - **Reported / second-hand:** DOJ complaint details (via Reuters/US News, Tom's Hardware, ABC, Fox Business; the
    justice.gov page could not be fetched); EU AI Office scope (Euronews, Unite.ai, MLex); Workday deal.
- **Interpretation, labelled as such:** the lead and the interpretation paragraphs in §1–§3.
- **Excluded.** A Reuters-attributed claim that the NYT, AFP and The Economist joined the SPUR publisher coalition
  could not be confirmed. An undated Sierra $350M round could not be placed in this window. An Arena #1 for Argon
  (1,525 Elo) dates from Oct 2 with preliminary vote counts and is not current.
- **Scraping resilience.** Direct fetches failed (DNS) for `blog.google`, `theneuron.ai`, `marktechpost.com`,
  `thenewstack.io`, `cbsnews.com`, `justice.gov`, `euronews.com`, `substack.com`, `digitalapplied.com` and
  `github.io`. The GitHub REST API was blocked for repos outside this session. `cloud.google.com`, `anthropic.com` and
  `github.com` pages were readable. Everything else comes from the search index, cross-checked across outlets where
  possible.

### Sources (by section)

- **Gemini 4 Argon.** [Google Cloud blog](https://cloud.google.com/blog/products/ai-machine-learning/gemini-4-argon-available-on-google-cloud) · [Google blog, Argon now available](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-argon/) · [Google developers blog](https://blog.google/innovation-and-ai/technology/developers-tools/build-with-gemini-4-argon/) · [Gemini app availability](https://blog.google/innovation-and-ai/products/gemini-app/gemini-4-argon-availability/) · [Reuters via Investing.com](https://www.investing.com/news/stock-market-news/google-launches-flagship-ai-model-gemini-4-argon-for-developers-businesses-4947240) · [9to5Google, Gemini app](https://9to5google.com/2026/10/13/gemini-app-4-argon) · [9to5Google, Antigravity in macOS app](https://9to5google.com/2026/10/13/gemini-app-macos-antigravity/) · [Android Police](https://www.androidpolice.com/gemini-4-argon-available-pro-ultra-subscribers/) · [Digital Trends](https://www.digitaltrends.com/computing/gemini-4-argon-is-finally-available-for-developers-businesses-and-paid-users/) · [Android Authority](https://www.androidauthority.com/gemini-4-argon-ai-model-launch-availability-3722792/) · [MarkTechPost](https://www.marktechpost.com/2026/10/13/google-gemini-4-argon-api-release/) · [The New Stack](https://thenewstack.io/gemini-4-argon-live/) · [Artificial Analysis article](https://artificialanalysis.ai/articles/gemini-4-argon-google-top-three-labs) · [Artificial Analysis on X](https://x.com/ArtificialAnlys/status/2105392625788637299) · [DataCamp](https://www.datacamp.com/blog/gemini-4-argon) · [Emergent, benchmark sources](https://emergent.sh/learn/gemini-4-argon-benchmarks) · [InfoWorld](https://www.infoworld.com/article/4235118/google-positions-gemini-4-argon-for-long-horizon-agentic-work.html) · [The Batch](https://www.deeplearning.ai/the-batch/argon-a-low-hallucination-model-build-for-knowledge-work)
- **OpenAI recording device.** [DOJ press release](https://www.justice.gov/opa/pr/saudi-national-arrested-installing-surreptitious-audio-recording-device-openai) · [Reuters via US News](https://www.usnews.com/news/top-news/articles/2026-10-13/fbi-arrests-former-openai-employee-for-planting-listening-device) · [Washington Post](https://www.washingtonpost.com/technology/2026/10/13/fbi-arrests-openai-employee-allegedly-planting-bug-office/) · [CBS News](https://www.cbsnews.com/news/openai-employee-arrest-recording-device/) · [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/saudi-openai-engineer-arrested-for-allegedly-planting-usd14-recording-device-in-company-office-cheap-microcontroller-was-meant-to-secretly-capture-sensitive-communications-about-the-companys-super-intelligence-technology) · [ABC News (Australia)](https://www.abc.net.au/news/2026-10-14/open-ai-employee-charged-after-alleged-covert-recording/107263252) · [France 24](https://www.france24.com/en/americas/20261013-fbi-arrests-saudi-openai-employee-for-allegedly-bugging-san-francisco-office) · [Al Arabiya](https://english.alarabiya.net/News/united-states/2026/10/14/saudi-openai-engineer-arrested-over-allegedly-installing-recording-device-in-meeting-room) · [Fox Business](https://www.foxbusiness.com/technology/saudi-national-accused-planting-recording-device-openai-executive-conference-room) · [NBC Bay Area](https://www.nbcbayarea.com/news/national-international/openai-engineer-arrest-hidden-listening-device/4157611/)
- **EU AI Act.** [Euronews](https://www.euronews.com/2026/10/14/eus-ai-rules-face-first-enforcement-test-over-lab-incidents) · [Unite.ai](https://www.unite.ai/eu-announces-first-ai-act-enforcement-actions-after-ai-agent-incidents/) · [MLex](https://www.mlex.com/mlex/artificial-intelligence/articles/2536118) · [The Next Web, OpenAI incident report](https://thenextweb.com/news/openai-eu-incident-report-german-wiki) · [Tech Times, RubyGems not reported](https://www.techtimes.com/articles/327760/20260920/rubygems-supply-chain-breach-was-never-reported-brussels-under-eu-ai-act-rules.htm) · [CNBC, Aug enforcement powers](https://www.cnbc.com/2026/08/03/eu-ai-act-enforcement-powers.html)
- **Company news.** [Anthropic, Singapore office](https://www.anthropic.com/news/singapore-office-opening) · [Investing.com, Workday–Anthropic](https://in.investing.com/news/stock-market-news/workday-partners-with-anthropic-to-integrate-claude-ai-93CH-5630860) · [Workday–Google Cloud, May](https://newsroom.workday.com/2026-05-28-Workday-and-Google-Cloud-Expand-Strategic-Partnership-to-Bring-AI-Agents-for-HR-and-Finance-Into-Employees-Daily-Workflows) · [The Decoder, distillation](https://the-decoder.com/anthropic-says-it-cut-claude-reasoning-token-theft-by-up-to-99-in-fight-against-industrial-scale-distillation/)
- **Open weights and research.** [OrcaRouter, Step 5 weights](https://www.orcarouter.ai/blog/step-5-preview-open-weights) · [Forkast, Step 5](https://forkast.news/?p=131752) · [TechCrunch, Mistral Large 4](https://techcrunch.com/2026/10/06/mistrals-new-1t-model-aims-to-leapfrog-closed-and-open-rivals/) · [DailyArXiv, Oct 14](https://github.com/jiangnanhugo/DailyArXiv/issues/571)
- **Tools.** [Claude Code releases](https://github.com/anthropics/claude-code/releases) · [Codex releases](https://github.com/openai/codex/releases) · [Codex issue #48195](https://github.com/openai/codex/issues/48195) · [Let's Data Science, GPT-5.5 retirement](https://letsdatascience.com/news/openai-retires-gpt-55-from-chatgpt-and-codex-1a6f69be)
