## 想要使用Windows Management Instrumentation（WMI）Cmdlet
+ 舊版PowerShell可用的WMI Cmdlet呼叫方式比新版少一些。但無法在 PowerShell 6+ 中使用。
  + Windows7就是舊版PowerShell。
  + Windows10部分仍保留舊版PowerShell呼叫方式。
  + 新版Powershell請改用CIM Cmdlet。
## 解決方案
+ 先檢查PowerShell支援狀態:
  + 目標WMI命令: Get-WMIObject
  + 目標CIM命令: Get-CimInstance
+ 檢查所有命令
```
PowerShell "Get-Command"
```
+ 檢查符合「Name」的命令(Get-WMIObject)
```
PowerShell "Get-Command -Name Get-WMIObject"
```
+ 檢查符合「Name」的命令(Get-WMIObject)，並且只找「Name」的內容
```
PowerShell "Get-Command -Name Get-WMIObject | Select-Object Name"
```
+ 檢查符合「Name」的命令(Get-WMIObject)，並且只找「Name」的內容，再調整顯示模式
```
PowerShell "Get-Command -Name Get-WMIObject | Select-Object Name | Format-List"
```


# 取得作業系統版本
### 精簡
PowerShell "Get-CimInstance -ClassName Win32_OperatingSystem"
### 調整顯示模式
PowerShell "Get-CimInstance -ClassName Win32_OperatingSystem | Format-List"
### 顯示全部
PowerShell "Get-CimInstance -ClassName Win32_OperatingSystem | Format-List *"
### 顯示標題
PowerShell "Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object Caption | Format-List"
### 顯示版本
PowerShell "Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object Version"


# 取得COM Ports 裝置
### 全部
PowerShell "Get-CimInstance -Class Win32_PnPEntity | Format-List *"
### 滿足物件「PNPClass」內有「Ports」
PowerShell "Get-CimInstance -Class Win32_PnPEntity | Where-Object PNPClass -Like 'Ports'"
### 只查看Name
PowerShell "Get-CimInstance -Class Win32_PnPEntity | Where-Object PNPClass -Like 'Ports' | Select-Object Name"
### 調整顯示模式
PowerShell "Get-CimInstance -Class Win32_PnPEntity | Where-Object PNPClass -Like 'Ports' | Select-Object Name | Format-List"
