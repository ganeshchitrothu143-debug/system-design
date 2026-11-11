# Primary references

[Curriculum index](README.md)

These resources support deeper reading and implementation-specific verification. The worked scenarios are original teaching examples; a source link is not a claim that every design is prescribed by that source. Check the version of the technology you actually use.

| Area | Primary reference | Related notes |
| --- | --- | --- |
| HTTP semantics | [RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html) | 001–010 |
| HTTP problem details | [RFC 9457](https://www.rfc-editor.org/rfc/rfc9457.html) | 004 |
| Database isolation | [PostgreSQL transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html) | 014–016 |
| Consensus | [Raft paper](https://raft.github.io/raft.pdf) | 054,057 |
| Reliability objectives | [Google SRE: Service Level Objectives](https://sre.google/sre-book/service-level-objectives/) | 061–063 |
| Retries and deadlines | [AWS Builders Library: Timeouts, retries, and backoff with jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/) | 042–043 |
| Authorization | [OWASP Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) | 071–073 |
| Server-side request forgery | [OWASP SSRF Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html) | 077,095 |

Pay special attention to vendor-specific isolation, replication acknowledgments, queue delivery, and key-management behavior. A generic diagram cannot establish a product's guarantees.
