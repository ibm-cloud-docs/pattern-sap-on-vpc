---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-25"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for security
{: #security-decisions}

The following are security architecture decisions for the SAP on VPC pattern.

## Architecture decisions for storage

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Primary Storage                         | Ability to encrypt data at rest                                                                                                     | [Block Storage encryption](/docs/vpc?topic=vpc-mng-data&interface=ui) with provider keys                                    | * Industry-Standard AES-256 encryption \n * Block Storage for VPC volumes are double-encrypted at rest. The double-encryptions includes the underlying volume that holds customer volumes                                                                                                                                                                                                                                                                                 |
| Backup storage and archive storage        | Ability to encrypt backups                                                                                                          | Cloud Object Storage Encryption                                                                                                                  | By default, all objects that are stored in {{site.data.keyword.cos_full_notm}} are encrypted by using randomly generated keys and an all-or-nothing-transform (AONT). |
{: caption="Table 1. Architecture decisions for storage" caption-side="bottom"}

## Architecture decisions for data encryption

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| HANA Data Encryption                    | Ability to encrypt SAP HANA data at rest                                                                                            | HANA Data Volume Encryption (DVE)                                                                                                                | DVE encrypts HANA data at the persistence layer, protecting data stored on disk from unauthorized access at the operating system level.                                                                                                                                                                                       |
| Data: Encryption in transit            | Ability to encrypt data while in transit, to servers and between servers | FTPs and HTTPs protocols (client to server) \n IPsec and X.509 certificates (file to server)                                                                                                      | [Enable secure end-to-end encryption](/docs/vpc?topic=vpc-file-storage-vpc-eit) of your data when you use file shares with security-group-based access control mode and mount targets with virtual network interfaces. Encryption in transit is not supported on {{site.data.keyword.bm_is_short}}.|
{: caption="Table 2. Architecture decisions for encryption" caption-side="bottom"}

## Architecture decisions for identity and access management

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Identity Access & Role Management (IDM) | Securely authenticate users for platform services and control access to resources consistently across {{site.data.keyword.Bluemix_notm}}                     | {{site.data.keyword.Bluemix_notm}} IAM                                                                                                                                    | Use IAM access policies to assign users, service IDs, and trusted profiles access to resources within the {{site.data.keyword.Bluemix_notm}} account.                                                                                                                                                                                              |
| Privileged Identity and Access Management | Privileged access management services for administrative purposes                                                                   | * Bring your own bastion host (or Privileged Access Gateway) with Privledge Management Access (PAM) software deployed in Edge VPC \n * 2FA Authentication though {{site.data.keyword.IBM}} Security Verify                                                            | Securely access remote resources over the private network for management purposes; bastion accessed by SSH. Session recording, tracking all activities that are successful or not, to note any potential threats |
{: caption="Table 1. Architecture decisions for access management" caption-side="bottom"}

## Architecture decisions for network protection
{: #network-protection-sd}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Core Network Protection                 | * Strict separation of duties \n * Isolated security zones between environments \n * Isolated, private cloud environment                                                                                                    | Separate VPCs, Subnets, ACLs, and Security Groups separating application from DB and production and nonproduction environments.                         | A design combination that uses: \n Separate VPCs (transit, management, workload) connected through transit gateway and, the use of edge firewall capabilities. Subnets, security groups, and ACLs to create an edge and transit VPC design. |
{: caption="Table 1. Architecture decisions for network protection" caption-side="bottom"}

## Architecture decisions for threat detection and response
{: #threat-protection-sd}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Threat detection and response | * Boundary protection: The highest level of isolation from external network threats \n * Intrusion Prevention Services (IPS) and Intrusion Detection Services (IDS) at all ingress and egress \n * Unified Threat Management (UTM) Firewall | Bring your own virtual firewall (on VSI) in Edge VPC (deployed across availability zones) client choices: \n [Fortigate](https://cloud.ibm.com/catalog/content/ibm-fortigate-AP-HA-terraform-deploy-5dd3e4ba-c94b-43ab-b416-c1c313479cec-global) {: external}  \n [Palo Alto](https://cloud.ibm.com/catalog/content/ibmcloud-vmseries-1.9-6470816d-562d-4627-86a5-fe3ad4e94b30-global) {: external}  |Can be provided by Enterprise Network DMZ \n In addition, if client requires: \n * Virtual FW on VSI in the Transit/Edge VPC \n * Client preference. The recommendation is Fortigate or Juniper \n * Fortigate supports native HA configuration \n * Fortigate and Juniper both support IPS and IDS|
{: caption="Table 1. Architecture decisions for threat detection" caption-side="bottom"}
