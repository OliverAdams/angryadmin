# Teams Rooms Event Logs

Configure the agent to collect the log named "Skype Room System"

Warning, Error and Informational Events

I will not cover these other logs in detail in this post but these are worth adding also.

Also Microsoft-Windows-Audio/CaptureMonitor
     Microsoft-Windows-Audio/GlitchDetection
     Microsoft-Windows-Audio/Informational
     Microsoft-Windows-Audio/Performance
     Microsoft-Windows-Audio/Diagnostic     
     Microsoft-Windows-Battery/Diagnostic
     Microsoft-Windows-Disk/Operational
     Microsoft-Windows-NetworkProfile/Diagnostic
     
Once these logs are added we can start to query these logs using the Kusto Query Language
     
Every five minutes the teams room device will write two events to the SRS event log.

If everything is working fine them events 2000 and 3000 are written to the event log.

If there is an issue with signin to Exchange,Teams or Skype the event 2001 is written instead of 2000

If there is an issue with a connected hardware component the event 3001 is written instead of 3001

If the teams app is restarted at any point the event 4000 is written to the event log.

## Skype-Room-System - Event 2000 Informational

This is a healthy heartbeat event. Every 5 minutes, Microsoft Teams Rooms checks that it is signed in to Microsoft Teams or Skype for Business and has network and Exchange connectivity.If all 3 factors are true, it writes Event ID 2000 into the event log every 5 minutes until the device is offline or one or more of the conditions are no longer met.

The data returned when this event triggers is show below:

```json
{"Description":"Heartbeat is healthy.", "ResourceState":"Healthy", "OperationName":"Heartbeat", "OperationResult":"Pass",
"OS":"Windows 10", "OSVersion":"10.0.14393.693", "Alias":"alias<span></span>@contoso.com", "DisplayName":"Display name",
"AppVersion":"1.0.38.0", "IPv4Address":"10.10.10.10", "IPv6Address":"IP v6 address"}
```

## Skype-Room-System - Event 2001 Error

This is an app error event. Every 5 minutes, Microsoft Teams Rooms checks that it is signed in to Microsoft Teams or Skype for Business with network and Exchange connectivity. If one or more factors are not true, it writes EventID 2001 into the event log every 5 minutes until the device is offline or all conditions are met once again.

The data returned when this event triggers is show below:

```
{"Description":"Network status : Healthy. Exchange status : Connected. Signin status: Unhealthy. Teams Signin status: Healthy.",
"ResourceState":"Unhealthy", "OperationName":"Heartbeat", "OperationResult":"Fail", "OS":"Windows 10",
"OSVersion":"10.0.14393.693", "Alias":"", "DisplayName":"Display Name", "AppVersion":"1.0.38.0",
"IPv4Address":"10.10.10.10", "IPv6Address":"ip v6 address"}
```

## Skype-Room-System - Event 3000 - Informational

This event verifies that a hardware check was run and found to be healthy. Every 5 minutes Microsoft Teams Rooms checks that configured hardware components such as front of room display, microphone, speaker, and camera are connected and functioning. If all components are healthy, it writes EventID 3000 into the event log. This event is written every 5 minutes unless there is an issue with a connected device.

```
{"Description":"HardwareCheckEngine is healthy.", "ResourceState":"Healthy", "OperationName":"HardwareCheckEngine", 
"OperationResult":"Pass", "OS":"Windows 10", "OSVersion":"10.0.14393.693", "Alias":"alias<span></span>@contoso.com",
"DisplayName":"Display Name", "AppVersion":"1.0.38.0", "IPv4Address":"10.10.10.10", "IPv6Address":"ip v6 address"}
```

## Skype-Room-System - Event 3001 - Error

This is a hardware error event. The Microsoft Teams Rooms app has a process that checks the health of connected hardware components (front of room, microphone, speaker, camera) every 5 minutes. If one or more of the components are unhealthy, it writes EventID 3001 into the event log. This event is written every 5 minutes until the issue with the device is fixed.

The data returned when this event triggers is show below:

```
{"Description":"HardwareCheckEngine is healthy.", "ResourceState":"Healthy", "OperationName":"HardwareCheckEngine",
"OperationResult":"Pass", "OS":"Windows 10", "OSVersion":"10.0.14393.693", "Alias":"alias<span></span>@contoso.com",
"DisplayName":"Display Name", "AppVersion":"1.0.38.0", "IPv4Address":"10.10.10.10", "IPv6Address":"ip v6 address"}
```

## Skype-Room-System - Event 4000

This is an App Restart event. Every time the app is restarted, it will log this event into the Windows event log.

The data returned when this event triggers is show below:

```
{"Description":"App restarts.", "ResourceState":"Healthy", "OperationName":"Restart", "OperationResult":"Pass",
"OS":"Windows 10", "OSVersion":"10.0.14393.693", "Alias":"alias<span></span>@domain.com",
"DisplayName":"Display Name", "AppVersion":"1.0.38.0", "IPv4Address":"10.10.10.10", "IPv6Address":"ip v6 address"}
```

In the next section we will look into parsing this information inside Log Analytics using the Kusto Query Language.

