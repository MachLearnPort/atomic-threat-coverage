| Title                | Microsoft Office Product Spawning Windows Shell                                                                                                                                                 |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Description          | Detects a Windows command line executable started from Microsoft Word, Excel, Powerpoint, Publisher and Visio.                                                                                                                                           |
| ATT&amp;CK Tactic    | <ul><li>[TA0002: Execution](https://attack.mitre.org/tactics/TA0002)</li><li>[TA0005: Defense Evasion](https://attack.mitre.org/tactics/TA0005)</li></ul>  |
| ATT&amp;CK Technique | <ul><li>[T1059: Command-Line Interface](https://attack.mitre.org/techniques/T1059)</li><li>[T1202: Indirect Command Execution](https://attack.mitre.org/techniques/T1202)</li></ul>                             |
| Data Needed          | <ul><li>[DN_0002_4688_windows_process_creation_with_commandline](../Data_Needed/DN_0002_4688_windows_process_creation_with_commandline.md)</li><li>[DN_0003_1_windows_sysmon_process_creation](../Data_Needed/DN_0003_1_windows_sysmon_process_creation.md)</li></ul>                                                         |
| Trigger              | <ul><li>[T1059: Command-Line Interface](../Triggers/T1059.md)</li><li>[T1202: Indirect Command Execution](../Triggers/T1202.md)</li></ul>  |
| Severity Level       | high                                                                                                                                                 |
| False Positives      | <ul><li>unknown</li></ul>                                                                  |
| Development Status   | experimental                                                                                                                                                |
| References           | <ul><li>[https://www.hybrid-analysis.com/sample/465aabe132ccb949e75b8ab9c5bda36d80cf2fd503d52b8bad54e295f28bbc21?environmentId=100](https://www.hybrid-analysis.com/sample/465aabe132ccb949e75b8ab9c5bda36d80cf2fd503d52b8bad54e295f28bbc21?environmentId=100)</li><li>[https://mgreen27.github.io/posts/2018/04/02/DownloadCradle.html](https://mgreen27.github.io/posts/2018/04/02/DownloadCradle.html)</li></ul>                                                          |
| Author               | Michael Haag, Florian Roth, Markus Neis                                                                                                                                                |


## Detection Rules

### Sigma rule

```
title: Microsoft Office Product Spawning Windows Shell
status: experimental
description: Detects a Windows command line executable started from Microsoft Word, Excel, Powerpoint, Publisher and Visio.
references:
    - https://www.hybrid-analysis.com/sample/465aabe132ccb949e75b8ab9c5bda36d80cf2fd503d52b8bad54e295f28bbc21?environmentId=100
    - https://mgreen27.github.io/posts/2018/04/02/DownloadCradle.html
tags:
    - attack.execution
    - attack.defense_evasion
    - attack.t1059
    - attack.t1202
author: Michael Haag, Florian Roth, Markus Neis
date: 2018/04/06
logsource:
    category: process_creation
    product: windows
detection:
    selection:
        ParentImage:
            - '*\WINWORD.EXE'
            - '*\EXCEL.EXE'
            - '*\POWERPNT.exe'
            - '*\MSPUB.exe'
            - '*\VISIO.exe'
            - '*\OUTLOOK.EXE'
        Image:
            - '*\cmd.exe'
            - '*\powershell.exe'
            - '*\wscript.exe'
            - '*\cscript.exe'
            - '*\sh.exe'
            - '*\bash.exe'
            - '*\scrcons.exe'
            - '*\schtasks.exe'
            - '*\regsvr32.exe'
            - '*\hh.exe'
            - '*\wmic.exe'
            - '*\mshta.exe'
            - '*\rundll32.exe'
            - '*\msiexec.exe'
            - '*\forfiles.exe'
            - '*\scriptrunner.exe'
            - '*\mftrace.exe'
            - '*\AppVLP.exe'
            - '*\svchost.exe'  # https://www.vmray.com/analyses/2d2fa29185ad/report/overview.html
    condition: selection
fields:
    - CommandLine
    - ParentCommandLine
falsepositives:
    - unknown
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
(ParentImage:("*\\\\WINWORD.EXE" "*\\\\EXCEL.EXE" "*\\\\POWERPNT.exe" "*\\\\MSPUB.exe" "*\\\\VISIO.exe" "*\\\\OUTLOOK.EXE") AND Image:("*\\\\cmd.exe" "*\\\\powershell.exe" "*\\\\wscript.exe" "*\\\\cscript.exe" "*\\\\sh.exe" "*\\\\bash.exe" "*\\\\scrcons.exe" "*\\\\schtasks.exe" "*\\\\regsvr32.exe" "*\\\\hh.exe" "*\\\\wmic.exe" "*\\\\mshta.exe" "*\\\\rundll32.exe" "*\\\\msiexec.exe" "*\\\\forfiles.exe" "*\\\\scriptrunner.exe" "*\\\\mftrace.exe" "*\\\\AppVLP.exe" "*\\\\svchost.exe"))
```


### splunk
    
```

```


### logpoint
    
```

```


### grep
    
```
grep -P '^(?:.*(?=.*(?:.*.*\\WINWORD\\.EXE|.*.*\\EXCEL\\.EXE|.*.*\\POWERPNT\\.exe|.*.*\\MSPUB\\.exe|.*.*\\VISIO\\.exe|.*.*\\OUTLOOK\\.EXE))(?=.*(?:.*.*\\cmd\\.exe|.*.*\\powershell\\.exe|.*.*\\wscript\\.exe|.*.*\\cscript\\.exe|.*.*\\sh\\.exe|.*.*\\bash\\.exe|.*.*\\scrcons\\.exe|.*.*\\schtasks\\.exe|.*.*\\regsvr32\\.exe|.*.*\\hh\\.exe|.*.*\\wmic\\.exe|.*.*\\mshta\\.exe|.*.*\\rundll32\\.exe|.*.*\\msiexec\\.exe|.*.*\\forfiles\\.exe|.*.*\\scriptrunner\\.exe|.*.*\\mftrace\\.exe|.*.*\\AppVLP\\.exe|.*.*\\svchost\\.exe)))'
```



