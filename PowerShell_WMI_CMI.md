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

```
| ConvertTo-Json -Compress
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
+ 檢查符合「Name」的命令(Get-WMIObject)，並且只找「Name」的內容，再調整顯示模式(精簡JSON模式)
```
PowerShell "Get-Command | Where-Object { $_.name -eq 'Get-WMIObject' } | Select-Object Name | Format-List | ConvertTo-Json -Compress"
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
### 只查看「Name」與「Caption」，並調整顯示模式(key : value模式)
+ Get-WMIObject:
  ```
  PowerShell "Get-CimInstance -Class Win32_PnPEntity | Select-Object -Property Name | Where-Object { $_.Name -match 'CH340' } | ConvertTo-Json -Compress" 
  ```
+ Get-CimInstance:
  ```
  PowerShell "Get-CimInstance -Class Win32_PnPEntity | Where-Object { $_.pnpclass -Match 'Ports' } | Select-Object Name,Caption | Format-List | ConvertTo-Json -Compress"
  ```
##

<br>

## 範例 - 取得DMM裝置(USB Test and Measurement Device (IVI))
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.description -Match 'USB Test and Measurement Device (IVI)' } | Select-Object Caption,DeviceID | Format-List | ConvertTo-Json -Compress"
```
# Get-Process
### 只查看「Name」，並調整顯示模式(key : value模式)
+ Get-Process:
  ```
  PowerShell "Get-Process  | Where-Object { $_.name -Match 'explorer' } | Select-Object Name |Format-List *"
  ```

## 範例 - 取得儲存裝置空間(主要目標是磁碟名稱和磁碟代號)
### 預設資訊(非全部)
+ Get-Volume:
  ```
  PowerShell "Get-Volume"
  ```
### 只選擇「DriveLetter」、「FileSystemLabel」與「DriveType」物件
+ Get-Volume:
  ```
  PowerShell "Get-Volume | Select-Object DriveLetter,FileSystemLabel,DriveType"
  ```
### 只選擇「DriveLetter」、「FileSystemLabel」與「DriveType」物件，並且DriveLetter不是空的
+ Get-Volume:
  ```
  PowerShell "Get-Volume | Select-Object DriveLetter,FileSystemLabel,DriveType | Where-Object {$_.DriveLetter -ne $null}"
  ```
### 只選擇「DriveLetter」、「FileSystemLabel」與「DriveType」物件，並且DriveLetter不是空的，DriveType不是「Fixed」。
+ Get-Volume:
  ```
  PowerShell "Get-Volume | Select-Object DriveLetter,FileSystemLabel,DriveType | Where-Object {$_.DriveLetter -ne $null} | Where-Object {$_.DriveType -ne 'Fixed'}"
  ```

### SwitchArray
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity"
```
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.PNPClass -Match 'Ports'}"
```
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.Name -Match 'CH340'}"
```
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.PNPClass -Match 'Ports' | Where-Object { $_.Name -Match 'CH340'}"
```
### DMM
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity"
```
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.PNPClass -Match 'USBTestAndMeasurementDevice'}"
```
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.PNPClass -Match 'USBTestAndMeasurementDevice'} | Select-Object PNPClass,PNPDeviceID"
```
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.PNPClass -Match 'USBTestAndMeasurementDevice'} | Select-Object PNPClass,PNPDeviceID | ConvertTo-Json -Compress"
```
```
PowerShell "Get-WMIObject -Class Win32_PnPEntity | Where-Object { $_.PNPClass -Match 'USBTestAndMeasurementDevice'} | Select-Object PNPDeviceID | ConvertTo-Json -Compress"
```
