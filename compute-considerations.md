---

copyright:
  years: 2023
lastupdated: "2023-12-28"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Compute design
{: #compute-design}

IBM Cloud for SAP on VPC provides SAP-certified infrastructure by using the latest Virtual or Bare Metal Servers. These servers are available and offered in different profiles that define CPU and RAM combinations suitable and certified for SAP workloads.

SAP only certifies specific VSI and Bare Metal server profiles in IBM Cloud, therefore it is critical that the appropriate profile(s) are chosen. The range of HANA certified profiles available on VPC VSIs cover 90% of Customer use cases for the HANA database service.

There are a variety of SAP certified VSI and Bare Metal server profiles for deployment of SAP NetWeaver and HANA on IBM Cloud VPC which can be found on IBM Cloud Docs at the following links.

[NetWeaver VSI profiles](https://cloud.ibm.com/docs/sap?topic=sap-nw-iaas-offerings-profiles-intel-vs-vpc)

[NetWeaver Bare Metal profiles](https://cloud.ibm.com/docs/sap?topic=sap-nw-iaas-offerings-profiles-intel-bm-vpc)

[HANA VSI profiles](https://cloud.ibm.com/docs/sap?topic=sap-hana-iaas-offerings-profiles-intel-vs-vpc)

[HANA Bare Metal profiles](https://cloud.ibm.com/docs/sap?topic=sap-hana-iaas-offerings-profiles-intel-bm-vpc)

For sizing information see [Sizing process for SAP Systems](https://cloud.ibm.com/docs/sap?topic=sap-sizing&interface=ui).

Choose an SAP Bare Metal or VSI profile from the list of certified servers in the IBM Cloud Catalog along with the appropriate SAP image. Changes are not allowed to Bare Metal servers.

HANA is an "in-memory" database so memory sizing must be taken into consideration. If a HANA database size exceeds 5.6 TB of memory, PowerVS (with a range of profiles up to 22.5 TB) is the recommended landing zone and is covered in [SAP on PowerVS](https://cloud.ibm.com/docs/pattern-sap-on-powervs?topic=pattern-sap-powervs-overview).

For a distributed SAP installation, it is best to have all nodes in the same location (for example, the same Availability Zone or Datacenter). Deviation from this setup can cause latency and timeouts, which render your SAP system unresponsive. Due to this, SAP does not support the application layer and database to be deployed across different zones; the application and database layers must exist in the same availability zone. Therefore, if the required memory for HANA targets a PowerVS deployment, the application layer must also be on PowerVS, NOT VPC.

Databases typically experience growth over time so database size and expected data growth rates should be taken into consideration when planning database deployments.

**SAP AnyDB**

AnyDB refers to any non-HANA, SAP supported database. SAP supports: IBM DB2, Oracle, Microsoft SQL Server, SAP Max DB, SAP ASE and SAP IQ.

Deploying SAP AnyDB on IBM Cloud is similar to deployments with infrastructure with on-premises data centers. The information that is provided from SAP and the RDBMS providers can be used. The following links contain design considerations for each database:

[IBM DB2](https://cloud.ibm.com/docs/sap?topic=sap-anydb-ibm-db2)

[Microsoft SQL Server](https://cloud.ibm.com/docs/sap?topic=sap-anydb-ms-sql-server)

[SAP Max DB](https://cloud.ibm.com/docs/sap?topic=sap-anydb-sap-maxdb)

[SAP ASE](https://cloud.ibm.com/docs/sap?topic=sap-anydb-sap-ase)

[SAP IQ](https://cloud.ibm.com/docs/sap?topic=sap-anydb-sap-iq)

Oracle is not an option for SAP on VPC and must be deployed on a Power Virtual Server SAP environment.
