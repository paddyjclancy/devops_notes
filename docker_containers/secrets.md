# Secrets
These are sensitive data, anything that may be a security threat if possible.

**Docker context:** A string of <= 500KB, requiring swarm-mode in order to leverage security protocols. It acts as a service.

Only provided to those nodes that _need_ the secret in order to execute its tasks.

Secrets are never stored, but transferred via memory without encryption from the /run/secrets

Secrets cannot be deleted when in use in a node elsewhere.
