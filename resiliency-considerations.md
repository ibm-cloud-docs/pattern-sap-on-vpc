---

copyright:
  years: 2023
lastupdated: "2023-12-26"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Resiliency design
{: #resiliency-design}

Resiliency is the ability of a workload to meet a specific target Service Level Objective (SLO), Service Level Availability (SLA) or recover from a service disruption and still meet the required SLA. Resiliency needs to be considered at both the infrastructure and application layers across the entire solution.

A resilient design may include Disaster Recovery (DR) and High Availability (HA) depending on SLA requirements and they are two different things.

Disaster Recovery is the infrastructure, application layers and accompanying set of policies and procedures to enable the recovery or continuation of vital technology infrastructure and applications following a natural or human-induced disaster.

High Availability is the resource availability in a solution throughout the stack, built in by design, to withstand individual component failures in the system.

Both DR and HA can be enabled using several technologies and approaches which depends on the Recovery Point Objective (RPO), Recovery Time Objective (RTO) and SLA requirements.

The table below shows a comparison of the different deployment options.

| Deployment    | Availability | Description   | Recommended use   |
|------------------|------------------|------------------|------------------|
| Single Zone                 | 99.9%^1^        |Single instance (single point of failure) or multiple instances (protects from infrastructure failures) |Low to medium priority applications                                             |
|                             |                 |Low/Medium cost                                                                                         |Non-production environment                                                      |
| Single Zone; Multi Instance | 99.95%          |Multi-instance (protects from infrastructure failures)                                                  |Core business applications                                                      |
|                             |                 |                                                                                                            |Production level environments with resiliency requirements not exceeding 99.95% |
| Multi-zone, Single Region   | 99.99%^2^       |Redundant resources                                                                                     |Core business applications                                                      |
|                             |                 |Protection from zone outages                                                                            |Production level environments with stringent resiliency requirements
|                             |                 |Medium/high cost                                                                                        |                                                                                    |
| Multi-zone, Multi-Region    | 99.99%          |Protection from region outages                                                                          |Disaster Recovery
|                             |                 |High cost                                                                                               |Business continuity policies with cross geo or cross-country requirements       |
{: caption="Table 1. Resiliency options" caption-side="bottom"}

1.  Based on Cloud infrastructure [SLA.](https://www.ibm.com/support/customer/csol/terms/?id=i126-9268&lc=en#detail-document) Does not represent application availability

2.  3 or more instances in separate Availability Zones

As mentioned in the Compute section, SAP does not support the application layer and database to be deployed across different zones; the application and database layers must exist in the same availability zone. Therefore, the highest availability that can be supported is 99.95%

For more information on Resiliency on IBM Cloud, see [High Availability and Resiliency on IBM Cloud](https://cloud.ibm.com/docs/ha-infrastructure?topic=ha-infrastructure-landing-about-ha-dr-backup).

99.95% infrastructure availability can be achieved in a single zone by deploying multiple server instances for each of the security, application and database components.

To maximize investment on DR infrastructure so DR infrastructure is not idle, it's recommended to have cross-region passive DR with the DR region hosing non-production workloads. This can optimize the DR environment for additional cost savings.

The IBM Cloud environment does not support any preconfigured high-availability (HA) scenarios for SAP. However, HA scenarios can be configured based on the HA extension for the operating system. HA extensions are created by adding the required hardware and the required software components to SAP landscapes.

[Placement groups](https://cloud.ibm.com/docs/vpc?topic=vpc-about-placement-groups-for-vpc) should be used when you deploy multiple virtual server instances. While the IBM Cloud VSI scheduler attempts to place the virtual server instances on different hypervisors, the scheduler might not succeed. If they are not placed on different hypervisors, then a single point of failure is introduced. Creating multiple virtual server instances that offer the same service and use placement groups, ensures the application is better protected against hardware or software failures, and even for unplanned maintenance.

IBM Cloud application load balancer spreads client requests or loads across 2 or more server instances for improved resiliency and improved performance. In addition, IBM Cloud load balancers do health checks to ensure that only \"healthy\" virtual server instances receive client requests.

[Here](https://cloud.ibm.com/docs/sap?topic=sap-refarch-hana-scaleout#network-layout-for-scale-out-configurations-2) is an overview of a single-zone resilient SAP Scale-out deployment.

A combination of SAP Native Database Backup tools is used to deliver the resiliency services such as:

-   DBACOCKPIT

-   HANACOCKPIT

-   Backint for SAP Database backups

To support database recovery for points in time going back at least one month, a daily database backup is required, along with redo log backups every 15 minutes.

-   For long-term recovery of data, an additional monthly backup is suggested with a one-year data retention or as determined by the customer.

-   The daily log backup frequency for production DB should be less than or equal to the customer desired RPO parameter for their Business Continuity Plan

-   Production System Monthly full retained for 60 days. Daily Full retained for 1 week. Daily incremental retained for 60 days. Weekly Full retained for 30 days.

-   Non-Productions System Monthly full retained for 60 days. Weekly Full retained for 14 days week. Daily incremental retained for 60 days.

Consider the largest DB size for full backups with room for addition growth. Recommend complementing the backup solution with Daily snapshots for production.
