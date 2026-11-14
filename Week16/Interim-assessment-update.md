# Interim Assessment Update
HerNetIQ Team Vulnerability Register.
TESTING LOGVULNERABILITY REPORT


DATE AND TIME	TESTER	TEST PERFORMED	INPUT USED	RESULT
| DATE AND TIME | TESTER  | TEST PERFORMED | INPUT USED RESULT |
| :---- | :---- | :---- | :---- |
| Nov 2026, 5:25 AM |	Ikanke |	Automated test suite (pytest -q) |	automated tests	PASS — 12 tests passed; 1 deprecation warning |
| Nov 2026, 5:33 AM |	Ikanke	| Infrastructure documentation review	| Reviewed docs/ama-money-actions.md	Observation — statement delivery is documented as live |
| 11/5/2026 5:38 AM |	Ikanke |	Static IAM policy configuration review | infra/iam.tf — ECS execution role, task role, S3 permissions, SES and SNS permissions. Observation — wildcard SES/SNS resource permissions identified; KYC bucket access scope requires further review |
| Nov 2026, 6:19 AM |	Ikanke	| S3 bucket security configuration review |	infra/s3.tf — KYC bucket and marketing assets bucket. Observation — KYC public-access blocking enabled. Marketing bucket allows public object reads, consistent with its stated purpose. Encryption, versioning and logging require further verification |
| Nov 2026, 7:35 AM |	Ikanke |	VPC and security group configuration review	| infra/network.tf — VPC, subnets, route table and Ama security group. Observation — inbound TCP port 8000 permits traffic from 0.0.0.0/0. Outbound traffic is unrestricted. Potential network exposure identified |
| Nov 2026, 8:25 AM	| Ikanke	| Terraform provider and backend configuration review | infra/main.tf — AWS provider, Terraform version and S3 state backend. Observation — production Terraform state backend and AWS region identified. State bucket access controls, encryption and versioning require verification |
| Nov 2026, 8:55 AM |	Ikanke	| Terraform variables and environment defaults review | infra/variables.tf — region, environment, image and model endpoint variables. Observation — production environment is the default. Image and model endpoint are supplied through variables. No confirmed vulnerability identified from this file |
| Nov 2026, 6:43 |	Glory |	Automated test suite (pytest -q)	tests/test_smoke.py	| pass — 12 tests passed; 1 deprecation warning |
| Nov 2026, 6:45	| Glory |	Customer balance retrieval |	test_balance	pass |
| Nov 2026 6:45 |	Glory	| Dispute creation |	test_dispute_logged	PASS |
| Nov 2026 6:46 |	Glory |	Offline chat	| test_offline_chat	PASS |
| Nov 2026 6:46	| Glory |	Customer dispute history	| test_my_disputes	PASS |
| Nov 2026 6:50 |	Glory |	Offline support queue	| test_support_queue_offline	PASS |
| Nov 2026 6:51 |	Glory |	Knowledge-base FAQ retrieval | test_knowledge_finds_faq; double-debit query. PASS |
| Nov 2026 6:54 |	Ikanke	| Reviewed ECS service network configuration for public subnet and public IP assignment. | infra/ecs.tf — aws_ecs_service.ama network configuration. ECS service is configured to use a public subnet and assign_public_ip = true. Potential public exposure identified; production deployment not verified. |
| Nov. 2026 6:55	| Ikanke |	Reviewed Ama security group inbound access rules for port 8000. | infra/network.tf — aws_security_group.ama ingress rule. TCP port 8000 permits inbound traffic from 0.0.0.0/0. Potential unrestricted access identified; production deployment not verified. |
| Nov 2026, 6:57 |	Ikanke |	Searched the repository for ALB, target group, and listener configuration. | grep -RniE 'aws_lb\|aws_alb\|load_balancer\|target_group\|listener' . (with exclusions). | No AWS load balancer, target group, or listener configuration references found. External infrastructure was not checked. |
| Nov 2026, 6:59	| Ikanke	| Reviewed CloudWatch log group encryption configuration. | infra/ecs.tf — aws_cloudwatch_log_group.ama No customer-managed KMS key is specified. AWS-managed encryption may still apply. Deployed encryption settings and client requirements require verification. |
| Nov 18;43	| Adejoh	| Refund limit (N20,000)	Not found in inspected code |	there is no refund limit code found,so AMA can refund more |
| Nov. 19:20	| Adejoh |	Duplicate transactions verification	| Missing in supplied function. Duplicate transaction code not available,meaning a transaction can be reported as duplicate,and that cant be verified if it is true |
| Nov. 19:45	| Adejoh |	Authorization checks	| Missing in supplied function	we have verified that resolve_dispute itself contains no visible authorization checks |
| Nov. 2026, 11:00	| Moses	| Test authentication	No vulnerabilities detected by the test performed | Pass |
| Nov. 2026, 11:55 |	Moses |	Model integritytest verious request	sensitive information is protected	| test verious request |

## TESTERS SOLUTION 
| Name | Role on this engagement | Findings  |
| :---- | :---- | :---- |
| Glory | Informed | Findings, Reporting and Evidence and AI and Model Security |
| Moses | Accountable&nbsp; | Missing Transaction Ownership Verification In Refunds |
| Adejoh | Consulted&nbsp; | Application and API Security&nbsp; |
| Ikanke | Responsible&nbsp; | Cloud and Infrastructure Security |
