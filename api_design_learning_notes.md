# API Design

## Http method

GET:
* `Idempotent`

POST:
* `Not Idempotent by definition`: Stripe has implementation for this. [Ref](https://stripe.com/blog/idempotency)

PUT:
* `Idempotent`
* Method only allows a complete replacement of a document.

PATCH:
* Modify an existing HTTP resource.

DELETE: <br>
* `Idempotent`: there is a caveat on DELETE. The problem with DELETE, which if successful would normally return a 200 (OK) or 204 (No Content), will often return a 404 (Not Found) on subsequent call <br>
respones: 204 no content

## Authentication


## Http headers

- `Accept`: Informs the server about the types of data that can be sent back.
  Ex:<br/>
  `Accept: 'application/vnd.api+json'` is for json api<br/>
  `Accept: 'application/json'` is for regular json<br/>

## Idempotency

Making multiple identical requests has the same effect as making a single request
The API supports idempotency for safely retrying requests without accidentally performing the same operation twice.

* Idempotency key: Provide an additional `Idempotency-Key: <key>` header to the request so the request knows it.

## Rate Limiter [Read](https://stripe.com/blog/rate-limiters)

### When do you need rate limiter?
- One of your users is responsible for a `spike in traffic`, and you need to `stay up for everyone else`.
- One of your users has a `misbehaving script which is accidentally sending you a lot of requests`. Or, even worse, one of your users is intentionally trying to overwhelm your servers.
- A user is sending you `a lot of lower-priority requests`, and you want to make sure that it doesn’t affect your high-priority traffic.
- Something in your system has gone wrong internally, and as a result you can’t serve all of your regular traffic and need to drop low-priority requests.

### Load shedding
  - You can use our API 1000 times a second
  - Drop low-priority requests to make sure that more critical requests get through

### Request rate limiter
- Restricts each user to N requests per second.
- After analyzing our traffic patterns, we added the ability to briefly burst above the cap for sudden spikes in usage during real-time events (e.g. a flash sale.)

### Concurrent Rate Limiter
  - You can only have 20 API requests in progress at the same time
  - Resource-intensive endpoints make users wait for the response longer so they retry. These retries add more demand to the already overloaded resource, slowing things down even more. The concurrent rate limiter helps address this nicely.

  - Concurrent request limiters manage resource contention for CPU-intensive API endpoints.

### Fleet usage load shedder
- Using this type of load shedder ensures that a certain percentage of your fleet will always be available for your most important API requests.
- 2 types: critical API methods (e.g. creating charges) and non-critical methods (e.g. listing charges.)

### Worker utilization load shedder (For damage control)

- Most API services use a set of workers to independently respond to incoming requests in a parallel fashion. This load shedder is the final line of defense. If your workers start getting backed up with requests, then this will shed lower-priority traffic.

- 4 type for traffics:
  - Critical methods
  - POSTs
  - GETs
  - Test mode traffic

- If a box is too busy to handle its request volume, it will slowly start shedding less-critical requests, starting with test mode traffic. If shedding test mode traffic gets it back into a good state, great! We can start to slowly bring traffic back. Otherwise, it’ll escalate and start shedding even more traffic.

### Implementation
- Algorithm: [Token Bucket](https://en.wikipedia.org/wiki/Token_bucket)

1. In Practice: Hook the rate limiters into your middleware stack safely.
2. Show clear exceptions to your users
3. Build in safeguards so that you can turn off the limiters
4. Dark launch each rate limiter to watch the traffic they would block