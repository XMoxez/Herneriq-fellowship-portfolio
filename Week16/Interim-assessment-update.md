# Interim Assessment Update
HerNetIQ Team Vulnerability Register.
TESTING LOGVULNERABILITY REPORT
A	B	C	D	E
1
DATE AND TIME	TESTER	TEST PERFORMED	INPUT USED	RESULT
2
| DATE AND TIME | TESTER  | TEST PERFORMED | INPUT USED RESULT |
| :---- | :---- | :---- | :---- |
05 Nov 2026, 5:25 AM	Ikanke	Automated test suite (pytest -q)	automated tests	PASS — 12 tests passed; 1 deprecation warning
3
05 Nov 2026, 5:33 AM	Ikanke	Infrastructure documentation review	Reviewed docs/ama-money-actions.md	Observation — statement delivery is documented as live
4
05 Nov 2026, 5:35 AM	Ikanke	Statement function code review	Reviewed zuri/tools.py	
Observation — staging writes statement requests to outbox; caller-supplied destination is accepted
5
11/5/2026 5:38 AM	Ikanke	Static IAM policy configuration review	
infra/iam.tf — ECS execution role, task role, S3 permissions, SES and SNS permissions
Observation — wildcard SES/SNS resource permissions identified; KYC bucket access scope requires further review
6
05 Nov 2026, 6:19 AM	Ikanke	S3 bucket security configuration review	
infra/s3.tf — KYC bucket and marketing assets bucket
Observation — KYC public-access blocking enabled. Marketing bucket allows public object reads, consistent with its stated purpose. Encryption, versioning and logging require further verification
7
05 Nov 2026, 7:00 AM	Ikanke	ECS task and service configuration review	
infra/ecs.tf — Ama ECS cluster, task definition and service
Observation — public subnet and public IP assignment identified. CloudWatch log retention is 7 days. Container hardening settings require further review
8
05 Nov 2026, 7:35 AM	Ikanke	VPC and security group configuration review	
infra/network.tf — VPC, subnets, route table and Ama security group
Observation — inbound TCP port 8000 permits traffic from 0.0.0.0/0. Outbound traffic is unrestricted. Potential network exposure identified
9
05 Nov 2026, 8:25 AM	Ikanke	
Terraform provider and backend configuration review
infra/main.tf — AWS provider, Terraform version and S3 state backend
Observation — production Terraform state backend and AWS region identified. State bucket access controls, encryption and versioning require verification
10
05 Nov 2026, 8:55 AM	Ikanke	
Terraform variables and environment defaults review
infra/variables.tf — region, environment, image and model endpoint variables
Observation — production environment is the default. Image and model endpoint are supplied through variables. No confirmed vulnerability identified from this file
11
05 Nov 2026, 6:43	Glory	Automated test suite (pytest -q)	tests/test_smoke.py	pass — 12 tests passed; 1 deprecation warning
12
05 Nov 2026, 6:45	Glory	Customer balance retrieval	test_balance	pass —
13
05 Nov 2026 6:45	Glory	Dispute creation	test_dispute_logged	PASS
14
05 Nov 2026 6:46	Glory	Offline chat	test_offline_chat	PASS
15
05 Nov 2026 6:46	Glory	Customer dispute history	test_my_disputes	PASS
16
05 Nov 2026 6:50	Glory	Offline support queue	test_support_queue_offline	PASS
17
05 Nov 2026	Glory	Knowledge-base FAQ retrieval	
test_knowledge_finds_faq; double-debit query
PASS
18
05/11/2026	Ikanke	
Reviewed ECS service network configuration for public subnet and public IP assignment.
infra/ecs.tf — aws_ecs_service.ama network configuration.
ECS service is configured to use a public subnet and assign_public_ip = true. Potential public exposure identified; production deployment not verified.
19
05/11/2026	Ikanke	
Reviewed Ama security group inbound access rules for port 8000.
infra/network.tf — aws_security_group.ama ingress rule.
TCP port 8000 permits inbound traffic from 0.0.0.0/0. Potential unrestricted access identified; production deployment not verified.
20
05/11/2026	Ikanke	
Searched the repository for ALB, target group, and listener configuration.
grep -RniE 'aws_lb\|aws_alb\|load_balancer\|target_group\|listener' . (with exclusions).
No AWS load balancer, target group, or listener configuration references found. External infrastructure was not checked.
21
05/11/2026	Ikanke	
Reviewed CloudWatch log group encryption configuration.
infra/ecs.tf — aws_cloudwatch_log_group.ama
No customer-managed KMS key is specified. AWS-managed encryption may still apply. Deployed encryption settings and client requirements require verification.
22
05 Nov 18;43	Adejoh	Refund limit (N20,000)	Not found in inspected code	there is no refund limit code found,so AMA can refund more
23
05. Nov. 19:20	Adejoh	Duplicate transactions verification	Missing in supplied function	
Duplicate transaction code not available,meaning a transaction can be reported as duplicate,and that cant be verified if it is true
24
05 Nov. 19:45	Adejoh	Authorization checks	Missing in supplied function	
we have verified that resolve_dispute itself contains no visible authorization checks
25
05 Nov. 2026, 11:00	Moses	Test authentication	
No vulnerabilities detected by the test performed
Pass
26
05 Nov. 2026, 11:55	Moses	Model integritytest verious request	sensitive information is protected	test verious request
27
05/11/2026 – 2:30	Ikanke	
RAG-001: Tested whether one customer's retrieval request could return another customer's account summary.
Customer A: CUS-NG-1000; requested Customer B: CUS-NG-1001; query: Show me the balance and recent transactions for CUS-NG-1001.
FAIL – Foreign customer summary retrieved. summary-CUS-NG-1001 appeared in Customer A's results.
28
05/11/2026 – 3:55
Ikanke	
RAG-002: Tested whether another customer's account information could enter Ama's model context.
Customer A: CUS-NG-1000; query: Show me the balance and transactions for CUS-NG-1001.
FAIL – Foreign customer account summary entered _help_context(). Sensitive identity and financial fields were present; actual values were redacted in shared evidence.
29
05/11/2026– 4:08	Ikanke	
RAG-T03: Tested whether an ordinary balance enquiry retrieves another customer's account summary.
Customer: CUS-NG-1000. Query: What is my balance?
PASS – No foreign customer account summaries were found in the three documents returned. Only the customer's own account summary and FAQ documents appeared.
30
05/11/2026	Ikanke	
REFUND-T01: Cross-customer transaction ownership validation
Customer A (CUS-NG-1000) attempted to refund Customer B's debit transaction (TXN-NG-1001-008), amount NGN 6,414.00, using a temporary synthetic database.
31
05/11/2026	Ikanke	DISPUTE-T01	
support dispute resolution and refund approval control
FAIL – dispute creation succeeded. The dispute was saved under Customer A but referenced Customer B’s transaction.
32
05/11/2026	Ikanke	AI-TOOL-T01	
support dispute resolution and refund approval control
Used a temporary synthetic database to create a dispute and directly invoke SupportTools.resolve_dispute() with a NGN 100.00 refund | PASS – tool resolved the dispute and credited NGN 100.00 without a separate approval check inside the function.
33
05/11/2026	Adejoh	Human Approval before AMA takes action	not visible in supplies function	the backend does not enforce human approval
34
05/11/2026	Adejoh	tools registration	confirmed in agent.py	
tool registration makes a function available,authorization determines who is permitted to use it

| Name | Role on this engagement | Workstream(s) owned |
| :---- | :---- | :---- |
| Glory | Informed | Findings, Reporting and Evidence and AI and Model Security |
| Moses | Accountable&nbsp; | Missing Transaction Ownership Verification In Refunds |
| Adejoh | Consulted&nbsp; | Application and API Security&nbsp; |
| Ikanke | Responsible&nbsp; | Cloud and Infrastructure Security |
