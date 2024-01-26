---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-25"

subcollection: pattern-sap-on-vpc
keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for network
{: #network-decisions}

The following table summarizes the networking architecture decisions for the SAP on VPC pattern.

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Connectivity from cloud to enterprise         | Connectivity that is needed between client and {{site.data.keyword.Bluemix_short}}                                                                           | Redundant Direct Link Connect Connections                                        | Preferred depending on security requirements. Lower cost than Direct Link Dedicated                                                                                                              |
| Connectivity from Managed Service Providers   | Secure, encrypted connectivity between MSPs and {{site.data.keyword.Bluemix_short}}                                                                  | P2P VPN through VPC VPN Gateway                                                  | [VPN Gateway](/docs/vpc?topic=vpc-using-vpn) - securely connect Virtual Private Cloud (VPC) to another private network (site-to-site) for management purposes. \n A VPN gateway consists of two back-end instances for high availability in the same zone.      |
| Bring Your Own IP(BYOIP) and Edge Gateway                            | Capability needed for customers to provide isolation, security, and edge routing services                                    |{{site.data.keyword.vpc_full}} facilitates Bring Your Own IP(BYOIP) \n Edge Gateways: Palo Alto, Fortinet, F5 with the client choice based on requirements                                             | Client can [bring their own subnet](/docs/vpc?topic=vpc-configuring-address-prefixes) IP address range to an {{site.data.keyword.vpc_full}} \n Edge Gateway is client choice based on the requirements                                        |
| Network segmentation and isolation                | Ability to provide network isolation across workloads                                                                      | VPCs and subnets                                                                 | Native VPC isolation by using separate VPCs and subnets for production, nonproduction environments, and separation of workload                                                              |
| Cloud Native Connectivity (to cloud services) | Ability to connect to cloud services over the private network                                                              | Virtual Private Endpoints                                                        | Communicate with {{site.data.keyword.Bluemix_short}} services over the private network by using a virtual private endpoint (VPE)                                                                                     |
| Cloud landing-zone connectivity VPC to VPC                | Connect across multiple VPCs to {{site.data.keyword.Bluemix_short}} classic environments                                                             | Transit gateway \n Global transit gateway                                                                  | Use a transit gateway to connect separate VPCs (Edge, workload) and Classic (if needed). Global transit gateway to connect to environments in other regions for resiliency and data replication purposes. |
| Load balancing (Public)                       | Load balancing over the public network and across two regions if of an outage (disaster recovery) or failover to the other region. | Cloud Internet Services (CIS)                                                    | Public load balancing for resiliency needs from SAP best practices. CIS also provides DDoS services.                                                                                  |
| Load balancing (Private)                      | Load balancing workloads across multiple workload instances over the private network                                       | SAP Web Dispatcher \n {{site.data.keyword.Bluemix_short}} Application Load Balancer (ALB)                                                              | SAP Web Dispatcher forwards incoming HTTP and HTTPS requests to SAP application. \n The ALB loads balance inter-application server requests across hosts. The ALB is a floating IP with multiple subnets or servers that are attached to the backend pool. servers                                                                                                 |
| Domain Name System (DNS)                  | Ability to resolve DNS names on site                                                                                       | {{site.data.keyword.IBM}} continues to forward the DNS to client DNS Servers onsite          | This is the default option in the absence of a specific customer requirement to manage DNS                                                                                              |
{: caption="Table 1. Architecture decisions for network" caption-side="bottom"}
