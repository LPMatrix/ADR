## Choose storage technology

## Problem statement
Working on apps that need data to be persisted, a decision on which storage technology needs to be adopted have to be made.

## Decision matrix

|Criteria|PostgreSQL|CosmosDb|
|---|---|---|
|Description  | Azure Database for PostgreSQL is a relational DB. There is no free tier. | CosmosDb is a multi-purpose document database that can handle multiple APIs. There is one [free tier](https://docs.microsoft.com/en-us/azure/cosmos-db/free-tier) database per Azure account with 1000 RUs and 25 Gb of storage. |
|Storage costs<br>(costs to store the data based on 10 years data retention)| Basic: $1/month ($0.10 GB/month).<br />General Purpose: $1.15/month ($0.115 GB/month). | Free, if the free tier can be used.<br/>Otherwise: 2.5 USD / month based on assumptions below |
|Operation costs<br>(costs per utilization, querying)| Basic (1 vCore, 2GiB memory) $24.82/month.<br/> General Purpose (2 vCore, 10GiB memory) $127.896/month | Free, if the free tier can be used.<br/>Otherwise: 400RU/s, 23.36 USD/month based on assumptions below |
|Complexity<br>(schema migrations, deployment automation) | Requires you to create and maintain a schema. Local emulator (local install or Docker). | Does not require you to maintain a schema.  We recommend using the SQL API (performance, support). Local emulator for all platforms Windows: local install. Other platforms: Docker. |
|Infrastructure<br/>(deployment through CI) | Supported by Terraform. | Supported by Terraform. |
|Disaster recovery<br>(Backup, SLA, Availability Zones, Multi region support) | It supports data backup and recovery. [More](https://docs.microsoft.com/en-us/azure/postgresql/howto-restore-server-portal)                                                | Backup: [Online backup](https://docs.microsoft.com/en-us/azure/cosmos-db/online-backup-and-restore)<br/>SLA: [99.99% to 99.999%](https://docs.microsoft.com/en-us/azure/cosmos-db/high-availability#slas-for-availability)<br/>Availability Zones: [In selected regions](https://docs.microsoft.com/en-us/azure/cosmos-db/high-availability#availability-zone-support)<br/>Multi region support: [yes](https://docs.microsoft.com/en-us/azure/cosmos-db/high-availability#high-availability-with-azure-cosmos-db-in-the-event-of-regional-outages) |
|Team/Developer experience<br>(can run/test locally)| Team has experience. Currently, no Docker experience in team. | No experience with CosmosDb in team currently, but NoSQL databases are known. Currently, no Docker experience in team. |
|Feature: multi results querying<br>(get pending payments, get notified customers)| Yes | Yes (need to pay attention to [partition strategy](https://devblogs.microsoft.com/cosmosdb/data-modeling-and-partitioning-for-relational-workloads/)) |
|Feature: create/update/get item by key<br>(get a payment, get a notified customer)| Yes | Yes |
|Feature: Power BI integration<br>(Power BI can connect to this data source)| [PostreSQL Connector](https://docs.microsoft.com/en-us/power-query/connectors/postgresql) | [CosmosDb Connector](https://docs.microsoft.com/en-us/azure/cosmos-db/sql/powerbi-visualize)|
|Feature: Security<br>(encryption transit/at rest, network isolation, ip firewall)| Supports [Firewall](https://docs.microsoft.com/en-us/azure/postgresql/howto-manage-firewall-using-portal) and [Encryption](https://docs.microsoft.com/en-us/azure/postgresql/howto-data-encryption-portal) | encryption (transit/at rest) [Encrypted in transit, at rest and in backup](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)<br/>network isolation: [use virtual network service tags to achieve network isolation](https://docs.microsoft.com/en-us/azure/cosmos-db/database-security?tabs=sql-api#how-does-azure-cosmos-db-secure-my-database)<br/> ip firewall: [supports policy driven IP-based access controls for inbound firewall support](https://docs.microsoft.com/en-us/azure/cosmos-db/database-security?tabs=sql-api#how-does-azure-cosmos-db-secure-my-database) |
|Feature: time to live<br>(delete data after X amount of time)| Not built-in. Can be implemented as a [trigger](https://stackoverflow.com/questions/26046816/is-there-a-way-to-set-an-expiry-time-after-which-a-data-entry-is-automaticall) | [Provides the ability to delete items automatically from a container after a certain time period.](https://docs.microsoft.com/en-us/azure/cosmos-db/sql/time-to-live) Deletion of expired items is a background task that consumes left-over Request Units |