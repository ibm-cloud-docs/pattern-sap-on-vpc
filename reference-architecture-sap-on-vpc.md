---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-25"

subcollection: pattern-sap-on-vpc

keywords:
# The release that the reference architecture describes

authors:
  - name: Doug Eppard

version: 1.0

deployment-url:

docs: /docs/pattern-sap-on-powervs

content-type: reference-architecture

---

{{site.data.keyword.attribute-definition-list}}

# SAP on VPC
{: #sap-on-vpc}
{: toc-content-type="reference-architecture"}
{: toc-version="1.0"}

## Architecture diagram
{: #architecture-diagram}

The SAP on VPC architecture provides a high-level summary of the pattern for an SAP single-zone, multi-region deployment on {{site.data.keyword.vpc_short}}.

The primary region supports production workloads on VPC running on either SAP-certified  {{site.data.keyword.baremetal_short}} or VSIs. The secondary region supports nonproduction and disaster recovery workloads if the customer has DR requirements. The components deployed to the Edge VPC provide security functions and resource isolation to the {{site.data.keyword.Bluemix_notm}} workloads.

![A diagram of a computer network description automatically generated](./image1.svg){: caption="Figure 1" caption-side="bottom"}

The diagram maps the flow of a computer network description that's automatically generated:

1.  Client network connectivity is accomplished through Direct Link with VPN access for MSPs.

2.  An Edge VPC is deployed which contains routing and security functions.

3.  Transit Gateway to the Workload VPC hosting the SAP application and databases.

4.  Public connectivity also routes through Cloud Internet Services (CIS) which can provide load balancing, failover, and DDoS services, then routes to the edge VPC

5.  Global Transit Gateway connecting the Workload VPC across regions to facilitate replication for DR purposes.

Figure 2 illustrates a more detailed network and component architecture for a single-zone, multi-region deployment to facilitate disaster recovery.

![A diagram of a computer network description automatically generated](./image2.svg){: caption="Figure 2" caption-side="bottom"}

1.  Two separate {{site.data.keyword.Bluemix_notm}} regions, one containing production, the other containing both nonproduction and DR.

2.  Client network connectivity is accomplished through Direct Links to each region with VPN access for managed service providers.

3.  An Edge VPC is deployed which contains routing and security functions. For security purposes, all ingress and egress traffic routes through the Edge VPC. It contains an sFTP server, Bastion host (jump), Firewalls providing advanced security functions and the SAP router and Web Dispatcher.

4.  The Edge VPC is connected to the workload VPC through a local Transit Gateway.

5.  Public connectivity routes through Cloud Internet services, which can provide load balancing, failover, and DDoS services, then routes to the edge VPC

6.  The VPC APP subnet contains SAP components that are hosted on redundant SAP certified VSIs or Bare metal that uses either local storage (BM) or shared block storage in an [SAP Scale-out](/docs/sap?topic=sap-refarch-hana-scaleout#network-layout-for-scale-out-configurations-2) environment.

7.  The VPC DB subnet hosts the SAP database, in this case HANA hosted on SAP certified VSIs or Bare metal that uses either local storage (BM) or block storage.

8.  Virtual Private endpoints are used to provide connectivity to cloud native services from each VPC

9.  Global Transit Gateway connecting the core and workload VPC across regions for data replication purposes between the two regions.

10. Multiple instances of redundant VSIs or BMs are used to provide 99.95% availability within a zone

## Design scope
{: #design-scope}

Following the [architecture framework](/docs/architecture-framework?topic=architecture-framework-taxonomy), SAP on VPC covers design considerations and architecture decisions for the following aspects and domains:

-   **Compute**: Bare Metal and Virtual infrastructure

-   **Storage**: Primary, Backup, Archive, and Migration

-   **Networking**: Enterprise Connectivity, Edge Gateways, segmentation and isolation, Cloud Native Connectivity and Load Balancing

-   **Security**: Data, Identity and Access Management, Infrastructure and Endpoint, Threat Detection and Response

-   **Resiliency**: Backup and Restore, Disaster Recovery, and High Availability

-   **Service Management**: Monitoring, Logging, Alerting, Management, and Orchestration

The architecture framework, described in [Introduction to the Architecture Framework](/docs/architecture-framework?topic=architecture-framework-intro), provides a consistent approach to design cloud solutions by addressing requirements across a pre-defined set of aspects and domains. The requirements are architectural areas that need to be considered for any enterprise solution. It can be used as a guide to make the necessary design and component choices to ensure that you have considered applicable requirements for each aspect and domain. After you have identified the requirements and domains that are in scope, you can evaluate and select the best fit for purpose components for your enterprise cloud solution.

The Figure 3 shows the domains that are covered in this solution.

![A diagram of a computer network description automatically generated](./heat-map-SAP-on-VPC.svg){: caption="Figure 3" caption-side="bottom"}

## Requirements
{: #requirements}

The following represents a baseline set of requirements, which are applicable to most clients and critical to successful SAP deployment.

| Aspects | Requirements |
| -------------- | -------------- |
| Network            | * Enterprise connectivity to customer data centers to provide access to applications from on-premises \n * Map and convert existing customer SAP Network functionality into {{site.data.keyword.Bluemix_notm}} and VPC networking services. \n * Migrate and redeploy customer IP addressing scheme within the {{site.data.keyword.Bluemix_notm}} environment. \n * Provide network isolation with the ability to separate applications based on attributes such as data classification, public instead of internal apps and function. |
| Security            | * Provide data encryption in transit and at rest. \n * Migrate customer Intrusion Dectection and Identity Acceess and Management Services to target {{site.data.keyword.Bluemix_notm}} environment. \n * Retain the same firewall rulesets across existing DCs. \n * Firewalls must be restrictively configured to provide advanced security features and prevent all traffic, both inbound and outbound, except that which is required, documented, and approved, and include Intrusion Protection(IPS)/Intrusion Detection(IDS) services. |
| Resiliency         | * Multi-site capability to support a disaster recovery strategy and solution that use {{site.data.keyword.Bluemix_notm}} infrastructure DR capabilities. \n * Provide backups for data retention. \n * RTO/RPO = 4 hours/15 minutes; Rollback to original environments should occur no later than specified RTOs. \n * 99.95 Availability. \n * Backups. \n * Production: Daily Full, logs per SAP product standard, 30 days retention time. \n * Non-production: Weekly full, logs per SAP product standard, 14 days retention time. |
| Service Management           | * Provide health and system monitoring with ability to monitor and correlate performance metrics and events and provide alerting across applications and infrastructure \n * Ability to diagnose issues and exceptions and identify error sources. \n * Automate management processes to keep applications and infrastructure secure, up to date, and available. |
| Other     | * Migrate SAP workloads from existing data center to {{site.data.keyword.Bluemix_notm}} VPC. \n * Customer's SAP systems and applications that are run on NetWeaver (application) and HANA (DB), AnyDB, or S/4 HANA. \n * Provide an Image Replication migration solution that minimizes disruption during cut-over. \n * Cloud infrastructure for the proposed IaaS solution must be SAP Certified. \n * {{site.data.keyword.Bluemix_notm}} IaaS is deployed to support SAP and surrounding non-SAP workloads. \n * Customer does not want to adopt [RISE](https://www.ibm.com/consulting/rise-with-sap?utm_content=SRCWW&p1=Search&p4=43700077624079785&p5=e&gclid=EAIaIQobChMIr9bRlt7LgQMVJdHCBB0cewwcEAAYASAAEgIVgfD_BwE&gclsrc=aw.ds) currently but wants to consider a Cloud deployment solution that facilitates a future RISE transformation |
{: caption="Table 1. Requirements" caption-side="bottom"}

## Components
{: #components}

| Aspects | Solution components | How the component is used |
| -------------- | -------------- | -------------- |
| Compute                            | [VPC VSIs](/docs/vpc?topic=vpc-creating-virtual-servers&interface=ui)                                                                                                                                        | NetWeaver and HANA DB                                                                    |
| Storage                            |[VPC Block Storage](/docs/vpc?topic=vpc-creating-block-storage&interface=ui)                                                                                                           | NetWeaver and HANA DB servers primary storage. Backup storage                            |
|                                    | [Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage)                                                                 | Backup and archive, application logs, operational logs, and audit logs                    |
| Networking                         | [VPC Virtual Private Network (VPN)](/docs/iaas-vpn?topic=iaas-vpn-getting-started)                                                                                                     | Remote access to manage resources in a private network                                     |
|                                    | [Virtual Private Gateway & Virtual Private Endpoint (VPE)](/docs/vpc?topic=vpc-about-vpe)                                                                                | For private network access to Cloud Services, for example Key Protect, Cloud Object Storage, and so on.                |
|                                    | [VPC Load Balancers](/docs/vpc?topic=vpc-load-balancers)                                                                                                                 | Application Load Balancing for web servers, app servers, and database servers            |
|                                    | Public Gateway                                                                                                                                                                                              | For web server access to the internet                                                    |
|                                    | [Cloud Internet Services (CIS)](/docs/cis?topic=cis-getting-started)                                                                                                                   | Public Load balancing and DDoS of web servers traffic across zones in the region         |
|                                    | [DNS Services](/docs/dns-svcs?topic=dns-svcs-about-dns-services)                                                                                                         |                                                                                          |
|                                    | [VPCs and subnets](/docs/vpc?topic=vpc-about-subnets-vpc&interface=ui)                                                                                                                 | Network Segmentation/Isolation                                                           |
|                                    | [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-about)                                                                                                                   | Connect across multiple VPCs                                                             |
|                                    | [{{site.data.keyword.Bluemix_notm}} Application Load Balancer](/docs/vpc?topic=vpc-load-balancers-about) (ALB) \n SAP Web Dispatcher                                                                                                 | Load balancing workloads across multiple workload instances over the private network     |
|Security   |[Block Storage encryption](/docs/vpc?topic=vpc-mng-data&interface=ui) with provider keys                                                                                 | Block Storage Encryption at rest                                                         |
|                                    | Cloud Object Storage Encryption                                                                                                                                                                             | Cloud Object Storage Encryption at rest                                                  |
|                                    | HANA Data Volume Encryption (DVE)                                                                                                                                                                           | HANA Database Encryption at rest                                                         |
|                                    | [IAM](/docs/account?topic=account-cloudaccess)                                                                                                                           | {{site.data.keyword.Bluemix_notm}} Identity & Access Management                                                   |
|                                    | Privileged Identity and Access Management                                                                                                                                                                   | Bring your own Bastion host (or Privileged Access Gateway) with Privledged Access Management(PAM) software deployed in Edge VPC         |
|                                    | [Bring your own Bastion Host on VPC VSI with PAM software](/docs/framework-financial-services?topic=framework-financial-services-vpc-architecture-connectivity-bastion-tutorial-teleport) | Remote access with Privileged Access Management                                          |
|                                    | [Virtual Private Clouds (VPCs), Subnets, Security Groups, ACLs](/docs/vpc?topic=vpc-getting-started)                                                                     | Core Network Protection                                                                  |
|                                    | [Cloud Internet Services (CIS)](/docs/cis?topic=cis-getting-started)                                                                                                                   | DDoS protection and Web App Firewall                                                     |
|                                    | One of the following: \n - [Fortigate](https://cloud.ibm.com/catalog/content/ibm-fortigate-AP-HA-terraform-deploy-5dd3e4ba-c94b-43ab-b416-c1c313479cec-global) \n - [Palo Alto](https://cloud.ibm.com/catalog/content/ibmcloud-vmseries-1.9-6470816d-562d-4627-86a5-fe3ad4e94b30-global)                                                    | - Intrusion Protection(IPS)/Intrusion Detection(IDS) at all ingress/egress \n- Unified Threat Management (UTM) Firewall                                            |
| Resiliency                         | HANA System Replication (HSR)                                                                                                                                                                               | Provide 99.95% availability for HANA DB                                                  |
|                                    | [Veeam](/docs/vpc?topic=vpc-about-veeam)                                                                                                                                               | Controls both the backups and restores of all VSIs or BMs. Veeam Backup & Replication 12 |
| Service Management (Observability) | [{{site.data.keyword.Bluemix_notm}} Monitoring](/docs/monitoring?topic=monitoring-about-monitor)                                                                                                                | Apps and operational monitoring                                                          |
|                                    | [IBM Log Analysis](/docs/log-analysis?topic=log-analysis-getting-started)                                                                                                              | Apps and operational logs                                                                |
{: caption="Table 2. Components" caption-side="bottom"}

The architecture framework is used to guide and determine the applicable aspects and domains for which architecture decisions need to be made. The following sections contain the considerations and architecture decisions for the aspects and domains that are in play in this solution pattern.
