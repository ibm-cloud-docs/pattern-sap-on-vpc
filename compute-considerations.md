---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-24"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Compute design
{: #compute-design}

{{site.data.keyword.ibm_cloud_sap}} provides SAP-certified infrastructure by using the latest {{site.data.keyword.BluVirtServers_short}} or {{site.data.keyword.baremetal_short_sing}}. These servers are available and offered in different profiles that define CPU and RAM combinations suitable and certified for SAP workloads.

It's critical that the appropriate profiles are chosen, since SAP certifies only specific VSI and {{site.data.keyword.baremetal_short_sing}} profiles in {{site.data.keyword.Bluemix_short}}. The range of HANA certified profiles available on {{site.data.keyword.vsi_is_short}} cover 90% of customer use cases for the HANA database service.

Multiple SAP certified VSI and {{site.data.keyword.baremetal_short_sing}} profiles are available for deployment of SAP NetWeaver and HANA on {{site.data.keyword.vpc_short}} that can be found by going to the following {{site.data.keyword.Bluemix_short}} docs:

- [NetWeaver VSI profiles](/docs/sap?topic=sap-nw-iaas-offerings-profiles-intel-vs-vpc)

- [NetWeaver Bare Metal profiles](/docs/sap?topic=sap-nw-iaas-offerings-profiles-intel-bm-vpc)

- [HANA VSI profiles](/docs/sap?topic=sap-hana-iaas-offerings-profiles-intel-vs-vpc)

- [HANA Bare Metal profiles](/docs/sap?topic=sap-hana-iaas-offerings-profiles-intel-bm-vpc)

For more information, see [Sizing process for SAP Systems](/docs/sap?topic=sap-sizing&interface=ui).

Choose a SAP {{site.data.keyword.baremetal_short_sing}} or VSI profile from the list of certified servers in the {{site.data.keyword.Bluemix_short}} catalog with the appropriate SAP image. You can't make changes to {{site.data.keyword.baremetal_short_sing}} servers.

HANA is an in-memory database, so memory sizing must be taken into consideration. If a HANA database size exceeds 5.6 TB of memory, PowerVS (with a range of profiles up to 22.5 TB) is the recommended landing zone and is covered in [SAP on PowerVS](/docs/pattern-sap-on-powervs?topic=pattern-sap-on-powervs-overview).

For a distributed SAP installation, it's  best to have all nodes in the same location (for example, the same availability zone or data center). Deviation from this setup can cause latency and timeouts, which render your SAP system unresponsive. Due to this, SAP does not support the application layer and database to be deployed across different zones; the application and database layers must exist in the same availability zone. Therefore, if the required memory for HANA targets a PowerVS deployment, the application layer must also be on PowerVS and not on VPC.

Databases typically experience growth over time so database size and expected data growth rates should be taken into consideration when planning database deployments.
{: tip}

## SAP AnyDB
{: #SAP-anydb}

AnyDB refers to any non-HANA, SAP supported database. SAP supports IBM DB2, Oracle, Microsoft SQL Server, SAP Max DB, SAP ASE, and SAP IQ.

Deploying SAP AnyDB on {{site.data.keyword.Bluemix_short}} is similar to deployments with infrastructure with on-premise data centers. The information that is provided from SAP and the RDBMS providers can be used. Review the following links to learn the design considerations for each database:

- [IBM DB2](/docs/sap?topic=sap-anydb-ibm-db2)

- [Microsoft SQL Server](/docs/sap?topic=sap-anydb-ms-sql-server)

- [SAP Max DB](/docs/sap?topic=sap-anydb-sap-maxdb)

- [SAP ASE](/docs/sap?topic=sap-anydb-sap-ase)

- [SAP IQ](/docs/sap?topic=sap-anydb-sap-iq)

Oracle is not an option for SAP on VPC and must be deployed on a {{site.data.keyword.powerSys_notm}} SAP environment.
{: note}
