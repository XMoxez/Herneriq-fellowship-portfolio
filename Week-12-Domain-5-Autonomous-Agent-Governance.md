The 7 required risk matrix
Risk
Threat / Scenario
Impact
Control
MAESTRO
NIST
1
Prompt injection – An attacker sends crafted instructions that manipulate the AI agent into ignoring its intended instructions.
Unauthorized actions, data exposure, or unsafe AI decisions.
Input validation, prompt/instruction separation, guardrails, adversarial testing, and human approval for sensitive actions.
Layer 1 – Foundation Models
Measure
2
Data poisoning – An attacker inserts false or malicious information into training data or a RAG knowledge base.
The AI produces incorrect, biased, or manipulated answers.
Data validation, trusted data sources, provenance checks, access controls, and continuous data-quality monitoring.
Layer 2 – Data Operations
Measure
3
Agent/tool misuse – A compromised or manipulated agent uses a tool outside its intended purpose, such as executing unauthorized commands.
Unauthorized database changes, data theft, or system compromise.
Least privilege, tool allowlists, parameter validation, sandboxing, and approval before high-risk tool calls.
Layer 3 – Agent Frameworks
Manage
4
Privilege escalation – An AI agent obtains permissions greater than those required for its task.
Attackers could gain access to sensitive systems or move laterally across the environment.
RBAC/IAM, least privilege, short-lived credentials, network segmentation, and continuous access monitoring.
Layer 4 – Deployment & Infrastructure
Manage
5
Insufficient monitoring – Malicious or abnormal agent behavior occurs without adequate logging or detection.
Security incidents may remain undetected, increasing damage and investigation difficulty.
Centralized immutable logs, SIEM monitoring, anomaly detection, alerts, and regular security reviews.
Layer 5 – Evaluation & Observability
Measure
6
Weak security controls – Poor authentication, exposed secrets, or inadequate authorization allows unauthorized access to AI components.
Credential theft, unauthorized access, data leakage, and compromise of the AI system.
MFA, secrets management, encryption, strong authentication, RBAC, policy enforcement, and credential rotation.
Layer 6 – Security & Compliance
Govern
7
Third-party/agent impersonation – A malicious external agent, API, or service pretends to be a trusted component.
Sensitive information may be disclosed or malicious instructions may enter the AI workflow.
Mutual authentication, API security, vendor validation, allowlisting, secure communication, and continuous third-party monitoring.
Layer 7 – Agent Ecosystem
Map
