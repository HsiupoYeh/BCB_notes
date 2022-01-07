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
    ListView1->Items->Count //行數
    ListView1->Items->Item[0]->Caption //第一行的第一欄文字
    ListView1->Items->Item[0]->SubItems->Strings[0] //第一行的第二欄文字
    ListView1->Items->Item[0]->SubItems->Strings[1] //第一行的第三欄文字
    ```   
