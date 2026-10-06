# Frozen Maker Recipe Contract

> **Intent Classification**: GENERIC INTENT (Universal / Parameterized Blueprint)

The constructor authors a recipe for the selected host family and work kind in the realization and proves it on the real target before promotion. The name is `<hostKind>-<workKind>.sh` when using the shell realization. Equivalent implementations retain this exact typed invocation/result contract; this OS contains no executable recipe.

## Inputs

Pass six separate positional arguments, in order: **rowId, class, matrix, digest, account, env**. Never concatenate form/ledger data into a command string. The row's optional typed params travel only as `SHAPER_PARAM_<KEY>` in the fresh environment built by the maker: required PATH, HOME and locale, the operator's declared `SHAPER_*` configuration, and allowed row keys. Reject invalid keys/types rather than silently removing them. Do not inherit arbitrary `LD_PRELOAD`, `BASH_ENV` or other process state.

A recipe is frozen and idempotent. It verifies the actual artifact digest and target identity. Each family declares its required host capabilities and is qualified using actual inner Podman containers/builds. Installed binary names are insufficient.

## Stamp

Verify the matrix exists and its bytes match the declared digest. Absence is exit **2**; unverified bytes exit **3**, both reported `STAMP_FAILED`. A replay of the same row cannot create a second instance. A successful stamp ends with one structured line of observed child facts, including a running `state`; output without those facts is not a birth, regardless of exit status. A declared `checks: true` causes the governor to derive validation work.

The parent public SSH key is installed as a file; its private key remains above. Build the unit application with its declared identity, private MariaDB and persistent volumes. The recipe never copies host/parent private keys into the child.

## Reap

For permitted disposable environments, end the target and independently verify its absence before success. An already-absent target is a successful idempotent result. Reaping an `env=prod` row is refused with exit **4**, reported as `REAP_REFUSED`, not a generic failure to retry. Production termination requires its explicit human/root path.

An instance's death does not delete the source matrix. The governor's references determine artifact retention; never infer all uses are gone from one instance's exit.

## Validate

Read the child's declared acceptance specification, conventionally `/etc/shaper/checks.json`, and run a verifier whose input is that bounded declarative vocabulary. Reject operations outside it. Wait a bounded interval for actual service readiness before judging; a silent child is a failed check with an explicit reason, not a healthy or invented verdict. Preserve the failing step and evidence such as screenshots where the check uses a browser.

| Exit | Meaning |
| :--- | :--- |
| 0 | `VALIDATED`; every applicable step passed |
| 1 | `VALIDATION_FAILED`, including child silent past its boot budget |
| 2 | Target facts changed: instance absent, no address or missing spec |
| Other nonzero | Harness/verification failure, explicitly distinguished in evidence |

Any nonzero validation result degrades rather than reporting success. A browser is used for graphical acceptance, not as a requirement for a headless task that needs none.

## Adopt

Use the class-declared unique `instance` param through `SHAPER_PARAM_INSTANCE`, with matrix/digest literally `none`. Observe and bind the existing container without creating, launching, modifying or executing inside it. End with observed running state and `legacy: true`; absent facts produce `ADOPT_FAILED`.

The same instance name must reach **reap and validate**, not only adopt. Qualify all three together before enabling adoption on that family. Never report `checks: true` when validation would derive a different target name. Adoption is not proof the adopted application satisfies a new realization's full contract.

## Required qualification

Exercise real birth, replay, absent/corrupt matrix refusal, typed hostile-looking data preserved as data, validation success and real defect, verified destruction, already-absent replay, production reap refusal, and adoption without mutation when supported. Test doubles may check argument construction, but target-host evidence is required for recipe capability. Retain exact conditions and effects without converting measured durations into an SLA.

[Governor](governor.md) owns state transitions and retry bounds; [maker](maker.md) owns identity and execution; [Rules 11, 20, 27 and 36](../../RULES.md) own containment, proof, bounded recovery and authority.
