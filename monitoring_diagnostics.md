# Azure Monitoring and Diagnostics

---

## Table of Contents


- [Azure Monitoring and Diagnostics](#azure-monitoring-and-diagnostics)
  - [Table of Contents](#table-of-contents)
  - [Pre-Requisites](#pre-requisites)
  - [Introduction](#introduction)
  - [Azure Monitor](#azure-monitor)
  - [Azure Application Insights](#azure-application-insights)
    - [Azure Application Insights Overview](#azure-application-insights-overview)
    - [Azure Application Insights Metrics](#azure-application-insights-metrics)
    - [Azure Application Insights Logs](#azure-application-insights-logs)
    - [Azure Application Insights Alerts](#azure-application-insights-alerts)
    - [Azure Application Insights Workbooks](#azure-application-insights-workbooks)
  - [Azure Log Analytics](#azure-log-analytics)
    - [Azure Log Analytics Overview](#azure-log-analytics-overview)
    - [Azure Log Analytics Metrics](#azure-log-analytics-metrics)
    - [Azure Log Analytics Logs](#azure-log-analytics-logs)
    - [Azure Log Analytics Alerts](#azure-log-analytics-alerts)
    - [Azure Log Analytics Workbooks](#azure-log-analytics-workbooks)
  - [Azure Diagnostic Logs](#azure-diagnostic-logs)
    - [Azure Diagnostic Logs Overview](#azure-diagnostic-logs-overview)
    - [Azure Diagnostic Logs Metrics](#azure-diagnostic-logs-metrics)
    - [Azure Diagnostic Logs Logs](#azure-diagnostic-logs-logs)
    - [Azure Diagnostic Logs Alerts](#azure-diagnostic-logs-alerts)
    - [Azure Diagnostic Logs Workbooks](#azure-diagnostic-logs-workbooks)
  - [Azure Monitor vs Azure Application Insights vs Azure Log Analytics vs Azure Diagnostic Logs](#azure-monitor-vs-azure-application-insights-vs-azure-log-analytics-vs-azure-diagnostic-logs)
  - [Azure Monitor vs Azure Application Insights vs Azure Log Analytics vs Azure Diagnostic Logs](#azure-monitor-vs-azure-application-insights-vs-azure-log-analytics-vs-azure-diagnostic-logs-1)
  - [Azure Monitor vs Azure Application Insights vs Azure Log Analytics vs Azure Diagnostic Logs](#azure-monitor)

---

## Pre-Requisites

- Knowledge of Azure resources and services that benefit from monitoring activities.
- Knowledge of the Azure portal so you can implement monitoring techniques.
- Familiarity with basic monitoring, evaluation, and reporting concepts.
- An Azure account with an active subscription (Free tier is enough). Sign up or login to your Azure account [here](https://azure.microsoft.com/en-us/free/)

---

## Introduction

Azure Monitor is a platform service that provides a single source that can monitor both Azure and on-premise resources. It provides a comprehensive solution for collecting, analyzing, and acting on telemetry from your cloud and on-premises environments. Azure Monitor helps you understand how your applications are performing and proactively identifies issues affecting them and the resources they depend on.

---

## Azure Monitor

- Various monitoring sources provide Azure Monitor with the metrics and logs data to analyze. These sources can include your `Azure subscription` and `tenant`,  your `Azure resources`, data from your `applications`, data about the `Operating system`, `your Azure service instances`, and more.

- Data stores in Azure Monitor hold your metrics and logs.  `Azure Monitor Metrics` and`Azure Monitor Logs` are the two base types of data used by the service.
    - **`Metrics`** are numerical values that describe some aspect of a system at a particular point in time. Metrics are lightweight and capable of supporting near real-time scenarios.
        - For many Azure resources, the metrics data collected by Azure Monitor is displayed on the `Overview page` for the resource in the Azure portal.
        - You can use Azure Monitor metrics explorer to view the metrics for your Azure services and resources.
        - In the Azure portal, select any `graph` for a resource to open the associated metrics data in metrics explorer. The tool lets you `chart` the `values` of multiple metrics over `time`. You can work with the charts interactively or pin them to a dashboard to view them with other visualizations.

    - **`Logs`** contain different kinds of data organized into records with different sets of properties for each type. Data like events and traces are stored as logs along with performance data so all the data can be combined for analysis.
        - In the Azure portal, log data collected by Azure Monitor is stored in `Log Analytics`.
        - Log Analytics includes a rich `query language` to help you quickly retrieve, consolidate, and analyze your collected data.
        - You can use the `Log Analytics query editor` in the Azure portal to interactively query your log data. 
            - The query editor provides a rich set of tools to help you write queries, visualize results, and save queries for later use.
            - You can use the `Log Analytics query language` to retrieve and analyze your log data. The query language is designed to be simple and easy to learn, but also powerful enough to write complex queries.

- `Azure Monitor Insights` performs different functions with the collected data, including analysis, alerting, and streaming to external systems. It also provides a platform for building custom monitoring solutions.

- `Azure Application Insights` is an extensible Application Performance Management (APM) service for web developers on multiple platforms. It provides a way to monitor your live web application. It will automatically detect performance anomalies and includes powerful analytics tools to help you diagnose issues and understand what users actually do with your app.

- `Azure Monitor Alerts` provide a way to get notified when issues occur. You can create alerts programmatically or through the Azure portal.

- `Azure Monitor Workbooks` provide a way to visualize your data in a variety of ways, including tables, charts, and more.
- `Activity Log` is a platform log that provides insight into subscription-level events that have occurred in Azure. This log is automatically created for each Azure subscription and cannot be disabled. 
    - Activity logs can help you determine the "what, who, and when" for any write operation (PUT, POST, DELETE) performed on resources in your subscription.
    - Activity logs are kept for 90 days.
    - In the Azure portal, you can filter your Azure Monitor activity logs so you can view specific information. The filters enable you to review only the activity log data that meets your criteria.


### Log Analytics

- Log Analytics is a tool in Azure Monitor that allows you to edit and run log queries for data collected in Azure Monitor Logs. It offers query features and tools, supports the `Kusto Query Language (KQL)`, and allows for detailed analysis and problem-solving.

- You can use Log Analytics to edit and run log queries for the data collected in Azure Monitor Logs. Log queries help you to search for patterns and identify issues. You can create simple or complex queries with KQL, including:
    - Search and sort by value, time, property state, and more
    - Join data from multiple tables
    - Aggregate large sets of data
    - Perform intricate operations with minimal code
- **Log Analytics Workspace** is a unique environment for storing and analyzing data. It is a container where you can collect data from multiple sources, query that data, and create visualizations. You can have multiple workspaces in a single Azure subscription. 
    - You can use the Azure portal to create and manage your Log Analytics workspace.
    - After you create your workspace, you configure your data sources and solutions to store their data in your workspace.
    - Note that not all `regions` support all features of Log Analytics. If you are unable to create a workspace in your desired region, you may need to search and choose a different region that supports the features you need.
    - The default `pricing` tier for a new workspace is pay-as-you-go. Charges incur only after you start collecting data.



- [Azure Monitor Documentation](https://learn.microsoft.com/en-us/azure/azure-monitor/)
- [Interactive Labs on Implementing Azure Monitor](https://learn.microsoft.com/en-us/training/modules/configure-azure-monitor/8-simulation-monitor)