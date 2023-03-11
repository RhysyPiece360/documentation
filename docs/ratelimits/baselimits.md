:::tip Ratelimits

excessive hits of ratelimiting can cause your service to be temp banned for upto 2 hours, please contact our support team incase that happens

:::

# Ratelimits for Route `/get_answer`

The `/get_answer` route has a ratelimit of 55 requests per minute. This means that a maximum of 55 requests can be made to this route in a period of one minute. If a client exceeds this limit, they will receive an HTTP 429 Too Many Requests response.

## How to handle ratelimits

When a client receives a 429 response, they should wait for a certain amount of time before making another request. The amount of time to wait can be found in the `Retry-After` header of the response. The client should wait for the specified number of seconds before making another request.

## How to detect if a request has been ratelimited

When a request is successfully processed and the client has not exceeded the ratelimit, the response will include a JSON object with the answer and a `ratelimited` key set to `False`. For example:
```
{
"answer": "example",
"ratelimited": False
}
```
If the client has exceeded the ratelimit and the request has been ratelimited, the response will include a JSON object with the `ratelimited` key set to `True`. For example:
```
{
"message": "Too many requests, please try again later.",
"ratelimited": True
}
```


## Notes on implementation

To enforce the ratelimit, the server will need to maintain a record of the number of requests made by each client in a given time period. This can be done using a database or a simple in-memory data structure.

When a client makes a request to the `/get_answer` route, the server should check if the client has exceeded the ratelimit. If the client has not exceeded the ratelimit, the server should process the request and update the record of requests for the client. If the client has exceeded the ratelimit, the server should return a 429 response with the appropriate headers and a JSON object indicating that the request has been ratelimited.
