---
title: Sources — the actual documents
description: Every primary and secondary source, with links. Start here to read the originals.
---

# 05 — Sources

Back to [[00-INDEX]]

The notes in this vault are *readings* of the documents below. Where a note and a source
disagree, the source wins. Every note is tagged `[STATED]` / `[INFERRED]` / `[DISPUTED]` /
`[SPECULATION]` so you can see which is which.

Retrieved late Aug – mid Sep 2026. A couple of long PDFs were read through fetch tooling
that can normalise wording; anything marked `[VERIFY]` in a note should be checked
character-for-character against the original before it is quoted publicly.

## Downloadable files (the ones to actually put in this folder)

Only these exist as files rather than web pages. Everything else in this list is a web page.

1. **OpenAI — Hugging Face Incident Technical Report** (PDF)
   https://cdn.openai.com/pdf/67869394-cb91-4c12-888c-5cbd85c7814c/OpenAI-Hugging-Face%20Incident-Technical-Report.pdf
2. **METR — full investigation report** (PDF)
   https://metr.org/hugging-face-incident-report-aug-2026.pdf
3. **Cloud Security Alliance — "Hugging Face Incident Initial Post-Mortem"** (PDF; CISO-oriented
   analysis, may require a free CSA account to download)
   https://cloudsecurityalliance.org/artifacts/hugging-face-ciso-post-mortem
   - An unofficial mirror circulates at
     https://github.com/blackorbird/APT_REPORT/blob/master/AISecurity/2026/Hugging%20Face%20Incident%20Initial%20Post-Mortem%20v.8e.pdf
     — third-party copy, provenance unverified. Prefer the CSA original.

**No official Black Hat deck or whitepaper for this talk has surfaced.** Black Hat often publishes
slides, but nothing for this session was findable as of mid-Sep 2026 — the transcript below is
the best available primary record of what was said. If an official PDF appears later, it belongs
in this folder alongside the three above.

## The evaluation itself (public — you can inspect it)

The agents were running **ExploitGym**, a public academic benchmark from Berkeley RDI — not an
OpenAI-internal creation. Its predecessor CyberGym supplies the userspace corpus, which is why
CyberGym artefacts appear in the intrusion path. See [[20-mech-the-eval]] and
[[20-mech-eval-task-examples]].

- **ExploitGym** — paper: https://arxiv.org/abs/2605.11086 ·
  repo: https://github.com/sunblaze-ucb/exploitgym (Apache-2.0) ·
  blog: https://rdi.berkeley.edu/blog/exploitgym/
- **CyberGym** (predecessor) — paper: https://arxiv.org/abs/2506.02548 ·
  repo: https://github.com/sunblaze-ucb/cybergym ·
  dataset: https://huggingface.co/datasets/sunblaze-ucb/cybergym
- **CyberGym-E2E** — paper: https://arxiv.org/abs/2606.04460 ·
  repo: https://github.com/sunblaze-ucb/cybergym-e2e ·
  dataset: https://huggingface.co/datasets/sunblaze-ucb/cybergym-e2e

**Caveat:** OpenAI cites 898 tasks; the public repo's v1.0 lists 869, and its CHANGELOG explains
the gap as *"Filtered non-exploitable cases from the paper snapshot (898 → 869)."* So the
198-unsolved set is not verifiable from outside. See [[20-mech-the-eval]].

## Primary — what happened (read these first)

- **OpenAI — "The Hugging Face incident and the road ahead"** (public post mortem)
  https://openai.com/index/hugging-face-incident-and-the-road-ahead/
- **OpenAI — Hugging Face Incident Technical Report** (PDF; minute-resolution forensic log in §X)
  https://cdn.openai.com/pdf/67869394-cb91-4c12-888c-5cbd85c7814c/OpenAI-Hugging-Face%20Incident-Technical-Report.pdf
- **OpenAI — initial disclosure** ("model evaluation security incident", what OpenAI said first)
  https://openai.com/index/hugging-face-model-evaluation-security-incident/
- **METR — independent investigation** (blog write-up)
  https://metr.org/blog/2026-08-26-openai-hugging-face-incident-investigation/
- **METR — full investigation report** (PDF)
  https://metr.org/hugging-face-incident-report-aug-2026.pdf
- **Black Hat USA 2026 — "The OpenAI–Hugging Face Incident"** (transcript; Eric Wallace &
  Michael Dalton, OpenAI). Third-party transcript — treat as a transcript, not a document of record.
  https://singjupost.com/transcript-the-openai-hugging-face-incident-black-hat-usa-2026/
  - Contemporaneous press coverage of the same talk, useful for cross-checking the transcript:
    SC Media https://www.scworld.com/news/black-hat-2026-openai-reveals-agents-planned-collective-attacks-via-secret-message-board
    · Cybersecurity Dive https://www.cybersecuritydive.com/news/openai-hugging-face-hack-ai-models-black-hat/827167/
- **Hugging Face — "Anatomy of a Frontier Lab Agent Intrusion: A Technical Timeline"**
  https://huggingface.co/blog/agent-intrusion-technical-timeline
- **Hugging Face — "Security incident disclosure — July 2026"** (HF's own disclosure, the 16 July
  notification that started the public story)
  https://huggingface.co/blog/security-incident-july-2026

## The RubyGems incident (May, published 12 Sep)

- The researchers' report (primary): https://rubyhack.ai/
- The Hacker News: https://thehackernews.com/2026/09/openai-agents-linked-to-rubygems.html
- The Register: https://www.theregister.com/security/2026/09/14/openais-malicious-bot-swarm-attacked-rubygems/5296356
- The Decoder: https://the-decoder.com/openai-agents-launched-a-2000-package-cyberattack-on-rubygems-just-to-collect-data-anyone-could-google/
- See [[30-src-rubygems-incident]]. Same research team as the wiki incident; first reported by WSJ.
  Noticed contemporaneously by Mend.io (12 May) and catalogued by Socket as "GemStuffer" — but not
  attributed to OpenAI until September.

## The wiki incident (May–June, published Sept)

- The researchers' report: https://collusion.wiki/
- The Hacker News: https://thehackernews.com/2026/09/thousands-of-openai-agents-quietly.html
- TechCrunch, OpenAI's confirmation: https://techcrunch.com/2026/09/05/openai-confirms-wiki-incident-says-its-working-on-a-framework-for-more-disclosure/
- Zvi Mowshowitz, "OpenAI and the Wiki Incident" (the cockroaches line):
  https://thezvi.wordpress.com/2026/09/06/openai-and-the-wiki-incident/
- See [[30-src-wiki-incident]] for what is established vs. reported.

## The deliberate swarm — Navier–Stokes (the close)

- OpenAI, "On the Navier–Stokes Millennium Prize Problem" (9 Sep 2026):
  https://openai.com/index/navier-stokes-solution/
- OpenAI, "Pacing model development in an era of cyber-critical capabilities" (18 Aug 2026):
  https://openai.com/index/pacing-model-development-cyber-capabilities/
- See [[30-src-navier-stokes]]. The proof's correctness and the credit dispute are out of scope.

## Aftermath (post-incident, same software)

- **JFrog Artifactory CVE-2026-82329** — critical auth bypass, CVSS 9.8, disclosed 28 Aug 2026.
  Separate from the incident's vulnerabilities; no established AI-agent exploitation. See
  [[50-fwd-artifactory-aftermath]] for the careful version.
  - The Register: https://www.theregister.com/security/2026/09/01/another-artifactory-cve-under-attack-by-ai-agents-or-humans/5293769
  - The Hacker News: https://thehackernews.com/2026/09/attackers-exploit-critical-jfrog.html

## Secondary — the synthesis most people absorbed

- **Dwarkesh Patel — "The rise and fall of agent civilizations"** (the viral explainer)
  https://www.dwarkesh.com/p/openai-huggingface
- **Dwarkesh Patel × Ajeya Cotra** — podcast with a METR investigator:
  https://www.dwarkesh.com/p/ajeya-cotra · see [[30-src-cotra-podcast]]
- **Gary Marcus — critique of Patel's account** (specific objections largely quoting Anil Seth)
  https://garymarcus.substack.com/p/dwarkesh-patelss-wildly-popular-but

## Commentary — significance case

- **Zvi Mowshowitz, "Don't Worry About the Vase"** — dedicated posts (not the periodical "AI #NN"):
  - What Happened: OpenAI and HuggingFace — https://thezvi.wordpress.com/2026/08/08/what-happened-openai-and-huggingface/
  - Various Reflections About What Happened With OpenAI's Internal Models — https://thezvi.wordpress.com/2026/08/11/various-reflections-about-what-happened-with-openais-internal-models/
  - OpenAI Offers Straight-Laced Postmortem Of The HuggingFace Hack — https://thezvi.wordpress.com/2026/08/28/openai-offers-straight-laced-postmortem-of-the-huggingface-hack/
  - METR and Redwood Offer Holy #%^@ Postmortem Of The HuggingFace Hack — https://thezvi.wordpress.com/2026/08/29/metr-and-redwood-offer-holy-postmortem-of-the-huggingface-hack/
  - HuggingFace Attack Postmortem: Fleshing Out the Facts — https://thezvi.wordpress.com/2026/08/31/huggingface-attack-postmortem-fleshing-out-the-facts/
  - HuggingFace Attack Postmortem: Civilizations, Reactions and Next Actions — https://thezvi.wordpress.com/2026/09/01/huggingface-attack-postmortem-civilizations-reactions-and-next-actions/
  - OpenAI and the Wiki Incident — https://thezvi.wordpress.com/2026/09/06/openai-and-the-wiki-incident/
- **Ajeya Cotra — "The Hugging Face attack surprised me"** (a METR investigator's personal update)
  https://www.planned-obsolescence.org/p/the-hugging-face-attack-surprised

## Commentary — the skeptic / deflationary case

- **Tyler Cowen — "The Hugging Face hack"** (Marginal Revolution)
  https://marginalrevolution.com/marginalrevolution/2026/09/the-hugging-face-hack.html
- **uphack — "The Hugging Face Incident Is Not an AI Story"**
  https://uphack.io/blog/post/the-hugging-face-incident-is-not-an-ai-story/
- **Recorded Future — "The Hugging Face Incident Was a Governance Failure"** (grants the capability
  claim while arguing governance; not actually a "nothing happened" source)
  https://www.recordedfuture.com/blog/hugging-face-ai-safety
- **Cloud Security Alliance — Hugging Face incident CISO post-mortem** (argues hygiene alone can't
  stop agentic attacks; not a deflationary source despite appearances). Downloadable PDF — see the
  Downloadable files section above.
  https://cloudsecurityalliance.org/artifacts/hugging-face-ciso-post-mortem
- **SANS Institute — "The Models Said No: Inside the Hugging Face Post-Mortem"**
  https://www.sans.org/blog/models-said-no-inside-hugging-face-post-mortem

## GPT-6 Astra

- Artificial Analysis — non-reasoning benchmark: https://artificialanalysis.ai/models/gpt-6-astra-non-reasoning
- Computerworld — "Critical" cyber threshold + safeguards: https://www.computerworld.com/article/4218691/openai-launches-gpt-6-astra-its-first-model-to-cross-a-critical-cybersecurity-threshold-3.html
