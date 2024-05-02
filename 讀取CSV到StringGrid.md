# 讀取CSV到StringGrid

```cpp
	//----------------------------------------------------------------------
	// OpenDialog1的初始資料夾路徑
	OpenDialog1->InitialDir=ExtractFileDir(Application->ExeName)+"\\";
	// OpenDialog1下拉選單過濾檔名
	OpenDialog1->Filter = "R2MS_Lite Raw CSV(*.csv)|*.csv";
	// 呼叫OpenDialog1
	if(OpenDialog1->Execute())
	{
		//展示檔案名稱
		Log_Memo->Lines->Add("選擇檔案名稱 = "+OpenDialog1->FileName);
		//----------------------------------------------------------------------
		// 利用TStringList讀取CSV檔案到StringGrid1元件中
		// 記得要拉一個StringGrid1出來
		//--
		// 宣告TStringList
		TStringList *all_csv_TStringList=new TStringList();
		TStringList *one_line_csv_TStringList=new TStringList();
		//--
		// 讀取檔案到物件中
		all_csv_TStringList->LoadFromFile(OpenDialog1->FileName);
		Log_Memo->Lines->Add("檔案行數 = "+String(all_csv_TStringList->Count));
		//--
		// 調整StringGrid1的RowCount，就是Y方向上有幾行。有+1是為了增加一個表格編號用行數。
		StringGrid1->RowCount=all_csv_TStringList->Count+1;
		//--
		// 逐行解析
		for (int y = 0; y < all_csv_TStringList->Count; y++)
		{
			//--
			// 把一行逗號分隔的文字放入物件中，使其依照逗號分隔拆分
			one_line_csv_TStringList->CommaText=all_csv_TStringList->Strings[y];
			//Log_Memo->Lines->Add("每行逗號分隔項目數量 = "+String(one_line_csv_TStringList->Count));
			//--
			if (y==0)
			{
				Log_Memo->Lines->Add("每行逗號分隔項目數量 = "+String(one_line_csv_TStringList->Count));
				// 調整StringGrid1的ColCount，就是X方向上有幾個逗號分隔的內容。有+1是為了增加一個表格編號用行數。
				StringGrid1->ColCount=one_line_csv_TStringList->Count+1;
			}
			else
			{
				if (StringGrid1->ColCount==(one_line_csv_TStringList->Count+1))
				{
					//Log_Memo->Lines->Add("本行逗號分隔項目數量與前一行相同!");
				}
				else
				{
					Log_Memo->Lines->Add("本行逗號分隔項目數量與前一行不同!");
                }
			}
			// 填入X方向表格編號
			if (y==0)
			{
				for (int x = 0; x < one_line_csv_TStringList->Count; x++)
				{
					StringGrid1->Cells[x+1][y]=String(x+1);
				}
			}
			// 填入Y方向表格編號
			StringGrid1->Cells[0][y+1]=String(y+1);
			// 填入內容
			for (int x = 0; x < one_line_csv_TStringList->Count; x++)
			{
				StringGrid1->Cells[x+1][y+1]=one_line_csv_TStringList->Strings[x];
			}
		}
		//--
		// 釋放TStringList
		delete all_csv_TStringList;
		delete one_line_csv_TStringList;
		//----------------------------------------------------------------------
	}
	else
	{
		Application->MessageBox(L"使用者取消!",L"錯誤",0+16);
        return;
	}
	//----------------------------------------------------------------------
```
