# Kusto Queries

### JSON Parse Health Status

```
Event 
| where Source == "SRS-App" and EventID == 2000
| extend d=parse_json(RenderedDescription) 
| extend Description=d.Description, ResourceState=d.ResourceState, OperationName=d.OperationName,OperationResult=d.OperationResult,OS=d.OS,OSVersion=d.OSVersion,Alias=d.Alias,DisplayName=d.DisplayName,Appversion=d.Appversion,IPV4Address=d.IPV4Address,IPV4Address2=d.IPV4Address2,IPV6Address=d.IPV6Address
| project Computer,Description,ResourceState,OperationName,OperationResult,OS,OSVersion,Alias,DisplayName,Appversion,IPV4Address,IPV4Address2,IPV6Address
```

### Heartbeats

```
Event 
| where Source == "SRS-App" and EventID == 2000
| project Computer, Source
| summarize Count=count() by Computer, Source
| render columnchart   
```

```
Event 
| where Source == "SRS-App" and EventID == 2001
| extend d=parse_json(RenderedDescription) 
| extend Description=d.Description
| project Computer, TimeGenerated,
NetworkStatus=replace_string(replace_string(tostring(NetworkStatus=split(Description,".",0)),'"]',""),'["Network status : ',""),
ExchangeStatus=replace_string(replace_string(tostring(ExchangeStatus=split(Description,".",1)),'"]',""),'[" Exchange status : ',""),
SigninStatus=replace_string(replace_string(tostring(SigninStatus=split(Description,".",2)),'"]',""),'[" Signin status:',""),
TeamsSigninStatus=replace_string(replace_string(tostring(TeamsSigninStatus=split(Description,".",3)),'"]',""),'[" Teams Signin status: ',"")
| summarize any(TimeGenerated) by Computer, NetworkStatus, ExchangeStatus, SigninStatus, TeamsSigninStatus
```

### Teams Sign in status monitor

```
Event 
| where Source == "SRS-App" and EventID == 2001
| extend d=parse_json(RenderedDescription) 
| extend Description=d.Description
| project Computer, TimeGenerated,
NetworkStatus=replace_string(replace_string(tostring(NetworkStatus=split(Description,".",0)),'"]',""),'["Network status : ',""),
ExchangeStatus=replace_string(replace_string(tostring(ExchangeStatus=split(Description,".",1)),'"]',""),'[" Exchange status : ',""),
SigninStatus=replace_string(replace_string(tostring(SigninStatus=split(Description,".",2)),'"]',""),'[" Signin status:',""),
TeamsSigninStatus=replace_string(replace_string(tostring(TeamsSigninStatus=split(Description,".",3)),'"]',""),'[" Teams Signin status: ',"")
| summarize  any(TimeGenerated) by Computer, NetworkStatus, ExchangeStatus, SigninStatus, TeamsSigninStatus
| where TeamsSigninStatus != "Healthy"
| project Computer, any_TimeGenerated
```

### Sigin status monitor

```
Event 
| where Source == "SRS-App" and EventID == 2001
| extend d=parse_json(RenderedDescription) 
| extend Description=d.Description
| project Computer, TimeGenerated,
NetworkStatus=replace_string(replace_string(tostring(NetworkStatus=split(Description,".",0)),'"]',""),'["Network status : ',""),
ExchangeStatus=replace_string(replace_string(tostring(ExchangeStatus=split(Description,".",1)),'"]',""),'[" Exchange status : ',""),
SigninStatus=replace_string(replace_string(tostring(SigninStatus=split(Description,".",2)),'"]',""),'[" Signin status:',""),
TeamsSigninStatus=replace_string(replace_string(tostring(TeamsSigninStatus=split(Description,".",3)),'"]',""),'[" Teams Signin status: ',"")
| summarize  any(TimeGenerated) by Computer, NetworkStatus, ExchangeStatus, SigninStatus, TeamsSigninStatus
| where SigninStatus != "Healthy"
| project Computer, any_TimeGenerated
```

### Network Status Monitor

```
Event 
| where Source == "SRS-App" and EventID == 2001
| extend d=parse_json(RenderedDescription) 
| extend Description=d.Description
| project Computer, TimeGenerated,
NetworkStatus=replace_string(replace_string(tostring(NetworkStatus=split(Description,".",0)),'"]',""),'["Network status : ',""),
ExchangeStatus=replace_string(replace_string(tostring(ExchangeStatus=split(Description,".",1)),'"]',""),'[" Exchange status : ',""),
SigninStatus=replace_string(replace_string(tostring(SigninStatus=split(Description,".",2)),'"]',""),'[" Signin status:',""),
TeamsSigninStatus=replace_string(replace_string(tostring(TeamsSigninStatus=split(Description,".",3)),'"]',""),'[" Teams Signin status: ',"")
| summarize  any(TimeGenerated) by Computer, NetworkStatus, ExchangeStatus, SigninStatus, TeamsSigninStatus
| where NetworkStatus != "Healthy"
| project Computer, any_TimeGenerated
```

### Exchange Monitor

```
Event 
| where Source == "SRS-App" and EventID == 2001 or EventID == 2000
| extend d=parse_json(RenderedDescription) 
| extend Description=d.Description
| project Computer, TimeGenerated,
NetworkStatus=replace_string(replace_string(tostring(NetworkStatus=split(Description,".",0)),'"]',""),'["Network status : ',""),
ExchangeStatus=replace_string(replace_string(tostring(ExchangeStatus=split(Description,".",1)),'"]',""),'[" Exchange status : ',""),
SigninStatus=replace_string(replace_string(tostring(SigninStatus=split(Description,".",2)),'"]',""),'[" Signin status:',""),
TeamsSigninStatus=replace_string(replace_string(tostring(TeamsSigninStatus=split(Description,".",3)),'"]',""),'[" Teams Signin status: ',"")
| summarize  any(TimeGenerated) by Computer, NetworkStatus, ExchangeStatus, SigninStatus, TeamsSigninStatus
| where ExchangeStatus  != "Connected"
| project Computer, any_TimeGenerated
```

```
Event 
| where Source == "SRS-App" and EventID == 2001
| project Computer, Source
| summarize Count=count() by Source,Computer
```

```
Event 
| where Source == "SRS-App" and EventID == 3001
| project Computer, Source
| summarize Count=count() by Source,Computer
```

Error Count Piechart

```
Event 
| where Source == "SRS-App" and EventID == 2001
| project Computer, Source
| summarize Count=count() by Computer, Source
| render piechart      
```

```
Event 
| where Source == "SRS-App" and EventID == 4000
| project Computer, Source
| summarize Count=count() by Computer, Source
| render barchart
```

```
Event 
| where Source == "SRS-App" and EventID == 4000
| project Computer, Source
| summarize Count=count() by Source,Computer
```


```
Event 
| where Source == "SRS-App" and EventID == 3001
| extend d=parse_json(RenderedDescription) 
| extend Description=d.Description
| project Computer, 
ConferencMicrophoneStatus=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",0)),'"]',""),'["Conference Microphone status : ',""),
ConferencSpeakerStatus=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",1)),'"]',""),'[" Conference Speaker status : ',""),
DefaultSpeakerStatus=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",2)),'"]',""),'[" Default Speaker status : ',""),
CameraStatus=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",3)),'"]',""),'[" Camera status : ',""),
FrontOfRoomDisplay=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",4)),'"]',""),'[" Front of Room Display status : ',""),
MotionSensor=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",5)),'"]',""),'[" Motion Sensor status : ',""),
HDMIIngest=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",6)),'"]',""),'[" HDMI Ingest status : ',""),
ContentCamera=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",7)),'"]',""),'[" Content Camera status : ',"")
| where FrontOfRoomDisplay == "Unhealthy"
```

SigninStatus

```
Event 
| where Source == "SRS-App" and EventID == 3001 or EventID == 3000
| extend d=parse_json(RenderedDescription) 
| extend Description=d.Description
| project Computer, 
ConferencMicrophoneStatus=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",0)),'"]',""),'["Conference Microphone status : ',""),
ConferencSpeakerStatus=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",1)),'"]',""),'[" Conference Speaker status : ',""),
DefaultSpeakerStatus=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",2)),'"]',""),'[" Default Speaker status : ',""),
CameraStatus=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",3)),'"]',""),'[" Camera status : ',""),
FrontOfRoomDisplay=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",4)),'"]',""),'[" Front of Room Display status : ',""),
MotionSensor=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",5)),'"]',""),'[" Motion Sensor status : ',""),
HDMIIngest=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",6)),'"]',""),'[" HDMI Ingest status : ',""),
ContentCamera=replace_string(replace_string(tostring(ConferenceSpeakerStatus=split(Description,".",7)),'"]',""),'[" Content Camera status : ',"")
| summarize count() by Computer,HDMIIngest , FrontOfRoomDisplay, ContentCamera, ConferencMicrophoneStatus, ConferencSpeakerStatus, DefaultSpeakerStatus, MotionSensor
| distinct Computer, HDMIIngest , FrontOfRoomDisplay, ContentCamera, ConferencMicrophoneStatus, ConferencSpeakerStatus, DefaultSpeakerStatus, MotionSensor
```
