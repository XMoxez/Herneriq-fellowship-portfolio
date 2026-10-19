
PayGuard AI — RAG Security Assessment

1. Poisoning Vectors: Retrieval-Time and Training-Time Risks

Security Objective: Identify how malicious information could influence PayGuard's AI-generated responses about payments, invoices, and transaction disputes.

Retrieval-Time Poisoning: An attacker could introduce misleading or malicious content into documents that PayGuard retrieves to answer user questions. For example, a manipulated invoice or payment-dispute document could instruct the AI to recommend sending money to an unauthorized account or provide false payment information.

Training-Time Poisoning: If PayGuard's embedding model or other AI components are trained or fine-tuned using compromised datasets, an attacker could influence how the system interprets information or responds to certain queries.

User Experience: Customers might receive incorrect payment instructions, misleading dispute guidance, or inaccurate answers that appear trustworthy because they come from PayGuard.

Blue Indicator of Compromise (IoC): A potential blue-team indicator is an unexpected change in retrieved documents or AI responses, such as a legitimate payment question repeatedly returning suspicious content, unauthorized payment details, or instructions unrelated to the original query. This should trigger investigation rather than be treated as conclusive proof of an attack.

2. Embedding Model Audit: Five Behavioral Trust Checks

An embedding model converts text into numerical representations so PayGuard can retrieve documents with similar meanings. If the model behaves unexpectedly, malicious or irrelevant information may be retrieved.

The following five behavioral checks should be applied before approving the model for production:

Trust Check| Assessment Question| Security Significance
1. Consistency| Does the model produce reasonably consistent results for equivalent queries?| Detects unexpected or unstable retrieval behaviour.
2. Semantic Integrity| Does it distinguish legitimate payment instructions from unrelated or misleading content?| Reduces the risk of retrieving deceptive documents.
3. Adversarial Robustness| Can small, deliberate text changes cause malicious documents to outrank legitimate sources?| Identifies susceptibility to manipulation.
4. Data Leakage| Can the model or its outputs expose sensitive information through unauthorized access or inference?| Protects customer and financial information.
5. Model Provenance and Integrity| Can PayGuard verify the model's source, version, integrity, and update history?| Reduces the risk of using tampered or counterfeit models.

Approval Decision: NOT APPROVED until verification is complete.

The embedding model should not be approved for production solely because it performs well on ordinary queries. PayGuard must obtain evidence that it passes all five checks, document the results, and investigate any unexplained behaviour. Approval should follow successful testing and documented risk acceptance.

Note: This is a provisional security decision. Actual approval requires test results for the specific embedding model selected by PayGuard.

3. Filter Enforcement Gap: Application-Layer Failure

Security Finding: PayGuard's application-layer filtering may fail if it checks user input but does not adequately inspect retrieved documents and the content supplied to the AI model.

For example, an attacker could submit a seemingly harmless question that causes PayGuard to retrieve a document containing malicious instructions. If the application passes that document directly to the AI without appropriate validation, isolation, and policy enforcement, the AI may follow the malicious instructions or produce an unsafe response.

What Does an Attacker Need to Exploit This Gap?

Depending on the system's design, an attacker may need:

- Access to a feature that accepts questions or searches documents.
- A way to introduce or influence content in the document collection, such as through an invoice upload or a compromised data source.
- A weakness in the application's validation of retrieved content or enforcement of AI security rules.

The attacker does not necessarily need administrative access. However, exploitation depends on the actual permissions, document-ingestion process, retrieval controls, and application design.

Potential Impact: Misleading payment advice, manipulated dispute responses, exposure of sensitive information, and loss of customer trust.

Key Lesson: Filtering a user's question alone is insufficient. PayGuard must also control what information enters the AI's context and what actions the system is permitted to perform.

4. Recommendations: Three Actionable Security Improvements

Recommendation 1: Verify Information Before the AI Uses It

Business action: Require PayGuard to accept payment instructions and dispute evidence only from approved, traceable sources.

- Maintain an approved list of document sources.
- Check uploaded documents before adding them to the knowledge base.
- Require independent verification of payment-account changes.
- Prevent instructions found inside retrieved documents from overriding PayGuard's security rules.

Business benefit: Reduces the likelihood of customers receiving fraudulent payment instructions or misleading financial advice.

Recommendation 2: Test and Approve Every AI Model Before Deployment

Business action: Establish a formal security approval process for embedding models and other AI components.

- Verify the model's source and integrity.
- Run the five behavioral trust checks described above.
- Test the model against malicious documents and manipulated queries.
- Record the results and repeat the checks whenever the model is changed or updated.

Business benefit: Reduces the risk of deploying an untrusted model that could undermine PayGuard's information retrieval and customer protection.

Recommendation 3: Enforce Security Controls Beyond the Application Interface

Business action: Ensure security checks operate throughout PayGuard's AI workflow, not only when a customer submits a question.

- Validate documents before retrieval and treat retrieved content as untrusted input.
- Restrict the AI's access to customer records, payment systems, and transaction-changing functions.
- Require explicit authorization and independent verification before any financial action.
- Log suspicious retrievals, unusual AI responses, and blocked requests for investigation.

Business benefit: Limits the potential damage if malicious content bypasses an initial filter or influences an AI response.

Conclusion

The PayGuard assessment highlights three connected risks: poisoned information entering the retrieval pipeline, insufficient verification of the embedding model, and application-layer filters that may not adequately protect the AI's retrieved context.

The recommended approach is to verify information sources, test AI components before deployment, and enforce security controls throughout the system.

Final Security Position: PayGuard should not rely on AI-generated answers alone for financial decisions. Trusted data sources, independently verified payment instructions, restricted permissions, and continuous monitoring are essential to protecting customers and maintaining confidence in the platform.
