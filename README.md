# OpenAI agent-swarm incidents (2026): research vault

Research behind the Contiamo Show and Tell talk "The HuggingFace incident" (23 Sept 2026).
Everything here comes from public sources.

- **Slides:** [`agent-swarms.html`](agent-swarms.html), a self-contained HTML deck. Download and open it in a browser.
- **Notes:** 48 Markdown files, written as an Obsidian vault. `[[name]]` links point to `name.md` in this folder.

## For agents

Start at [`00-INDEX.md`](00-INDEX.md). It states the talk's thesis and says what to read first. Sources are in [`05-sources.md`](05-sources.md), and they win over any note that disagrees with them.

Every factual line carries a provenance tag. Keep it when you quote the line:

| Tag | Meaning |
|---|---|
| `[STATED]` | a source says it directly |
| `[INFERRED]` | a source concludes it from evidence it shows |
| `[DISPUTED]` | sources conflict |
| `[SPECULATION]` | commentary, not established |
| `[ILLUSTRATIVE]` | a constructed example, never a real named instance |
| `[BREAKING]` | single source or social media, days old at time of writing |

The file prefix gives the kind of note:

| Prefix | Contents |
|---|---|
| `00`, `05` | index, source list |
| `10` | narrative arc, timeline |
| `20-mech-*` | mechanics: the eval, sandbox, exploit chain, message board |
| `30-src-*` | readings of individual sources (OpenAI, METR, commentators, critics) |
| `40-claim-*` | claims and counter-claims, with evidence |
| `50-fwd-*` | forward-looking implications |
| `60`, `70`–`73` | presentation device, outlines, slide text |
| `90` | open questions |

Clone it to search across all notes (best for real questions):

```sh
gh repo clone aletar89/hf-incident-research && cd hf-incident-research
```

Or read single files without cloning:

```sh
gh api repos/aletar89/hf-incident-research/contents/00-INDEX.md -H "Accept: application/vnd.github.raw"
# no auth needed: https://raw.githubusercontent.com/aletar89/hf-incident-research/main/00-INDEX.md
```

The notes date from early September 2026. `30-src-sept-updates.md` covers later developments up to 21 Sept.
