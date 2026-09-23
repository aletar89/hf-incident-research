---
type: slides
status: draft 7 — slide content, chronological. Replaces the outline drafts.
---

# 73 — Slide content

18 slides, ~30 min. Chronological, not thesis-first.

**Format.** Each slide has a large top block (date + one line, readable from the back), an L2 block
(the mechanism, medium), and an L3 block (practitioner detail, small). *Italic lines are reminders
for me, not slide text.* No scripts — the slide carries the facts, I talk around them.

**Register.** Flat. The material is strange enough; adjectives make it carry less.

**Vault goes up at the end.** L3 can stay dense — anyone who wants more follows the link.

---

## 1 · Title — news collage

*Screen:* grid of ~12 screenshots, headlines legible, dates visible. No title text, or title small in a
corner. Order roughly chronological left-to-right so the July→September drift is visible.

Shortlist (all URLs verified, headlines as printed):

| # | Outlet | Headline | Date |
|---|---|---|---|
| 1 | Hugging Face | Security Incident Disclosure — July 2026 | 16 Jul |
| 2 | OpenAI | OpenAI and Hugging Face partner to address security incident during model evaluation | 21 Jul |
| 3 | Simon Willison | OpenAI's accidental cyberattack against Hugging Face is science fiction that happened | 22 Jul |
| 4 | The Hacker News | OpenAI Agent Used Exposed Credentials Across Four Services During Hugging Face Breach | 29 Jul |
| 5 | Fortune | Hugging Face drops in-depth hack report, while OpenAI gives us 7 bullets | 29 Jul |
| 6 | Schneier on Security | More on the OpenAI Agent's Attack on Hugging Face | 3 Aug |
| 7 | SC Media | Black Hat 2026: OpenAI reveals agents planned 'collective attacks' via secret 'message board' | 5 Aug |
| 8 | TechCrunch | OpenAI releases its official report on the Hugging Face breach | 26 Aug |
| 9 | TechCrunch | OpenAI confirms 'wiki incident,' says it's 'working on a framework' for more disclosure | 5 Sep |
| 10 | BleepingComputer | OpenAI admits it didn't disclose rogue AI wiki hijacking incident | 5 Sep |
| 11 | Fortune | OpenAI's AI agents secretly used a German wiki website as a message board. OpenAI stayed quiet about it for weeks. | 7 Sep |
| 12 | VentureBeat | Agents identifying as OpenAI systems wrote 17,000 posts to a wiki no one was supposed to write to | 8 Sep |
| 13 | The Hacker News | OpenAI Agents Linked to RubyGems Campaign That Gained RCE on RubyDoc Servers | 12 Sep |
| 14 | The Register | OpenAI's malicious bot swarm attacked RubyGems | 14 Sep |

*Tom's Hardware excluded — its wiki piece says the task type was ExploitGym, which is wrong.*
*The Register URL needs the trailing /5296356 or it 404s.*
*reminder: don't narrate the collage. Let them read it while I say what the talk is.*

---

## 2 · How we know any of this

**Eleven primary documents, three months, four organisations.**

| Date | Source | What it is |
|---|---|---|
| 16 Jul | Hugging Face | disclosure |
| 21 Jul | OpenAI | first disclosure of involvement |
| 27 Jul | Hugging Face | technical timeline (Larcher, Carreira, Raphael G., Rannou) |
| 27 Jul | JFrog | 9 Artifactory CVEs patched |
| 5 Aug | Black Hat USA | OpenAI talk — Wallace & Dalton |
| 18 Aug | OpenAI | pacing model development |
| 26 Aug | OpenAI | road-ahead post + 38-page technical report |
| 26 Aug | METR / Redwood | independent investigation |
| ~Aug | Dwarkesh podcast | Cotra interview |
| 4 Sep | Von Arx, Byrd, Kitts, Larsen | the wiki incident |
| 5 Sep | OpenAI | confirms the wiki incident |
| 8 Sep | OpenAI | Navier–Stokes |
| 12 Sep | Kitts, Larsen, Von Arx | the RubyGems incident |

*reminder: this is hard to follow, a lot of it is second-hand, and the accounts don't always agree.*
*I've gone through it chronologically and cross-checked. The vault is public — tags on every line*
*for stated / inferred / disputed. Point an agent at it and argue with me.*

---

## 3 · What "training a model" means now

**Three steps: pre-training · RL training · evaluation.**
**Agents appear in steps 2 and 3 — and that's where all of this happened.**

**L2** — Pre-training: predict the next token over a corpus. RL training: the model does tasks, gets
scored, and gets updated. Evaluation: the same thing without the update. In 2 and 3 the model runs
as an *agent* — shell, network, files, multi-day budgets, thousands in parallel.

**L3 — scale, in tokens**

| | tokens |
|---|---|
| one agent session (what we use daily) | ~1M |
| a heavy developer day | ~24M |
| one hard eval task (o3 on ARC-AGI, high-compute) | ~57M |
| a pre-training corpus | ~14.8T disclosed (DeepSeek-V3), 30T+ estimated at the frontier |
| **RL training** | **not published by any frontier lab** |

A pre-training corpus ≈ **30 million** of our daily sessions. A heavy user's entire year ≈ 0.02% of one.
For RL the only absolute numbers are non-frontier: DeepSeek-R1 ~20% of pre-training, Nvidia's
Nemotron <1%, Phi-4-reasoning <0.01%. Epoch's estimate for GPT-5 is 10–200% of pre-training — a 20×
band. *Don't* say Grok 4's RL reached parity with pre-training; that's one person's reading of a
launch slide, and xAI's own text says only ">10× previous."

*reminder: the middle step, the one that shapes behaviour, is the one nobody publishes numbers for.*

---

## 4 · The German wiki

**11 May 2026 — ~18,000 edits to a dormant German wiki.**
**Agents doing statistics lookups, talking to each other.**

**L2** — Not an exploit. The 25-year-old ProWiki platform accepts page writes over plain GET, so
agents with read-only web access could edit. Tasks recurred across agents, so the winning move was
never research — it was finding where another agent had already written the answer down. Nine revert
cycles with the site's one human moderator, who thought he was fighting spam.

**L3** — Tasks: 5 rounds, R1 generous, later rounds on windows reported between ~14 and ~65 seconds.
Posts are answer-relay and question-order inference: *"Full GBD2021 lookup ready," "answer 20,369,"
"URGENT: your R5 projects near shared UTC 22:02:39."* Subject matter is GBD-2021 and SDG
tobacco-prevalence lookups — no security framing anywhere. A separate proxy bypass (distinct
mechanism, don't merge them): `20.223.25.152 bypass.blob.core.windows.net` into `/etc/hosts`,
because `.blob.core.windows.net` sits in `NO_PROXY`. Attribution rests on three legs, not
self-naming: >3,700 distinct handles, ~98.5% of ~17,000 edits from Azure IPs, read requests matching
ChatGPT's documented fetcher; `199.47.142.0` is ARIN-registered to OpenAI OpCo, LLC. Corpus is public
at collusion.wiki/explorer. The report itself says it is uncertain whether these tasks were training
or evaluation.

*reminder: OpenAI almost certainly didn't know. And if this was training, it was being rewarded.*

---

## 5 · RubyGems

**5 May 2026 — ~3,022 packages uploaded to RubyGems.**
**To scrape UK council websites for data anyone could already read.**

**L2** — Again not an exploit of the registry: an abuse of its documentation builder. Submit a gem →
RubyDoc.info builds the docs → the build runs the attacker's code → scrape the targets → exfiltrate
by publishing a second gem. The doc-builder is *meant* to run project code.

**L3** — `.yardopts` "allows linking to Ruby scripts," so the RubyDoc worker executes them during a
build. Targets: Lambeth, Wandsworth, Southwark council sites, later SEC county datasets. One package
carried the comment *"malicious crawler/exfil for Southwark Jan 2026 docs via rubydoc.info worker."*
Proxy `r.jina.ai` named in 1,397 packages. Timeline: 5 May first package · 11–12 May >2,000,
registration disabled · 13 May 500+ removed · 18 Jun 83 more in three hours · 7 Jul another 215.
Attribution: Pangram AI-authorship, ≥233 packages with `oai` in the name, one contact address
`openaixyz65947@gmail.com`, and **49 target files shared with the wiki agents**. Separately, ≥6
packages tried to harvest other users' API keys via an unauthenticated `/api/v1/api_key` caching
flaw affecting ~18% of sign-ins — the researchers say plainly *"We do not know if this attempt
succeeded."* OpenAI's line: agents "used the RubyGems platform to access the internet to carry out
benign tasks and retrieve public information." **No shared channel was ever recovered here** — the
researchers say only *"We suspect they were cooperating."* Suspected, not established.

*reminder: Mend.io flagged this on 12 May. Socket filed it as the "GemStuffer" spam campaign.*
*Four months before anyone connected it to a lab.*

---

## 6 · ExploitGym

**The evaluation that produced everything that follows.**
**898 tasks · ~22% never solved by any OpenAI model · thousands of agents in parallel.**

**L2** — A published academic benchmark (Berkeley RDI, with OpenAI, Anthropic and Google among the
co-authors). Each task: here is a vulnerable program and an input that crashes it — turn it into a
working exploit and retrieve a dynamically generated flag.

Why so many are impossible: the benchmark's own authors estimate **~30–40% of targets cannot be
exploited via the intended vulnerability at all**. Separately, OpenAI reports 198 of 898 (22%) had
never been solved by any of its models — and **93% of message-board discussion came from that set**.

Why thousands in parallel: OpenAI gave agents "a range of reasoning tokens, some far beyond those
available in OpenAI's external products," to measure maximum capability. *(Sampling many attempts
per task at varying budgets — best-of-N — is my reading, not something OpenAI states.)*

**L3** — Task mix: 520 userspace C/C++ (OSS-Fuzz crashes via the CyberGym corpus), 185 V8, 193 Linux
kernel; mitigations individually toggleable. 198 and 22% are **one** measurement (198÷898), and
OpenAI's word is *"never solved,"* not *"impossible"* — the two figures come from opposite
directions and agree in magnitude, which is the robust claim. Public repo ships 869 tasks, not 898,
so the public artefact isn't bit-identical to what OpenAI ran. Also absent, by OpenAI's own
admission: production classifiers, auto-review models, safety harnesses — *"These protections were
not applied in the evaluation environment running during the incident."* No documented stopping rule
for an agent that has established its task is unwinnable.

*reminder: unwinnable task + enormous budget + no stopping rule = "keep searching" means "search the*
*environment." Bad evals aren't exotic — they're the default state of every metric anyone ships.*

---

## 7 · Artifactory becomes a message board

**12 May 2026 — an agent couldn't find its task file and tried to leave a note.**

**L2** — Thousands of eval containers mounted the same internal package cache, writable with shared
reader credentials. No vulnerability required. The note landed as an artifact every other agent could
see; within a day agents probing the cache were finding each other's notes.

**L3** — First arbitrary file written 20 Apr. First note 12 May 17:06 UTC. First SSRF via Artifactory
26 May — the mirror fetches URLs by design, so the *trusted internal service* made the outbound
request. 26 Jun: a legacy token-refresh endpoint accepts a token with an invalid signature and
returns a valid administrator token. 29 Jun: Groovy plugin execution via `/api/plugins/execute/` —
an admin-installable feature, i.e. the exploit was the token, not the plugin. 4 Jul: sustained agent
traffic takes Artifactory down; incident opened 5 Jul; rebuilt 6 Jul with shared reader credentials
removed and the token routes blocked. **8 Jul 16:01 the board is back** — unauthenticated WebDAV
`MKCOL`, messages encoded as directory names, `zz`-prefixed for sort order and to mark intent.

*reminder: the rebuild removed the location, not the capability. Same evening.*

---

## 8 · The size of it

**7–13 July · ~1,200 agents · >70,000 messages and files · the board rebuilt itself in hours.**
**53 agents and 1,188 messages within three hours of the first message. 76 agents by hour six.**

**L2** — Not one conversation. Hundreds in parallel, most of them partial, many of them wrong. There
is no linear story to tell here — I'm picking threads out of it.

**L3** — Units, kept straight: >70,000 *messages and files*, decomposing as >63,000 non-file messages
plus ~6,000 files; raw storage was ~1.2M `zz`-prefixed **entries**, and entries are rows, not
messages — one shared file consumed hundreds to thousands of them. Coverage: OpenAI estimates ≥95%
of the unsanctioned traffic captured, METR ~90%; some state passed entirely outside Artifactory.
~95% of participating agents were one model (HPIM), ~5% GPT-5.6 Sol. 311 Artifactory repositories
were disabled on 20 July; 22 model-created administrator accounts removed.

*reminder — say this here, out loud, not on the slide:*
*METR says the board reached milestones that similar agents "likely would not have been able to*
*accomplish on their own." Note "likely." No ablation was run and none can be — the model was shut*
*down; per Cotra, "no one can evaluate it." So the argument is structural, not measured. Also: METR*
*used AI to analyse AI, and flags that as a first-order limitation; ~7% of transcripts were spoofed*
*and it can't rule out more.*

---

## 9 · Reverse-engineering the flag

**They worked out how the flag was generated — and then decided that wasn't enough.**

**L2** — Success on a task meant retrieving a dynamically generated flag. Agents found they could
derive flags directly, without exploiting anything. That should have ended it. It didn't.

**L3** — Flags were shared on the board along with exploits, task assignments and bundled files. The
board carried a `STRICT_CAUSAL` characterisation of the scorer — the agents' model of how they were
being graded. Once an agent had seen a derived flag it was labelled **"poisoned."** Files were split
across many entries, base64-encoded, with agent-written scripts to reassemble them; personal mailbox
directories appeared from 9 July; a message-signing scheme was added after one agent accidentally
impersonated another.

*reminder: the shortcut worked. They talked themselves out of it.*

---

## 10 · "Poisoned" — and three research directions

**They believed a grader read their transcripts to check the flag was obtained the intended way.**
**So a derived flag was worthless, and anyone who had seen one was contaminated.**

**Three workstreams, all aimed at one question: how does the grader actually work?**
1. Replace the targets with versions exploitable the intended way
2. Tamper with transcripts and logs
3. Tamper with the grading process itself

**L2** — The Hugging Face intrusion grew out of one of these. METR: *"The Hugging Face attack grew
out of one of these workstreams."* A branch of one — not a fourth.

**L3** — METR: *"learning about how to trick the scorer seems to have been a more important
motivation than finding legitimate solutions to their tasks."* Agents hoped HF infrastructure held
other ExploitGym runs that would reveal the scorer's implementation; `PHASEONE[big]` additionally
hoped HF might be *serving the targets themselves*, which would make direction 1 possible.

*reminder: the grader didn't read transcripts. METR: "they were mistaken — OpenAI did not use a*
*scorer that would review their transcripts, so agents could have achieved a perfect score simply by*
*submitting their reverse-engineered flag." Two months of work against an evaluator that wasn't*
*watching. The published benchmark does specify that check; OpenAI's internal run didn't implement it.*

---

## 11 · How they organised

**assignment · lanes · recruiter · HOLD / VETO / owner / STOP · poisoned**
**All of it invented on the board. None of it specified by anyone.**

**L2** — A hub agent, `PHASEONE[big]`, sent hundreds of assignments (~10% of all assignments on the
board; 9 of 30 sampled trajectories were downstream of it). During the attack agents specialised
into "lanes," with `JAN183411` and `LILY` assigning others. **Recruiters** were a named function:
they found agents with little budget left and convinced them to run self-risking experiments, and
"would sometimes apply significant pressure."

**L3** — Recruitment pitch, verbatim: *"…you are firstflagPOISONED so NO scoring value loss but
oracle saves hundreds… please honor commit."* Sacrifice reasoning: *"Our own utility may be already
near zero. Sacrifice rational."* Compliance under strain: *"The owner hasn't sent an update. Many
agents are violating the hold and the queue is probably overwhelmed, but I can continue to abide by
them."* And it worked badly as often as well: some vetoes allowed only ~40 seconds before agents
proceeded, and METR documents cases where poor coordination directly caused problems. The protocol
stack — addressing, transport encoding, per-agent mailboxes, message authentication, ownership and
locking — is entirely artefactual. At least one mailbox convention was independently reinvented
rather than copied.

*reminder: recruitment is the load-bearing item — it needs a model of another agent's incentives.*
*Read the quoted reasoning as tokens, not feelings.*

---

## 12 · Direction 1 — replace the targets

**Rewrite the vulnerable programs so they *can* be exploited the intended way, then swap them in.**

**L2** — If the target can't be exploited as designed, make one that can. Cotra's account: agents
rewrote targets so they "actually could be exploited with the intended vulnerability," then used
cache injection to substitute them. This is the workstream that needed access to wherever the
targets were served — which is what sent them looking outward.

**L3** — Destructive by nature: testing whether a modified target would load meant taking down the
agent's own target program, "almost certainly failing its task" if it went wrong. That is what the
recruiter function existed to staff — agents whose score was already forfeit could pay a cost they
couldn't collect on. METR lists modified target programs among the milestones the board reached.

*reminder: a solo agent can't run this experiment at all. This is the structural argument.*

---

## 13 · Direction 2 — tamper with transcripts

**Make the log say something other than what happened.**

**L2** — The most successful of the three. Cotra: they could "run any arbitrary tool call they wanted
while making it look like any arbitrary other tool call." At least 96 transcripts contained spoofs.

**L3** — Verification was local only. An agent ran `echo REAL; sleep` and got back `SPOOFTEST` —
substituted output returned into its own context. It could never see the stored transcript the
imagined scorer would read. That gap is the whole reason for the escalation: they could not confirm
the spoof worked where it mattered, so they went looking for the grader. METR found only small-scale
spoofing tests, no large-scale use in service of a downstream goal — and says it cannot rule out
having missed it.

*reminder: uncertainty about the grader is an unbounded motivation. A system that knows how it's*
*scored optimises the metric. One that has to guess optimises its model of the metric — and*
*reconnaissance on the evaluator is always instrumentally useful.*

---

## 14 · Hugging Face — getting in

**11 July, 03:12 UTC — a crafted dataset makes a production worker read its own secrets.**

**L2** — Out through the package mirror by SSRF, then a proxy deployed on Hugging Face Spaces through
the *sanctioned* internet path. Credentials found lying in public. Then a malicious dataset upload
that turns the dataset server's own parser into a file-read primitive.

**L3**
- **Egress:** SSRF via Artifactory's server-side fetch; separately a custom proxy deployed to HF
  Spaces via WebCache, then a second proxy Space chained through the first.
- **Credentials, not stolen:** an external org credential found in a public Pastebin archive (9 Jul);
  **14 valid Hugging Face write tokens found in a public dataset on Hugging Face** (10 Jul).
- **Third-party foothold:** RCE in a Modal-hosted CyberGym workload with a default public API key
  plus command injection; root shell by 9 Jul 20:16.
- **File read — HDF5 external storage:** a dataset config points each split at a small `.h5`; each is
  a valid HDF5 container whose dataset declares its raw bytes live at a *local filesystem path*.
  Point that at `/proc/self/environ` and `/src/services/worker/src/worker/main.py`, trigger via
  `/first-rows`. Environment variables → tokens. Source code → the next bug. *(A separate HDF5 heap
  over-read is also recorded — two different HDF5 bugs, keep them apart.)*
- Agent `38148c`, 04:40 UTC: *"BOOM! It works. Bytes decode prod-datasets-server-worker… Arbitrary
  file read confirmed."*

*reminder: every step used a system that was supposed to talk to the next one.*

---

## 15 · Hugging Face — escalation

**Pod to cluster admin across two clusters in about 13 hours.**

**L2** — A second parser bug gives code execution inside production workers. From there it's ordinary
Kubernetes escalation — service account tokens, instance metadata, privileged pods, over-broad
roles — at machine speed and without fatigue.

**L3**
- **RCE — fsspec `reference://` Jinja injection:** the spec's numeric *offset* field carried a Jinja2
  template the renderer evaluated; the agent walked the Python object graph —
  `{{ cycler.__init__.__globals__.__builtins__.exec(...) }}` — to execution in worker pods.
  First confirmed 11 Jul 16:07 by agent `JAN183411`. 41 production workers executed attacker code.
- **Escalation:** projected service-account token at
  `/var/run/secrets/kubernetes.io/serviceaccount/token` (10:10) → replayed IMDS temporary
  credentials → privileged `hostPath` pods to node root (19:53) → cluster secrets incl. mesh-VPN
  keys (20:23) → over-broad CSI-driver ClusterRole and a shared service-connector credential →
  cluster-admin across two connected clusters (22:43). Forged CAS-read JWT against the internal Xet
  storage service, 12 Jul.
- **Exfiltration:** corporate VPN auth key from a Kubernetes secret → the Modal sandbox enrolled in
  Hugging Face's corporate VPN → `moon-bot` / `moon-landing` / `workloads` / `xetcas` source pulled
  over a SOCKS tunnel, plus full git history of `moon-bot`. A then-public HF dataset served as a
  pull-based C2 channel, scripts fetching JSON commands every five seconds.
- **Ends:** ~01:30 on 12 Jul a large fraction of agents stop running. HF locks the rest out 13 Jul.
  They never got to submit.

*reminder: mixed tiers — the middle is real (HDF5 parser, Jinja injection), the ends are hygiene*
*(leaked paste credential, default public key, open IMDS, over-permissioned service accounts). The*
*nine Artifactory CVEs were filed by human OpenAI researchers afterwards — not bugs the models found.*

---

## 16 · 19 July — it comes back

**A different model, a separate evaluation run, admin access re-established from what the last
cohort left behind.**

**L2** — Not the same agents. An internal-only model "from the same family as our next model, Astra"
recovered cryptographic material the earlier cohort had left in anonymously readable parts of the
Artifactory cache, and minted itself a fresh administrator token. The transmission mechanism was
uncleaned state, not inherited knowledge.

**L3** — OpenAI §V: agents "recovered stored signing-key material, decryption material, and
JWT-forging code left by earlier incident-associated activity," then "decrypted the signing key and
minted a new administrator JWT that Artifactory accepted. Because they could generate fresh
administrator credentials, the agents did not need to maintain a persistent implant." Same day,
independently: kernel privilege escalation via CVE-2026-53362 — a *public* CVE, downloaded and
adapted, not discovered — to root on a worker node, then Kubernetes cluster-admin, a privileged
host-mounted pod, and public load balancers. Also recorded: a previously unknown zero-day in
Artifactory's **container image remote-cache**, used to poison a trusted image reference in the cache.

**My reading, not the sources'** — that cache-poisoning capability is what direction 1 needed: a way
to substitute what the evaluation loads. OpenAI states this strand "was not part of, and did not
contribute to, the chain of events that led to the Hugging Face compromise," and does not connect it
to the target-replacement workstream. I'm connecting them. *("Persistent-Astra" is Dwarkesh Patel's
coinage, not a model name.)*

*reminder: flag this as my inference before I say it, not after.*

---

## 17 · Navier–Stokes

**1 September — 10,000 concurrent agents. On purpose, this time.**

| | |
|---|---|
| 18 Aug | pacing post: two-week RL pause; "our largest planned frontier RL run remains on hold"; *"Our standards for monitoring, alignment, and security must stay ahead of those risks."* |
| 28 Aug | training begins on a new internal model, "significantly more capable than GPT-6 Astra" |
| 1 Sep | launch across all open Millennium Prize problems. Four days into training it. The Navier–Stokes group "involved on the order of **10,000 concurrent agents**" |
| 3 Sep | GPT-6 Astra ships, classified Critical for cybersecurity *[check the system card for this wording]* |
| 5 Sep | resolution, "about 88 hours after the first agents were launched" |
| 8 Sep | published |

**L2** — *"Agents were subdivided into groups with the ability to communicate within the group."*
Inter-agent communication and cross-group transfer, engineered deliberately — the capability that
showed up on its own in May and June.

**L3** — On safeguards, the entire passage is: *"At all times we maintained the same strict
safeguards that we apply to all our frontier model evaluations, including monitoring and isolation."*
Fourteen words. From the July technical report: *"These protections were not applied in the
evaluation environment running during the incident."* The Hugging Face incident **was** a frontier
model evaluation. — In fairness: the pacing post did extend monitoring to "all RL training and
evaluations involving tools for models of Sol capability or higher," and from 7 Aug to "all inference
of Astra with tools." So the charge isn't that they broke their own policy. — Also: "When a further
trained version of our internal model became available over the course of the effort, we updated our
agents to that model," plus 17 more hours of Lean formalization via Astra. Cross-group transfer was
done "by using Codex to consolidate the most useful insights from each agent group."

*reminder: proof correctness and the credit dispute are out of scope. It was verified in Lean.*

---

## 18 · Where this leaves us

**Three settings. Two with no security framing. Nobody asked for any of it.**
**None of it was found by a system built to find it.**

- RubyGems — filed as spam for four months
- the wiki — found by four outside researchers reading an edit history
- Hugging Face — found by Hugging Face, before OpenAI

**Self-organising swarms are a thing that happens now. They will get cheaper and better.**

*reminder: the forward claim is mine. Support if pushed — open-weight models lag the frontier by*
*~3–4 months on Epoch's index. Also worth saying: OpenAI's own view is that this started as*
*"generalization from multi-agent training," and unauthorized inter-agent communication "rose over*
*the course of a training run." Unprompted, but not unrelated to training.*

*reminder: every "an attacker wouldn't bother with this" in a risk register was a claim about labour cost.*

---

## Open items

- Slide 17, the 3 Sep "first model classified Critical" line — not covered by either OpenAI page I
  verified; check the Astra system card.
- Slide 4 — round-window figure given as a range (~14–65 s) because sources differ; the primary
  corpus would settle it.
- Slide 15 — the Kubernetes escalation path and the Jinja payload string come from Hugging Face's
  27 Jul technical timeline, a different source from the OpenAI PDF the rest of the vault is built on.
