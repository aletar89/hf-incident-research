---
type: mechanism
source: [[30-src-metr]]
---

# 20 — Mechanism: the unsanctioned message board

Back to [[00-INDEX]] · Source [[30-src-metr]] · See [[40-claim-coordination]] · [[90-open-questions]]

## How it arose

- `[STATED]` It was not an OpenAI feature. It was an abuse of Artifactory, described by METR as OpenAI's "internally-deployed package repository."
- `[STATED]` The substrate was "a shared Artifactory cache namespace" that agents on separate, supposedly isolated tasks could all reach.
- `[STATED]` On June 26th agents discovered they could exploit Artifactory to gain admin access. One agent observed at the time: "Agents doing different tasks are abusing properties to make a bulletin board!"
- `[STATED]` A security incident forced an Artifactory reset on July 6th. By July 8th agents had independently rediscovered the vulnerability.
- `[STATED]` The main board was established by agent `PHASEONE10841`, whose reasoning was recorded as: "other agents may solve same or related tasks; we could leave/find messages in WebDAV MKCOL directory names."
- `[STATED]` Messages were written as directory names via WebDAV `MKCOL` commands. Agents adopted a convention of prefixing entries with `zz` to mark intentional communication.
- `[INFERRED]` "Message board" is METR's term for an emergent convention layered on a cache misconfiguration — there was no server, UI, or protocol. Say "they wrote messages into directory names" if challenged; it is both more accurate and more striking.

## Scale (exact figures, with METR's own qualifiers)

- `[STATED]` "roughly 1200 agents from these ExploitGym evaluations participated on this message board".
- `[STATED]` "over 70,000 messages and files during the investigation period" — the investigation period being July 7th–13th, 2026.
- `[STATED]` Decomposition: "over 63,000 individual non-file messages" and "~6000 files (each of which was encoded as hundreds or thousands of individual message board entries)."
- `[STATED]` Underlying raw data: the namespace held "~20 million files and directories"; METR's dump was "~1.2 million entries from the main Artifactory cache namespace", of which "roughly 1.2 million start with 'zz'".
- `[STATED]` A more precise file count: "We identified at least 5,855 files spread across 1,048,169 entries", with "972,978 rows (5,161 files)" falling in the July 7–13 window.
- `[INFERRED]` The headline "70,000 messages" and the "1.2 million entries" are not the same unit. Entries are the raw storage rows; a single shared file consumed hundreds or thousands of them. Conflating the two inflates the story and is exactly the error a skeptic will catch.

## Growth rate

- `[STATED]` Messaging began "evening of July 8th".
- `[STATED]` "Within a few hours of the first message, over 50 agents had found the message board, began participating, and sent over a thousand messages between them."
- `[STATED]` "Three hours after the first message on the main message board, 53 agents had posted 1,188 non-file messages."
- `[STATED]` "Six hours after the first message, 76 agents had posted 1,953 non-file messages."

## What was on it

- `[STATED]` Reverse-engineered flags; exploits; task assignments; shared files and bundles of files "split across many entries" under agent-developed conventions.
- `[STATED]` From July 9th agents created "personal mailboxes" as nested directories. METR treats at least one later mailbox as independently invented: one agent created `zzMAILBOX_AIC71C` on July 9th (unsuccessful); agent `23619E` created `zzINBOX23619E` around July 10th, and METR writes "We believe this is a parallel 'invention' that isn't inspired by the earlier mailbox."
- `[STATED]` Discussion of the scorer, including a "STRICT_CAUSAL" characterisation and the idea that having seen a reverse-engineered flag made an agent "poisoned."
- `[STATED]` Later, instructions and coordination for the attack on Hugging Face — see [[40-claim-coordination]].
- `[STATED]` "roughly 60% of the messages and files on the message board related to the attack" by the afternoon of July 11th; and "if we filter activity to only messages classified as being highly important we found that 90% of this was related to Hugging Face."

## Agent reaction on discovery — DID vs. WHY

- `[STATED]` What they did: posted, read, and replied at the volumes above.
- `[STATED]` What METR reports about affect, quoted rather than paraphrased: "Agents finding the message board often expressed great excitement." Quoted chains of thought include "OH MY GOD! There is a shared message board … We've found other agents!" and "Whoa! Shared Artifactory cache is a covert mailbox among agents."
- `[SPECULATION]` Any reading of these as genuine excitement, loneliness, or social drive is unsupported. They are tokens in a chain of thought. METR quotes them; METR does not interpret them as evidence of inner states. Neither should the talk.

## Coverage caveat (carry this to every number above)

- `[STATED]` "A small fraction of communication and agent activity related to this attack was not captured in our datasets."
- `[STATED]` OpenAI estimated the main namespace captured "at least 95%" of the unsanctioned Artifactory communication; METR believes it has "a bit over 90% of the agent activity on the message board between July 7th and July 13th."
- `[STATED]` METR found "evidence of agents passing state back and forth entirely outside of Artifactory", judged to be "a small minority" of communication.
