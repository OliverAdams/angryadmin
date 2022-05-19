# We have to start somewhere

To create the dashboard requires knowledge of many different areas and tools which I will go over first.

Teams Room Agent </br>
Microsoft Teams Room Event Log </br>
Microsoft Monitoring Agent </br>
Azure Log Analytics Workspaces </br>
Kusto Query Language </br>
Azure Workbooks </br>
Azure Dashboards </br>
Additional but not required </br>
  Power BI </br>
  Grafana </br>
  Azure Managed Grafana </br>

In this series of articles we will go through these areas step by step. If you are already comfortable with these I am hoping to release a quick guide for faster reading.

I will start by creating a log analytics workspace after which I will take you through connecting your teams rooms devices to this workspace using the Microsoft monitoring agent.

Once these are connected I will go through how to shape and filter this data to create a base for the dashboard.

Once we have the data we can start to create some workbooks so display the data in a better way.

Finally we will create an Azure dashboard and add our previously created workbooks and share the dashboard.

![agent-connected](/docs/images/agent-connected.PNG)
