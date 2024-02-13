# Secure Storage of Customer Credentials

At Census, we prioritize the security and confidentiality of our customers' sensitive information, including their credentials. We implement multiple layers of encryption within our Aurora database infrastructure to ensure robust protection against unauthorized access or malicious activities.

#### Encryption Methodology

1. **Aurora Database Symmetric Encryption**:
   * Census utilizes Aurora's symmetric encryption feature to encrypt data at rest within the database, ensuring that customer credentials are securely stored.
   * Symmetric encryption uses a single encryption key for both encryption and decryption operations, providing efficient data protection.
2. **AWS Key Management Service (KMS)**:
   * Encryption keys used for Aurora database encryption are securely managed by AWS Key Management Service (KMS), adding an additional layer of security.
   * Census leverages KMS to generate and manage encryption keys, ensuring strong cryptographic protection for customer credentials.
3. **Application-Level Encryption Keys**:
   * Census implements a second layer of encryption using application-level keys to further enhance data security.
   * These application-level keys serve as an additional barrier to unauthorized access, ensuring that even if the database encryption key is compromised, the data remains protected.

#### Security Measures

1. **Access Control**:
   * Access to the Aurora database containing customer credentials is tightly controlled using AWS IAM policies.
   * Census enforces strict access controls to both the database encryption keys and the application-level encryption keys, minimizing the risk of unauthorized access.
2. **Data Integrity**:
   * Aurora's symmetric encryption and the additional layer of application-level encryption ensure data integrity, mitigating the risk of data tampering or corruption.
   * These encryption layers work together to provide comprehensive protection for customer credentials stored within the database.
3. **Compliance and Auditing**:
   * Census leverages AWS compliance certifications and auditing tools to ensure adherence to industry standards and regulations.
   * AWS CloudTrail provides audit logs that enable Census to monitor database access and track security-related events or changes, ensuring compliance and accountability.

For more details, go to [getcensus.com/security](http://getcensus.com/security) where you can read about Census' security architecture and request additional information from our data room.
