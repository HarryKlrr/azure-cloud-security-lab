# Azure Cloud Security Lab

Cloud-side detection work on Microsoft Azure. This is the follow-on to my
[SOC Detection Lab](https://github.com/HarryKlrr/soc-detection-lab), which
covered on-prem Windows telemetry through Wazuh. This one moves the same
question — *would I actually see this happen?* — into a cloud tenant.

**Status: in progress.** The tenant is up and logs are flowing. The detection
content is not finished, so there are no incident reports here yet. I would
rather say that than publish an empty folder structure and call it complete.

---

## Why I'm building it

Most of the job adverts I'm reading for junior SOC roles list Microsoft
Sentinel or Defender somewhere in the requirements, and a lot of them are for
teams whose estate is mostly Microsoft 365 and Entra ID rather than servers in
a rack. My Wazuh lab taught me how a detection fires against endpoint
telemetry. It didn't teach me what an identity attack looks like in sign-in
logs, or how you write a KQL query when someone hands you a question instead of
an alert.

So the point of this lab is narrower than "learn Azure". It's to get to the
stage where I can read a Sentinel incident, pivot into the raw table it came
from, and say something useful about it.

---

## What's in the environment

| Component | What it's for |
|---|---|
| Entra ID tenant | Users, groups, conditional access, sign-in and audit logs |
| Log Analytics workspace | Where the logs land and where KQL runs |
| Microsoft Sentinel | SIEM layer — analytics rules, incidents, workbooks |
| Defender for Cloud | Posture management and the secure score baseline |

Everything is inside a free/developer tenant that I own. No real user data is
involved and nothing here touches a production system.

---

## The plan

1. **Get logs in.** Sign-in logs, audit logs and activity logs into Log
   Analytics, and confirm they're actually arriving rather than assuming.
2. **Break things deliberately.** Impossible-travel sign-ins, a stale account
   given Global Administrator, conditional access switched off, a storage
   account opened to public read. The same approach as the Wazuh lab: cause the
   event, then go looking for it.
3. **Write the KQL.** One hunting query per misconfiguration class, saved with
   a short note on what it catches and where it would be noisy.
4. **Turn the good ones into analytics rules** and check they produce a
   sensible Sentinel incident rather than a wall of duplicates.
5. **Write it up.** A short remediation note per finding, and a baseline
   hardening guide for a small tenant.

---

## Progress

| Step | State |
|---|---|
| Tenant and workspace built | Done |
| Sign-in / audit / activity logs ingesting | Done |
| Misconfigurations introduced | In progress |
| KQL hunting queries | In progress |
| Analytics rules and tuning | Not started |
| Remediation notes and baseline guide | Not started |

I'll update this table as things land rather than rewriting history at the end.

---

## A note on scope

I'm one person with a developer tenant, so this is a learning lab, not a
representative enterprise estate. Some of what a real environment would throw
at you — scale, noise, competing business requirements, other people's
mistakes — isn't reproducible here, and I'm not going to pretend otherwise.
What it does give me is the query language, the log schemas, and the habit of
checking whether a control actually works instead of trusting that it does.

---

## Author

**Harry Klair** — BSc (Hons) Cyber Security, Nottingham Trent University.
SC cleared. Working toward CompTIA Security+.

Portfolio: [harryklrr.github.io](https://harryklrr.github.io) ·
GitHub: [@HarryKlrr](https://github.com/HarryKlrr)
