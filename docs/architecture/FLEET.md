# Fleet Map Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

A `<scope>-fleet` repository contains `fleet.yml`: the map of pinned reusable definitions and host capabilities needed to reconstruct the fleet. It is neither an instance ledger nor a deploy tool.

## Complete top-level schema

| Field | Required contents |
| :--- | :--- |
| `base` | This OS's repository and immutable revision/tag, plus the selected base realization reference when one is constructed |
| `catalogue` | Repository and immutable tag for the reusable catalogue actually consumed; explicitly absent when none is used |
| `classes` | Entries with `name`, `repo`, immutable `tag`, and `governedBy` (governor slug, or `self` for standalone) |
| `machines` | Entries with `name`, `kinds`, optional `registry` and nonsecret `reach` description |

`kinds` is a list drawn from `proxmox`, `lxd`, `liblxc`, `nested`, at most one family per shape. The first three make LXC universes; `nested` makes a rootful Podman universe. A machine can offer LXD and nested together. Its maker selects the qualified recipe matching the class's shape.

If a registry is used, its address must be reachable from **inside** the consuming universe, not merely relative to the host. The agent records the actual parameter and never invents one. First construction needs no catalogue or registry; create and pin the generated realization before TEST/PROD promotion. Recommend registry-backed reuse afterward.

## Map laws

1. Definitions and immutable references belong here, never instance rows, secrets or data. Instance state lives in the governor's private MariaDB; `r2://<instance-id>` is derivable, not a list in this map.
2. DEV bypasses fleet registration. TEST and PROD promotion require their class to be registered in their own scope's map. The constructor implements and verifies this guard; the code-free OS supplies no executable guard.
3. The map's reference is the default for new instances and the recovery floor. The ledger's actual `matrix` and `digest` are the truth for each instance and may differ during a canary. An audit reconciles them; a source tag is not an image digest.
4. A sovereign fork keeps its own mirrored map and pinned definitions. Registration in that scope suffices; recovery does not depend on another owner's private repository. Apply the naming mirror rule.
5. Recovery follows dependency order: retrieve pinned definitions, reconstruct or pull their locked artifacts, restore a governor before the classes it governs, then restore instance volumes from their declared backup location. The governor's own recovery references break circular dependence on the running fleet/registry. Git contains definitions, never the data backup.

See [Rules 1, 16, 25 and 37](../../RULES.md), [governor](../contracts/governor.md) and [maker](../contracts/maker.md).
