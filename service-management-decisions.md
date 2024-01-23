---

copyright:
  years: 2023
lastupdated: "2023-12-26"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for service management
{: #service management}

Typically, Service management tools are integrated with a centralized Service Management SOC/Ticketing System to provide a single pane of glass for all operations activities.

|Architecture decision|Requirement|Decision|Rationale|
|---|---|---|---|
| Monitoring (Application)    |Provide Integration, Exception, Health and System Monitoring                                                                                 |SAP App: SAP FRUN (part of SAP Digital Ops Suite)                                                              |- Provides templates for monitoring of technical systems including their instances, databases and hosts. \n- Displays the status of managed objects and detailed drill down to each single metric or event. Shows the history of each metric in the Metric Monitor. \n- Automatic alert generation when thresholds are violated.|
 | | |Instana                                                                                                        |Instana provides additional application performance metrics and automate application performance management for the Web, App, and Database tiers.  Provides data and actionable insights to monitor the applications and automate root-cause analysis. |
| Monitoring Cloud (Platform) | Monitor and correlate performance metrics and events                                                                                         | Infrastructure: Instana, LogDNA, [IBM Cloud Monitoring](/docs/monitoring?topic=monitoring-about-monitor)                                                                                | -   A fully-automated application performance management (APM) solution \n -   Automates root-cause analysis by using event correlation, performance thresholds, errors, changes, and analysis of service level agreement (SLA) violations. \n -   Provides full context across the application infrastructure supporting all physical, virtual, and serverless services and functions \n  -   Provides data and actionable insights to monitor the applications, understand and respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health.                                                    |
| Logging                     |Diagnose issues, analyze stack traces and exceptions, identify the source of errors, and monitor different log sources through a single view| [IBM Log Analysis](/docs/log-analysis?topic=log-analysis-getting-started)                 | Recommended tool for infra Logging for any non-VMWare workloads. Ingestion and integration with other tools for diagnosis and alerts|
| Alerting                    |Provide tracking and alerting functions across application and infrastructure.|- [IBM Cloud Activity Tracker with LogDNA](/docs/activity-tracker?topic=activity-tracker-getting-started) \n - Pager Duty + ServiceNow (SNOW) + Customer SIEM \n - Instana|Full stack observability for application and infrastructure| IBM Cloud Activity Tracker provides interfaces to capture, store, view, search, and monitor API activity and supports the configuration of alerts to send notifications on one or more target channels
|Management/Orchestration|Automate management processes to keep applications and infrastructure secure, up to date, and available|Ansible and Terraform| |
{: caption="Table 1. Architecture decisions for service management" caption-side="bottom"}
