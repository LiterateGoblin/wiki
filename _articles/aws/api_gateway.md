---
title: AWS API Gateway
---
API Gateway is a service offered by Amazon Web Services (AWS) that facilitates the creation, publishing, maintenance, and monitoring of [APIs](/api.html). In particular, API Gateway can be used to create and manage REST APIs and WebSocket APIs. Each API supports different API types and can integrate with several kinds of backend to generate the response. An API Gateway can be integrated with AWS IAM, AWS Lambda, or Amazon Cognito to manage authentication and authorization. API keys linked to the API can be distributed to customers in order to throttle and limit their rates. API Gateway exports AWS CloudWatch metrics and logs for monitoring.

## Concepts

The primary resource that API Gateway creates and manages is called an API Gateway API.

### Backends

In order to handle communication from a client, each route of the API Gateway API must be integrated with a *backend*. An API Gateway API will forward a client's request to the backend, receive a response from the backend, then forward the backend's response back to the client. Optionally, the API Gateway API can perform transformations on the incoming request and the backend's response. Each route can have a different backend.

Valid backends include:

- AWS Lambda
- any existing HTTP endpoint
- AWS Simple Queue Service (SQS)
- a hardcoded response configured directly in the API Gateway API (called a "mock" integration)
- an AWS Network Load Balancer inside of an AWS Virtual Private Cloud (VPC)

### Stages

When an API Gateway API is deployed, it is deployed to a stage. A stage represents a snapshot of an API, and is an independent version of the API.

Stages are meant to be conceptualized as different environments. Each stage can have variables associated with it, called *stage variables*, that are independent of the other stages within the same API.

A stage can be designated as a *canary*, where a smaller portion of the traffic for another stage is routed instead to this one. Once this stage has been verified to be functioning as intended, the canary stage can be promoted; 100% of the traffic can be routed to the canary stage, and it will replace the old stage.

### Invoke URL

Once an API Gateway API has been deployed to a stage, an invoke URL is generated for it that a client can use to send a request to it. It follows this pattern:

```
https://<api_id>.execute-api.<region>.amazon.com/<stage>/<resource>
```

where `<api_id>` is the ID of the API Gateway API, `<region>` is the AWS region, `<stage>` is the name of the stage, and `<resource>` is the name of a resource (if the resource is omitted the base route `/` is assumed).

## API Types

### WebSocket APIs

A WebSocket API is one where the client and server can send messages to each other at any time; this is described as two-way communication. For this reason, WebSocket APIs are best suited for real-time applications, such as text messaging. One-way communication is also possible, where a client sends messages and receives no response from the server.

When a client connects or disconnects to the API, a message can be sent to a backend. Responses can be configured for when a client sends a message to a route that has not been created, called **$default**.

API Gateway APIs can use WebSocket selection expressions to determine whether to process a request at all, which route should handle a request, or which stage should handle a request.

 API Gateway manages persistence and state of the WebSocket connection.

### REST APIs

REST APIs use a request-response model to facilitate communication. A server will only send a response once a client establishes a connection and makes a request; once the response has been received, the connection is terminated. This is described as synchronous communication.

REST APIs come in three kinds of endpoints:

- regional endpoint - an endpoint designed for lower latency when accessed by a resource in the same region as the endpoint.
- edge-optimized endpoint - an endpoint designed for low latency no matter where the client is geographically
- private endpoint - an endpoint designed for applications with strict security requirements. Only compute within the same VPC as this endpoint can send requests to it

Each endpoint can be transformed in-place to each other kind of endpoint with one exception: a private endpoint cannot be directly transformed into an edge-optimized endpoint.

If a REST API has caching enabled, each endpoint response can be cached to reduce the number of calls to the backend.

## Authentication and Authorization

There are three main ways to authenticate and authorize an incoming request using the features of API Gateway:

- Use AWS Identity and Access Management (IAM). All requests sent to an API Gateway API secured using AWS IAM must be signed using the AWS version 4 signing process (Sig v4).
- Use an authorizer Lambda. This approach is often used when authorization is done using OAuth. The authorizer Lambda can be either receive the token as input, or the token along with additional request details.
- Use Amazon Cognito. Cognito user pools (a resource created as part of the Amazon Cognito service) are intended for use cases where a mobile or web application has users that can sign-in to authenticate.

## References

- <https://explore.skillbuilder.aws/learn/course/52/play>
