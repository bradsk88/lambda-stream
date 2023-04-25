# Lambda-Stream

This library adds types and local support for AWS Lambda Response Streaming. Locally, it'll buffer and return the entire response.

In AWS Lambda, it'll simply use the global `awslambda.streamifyResponse`.

This library exposes a `ResponseStream` class, the `streamifyResponse` method, and `isInAWS` method.



Works like this:

```javascript
import { APIGatewayProxyEvent } from "aws-lambda";
import { streamifyResponse, ResponseStream } from 'lambda-stream'

export const handler = streamifyResponse(myHandler)

async function myHandler (event: APIGatewayProxyEvent, responseStream: ResponseStream): Promise<void> {
        console.log('Handler got event:', event)
        responseStream.setContentType("text/plain");
        responseStream.write("Hello, world!");
        responseStream.end();
}
```

Or in commonjs:

```javascript
'use strict';
const { streamifyResponse } = require('lambda-stream')

module.exports.hello = streamifyResponse(
    async (event, responseStream, context) => {
        responseStream.setContentType("text/plain");
        responseStream.write("Hello, world!");
        responseStream.end();
    }
);
```
