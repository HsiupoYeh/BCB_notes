# BCB_notes

+ Memo
    ```cpp
    Memo1->Lines->Count //行數
    Memo1->Lines->Strings[n] //第n行文字
    Memo1->Lines->Add("增加一行"); //增加一行
    ```
+ ListView
    ```cpp
    // 「ViewStyle」設定為「vsReport」的狀況下...
    // 表格標頭是在「Column」
    // 表格內容是在「Item」
    ListView1->Items->Count //內容行數
    ListView1->Items->Item[0]->Caption //內容第一行的第一欄文字
    ListView1->Items->Item[0]->SubItems->Strings[0] //內容第一行的第二欄文字
    ListView1->Items->Item[0]->SubItems->Strings[1] //內容第一行的第三欄文字
    ```   
