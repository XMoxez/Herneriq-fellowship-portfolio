# AI Application Security Assessment Report

Project: HerNetIq AI Application Security Assessment
Application: CartBot AI - Level 3 AI Defense Lab 
Security Domain: Application and API Security
Assessment Type: Vulnerability Identification, Remediation, and Verification

1. Vulnerability Findings

The assessment focused on identifying weaknesses in CartBot AI's application and API security controls.

The key vulnerability areas assessed included:

- Broken Object-Level Authorization (BOLA): An authenticated user might access another user's resources if the server fails to verify ownership or authorization.
- Insufficient API Input Validation: Improper validation of user-supplied data could allow unexpected or malicious inputs to reach application logic.
- Inadequate Authentication and Authorization: Weak enforcement of access controls could expose sensitive application functions or resources.
- Sensitive Information Exposure: Improper error handling or API responses could reveal internal implementation details or confidential information.

Primary finding: Broken Object-Level Authorization is a critical concern if the server relies on a user-supplied object ID without independently verifying the authenticated user's permission to access that object.

Note: These are assessment targets and example findings. Confirm which vulnerabilities were actually reproduced in CartBot AI before reporting them as verified findings.

Authenticated customer
        |
        v
Changes customer_id
        |
        v
API accepts client value
        |
        v
No object-ownership verification
        |
        v
Another customer's orders exposed

2. Business/Security Impact

If these vulnerabilities are present and exploitable, they could affect the confidentiality, integrity, and availability of the application.

Potential business impacts include:

- Data exposure: Unauthorized users could access other customers' records or sensitive information.
- Data manipulation: Weak authorization could allow unauthorized modification of customer resources.
- Financial and operational losses: Security incidents could result in investigation costs, service disruption, and potential financial losses.
- Reputational damage: Customers may lose confidence in the platform if their information is not adequately protected.
- Compliance risks: Exposure of personal information could create legal or regulatory obligations, depending on the data and applicable requirements.

For an AI-powered application, compromised application or API controls could also expose information used by AI features or allow unauthorized users to invoke protected functionality.

3. Remediation Recommendations

The following security controls are recommended:

1. Enforce server-side authorization: Verify that every authenticated user is authorized to access the specific resource requested.
2. Apply least privilege: Grant users, services, and API credentials only the permissions required for their functions.
3. Validate all inputs: Apply appropriate schema validation, type checks, length limits, and business-rule validation.
4. Secure API endpoints: Enforce authentication and authorization consistently across all protected endpoints.
5. Protect sensitive information: Avoid returning secrets, internal stack traces, or unnecessary customer data in API responses.
6. Implement security logging: Record relevant authorization failures and suspicious API activity without logging passwords, tokens, or other secrets.
7. Add regression tests: Test unauthorized access attempts and confirm that security controls remain effective after future code changes.

4. Evidence of the Remediation

Remediation should be supported by reproducible tests and a clear record of the changes made.

Recommended evidence includes:

- A screenshot or code excerpt showing the original vulnerability.
- A code diff demonstrating the security fix.
- A test showing that an authorized user can access their own resource.
- A negative test showing that a different authenticated user cannot access that resource.
- An API response demonstrating that unauthorized access is rejected.
- Test results confirming that legitimate requests continue to work.

Verification scenario:

Test| Expected Result
User A requests User A's resource| Access permitted
User B requests User A's resource| Access denied
Unauthenticated user requests a protected resource| Authentication required
Request contains an invalid object ID| Request rejected safely

Verification status: To be completed using actual test results from the application.

A successful remediation should demonstrate that authorization is enforced by the server, rather than relying on the frontend to hide or restrict resources.

5. Vulnerable Configuration

The following Python example illustrates an insecure API pattern. It is a demonstration, not a confirmed extract from CartBot AI.

@app.get("/orders/{order_id}")
def get_order(order_id: int):
    order = db.get_order(order_id)

    if not order:
        raise HTTPException(
            status_code=404,
            detail="Order not found"
        )

    return order

Security weakness:

The endpoint retrieves an order using the supplied "order_id" without demonstrating an authorization check that verifies whether the authenticated user owns the order or has permission to access it.

If no equivalent authorization control exists elsewhere, an authenticated attacker could change the order ID and potentially access another customer's order.

Risk level: High, if unauthorized cross-customer access is reproducible and the exposed data is sensitive.

6. Hardened Configuration

The following example demonstrates a safer approach using an authenticated user and a database query restricted to that user's authorized records.

from fastapi import Depends, HTTPException

@app.get("/orders/{order_id}")
def get_order(
    order_id: int,
    current_user=Depends(get_current_user)
):
    order = db.get_order_for_user(
        order_id=order_id,
        user_id=current_user.id
    )

    if not order:
        raise HTTPException(
            status_code=404,
            detail="Order not found"
        )

    return order

Security improvements:

- The endpoint obtains the authenticated user's identity from a server-controlled authentication mechanism.
- The database lookup restricts the requested order to the authenticated user's authorized records.
- Requests for other users' orders do not return those orders.
- Returning a generic "404" response can reduce resource-existence disclosure, although it does not replace authorization enforcement.

Important implementation note: The example assumes "get_current_user()" securely authenticates the request and "get_order_for_user()" enforces the ownership restriction in the database query. Both functions must be implemented and tested correctly.

7. GitHub Commit

The remediation should be committed to the project's GitHub repository so the security improvement is traceable and reviewable.

Suggested commit message:

Fix CartBot AI API authorization vulnerabilities

Suggested Git commands:

git status
git diff
git add .
git commit -m "Fix CartBot AI API authorization vulnerabilities"
git push origin main

Before committing, review the staged changes and ensure that secrets, access tokens, and sensitive test data are not included.

Evidence to record:

- Repository name and link.
- Commit hash.
- Files changed.
- Security tests executed and their results.
- Before-and-after code comparison.

Actual GitHub commit: Insert the commit hash and repository link after the changes have been committed and pushed. Do not report a commit as completed until it exists in the repository.

Conclusion

The AI Application Security Assessment demonstrates the importance of securing application logic and API endpoints beyond basic authentication. Effective remediation requires server-side authorization, input validation, least-privilege access, secure error handling, and repeatable security testing.

By documenting the original weakness, implementing the appropriate fix, validating the results, and recording the changes in GitHub, the assessment creates a traceable security improvement that can be reviewed by developers, security engineers, and technical stakeholders.
