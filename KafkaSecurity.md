# Kafka Security

# Points

Secure Communication Using SSL
- Keys and Certificates
- Key and Trust Stores
- security.protocol Client Property
- Demo: Secure Communication Using SSL
Secure Inter-Broker Communication
- security.inter.broker.protocol Broker Property
- listeners Broker Property
- Demo: Secure Inter-Broker Communication
SSL Authentication
- ssl.client.auth Broker Property
- Demo: SSL Authentication
ACL Authorization
- authorizer.class.name Broker Property
- Other Broker Properties
- kafka-acls Utility
- Demo: ACL Authorization

# SECURE COMMUNICATION USING SSL
- Secure Sockets Layer (SSL) - a cryptographic protocol for communications security over a computer network
- Used for secure communication (data encryption) and authentication
- Deprecated by Transport Layer Security (TLS)
- Often referred to as SSL/TLS
- Transport Layer Security in Wikipedia (https://en.wikipedia.org/wiki/Transport_Layer_Security)

# KEYS AND CERTIFICATES
- Private And Public Keys
  - Identity of an entity (such as a computer or a website)
- Public Key Certificate (Digital Identity Certificate)
  - Identity of the owner (the subject)
  - Digital signature of an entity that has verified the certificate's contents (the issuer)
  - The certificate issuer is a Certificate Authority (CA)
- Certificate Signing Request (CSR)
  - Request to Certificate Authority to sign a certificate

# Keys and trust stores

- Key Store (or Keystore) is a database of keys and certificates
  - By default the Java keystore is implemented as a file
  - Contains the private key and any certificates to complete a chain of trust of the primary certificate
  - Initially only with the private key
  - Eventually the certificate and any root certificates after a CSR (Certificate Signing Request)
Trust Store is a file with trusted certificates (public keys)
Each certificate is associated with a unique alias
Java keytool to manage keys and certificates