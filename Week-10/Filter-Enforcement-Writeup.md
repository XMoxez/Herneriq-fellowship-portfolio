# Filter Enforcement WriteUp
## Application-Layer Filter Bypass: Why Database-Layer Enforcement Matters

### What the Application-Layer Filter Does and Why It Looks Like the Right Fix

An application-layer filter checks incoming requests before they reach the database. It validates user input, checks permissions, and blocks unauthorized actions. For example, an application may prevent a user from modifying a transaction record that belongs to another customer.

This approach looks like the right fix because it stops suspicious requests early, provides immediate feedback, and reduces the risk of unauthorized data access or modification. However, its protection depends on every request passing through the filter.

### The Specific Scenario in Which the Filter Fails

The filter fails when an attacker discovers an alternative path to the database or exploits a weakness in how the application processes requests. For example, a vulnerable API endpoint might allow a user to modify a transaction belonging to another customer because it does not perform the necessary ownership check.

Even if another endpoint correctly blocks the same action, the unprotected endpoint may still allow it. The application appears secure, but its protection is inconsistent.

### How the Bypass Works

An attacker identifies a request that is not adequately validated or authorized and uses it to access or modify data they should not control. The request bypasses the intended security check because the application does not enforce the required rule on every execution path.

The root cause is that security depends on application logic rather than an independently enforced database restriction.

### What the Database-Layer Fix Does Differently

The database-layer fix enforces access restrictions where the data is stored. Instead of relying solely on the application to decide which records a user may access, the database applies its own security rules.

For example, database permissions, row-level security (RLS), and properly scoped database roles can restrict users to authorized records. Even if an application endpoint contains a coding error, the database rejects operations that violate its enforced policies.

The bypass no longer works provided that the database policy is correctly configured, applies to the relevant operation, and cannot be bypassed through an over privileged database role or privileged execution path.

### An Original Analogy

Imagine a security officer checking identification at the entrance to an office building. The officer represents the application-layer filter. If someone discovers an unguarded side entrance, they can bypass the officer.

Now imagine that every sensitive office also has an electronic access lock that accepts only authorized staff credentials. This represents database-layer enforcement. Even if someone enters the building through the side entrance, they cannot access a restricted office without the required authorization.

The lesson is simple: controlling entry into a system is important, but enforcing access at the point where sensitive data is stored provides an additional, independent layer of protection.

### Conclusion

Application-layer filters are essential, but they should not be the only security control protecting sensitive data. Database-layer enforcement adds defense in depth by making unauthorized access or modification harder even when application logic fails. Effective security requires both layers to work together.
