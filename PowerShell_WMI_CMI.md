### 想要使用Windows Management Instrumentation（WMI）Cmdlet
+ 舊版PowerShell可用的WMI Cmdlet呼叫方式比新版少一些。但無法在 PowerShell 6+ 中使用。
  + Windows7就是舊版。
  + Windows10部分仍保留舊版呼叫方式。
  + 新版Powershell請改用CIM Cmdlet。
### 解決方案
+ 先檢查PowerShell支援狀態:
  + 目標WMI命令: Get-WMIObject
  + 目標CIM命令: Get-CimInstance
