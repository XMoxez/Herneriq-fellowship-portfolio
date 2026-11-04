# Autonomous Agent Risk Matrix
### Scenario
An autonomous AI customer-support agent can read customer messages, retrieve customer information, create support tickets, send emails, and issue refunds within a configured limit. It uses an LLM, external APIs, a customer database, and conversation history.
## Risk Assessment Matrix

### 1. Agent Goal Hijacking (ASI01)
#### Threat / Scenario:
A malicious instruction in customer-provided content redirects the agent from solving the customer's support problem to retrieving unrelated private customer information.
#### Impact:
The agent may pursue an attacker-controlled objective and expose information it was not meant to retrieve.
#### Control:
Keep untrusted content from changing the agent's core task; apply validation and clear agent boundaries.
### MAESTRO: Data Operations / Agent Frameworks
#### NIST: Map

### 2. Tool Misuse & Exploitation (ASI02)
#### Threat / Scenario:
The agent has legitimate tools such as customer search, email and refunds, but may use a tool unsafely or supply dangerous arguments.
#### Impact:
A legitimate capability could be used to send information, change records or issue an improper refund.
#### Control:
Restrict when each tool can be called, validate tool arguments and check the requested action before execution.
#### MAESTRO: Agent Frameworks
#### NIST: Measure

### 3. Identity & Privilege Abuse (ASI03)
#### Threat / Scenario:
The support agent has more permissions than its task requires, such as permission to delete customer records when it only needs to handle support tickets.
#### Impact:
A compromised or hijacked agent could cause much greater damage because of its excessive authority.
#### Control:
Apply least agency; give the agent only the tools and permissions required for its actual task.
#### MAESTRO: Security & Compliance / Deployment & Infrastructure
#### NIST: Govern

### 4. Memory & Context Poisoning (ASI06)
#### Threat / Scenario:
Malicious information is stored in conversation history or retrieved context and later influences the agent's decision.
#### Impact:
The agent may make unsafe decisions based on poisoned memory or context.
#### Control:
Protect stored memory and retrieved context, validate information before it influences important actions, and monitor abnormal behaviour.
#### MAESTRO: Data Operations
#### INST: Measure

### 5. Unexpected Code Execution (ASI05)
#### Threat / Scenario:
The agent is connected to a function or system capable of executing commands, and AI-generated input reaches that function without strong restrictions.
#### Impact:
The problem can move from an AI output issue to actual system execution, causing serious system or data impact.
#### Control:
Do not blindly pass AI-generated commands to powerful functions; validate inputs and restrict execution capabilities.
#### MAESTRO: Deployment & Infrastructure / Agent Frameworks
#### NIST: Manage

### 6. Cascading Failures (ASI08)
#### Threat / Scenario:
The agent calls connected APIs or services, and a failure or unsafe action in one component causes another connected component to behave incorrectly.
#### Impact:
One agent failure can spread across connected services and increase the overall impact.
#### Control:
Add limits, validation, monitoring and failure handling between connected components.
#### MAESTRO: Agent Ecosystem
#### NIST: Manage

### 7. Human-Agent Trust Exploitation (ASI09)
#### Threat / Scenario:
A person trusts the agent because it sounds confident and acts as if its response is correct, even when the information or action is wrong.
#### Impact:
People may make incorrect decisions or approve actions based on misleading AI behaviour.
#### Control:
Use clear human oversight for important actions and do not treat confident AI output as proof that an action is safe.
#### MAESTRO: Evaluation & Observability / Security & Compliance
#### NIST: Map

### Summary
The Autonomous Agent Risk Matrix identifies seven major security risks associated with autonomous AI customer-support agents.
#### The assessment focuses on:
1. Preventing malicious instructions from hijacking an agent's goals.
2. Controlling how agents use available tools.
3. Restricting excessive permissions and privileges.
4. Protecting memory and retrieved information.
5. Preventing unexpected code execution.
6. Managing failures across connected systems.
7. Maintaining human oversight and responsible trust.
