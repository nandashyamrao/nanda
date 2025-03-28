# Assumptions for Dynatrace–Oracle Exadata Integration Project

This document lists the key assumptions considered during the planning and execution of the Dynatrace integration with Oracle Exadata using ActiveGate.

## Assumptions

1. An on-prem Linux or Windows VM will be provisioned for Dynatrace ActiveGate, with outbound internet access to `*.dynatrace.com` and `*.live.dynatrace.com`.
2. The Oracle Exadata database exposes required performance metrics either via JMX (port 7879) or via SQL queries.
3. The necessary firewall rules will be opened between ActiveGate and Oracle Exadata (TCP port 7879) in time for testing.
4. Oracle DB team will provide read-only credentials or allow access for metrics collection.
5. The network team will support validating connectivity between ActiveGate and the Oracle Exadata host.
6. Dynatrace SaaS and the assigned ActiveGate are already set up and licensed to support extensions.
7. Project timelines are based on receiving all required access and approvals on schedule.
8. No sensitive data (PII, credentials) will be pushed to Dynatrace SaaS; only performance metrics.
9. The test Oracle DB instance used for the POC is representative of production performance behavior.
10. Any JMX-based polling won't impact database performance due to lightweight, read-only access.
