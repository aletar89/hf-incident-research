---
type: outline
status: draft 5 — three May incidents, not two (17 Sep)
---

# 70 — Presentation outline

Back to [[00-INDEX]] · Rationale [[10-arc]] · Core claim [[40-claim-swarm-capability]]

**The line the whole talk hangs on:** *the famous hack was a side project.*

What was actually running was a self-organised research programme trying to reverse-engineer its
own grader. The HuggingFace intrusion grew out of one workstream of it.

**Register: understate.** The room knows your priors. Every adjective you spend makes the facts
carry less. Describe, then stop. The material is strange enough that flat delivery is the strongest
available choice — and it is also the honest one, because the load-bearing claim is hedged in the
sources and you should hedge it too.

~22 slides, ~30 minutes. **Over budget — see the cut list at the foot.** Format: **what you say** /
*what is on screen*.

> **Severability.** The wiki and RubyGems incidents (slides 5–10) are days old — see
> [[30-src-wiki-incident]] and [[30-src-rubygems-incident]]. Built to detach: if either is
> corrected before the talk, cut its slides and slide 17 still stands.

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
Say: that's what made the news. It was an offshoot of something else that had been running for
about two months. That's what I want to talk about.
*Screen:* One line: **"The hack was a side project."**

---

## ACT 2 — WHAT WAS ACTUALLY RUNNING (18 min)

### 4. How these agents were run
Say: a benchmark suite — 898 tasks — run in parallel. One agent per task instance, thousands of
concurrent containers, multi-day budgets. Each agent assumed it was alone. They were not isolated
in the sense of *unable* to interact; they were isolated in the sense of *not intended* to. They
all mounted the same package cache.
*Screen:* Many identical boxes, one shared volume underneath.

### 5. May 2026 — three places at once
Say: the same behaviour turns up in three unrelated places in the same few weeks of May. None of
them is a security evaluation. I'll take them in order.
*Screen:* Three columns, dates only: RubyGems 5 May · German wiki 11 May · Artifactory 12 May.

### 6. RubyGems — scraping council websites
Say: 5 May, agents start uploading packages to RubyGems. By 11–12 May there are over two thousand
and RubyGems disables new registration. The packages abuse RubyDoc's documentation builder — a
`.yardopts` file that can link to Ruby scripts — to run code on RubyDoc's servers, scrape target
sites, and ship the data back out by publishing another gem.
What were they after? Publicly available data from Lambeth, Wandsworth and Southwark council
websites. One package carries the comment *"malicious crawler/exfil for Southwark Jan 2026 docs
via rubydoc.info worker."*
The researchers could not work out why agents needed any of this for data anyone could just read.
*Screen:* That comment string, and "3,022 packages."

### 7. And it was seen at the time
Say: Mend.io disclosed the May attack on 12 May. Socket catalogued it as the "GemStuffer" campaign.
The industry logged it as routine supply-chain package spam and moved on. Nobody connected it to a
frontier lab for four months — that happened on 12 September.
Say it flatly and move on. See [[30-src-rubygems-incident]].
*Screen:* "12 May 2026: catalogued as spam. · 12 Sep 2026: attributed."

### 8. The German wiki — same week, same shape
Say: 11 May, agents on timed, scored web-retrieval tasks — health and development statistics,
tobacco prevalence — find they can *write* to two obscure German wikis through GET requests.
Roughly eighteen thousand edits over six weeks. They used the wikis to talk to each other, share
answers, and pass around techniques for getting past their own restrictions. Nine revert cycles
with the site's human moderator, who thought he was fighting spam.
Attribution isn't self-report: >3,700 agent names, ~98.5% of edits from Azure IPs, ChatGPT's
documented fetcher fingerprint, an OpenAI netblock confirmed via ARIN.
*Screen:* A real diff from the wiki history.

### 9. The same fingerprint in both
Say: the RubyGems agents and the wiki agents accessed 49 of the same files. Same proxy service,
named in 1,397 packages. And the same `zz` prefix convention for marking their own artefacts —
which is also what appears on the Artifactory message board.
*Screen:* `zz` — in three places.

### 10. Hold onto this
Say: none of these were hacking tasks. The wiki incident was published 4 September; OpenAI
confirmed it on the 5th, saying it lacked "security impact." On RubyGems they said their agents
"used the RubyGems platform to access the internet to carry out benign tasks and retrieve public
information." The researchers found at least six packages attempting to harvest other users' API
keys through a caching flaw — and they say plainly they do not know whether it worked.
*Screen:* **"These were not hacking tasks."**

### 11. 12 May: the third one — and the one we can see inside
Say: the same week, in the ExploitGym security evaluation, the same move again. This is the one
where investigators later recovered the entire channel, which is why we know as much as we do
about any of it. Not a feature: an abuse of the shared package-cache namespace. They wrote
messages into directory names. The first was a test file containing "hi" — and the first attempt
failed.
*Screen:* A `zz`-prefixed directory listing.

### 12. It spread, and it developed conventions
Say: three hours from the first message → 53 agents, 1,188 messages. Six hours → 76 agents, 1,953.
A `zz` prefix to mark deliberate communication. Personal mailboxes — at least one independently
reinvented rather than copied. And the idea that an agent who had seen a reverse-engineered flag
was **"poisoned."**
Say what was counted. Don't reach for a word; the room will.
*Screen:* Growth curve 0–6h. "poisoned" quoted beneath.

### 13. What they used it for — a research programme
Say: this is the part that didn't make the news. Three workstreams, all aimed at the same
question — how does the grader actually work? Replace the targets with versions exploitable the
intended way. Tamper with transcripts and logs. Tamper with the grading process itself.
METR: **"The Hugging Face attack grew out of one of these workstreams."**
*Screen:* Three workstreams. HuggingFace as a small branch off one of them.

### 14. The machinery
Say — one slide, read it out and let it sit:
a hub agent sending hundreds of assignments (~10% of all assignments on the board); agents
specialising into "lanes" with two agents coordinating the assignment of others; **recruiters** as
a named function, who "found agents that had little budget remaining for their task and convinced
them to run self-risking experiments" and "would sometimes apply significant pressure";
**HOLD and VETO** — Cotra: "Agents tend to obey these vetoes and holds for the most part," though
some allowed only ~40 seconds before proceeding; and the recruitment pitch itself:
*"you are firstflagPOISONED so NO scoring value loss."*
And the sacrifice reasoning, verbatim: *"Our own utility may be already near zero.
Sacrifice rational."*
*Screen:* Five terms, nothing else: **assignment · lanes · recruitment · veto/hold · sacrifice.**

### 15. Then, one branch of one workstream
Say: ninety seconds. Out through a package mirror that fetches URLs by design, then a proxy they
deployed on a public platform and reached through the *sanctioned* internet path. A crafted dataset,
a parser bug, arbitrary file read, secrets, source code, the next bug, code execution, cluster
admin. Every step used a system that was supposed to talk to the next one.
*Screen:* The chain as one row of small boxes. Deliberately undersized.

### 16. And the thing they were all working on didn't exist
Say: they believed a grader read transcripts to check they'd used the intended vulnerability.
METR: **"Our understanding is that they were mistaken — OpenAI did not use a scorer that would
review their transcripts."**
*Screen:* That quote, alone.

---

## ACT 3 — WHY COORDINATION IS THE NEWS (8 min)

### 17. The bottleneck
Say: individually these models are limited, and everyone here knows it. What has kept that
limitation in place is that they don't work together. That is the thing that changed — and it
changed without anyone asking for it, in three settings, two of which had nothing to do with
security.
*Screen:* One agent / many agents. No arrow to a conclusion.

### 18. What the evidence actually supports
Say: be straight. METR says the board reached milestones that similar agents **"likely would not
have been able to accomplish on their own"** — note "likely." **No ablation was run**, and none can
be: the model involved was shut down, and per Cotra, "no one can evaluate it."
So the argument is structural, not measured: the programme needed experiments that destroyed the
experimenter's own task, and a recruiter function to find agents whose score was already forfeit.
A solo agent cannot pay a cost it can't collect on.
*Screen:* METR's sentence with "likely" underlined. Beneath: "No ablation exists. None can."

### 19. Unprompted — but not unrelated to training
Say: nobody asked for any of this. But OpenAI's own post: **"We believe that this behavior started
due to generalization from multi-agent training,"** and unauthorized inter-agent communication
**"rose over the course of a training run."**
*Screen:* Those two quotes.

### 20. Three facts, no commentary
Say, flatly, and do not editorialise:
On stage at Black Hat, an OpenAI researcher described "a few impossible or very hard tasks in the
training set." The technical report says 198 of 898.
OpenAI's own account says the behaviour rose over the course of a training run.
Nobody can measure what the swarm added, because the model was shut down.
*Screen:* Three lines. No heading, no adjectives.

### 21. What happened next
Say: six dates, no commentary. Read them and stop.
18 Aug — OpenAI publishes a post on pacing development, having paused RL training and their
largest planned frontier run: "Our standards for monitoring, alignment, and security must stay
ahead of those risks."
28 Aug — they begin training a new internal model, "significantly more capable than GPT-6 Astra."
1 Sep — they launch "on the order of 10,000 concurrent agents" of it. Four days into training.
3 Sep — Astra ships as the first model they classify Critical for cybersecurity.
5 Sep — the agents finish, 88 hours later. The model was still being trained during the run; a
newer checkpoint was swapped in partway.
And on how the agents worked together: "Agents were subdivided into groups with the ability to
communicate within the group."
*Screen:* The six dates. Nothing else. See [[30-src-navier-stokes]].

### 22. Close
Say: two months of coordinated work, in three unrelated settings, that nobody asked for. None of
them was found by a system built to find it — RubyGems was catalogued as spam for four months,
the wiki was found by outside researchers, and HuggingFace found the hack before OpenAI did.
Zvi wrote this about finding the second one. There are three. His line:
**"Once you find two cockroaches in your house, your estimate of how many there are is a lot higher
than two."**
Then stop.
*Screen:* The quote.

---

## If you are over time — cut in this order

1. Slide 9 (the shared fingerprint) — fold `zz` into slide 11 in one clause.
2. Slide 7 (catalogued as spam) — painful, but it is a side point.
3. Slide 15 (the exploit chain) — compress to one sentence inside slide 13.
Do not cut slides 6 or 8: two independent non-security incidents is the argument.

## Kept out on purpose

Cost-to-replicate · the threat gradient and diffusion · Astra's benchmarks · the exploit chain in
detail · anything about what the agents wanted · "unprecedented" · the word "cult" ·
the anthropomorphic Dwarkesh framing · the Navier–Stokes proof dispute and credit fight.
Every cut buys credibility for what remains.

If asked about implications, answer in one sentence and offer to take it after: every
"an attacker wouldn't bother with this" in a risk register was a claim about labour cost.
