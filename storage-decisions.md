---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-25"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for storage
{: #storage-decisions}

The following tables summarize the storage architecture decisions for SAP on VPC:

## Architecture decisions for Bare Metal storage
{: #bare-metal-storage table}

The following are architecture decisions for Bare Metal workloads for this design.

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Primary Storage             | Local file storage on bare metal                           | Local Non-Volatile Memory Express (NVMe) storage                                                                                                              | All SAP Certified {{site.data.keyword.baremetal_short}} have local NVMe storage. Block and file storage aren't applicable.                                            |
| Backup Storage              | Backup storage for {{site.data.keyword.baremetal_short}}                      | Block storage \n {{site.data.keyword.cos_full_notm}}                                                                                                                   | -  {{site.data.keyword.cos_full_notm}} is more cost effective. \n -   Combine block and {{site.data.keyword.cos_full_notm}} for long-term needs.|
| Archive Storage             | Archive Storage for {{site.data.keyword.baremetal_short}}                     | {{site.data.keyword.cos_full_notm}}                                                                                                            | {{site.data.keyword.cos_full_notm}} is used for cost optimized options such as archiving                                                                       |
{: caption="Table 1. Architecture decisions for Bare Metal storage" caption-side="bottom"}


## Architecture decisions for VSIs
{: #bare-metal-storage table}

The following are architecture decisions for VSIss for this design.

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Primary Storage             | Primary storage for VSIs                           | Block Storage                                                                                                                   | -   Use a mix of IOPs block storage for production workloads and less cost storage when high IOPs are not required \n *SAP HANA production systems require 10 IOPS/GB block storage \n * 3 IOPS for application servers \n * 5 IOPS for nonproduction databases \n * Block allows clustering of volumes at the application layer for higher IOPS                              |
| Backup Storage              | Backup storage for VSIs                            | combination of {{site.data.keyword.cos_full_notm}} and Block Storage                                                                                            | * Combine Block, Endurance, and {{site.data.keyword.cos_full_notm}} for long-term needs \n * {{site.data.keyword.cos_full_notm}} is used for cost optimized options for Backups \n * {{site.data.keyword.cos_full_notm}} Regional or Cross Regional based on availability|
| Archive Storage             | Archive storage for VSIs                           | {{site.data.keyword.cos_full_notm}}                                                                                                            | {{site.data.keyword.cos_full_notm}} cold vault or archiving tier is used for cost optimized options such as archiving                                          |
| Data and storage migration \n For more information, see [Moving SAP Workloads](/docs/sap?topic=sap-faq-moving-sap-workloads#faq-moving-sap-workloads-overview)| Migration tools from existing environment to PowerVS | Migration tools from existing environment to PowerVS                                                                                               |Image import removes the need for testing and is useful for nonproduction and PoC systems
|                                   |                                                        |DB DR replication                                                                                                                                    |Using Native DB replication minimizes the need for testing efforts
|                                   |                                                        |SAP Standard Migration tools                                                                                                                        |SAP Standard Migration options like SWPM, DMO
|                                   |                                                        |Backup and restore tools                                                                                                                                |Aspera for high-speed data transfer is ideal for migrations
|                                   |                                                        |Aspera data transfer                                                                                                                                 | Minimize business disruption due to migration. Minimize the cost and efforts that are incurred in testing migrated databases. |
{: caption="Table 2. Architecture decisions for VSIs" caption-side="bottom"}
