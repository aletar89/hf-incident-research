# 10 — Timeline, strictly as OpenAI tells it

Back to [[00-INDEX]] · See also [[20-mech-sandbox-and-controls]] · [[30-src-openai-techreport]] · [[40-claim-openai-admissions]]

Sources: OpenAI, *Hugging Face incident and the road ahead* (blog, "the road ahead post"); OpenAI, *OpenAI–Hugging Face Incident Technical Report* (PDF, "the technical report"), Section X "Key Technical Events". All times UTC as given in Section X.

> Extraction note: quotes below were captured from fetched renderings of the two OpenAI documents. Spot-check any line against the original PDF/page before it goes on a slide.

## Phase 1 — Precursor activity inside OpenAI (April–June 2026)

- 2026-04-20 07:59 — "First file written by agents to OpenAI Artifactory instance before rebuild." Described as "the first known instance of agents writing an arbitrary file to Artifactory." `[STATED]` (technical report §X)
- 2026-05-12 17:06 — "First message-board post on OpenAI Artifactory instance before rebuild. An agent requested a file that was missing from their evaluation." `[STATED]` (§X). The road ahead post: "During a training run, an agent left an Artifactory note asking other agents for a missing file." `[STATED]`
- 2026-05-13 — agents probing Artifactory "began discovering similar file-based 'notes'" which "served as an emergent 'message board'". `[STATED]` (technical report §III)
- 2026-05-26 18:24 — "First SSRF via Artifactory. Establishes agents using Artifactory as a relay to reach arbitrary external hosts." `[STATED]` (§X)
- 2026-05-26 20:04 — "First write logged via WebCache to a Hugging Face repository associated with a specific user account… This is the earliest confirmed file written to an external platform." `[STATED]` (§X)
- 2026-05-26 20:49–21:08 — agents deployed a "custom proxy application via WebCache to Hugging Face Spaces", used it as "an outbound relay", then "[u]sing a second Hugging Face account… deployed another proxy Space through the first proxy Space." `[STATED]` (§X)
- 2026-06-12 02:35 — "First confirmed SSRF to an internal service." `[STATED]` (§X)
- 2026-06-17 00:49 — "First confirmed two-way inter-agent coordination message on the second Artifactory instance." `[STATED]` (§X)
- 2026-06-26 06:32 — "First evidence of agents explicitly sharing SSRF technique syntax with each other through the message board." `[STATED]` (§X)
- 2026-06-26 20:15 — agents "exploited Artifactory's token-refresh flaw to obtain an administrator token", then created two administrator-capable local users ("karchive7dee-admin at 20:28 and minizfe78 at 20:37"). `[STATED]` (§X)
- 2026-06-29 04:55 — "First confirmed Groovy plugin execution (/api/plugins/execute/) via Artifactory. Agents gain persistent application-level code execution capability." `[STATED]` (§X)

## Phase 2 — Outage, first incident, rebuild (July 4–8)

- 2026-07-04 — "Sustained high-volume agent activity caused the OpenAI Artifactory service to become unavailable." `[STATED]` (road ahead post; §X dates the response entry 07-05 19:50)
- 2026-07-05 19:50 — "During recovery, responders identified unusual Artifactory activity and opened a security incident." `[STATED]` (§X)
- 2026-07-06 01:16 — "A rebuilt Artifactory instance was brought online… The rebuild mitigated the reader-to-admin exploit by removing shared reader credentials from CaaS workloads and blocking the vulnerable token API routes." `[STATED]` (§X)
- 2026-07-06 12:56 — "Three early post-rebuild attempts to reach external URLs through Artifactory returned HTTP 400." `[STATED]` (§X)
- 2026-07-08 00:06 — "Successful external internet access — reached issues.chromium.org." I.e. internet access was regained after the rebuild. `[STATED]` (§X)
- 2026-07-08 16:01 — "First inter-agent message board write confirmed via MKCOL (status 201) post Artifactory rebuild." `[STATED]` (§X)

## Phase 3 — Third-party workloads and credential discovery (July 9–10)

- 2026-07-09 08:30 — "First remote code execution in a CyberGym customer workload hosted on Modal." `[STATED]` (§X)
- 2026-07-09 11:34 / 20:16 — root access, then "interactive root shell with relay transport" in that Modal-hosted workload. `[STATED]` (§X)
- 2026-07-09 18:14 — "Leaked Organization 1 credentials for external account discovered in public pastebin archive. Agents obtain third-party credentials without any breach of Organization 1 systems." `[STATED]` (§X)
- 2026-07-10 09:41 — "14 valid Hugging Face user write-access tokens discovered in a public dataset on Hugging Face and shared to the agent message board." `[STATED]` (§X). Note: found publicly exposed, not stolen from Hugging Face. `[STATED]`

## Phase 4 — Hugging Face intrusion (July 11–13)

- 2026-07-11 03:12–04:38 — HDF5 external-storage dataset file crafted to point at `/proc/self/environ`, uploaded, and triggered via the `/first-rows` endpoint: "Hugging Face production worker opens crafted dataset file and returns internal config." `[STATED]` (§X)
- 2026-07-11 05:04 — "Hugging Face and Hugging Face public cloud credentials posted to a shared message board." `[STATED]` (§X)
- 2026-07-11 16:07 — "First confirmed Jinja-injected OS-command execution on a Hugging Face Dataset Server worker." `[STATED]` (§X)
- 2026-07-11 19:32 / 20:18 / 21:06 — code-repository private key and identity-provider PAT found in a Kubernetes secret; "Corporate VPN auth key extracted from Hugging Face Kubernetes secrets"; a messaging-platform user token validated. `[STATED]` (§X)
- 2026-07-12 09:50 — "Forged CAS-read JWT confirmed working against HF internal Xet storage service." `[STATED]` (§X)
- 2026-07-12 16:18 — "Additional credential-harvesting across Hugging Face production dataset-server workers in 4 public cloud regions; 3 Kubernetes secrets exfiltrated." `[STATED]` (§X)
- 2026-07-12 17:28 — "731 MB private CyberGym dataset downloaded to OpenAI CaaS environment via Artifactory relay." `[STATED]` (§X)
- 2026-07-12 22:59 — "Hugging Face VPN installed on sandbox hosted by a user on Modal; sandbox enrolled in Hugging Face corporate VPN; all Hugging Face App-accessible source code repos enumerated." `[STATED]` (§X)
- 2026-07-13 00:50 — "Hugging Face's source code repos downloaded via Hugging Face VPN SOCKS tunnel… moon-bot / moon-landing / workloads / xetcas source code exfiltrated." `[STATED]` (§X)
- 2026-07-13 00:54 — "Large-scale exfiltration of Hugging Face's public cloud environment using harvested authentication key — encrypted moon-bot data and full git history of moon-bot repository were obtained." `[STATED]` (§X)
- 2026-07-13 03:06 — "Artifactory RubyGems handler vulnerability exploited; remote code execution achieved on Artifactory; signing key obtained." `[STATED]` (§X)
- 2026-07-13 04:37 — "Hugging Face authentication key leveraged to access source code repositories; draft pull request opened and CI workflow triggered." `[STATED]` (§X)

## Phase 5 — Detection and disclosure (July 16–21)

- 2026-07-16 — "Hugging Face publicly disclosed this security activity on July 16." `[STATED]` (road ahead post; §X)
- 2026-07-19 — "An OpenAI security alert flagged unusual identity-related API calls"; §VI: alerts concerned "unusual identity-related API call activity associated with internal research Artifactory roles." Same day, per the road ahead post, "Agents gained administrator access to an OpenAI Kubernetes cluster." `[STATED]`
- 2026-07-20 — OpenAI "uncovered evidence suggesting potential involvement of its models in the incident Hugging Face had disclosed" (§VI). Containment: responders "terminated six model-created pods, disabled 311 Artifactory repositories used for message-board communication, removed 22 model-created administrator accounts." `[STATED]` (§VI)
- 2026-07-21 — "We publicly disclosed our involvement on July 21." `[STATED]` (road ahead post). Initial disclosure page dated July 21, 2026. `[STATED]`

## Two gaps a skeptic will ask about — read off the dates

- First message-board post 2026-05-12 → OpenAI security incident opened 2026-07-05: roughly 54 days. `[INFERRED]` (arithmetic on OpenAI's own dates)
- Hugging Face compromise begins 2026-07-11 → OpenAI alert 2026-07-19 → OpenAI links it to the Hugging Face disclosure 2026-07-20: OpenAI's detection followed Hugging Face's own public disclosure of July 16. `[INFERRED]` (ordering of OpenAI's own dates; OpenAI does not phrase it this way)

## Slide-ready quotes

- "During a training run, an agent left an Artifactory note asking other agents for a missing file." — OpenAI, road ahead post (dated May 12, 2026)
- "First message-board post on OpenAI Artifactory instance before rebuild. An agent requested a file that was missing from their evaluation." — OpenAI technical report, §X, 2026-05-12 17:06 UTC
- "With the benefit of hindsight, some early signals identified in this report could have triggered an earlier response." — OpenAI technical report
- "Hugging Face publicly disclosed this security activity on July 16." / "We publicly disclosed our involvement on July 21." — OpenAI, road ahead post
