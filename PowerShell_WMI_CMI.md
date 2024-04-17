## 想要使用Windows Management Instrumentation（WMI）Cmdlet
+ 舊版PowerShell可用的WMI Cmdlet呼叫方式比新版少一些。但無法在 PowerShell 6+ 中使用。
  + Windows7就是舊版PowerShell。
  + Windows10部分仍保留舊版PowerShell呼叫方式。
  + 新版Powershell請改用CIM Cmdlet。
 
### 解決方案
+ 先檢查PowerShell支援狀態:
  + 目標WMI命令: Get-WMIObject
  + 目標CIM命令: Get-CimInstance
+ 檢查所有命令
```
PowerShell "Get-Command"
```
#### Get-WMIObject
+ 使用Where-Object檢查符合「Name」的命令(Get-WMIObject)
```
PowerShell "Get-Command | Where-Object { $_.name -eq 'Get-WMIObject' }"
```
+ 檢查符合「Name」的命令(Get-WMIObject)，並且只找「Name」的內容
```
PowerShell "Get-Command | Where-Object { $_.name -eq 'Get-WMIObject' } | Select-Object Name"
```
+ 檢查符合「Name」的命令(Get-WMIObject)，並且只找「Name」的內容，再調整顯示模式(key : value模式)
```
PowerShell "Get-Command | Where-Object { $_.name -eq 'Get-WMIObject' } | Select-Object Name | Format-List"
```
+ 接下來透過對內容的檢查就可以知道「Get-WMIObject」命令能不能用。
  + 能用的話就是會顯示名稱
  + 不能用的話就是沒有任何內容顯示。


#### Get-CimInstance
+ 使用Where-Object檢查符合「Name」的命令(Get-CimInstance)
```
PowerShell "Get-Command | Where-Object { $_.name -eq 'Get-CimInstance' }"
```
+ 檢查符合「Name」的命令(Get-CimInstance)，並且只找「Name」的內容
```
PowerShell "Get-Command | Where-Object { $_.name -eq 'Get-CimInstance' } | Select-Object Name"
```
+ 檢查符合「Name」的命令(Get-CimInstance)，並且只找「Name」的內容，再調整顯示模式(key : value模式)
```
PowerShell "Get-Command | Where-Object { $_.name -eq 'Get-CimInstance' } | Select-Object Name | Format-List"
```
+ 接下來透過對內容的檢查就可以知道「Get-WMIObject」命令能不能用。
  + 能用的話就是會顯示名稱
  + 不能用的話就是沒有任何內容顯示。
 + 確定可以用之後，就選一個可用的來進行後面操作

<br>

## 範例 - 取得作業系統版本
### 預設資訊(非全部)
+ Get-WMIObject:
  ```
  PowerShell "Get-WMIObject -Class Win32_OperatingSystem"
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_OperatingSystem"
  ```
### 調整顯示模式
+ Get-WMIObject:
  ```
  PowerShell "Get-WMIObject -Class Win32_OperatingSystem | Format-List"
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_OperatingSystem | Format-List"
  ```
### 顯示全部資訊
+ Get-WMIObject:
  ```
  PowerShell "Get-WMIObject -Class Win32_OperatingSystem | Format-List *"
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_OperatingSystem | Format-List *"
  ```
### 只顯示「Caption」內容
+ Get-WMIObject:
  ```
  PowerShell "Get-WMIObject -Class Win32_OperatingSystem | Select-Object Caption | Format-List"
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_OperatingSystem | Select-Object Caption | Format-List"
  ```
### 只顯示「Version」內容
+ Get-WMIObject:
  ```
  PowerShell "Get-WMIObject -Class Win32_OperatingSystem | Select-Object Version | Format-List"
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_OperatingSystem | Select-Object Version | Format-List"
  ```

<br>

## 範例 - 取得Serial port裝置(COM Ports)
### 預設資訊(非全部)
+ Get-WMIObject:
  ```
  PowerShell "Get-WMIObject -Class Win32_PnPEntity"
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_PnPEntity"
  ```
### 使用Where-Object檢查物件「PNPClass」符合「Ports」的內容
+ Get-WMIObject:
  ```
  PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.pnpclass -Match 'Ports' }"
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_PnPEntity | Where-Object { $_.pnpclass -Match 'Ports' }"
  ```
### 只查看「Name」，並調整顯示模式(key : value模式)
+ Get-WMIObject:
  ```
  PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.pnpclass -Match 'Ports' } | Select-Object Name | Format-List"
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_PnPEntity | Where-Object { $_.pnpclass -Match 'Ports' } | Select-Object Name | Format-List"
  ```
### 只查看「Caption」，並調整顯示模式(key : value模式)
+ Get-WMIObject:
  ```
  PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.pnpclass -Match 'Ports' } | Select-Object Caption | Format-List"
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_PnPEntity | Where-Object { $_.pnpclass -Match 'Ports' } | Select-Object Caption | Format-List"
  ```

### 調整顯示模式
PowerShell "Get-CimInstance -Class Win32_PnPEntity | Where-Object PNPClass -Like 'Ports' | Select-Object Name | Format-List"
