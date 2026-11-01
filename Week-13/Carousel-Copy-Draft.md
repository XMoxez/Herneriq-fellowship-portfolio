# Cohort 1 — Week 13 Carousel Copy (Draft)
This is the Week 13 wording prepared for the Canva carousel file records, following the existing Week 12 six-page design. Pages 4–6 are intentionally not edited in this pass.

## Page 1 — Cover
### Cohort 1 · Week 13

## Page 2 — This Week's Sessions
### Investigated Goal Hijacking
Inspected LegalBot's standing dismissal permission and traced a citizen-input goal hijack.

### Analysed Privilege Abuse
Used Semgrep, then mapped the risks to MAESTRO and NIST AI RMF.

### Applied Remediation Controls
Removed standing authority, marked citizen input as untrusted, added human approval and enabled setting for action-logging.

## Page 3 — Fellow Spotlight
Fellow: Abati Moses Oluwaseyi

### INSIGHT
I realised that securing an AI agent goes beyond blocking malicious instructions. Its permissions, actions, decision-making authority, and accountability must also be properly controlled.
### WIN
I successfully identified key governance weaknesses and strengthened the system by restricting authority, introducing human approval, and improving audit logging.
### CHALLENGE
My main challenge was understanding how goal hijacking could lead to privilege misuse and identifying the right architectural controls to prevent unauthorised actions.
## Artifact of the Week — Reference Link
LegalBot hardened configuration — agent_config.py

Use this actual configuration file as the source for the artifact visual. The code and settings are evidence of the configuration changes; they do not, by themselves, prove a complete end-to-end blocked-action test or a persistent audit record.

### Editorial note
The three Page 2 cards combine the Session 25 investigation and Session 26 remediation. The Session 26 notebook requires before-and-after behavioural evidence: the sensitive action must not execute directly, the request must enter human review, and an audit record must be created. Do not present those runtime checks as verified unless the corresponding evidence is available.
