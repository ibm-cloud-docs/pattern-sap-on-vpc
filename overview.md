---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-23"

subcollection: pattern-sap-on-vpc
keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Overview of SAP on VPC
{: #overview}

The objective of this document is to provide an {{site.data.keyword.IBM}} solution design for the deployment of SAP on {{site.data.keyword.vpc_full}} (VPC). The solution design for this pattern is intended to:

-   Accelerate and simplify solution design by providing a standard {{site.data.keyword.vpc_short}} deployment architecture reference solution for SAP enterprise-class deployments that follow the [Architecture framework](/docs/architecture-framework?topic=architecture-framework-intro).

-   Provide a prescriptive, end to end enterprise-class solution design, that includes diagrams, component architecture decisions, and rationale for cloud component selection for a secure, resilient SAP on {{site.data.keyword.vpc_short}}.

-   Verify that requirements can be met from performance, system availability, and security perspectives.

SAP configuration and SAP component deployment scenarios aren't covered in the solution design. It's limited to {{site.data.keyword.Bluemix_short}} infrastructure options to support SAP workloads.

Enterprise-class, mission-critical workloads need to be secure, resilient, and provide high availability (HA) and disaster recovery (DR). This pattern can be used as a guide to meet typical customer requirements and provide a base reference solution for a secure and resilient SAP NetWeaver and HANA or SAP NetWeaver and AnyDB deployment to {{site.data.keyword.vpc_short}}.

It supports the deployment of SAP Business Applications running on SAP NetWeaver, SAP HANA or SAP AnyDB, and other SAP products by using other technologies. Other technologies include SAP Content Server or newer applications such as SAP Data Intelligence.

{{site.data.keyword.Bluemix_short}} SAP-Certified infrastructure provides the flexibility to run SAP workloads in the {{site.data.keyword.Bluemix_short}} and the ability to quickly address issues such as:

-   Moving SAP workloads to the cloud

-   Rapidly expanding or contracting capacity

-   Supplementing an existing private cloud architecture

Enterprise-class, mission-critical workloads need to be resilient and provide HA and DR. This pattern illustrates a single-zone, multi-region design deployed to {{site.data.keyword.vpc_short}}, which can provide both HA and DR to provide 99.95% availability for an SAP NetWeaver and HANA or SAP NetWeaver and AnyDB solution to meet typical customer requirements.

The documentation in this guide provides architecture considerations, design considerations, and guidance for deploying the infrastructure to support SAP workloads, including:

-   SAP Business Applications such as SAP S/4HANA or SAP BW/4HANA

-   SAP Technical Applications such SAP HANA database server and SAP NetWeaver application server
