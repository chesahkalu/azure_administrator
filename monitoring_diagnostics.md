# Azure Monitoring and Diagnostics

---

## Table of Contents


- [Azure Monitoring and Diagnostics](#azure-monitoring-and-diagnostics)
  - [Table of Contents](#table-of-contents)
  - [Pre-Requisites](#pre-requisites)
  - [Introduction](#introduction)
  - [Azure Monitor](#azure-monitor)
  - [Azure Log Analytics](#azure-log-analytics)
  - [Monitor Alerts](#monitor-alerts)

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

    - **`Logs`** contain different kinds of data organized into records with different sets of properties for each type. Data like events and traces are stored as logs along with performance data so all the data can be combined for analysis. Azure Monitor doesn't collect logs by default, but you can configure Azure Monitor Logs to collect from any Azure resource.
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

---

### Log Analytics

- Log Analytics is a tool in Azure Monitor that allows you to edit and run log queries for data collected in Azure Monitor Logs. It offers query features and tools, supports the `Kusto Query Language (KQL)`, and allows for detailed analysis and problem-solving.

- You can use Log Analytics to edit and run log queries for the data collected in Azure Monitor Logs. Log queries help you to search for patterns and identify issues. You can create simple or complex queries with KQL, including:
    - Search and sort by value, time, property state, and more
    - Join data from multiple tables
    - Aggregate large sets of data
    - Perform intricate operations with minimal code
    - Configure your saved log searches to run automatically.
    - Add visualizations for your saved log searches to see graphical views of your environment health.

- **Log Analytics Workspace** is a unique environment for storing and analyzing data. It is a container where you can collect data from multiple sources, query that data, and create visualizations. You can have multiple workspaces in a single Azure subscription. 
    - You can use the Azure portal to create and manage your Log Analytics workspace.
    - After you create your workspace, you configure your data sources and solutions to store their data in your workspace.
    - Note that not all `regions` support all features of Log Analytics. If you are unable to create a workspace in your desired region, you may need to search and choose a different region that supports the features you need.
    - The default `pricing` tier for a new workspace is pay-as-you-go. Charges incur only after you start collecting data.

- **Query Editor** is a tool in the Azure portal that allows you to interactively query your log data. You can use the query editor to write and run queries, visualize results, and save queries for later use. 
    - Administrators build Log Analytics queries from data stored in dedicated `tables` in the Log Analytics workspace. Some common dedicated tables include `Event`, `Syslog`, `Heartbeat`, and `Alert`. When you build a Kusto Query Language (KQL) query, you begin by determining which tables in the Azure Monitor Logs repository have the data you're looking for.
    - Documentation for each data source and solution includes the name of the data type that it creates and a description of each of its properties.
    - The basic structure of a query is a source table followed by a series of commands (referred to as `operators`).
    - A query can have a chain of multiple operators to refine your data and perform advanced functions.
    - Each operator in a query chain begins with a pipe character `|`.
    - Many queries require data from a single table only, but other queries can use various options and include data from multiple tables.

- **Tables** are the primary data structures in Log Analytics. Each table contains a set of records with fields that describe the data. You can query tables to retrieve data and perform operations on the data. 
    - Each table has a schema that defines the fields and data types for the records in the table.
    - You can use the `schema` to understand the data in the table and to write queries that retrieve the data you need.
    - The schema for a table is defined by the data source that writes data to the table. The schema is fixed and cannot be changed by users.
    - The schema for a table is documented in the Azure Monitor Logs data reference. 
    - The columns in a table are called `fields`. Each field has a name and a data type. The data type defines the kind of data that can be stored in the field.
    eg, type, event, duration, start, time, etc.

- **Examples of Log Analytics Queries**:
    - Query to retrieve all records from the `Heartbeat` table:
        ```sql
        Heartbeat
        ```
    - Query to retrieve all records from the `Heartbeat` table where the `Computer` field is equal to `Server01`:
        ```sql
        Heartbeat | where Computer == "Server01"
        ```
    - Query to retrieve all records from the `Heartbeat` table where the `Computer` field is equal to `Server01` and the `TimeGenerated` field is greater than `2022-01-01T00:00:00Z`:
        ```sql
        Heartbeat | where Computer == "Server01" and TimeGenerated > datetime(2022-01-01T00:00:00Z)
        ```
    - Query to return the first three data records from the `Stormevent` table, ordered by the `event severity duration`:
        ```sql
       StormEvent | top 3 by event severity duration
        ```
    -  The following example retrieves the most recent heartbeat record for each computer. The computer is identified by its `IP address`. In this example, the summarize aggregation with the `arg_max` function returns the record with the most recent value for each IP address.
        ```sql
        Heartbeat
        | summarize arg_max(TimeGenerated, *) by ComputerIP
        ```
    - The following example retrieves the average `CPU `usage for each computer in the `Heartbeat` table. The summarize aggregation with the `avg` function calculates the average CPU usage for each computer.
        ```sql
        Heartbeat
        | summarize avg(CPU_s) by Computer
        ```
    - The data for an event table, stored in rows, is filtered by the value of the `StartTime` column. The data is filtered further by the value of the `State` column. The query then returns the `count` of the resulting rows.
        ```sql
        Events
        | where StartTime >= datetime(2018-11-01) and StartTime < datetime(2018-12-01)
        | where State == "FLORIDA"  
        | count
        ```

---

### Monitor Alerts

Azure Monitor Alerts provide a way to get notified when issues occur. You can create alerts programmatically or through the Azure portal. Alerts can be based on metrics, logs, or activity log events. You can configure alerts to notify you by email, SMS, or webhook. You can also configure alerts to trigger an action group, which can run a logic app, a function, or an automation runbook.

- `Metric alerts` provide an alert trigger when a specified `threshold` is exceeded. For example, a metric alert can notify you when CPU usage is greater than 95 percent.
- `Activity log alerts` notify you when Azure resources change state. For example, an activity log alert can notify you when a resource is deleted.
- `Log alerts` are based on things written to log files. For example, a log alert can notify you when a web server has returned a number of 404 or 500 responses.
 
**Alert Rule** is a configuration that defines the conditions under which an alert is created. The rule specifies the target resource, the condition, and the action to take when the condition is met. The composition of an alert rule includes:
- **Resource**: The resource to monitor. Various resources can be assigned a single alert rule.
- **Condition**: The condition that triggers the alert. The signal type can be a metric, an activity log, or logs
- **Action**: The action to take when the alert is triggered, like sending an email, sending an SMS message, or using a webhook.
- **Alert Details**: The details of the alert, such as the severity and the alert rule name. `5` severity levels are available:
    - `Sev 0`: Critical
    - `Sev 1`: Error
    - `Sev 2`: Warning
    - `Sev 3`: Informational
    - `Sev 4`: Verbose

**Alert Condition** is the condition that triggers the alert. The condition can be a metric, an activity log, or logs. The condition can be a single condition or a combination of conditions. The condition can be a simple comparison, a complex comparison, or a combination of comparisons.

- `Metric Alerts`: You must define the type of statistical analysis to be used with either `static` or `dynamic` metric alerts. Example types are minimum, maximum, average, and total. In an example, you define the `period` of data to be assessed: the last 10 minutes. Finally, you set the `frequency` by which the alert conditions are checked: every two minutes.
    - `Static` : static alert with a threshold of 85 percent CPU utilization checks the rule every two minutes. It evaluates the last 10 minutes of CPU utilization data to assess if it rises above the threshold. If the evaluation is true, the alert triggers the actions associated with the action group.
    - `Dynamic` : Uses a machine learning algorithm to determine the threshold. Using a `look-back` period of example 3, will be `10 minutes * 3 = 30 minutes`. Then `number 0f violation` set to `2`expresses how many times the logic condition has to deviate from the expected behavior before the alert rule fires a notification.

    - Wth `Dimension` you can supply multiple data from different instances of the same resource. For example, you can monitor the CPU utilization of all virtual machines in a resource group.

- `Log Alerts`: You can create an alert rule for a specific condition or for a set of conditions. Log alerts use log data to assess the rule logic and, if necessary, trigger an alert. This data can come from any Azure resource: server logs, application server logs, or application logs. `By its nature, log data is historical, so usage is focused on analytics and trends`. The first part of a log alert defines the log search rule. The rule defines how often it should run, the time period under evaluation, and the query to be run. When a log search evaluates as positive, it creates an alert record and triggers any associated actions. The composition of a log alert includes:
    - `Log Query`: Query that runs every time the alert rule fires.
    - `Time Period`: The time period over which the log query runs.
    - `Frequency`: How often the log query runs.
    - `Threshold`: The threshold that triggers the alert.

- `Activity Log Alerts`: Activity log alerts allow you to be notified when a specific event happens on some Azure resource. For example, you can be notified when someone creates a new VM in a subscription. The first part of an activity log alert defines the activity log rule. The rule defines the event type, the resource group, and the subscription to monitor. When the rule evaluates as positive, it creates an alert record and triggers any associated actions. Two types of activity log alerts are available:
    - **Service Health**: Alerts you when there is a service health event.  Include notice of incidents and maintenance of target resources.
    - **Specific Operations**: Alerts you when a specific operation is performed on a target resource. For example, you can be alerted when a VM is created or deleted.
The composition of an activity log alert includes:
    `Category`: Administrative, service health, autoscale, policy, or recommendation
    `Scope`: Resource level, resource group level, or subscription level
    `Resource group`: Where the alert rule is saved
    `Resource type`: Namespace for the target of the alert
    `Operation name`: Operation name
    `Level`: Verbose, informational, warning, error, or critical
    `Status`: Started, failed, or succeeded
    `Event initiated by`: Email address or Microsoft Entra identifier (known as the "caller") for the user

- `Service Health Alerts`: 
    - Service health alerts aren't like all the other alert types you've seen so far in this module.
    - The only difference is that you no longer need to select a resource, because the alert is for a whole region in Azure. 
    - What you can select is the kind of health event on which you want to be alerted. 
    - You can select service issues, planned maintenance, health advisories, or choose all of the events. 
    - The remaining steps of performing actions and naming the alerts are the same.

- `Action Group`: An action group is a collection of notification preferences defined by the user. The action group can be used across multiple alert rules. The action group defines the actions to take when an alert is triggered. You can run one or more actions for each triggered alert. Azure Monitor can perform any of the following actions:
    - Send an email to a group of people
    - Send a text message to a mobile phone
    - Call or send a notification to a webhook
    - Create an Azure app push notification
    - Make a voice call to a number
    - Call an Azure function
    - Trigger a logic app
    - Create an ITSM ticket
    - Use a runbook (to restart a VM or scale a VM up or down)

**Alert Processing Rule** is a rule that defines how alerts are processed. The rule specifies the target resource, the condition, and the action to take when the condition is met. Use alert processing rules to override the normal behavior of a fired alert by adding or suppressing an action group. You can use alert processing rules to add action groups or remove (suppress) action groups from your fired alerts. Alert processing rules are different from `alert rules`. Alert rules trigger alerts when a condition is met in your monitored resources. Alert processing rules modify the alerts as they're being fired.

---

## VM Monitoring and Diagnostics

- Azure Monitor `Metrics` automatically monitors a predefined set of metrics for every Azure VM, and retains the data for 93 days with some exceptions.
- You can use Azure Monitor `Logs` to collect data from the VMs and analyze it.

**Monitoring Layers**: Azure VMs have several layers that require monitoring. Each of the following layers has a distinct set of telemetry and monitoring requirements.
- **Host VM**: The physical or virtual machine that hosts the VM. Monitoring the host layer is essential for understanding the health and performance of the VM. It includes monitoring the CPU, memory, disk, and network usage of the host VM.
- **Guest Operating System**
- **Client Workload**
- **Application**

VM client monitoring can include monitoring the operating system (OS), workloads, and applications that run on the VM. To collect metrics and logs from guest OS and client workloads and applications, you need to install Azure Monitor Agent and set up a `data collection rule (DCR)`.

DCRs define what data to collect and where to send that data. You can use a DCR to send Azure Monitor metrics data, or performance counters, to Azure Monitor Logs or Azure Monitor Metrics. Or, you can send event log data to Azure Monitor Logs. `In other words, Azure Monitor Metrics can store only metrics data, but Azure Monitor Logs can store both metrics and event logs`.

### Create a VM and enable recommended alerts

1. Sign in to the Azure portal, and in the Search field, enter `virtual machines`.

2. On the Virtual machines page, select `Create`, and then select Azure virtual machine.

3. On the Basics tab of the `Create a virtual machine` page:

    - In the `Subscription` field, select the correct subscription if not already selected.
    - Under `Resource group`:
        1. Select `Create new`.
        2. Under `Name`, enter `learn-monitor-vm-rg`.
        3. Select `OK`.
    - For Virtual machine name, enter monitored-linux-vm.
    - For Image, select Ubuntu Server 20.04 LTS - x64 Gen2.

4. Leave the other settings at their current values, and select the `Monitoring tab`.

5. On the Monitoring tab, select the checkbox next to `Enable recommended alert rules`.

6. On the `Set up recommended alert rules` screen:

    - Select all the listed alert rules if not already selected, and adjust the values if desired.
    - Under `Notify me by`, select the checkbox next to `Email`, and enter an email address to receive alert notifications.
    - Select `Save`.
7. Under `Diagnostics`, for `Boot diagnostics`, ensure that `Enable with managed storage account (recommended)` is selected.

8. Select `Review + create`, and then select `Create`.

9. On the `Generate new key pair` popup dialog box, select `Download private key and create resource`.

It can take a few minutes to create the VM. When you get the notification that the VM is created, select `Go to resource` to see basic metrics data.

### View built-in metrics graphs

Once your VM is created, Azure starts collecting basic metrics data automatically. Built-in metrics graphs, along with the recommended alerts you enabled, can help you monitor whether and when your VM encounters health or performance issues. You can then use more advanced monitoring and analytics capabilities to investigate issue causes and remediation.

1. To view basic metrics graphs, on the VM's `Overview` page, select the `Monitoring tab`.

2. Under `Performance and utilization` > `Platform metrics`, review the following metrics graphs related to the VM's performance and utilization. Select `Show more` metrics if all the graphs don't appear immediately.

    - VM Availability
    - CPU (average)
    - Disk bytes (total)
    - Network (total)
    - Disk operations/sec (average)

3. Under Guest OS metrics, notice that guest OS metrics aren't being collected yet. This is because you haven't set up a data collection rule to collect guest OS metrics.

4. **You can view the VM's activity log by selecting `Activity log` from the VM's left `navigation` menu. You can also retrieve entries by using PowerShell or the Azure CLI.**

5. **You can view boot diagnostics by selecting `Boot diagnostics` from the VM's left navigation menu under `Help`.**


### Metric Explorer

- **Metric Explorer** is a tool in the Azure portal that allows you to view and analyze metrics data collected by Azure Monitor. If the built-in metrics charts for a VM don't already show the data you need, You can use Metric Explorer to create and customize charts that show metrics data for your Azure resources. You can also use Metric Explorer to pin charts to dashboards for easy access. To open Metrics Explorer, you can:

    - Select `Metrics` from the VM's left navigation menu under `Monitoring`.
    - Select the `See all Metrics` link next to `Platform metrics` on the `Monitoring` tab of the VM's `Overview` page.
    - Select `Metrics` from the left navigation menu on the Azure Monitor `Overview` page.

In Metrics Explorer, you can select the following values from the dropdown fields:
    - `Scope`: If you open Metrics Explorer from a VM, this field is prepopulated with the VM name. You can add more items with the same resource type (VMs) and location.
    - `Metric Namespace`: Most resource types have only one namespace, but for some types, you must pick a namespace. For example, storage accounts have separate namespaces for files, tables, blobs, and queues.
    - `Metric`: Each metrics namespace has many metrics available to choose from.
    - `Aggregation`: For each metric, Metrics Explorer applies a default aggregation. You can use a different aggregation to get different information about the metric.

You can apply the following aggregation functions to metrics:
    - `Count`: Counts the number of data points.
    - `Average (Avg)`: Calculates the arithmetic mean of values.
    - `Maximum (Max)`: Identifies the highest value.
    - `Minimum (Min)`: Identifies the lowest value.
    - `Sum`: Adds up all the values.

You can select flexible time ranges for graphs from the past 30 minutes to the last 30 days, or custom ranges. You can specify time interval granularity from one minute to one month.

**Creating a custom chart in Metric Explorer**:

To create a Metrics Explorer graph that shows host VM maximum percentage CPU and inbound flows together for the past 30 minutes:

1. Open `Metrics Explorer` by selecting `See all Metrics` on the VM's `Monitoring` tab or selecting `Metrics` from the VM's left navigation menu.

2. `Scope` and `Metric Namespace` are already **populated** for the host VM. Select `Percentage CPU` from the `Metrics` dropdown list.

3. `Aggregation` is automatically **populated** with Avg, but change it to `Max`.

4. Select `Add` metric at upper left.

5. Under `Metric`, select `Inbound Flows`. Leave `Aggregation` at `Avg`.

6. At upper right, select `Local Time: Last 24 hours (Automatic - 15 minutes)`, change it to `Last 30 minutes`, and select `Apply`.

### VM Insights

- Besides monitoring your VM host's health, utilization, and performance, you need to monitor the `software` and `processes` running on your VM, which are called the VM `guest` or `client`. Azure Monitor provides a solution called `VM Insights` that helps you monitor the guest OS and applications running on your VM. VM Insights collects and analyzes guest OS and application performance data, and provides insights into the performance and health of your VM.

- To monitor the software running on your VM, you install the **`Azure Monitor Agent`**, which collects data from inside the VM. VM insights:





---

## References and Further Reading

- [Azure Monitor Documentation](https://learn.microsoft.com/en-us/azure/azure-monitor/)
- [Interactive Labs on Implementing Azure Monitor](https://learn.microsoft.com/en-us/training/modules/configure-azure-monitor/8-simulation-monitor)
- [Analyze monitoring data with Kusto Query Language](https://learn.microsoft.com/en-us/training/paths/analyze-monitoring-data-with-kql/)