# probable-adventure
A simple serverless aws lambda + api gateway

[serverless site](https://www.serverless.com/ "serverless site")

just as a demonstration of creating a lambda + api gateway in the minimal configuration

## Lambda code

```javascript
'use strict';

module.exports.hello = function (event, context, callback) {
  console.log(event); // Contains incoming request data (e.g., query params, headers and more)

  const response = {
    statusCode: 200,
    headers: {
      'x-custom-header': 'My Header Value',
    },
    body: JSON.stringify({ message: 'Hello World!' }),
  };

  callback(null, response);
};
```
## Serverless config

```yaml
service: simple-lambda

frameworkVersion: '2 || 3'

provider:
  name: aws
  region: us-west-2
  runtime: nodejs12.x
  endpointType: REGIONAL
  lambdaHashingVersion: 20201221

functions:
  hello:
    handler: handler.hello
    events:
      - http:
          path: hello
          method: get
          cors: true
```
