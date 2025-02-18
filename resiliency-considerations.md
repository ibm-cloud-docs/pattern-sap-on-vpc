---

copyright:
  years: 2023, 2024
lastupdated: "2025-02-18"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Resiliency design
{: #resiliency-design}

Resiliency is the ability for a workload to meet a specific target Service Level Objective (SLO), Service Level Availability (SLA), or recover from a service disruption and still meet the required SLA. Resiliency needs to be considered at both the infrastructure and application layers across the entire solution.

A resilient design might include High Availability (HA) and Disaster Recovery (DR) depending on SLA requirements.

Disaster recovery is the infrastructure, application layers, and accompanying set of policies and procedures that enable the recovery or continuation of vital technology infrastructure and applications from a natural or human-induced disaster.

High availability is the resource availability in a solution throughout the stack. It's built in by design to withstand individual component failures in the system.

You can enable both HA and DR by using several technologies and approaches that depend on the Recovery Point Objective (RPO), Recovery Time Objective (RTO), and SLA requirements.

The following tables show a comparison of the different deployment options.

| Deployment | Availability | Description | Recommended use |
|------------------|------------------|------------------|------------------|
| Single Zone                 | 99.9%[^tabletext]        |Single instance (single point of failure) or multiple instances (protect from infrastructure failures) |Low to medium priority applications                                             |
|                             |                 |Low to Medium cost                                                                                         |Nonproduction environment                                                      |
| Single Zone; Multi-Instance | 99.95%          |Multi-instance (protects from infrastructure failures)                                                  |Core business applications                                                      |
|                             |                 |                                                                                                            |Production level environments with resiliency requirements not exceeding 99.95% |
| Multi-zone, Single Region   | 99.99%[^tabletext2]       |Redundant resources                                                                                     |Core business applications                                                      |
|                             |                 |Protection from zone outages                                                                            |Production level environments with stringent resiliency requirements
|                             |                 |Medium to high cost                                                                                        |                                                                                    |
| Multi-zone, Multi-Region    | 99.99%          |Protection from region outages                                                                          |Disaster Recovery
|                             |                 |High cost                                                                                               |Business continuity policies with cross-geo or cross-country requirements       |

[^tabletext]: Based on Cloud infrastructure [SLA.](https://www.ibm.com/support/customer/csol/terms/?id=i126-9268&lc=en#detail-document) Does not represent application availability.

[^tabletext2]: Three or more instances in separate Availability Zones
{: caption="Resiliency options" caption-side="bottom"}

SAP does not support the application layer and database to be deployed across different zones. The application and database layers must exist in the same availability zone. Therefore, the highest availability that can be supported is 99.95%.
{: important}

For more information, see [High Availability and Resiliency on {{site.data.keyword.Bluemix_notm}}](/docs/resiliency?topic=resiliency-resiliency-overview).

## Availability considerations
{: #availability-considerations}

99.95% infrastructure availability can be achieved in a single zone by deploying multiple server instances for each of the security, application, and database components. To maximize investment on DR infrastructure so DR infrastructure is not idle, it's recommended to have cross-region passive DR with the DR region hosing nonproduction workloads. This can optimize the DR environment for additional cost savings. The {{site.data.keyword.Bluemix_notm}} environment does not support any preconfigured high-availability (HA) scenarios for SAP. However, HA scenarios can be configured based on the HA extension for the operating system. HA extensions are created by adding the required hardware and the required software components to SAP landscapes.

[Placement groups](https://cloud.ibm.com/docs/vpc?topic=vpc-about-placement-groups-for-vpc) should be used when you deploy multiple virtual server instances. While the {{site.data.keyword.Bluemix_notm}} VSI scheduler attempts to place the virtual server instances on different hypervisors, the scheduler might not succeed. If they are not placed on different hypervisors, then a single point of failure is introduced. Creating multiple virtual server instances that offer the same service and use placement groups, ensures that the application is better protected against hardware or software failures, and even for unplanned maintenance.

{{site.data.keyword.Bluemix_notm}} application load balancer spreads client requests or loads across 2 or more server instances for improved resiliency and improved performance. In addition, {{site.data.keyword.Bluemix_notm}} load balancers do health checks to ensure that only "healthy" virtual server instances receive client requests.

To learn more about single-zone resilient SAP deployment, see [Network layout for Scale-out configurations](/docs/sap?topic=sap-refarch-hana-scaleout#network-layout-for-scale-out-configurations-2).


## SAP Native Database backup tools
{: #SAP-database-tools}

A combination of SAP Native Database Backup tools are used to deliver the resiliency services:

* DBACOCKPIT

* HANACOCKPIT

* Backint for SAP Database backups


Review the following information about the backup tools and their requirements:

* To support database recovery that goes back at least one month, a daily database backup is required, along with redo log backups every 15 minutes.

* Long-term recovery of data: Additional monthly backup is suggested with a one year data retention or as determined by the customer.

* Frequency: The daily log backup frequency for production database should be less than or equal to the customer desired RPO parameter for their Business Continuity Plan.

* Retention: The production system monthly full is retained for 60 days. Daily full is retained for 1 week. Daily incremental retained for 60 days. Weekly Full retained for 30 days.

* Nonproductions system monthly full retained for 60 days. Weekly full retained for 14 days a week. Daily incremental retained for 60 days.

Consider the largest database size for full backups with room for addition growth. It's recommended to complement the backup solution with Daily snapshots for production.
{: tip}
