# Vault Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

The Vault encrypts, persists and supplies credentials without requiring a cloud vault.

* Use AES-256-GCM at rest; accept the declared master key or its SHA-256-normalized key material. Keep key handling separate from encrypted payloads and backups.
* Provide equivalent in-process and HTTP access where the realization needs those modes. Keep the reusable encryption core free of unnecessary dependencies; language and database client choices belong to the realization.
* Know no consuming universe or client. A mailbox schema is a reusable credential contract, not embedded business policy. Generic metadata names no infrastructure owner.
* Initialize an explicit empty durable state even when no credential has yet been added. The Vault functional unit persists its own encrypted records in its own private MariaDB. Any local key/export or credential file is owner-only (`0600`) and repaired to that mode on write.
* Reject example-template master keys or tokens such as `<...>` or `changeme` before creating protected state. Missing usable key material blocks Vault initialization, not unrelated construction.
* Inject only authorized consumers' credentials and never expose them in logs, public documents or backups alongside their opening key.

Apply [Rules 4, 12 and 26](../../RULES.md) and the [unit profile](../profiles/SEPTEMBER-CONTAINER-MARIADB.md). Prove encryption, restart durability, authorized retrieval, rejection and recovery using the real unit.
