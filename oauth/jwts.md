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
```
const jwt = require('json-web-token');
var secret = process.env.JWT_SECRET;

    jwt.decode(secret, token, function (err, decodedJWT) {
      if (err) {
        return console.log(err, 'There was an error decoding');
      } else {
        console.log(decodedJWT);
      }
    });

    <!-- token is the JWT you are trying to decode -->
```

[Check out this cool resource](http://calebb.net/)  to see what a decoded JWT looks like before and after.

To see the full example this code snippet came from, [look here.](https://www.npmjs.com/package/json-web-token)

# How do you use the module `hapi-auth-jwt2`?
`hapi-auth-jwt2` is the authentication scheme for Hapi.js apps using JWTs.

For a full walk-through [see DWYL's excellent README](https://github.com/dwyl/hapi-auth-jwt2).

```
var people = { // our "users database"
    1: {
      id: 1,
      name: 'Jen Spencer'
    }
};

// Our own validation function
var validate = function (decoded, request, callback) {

    // do your checks to see if the person is valid
    if (!people[decoded.id]) {
      return callback(null, false);
    }
    else {
      return callback(null, true);
    }
};

var server = new Hapi.Server();
server.connection({ port: 8000 });
  // ** INCLUDE MODULE HERE ↓↓ **
server.register(require('hapi-auth-jwt2'), (err) => {
  if(err){ console.log(err);
  }

  server.auth.strategy('jwt', 'jwt',
    { key: process.env.JWT_SECRET,         
      validateFunc: validate,            // validate function defined above
      verifyOptions: { algorithms: [ 'HS256' ] } // pick a strong algorithm
    });

    server.auth.default('jwt');

    server.route([
      {
        method: "GET",
        path: "/",
        config: { auth: false },
        handler: function(request, reply) {
          reply({text: 'Token not required'});
        }
      },
      {
        method: 'GET',
        path: '/restricted',
        config:{ auth: 'jwt' },
        handler: function(request, reply){
          reply({text: 'You used a Token!'})
          .header("Authorization", request.headers.authorization);
        }
      }
    ]);
});

server.start(function () {
  console.log('Server running at:', server.info.uri);
});
```
