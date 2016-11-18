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

### SSL
1-way (simple) authentication:
The server provides the client with its certificate. The client then verifies it against its own collection, to decide whether the server is trustworthy
The server's certificate is deemed trustworthy by looking at whether:
- the server's certificate is in the client's collection
- the server's certificate has been signed by a CA whose own certificate is in the client's collection - this is the 'chain of trust'
Authentication is successful after 9 of these "handshakes"

2-way (mutual) authentication:
Both parties supply each other with their certificate collections i.e. 1-way auth + the server also receives the client's collection of certificates.
The same process as above is performed by both parties and authentication is successful after 12 handshake messages.

Problems - the following are not scalable:
- 2-way auth only works if all users have a personal digital certificate that is signed by a root CA
- requires the server to import each client's certificate into its trusted certificate store



## What are some of the different ways Hapi implements authentication?

## Build a small project which demonstrates authentication using Hapi.
