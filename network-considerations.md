---

copyright:
  years: 2023
lastupdated: "2023-12-26"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Network design
{: #network-design}

Networking is a key aspect of any cloud deployment that should not be overlooked. The network design should consider enterprise connectivity, latency, throughput, resiliency, and security requirements.

For security purposes, it is recommended to isolate production from non-production workloads as a best practice. In addition, it's also a best practice to isolate by application tiers (e.g. application vs. database). IBM Virtual Private Cloud (VPC) enables the creation of logically isolated sections of the IBM Cloud.

To provide isolation and centralize advanced security functions, the network design follows "Hub and spoke" VPC model. The Edge VPC serves as the hub for which all ingress and egress traffic flows. The Edge is a virtual network (VPC) that acts as a central point of connectivity to on-premises network and all other VPCs. Workload VPCs are connected to the Edge ("Hub") via a Transit Gateway which allows traffic routing between each of the VPCs in the IBM Cloud account.

Enterprise connectivity is needed to connect the SAP environment to the client data center(s). IBM Cloud Direct Link is typically used for this connectivity and if redundancy is needed, two direct links can be used in a resilient design.

A separate Management VPC (not illustrated) can be deployed into multiple regions, to host management infrastructure and services also connected to the Edge and workload VPCs through Transit Gateway.

For a list of all Networking Considerations, see [Networking design considerations](https://cloud.ibm.com/docs/sap?topic=sap-networking-design-considerations).
