# Validation

### What is validation and why is it important (absolutely critical)?

Validation is where you check user inputs match the type or format and length that you expect (and therefore can work with). For example, checking that a telephone number is a specific length and is composed only of digits.

### What is Joi and how would you use it with Hapi?

#### How does validation work in Hapi?

1 - Input validation

Input validation can be set by rules in the `config` object on a route (`server.route`).

|Input parameter    | Parameter passed in the `config` object |
|-------------------|-----------------------------------------|
|path parameters    |`validate.params`                        |
|query parameters   |`validate.query` (*note:* if you specify validation rules for one query parameter you **must** then validate all query parameters)                       |
|headers    |`validate.headers`                        |
|body data    |`validate.payload` (*note:* if you specify validation rules for one query parameter you **must** then validate all query parameters)                      |

2 - Output validation

Input validation can be set by rules in the `response` property of the `config` object on a route (`server.route`). If the response does not pass the specified validation, a 500 (Internal Server Error) response will be sent to the client.

#### What is Joi?

Joi is a validation library built by the same team as Hapi, and it can be used in conjunction with Hapi or separately. You would use it with Hapi by requiring it (it's a module).

### Create a small project demonstrating some example situations where you'd use Joi.

Set up some validation schemas for these examples. The hapi.js validation tutorial may be of use to you.
