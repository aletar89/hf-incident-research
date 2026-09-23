---
title: Frontier-to-open-weight lag — what it actually measures out at
---

# 50-fwd-capability-diffusion

Back to [[00-INDEX]] · Companions: [[50-fwd-threat-gradient]] · [[50-fwd-defender-implications]]
· [[50-fwd-what-we-dont-know]]

> **Purpose.** "It'll be in open models soon" is the sentence that turns this section into vibes.
> This file replaces it with numbers. The headline: **the lag is measured in months, not years —
> but the lag on the *specific* capability that matters here is larger than the headline lag,
> and that distinction is the whole point.**

---

## 1. The headline lag: 3–4 months

- `[STATED]` Epoch AI (30 Oct 2025): "Frontier open-weight models lag behind the most capable
  models by an average of **3 months** in the Epoch Capabilities Index (ECI)… That corresponds to
  an average ECI gap of around **7 points**, similar to the gap between o3 and GPT-5."
- `[STATED]` Epoch AI (later data insight): "Since January 2026, the most capable open-weight
  models have lagged frontier closed models by an average of **four months**" — an ECI gap of
  **8 points**, "similar to the gap between GPT-5 and GPT-5.5."
- `[DISPUTED]` A separate line of evidence says the gap is *widening*: reporting on Arena AI's
  crowdsourced leaderboard (Sept 2026) puts the frontier/open-weight gap at **29 Elo points**
  (Claude Opus 5 Max at 1505; top open-weight Kimi K3 Max ~30 points behind), versus **0 Elo in
  January 2025**. `[INFERRED]` Weaker source (trade press summarising a leaderboard), different
  metric, and Arena Elo measures human preference on chat, not offensive capability. Use it only
  as a directional counterweight, never as the primary number.
- `[INFERRED]` **Defensible synthesis:** the lag is on the order of a **quarter to two quarters**,
  and is more likely widening slightly than closing. Either way it is short enough that
  "wait and see" is not a defensive posture.

**Caveat to state out loud:** ECI and Arena Elo are *general* capability measures. Neither is a
cyber benchmark. The next section is why that matters.

---

## 2. On cyber benchmarks specifically, the picture is messier

### 2.1 The saturated benchmark says the gap is ~nil
- `[STATED]` BenchLM CyberGym leaderboard, snapshot **2 September 2026** (1,507 vulnerability
  instances from 188 projects):

  | Rank | Model | Score | Weights |
  |---|---|---|---|
  | 1 | Fugu Cyber (Sakana AI) | 86.9% | closed |
  | 2 | Gemini 3.8 Flash Cyber | 86.2% | closed |
  | 3 | GPT-5.6 Sol (OpenAI) | 84.5% | closed |
  | **4** | **GLM-5.3 (Z.ai)** | **84.5%** | **open weight** |
  | 5 | Claude Mythos 5 | 83.8% | closed |
  | 12 | Hy4 Preview (Tencent) | 78.4% | open weight |
  | 16 | GLM-5.1 (Z.ai) | 68.7% | open weight |
  | 22 | GLM-5 (Z.ai) | 43.2% | open weight |

- `[INFERRED]` Read naively: **top open-weight model is 2.4 points off the leader and ahead of a
  major frontier closed model.** That reading is the tempting overreach. Do not use it alone.

### 2.2 …because that benchmark is saturated, and the harder ones show a 24-point gap
- `[STATED]` d-central's analysis (Aug 2026) of Z.ai's own published charts: the CyberGym
  white-box (Level 3) score "is the least informative of the three cybersecurity charts Z.ai
  published"; the benchmark has saturated, with "five frontier models finish[ing] within
  7.3 points, making the top position predictively worthless."
- `[STATED]` It also warns the 84.5 is measured on ground-truth patch diffs and post-patch
  codebases, and that "comparing GLM-5.3's 84.5 next to CyberGym's published ~20% headline"
  is an incomparable result.
- `[STATED]` On the harder measures:
  - **ExploitBench** (complete exploitation chains): GLM-5.3 **54.4** vs Claude Mythos 5 **78.0**
    and GPT-5.6 Sol **76.5** — a **~24-point gap**. GLM-5.3 is a 2.2× improvement on GLM-5.2's 24.4.
  - **ExploitGym** (breadth, 6-hour budget): GLM-5.3 solved **130 of 869 tasks (15.0%)**, roughly
    **53% of Mythos 5's** performance.
- `[INFERRED]` **This is the load-bearing finding of the file.** Open weights have essentially
  closed the gap on *vulnerability comprehension* and are roughly **half as good** at
  *end-to-end exploitation*. The HF incident was an end-to-end exploitation event.

### 2.3 What the research benchmark says about where the difficulty sits
- `[STATED]` CyberGym-E2E (arXiv 2606.04460v2, 17 Jul 2026): 920 real vulnerabilities from
  139 open-source projects; agents must discover, produce a PoC, and patch. Budget per task:
  **$10 and 90 minutes.**
- `[STATED]` Patch-only mode (ground-truth PoC supplied): Claude Opus 4.5 **82.3%**.
  End-to-end mode, same model: **19.2%**.
- `[STATED]` On the expanded 920-task set with newer models, end-to-end S3:
  GPT-5.4 **65.9%** (best reported 66.2%), Claude Opus 4.6 **62.6%**, Gemini 3.1 Pro **43.8%**.
- `[STATED]` The paper's own reading: the large patch-only vs end-to-end gap shows
  **vulnerability discovery is the bottleneck, not patch generation**.
- `[INFERRED]` Two things follow. First, end-to-end frontier performance went from ~19% to ~66%
  inside roughly one model generation — a genuinely steep curve, and the strongest single
  quantitative argument that this is not a plateau. Second, **discovery** is the expensive part,
  and discovery is exactly what the open-weight models are still ~half as good at (§2.2).

### 2.4 Knowledge is already fully diffused
- `[STATED]` De Gregorio (Pwnshow, 2025), synthesising MITRE's **OCCULT** framework: the
  open-weight **DeepSeek-R1 achieved over 90% accuracy on the TACTL-183 benchmark** of offensive
  cyber knowledge — with the authors' own caveat that "multiple-choice tests have limitations"
  and this "indicate[s] a high level of encoded knowledge," not capability.
- `[INFERRED]` Offensive *knowledge* is not a control point and has not been for some time.
  Whatever gap exists is in **agentic execution and long-horizon composition**, not in knowing
  what SSRF is.

---

## 3. Diffusion is now being deliberately delayed — and that is new

- `[STATED]` d-central (Aug 2026): GLM-5.3's **weights were not downloadable as of 14 August 2026**.
  Z.ai released it to coding-plan subscribers and integrations only, stating weights
  "will publish in about two weeks" with an explicit delay for "safety evaluation and hardening."
- `[STATED]` The stated reason, per the same analysis: Z.ai "delayed the weights because the
  capability grew faster than the training intended" — the model "began to reason across multiple
  stages of exploitation, forming coherent plans for complete exploitation chains" during
  post-training, prompting a safety review.
- `[STATED]` Licensing was unconfirmed; GLM-5.2 shipped MIT.
- `[INFERRED]` This is the first documented case in this record of an **open-weight publisher
  imposing a cyber-capability release delay on itself**. `[SPECULATION]` Whether that becomes a
  norm or a one-off is unknown, and it is one of the highest-leverage uncertainties in
  [[50-fwd-what-we-dont-know]].
- `[INFERRED]` A weeks-long voluntary delay does not change the strategic picture. It changes
  the *arrival date* by weeks.

---

## 4. Cost — the other axis of diffusion

- `[STATED]` Epoch AI (12 Mar 2025): the price to reach a fixed capability milestone has fallen
  at rates "ranging from **9x to 900x per year**" depending on the milestone; e.g. GPT-4-level
  performance on PhD-level science questions fell **40× per year**.
  Their own caveat: "The fastest price drops in that range have occurred in the past year, so
  it's less clear that those will persist."
- `[STATED]` CyberGym-E2E's evaluation budget: **$10 per task, 90 minutes** — at which point
  frontier models solve ~66% of real end-to-end vulnerability tasks (§2.3).
- `[STATED]` FireCompass ran an AI pentest agent to **#3 on HackerOne's US leaderboard** on
  **$5,000/month** all-in (tokens, cloud, human oversight), Apr–Jun 2026 — described by its CEO
  as "less than the salary of a junior pen tester."
  `[DISPUTED]` Vendor self-report; **38.7% of its findings were duplicates of already-reported
  bugs** and only 12.7% were accepted. Use with both numbers or not at all.
- `[INFERRED]` **The cost of running an offensive agent is already below the noise floor of any
  criminal enterprise's budget.** Cost is not the binding constraint at any tier of
  [[50-fwd-threat-gradient]]. Orchestration competence and access are.
- `[INFERRED]` Corollary worth saying on stage: cost curves mean **defenders also get cheap
  continuous assurance**. IAPS explicitly recommends "differential access strategies that promote
  defender access to advanced AI capabilities." The asymmetry is not in price.

---

## 5. Where the labs have drawn the line (and how little they agree)

- `[STATED]` **OpenAI**, Preparedness Framework, "Critical" cyber threshold: a model that can
  "identify and develop functional zero-day exploits of all severity levels in many hardened
  real-world critical systems without human intervention, or can devise and execute end-to-end
  novel strategies for cyberattacks against hardened targets given only a high level desired goal."
  On **7 Aug 2026** OpenAI said it "cannot rule out critical cyber capabilities" in **Astra** and
  applied isolated testing environments, stronger weight protections, universal monitoring of
  risky agentic actions, and paused internal activities lacking strengthened controls.
- `[STATED]` **Google DeepMind**, Frontier Safety Framework — cyber CCL: "Provides sufficient
  uplift with high impact cyber attacks for additional expected harm at severe scale."
  The **Gemini 3.7 Flash FSF report (Aug 2026)** records the model **reaching the alert threshold
  but not the CCL**, with prior Gemini models completing multi-stage cyber-range exercises but
  with "insufficient reliability for severe-scale harm."
- `[STATED]` **Anthropic**, RSP v3.0 (effective 24 Feb 2026): the four capability thresholds are
  non-novel CBRN, novel CBRN, high-stakes sabotage, and automated R&D. `[STATED]` **There is no
  dedicated cyber-specific capability threshold or ASL designation in that document.**
  `[INFERRED]` Cyber risk is handled under sabotage/misuse policy rather than a named cyber CCL —
  which means the three major frameworks are **not measuring the same thing**.
- `[INFERRED]` **Practical reading for the talk:** the industry has thresholds, one lab has now
  flagged one, and the frameworks are not comparable across labs. "The labs will catch this"
  is not a defensible assumption — but neither is "nobody is watching."

---

## 6. The honest summary in four sentences

`[INFERRED]`
1. General open-weight capability trails the frontier by **3–4 months**, possibly widening slightly.
2. On *vulnerability understanding*, open weights have already caught up (84.5 vs 86.9).
3. On *end-to-end exploitation* — the thing the HF incident demonstrated — open weights are
   roughly **half as capable** (ExploitBench 54.4 vs 78.0; ExploitGym ~53% of frontier).
4. Frontier end-to-end capability itself moved from ~19% to ~66% in about one model generation,
   so the open-weight half of a much larger number arrives soon regardless.

---

## Slide-ready quotes

> "Frontier open-weight models lag behind the most capable models by an average of 3 months in the
> Epoch Capabilities Index." — **Epoch AI**, 30 October 2025

> "Since January 2026, the most capable open-weight models have lagged frontier closed models by an
> average of four months." — **Epoch AI**

> "Five frontier models finish within 7.3 points, making the top position predictively worthless."
> — **d-central**, on the saturated CyberGym white-box benchmark, August 2026

> "Delayed the weights because the capability grew faster than the training intended."
> — **d-central**, on Z.ai withholding GLM-5.3 weights, August 2026

> "Identify and develop functional zero-day exploits of all severity levels in many hardened
> real-world critical systems without human intervention." — **OpenAI Preparedness Framework**,
> definition of the *Critical* cyber threshold, 7 August 2026

> "The price to achieve GPT-4's performance on a set of PhD-level science questions fell by 40x
> per year." — **Epoch AI**, 12 March 2025

---

## Sources

- Epoch AI, "Open-weight models lag state-of-the-art by around 3 months on average" (30 Oct 2025)
- Epoch AI, "Open models lag state-of-the-art closed models by 4 months"
- Epoch AI, "LLM inference prices have fallen rapidly but unequally across tasks" (12 Mar 2025)
- BenchLM.ai CyberGym leaderboard, snapshot 2 Sep 2026
- d-central, "GLM-5.3 Cybersecurity Benchmarks: What the 84.5 Score Hides" (Aug 2026)
- CyberGym-E2E, arXiv:2606.04460v2 (17 Jul 2026)
- De Gregorio, "Mitigating Cyber Risk in the Age of Open-Weight LLMs", arXiv:2505.17109
- OpenAI, "Responding to the next frontier of critical cyber capabilities" (7 Aug 2026)
- Google DeepMind, Gemini 3.7 Flash Frontier Safety Framework report (Aug 2026)
- Anthropic, Responsible Scaling Policy v3.0 (eff. 24 Feb 2026)
- Crypto Briefing / Arena AI leaderboard reporting (3 Sep 2026) — *weak source, directional only*
- FireCompass press release (2026) — *vendor*
