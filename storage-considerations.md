---

copyright:
  years: 2023
lastupdated: "2023-12-26"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Storage design
{: #storage-design}

SAP solutions will want to ensure there is enough available storage to accommodate the existing environment and allow for additional data growth for primary, backup and archive storage. You will need to choose the appropriate SAP Certified profile to meet primary storage and growth requirements for workloads.

Bare Metal Storage Considerations

By default, IBM Cloud Bare Metal Servers come with high-performance and highly reliable internal storage based on solid-state disks and high-performance RAID adapters. All SAP certified Bare Metal Server profiles for VPC provide one 0.96 TB SATA M.2 mirrored SSD as the boot disk. Additionally, All SAP certified Bare Metal servers for VPC have 8 - 16 NVMe (Non-Volatile Memory Express) U.2 solid-state drives (SSD) as secondary local storage -- depending on their size -- which need to be configured after server deployment. NVMe SSDs provides fast and affordable storage to support customer-managed RAID.

Storage for VPC Bare Metal Servers is unmanaged. Client is responsible for backing up data.

If more storage is required on Bare metal servers, for example, for backup purposes, NFS-based file shares can be created and mounted. Learn more details in the corresponding chapter [Creating file shares and mount targets](https://cloud.ibm.com/docs/vpc?topic=vpc-file-storage-create). Encryption in transit is not supported between Block Storage for VPC and Bare Metal Servers for VPC.

File shares can be mounted only on supported on Linux operating systems that support NFS file shares.

For specific storage layouts, see the compute considerations section and profiles links above.

[Other Storage Considerations](https://cloud.ibm.com/docs/sap?topic=sap-storage-design-considerations)
