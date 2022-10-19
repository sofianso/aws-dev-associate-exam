# API Gateway Notes

API Gateway forms the app-facing part of the AWS serverless infrastructure.

## Integration Types

- AWS (non-proxy type only)
- AWS_PROXY
  - In Lambda proxy integration, when a client submits an API request, API Gateway passes to the integrated Lambda function the raw request as-is, except that the order of the request parameters is not preserved.
- HTTP
- Mock

## Mapping Tempalates

API Gateway lets you use mapping templates to transform the payload from JSON to XML or vice versa.

## Stages & Deployments

- Stages have their own ARN.
- You can configure caching, throttling, Stage Variables and Canary deployment.

## Open API 3 & Swagger

Main function of both Open API 3 & Swagger is to export API.

## Caching

- Caching is used to reduce the number of calls to the backend and improve latency requests to the API.
- You can set TTL, 300 seconds by default. (min 0, max 3600)
- Caches are defined per stage.
- You can encrypt caches.
- **Clients can invalidate the cache with the header: Cache-Control: max-age=0.**

## Throttling

There are two types of throttling:

- Server-side: The limit exists to prevent your API-and your account-from being overwhelmed by too many requests.
- Per-client: The limits are applied to to clients with API keys.

## Usage Plans & API Keys

A usage plan specifies who can access one or more deployed API stages and methods — and also how much and how fast they can access them. You can use a usage plan to configure throttling and quota limits, which are enforced on individual client API keys. The plan uses API keys to identify API clients and meters access to the associated API stages for each key. Think of paying a premium service and how you're getting a different content if you are a paid subscriber.

## How To Control Access To An API

- Resource-based policies.
- IAM Roles and Policies.
- IAM Tags.
- Endpoint policies for interface VPC endpoints.
- **Lambda authorizer** is an API Gateway feature that uses a Lambda function to control access to your API. A Lambda authorizer is useful if you want to implement a custom authorization scheme that uses a bearer token authentication strategy such as OAuth or SAML, or that uses request parameters to determine the caller's identity. When a client makes a request to one of your API's methods, API Gateway calls your Lambda authorizer, which takes the caller's identity as input and returns an IAM policy as output.
  - Token-based.
  - Request parameter-based.
- For WebSocketAPIs, only request parameter-based authorizers are supported.
- Amazon Cognito user pools.

## Monitoring, Logging & Auditing

- Latency measures the overall responsiveness of the API.
- IntegrationLatency measures the responsiveness of the backend (Lambda, API URL).
- CacheHitCount and CacheMissCount monitor the optimization of the cache.
