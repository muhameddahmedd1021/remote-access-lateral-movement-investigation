# Query guide

Each search uses the recorded case window. Case times and filters keep the stages separate.

| Question | Searches |
|---|---|
| R-Q01: remote logon context | [RDP logons](../cases/R02/queries/R02-logons.spl), [WinRM logons](../cases/R05/queries/R05-network-logons.spl), [source connections](../cases/R05/queries/R05-source-connection.spl) |
| R-Q02: session lifecycle | [RDP sessions](../cases/R02/queries/R02-sessions.spl), [RDP authentication](../cases/R02/queries/R02-rdp-auth.spl) |
| R-Q03: share authorization | [Network logons](../cases/R03/queries/R03-logons.spl), [share summary](../cases/R03/queries/R03-share-access.spl) |
| R-Q04: verified transfer | [Target file event](../cases/R04/queries/R04-file-events.spl), [share checks](../cases/R04/queries/R04-share-write.spl) |
| R-Q05: remote execution | [Target processes](../cases/R05/queries/R05-target-processes.spl), [command text](../cases/R05/queries/R05-command-text.spl) |
| R-Q06: privilege context | [Privilege events](../cases/R06/queries/R06-privilege-events.spl), [account memberships](../cases/R06/results/account-context.csv) |
| R-Q07: phase comparison | [Selected evidence anchors](../cases/R07/queries/R07-evidence-anchors.spl), [controls](../cases/R07/results/comparison-controls.csv) |

`table` selects useful fields; `sort` places observations in time order; `stats count by` summarizes repeated audit records. The selected-anchor query is a case lookup. The alert query independently selects child processes of wsmprovhost rather than treating every network logon as remote execution.

## R10: from transfer to execution

| Question | Search |
|---|---|
| Did the script arrive? | [Arrival](../cases/R10/queries/R10-script-arrival.spl) |
| Did WinRM launch PowerShell with a file? | [Execution](../cases/R10/queries/R10-script-execution.spl) |
| What did the script do? | [Script content](../cases/R10/queries/R10-script-content.spl) |
| Which source process connected? | [Source connection](../cases/R10/queries/R10-source-connection.spl) |
| Which process created the output? | [File timeline](../cases/R10/queries/R10-file-timeline.spl) |
| Which account obtained the target ticket? | [Domain ticket](../cases/R10/queries/R10-domain-ticket.spl) |

The [scheduled alert](../cases/R10/queries/R10-remote-script-alert.spl) uses a moving five-minute window. Investigation searches use the fixed UTC case window. `dedup Computer Channel EventRecordID` keeps each native record once. Process GUIDs and parent IDs are checked in original XML alongside the small Search UI tables.
