---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-25"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Network design
{: #network-design}

Networking is a key aspect of any cloud deployment that should not be overlooked. The network design should consider enterprise connectivity, latency, throughput, resiliency, and security requirements.

For security purposes, it is recommended to isolate production from nonproduction workloads as a best practice. In addition, it's also a best practice to isolate by application tiers, for example, application versus database. {{site.data.keyword.vpc_full}} (VPC) enables the creation of logically isolated sections of the {{site.data.keyword.Bluemix_notm}}.

To provide isolation and centralized advanced security functions, the network design follows the Hub and spoke VPC model. The Edge VPC serves as the hub for which all ingress and egress traffic flows. The Edge is a virtual network (VPC) that acts as a central point of connectivity to on-premises network and all other VPCs. Workload VPCs are connected to the Edge ("Hub") by a transit gateway, which allows traffic routing between each of the VPCs in the {{site.data.keyword.Bluemix_notm}} account.

Enterprise connectivity is needed to connect the SAP environment to the client data centers. {{site.data.keyword.Bluemix_notm}} Direct Link is typically used for this connectivity and if redundancy is needed, two direct links can be used in a resilient design.

A separate management VPC (not illustrated) can be deployed into multiple regions to host management infrastructure and services that are also connected to the Edge and workload VPCs through transit gateway.

For a list of the networking considerations, see [Networking design considerations](/docs/sap?topic=sap-networking-design-considerations).
