# Operator direction — monthly SQL partitions in private unit databases

Direction: **[MANDATE]** operator clarification of 13 October 2026.
The operator confirmed that "partitioned tables" means monthly SQL partitions
for histories and call records, not technical/business table separation, and
asked that the rule be written into SHAPER OS if absent.

## Canonical placement

[Rule 4](../docs/rules/02-CONSTRUCTION.md#rule-4) owns the construction rule:
time-series histories and call-detail records in each functional unit's private
MariaDB use UTC calendar-month SQL partitions. Mutable current records and
pending work may remain ordinary tables. The unit explicitly declares archive
and future boundaries, indexes and its administrative calendar-maintenance path.
The application has no schema or partition DDL privileges.

[Rule 26](../docs/rules/05-REPAIR-AND-DATA.md#rule-26) owns the bounded inventory
and persistence/recovery observations. Retention is a separate data-contract
choice; month rollover grants no deletion authority.

This supplements the [10 October unit-database method](2026-10-10-UNIT-DATABASE-TURBINOBASH-METHOD.md)
and [September profile](../docs/profiles/SEPTEMBER-CONTAINER-MARIADB.md).
It adds no shared database, no implementation code and no automatic production
migration. A deployed instance's adopted revision and actual partition state
remain its own evidence. This direction certifies no built artifact.
