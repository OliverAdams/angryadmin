# Installing The Log Analytics Agent

## Where to download the agent

  Go to your log analytics workspace and copy the workspace ID and key from the agent configuration node

## Firewall ports and urls

  Agent Resource	Ports	Direction	Bypass HTTPS inspection
*.ods.opinsights.azure.com	Port 443	Outbound	Yes
*.oms.opinsights.azure.com	Port 443	Outbound	Yes
*.blob.core.windows.net	Port 443	Outbound	Yes
*.azure-automation.net	Port 443	Outbound	Yes

## Log Analytics Gateway

  You can also install the log analyitics gateway if you have machines/servers without direct internet access.

## The Install Process

Except for two parts the install is next, next finish.

You will be asked to enter your workspace id and key. These you copied from your log analytics workspace in the first step.



## Post Install Checks

Open your log analytics workspace, go to agent management and check the device count is now one

Next we will start to select which log files we want to ingest into our workspace.
