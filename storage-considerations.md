---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-25"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Storage design considerations
{: #storage-design}

SAP solutions want to ensure that enough storage available to accommodate the existing environment and allow for more data growth for primary, backup, and archive storage. You need to choose the appropriate SAP certified profile to meet primary storage and growth requirements for workloads.

## Bare Metal Storage considerations
{: #bare-metal-considerations}

By default, {{site.data.keyword.baremetal_long}} come with high-performance and highly reliable internal storage based on solid-state disks and high-performance RAID adapters. All SAP certified {{site.data.keyword.baremetal_short}} profiles for VPC provide one 0.96 TB SATA M.2 mirrored SSD as the boot disk. Also, all SAP certified {{site.data.keyword.bm_is_short}} have 8 - 16 Non-Volatile Memory Express (NVMe) U.2 solid-state drives (SSD) as secondary local storage, depending on their size, which needs to be configured after the server deployment. NVMe Solid State Drive (SSD) provides fast and affordable storage to support customer-managed RAID.

Storage for {{site.data.keyword.bm_is_short}} is not managed. The client is responsible for backing up data.

If more storage is required on {{site.data.keyword.baremetal_short}}, for example, for backup purposes, NFS-based file shares can be created and mounted. For more information, see [Creating file shares and mount targets](/docs/vpc?topic=vpc-file-storage-create).

Encryption in transit is not supported between {{site.data.keyword.block_storage_is_short}} and {{site.data.keyword.bm_is_short}}.
{: note}

File shares can be mounted only on supported on Linux&reg; operating systems that support NFS file shares. For specific storage layouts and profiles, see the [compute considerations section](/docs-draft/pattern-sap-on-vpc?topic=pattern-sap-on-vpc-compute-design) and [other storage considerations](/docs/sap?topic=sap-storage-design-considerations)
