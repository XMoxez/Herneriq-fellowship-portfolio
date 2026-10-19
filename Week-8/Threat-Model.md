Application accepting customer/object identifier is not automatically vulnerability but is weather the server verifies that the authenticated customer is authorized to access that object.
An application that accepts a customer or object identifier is not automatically vulnerable. The critical security question is whether the server verifies that the authenticated user is authorized to access the requested object.

For example, a customer may be authenticated and legitimately access their own account information. However, if they change the customer ID in an API request and the server returns another customer's information without verifying ownership or access permissions, the application has a Broken Object-Level Authorization (BOLA) vulnerability.

The security principle is simple: Authentication establishes who the user is, while authorization determines what that user is permitted to access.

Therefore, authorization checks must be enforced on the server for every relevant object request. Client-side filters and application-layer validation alone are insufficient if the backend does not independently enforce access controls.
