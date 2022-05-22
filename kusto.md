#What is Kusto? (KQL)

The Kusto Query Language is used to query log analytics workspaces.

This language for me is very similar to SQL in many ways.

If you are good at sql this cheatsheet from SQL to Kusto.

https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/sqlcheatsheet

Otherwise there are some great tutorials linked below to learn KQL (Kusto Query Language)

Once we have been through the basics we can go through some queries we will build our dashboard on.

This KQL query selects the number of EventID 2000 events stored for all devices and displays this in a columnchart.

```
| Event // Select From Event
| where source == "SRS-APP" and EventID == 2000 // Filter on source (logname) and EventID
| project Computers,Source // Extract just these fields
| summarize Count=count() by Computer,Source // Use summarise to create a Count column and 
| render Columnchart //Display the result as a column chart
```

Let's take this step by step

Run these one by one to see how the results are built and shaped at each step.

```
| Event // Select From Event
```

```
| Event // Select From Event
| where source == "SRS-APP" and EventID == 2000
```

```
| Event // Select From Event
| where source == "SRS-APP" and EventID == 2000 // Filter on source (logname) and EventID
| project Computers,Source // Extract just these fields
```

```
| Event // Select From Event
| where source == "SRS-APP" and EventID == 2000 
| project Computers,Source 
| summarize Count=count() by Computer,Source 
```

```
| Event // Select From Event
| where source == "SRS-APP" and EventID == 2000 
| project Computers,Source 
| summarize Count=count() by Computer,Source 
| render Columnchart 
```

