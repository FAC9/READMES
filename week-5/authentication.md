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


## HTTP Basic authentication
Sending an encoded username and password on every HTTP request that needs authentication. This is achieved through a dedicated HTTP header.  
But! This method would mean that the user would have to enter their login credentials every single time an HTTP request is sent. The client (i.e. browser) therefore needs to store, or cache, the credentials for a period of time.

Drawbacks:
- fundamentally insecure
- no standard way to log out
- login is not customisable
- requires broswer to cache credentials securely - must be paired with SSL/TLS (see problems above)

## Digest Access Authentication
Digest addresses the insecurities of basic authentication. Instead of sending the full credentials to the server, they are sent via an [MD5 hash](https://en.wikipedia.org/wiki/MD5).

Whilst better than basic auth, and supported by most browsers, DAA's reliance on MD5 means that it is still susceptible to interception attacks.

## Cookies/Tokens
Once the user is logged in, an authentication token (cookie) is created. When this token is encrypted and sent to the server, the server can decrypt the token and extract the authenticated user information. This makes automatic login possible.

All hosts must have a shared key and have their clocks synchronized. It is considered good practice to only pass the cookie via a secure channel and to prevent access to it client-side (via HttpOnly flag) to prevent scripting hacks.

## OAuth2
OAuth 2 allows a provider app to grant a consumer application access to a specific resource - OAuth is technically an authorisation tool, rather than an authentication tool.

The consumer app has to register with the provider app. This is a manual, one-time process that typically involves providing basic information such as application name, website, a logo, etc. To prevent against certain types of attack, a redirect URI needs to be used.

- Consumer makes an (OAuth2) resource request to the provider
- Provider application informs the user of the request and prompts them to authenticate
- An authentication scheme is used
- Control reverts back to the consumer (via the redirect URI), now with an access token, giving access to the provider's resource
- This access token is provided in the HTTP header for later requests

With OAuth2, the user’s credentials are never exposed to the consumer application. The consumer is only given a temporary token which can be revoked by the user or provider application at any time without any need for the credentials to change. OAuth2 _require_ the use of SSL/TLS.


## What are some of the different ways Hapi implements authentication?

## Build a small project which demonstrates authentication using Hapi.
