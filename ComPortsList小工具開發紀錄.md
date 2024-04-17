# ComPortsList小工具開發紀錄
+ 作者: HsiupoYeh
+ 更新日期: 2024-04-17

### 步驟
(1) 選擇32bit版本開發(因為目前沒用到64bit才能執行的功能，記憶體需求也不大)。  
> (1.1) 按下「New->VCL Forms Application - C++ Builder」。並確認「Target Platforms」是「Win32」。

(2) 獨立把專案存到指定資料夾中，以利日後管理。大部分自訂程式碼都會是相對路徑，未來只需要帶走這個資料夾即可在其他地方重新使用。
> (2.1) 按下「File->Save Project As」。

(3) 專案有許多常用設定需要調整，可使專案產生獨立執行檔、編譯器選擇、程式碼自動完成與提示等等。
> (3.1) 按下「Project->Options」，進行以下操作:  
>> (3.1.1) 檢查「C++ (Shared Options)」頁面下「_TCHAR map to」為「wchar_t」。  
>>> (3.1.1.1) 說明:「wchar_t」表示使用「UNICODE」。「char」表示使用「ANSI」。非英文語系的程式建議都選UNICODE。

>> (3.1.2) 檢查「C++ Compiler」頁面下「Classic Compiler->Use 'classic' Borland compiler」為「true」。  
>>> (3.1.2.1) 說明:僅有32位元平台有此設定。「true」表示使用「Borland編譯器」，不支援C++ 11。選「false」表示使用「clang編譯器」，支援C++ 11以上(不確定最新支援到哪)，但可能會導致程式碼自動完成與提示功能異常。

>> (3.1.3) 設定「C++ Linker」頁面下「Link with Dynamic RTL」為「false」。  
>>> (3.1.3.1) 說明: 表示把功能都編譯到程式中，執行時不需要外部dll就可獨立運行。  

>> (3.1.4) 設定「Application」頁面下利用「Load Icon 」按鈕更換自訂圖示。  
>>> (3.1.4.1) 說明: 程式圖示。  

>> (3.1.5) 檢查「Application」頁面下「Execution Level 」為「As Invoker」。  
>>> (3.1.5.1) 說明: 「As Invoker、Highest Available」都是普通權限就可以執行，「requireAdministrator」是執行前請求獲得管理者權限才能執行。  

>> (3.1.6) 設定「Application->Appearance」頁面下「Application settings->Title 」為「ComPortsList小工具」。  
>>> (3.1.6.1) 說明: 此參數是專屬本應用程式的欄位，可做為找到此程式的依據之一，常見可以在運行程式前先檢查是否有相同Title的程式正在執行，以達到禁止重複運行的功能。  

>> (3.1.7) 設定「Packages->Runtime Packages」頁面下「Link with runtime packages」為「false」。  
>>> (3.1.7.1) 說明: 表示把元件都編譯到程式中，執行時不需要外部bpl及dll就可以獨立運行。

(4) 編輯工具有部分設定可以協助撰寫程式碼，不過非必要。  
> (4.1) 按下「Tools->Options」，進行以下操作:  
>> (4.1.1) 設定「Formatter->C++->Line breaks」頁面下「Line breaks for braces->Line break before open brace」為「Yes」。  
>>> (4.1.1.1) 說明: 左大括號前面是否換行，預設是不換行比較精簡，但我喜歡換行，比較好讀。

```
以上都是比較基礎的設定，與程式設計無關，每個專案開始都類似，照做即可。接下來則是開始進行設計:
```

(5) 預設狀況下就有一個Form元件存在，預設名稱叫做「Form1」，先做一些基礎設定以利後續排版。  
> (5.1) 設定「Form1」的「properties」。這裡主要列出常用的一些。  
>> (5.1.1) 檢查「Form1」的「properties」頁面下「BorderIcon」為「[biSystemMenu,biMinimize,biMaximize]」。  
>>> (5.1.1.1) 說明:設定窗體右上角的按鈕如果存在的話要不要被啟用。「[biSystemMenu,biMinimize,biMaximize]」表示這三個被打勾。  

>> (5.1.2) 檢查「Form1」的「properties」頁面下「BorderStyle」為「bsSizeable」。  
>>> (5.1.2.1) 說明:設定窗體的樣式。可依需求嘗試不同風格決定是否符合需求。  

>> (5.1.2) 設定「Form1」的「properties」頁面下「Caption」為「ComPortsList小工具」。  
>>> (5.1.2.1) 說明:設定窗體的標題列文字。

>> (5.1.3) 設定「Form1」的「properties」頁面下「Color」為「clWindow」。  
>>> (5.1.3.1) 說明:設定成白色使工具列元件底色是白色。  

>> (5.1.4) 設定「Form1」的「properties」頁面下「Height」為「600」。  
>>> (5.1.4.1) 說明:設定窗體的外框高度。  

>> (5.1.5) 設定「Form1」的「properties」頁面下「Position」為「poScreenCenter」。  
>>> (5.1.5.1) 說明:設定窗體的出現位置，建議是用「poScreenCenter」，在螢幕中央。  

>> (5.1.6) 設定「Form1」的「properties」頁面下「Width」為「800」。  
>>> (5.1.6.1) 說明:設定窗體的外框寬度。

```
預設尺寸確定後就可以開始排版。
```

(6) 經典的Windows應用程式會在下方放置一個狀態列。如果不趕時間應該避免當作SimplePanel來使用。建議使用標準的(TStatusPanels)來規劃出多分隔的狀態列。
```
可參考經典軟體「記事本」與「NotePad++」的狀態列規劃。
```
> (6.1) 拖拉一個「TStatusBar」到「Form1」中。預設名稱會是「StatusBar1」。  

> (6.2) 設定「TStatusBar」的「Properties」。這裡主要列出常用的一些。  
>> (6.2.1) 檢查「StatusBar1」的「Properties」頁面下「Align」為「alBottom」。  
>>> (6.2.1.1) 說明:設定狀態列位置緊貼窗體下方。  

>> (6.2.2) 設定「StatusBar1」的「Properties」頁面下「Panel」，按下「...」後會出現編輯介面。從編輯介面建立5個TStatusPanels。  
>>> (6.2.2.1) 說明:建立狀態列中多個小版面。  

>> (6.2.3) 設定各「TStatusPanels」的「Properties」。  
>>> (6.2.3.1) 檢查「TStatusPanels」的「Properties」頁面下「Alignment」為「taLeftJustify」。  
>>>> (6.2.3.1.1) 說明:「taLeftJustify」是文字靠左對齊，「taCenter」是文字水平置中，「taRightJustify」是文字靠右對齊。注意，如果有人改掉「BiDiMode」可能會顛倒，所以建議不要動「BiDiMode」這個屬性。  

>>> (6.2.3.2) 檢查「TStatusPanels」的「Properties」頁面下「Style」為「psText」。  
>>>> (6.2.3.2.1) 說明:「psText」是可寫文字，「psOwnerDraw」是用另外的函數處理非文字。  

>>> (6.2.3.3) 設定「TStatusPanels」的「Properties」頁面下「Text」為「初始文字」。  
>>>> (6.2.3.3.1) 說明:初始文字可以預先在排版階段測試顯示效果，其中最靠右會被吃掉字元，請依需求測試設定文字內容。  

>>> (6.2.3.4) 設定「TStatusPanels」的「Properties」頁面下「Width」為「120」。  
>>>> (6.2.3.4.1) 說明:可以搭配初始文字來調整Width，以利排版。預設只能靠右對齊來分配欄位，其他效果則需要利用程式碼做調整。  

>>> (6.2.4) 設定「StatusBar1」的「Properties」頁面下「SimplePanel」為「false」。  
>>>> (6.2.4.1) 說明:要使前面設定的TStatusPanels有效，須將「SimplePanel」設為「false」。  

> (6.3) 設定「TStatusBar」的「Event」。  
>> (6.3.1) 設定「StatusBar1」的「Event」頁面下「OnResize」為如下程式碼。  
```C
void __fastcall TForm1::StatusBar1Resize(TObject *Sender)
{
int temp_remain_width=StatusBar1->Width;
//--
// 先配置最後一格，希望是100
StatusBar1->Panels->Items[4]->Width=100;
// 計算剩餘空間
temp_remain_width=temp_remain_width-StatusBar1->Panels->Items[4]->Width;
//--
// 配置隔壁一格，希望是200
StatusBar1->Panels->Items[3]->Width=200;
if (temp_remain_width<StatusBar1->Panels->Items[3]->Width)
{
StatusBar1->Panels->Items[3]->Width=temp_remain_width;
}
// 計算剩餘空間
temp_remain_width=temp_remain_width-StatusBar1->Panels->Items[3]->Width;
//--
// 配置隔壁一格，希望是200
StatusBar1->Panels->Items[2]->Width=200;
if (temp_remain_width<StatusBar1->Panels->Items[2]->Width)
{
StatusBar1->Panels->Items[2]->Width=temp_remain_width;
}
// 計算剩餘空間
temp_remain_width=temp_remain_width-StatusBar1->Panels->Items[2]->Width;
//--
//  配置隔壁一格，希望是120
StatusBar1->Panels->Items[1]->Width=120;
if (temp_remain_width<StatusBar1->Panels->Items[1]->Width)
{
StatusBar1->Panels->Items[1]->Width=temp_remain_width;
}
// 計算剩餘空間
temp_remain_width=temp_remain_width-StatusBar1->Panels->Items[1]->Width;
//--
// 最前方一格享受最大空間
StatusBar1->Panels->Items[0]->Width=temp_remain_width;
//--
}
```
