# Installing The Log Analytics Agent


## Requirements

The Agent
The Firewall Rules (if needed)
Workspace ID and Key
About 15 minutes

## Where to find it

    Resource group - Log Analytics Workspace - Agent Management - Download Agent

## Firewall rules and the log analytics gateway

The Microsoft rules
https://github.com/OliverAdams/angryadmin/blob/gh-pages/docs/images/FirewallRequirements.PNG

The login.microsoft.com additions


## Log Analytics vs Azure Monitor

    Why use log analytics instead of Azure Arc?
    
    Log analytics is a simplified approach to the solution I needed.
    
    As I am aware at the moment it is not possible to add custom logs when using arc. This is needed to setup
    I did not know about Arc when I started to set this up but I will make an extra article going through the arc part of this process
    The Log Analytics agents are on a deprecation path and will no longer be supported after August 31, 2024

## Workspace ID and Key

    (https://github.com/OliverAdams/angryadmin/blob/gh-pages/docs/images/idandkey.PNG)

## The installation
    
    If you have followed all of the steps so far correctly
   

Next we will configure the logs we want to recieve
