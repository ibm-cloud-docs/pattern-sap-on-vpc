---

copyright:
  years: 2023
lastupdated: "2023-12-26"

subcollection: pattern-sap-on-vpc
keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Overview
{: #overview}

The objective of this document is to provide an IBM Solution Design for the deployment of SAP on IBM Cloud Virtual Private Cloud (VPC) to:

-   Accelerate and simplify solution design by providing a standard IBM Cloud deployment architecture reference solution for SAP on IBM PowerVS enterprise-class deployments following the [IBM Architecture Framework](https://cloud.ibm.com/docs/architecture-framework?topic=architecture-framework-intro).

-   Provide a prescriptive, end-2-end enterprise-class solution design, with diagrams, component architecture decisions along with rationale for cloud component selection for a secure, resilient SAP on IBM Cloud VPC.

-   Ensure requirements can be met from performance, system availability and security perspectives.

This guide does not cover SAP configuration and SAP component deployment scenarios, it is limited to IBM cloud infrastructure options to support SAP workloads.

Enterprise-class, mission critical workloads need to be secure, resilient and provide disaster recovery (DR) capabilities and high availability (HA). This pattern can be used as a guide to meet typical customer requirements and provide a base reference solution for a secure and resilient SAP NetWeaver/HANA or SAP NetWeaver/AnyDB deployment to IBM VPC.

It supports the deployment of SAP Business Applications Running on SAP NetWeaver, SAP HANA or SAP AnyDB and other SAP products using other technologies (SAP Content Server, or newer applications such as SAP Data Intelligence).

IBM Cloud SAP-Certified Infrastructure provides the flexibility to run SAP workloads in the IBM Cloud and the ability to quickly address issues such as:

-   Moving SAP workloads to the cloud

-   Rapidly expanding or contracting capacity

-   Supplementing an existing private cloud architecture

Enterprise-class, mission critical workloads need to be resilient and provide disaster recovery (DR) capabilities and high availability (HA). This pattern illustrates a Single-Zone, Multi-Region design deployed to IBM Virtual Private Cloud (VPC), which can provide both DR and HA to provide 99.95 availability for an SAP NetWeaver/HANA or SAP NetWeaver/AnyDB solution to meet typical customer requirements.

The following documentation provides architecture, design considerations and guidance for deploying the infrastructure to support SAP workloads, including:

-   SAP Business Applications such as SAP S/4HANA or SAP BW/4HANA

-   SAP Technical Applications such SAP HANA database server and SAP NetWeaver application server
