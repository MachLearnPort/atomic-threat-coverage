| Title                | WMI Persistence                                                                                                                                                 |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Description          | Detects suspicious WMI event filter and command line event consumer based on event id 5861 and 5859 (Windows 10, 2012 and higher)                                                                                                                                           |
| ATT&amp;CK Tactic    | <ul><li>[TA0002: Execution](https://attack.mitre.org/tactics/TA0002)</li><li>[TA0003: Persistence](https://attack.mitre.org/tactics/TA0003)</li></ul>  |
| ATT&amp;CK Technique | <ul><li>[T1047: Windows Management Instrumentation](https://attack.mitre.org/techniques/T1047)</li></ul>                             |
| Data Needed          | <ul><li>[DN_0080_5859_wmi_activity](../Data_Needed/DN_0080_5859_wmi_activity.md)</li><li>[DN_0081_5861_wmi_activity](../Data_Needed/DN_0081_5861_wmi_activity.md)</li></ul>                                                         |
| Trigger              | <ul><li>[T1047: Windows Management Instrumentation](../Triggers/T1047.md)</li></ul>  |
| Severity Level       | high                                                                                                                                                 |
| False Positives      | <ul><li>Unknown (data set is too small; further testing needed)</li></ul>                                                                  |
| Development Status   | experimental                                                                                                                                                |
| References           | <ul><li>[https://twitter.com/mattifestation/status/899646620148539397](https://twitter.com/mattifestation/status/899646620148539397)</li><li>[https://www.eideon.com/2018-03-02-THL03-WMIBackdoors/](https://www.eideon.com/2018-03-02-THL03-WMIBackdoors/)</li></ul>                                                          |
| Author               | Florian Roth                                                                                                                                                |


## Detection Rules

### Sigma rule

```
title: WMI Persistence
status: experimental
description: Detects suspicious WMI event filter and command line event consumer based on event id 5861 and 5859 (Windows 10, 2012 and higher)
author: Florian Roth
references:
    - https://twitter.com/mattifestation/status/899646620148539397
    - https://www.eideon.com/2018-03-02-THL03-WMIBackdoors/
tags:
    - attack.execution
    - attack.persistence
    - attack.t1047
logsource:
    product: windows
    service: wmi
detection:
    selection:
        EventID: 5861
    keywords:
        - 'ActiveScriptEventConsumer'
        - 'CommandLineEventConsumer'
        - 'CommandLineTemplate'
        # - 'Binding EventFilter'  # too many false positive with HP Health Driver
    selection2:
        EventID: 5859
    condition: selection and 1 of keywords or selection2
falsepositives:
    - Unknown (data set is too small; further testing needed)
level: high


```





### es-qs
    
```

```


### xpack-watcher
    
```

```


### graylog
    
```
((EventID:"5861" AND ("ActiveScriptEventConsumer" OR "CommandLineEventConsumer" OR "CommandLineTemplate")) OR EventID:"5859")
```


### splunk
    
```

```


### logpoint
    
```

```


### grep
    
```
grep -P '^(?:.*(?:.*(?:.*(?=.*5861)(?=.*(?:.*(?:.*ActiveScriptEventConsumer|.*CommandLineEventConsumer|.*CommandLineTemplate))))|.*5859))'
```



