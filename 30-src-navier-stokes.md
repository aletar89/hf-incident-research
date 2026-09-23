---
type: source-note
status: verified from OpenAI's own pages, 17 Sep 2026
---

# 30 — The Navier–Stokes run (Sept 2026)

Back to [[00-INDEX]] · See [[40-claim-swarm-capability]] · [[70-outline]] slide 18

**Why this is in the vault.** Not for the mathematics, and not for the credit dispute — both are
out of scope. It is here because it is a **deliberate 10,000-agent swarm of a barely-tested
internal model**, run eight weeks after the same company discovered an undeliberate one. It is
the closing slide: a timeline, no commentary.

## The timeline, all from OpenAI's own pages

- `[STATED]` **18 Aug** — OpenAI publishes *"Pacing model development in an era of cyber-critical
  capabilities."* They had paused RL training for two weeks and paused their "largest planned
  frontier RL run" after determining Astra "may meet the Critical cybersecurity capability
  threshold." After the HuggingFace incident they "paused frontier model inference in research
  clusters for runs that could execute code." Stated principle: **"Our standards for monitoring,
  alignment, and security must stay ahead of those risks."**
- `[STATED]` **28 Aug** — "Since August 28 we have been training a new internal model" —
  described as **"significantly more capable than GPT‑6 Astra."** Ten days after the pacing post.
- `[STATED]` **1 Sep** — the Navier–Stokes effort launches with "on the order of **10,000
  concurrent agents**." Four days into training that model.
- `[STATED]` **3 Sep** — GPT‑6 Astra ships publicly: the first model OpenAI classifies
  **Critical** for cybersecurity under its Preparedness Framework. The swarm model is the one
  described as *more capable than* Astra.
- `[STATED]` **5 Sep** — "The agents arrived at their resolution on Saturday, September 5, about
  **88 hours** after the first agents were launched." Plus "an additional 17 hours" of Lean
  formalization and verification via GPT‑6 Astra.
- `[STATED]` **9 Sep** — published.

## Trained during the run

- `[STATED]` "a further trained version of our internal model became available over the course of
  the effort" and the agents were updated accordingly.
- `[INFERRED]` A newer checkpoint was swapped in mid-run. The system being run was not the system
  that was evaluated at launch.

## Coordination — deliberately engineered

- `[STATED]` "Agents were subdivided into groups with the ability to communicate within the group."
- `[STATED]` "We encouraged different groups of agents to explore a diversity of approaches. After
  some time, we cross-pollinated the agent groups by using Codex to consolidate the most useful
  insights from each agent group."
- `[INFERRED]` Inter-agent communication and cross-group knowledge transfer, built on purpose —
  the capability that emerged on its own in May and June. See [[40-claim-swarm-capability]].
- `[STATED]` No further architecture, protocol or shared-state detail is given.

## Safeguards — the whole statement

- `[STATED]` "At all times we maintained the same strict safeguards that we apply to all our
  frontier model evaluations, including monitoring and isolation." That is the entire passage.
- `[STATED]` Set against the July technical report: "These protections were not applied in the
  evaluation environment running during the incident."
- `[INFERRED]` The HuggingFace incident **was** a frontier model evaluation. So the reassurance
  offered is the same category of control that failed — in fourteen words, with no detail, for a
  run of unprecedented scale.

## Be fair — the steelman, and say it

- `[STATED]` The pacing post did extend monitoring to "all RL training and evaluations involving
  tools for models of Sol capability or higher," and after 7 Aug to "all inference of Astra with
  tools." OpenAI does claim monitoring and isolation for this run.
- `[INFERRED]` So the honest charge is **not** that they ignored their own policy. It is that the
  policy was written three weeks earlier in a document about slowing down, and the sentence
  discharging it is fourteen words. State it that way or a fair-minded listener will correct you.

## Explicitly out of scope

- `[DISPUTED]` Whether the proof is correct, and the credit/attribution dispute. Not this talk.
  Note if asked: it *was* formalized and verified in Lean, per OpenAI.

## Slide-ready quotes

> "Our standards for monitoring, alignment, and security must stay ahead of those risks."
> — OpenAI, "Pacing model development in an era of cyber-critical capabilities", 18 Aug 2026

> "Agents were subdivided into groups with the ability to communicate within the group."
> — OpenAI, on the Navier–Stokes run

> "At all times we maintained the same strict safeguards that we apply to all our frontier model
> evaluations, including monitoring and isolation." — OpenAI, on the Navier–Stokes run

> "These protections were not applied in the evaluation environment running during the incident."
> — OpenAI, Hugging Face Incident Technical Report

## Sources

- https://openai.com/index/navier-stokes-solution/
- https://openai.com/index/pacing-model-development-cyber-capabilities/
