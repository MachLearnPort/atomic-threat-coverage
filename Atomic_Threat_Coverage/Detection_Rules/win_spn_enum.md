| Title                | Possible SPN Enumeration                                                                                                                                                 |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Description          | Detects Service Principal Name Enumeration used for Kerberoasting                                                                                                                                           |
| ATT&amp;CK Tactic    | <ul><li>[TA0006: Credential Access](https://attack.mitre.org/tactics/TA0006)</li></ul>  |
| ATT&amp;CK Technique | <ul><li>[T1208: Kerberoasting](https://attack.mitre.org/techniques/T1208)</li></ul>                             |
| Data Needed          | <ul></ul>                                                         |
| Trigger              | <ul><li>[T1208: Kerberoasting](../Triggers/T1208.md)</li></ul>  |
| Severity Level       | medium                                                                                                                                                 |
| False Positives      | <ul><li>Administrator Activity</li></ul>                                                                  |
| Development Status   | experimental                                                                                                                                                |
| References           | <ul><li>[https://p16.praetorian.com/blog/how-to-use-kerberoasting-t1208-for-privilege-escalation](https://p16.praetorian.com/blog/how-to-use-kerberoasting-t1208-for-privilege-escalation)</li></ul>                                                          |
| Author               | Markus Neis, keepwatch                                                                                                                                                |


## Detection Rules

### Sigma rule

```
title: Possible SPN Enumeration
description: Detects Service Principal Name Enumeration used for Kerberoasting
status: experimental
references:
    - https://p16.praetorian.com/blog/how-to-use-kerberoasting-t1208-for-privilege-escalation
author: Markus Neis, keepwatch
date: 2018/11/14
tags:
    - attack.credential_access
    - attack.t1208
logsource:
    category: process_creation
    product: windows
detection:
    selection_image:
        Image: '*\setspn.exe'
    selection_desc:
        Description: '*Query or reset the computer* SPN attribute*'
    cmd:
        CommandLine: '*-q*'
    condition: (selection_image or selection_desc) and cmd
falsepositives:
    - Administrator Activity
level: medium

```





### es-qs
    
```

```


### xpack-watcher
    
```

```


### graylog
    
```
((Image:"*\\\\setspn.exe" OR Description:"*Query or reset the computer* SPN attribute*") AND CommandLine:"*\\-q*")
```


### splunk
    
```

```


### logpoint
    
```

```


### grep
    
```
grep -P '^(?:.*(?=.*(?:.*(?:.*.*\\setspn\\.exe|.*.*Query or reset the computer.* SPN attribute.*)))(?=.*.*-q.*))'
```



