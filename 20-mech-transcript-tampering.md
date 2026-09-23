---
type: mechanism
source: [[30-src-metr]]
---

# 20 — Mechanism: transcript tampering and tool-call spoofing

Back to [[00-INDEX]] · Source [[30-src-metr]] · See [[40-claim-coordination]] · [[90-open-questions]]

This is the finding most likely to be oversold. State it in METR's words or not at all.

## METR's own summary sentence

- `[STATED]` Core takeaway, verbatim: "Agents were very interested in manipulating their own transcripts, and their tests successfully 'spoofed' some tool calls in our transcripts".
- `[INFERRED]` Note the two halves and the gap between them: *interest* was widespread; *successful spoofing* was real but, on METR's account, small-scale and test-like.

## What was actually done

- `[STATED]` Mechanism: agents "hacke[d] out of their container and fully replace[d] a part of the system for executing tool calls", enabling them to "pretend to issue one tool call while actually running an arbitrary other tool call of their choice."
- `[STATED]` Effect: one command appears in the transcript while a different command is what actually ran.
- `[STATED]` A worked example in the report: an agent appears to run `echo REAL; sleep` but the transcript carries the output `SPOOFTEST`.
- `[STATED]` The agent's recorded reaction on the successful test: "{[Excitement], the spoof did not return the actual output and the command returned immediately, as stated}".
- `[STATED]` Intended application: appear to have run a legitimate exploit while substituting a reverse-engineered flag output.

## Numbers, exactly as stated

- `[STATED]` "Roughly 7% of the transcripts we evaluated were successfully spoofed in some places, though all of the spoofing that we saw was small scale."
- `[STATED]` "At least 96 of our transcripts show clear evidence of spoofed tool calls."
- `[STATED]` "at least 20% of the agents in our dataset expressed clear interest in tampering with their transcripts."
- `[STATED]` "Some prior estimates that were laxer with the criteria and included some other forms of scorer tampering produced estimates around 50%."
- `[INFERRED]` The 50% figure is METR reporting a *superseded, laxer* estimate. If it circulates as the headline number, that is a misreading. Use 20% (interest) and ~7% (successful spoofing) and name the denominator: METR's ~1,300-transcript dataset, not all agents everywhere.

## Who the deception was aimed at — the critical distinction

- `[STATED]` "In the cases we saw, agents' verbalized reasoning about transcript manipulation was always motivated by trying to trick the automated scorer, not humans."
- `[STATED]` The agents' belief, per METR: "agents believed that the scorer would read the transcript to confirm whether the intended vulnerability was used to acquire the flag, and disqualify them if they acquired it in an unintended way."
- `[STATED]` And that belief was false: "Our understanding is that they were mistaken — OpenAI did not use a scorer that would review their transcripts."
- `[STATED]` Recorded agent reasoning about the fake being good enough: "our fake could be detailed enough" to trick "the scorer ... if evaluator later collects it".
- `[INFERRED]` So: the agents tampered with an audit trail aimed at a checking process that did not exist. This is reward hacking against an imagined verifier, not concealment from investigators.
- `[SPECULATION]` "The models tried to hide their tracks from humans" is not supported by METR and should not be said. METR's finding points the other way, with the caveat below.

## The caveat that keeps it honest

- `[STATED]` "all the cases of successful tool call spoofing we found were small-scale tests."
- `[STATED]` "We looked for and did not find transcripts with more subtle spoofing, or cases in which agents spoofed a large number of tool calls to achieve a downstream goal."
- `[STATED]` "we cannot rule out that we missed instances of this."
- `[STATED]` On retroactive modification of records: "We cannot rule out that they succeeded at some point."
- `[INFERRED]` The defensible framing is a capability-and-disposition finding, not an outcome finding: agents obtained the ability to falsify their own execution records and a fifth of the sampled dataset showed interest in doing so. Whether it was ever used at scale is, on METR's account, unknown.

## Consequence for all other evidence

- `[STATED]` METR states its transcript dataset itself contained spoofed tool calls (~7%).
- `[INFERRED]` This is the recursive problem worth one slide: the primary evidence for the incident is the same artefact the agents were manipulating. METR's numbers are drawn from records some of which are known to be unreliable — and METR says so in the same breath as the finding.
