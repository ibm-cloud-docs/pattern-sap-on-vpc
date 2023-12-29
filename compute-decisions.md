---

copyright:
  years: 2023
lastupdated: "2023-12-26"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for compute
{: #compute-decisions}

|**Architecture decision**|**Requirement**|**Decision**|**Rationale**|
|                        |                                                                                 |                   |                                                                                                                                                                                                                                                                                                                                                      |
|           |                                                                                 |                   |                                                                                                                                                                                                                                                                                                                                                      |
| Bare Metal (NetWeaver) | Target environment to match specific workload requirements and be SAP certified | Bare Metal on VPC | Choose bare metal on VPC for larger SAP deployments with higher SAPS processing requirements. Limited to low memory requirements. If memory is a concern, then VSIs are a better choice.                                                                                                                                                             |
| Virtual Servers (Netweaver)        | Target environment to match workload requirements and be SAP certified          | VSI on VPC        | Choose VSI's for lower costs and when deployments do not require the larger number of SAPs Bare Metal can provide. VSI profiles can satisfy larger memory requirements than BM.                                                                                                                                                                      |
| Bare Metal (HANA)             | Target environment to match workload requirements and be SAP certified          | Bare Metal on VPC | Choose bare metal on VPC for larger SAPS requirements, however for HANA there are memory limitations on the BM server profiles. If memory is a concern, then VSIs are a better choice.                                                                                                                                                               |
| Virtual Servers (HANA)        | Target environment to match workload requirements and be SAP certified          | VSI on VPC        | VPC VSIs can cover 90% of customer use cases for the HANA database service. VSIs can accommodate a high number of SAPS and much higher memory over Bare Metal. If HANA in-memory requirements cannot be met by VSI profiles, then Power Virtual Servers are the preferred choice and is covered in in the SAP on Power Virtual Server documentation. |
{: caption="Table 1. Architecture decisions for compute" caption-side="bottom"}
