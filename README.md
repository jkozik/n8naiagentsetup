# N8N-based AI Agent leveraging ollama on Mac Mini M4
## Basic Ollama setup to run on Mac Mini M4 (not in docker)
I setup my new Mac Mini M4 and installed [Ollama](https://ollama.com/) on it following the instructions in  [Raid Owl](https://www.youtube.com/@RaidOwl)'s video. That is, I installed Ollama native on MacOS so that I can take advantage of [Apple Silicon](https://en.wikipedia.org/wiki/Apple_silicon). I followed [Raid Owl](https://www.youtube.com/@RaidOwl)'s setup and exposed Ollama through the Open Webui portal.  I found a [video](https://www.youtube.com/watch?v=3qGLMlsB8Us) by [BlueSpork](https://www.youtube.com/@BlueSpork) that helps -- it is a relatively straight forward docker container. 

I have a reverse proxy, and I expose this OpenWebUI portal as a subdomain on one of my domain names.  Pretty neat.
![image](https://github.com/user-attachments/assets/def82ba9-5e46-48f5-b697-556d84c4e1dd)

## N8N AI Startup Kit
Leveraging my Ollama on Mac Mini M4 setup, I decided to give AI Agent development a try.  On the [N8N github account](https://github.com/n8n-io), there's the [self-hosted-ai-starter-kit](https://github.com/n8n-io/self-hosted-ai-starter-kit) is an excellent tutorial that I follow in this section.

### Install n8n using Docker Compose
Following the README, I cloned the repository, built and ran the `docker-compose.yml`
```
(base) jackkozik@Jacks-Mac-mini projects % git clone https://github.com/n8n-io/self-hosted-ai-starter-kit.git
Cloning into 'self-hosted-ai-starter-kit'...
remote: Enumerating objects: 139, done.
remote: Total 139 (delta 0), reused 0 (delta 0), pack-reused 139 (from 1)
Receiving objects: 100% (139/139), 3.91 MiB | 10.68 MiB/s, done.
Resolving deltas: 100% (65/65), done.
(base) jackkozik@Jacks-Mac-mini projects % cd self-hosted-ai-starter-kit
(base) jackkozik@Jacks-Mac-mini self-hosted-ai-starter-kit % ls
LICENSE                 README.md               assets                  docker-compose.yml      n8n
(base) jackkozik@Jacks-Mac-mini self-hosted-ai-starter-kit % vi docker-compose.yml <--- edit environment  variable OLLAMA_HOSTn8n
(base) jackkozik@Jacks-Mac-mini self-hosted-ai-starter-kit % docker compose up
[+] Running 0/4
 ⠋ n8n-import Pulling                                                                                                                                                     0.1s
 ⠋ qdrant Pulling                                                                                                                                                         0.1s
 ⠋ n8n Pulling                                                                                                                                                            0.1s
 ⠋ postgres Pulling                                                                                                                                                       0.1s
error getting credentials - err: exit status 1, out: `error getting credentials - err: exit status 1, out: `keychain cannot be accessed because the current session does not allow user interaction. The keychain may be locked; unlock it by running "security -v unlock-keychain ~/Library/Keychains/login.keychain-db" and try again``
(base) jackkozik@Jacks-Mac-mini self-hosted-ai-starter-kit % security -v unlock-keychain ~/Library/Keychains/login.keychain-db
unlock-keychain "/Users/jackkozik/Library/Keychains/login.keychain-db"
password to unlock /Users/jackkozik/Library/Keychains/login.keychain-db:
(base) jackkozik@Jacks-Mac-mini self-hosted-ai-starter-kit % docker compose up
[+] Running 22/22
 ✔ n8n Pulled                                                                                                                                                             1.1s
 ✔ qdrant Pulled                                                                                                                                                         12.6s
   ✔ 4f4fb700ef54 Pull complete                                                                                                                                           0.0s
   ✔ 44113adf5a0e Pull complete                                                                                                                                           0.1s
   ✔ b16f1b166780 Pull complete                                                                                                                                           5.0s
   ✔ a6e17ca61522 Pull complete                                                                                                                                           4.4s
   ✔ 003dba7d7b22 Pull complete                                                                                                                                           5.2s
   ✔ dc84f73ed3cf Pull complete                                                                                                                                           1.3s
   ✔ 13573604b890 Pull complete                                                                                                                                          10.0s
   ✔ a60c2e005c05 Pull complete                                                                                                                                           0.4s
 ✔ n8n-import Pulled                                                                                                                                                      1.1s
 ✔ postgres Pulled                                                                                                                                                       11.4s
   ✔ c5a4a70d6ab6 Pull complete                                                                                                                                           0.4s
   ✔ b77aad30e136 Pull complete                                                                                                                                           8.8s
   ✔ 10cef688189b Pull complete                                                                                                                                           0.4s
   ✔ df10ca38afc9 Pull complete                                                                                                                                           0.4s
   ✔ f902a55e1f5c Pull complete                                                                                                                                           0.9s
   ✔ ba7187ed4892 Pull complete                                                                                                                                           0.4s
   ✔ 92fd87599cc9 Pull complete                                                                                                                                           0.4s
   ✔ 80d2520a24d9 Pull complete                                                                                                                                           0.4s
   ✔ 6320dbbd0635 Pull complete                                                                                                                                           0.4s
   ✔ 02bbd938cacb Pull complete                                                                                                                                           0.4s
[+] Running 8/8
 ✔ Network self-hosted-ai-starter-kit_demo               Created                                                                                                          0.0s
 ✔ Volume "self-hosted-ai-starter-kit_postgres_storage"  Created                                                                                                          0.0s
 ✔ Volume "self-hosted-ai-starter-kit_qdrant_storage"    Created                                                                                                          0.0s
 ✔ Volume "self-hosted-ai-starter-kit_n8n_storage"       Created                                                                                                          0.0s
 ✔ Container qdrant                                      Created                                                                                                          0.1s
 ✔ Container self-hosted-ai-starter-kit-postgres-1       Created                                                                                                          0.1s
 ✔ Container n8n-import                                  Created                                                                                                          0.1s
 ✔ Container n8n                                         Created                                                                                                          0.1s
Attaching to n8n, n8n-import, qdrant, postgres-1
qdrant      |            _                 _
qdrant      |   __ _  __| |_ __ __ _ _ __ | |_
qdrant      |  / _` |/ _` | '__/ _` | '_ \| __|
qdrant      | | (_| | (_| | | | (_| | | | | |_
qdrant      |  \__, |\__,_|_|  \__,_|_| |_|\__|
qdrant      |     |_|
qdrant      |
qdrant      | Version: 1.14.1, build: 530430fa
qdrant      | Access web UI at http://localhost:6333/dashboard
qdrant      |
qdrant      | 2025-05-25T18:17:52.090250Z  INFO storage::content_manager::consensus::persistent: Initializing new raft state at ./storage/raft_state.json
qdrant      | 2025-05-25T18:17:52.097009Z  INFO qdrant: Distributed mode disabled
qdrant      | 2025-05-25T18:17:52.097067Z  INFO qdrant: Telemetry reporting enabled, id: 1da5cba2-30eb-4516-aedf-88372c3d8609
qdrant      | 2025-05-25T18:17:52.097107Z  INFO qdrant: Inference service is not configured.
postgres-1  | The files belonging to this database system will be owned by user "postgres".
postgres-1  | This user must also own the server process.
postgres-1  |
postgres-1  | The database cluster will be initialized with locale "en_US.utf8".
postgres-1  | The default database encoding has accordingly been set to "UTF8".
postgres-1  | The default text search configuration will be set to "english".
postgres-1  |
postgres-1  | Data page checksums are disabled.
postgres-1  |
postgres-1  | fixing permissions on existing directory /var/lib/postgresql/data ... ok
postgres-1  | creating subdirectories ... ok
postgres-1  | selecting dynamic shared memory implementation ... posix
postgres-1  | selecting default max_connections ... 100
postgres-1  | selecting default shared_buffers ... 128MB
qdrant      | 2025-05-25T18:17:52.135343Z  INFO qdrant::actix: TLS disabled for REST API
qdrant      | 2025-05-25T18:17:52.135410Z  INFO qdrant::actix: Qdrant HTTP listening on 6333
qdrant      | 2025-05-25T18:17:52.135425Z  INFO actix_server::builder: starting 11 workers
qdrant      | 2025-05-25T18:17:52.135427Z  INFO actix_server::server: Actix runtime found; starting in Actix runtime
postgres-1  | selecting default time zone ... UTC
qdrant      | 2025-05-25T18:17:52.135435Z  INFO actix_server::server: starting service: "actix-web-service-0.0.0.0:6333", workers: 11, listening on: 0.0.0.0:6333
postgres-1  | creating configuration files ... ok
qdrant      | 2025-05-25T18:17:52.139661Z  INFO qdrant::tonic: Qdrant gRPC listening on 6334
qdrant      | 2025-05-25T18:17:52.139673Z  INFO qdrant::tonic: TLS disabled for gRPC API
postgres-1  | running bootstrap script ... ok
postgres-1  | sh: locale: not found
postgres-1  | 2025-05-25 18:17:52.245 UTC [35] WARNING:  no usable system locales were found
postgres-1  | performing post-bootstrap initialization ... ok
postgres-1  | syncing data to disk ... ok
postgres-1  |
postgres-1  |
postgres-1  | Success. You can now start the database server using:
postgres-1  |
postgres-1  |     pg_ctl -D /var/lib/postgresql/data -l logfile start
postgres-1  |
postgres-1  | initdb: warning: enabling "trust" authentication for local connections
postgres-1  | initdb: hint: You can change this by editing pg_hba.conf or using the option -A, or --auth-local and --auth-host, the next time you run initdb.
postgres-1  | waiting for server to start....2025-05-25 18:17:52.420 UTC [41] LOG:  starting PostgreSQL 16.9 on aarch64-unknown-linux-musl, compiled by gcc (Alpine 14.2.0) 14.2.0, 64-bit
postgres-1  | 2025-05-25 18:17:52.421 UTC [41] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres-1  | 2025-05-25 18:17:52.422 UTC [44] LOG:  database system was shut down at 2025-05-25 18:17:52 UTC
postgres-1  | 2025-05-25 18:17:52.424 UTC [41] LOG:  database system is ready to accept connections
postgres-1  |  done
postgres-1  | server started
postgres-1  | CREATE DATABASE
postgres-1  |
postgres-1  |
postgres-1  | /usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*
postgres-1  |
postgres-1  | waiting for server to shut down....2025-05-25 18:17:52.551 UTC [41] LOG:  received fast shutdown request
postgres-1  | 2025-05-25 18:17:52.552 UTC [41] LOG:  aborting any active transactions
postgres-1  | 2025-05-25 18:17:52.553 UTC [41] LOG:  background worker "logical replication launcher" (PID 47) exited with exit code 1
postgres-1  | 2025-05-25 18:17:52.553 UTC [42] LOG:  shutting down
postgres-1  | 2025-05-25 18:17:52.553 UTC [42] LOG:  checkpoint starting: shutdown immediate
postgres-1  | 2025-05-25 18:17:52.574 UTC [42] LOG:  checkpoint complete: wrote 924 buffers (5.6%); 0 WAL file(s) added, 0 removed, 0 recycled; write=0.009 s, sync=0.012 s, total=0.022 s; sync files=301, longest=0.004 s, average=0.001 s; distance=4267 kB, estimate=4267 kB; lsn=0/191AB10, redo lsn=0/191AB10
postgres-1  | 2025-05-25 18:17:52.575 UTC [41] LOG:  database system is shut down
postgres-1  |  done
postgres-1  | server stopped
postgres-1  |
postgres-1  | PostgreSQL init process complete; ready for start up.
postgres-1  |
postgres-1  | 2025-05-25 18:17:52.672 UTC [1] LOG:  starting PostgreSQL 16.9 on aarch64-unknown-linux-musl, compiled by gcc (Alpine 14.2.0) 14.2.0, 64-bit
postgres-1  | 2025-05-25 18:17:52.672 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
postgres-1  | 2025-05-25 18:17:52.672 UTC [1] LOG:  listening on IPv6 address "::", port 5432
postgres-1  | 2025-05-25 18:17:52.673 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
postgres-1  | 2025-05-25 18:17:52.675 UTC [57] LOG:  database system was shut down at 2025-05-25 18:17:52 UTC
postgres-1  | 2025-05-25 18:17:52.677 UTC [1] LOG:  database system is ready to accept connections
n8n-import  | Permissions 0644 for n8n settings file /home/node/.n8n/config are too wide. This is ignored for now, but in the future n8n will attempt to change the permissions automatically. To automatically enforce correct permissions now set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true (recommended), or turn this check off set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=false.
n8n-import  | Migrations in progress, please do NOT stop the process.
n8n-import  | Starting migration InitialMigration1587669153312
n8n-import  | Finished migration InitialMigration1587669153312
n8n-import  | Starting migration WebhookModel1589476000887
n8n-import  | Finished migration WebhookModel1589476000887
n8n-import  | Starting migration CreateIndexStoppedAt1594828256133
n8n-import  | Finished migration CreateIndexStoppedAt1594828256133
n8n-import  | Starting migration MakeStoppedAtNullable1607431743768
n8n-import  | Finished migration MakeStoppedAtNullable1607431743768
n8n-import  | Starting migration AddWebhookId1611144599516
n8n-import  | Finished migration AddWebhookId1611144599516
n8n-import  | Starting migration CreateTagEntity1617270242566
n8n-import  | Finished migration CreateTagEntity1617270242566
n8n-import  | Starting migration UniqueWorkflowNames1620824779533
n8n-import  | Finished migration UniqueWorkflowNames1620824779533
n8n-import  | Starting migration AddwaitTill1626176912946
n8n-import  | Finished migration AddwaitTill1626176912946
n8n-import  | Starting migration UpdateWorkflowCredentials1630419189837
n8n-import  | Finished migration UpdateWorkflowCredentials1630419189837
n8n-import  | Starting migration AddExecutionEntityIndexes1644422880309
n8n-import  | Finished migration AddExecutionEntityIndexes1644422880309
n8n-import  | Starting migration IncreaseTypeVarcharLimit1646834195327
n8n-import  | Finished migration IncreaseTypeVarcharLimit1646834195327
n8n-import  | Starting migration CreateUserManagement1646992772331
n8n-import  | Finished migration CreateUserManagement1646992772331
n8n-import  | Starting migration LowerCaseUserEmail1648740597343
n8n-import  | Finished migration LowerCaseUserEmail1648740597343
n8n-import  | Starting migration CommunityNodes1652254514002
n8n-import  | Finished migration CommunityNodes1652254514002
n8n-import  | Starting migration AddUserSettings1652367743993
n8n-import  | Finished migration AddUserSettings1652367743993
n8n-import  | Starting migration AddAPIKeyColumn1652905585850
n8n-import  | Finished migration AddAPIKeyColumn1652905585850
n8n-import  | Starting migration IntroducePinData1654090467022
n8n-import  | Finished migration IntroducePinData1654090467022
n8n-import  | Starting migration AddNodeIds1658932090381
n8n-import  | Finished migration AddNodeIds1658932090381
n8n-import  | Starting migration AddJsonKeyPinData1659902242948
n8n-import  | Finished migration AddJsonKeyPinData1659902242948
n8n-import  | Starting migration CreateCredentialsUserRole1660062385367
n8n-import  | Finished migration CreateCredentialsUserRole1660062385367
n8n-import  | Starting migration CreateWorkflowsEditorRole1663755770893
n8n-import  | Finished migration CreateWorkflowsEditorRole1663755770893
n8n-import  | Starting migration WorkflowStatistics1664196174001
n8n-import  | Finished migration WorkflowStatistics1664196174001
n8n-import  | Starting migration CreateCredentialUsageTable1665484192212
n8n-import  | Finished migration CreateCredentialUsageTable1665484192212
n8n-import  | Starting migration RemoveCredentialUsageTable1665754637025
n8n-import  | Finished migration RemoveCredentialUsageTable1665754637025
n8n-import  | Starting migration AddWorkflowVersionIdColumn1669739707126
n8n-import  | Finished migration AddWorkflowVersionIdColumn1669739707126
n8n-import  | Starting migration AddTriggerCountColumn1669823906995
n8n-import  | Finished migration AddTriggerCountColumn1669823906995
n8n-import  | Starting migration MessageEventBusDestinations1671535397530
n8n-import  | Finished migration MessageEventBusDestinations1671535397530
n8n-import  | Starting migration RemoveWorkflowDataLoadedFlag1671726148421
n8n-import  | Finished migration RemoveWorkflowDataLoadedFlag1671726148421
n8n-import  | Starting migration DeleteExecutionsWithWorkflows1673268682475
n8n-import  | Finished migration DeleteExecutionsWithWorkflows1673268682475
n8n-import  | Starting migration AddStatusToExecutions1674138566000
n8n-import  | Finished migration AddStatusToExecutions1674138566000
n8n-import  | Starting migration CreateLdapEntities1674509946020
n8n-import  | Finished migration CreateLdapEntities1674509946020
n8n-import  | Starting migration PurgeInvalidWorkflowConnections1675940580449
n8n-import  | Finished migration PurgeInvalidWorkflowConnections1675940580449
n8n-import  | Starting migration MigrateExecutionStatus1676996103000
n8n-import  | Finished migration MigrateExecutionStatus1676996103000
n8n-import  | Starting migration UpdateRunningExecutionStatus1677236854063
n8n-import  | Finished migration UpdateRunningExecutionStatus1677236854063
n8n-import  | Starting migration CreateVariables1677501636754
n8n-import  | Finished migration CreateVariables1677501636754
n8n-import  | Starting migration CreateExecutionMetadataTable1679416281778
n8n-import  | Finished migration CreateExecutionMetadataTable1679416281778
n8n-import  | Starting migration AddUserActivatedProperty1681134145996
n8n-import  | Finished migration AddUserActivatedProperty1681134145996
n8n-import  | Starting migration RemoveSkipOwnerSetup1681134145997
n8n-import  | Finished migration RemoveSkipOwnerSetup1681134145997
n8n-import  | Starting migration MigrateIntegerKeysToString1690000000000
n8n-import  | Finished migration MigrateIntegerKeysToString1690000000000
n8n-import  | Starting migration SeparateExecutionData1690000000020
n8n-import  | Finished migration SeparateExecutionData1690000000020
n8n-import  | Starting migration RemoveResetPasswordColumns1690000000030
n8n-import  | Finished migration RemoveResetPasswordColumns1690000000030
n8n-import  | Starting migration AddMfaColumns1690000000030
n8n-import  | Finished migration AddMfaColumns1690000000030
n8n-import  | Starting migration AddMissingPrimaryKeyOnExecutionData1690787606731
n8n-import  | Finished migration AddMissingPrimaryKeyOnExecutionData1690787606731
n8n-import  | Starting migration CreateWorkflowNameIndex1691088862123
n8n-import  | Finished migration CreateWorkflowNameIndex1691088862123
n8n-import  | Starting migration CreateWorkflowHistoryTable1692967111175
n8n-import  | Finished migration CreateWorkflowHistoryTable1692967111175
n8n-import  | Starting migration ExecutionSoftDelete1693491613982
n8n-import  | Finished migration ExecutionSoftDelete1693491613982
n8n-import  | Starting migration DisallowOrphanExecutions1693554410387
n8n-import  | Finished migration DisallowOrphanExecutions1693554410387
n8n-import  | Starting migration MigrateToTimestampTz1694091729095
n8n-import  | Finished migration MigrateToTimestampTz1694091729095
n8n-import  | Starting migration AddWorkflowMetadata1695128658538
n8n-import  | Finished migration AddWorkflowMetadata1695128658538
n8n-import  | Starting migration ModifyWorkflowHistoryNodesAndConnections1695829275184
n8n-import  | Finished migration ModifyWorkflowHistoryNodesAndConnections1695829275184
n8n-import  | Starting migration AddGlobalAdminRole1700571993961
n8n-import  | Finished migration AddGlobalAdminRole1700571993961
n8n-import  | Starting migration DropRoleMapping1705429061930
n8n-import  | Finished migration DropRoleMapping1705429061930
n8n-import  | Starting migration RemoveFailedExecutionStatus1711018413374
n8n-import  | Finished migration RemoveFailedExecutionStatus1711018413374
n8n-import  | Starting migration MoveSshKeysToDatabase1711390882123
n8n-import  | [MoveSshKeysToDatabase1711390882123] No SSH keys in filesystem, skipping
n8n-import  | Finished migration MoveSshKeysToDatabase1711390882123
n8n-import  | Starting migration RemoveNodesAccess1712044305787
n8n-import  | Finished migration RemoveNodesAccess1712044305787
n8n-import  | Starting migration CreateProject1714133768519
n8n-import  | Finished migration CreateProject1714133768519
n8n-import  | Starting migration MakeExecutionStatusNonNullable1714133768521
n8n-import  | Finished migration MakeExecutionStatusNonNullable1714133768521
n8n-import  | Starting migration AddActivatedAtUserSetting1717498465931
n8n-import  | Finished migration AddActivatedAtUserSetting1717498465931
n8n-import  | Starting migration AddConstraintToExecutionMetadata1720101653148
n8n-import  | Finished migration AddConstraintToExecutionMetadata1720101653148
n8n-import  | Starting migration FixExecutionMetadataSequence1721377157740
n8n-import  | Finished migration FixExecutionMetadataSequence1721377157740
n8n-import  | Starting migration CreateInvalidAuthTokenTable1723627610222
n8n-import  | Finished migration CreateInvalidAuthTokenTable1723627610222
n8n-import  | Starting migration RefactorExecutionIndices1723796243146
n8n-import  | Finished migration RefactorExecutionIndices1723796243146
n8n-import  | Starting migration CreateAnnotationTables1724753530828
n8n-import  | Finished migration CreateAnnotationTables1724753530828
n8n-import  | Starting migration AddApiKeysTable1724951148974
n8n-import  | Finished migration AddApiKeysTable1724951148974
n8n-import  | Starting migration CreateProcessedDataTable1726606152711
n8n-import  | Finished migration CreateProcessedDataTable1726606152711
n8n-import  | Starting migration SeparateExecutionCreationFromStart1727427440136
n8n-import  | Finished migration SeparateExecutionCreationFromStart1727427440136
n8n-import  | Starting migration AddMissingPrimaryKeyOnAnnotationTagMapping1728659839644
n8n-import  | Finished migration AddMissingPrimaryKeyOnAnnotationTagMapping1728659839644
n8n-import  | Starting migration UpdateProcessedDataValueColumnToText1729607673464
n8n-import  | Finished migration UpdateProcessedDataValueColumnToText1729607673464
n8n-import  | Starting migration AddProjectIcons1729607673469
n8n-import  | Finished migration AddProjectIcons1729607673469
n8n-import  | Starting migration CreateTestDefinitionTable1730386903556
n8n-import  | Finished migration CreateTestDefinitionTable1730386903556
n8n-import  | Starting migration AddDescriptionToTestDefinition1731404028106
n8n-import  | Finished migration AddDescriptionToTestDefinition1731404028106
n8n-import  | Starting migration MigrateTestDefinitionKeyToString1731582748663
n8n-import  | Finished migration MigrateTestDefinitionKeyToString1731582748663
n8n-import  | Starting migration CreateTestMetricTable1732271325258
n8n-import  | Finished migration CreateTestMetricTable1732271325258
n8n-import  | Starting migration CreateTestRun1732549866705
n8n-import  | Finished migration CreateTestRun1732549866705
n8n-import  | Starting migration AddMockedNodesColumnToTestDefinition1733133775640
n8n-import  | Finished migration AddMockedNodesColumnToTestDefinition1733133775640
n8n-import  | Starting migration AddManagedColumnToCredentialsTable1734479635324
n8n-import  | Finished migration AddManagedColumnToCredentialsTable1734479635324
n8n-import  | Starting migration AddStatsColumnsToTestRun1736172058779
n8n-import  | Finished migration AddStatsColumnsToTestRun1736172058779
n8n-import  | Starting migration CreateTestCaseExecutionTable1736947513045
n8n-import  | Finished migration CreateTestCaseExecutionTable1736947513045
n8n-import  | Starting migration AddErrorColumnsToTestRuns1737715421462
n8n-import  | Finished migration AddErrorColumnsToTestRuns1737715421462
n8n-import  | Starting migration CreateFolderTable1738709609940
n8n-import  | Finished migration CreateFolderTable1738709609940
n8n-import  | Starting migration CreateAnalyticsTables1739549398681
n8n-import  | Finished migration CreateAnalyticsTables1739549398681
n8n-import  | Starting migration UpdateParentFolderIdColumn1740445074052
n8n-import  | Finished migration UpdateParentFolderIdColumn1740445074052
n8n-import  | Starting migration RenameAnalyticsToInsights1741167584277
n8n-import  | Finished migration RenameAnalyticsToInsights1741167584277
n8n-import  | Starting migration AddScopesColumnToApiKeys1742918400000
n8n-import  | Finished migration AddScopesColumnToApiKeys1742918400000
n8n-import  | Starting migration AddWorkflowStatisticsRootCount1745587087521
n8n-import  | Finished migration AddWorkflowStatisticsRootCount1745587087521
n8n-import  | Starting migration AddWorkflowArchivedColumn1745934666076
n8n-import  | Finished migration AddWorkflowArchivedColumn1745934666076
n8n-import  | Starting migration DropRoleTable1745934666077
n8n-import  | Finished migration DropRoleTable1745934666077
n8n-import  |
n8n-import  | There is a deprecation related to your environment variables. Please take the recommended actions to update your configuration:
n8n-import  |  - N8N_RUNNERS_ENABLED -> Running n8n without task runners is deprecated. Task runners will be turned on by default in a future version. Please set `N8N_RUNNERS_ENABLED=true` to enable task runners now and avoid potential issues in the future. Learn more: https://docs.n8n.io/hosting/configuration/task-runners/
n8n-import  |
n8n-import  | Successfully imported 2 credentials.
n8n-import  | Permissions 0644 for n8n settings file /home/node/.n8n/config are too wide. This is ignored for now, but in the future n8n will attempt to change the permissions automatically. To automatically enforce correct permissions now set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true (recommended), or turn this check off set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=false.
n8n-import  | User settings loaded from: /home/node/.n8n/config
n8n-import  |
n8n-import  | There is a deprecation related to your environment variables. Please take the recommended actions to update your configuration:
n8n-import  |  - N8N_RUNNERS_ENABLED -> Running n8n without task runners is deprecated. Task runners will be turned on by default in a future version. Please set `N8N_RUNNERS_ENABLED=true` to enable task runners now and avoid potential issues in the future. Learn more: https://docs.n8n.io/hosting/configuration/task-runners/
n8n-import  |
n8n-import  | Importing 1 workflows...
n8n-import  | Successfully imported 1 workflow.
n8n-import exited with code 0
n8n         | Permissions 0644 for n8n settings file /home/node/.n8n/config are too wide. This is ignored for now, but in the future n8n will attempt to change the permissions automatically. To automatically enforce correct permissions now set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true (recommended), or turn this check off set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=false.
n8n         | Initializing n8n process
n8n         | n8n ready on 0.0.0.0, port 5678
n8n         |
n8n         | There is a deprecation related to your environment variables. Please take the recommended actions to update your configuration:
n8n         |  - N8N_RUNNERS_ENABLED -> Running n8n without task runners is deprecated. Task runners will be turned on by default in a future version. Please set `N8N_RUNNERS_ENABLED=true` to enable task runners now and avoid potential issues in the future. Learn more: https://docs.n8n.io/hosting/configuration/task-runners/
n8n         |
n8n         | [license SDK] Skipping renewal on init because renewal is not due yet or cert is not initialized
n8n         | Version: 1.93.0
n8n         |
n8n         | Editor is now accessible via:
n8n         | http://localhost:5678
n8n         | Owner was set up successfully
postgres-1  | 2025-05-25 18:22:52.781 UTC [55] LOG:  checkpoint starting: time
n8n         | Failed to renew license: renewal failed because current cert is not initialized
postgres-1  | 2025-05-25 18:23:29.730 UTC [55] LOG:  checkpoint complete: wrote 355 buffers (2.2%); 0 WAL file(s) added, 0 removed, 0 recycled; write=36.905 s, sync=0.036 s, total=36.949 s; sync files=468, longest=0.002 s, average=0.001 s; distance=2852 kB, estimate=2852 kB; lsn=0/1BE3D40, redo lsn=0/1BE3D08
n8n         | The connection cannot be established, this usually occurs due to an incorrect host (domain) value
n8n         | getaddrinfo ENOTFOUND ollama
n8n         | getaddrinfo ENOTFOUND ollama
postgres-1  | 2025-05-25 18:27:52.833 UTC [55] LOG:  checkpoint starting: time
postgres-1  | 2025-05-25 18:27:53.249 UTC [55] LOG:  checkpoint complete: wrote 5 buffers (0.0%); 0 WAL file(s) added, 0 removed, 0 recycled; write=0.408 s, sync=0.002 s, total=0.417 s; sync files=5, longest=0.001 s, average=0.001 s; distance=1 kB, estimate=2567 kB; lsn=0/1BE4168, redo lsn=0/1BE4130
postgres-1  | 2025-05-25 19:22:53.052 UTC [55] LOG:  checkpoint starting: time
postgres-1  | 2025-05-25 19:22:55.768 UTC [55] LOG:  checkpoint complete: wrote 27 buffers (0.2%); 0 WAL file(s) added, 0 removed, 0 recycled; write=2.701 s, sync=0.009 s, total=2.717 s; sync files=22, longest=0.005 s, average=0.001 s; distance=95 kB, estimate=2320 kB; lsn=0/1BFC058, redo lsn=0/1BFC020
postgres-1  | 2025-05-25 19:27:53.822 UTC [55] LOG:  checkpoint starting: time
postgres-1  | 2025-05-25 19:27:54.036 UTC [55] LOG:  checkpoint complete: wrote 2 buffers (0.0%); 0 WAL file(s) added, 0 removed, 0 recycled; write=0.205 s, sync=0.003 s, total=0.215 s; sync files=2, longest=0.003 s, average=0.002 s; distance=7 kB, estimate=2088 kB; lsn=0/1BFDE68, redo lsn=0/1BFDE30
postgres-1  | 2025-05-25 20:22:53.705 UTC [55] LOG:  checkpoint starting: time
postgres-1  | 2025-05-25 20:22:56.148 UTC [55] LOG:  checkpoint complete: wrote 24 buffers (0.1%); 1 WAL file(s) added, 0 removed, 0 recycled; write=2.415 s, sync=0.008 s, total=2.444 s; sync files=20, longest=0.006 s, average=0.001 s; distance=88 kB, estimate=1888 kB; lsn=0/1C140A8, redo lsn=0/1C14070
postgres-1  | 2025-05-25 21:22:53.894 UTC [55] LOG:  checkpoint starting: time
postgres-1  | 2025-05-25 21:22:56.214 UTC [55] LOG:  checkpoint complete: wrote 23 buffers (0.1%); 0 WAL file(s) added, 0 removed, 0 recycled; write=2.308 s, sync=0.005 s, total=2.320 s; sync files=18, longest=0.004 s, average=0.001 s; distance=93 kB, estimate=1709 kB; lsn=0/1C2B760, redo lsn=0/1C2B728
postgres-1  | 2025-05-25 22:22:54.033 UTC [55] LOG:  checkpoint starting: time
postgres-1  | 2025-05-25 22:22:55.821 UTC [55] LOG:  checkpoint complete: wrote 18 buffers (0.1%); 0 WAL file(s) added, 0 removed, 0 recycled; write=1.775 s, sync=0.005 s, total=1.789 s; sync files=14, longest=0.004 s, average=0.001 s; distance=99 kB, estimate=1548 kB; lsn=0/1C44698, redo lsn=0/1C44660
postgres-1  | 2025-05-25 23:22:55.666 UTC [55] LOG:  checkpoint starting: time
postgres-1  | 2025-05-25 23:22:57.978 UTC [55] LOG:  checkpoint complete: wrote 23 buffers (0.1%); 0 WAL file(s) added, 0 removed, 0 recycled; write=2.300 s, sync=0.005 s, total=2.313 s; sync files=18, longest=0.004 s, average=0.001 s; distance=95 kB, estimate=1403 kB; lsn=0/1C5C4B8, redo lsn=0/1C5C480

```
Note: In order for a docker container to access a host port outside of docker, one must change 'localhost' to 
`host.docker.internal`.  Thus, following the [For Mac users running OLLAMA locally](https://github.com/n8n-io/self-hosted-ai-starter-kit?tab=readme-ov-file#for-mac-users-running-ollama-locally) instructions, one must edit the environment variable to 
```
  environment:
    # ... other environment variables ...
    - OLLAMA_HOST=host.docker.internal:11434
```
### Run n8n
```
(base) jackkozik@Jacks-Mac-mini self-hosted-ai-starter-kit % docker compose up
[+] Running 4/4
 ✔ Container qdrant                                 Running                                              0.0s
 ✔ Container self-hosted-ai-starter-kit-postgres-1  Running                                              0.0s
 ✔ Container n8n-import                             Created                                              0.0s
 ✔ Container n8n                                    Running                                              0.0s
Attaching to n8n, n8n-import, qdrant, postgres-1
n8n-import  | Permissions 0644 for n8n settings file /home/node/.n8n/config are too wide. This is ignored for now, but in the future n8n will attempt to change the permissions automatically. To automatically enforce correct permissions now set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true (recommended), or turn this check off set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=false.
n8n-import  | User settings loaded from: /home/node/.n8n/config
n8n-import  |
n8n-import  | There is a deprecation related to your environment variables. Please take the recommended actions to update your configuration:
n8n-import  |  - N8N_RUNNERS_ENABLED -> Running n8n without task runners is deprecated. Task runners will be turned on by default in a future version. Please set `N8N_RUNNERS_ENABLED=true` to enable task runners now and avoid potential issues in the future. Learn more: https://docs.n8n.io/hosting/configuration/task-runners/
n8n-import  |
n8n-import  | Successfully imported 2 credentials.
n8n-import  | Permissions 0644 for n8n settings file /home/node/.n8n/config are too wide. This is ignored for now, but in the future n8n will attempt to change the permissions automatically. To automatically enforce correct permissions now set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true (recommended), or turn this check off set N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=false.
n8n-import  | User settings loaded from: /home/node/.n8n/config
n8n-import  |
n8n-import  | There is a deprecation related to your environment variables. Please take the recommended actions to update your configuration:
n8n-import  |  - N8N_RUNNERS_ENABLED -> Running n8n without task runners is deprecated. Task runners will be turned on by default in a future version. Please set `N8N_RUNNERS_ENABLED=true` to enable task runners now and avoid potential issues in the future. Learn more: https://docs.n8n.io/hosting/configuration/task-runners/
n8n-import  |
n8n-import  | Importing 1 workflows...
n8n-import  | Successfully imported 1 workflow.
n8n-import exited with code 0
postgres-1  | 2025-05-26 01:37:57.633 UTC [55] LOG:  checkpoint starting: time
postgres-1  | 2025-05-26 01:37:57.871 UTC [55] LOG:  checkpoint complete: wrote 3 buffers (0.0%); 0 WAL file(s) added, 0 removed, 0 recycled; write=0.222 s, sync=0.004 s, total=0.239 s; sync files=3, longest=0.003 s, average=0.002 s; distance=2 kB, estimate=1043 kB; lsn=0/1C991D8, redo lsn=0/1C991A0


postgres-1  | 2025-05-26 02:22:58.501 UTC [55] LOG:  checkpoint starting: time
n8n         | fetch failed
n8n         | getaddrinfo ENOTFOUND ollama
postgres-1  | 2025-05-26 02:23:01.976 UTC [55] LOG:  checkpoint complete: wrote 34 buffers (0.2%); 0 WAL file(s) added, 0 removed, 0 recycled; write=3.458 s, sync=0.014 s, total=3.476 s; sync files=29, longest=0.006 s, average=0.001 s; distance=111 kB, estimate=950 kB; lsn=0/1CB6D38, redo lsn=0/1CB4E98
n8n         | The connection cannot be established, this usually occurs due to an incorrect host (domain) value
n8n         | getaddrinfo ENOTFOUND ollama
n8n         | getaddrinfo ENOTFOUND ollama
n8n         | The connection cannot be established, this usually occurs due to an incorrect host (domain) value
n8n         | getaddrinfo ENOTFOUND ollama
n8n         | getaddrinfo ENOTFOUND ollama
postgres-1  | 2025-05-26 02:27:59.009 UTC [55] LOG:  checkpoint starting: time
postgres-1  | 2025-05-26 02:28:00.806 UTC [55] LOG:  checkpoint complete: wrote 18 buffers (0.1%); 0 WAL file(s) added, 0 removed, 0 recycled; write=1.783 s, sync=0.007 s, total=1.797 s; sync files=15, longest=0.004 s, average=0.001 s; distance=14 kB, estimate=857 kB; lsn=0/1CB88A8, redo lsn=0/1CB8870  ,
```
The n8n tool runs on `http://localhost:5678`.  I have a reverse proxy and I have it mapped to a subdomain on one of my domain names.  

### login to n8n
I access the n8n portal for the first time.  I prompts me to setup an admin account with a user id / password.  Then all access to n8n starts with a login screen

![image](https://github.com/user-attachments/assets/75fc6fc7-6728-40fc-ab5b-58e1629c1b5c)

### Click on Demo Work Flow

The n8n repository sets up a nice Demo Workflow -- sort of a hello world for an agent that works with an LLM.  Click on Demo Workflow:

![image](https://github.com/user-attachments/assets/80763c46-248a-4fc4-ac72-ff970b58643a)

Click on the Ollama Chat Model and verify:

![image](https://github.com/user-attachments/assets/b4a1fae1-316c-4385-930d-0eec0658e6ca)

That the Model has an error fetching options from the Ollama Chat Model.  That error is because n8n is running in a docker container and ollama is not.  Go back to the Overview section.  Click on credentials->Local Ollama Service. Change the Base URL to `http://host.docker.internal:11434`.  Click Retry to verify that the Connection is setup correctly.

![image](https://github.com/user-attachments/assets/550e6ea2-70c9-4cec-9dae-cfc6a5277677)

And Save it.

### Try a simple Chat
I verify that the n8n setup queries ollama by trying a Chat.  Click on Open Chat and type a message.  It should reply back quickly.  Note: if the reply is a slow one, word, at, a, time -- that indicates that the Ollama setup is not configured to use the Apple SIlicon.  
![image](https://github.com/user-attachments/assets/5e08b278-e5aa-495d-9c36-d8e5a38e01c5)

Note also, the graphic animates showing the progress of the prompt back and forth.











# References

 - [They made a Mac for EVERYBODY - M4 Mac Mini](https://www.youtube.com/watch?v=9h8jf4wgW3o) by [Raid Owl](https://www.youtube.com/@RaidOwl)
 - [How to Install Ollama, Docker, and Open WebUI on MacOS](https://www.youtube.com/watch?v=3qGLMlsB8Us) by [BlueSpork](https://www.youtube.com/@BlueSpork)
 - [self-hosted-ai-starter-kit](https://github.com/n8n-io/self-hosted-ai-starter-kit) repository by [N8N github account](https://github.com/n8n-io)
 - [Installing and Using Local AI for n8n](https://www.youtube.com/watch?v=xz_X2N-hPg0)
 - [The BEST Local AI Setup – Run Everything FREE (LLMs + n8n + MCP, No Code)](https://www.youtube.com/watch?v=PB24nnMBHlc&t=53s)
 - 

