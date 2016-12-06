# What is a JWT?

## Abstract definition
> A JSON Web Token (JWT) is a JSON object that is defined in RFC 7519 as a safe way to represent a set of
> information between two parties. The token is composed of a header, a payload, and a signature.

## JWT format
```
header.payload.signature
```
## How and why JWTs are used
![jwt explained](./images/jwt.png)

## JWTs

- JWTs are used across several programming languages .NET, Python, Node.js, Java, PHP, Ruby, Go, JavaScript, and Haskell.

- JWTs are self-contained: self-contained means that the payload contains all the necessary infomation about the user, avoiding to query the database more than once.

- JWTs can be passed around easily: JWTs are small, they can be sent through URL, POST parameter, or inside an HTTP header.

## When should you use JSON Web Tokens?

- Authentication: the most common use of JWTs. After logging in, each subsequent request will include the JWT, allowing the user to access the routes and services that are allowed with that token.

- Information Exchange: JWTs can be used to securely transmit information between parties, since they can be signed e.g.: using public/private key pairs. The signature is calculated using both the header and the payload, so you can check that the content hasn't been tampered with.


### Resources
1. [medium on jwt](https://medium.com/vandium-software/5-easy-steps-to-understanding-json-web-tokens-jwt-1164c0adfcec#.fl1xahvou)
2. [scotch.io](https://scotch.io/tutorials/the-anatomy-of-a-json-web-token)
3. [jwtt.io](https://jwt.io/)
4. [encoding vs encryption](https://danielmiessler.com/study/encoding-encryption-hashing-obfuscation/#encoding)




# How do you create a JWT?
# How do you decode a JWT?
# How do you use the module `hapi-auth-jwt2`?
