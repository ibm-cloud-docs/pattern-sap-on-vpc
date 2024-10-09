---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-25"

subcollection: pattern-sap-on-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Architecture decisions for service management
{: #service management}

Typically, service management tools are integrated with a centralized service management SOC and ticketing system to provide a single pane of glass for all operations activities. The following sections summarize the architecture decisions for service management for the SAP on VPC pattern.

## Architecture decisions for application monitoring
{: #application-monitoring-sm}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Monitoring (Application)    |Provide integration, exception, health, and system monitoring                                                                                 |SAP App: SAP FRUN (part of SAP Digital Ops Suite)                                                              |* Provides templates for the monitoring of technical systems that include their instances, databases, and hosts. \n * Displays the status of managed objects and a detailed drill down to each single metric or event. Provides the history of each metric in the Metric Monitor. \n * Automatic alert generation when thresholds are violated.|
 | | |Instana                                                                                                        |Instana provides additional application performance metrics and automates Application Performance Management for the web, app, and database tiers. Provides the data and actionable insights to monitor the applications and automate root-cause analysis. |
{: caption="Architecture decisions for application monitoring" caption-side="bottom"}

## Architecture decisions for platform monitoring
{: #application-platform-monitoring-sm}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Monitoring Cloud (Platform) | Monitor and correlate performance metrics and events                                                                                         | Infrastructure: Instana, LogDNA, [{{site.data.keyword.Bluemix_notm}} Monitoring](/docs/monitoring?topic=monitoring-about-monitor)                                                                                | * A fully automated Application Performance Management (APM) solution \n * Automates root-cause analysis by using event correlation, performance thresholds, errors, changes, and analysis of service level agreement (SLA) violations. \n * Provides full context across the application infrastructure that supports all physical, virtual, and serverless services and functions. \n * Provides data and actionable insights to monitor the applications, understand and respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health.                                                    |
{: caption="Architecture decisions for platform monitoring" caption-side="bottom"}

## Architecture decisions for logging
{: #application-logging-sm}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Logging                     |Diagnose issues, analyze stack traces and exceptions, identify the source of errors, and monitor different log sources through a single view | [IBM Log Analysis](/docs/log-analysis?topic=log-analysis-getting-started)                 | Recommended tool for infrastructure logging for any non-VMWare workloads. Ingestion and integration with other tools for diagnosis and alerts |
{: caption="Architecture decisions for application monitoring for logging" caption-side="bottom"}

## Architecture decisions for alerting
{: #application-alerting-sm}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Alerting                    | Provide tracking and alerting functions across application and infrastructure. | * [{{site.data.keyword.Bluemix_notm}} Activity Tracker with LogDNA](/docs/activity-tracker?topic=activity-tracker-getting-started) \n * Pager Duty, ServiceNow (SNOW), and Customer SIEM \n * Instana | Full stack observability for application and infrastructure | {{site.data.keyword.Bluemix_notm}} Activity Tracker provides interfaces to capture, store, view, search, and monitor API activity and supports the configuration of alerts to send notifications on one or more target channels |
{: caption="Architecture decisions for alerting" caption-side="bottom"}

## Architecture decisions for management
{: #application-management-sm}

| Architecture decision | Requirement | Decision | Rationale |
| -------------- | -------------- | -------------- | -------------- |
| Management and orchestration | Automate management processes to keep applications and infrastructure secure, up to date, and available | Ansible and Terraform| |
{: caption="Architecture decisions for management and orchestration" caption-side="bottom"}
