# Triage Labels

The skills speak in terms of canonical triage roles and execution hints. This file maps those roles to the actual label strings used in this repo's issue tracker.

| Canonical Role / Skill Label | Label in our tracker | Meaning                                                                   |
| ---------------------------- | -------------------- | ------------------------------------------------------------------------- |
| `needs-triage`               | `needs-triage`       | Maintainer needs to evaluate this issue                                   |
| `needs-info`                 | `needs-info`         | Waiting on reporter for more information                                  |
| `needs-audit`                | `needs-audit`        | Drafted specification waiting on `/spec-audit`                            |
| `ready-for-agent`            | `ready-for-agent`    | Fully specified, passed audit, ready for an agent                         |
| `ready-for-human`            | `ready-for-human`    | Requires human implementation                                             |
| `wontfix`                    | `wontfix`            | Will not be actioned                                                      |
| `complexity:high`            | `complexity:high`    | High architectural uncertainty; triggers parallel `/arena` in `/implement` |
| `arena`                      | `arena`              | Alias for `complexity:high`                                               |

When a skill mentions a role (e.g. "apply the AFK-ready triage label"), use the corresponding label string from this table.

Edit the "Label in our tracker" column to match whatever vocabulary you actually use.
