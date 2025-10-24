When to use ConfigMaps vs Secrets

ConfigMaps

Use for non-sensitive configuration data: feature flags, environment settings, config files, URLs, timeouts, etc.

Values are stored in plaintext in etcd (unless you encrypt etcd).

Can be mounted as files or injected as environment variables.

Good for application-level configuration and toggles.

Secrets

Use for sensitive data: DB credentials, API keys, TLS certs, tokens.

Stored as base64 in the Kubernetes API; base64 is not encryption — consider enabling encryption at rest for etcd (EncryptionConfiguration) and RBAC for secret access.

Use Secret objects and valueFrom.secretKeyRef or secret-volume mounts to inject values.

Avoid exposing secrets in logs, command-line arguments, or ConfigMaps.

Best practices

Never store secrets in ConfigMaps. Treat ConfigMaps as public-ish in your cluster context.

Enable encryption at rest for etcd if storing secrets in cluster (recommended for production).

Use RBAC to restrict which service accounts and users can read Secrets and ConfigMaps.

Use separate namespaces and limit access where appropriate.

For complex templates / overlays, consider using tools like Helm, Kustomize, or SOPS (for managing secrets).

When mounting as files, set the mountPath to a non-writable directory and run containers with least privilege.

Rotate secrets regularly and avoid long-lived static credentials where possible.

Avoid printing secret values in kubectl describe or logs; kubectl describe secret will not show plaintext values by default.
