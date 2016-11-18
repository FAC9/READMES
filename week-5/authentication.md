# Authentication

##-What is authentication and why do we need it when building web applications?


## What are authentication schemes and strategies?

## SSL/TLS Mutual Authentication
This requires a secure channel to be established through digital certificates, before credentials will be shared.

### What is a digital certificate and how are they used?
A digital certificate is an electronic document that proves ownership of a public key. It contains details about the key, the owner and the Certificate Authority (CA) who vouches for its contents.

Every web client has a default collection of hundreds of certificates from major root authorities, and this collection is then included in browsers.
  - Each certificate in the collection is signed by a single authority
  - The signer's own certificate is in turn signed by another authority, each one becoming more widely accepted
  - Finally the root authority's certificate is self-signed and widely distributed


HTTP Basic authentication
Cookies
Tokens
Signatures
One-time passwords
OAuth2
SAML

## What are some of the different ways Hapi implements authentication?

## Build a small project which demonstrates authentication using Hapi.
