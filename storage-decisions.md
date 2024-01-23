---

copyright:
  years: 2023
lastupdated: "2023-12-26"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for storage
{: #storage-decisions}

|Architecture decision                |Requirement                                                                 |Decision                 |Rationale                                                                    |
|---|---|---|---|
| **Workloads -- Bare Metal** |                                                    |                                                                                                                                 |                                                                                                                                                 |
| Primary Storage             | local file storage on BM                           | Local NVMe storage                                                                                                              | All SAP Certified BM servers have local NVMe storage. There are no options for block or file storage.                                           |
| Backup Storage              | Backup storage for BM servers                      | Block storage \n Cloud Object Storage                                                                                                                   | -   Cloud Object Storage for lower costs \n -   Combine Block and COS for long-term needs|
| Archive Storage             | Archive Storage for BM servers                     | Cloud Object Storage                                                                                                            | Cloud Object Storage is used for cost optimized options such as Archiving                                                                       |
| **Workloads -- VSIs**       |                                                    |                                                                                                                                 |                                                                                                                                                 |
| Primary Storage             | Primary storage for VSIs                           | Block Storage                                                                                                                   | -   Use a mix of IOPs block storage for production workloads and lower cost storage when high IOPs not required \n-   SAP HANA production systems require 10 IOPS/GB block storage \n-   3 IOPS for application servers \n-   5 IOPS for non production databases \n-   Block allows clustering of volumes at the application layer for higher IOPS                              |
| Backup Storage              | Backup storage for VSIs                            | Combination of COS and Block Storage                                                                                            | -   Combine Block/Endurance and COS for long-term needs \n -   Cloud Object Storage is used for cost optimized options for Backups  \n -   COS Regional or Cross Regional based on availability|
| Archive Storage             | Archive storage for VSIs                           | Cloud Object Storage                                                                                                            | Cloud Object Storage Cold Vault or Archiving tier is used for cost optimized options such as Archiving                                          |
| Data/Storage Migration \n For more migration information see [Moving SAP Workloads](/docs/sap?topic=sap-faq-moving-sap-workloads#faq-moving-sap-workloads-overview)| Migration tooling from existing environment to PowerVS | Migration tooling from existing environment to PowerVS                                                                                               |Image import obviates need for testing and useful for non-prod/PoC systems
|                                   |                                                        |DB DR Replication                                                                                                                                    |Using Native DB Replication minimizes need for testing efforts
|                                   |                                                        |SAP Standard Migration Tools                                                                                                                        |SAP Standard Migration options like SWPM, DMO
|                                   |                                                        |Backup/ Restore tools                                                                                                                                |ASPERA for high-speed data transfer ideal for Migrations
|                                   |                                                        |Aspera data transfer                                                                                                                                 | Minimize \n -   Business disruption due to migration \n -   Cost and efforts incurred in testing migrated databases|
{: caption="Table 1. Architecture decisions for storage" caption-side="bottom"}
