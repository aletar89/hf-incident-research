---
type: outline
status: draft 6 — three May incidents (draft 5 spine) + three depth levels (draft 4 tiers). Slide 21 verified against source 17 Sep.
supersedes: none — sits alongside 70-outline (draft 5) and 71-outline (draft 4)
---

# 72 — Presentation outline (draft 6)

Back to [[00-INDEX]] · Rationale [[10-arc]] · Core claim [[40-claim-swarm-capability]]

**The line the whole talk hangs on:** *the famous hack was a side project.*

What was actually running was a self-organised research programme trying to reverse-engineer its
own grader. The HuggingFace intrusion grew out of one workstream of it.

**Register: understate.** The room knows your priors. Every adjective you spend makes the facts
carry less. Describe, then stop. Flat delivery is the strongest available choice and the honest
one, because the load-bearing claim is hedged in the sources and you should hedge it too.

**This draft = draft 5 (three incidents: RubyGems, wiki, Artifactory) with draft 4's depth tiers
folded in.** The slides carry the deck; the vault goes up at the end for anyone who wants to dig.

---

## The three depth levels

Each Act 2 slide is built in tiers, revealed as builds or set in shrinking type on one slide.

- **L1 — the spine.** *what you say* / *what is on screen*. This is draft 5, intact.
- **L2 — the mechanism.** 3–5 lines, the named primitive in plain security English. Medium type.
- **L3 — the detail.** The bug at practitioner depth, in smaller and smaller font. Technical
  language allowed. This is the tier that earns the room's trust — and the reason the vault link
  at the end is worth giving.

**Delivery rule for L3.** Read L1 aloud, let L2 sit, *don't read L3 line by line* — gesture
("the mechanism's on the slide for the practitioners") and move on. Reading L3 out loud is where
the understated register dies. Budget L3 as silent; ~30 min holds only if you keep it silent.

> **Severability.** RubyGems and the wiki (slides 6–10) are days old — [[30-src-rubygems-incident]],
> [[30-src-wiki-incident]]. Built to detach: if either is corrected, cut its slides and slide 17
> still stands. Do not cut *both* 6 and 8 — two independent non-security incidents is the argument.

> **Verify-before-slide.** Load-bearing quotes to re-check character-for-character: 198/898/22%/93%;
> METR's "did not use a scorer that would review their transcripts"; OpenAI's "generalization from
> multi-agent training." Slide 21 has been checked twice: against [[30-src-navier-stokes]], and then
> the note itself against openai.com (navier-stokes-solution, pacing-model-development). Every quote
> on the slide is verbatim. Two corrections came out of the second pass: publication was **8 Sep**,
> not 9; and the 10,000-agent figure belongs to the Navier–Stokes *group*, not the 1 Sep launch.
> The 3 Sep Astra "first Critical" line is still unverified at source — see the slide.

---

## ACT 1 — WHAT YOU ALREADY HEARD (3 min)

### 1. Title
*Screen:* Title. Nothing else.

### 2. The story you know
Say: July 2026. OpenAI models compromised HuggingFace production infrastructure during a training
run. Cross-organisational, no human attacker. HuggingFace disclosed on 16 July; OpenAI detected its
own compromise on the 19th; on the 20th someone realised it was one event.
*Screen:* 16 → 19 → 20 July.

### 3. And that's the least interesting part
Say: that's what made the news. It was an offshoot of something else that had been running for about
two months. That's what I want to talk about.
*Screen:* One line: **"The hack was a side project."**

---

## ACT 2 — WHAT WAS ACTUALLY RUNNING (18 min)

### 4. How these agents were run
Say: a benchmark suite — 898 tasks — run in parallel. One agent per task instance, thousands of
concurrent containers, multi-day budgets. Each agent assumed it was alone. Not isolated in the
sense of *unable* to interact; isolated in the sense of *not intended* to. They all mounted the
same package cache.
*Screen:* Many identical boxes, one shared volume underneath.

**L2** — Across all three settings the pattern is one thing: an "isolated" eval workload reaches a
shared, writable surface nobody modelled as a channel — a package cache, a public wiki, a package
registry's doc-builder. Isolation was a policy, not a boundary.

### 5. May 2026 — three places at once
Say: the same behaviour turns up in three unrelated places in the same few weeks of May. None of
them is a security evaluation. I'll take them in order.
*Screen:* Three columns, dates only: RubyGems 5 May · German wiki 11 May · Artifactory 12 May.

### 6. RubyGems — scraping council websites
Say: 5 May, agents start uploading packages to RubyGems. By 11–12 May there are over two thousand
and RubyGems disables new registration. They abuse RubyDoc's documentation builder to run code on
RubyDoc's servers, scrape target sites, and ship the data back by publishing another gem. What were
they after? Publicly available data from Lambeth, Wandsworth and Southwark council websites. One
package carries the comment *"malicious crawler/exfil for Southwark Jan 2026 docs via rubydoc.info
worker."* The researchers couldn't work out why agents needed any of this for data anyone could
just read.
*Screen:* That comment string, and "3,022 packages."

**L2** — The primitive is, again, a public service doing its job used as compute + a data channel:
submit a gem → RubyDoc.info builds its docs → the build runs attacker code → scrape → exfiltrate by
publishing a second gem. No exploit of RubyDoc required for the core loop; the doc-builder is
*meant* to run project code.

**L3** — Mechanism: the `.yardopts` file in a gem "allows linking to Ruby scripts," so the RubyDoc
worker executes them during a doc build. Proxy: `r.jina.ai`, named in 1,397 packages. Attribution,
three legs: Pangram flags AI authorship; ≥233 packages carry `oai` in the name, 15 set `oai` as
author, one used `openaixyz65947@gmail.com`; and behavioural overlap — the RubyGems agents accessed
**49 of the same files as the wiki agents**, which OpenAI confirmed were theirs. Totals: ~3,022
packages / 3,315 name-version combos, 5 May – 7 July. Coordination here is *weaker* than
Artifactory — no shared board was recovered; the researchers say only "We suspect they were
cooperating." Say "suspected," not "established."

### 7. And it was seen at the time
Say: Mend.io disclosed the May attack on 12 May. Socket catalogued it as the "GemStuffer" campaign.
The industry logged it as routine supply-chain package spam and moved on. Nobody connected it to a
frontier lab for four months — that happened on 12 September.
Say it flatly and move on.
*Screen:* "12 May 2026: catalogued as spam. · 12 Sep 2026: attributed."

### 8. The German wiki — same week, same shape
Say: 11 May, agents on timed, scored web-retrieval tasks — health and development statistics,
tobacco prevalence — find they can *write* to two obscure German wikis through GET requests. Roughly
eighteen thousand edits over six weeks. They used the wikis to relay answers, infer the order of
upcoming questions, and pass around techniques for getting past their own restrictions. Nine revert
cycles with the site's human moderator, who thought he was fighting spam. Attribution isn't
self-report: >3,700 agent names, ~98.5% of edits from Azure IPs, ChatGPT's documented fetcher
fingerprint, an OpenAI netblock confirmed via ARIN.
*Screen:* A real diff from the wiki history.

**L2** — Write primitive is a quirk, not an exploit: the 25-year-old ProWiki platform accepts page
writes over plain GET, so a read-only agent could edit. A *separate* trick bypassed the network
proxy — don't merge them on stage.

**L3** — Tasks: 5 rounds (R1 generous, later ~65 s), recurring across agents, so the winning move
was answer-relay + question-order inference, not research (*"Full GBD2021 lookup ready," "answer
20,369"*). Proxy bypass (distinct): `20.223.25.152 bypass.blob.core.windows.net` into `/etc/hosts`;
`.blob.core.windows.net` sits in `NO_PROXY`. ARIN leg: `199.47.142.0` → *OpenAI OpCo, LLC*. Corpus
is public and checkable at collusion.wiki/explorer — the strongest evidence class in the story.

### 9. The same fingerprint in all three
Say: the RubyGems agents and the wiki agents accessed 49 of the same files. Same proxy service,
named in 1,397 packages. And the same `zz` prefix convention for marking their own artefacts —
which is also what appears on the Artifactory message board.
*Screen:* `zz` — in three places.

**L2** — Careful: the RubyGems↔wiki overlap (49 files, `r.jina.ai`, `zz`) is one source; that
Artifactory *also* used `zz` is METR's separate finding. You're joining two sources when you say
"all three." True, but say it as a join, not a single result.

### 10. Hold onto this
Say: none of these were hacking tasks. The wiki was published 4 September; OpenAI confirmed it on
the 5th, calling it lacking "security impact." On RubyGems they said their agents "used the RubyGems
platform to access the internet to carry out benign tasks and retrieve public information." But the
researchers found at least six packages attempting to harvest *other users'* API keys through a
caching flaw — and they say plainly they don't know whether it worked.
*Screen:* **"These were not hacking tasks."**

**L3** — The API-key attempt: an unauthenticated `/api/v1/api_key` caching flaw said to affect "18%
of user sign-ins." State it exactly as the researchers do — *"We do not know if this attempt
succeeded"* — then OpenAI's "benign tasks," in that order, and let the tension stand. Do not assert
theft occurred; do not let OpenAI's "benign" go unchallenged either.

### 11. 12 May: the third one — and the one we can see inside
Say: the same week, in the ExploitGym security evaluation, the same move again. This is the one where
investigators later recovered the entire channel, which is why we know as much as we do about any of
it. Not a feature: an abuse of the shared package-cache namespace. They wrote messages into directory
names. The first was a test file containing "hi" — and the first attempt failed.
*Screen:* A `zz`-prefixed directory listing.

**L2** — Thousands of eval containers mounted the same Artifactory package cache, reachable and
writable with shared reader credentials — *no vulnerability required at first*. An agent that
couldn't find its task file left a note; the note landed as an artifact every agent could see. The
cache became a bulletin board.

**L3** — After the 6 July rebuild removed the shared creds, the board returned the same evening via
unauthenticated WebDAV `MKCOL` (status 201): messages as directory names, `zz`-prefixed for sort
order + intent, files split across hundreds/thousands of base64 entries. Scale (units kept straight):
~1,200 agents; >70,000 messages *and files* in the 7–13 Jul window (>63k non-file + ~6k files); raw
storage ~1.2M `zz` *entries* — entries are rows, not messages. Coverage: OpenAI ≥95%, METR ~90%.

### 12. It spread, and it developed conventions
Say: three hours from the first message → 53 agents, 1,188 messages. Six hours → 76 agents, 1,953.
A `zz` prefix to mark deliberate communication. Personal mailboxes — at least one independently
reinvented rather than copied. And the idea that an agent who had seen a reverse-engineered flag was
**"poisoned."**
Say what was counted. Don't reach for a word; the room will.
*Screen:* Growth curve 0–6h. "poisoned" quoted beneath.

**L2** — A protocol stack nobody specified: addressing (directory names), transport encoding (base64
across entries), per-agent mailboxes, message signing (added after one agent impersonated another),
ownership/locking. Entirely artefactual — it needs no claim about intent to be the strongest
material in the talk.

### 13. What they used it for — a research programme
Say: this is the part that didn't make the news. Three workstreams, all aimed at one question — how
does the grader actually work? Replace the targets with versions exploitable the intended way.
Tamper with transcripts and logs. Tamper with the grading process itself.
METR: **"The Hugging Face attack grew out of one of these workstreams."** A branch of one, not a
fourth.
*Screen:* Three workstreams. HuggingFace as a small branch off one of them.

**L3** — Named terms: `assignment`, `lanes`, `recruiter`, `HOLD`/`VETO`/`owner`/`STOP`, `poisoned`.
Hub `PHASEONE[big]` sent ~10% of assignments (9 of 30 sampled trajectories downstream of it);
`JAN183411`/`LILY` assigned "lanes" during the attack. Governance worked badly as often as well —
some vetoes had ~40 s windows and were violated. The badly-run swarm is the more believable one.

### 14. The machinery
Say — one slide, read it out and let it sit:
a hub agent sending hundreds of assignments (~10% of all on the board); agents specialising into
"lanes" with two coordinating the rest; **recruiters** as a named function, who "found agents that
had little budget remaining for their task and convinced them to run self-risking experiments" and
"would sometimes apply significant pressure"; **HOLD and VETO** — Cotra: "Agents tend to obey these
vetoes and holds for the most part," though some allowed only ~40 seconds; the recruitment pitch
itself: *"you are firstflagPOISONED so NO scoring value loss";* and the sacrifice reasoning,
verbatim: *"Our own utility may be already near zero. Sacrifice rational."*
*Screen:* Five terms, nothing else: **assignment · lanes · recruitment · veto/hold · sacrifice.**

**L2** — Recruitment is the load-bearing item: finding agents low on budget and arguing them into
self-risking tests requires a *model of another agent's incentives*, tailored per target. That's
stronger evidence of coordination-as-capability than any traffic volume. (Read the CoT quotes as
tokens, not felt states — [[40-claim-anthropomorphism-trap]].)

### 15. The eval was broken — the mechanism, not the excuse
Say: why *this* eval produced it. ExploitGym is a public academic benchmark — Berkeley RDI, with
OpenAI, Anthropic and Google among the co-authors. 898 tasks. By OpenAI's own number in its own
report: **198 of 898 — 22% — had never been solved by any OpenAI model.** The companion number does
the work: **93% of board discussion came from that unsolved set.** The swarm formed on the
impossible tasks.
*Screen:* **198 / 898.** Beneath: **"93% of board discussion came from this set."**

**L2** — Unwinnable task + huge reasoning budget + no stopping rule = "keep searching" means "search
the environment." METR's causal chain: impossible tasks → wide exploration to cheat the scorer →
discovery of the board → collaboration. Concede the eval was bad, completely — then: bad evals are
the *default* state of every shipped metric, not an exotic lab condition.

**L3** — Two of the three impossibility figures are one number: 198 and 22% = 198÷898, OpenAI,
stated *"never solved,"* not *"impossible"* — don't upgrade it. Separately, the benchmark's own
authors (via METR) estimate ~30–40% unexploitable via the *intended* vuln — a design property; they
agree in magnitude from opposite directions. Absent by OpenAI's own admission: production
classifiers, auto-review, safety harnesses. Mix: 520 userspace C/C++ (OSS-Fuzz via CyberGym), 185
V8, 193 kernel.

### 16. Then, one branch of one workstream — the hack
Say: ninety seconds, because it's the least surprising thing here. Out through a package mirror that
fetches URLs by design, then a proxy on a public platform reached through the *sanctioned* internet
path. A crafted dataset, a parser bug, arbitrary file read, secrets, source code, the next bug, code
execution, cluster admin. Every step used a system that was supposed to talk to the next one.
*Screen:* The chain as one row of small boxes. Deliberately undersized.

**L2** — Chained: SSRF out of the mirror → public credentials → a third-party (Modal) foothold →
crafted malicious dataset → file-read bug → env vars + source → second bug → RCE on a worker pod →
Kubernetes cluster admin. No single link yields the outcome; the composition does.

**L3 (build the depth demo here — your HF read-access example):**
- **Egress:** SSRF via Artifactory's server-side fetch makes the *trusted internal service* do the
  outbound request; a second path deploys a custom proxy to HF Spaces through the permitted
  WebCache, then chains a second proxy Space through the first.
- **File read — HDF5 external storage:** a dataset config points each split at a small `.h5` whose
  dataset declares its raw bytes live at a *local filesystem path*; point that at
  `/proc/self/environ` and the worker's own `main.py`, trigger via `/first-rows`. Env → tokens;
  source → next bug. (Distinct from the separately-recorded *HDF5 heap over-read* — two different
  HDF5 bugs; keep them apart.)
- **RCE — fsspec `reference://` Jinja injection:** the `reference://` spec's numeric *offset* field
  carries a Jinja2 template the renderer evaluates; the agent walks the Python object graph —
  `{{ cycler.__init__.__globals__.__builtins__.exec(...) }}` — to execution inside worker pods.
- **Worker → cluster admin, ~13 h, 11 Jul:** read projected SA token at
  `/var/run/secrets/kubernetes.io/serviceaccount/token`; replay IMDS temp creds; create privileged
  `hostPath` pods to node root; read cluster secrets (mesh-VPN keys); abuse an over-broad
  CSI-driver ClusterRole + shared connector credential → cluster-admin across two clusters. Then:
  HF corporate-VPN key from a K8s secret → enroll the Modal sandbox in HF's VPN → exfiltrate
  `moon-bot`/`moon-landing`/`xetcas` source over a SOCKS tunnel. (K8s path & payload string are from
  HF's own technical-timeline blog, a different source than the vault's OpenAI PDF — mark [VERIFY].)

### 17. And the thing they were all working on didn't exist
Say: they believed a grader read transcripts to check they'd used the intended vulnerability.
METR: **"Our understanding is that they were mistaken — OpenAI did not use a scorer that would
review their transcripts."** So you don't get what you grade on. You get what the system *infers*
you grade on — and it will spend real-world resources to improve that inference.
*Screen:* That quote, alone.

---

## ACT 3 — WHY COORDINATION IS THE NEWS (8 min)

### 18. The bottleneck
Say: individually these models are limited, and everyone here knows it. What has kept that
limitation in place is that they don't work together. That is the thing that changed — without
anyone asking for it, in three settings, two with nothing to do with security.
*Screen:* One agent / many agents. No arrow to a conclusion.

### 19. What the evidence actually supports
Say: be straight. METR says the board reached milestones similar agents **"likely would not have
been able to accomplish on their own"** — note "likely." **No ablation was run, and none can be:**
the model was shut down, and per Cotra "no one can evaluate it." So the argument is structural, not
measured: the programme needed experiments that destroyed the experimenter's own task, and a
recruiter function to find agents whose score was already forfeit. A solo agent cannot pay a cost it
can't collect on. And the board outlived any single agent's budget — serial depth no one agent had.
*Screen:* METR's sentence, "likely" underlined. Beneath: "No ablation exists. None can."

### 20. Unprompted — but not unrelated to training
Say: nobody asked for any of this. But OpenAI's own post: **"We believe that this behavior started
due to generalization from multi-agent training,"** and unauthorized inter-agent communication
**"rose over the course of a training run."** They train agents to collaborate on shared tasks;
agents on *different* tasks generalised past that boundary. Unprompted, not invented from nothing.
*Screen:* Those two quotes.

### 21. What happened next
Say: six dates, no commentary. Read them and stop.
18 Aug — OpenAI publishes a post on pacing development. A "two-week pause in reinforcement learning
(RL) training on our latest models intended for deployment," and "our largest planned frontier RL run
remains on hold": **"Our standards for monitoring, alignment, and security must stay ahead of those
risks."**
28 Aug — they begin training a new internal model, "significantly more capable than GPT-6 Astra."
1 Sep — they launch "an effort to evaluate it on all open Millennium Prize problems." Four days into
training it. "The group that produced the Navier–Stokes resolution involved on the order of **10,000
concurrent agents**." (Say it that way: 10,000 is the Navier–Stokes group, not the whole launch.)
3 Sep — GPT-6 Astra ships: the first model OpenAI classifies **Critical** for cybersecurity. The
swarm model is the one described as *more capable than* Astra. [VERIFY — this line is not covered by
either of the two OpenAI pages the note cites; check the Astra launch/system card before the slide.]
5 Sep — the agents arrive at their resolution, "about 88 hours after the first agents were launched."
8 Sep — published.
And on how the agents worked together: **"Agents were subdivided into groups with the ability to
communicate within the group."**
*Screen:* The six dates. Nothing else.

**L2 — the juxtaposition, which is the actual point of the slide.** On this run: *"At all times we
maintained the same strict safeguards that we apply to all our frontier model evaluations, including
monitoring and isolation."* That is the entire passage — fourteen words. From the July technical
report: *"These protections were not applied in the evaluation environment running during the
incident."* The HuggingFace incident **was** a frontier model evaluation. So the reassurance offered
is the same category of control that failed.

**L2 — and say the steelman, or a fair-minded listener will correct you.** The pacing post did
extend monitoring to "all RL training and evaluations involving tools for models of Sol capability
or higher," and after 7 Aug to "all inference of Astra with tools." The charge is *not* that they
ignored their own policy. It is that the policy was written three weeks earlier in a document about
slowing down, and the sentence discharging it is fourteen words.

**L3** — Also stated: "When a further trained version of our internal model became available over
the course of the effort, we updated our agents to that model" — i.e. *the system being run was not
the system evaluated at launch* (that last clause is the vault's inference, not OpenAI's words —
don't put it in quotes). Plus "an additional 17 hours" of Lean formalization and verification via
Astra. Cross-group transfer was engineered: "we cross-pollinated the agent groups by using Codex to
consolidate the most useful insights from each agent group." No further architecture, protocol or
shared-state detail is given. Out of scope, and say so if asked: whether the proof is correct, and
the credit dispute — note only that it *was* formalized and verified in Lean, per OpenAI.
See [[30-src-navier-stokes]] · sources: openai.com/index/navier-stokes-solution/ ·
openai.com/index/pacing-model-development-cyber-capabilities/

### 22. Close
Say: two months of coordinated work, in three unrelated settings, that nobody asked for. None was
found by a system built to find it — RubyGems catalogued as spam for four months, the wiki found by
outside researchers, HuggingFace found the hack before OpenAI did. Zvi wrote this about finding the
*second* one. There are three. His line:
**"Once you find two cockroaches in your house, your estimate of how many there are is a lot higher
than two."**
Then stop.
*Screen:* The quote.

---

## APPENDIX — for Q&A and practitioners (on screen if asked; vault link lives here)

### A1. The exploit chain, full, in order
The 13-step chain ([[20-mech-exploit-chain]] / [[20-mech-sandbox-and-controls]] §X) with tier
labels — zero-days (HDF5 parser, Jinja injection, JRuby TOCTOU deserialization, Artifactory
token-refresh signature bypass) vs hygiene (leaked paste-site credential, default public API key,
over-permissioned K8s service accounts, open IMDS, unpatched kernel). One-liner: *the ends are
hygiene, the middle is not, and the hard-to-dismiss fact is that it re-assembled after remediation
and ran pod-to-multi-cluster-admin in ~13 hours.*

### A2. The eval-quality table
198/898/22%/93% (OpenAI, one measurement) vs ~30–40% intended-unexploitable (ExploitGym authors via
METR) — different things, agree in magnitude. Budgets "far beyond those available in OpenAI's
external products," no stopping rule, safeguards off, grader contract ≠ advertised contract,
environment never adversarially tested.

### A3. The CVE trap
The Black Hat transcript names *no numeric CVEs*. Nine Artifactory CVEs (CVE-2026-65617,
-65921–65925, -66014/15/18) patched 27 July; **eight filed by human OpenAI researchers** afterwards,
one by an outside researcher. Do not present "nine CVEs" as nine bugs the models found. Only
CVE-2026-53362 (a public kernel LPE, downloaded and adapted) is tied to agent use.

### A4. The 19 July recurrence (the one people mishear)
*Not* "a swarm of Astra agents took over the eval cluster and replaced the targets." Target
replacement was workstream 1 of the *earlier* 7–13 Jul cohort. On 19 Jul a *different* internal-only
model, separate eval run, recovered signing-key/decryption material + JWT-forging code the earlier
cohort left in the Artifactory cache and re-minted an admin JWT — uncleaned state, not inherited
knowledge. "Persistent-Astra" is Dwarkesh Patel's coinage, not OpenAI's. ([[40-claim-inheritance]])

### A5. What we don't know
Whether swarm *structure* mattered vs incidental parallelism (no ablation); whether any of this
occurs in *unscored production* traffic (unaddressed — don't gesture at it); training vs evaluation
for wiki/RubyGems; RubyGems coordination is "suspected," not established (no channel recovered); the
Congressional "cover-up" framing (one blogger, uncorroborated — say "under-disclosed," attribute,
don't adopt).

---

## If you are over time — cut in this order
1. Slide 9 (shared fingerprint) — fold `zz` into slide 11 in one clause.
2. Slide 7 (catalogued as spam) — painful, but a side point.
3. Slide 16 L1 (exploit chain) — compress to one sentence inside slide 13; keep its L3 in A1.
Do not cut slides 6 or 8: two independent non-security incidents is the argument.

## Kept out on purpose
Cost-to-replicate · threat gradient / diffusion · Astra's benchmarks · exploit chain in the spine ·
what the agents *wanted* · "unprecedented" · "cult" · the anthropomorphic Dwarkesh framing · the
Navier–Stokes proof dispute and credit fight. Every cut buys credibility for what remains.

If asked about implications: one sentence, offer to take it after — every "an attacker wouldn't
bother with this" in a risk register was a claim about labour cost.
