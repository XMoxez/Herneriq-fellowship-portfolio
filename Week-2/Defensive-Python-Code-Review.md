MEDVITALS AI Python script 

Security Findings Report

Assessment Area: Cloud Infrastructure and Python Configuration Security
Project: MedVitals AI Defense Lab
Report Type: Security Vulnerability Assessment
Prepared by: Abati Moses, AI Security Fellow
Overall Risk: High — based on the identified configuration weaknesses

1. Executive Summary

During the security assessment of the MedVitals AI Python configuration, two important security weaknesses were identified: hardcoded API credentials and overly permissive cloud access permissions.

These weaknesses could expose sensitive system credentials and allow an attacker to access cloud resources beyond what the application needs.

In a healthcare environment, a successful attack could put patient information at risk, disrupt hospital operations, and damage the organisation's reputation.

The recommended solution is to securely manage credentials, restrict cloud permissions to the minimum necessary, and test the updated configuration to confirm that the security weaknesses have been addressed.

2. Security Findings

Finding 1: Hardcoded API Credentials

Severity: High

What is wrong?

Sensitive API credentials are stored directly inside the Python script or its configuration instead of being managed through a secure secrets-management system.

Where is the problem?

In the MedVitals AI Python configuration, where credentials are defined or used by the application.

Why does this matter?

If the script is uploaded to a public repository, shared with unauthorised people, or accessed by an attacker, the credentials could be exposed.

An attacker who obtains valid credentials may be able to impersonate the application and access services permitted to those credentials.

Recommended fix:

- Remove hardcoded credentials from the source code.
- Store secrets in a secure secrets manager or an appropriately protected environment configuration.
- Rotate any credentials that may already have been exposed.
- Restrict access to secrets and monitor their use.
- Ensure credentials are excluded from version control.

Expected outcome: Credentials are no longer embedded in the source code, reducing the risk of accidental exposure and unauthorised access.

Finding 2: Overly Permissive Cloud Permissions

Severity: High

What is wrong?

The cloud access policy grants permissions that may be broader than the application requires.

For example, permissions that allow access to storage containing patient documents or provide access to database-related resources must be carefully restricted.

Where is the problem?

In the cloud IAM (Identity and Access Management) policy associated with the MedVitals AI application.

Why does this matter?

If an attacker compromises the application's credentials, excessive permissions could allow the attacker to access additional cloud resources.

Depending on the exact permissions granted, this could expose sensitive files, enable unauthorised data access, or increase the attacker's ability to interfere with cloud services.

Recommended fix:

- Apply the principle of least privilege.
- Allow only the specific cloud actions the application needs.
- Restrict access to approved storage buckets, objects, and database resources.
- Avoid wildcard permissions that grant unnecessarily broad access.
- Review permissions regularly and monitor cloud activity.

Expected outcome: The application can perform its legitimate functions without having unnecessary access to sensitive cloud resources.

3. Business and Security Impact

If these weaknesses remain unresolved, MedVitals AI could face the following risks:

Patient confidentiality: Unauthorised access to cloud resources could expose patient information if those resources contain sensitive records.

Operational disruption: Compromised credentials or cloud resources could interfere with the availability or reliability of the application.

Financial and regulatory consequences: A security incident involving patient information could result in investigation costs, recovery expenses, and potential regulatory consequences.

Loss of trust: Patients, healthcare professionals, and business partners may lose confidence in an organisation that fails to protect sensitive information.

These are potential consequences, not evidence that a breach has occurred.

4. Remediation Plan

The following actions are recommended:

Priority| Required Action| Security Benefit
1| Remove hardcoded credentials and rotate potentially exposed secrets.| Reduces the risk of credential misuse.
2| Replace broad cloud permissions with narrowly scoped permissions.| Limits what compromised credentials can access.
3| Restrict access to patient-related storage and database resources.| Reduces the risk of unauthorised data access.
4| Enable appropriate cloud audit logging and monitoring.| Improves the ability to detect suspicious activity.
5| Test the updated configuration and document the results.| Provides evidence that the fixes work as intended.

5. Verification and Evidence

After implementing the fixes, the following checks should be performed:

Credential security

- Inspect the Python script to confirm that live API credentials are no longer hardcoded.
- Verify that secrets are retrieved securely at runtime.
- Confirm that any potentially exposed credentials have been rotated.
- Scan the repository for accidentally committed secrets.

Cloud permissions

- Review the updated IAM policy to confirm that permissions are limited to required resources and actions.
- Test that the application can still perform its intended operations.
- Confirm that unauthorised access attempts are denied.
- Review cloud audit logs for relevant access events.

Evidence to retain

- Before-and-after configuration files with sensitive values removed.
- The updated IAM policy.
- Test results showing allowed and denied operations.
- Screenshots or logs demonstrating successful verification.
- The relevant GitHub commit documenting the remediation.

These checks should be completed before the fixes are reported as verified.

6. Conclusion

The MedVitals AI assessment identified two important areas requiring improvement: credential management and cloud access control.

The central issue is not simply that credentials exist or that the application has cloud permissions. It is whether credentials are protected and whether access is limited to what the application genuinely needs.

By removing hardcoded secrets, applying least-privilege permissions, and testing the resulting configuration, the project can reduce the risk of unauthorised access and improve the protection of sensitive healthcare resources.

Final Recommendation: Implement both security fixes, verify them through repeatable tests, and preserve the evidence in the project's GitHub repository.
