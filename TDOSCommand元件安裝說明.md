# TDOSCommand元件安裝說明
TDOSCommand元件安裝說明  
  
## 開發環境:  
Windows 7 SP1 64bit 繁體中文版  
Embarcadero® C++Builder 10.2 Version 25.0.28979.1978 

## 運行需求:  
Windosw作業系統。  
可運行32位元應用程式。  

## 注意事項:  
本專案有使用TDOSCommand元件。  
  
- 來源: DOSCommand-102Tokyo
- 網址: https://github.com/TurboPack/DOSCommand/
- 網址: https://github.com/TurboPack/DOSCommand/releases/tag/102Tokyo


- HsiupoYeh修正:  
    > 已將「...\TurboPack\DOSCommand-102Tokyo\Source\DosCommand.pas」
    > 部分程式碼改為以下:  
    ```delphi
    procedure TDosCommand.Stop;
    begin
      if (FThread <> nil) then
      begin
        FThread.Terminate; // by sirius
        //------------------------------
        // Edited by HsiupoYeh
        // FThread.WaitFor; // by sirius2
        // FreeAndNil(FThread);
        //------------------------------
      end;
    end;
    ```
    > 以上是修正Stop功能有關的多執行續操作錯誤。


## 安裝說明:
1. 解壓縮至「C:\」。使檔案結構如下:
    ```
    C:\
    └─TurboPack
        │  說明.txt
        │  
        └─DOSCommand-102Tokyo
            │  README.md
            │  
            ├─Packages
            │          
            └─Source
    ```
2. 執行「C++Builder 10.2」主程式。  
3. 按下「Tools->Options」，會跳出「Options」視窗。  
    + 3.1 找到「Environment Options->Delphi Options->Library」頁面。在「Selected Platform」，選擇「32-bit Windows」。
    + 3.2 接著在「Library path」按下最後面的「...」按鈕。會跳出「Directories」視窗。
    + 3.3 接著在「Greyed items denote invalid path.」按下「資料夾」按鈕。選擇「C:\TurboPack\DOSCommand-102Tokyo\Source」。
    + 3.4 接著按下「Add」。完成後按下「OK」。
    + 3.5 最後「Options」視窗也按下「OK」。
4. 按下「Tools->Options」，會跳出「Options」視窗。  
    + 4.1 找到「Environment Options->Delphi Options->Library」頁面。在「Selected Platform」，選擇「64-bit Windows」。
    + 4.2 接著在「Library path」按下最後面的「...」按鈕。會跳出「Directories」視窗。
    + 4.3 接著在「Greyed items denote invalid path.」按下「資料夾」按鈕。選擇「C:\TurboPack\DOSCommand-102Tokyo\Source」。
    + 4.4 接著按下「Add」。完成後按下「OK」。
    + 4.5 最後「Options」視窗也按下「OK」。
5. 按下「Tools->Options」，會跳出「Options」視窗。
    + 5.1 找到「Environment Options->C++ Options->Paths and Directories」頁面。在「Selected Platform」，選擇「32-bit Windows」。
    + 5.2 選擇「Compiler」標籤頁，在「System Include path」按下最後面的「...」按鈕。會跳出「Directories」視窗。
    + 5.3 接著在「Greyed items denote invalid path.」按下「資料夾」按鈕。選擇「C:\TurboPack\DOSCommand-102Tokyo\Source\hpp\Win32\Release」。
    + 5.4 接著按下「Add」。完成後按下「OK」。
    + 5.5 最後「Options」視窗也按下「OK」。
6. 按下「Tools->Options」，會跳出「Options」視窗。
    + 6.1 找到「Environment Options->C++ Options->Paths and Directories」頁面。在「Selected Platform」，選擇「32-bit Windows」。
    + 6.2 選擇「Classic Compiler」標籤頁，在「System Include path」按下最後面的「...」按鈕。會跳出「Directories」視窗。
    + 6.3 接著在「Greyed items denote invalid path.」按下「資料夾」按鈕。選擇「C:\TurboPack\DOSCommand-102Tokyo\Source\hpp\Win32\Release」。
    + 6.4 接著按下「Add」。完成後按下「OK」。
    + 6.5 最後「Options」視窗也按下「OK」。
7. 按下「Tools->Options」，會跳出「Options」視窗。
    + 7.1 找到「Environment Options->C++ Options->Paths and Directories」頁面。在「Selected Platform」，選擇「64-bit Windows」。
    + 7.2 在「System Include path」按下最後面的「...」按鈕。會跳出「Directories」視窗。
    + 7.3 接著在「Greyed items denote invalid path.」按下「資料夾」按鈕。選擇「C:\TurboPack\DOSCommand-102Tokyo\Source\hpp\Win64\Release」。
    + 7.4 接著按下「Add」。完成後按下「OK」。
    + 7.5 最後「Options」視窗也按下「OK」。
8. 按下「Tools->Options」，會跳出「Options」視窗。
    + 8.1 找到「Environment Options->C++ Options->Paths and Directories」頁面。在「Selected Platform」，選擇「32-bit Windows」。
    + 8.2 選擇「Compiler」標籤頁，在「Library path」按下最後面的「...」按鈕。會跳出「Directories」視窗。
    + 8.3 接著在「Greyed items denote invalid path.」按下「資料夾」按鈕。選擇「C:\TurboPack\DOSCommand-102Tokyo\Source」。
    + 8.4 接著按下「Add」。完成後按下「OK」。
    + 8.5 最後「Options」視窗也按下「OK」。
9. 按下「Tools->Options」，會跳出「Options」視窗。
    + 9.1 找到「Environment Options->C++ Options->Paths and Directories」頁面。在「Selected Platform」，選擇「32-bit Windows」。
    + 9.2 選擇「Classic Compiler」標籤頁，在「Library path」按下最後面的「...」按鈕。會跳出「Directories」視窗。
    + 9.3 接著在「Greyed items denote invalid path.」按下「資料夾」按鈕。選擇「C:\TurboPack\DOSCommand-102Tokyo\Source」。
    + 9.4 接著按下「Add」。完成後按下「OK」。
    + 9.5 最後「Options」視窗也按下「OK」。
10. 按下「Tools->Options」，會跳出「Options」視窗。
    + 10.1 找到「Environment Options->C++ Options->Paths and Directories」頁面。在「Selected Platform」，選擇「64-bit Windows」。
    + 10.2 選擇「Classic Compiler」標籤頁，在「Library path」按下最後面的「...」按鈕。會跳出「Directories」視窗。
    + 10.3 接著在「Greyed items denote invalid path.」按下「資料夾」按鈕。選擇「C:\TurboPack\DOSCommand-102Tokyo\Source」。
    + 10.4 接著按下「Add」。完成後按下「OK」。
    + 10.5 最後「Options」視窗也按下「OK」。
11. 按下「File->Open」，會跳出「Open」視窗。
    + 11.1 選擇「C:\TurboPack\DOSCommand-102Tokyo\Packages\CBuilder\CBuilder.groupproj」後按下「開啟舊檔」。
    + 11.2 在「Project Manager」區塊找到檔案結構樹，於「DOSCommandCR250.bpl」節點按下右鍵，按下「Build」。
    + 11.3 出現警告提示「There are warnings.」是正常現象，按下「OK」按鈕。
    + 11.4 在「Project Manager」區塊找到檔案結構樹，於「DOSCommandCD250.bpl」節點按下右鍵，按下「Install」。
    + 11.5 出現提示視窗，按下「OK」按鈕。
12. 關閉「C++Builder 10.2」主程式，詢問是否儲存全部按否。
13. 完成!
