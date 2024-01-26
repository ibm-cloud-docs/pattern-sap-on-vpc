---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-25"

subcollection: pattern-sap-on-vpc
keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for resiliency
{: #resiliency-decisions}

The following sections summarize the resiliency architecture decisions for risiliency for the SAP on VPC pattern.


## Architecture decisions for high availability
{: #ha-arch}

| Architecture decision | Requirement | Alternative | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| High Availability HANA                          | Provide 99.95% availability for HANA DB               | HANA System Replication (HSR)                                                                                                                                                                                                                     | Enabling HANA HSR addresses SAP HANA outage reduction due to planned maintenance, faults, and disasters. It supports a recovery point objective (RPO) of 0 seconds and a recovery time objective (RTO) measured in minutes.                                                                                                                                               |
| High Availability Infrastructure                | Provide 99.95% availability for infrastructure        | -   Redundant VSIs in an [SAP Scale-out](/docs/sap?topic=sap-refarch-hana-scaleout#network-layout-for-scale-out-configurations-2) deployment with VPC ALB solution on a single-zone can provide an application SLA of 99.95% \n Auto Scale for VPC (optional)  | Minimize cost, implementation and maintenance complexity, potential latency and maximize value with IBM solutions.                                                                                                                                                                                                                                                        |
{: caption="Table 1. Architecture decisions for High Availability(HA)" caption-side="bottom"}


## Architecture decisions for disaster recovery
{: #da-arch}

| Architecture decision | Requirement | Alternative | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Disaster Recovery -- application/infrastructure | Disaster recovery capability in secondary region      | Veeam                                                                                                                                                                                                                                             | -   Support for databases (HANA, Oracle or MSSQL). \n -   DR capability for RPO \< 15 min, RTO \< 4 hours. Veeam service seamlessly integrates directly with IBM cloud VPC to help achieve high availability. This service provides recovery points and time objectives for SAP application servers. Controls both the backups and restores of all virtual machines (VMs) for SAP applications directly from the Veeam console.                                                                                                                                                                                                                                                                                                                         |
| Disaster Recovery - HANA                        | HANA disaster recovery capability in secondary region | Hana System Replication (HSR)                                                                                                                                                                                                                     | Continuous replication of data from a primary to a secondary system in a separate region, including in-memory loading, system replication facilitates rapid failover in the event of a disaster                                                                                                                                                                           |
{: caption="Table 2. Architecture decisions for Disaster Recovery (DR)" caption-side="bottom"}

## Architecture decisions for backup and restore
{: #backup-arch}

| Architecture decision | Requirement | Alternative | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- | -------------- |
| Backup (SAP)                                    | Back up of NetWeaver and HANA data                    | -   SAP NW file level backup \n -   SAP NW storage snapshot \n -   SAP HANA file level backup \n -   SAP HANA storage snapshot                                                                                                                                                                                                                    | Minimize cost and operational ease using SAP Native tools like **DBACOCKPIT, HANACOCKPIT, backint** will be used to take SAP Database backup.                                                                                                                                                                                                                             |
| Backup (Infrastructure) - VPC                   | Infrastructure backups                                | Veeam for snapshot backups at VM/BM level.                                                                                                                                                                                                        |The backups will be integrated with IBM Cloud native backup solution of Veeam using the API available to store the backup in the IBM Cloud Object Storage.                                                                                                                                                                                                            |
{: caption="Table 3. Architecture decisions for backup and restore" caption-side="bottom"}
