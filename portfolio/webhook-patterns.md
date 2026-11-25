# Reliable webhook processing

A generic integration should verify the provider's signature against the raw request body before accepting an event. Apply timestamp or replay checks when the provider supports them.

1. Authenticate the request and validate its schema.
2. Persist a unique provider event identifier and enqueue work durably.
3. Return success only after durable acceptance.
4. Process asynchronously using idempotent handlers and bounded retries.
5. Route permanent failures to a dead-letter queue and alert operators.

For outgoing calls, set timeouts, use exponential backoff with jitter for transient failures, and distinguish non-retryable errors. Use provider-supported idempotency keys for external side effects.

Test invalid signatures, duplicate delivery, out-of-order events, timeout recovery and worker restarts. Avoid recording sensitive payloads in logs.

This note describes an independent example pattern, not a production integration.
