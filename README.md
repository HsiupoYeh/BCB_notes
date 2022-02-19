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
+ 資料夾與檔案管理
     ```cpp
    //-----------------------------------------------------------------
	// 檔案存在 (請盡量使用絕對路徑，若使用相對路徑請添加「.」或「..」)
	//--
	// 1. 絕對路徑
	if (FileExists("C:\\Windows\\system32\\mspaint.exe"))
	{
		Memo1->Lines->Add("檔案存在");
	}
	else
	{
		Memo1->Lines->Add("檔案不存在");
	}
	// 2. 相對路徑
	if (FileExists(".\\Project1.exe"))
	{
		Memo1->Lines->Add("檔案存在");
	}
	else
	{
		Memo1->Lines->Add("檔案不存在");
	}
	//-----------------------------------------------------------------
	//-----------------------------------------------------------------
	// 資料夾建立 (請盡量使用絕對路徑，若使用相對路徑請添加「.」或「..」)
	// ForceDirectories可以強制建立多層資料夾
	//--
	// 1. 絕對路徑
	ForceDirectories("C:\\MyNewFolder1\\SubFolder\\");
	// 2. 相對路徑
	ForceDirectories(".\\MyNewFolder2\\SubFolder\\");
	//-----------------------------------------------------------------
	//-----------------------------------------------------------------
	// 資料夾存在 (請盡量使用絕對路徑，若使用相對路徑請添加「.」或「..」)
	//--
	// 1. 絕對路徑
	if (DirectoryExists("C:\\MyNewFolder1\\"))
	{
		Memo1->Lines->Add("資料夾存在");
	}
	else
	{
		Memo1->Lines->Add("資料夾不存在");
	}
	//--
	// 2. 相對路徑
	if (DirectoryExists(".\\MyNewFolder2\\"))
	{
		Memo1->Lines->Add("資料夾存在");
	}
	else
	{
		Memo1->Lines->Add("資料夾不存在");
	}
	//-----------------------------------------------------------------
     ```
     ```cpp
	//-----------------------------------------------------------------
	// C++ Builder提供了IOUtils函式庫，內部主要有TDirectory、TFile、TPath
	//--
	// TDirectory類別提供了許多常用的資料夾操作。
	//
	// static void __fastcall Copy(const System::UnicodeString SourceDirName, const System::UnicodeString DestDirName);
	// static void __fastcall CreateDirectory(const System::UnicodeString Path);
	// static void __fastcall Delete(const System::UnicodeString Path)/* overload */;
	// static void __fastcall Delete(const System::UnicodeString Path, const bool Recursive)/* overload */;
	// static bool __fastcall Exists(const System::UnicodeString Path, bool FollowLink = true);
	// static TFileAttributes __fastcall GetAttributes(const System::UnicodeString Path, bool FollowLink = true);
	// static System::UnicodeString __fastcall GetCurrentDirectory();
	// static void __fastcall SetCurrentDirectory(const System::UnicodeString Path);
	// static System::TStringDynArray __fastcall GetLogicalDrives();
	// static System::TDateTime __fastcall GetCreationTime(const System::UnicodeString Path);
	// static System::TDateTime __fastcall GetCreationTimeUtc(const System::UnicodeString Path);
	// static System::TDateTime __fastcall GetLastAccessTime(const System::UnicodeString Path);
	// static System::TDateTime __fastcall GetLastAccessTimeUtc(const System::UnicodeString Path);
	// static System::TDateTime __fastcall GetLastWriteTime(const System::UnicodeString Path);
	// static System::TDateTime __fastcall GetLastWriteTimeUtc(const System::UnicodeString Path);
	// static void __fastcall SetAttributes(const System::UnicodeString Path, const TFileAttributes Attributes);
	// static void __fastcall SetCreationTime(const System::UnicodeString Path, const System::TDateTime CreationTime);
	// static void __fastcall SetCreationTimeUtc(const System::UnicodeString Path, const System::TDateTime CreationTime);
	// static void __fastcall SetLastAccessTime(const System::UnicodeString Path, const System::TDateTime LastAccessTime);
	// static void __fastcall SetLastAccessTimeUtc(const System::UnicodeString Path, const System::TDateTime LastAccessTime);
	// static void __fastcall SetLastWriteTime(const System::UnicodeString Path, const System::TDateTime LastWriteTime);
	// static void __fastcall SetLastWriteTimeUtc(const System::UnicodeString Path, const System::TDateTime LastWriteTime);
	// static System::UnicodeString __fastcall GetParent(const System::UnicodeString Path);
	// static System::TStringDynArray __fastcall GetDirectories(const System::UnicodeString Path)/* overload */;
	// static System::TStringDynArray __fastcall GetDirectories(const System::UnicodeString Path, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::TStringDynArray __fastcall GetDirectories(const System::UnicodeString Path, const System::UnicodeString SearchPattern)/* overload */;
	// static System::TStringDynArray __fastcall GetDirectories(const System::UnicodeString Path, const System::UnicodeString SearchPattern, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::TStringDynArray __fastcall GetDirectories(const System::UnicodeString Path, const System::UnicodeString SearchPattern, const TSearchOption SearchOption)/* overload */;
	// static System::TStringDynArray __fastcall GetDirectories(const System::UnicodeString Path, const System::UnicodeString SearchPattern, const TSearchOption SearchOption, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::TStringDynArray __fastcall GetDirectories(const System::UnicodeString Path, const TSearchOption SearchOption, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::UnicodeString __fastcall GetDirectoryRoot(const System::UnicodeString Path);
	// static System::TStringDynArray __fastcall GetFiles(const System::UnicodeString Path)/* overload */;
	// static System::TStringDynArray __fastcall GetFiles(const System::UnicodeString Path, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::TStringDynArray __fastcall GetFiles(const System::UnicodeString Path, const System::UnicodeString SearchPattern)/* overload */;
	// static System::TStringDynArray __fastcall GetFiles(const System::UnicodeString Path, const System::UnicodeString SearchPattern, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::TStringDynArray __fastcall GetFiles(const System::UnicodeString Path, const System::UnicodeString SearchPattern, const TSearchOption SearchOption)/* overload */;
	// static System::TStringDynArray __fastcall GetFiles(const System::UnicodeString Path, const System::UnicodeString SearchPattern, const TSearchOption SearchOption, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::TStringDynArray __fastcall GetFiles(const System::UnicodeString Path, const TSearchOption SearchOption, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::TStringDynArray __fastcall GetFileSystemEntries(const System::UnicodeString Path)/* overload */;
	// static System::TStringDynArray __fastcall GetFileSystemEntries(const System::UnicodeString Path, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::TStringDynArray __fastcall GetFileSystemEntries(const System::UnicodeString Path, const System::UnicodeString SearchPattern)/* overload */;
	// static System::TStringDynArray __fastcall GetFileSystemEntries(const System::UnicodeString Path, const System::UnicodeString SearchPattern, const _di_TFilterPredicate Predicate)/* overload */;
	// static System::TStringDynArray __fastcall GetFileSystemEntries(const System::UnicodeString Path, const TSearchOption SearchOption, const _di_TFilterPredicate Predicate)/* overload */;
	// static bool __fastcall IsEmpty(const System::UnicodeString Path);
	// static bool __fastcall IsRelativePath(const System::UnicodeString Path);
	// static void __fastcall Move(const System::UnicodeString SourceDirName, const System::UnicodeString DestDirName);
    //--
	// TFile類別也提供了一些常用的檔案操作。
	// 要使用前必須，須引用「IOUtils.hpp」
	// #include <IOUtils.hpp>
	//-----------------------------------------------------------------
	//-----------------------------------------------------------------
	// 資料夾存在，TDirectory::Exists。
	//--
	// 1. 絕對路徑
	if (TDirectory::Exists("C:\\MyNewFolder1\\"))
	{
		Memo1->Lines->Add("資料夾存在");
	}
	else
	{
		Memo1->Lines->Add("資料夾不存在");
	}
	//--
	// 2. 相對路徑
	if (TDirectory::Exists(".\\MyNewFolder2\\"))
	{
		Memo1->Lines->Add("資料夾存在");
	}
	else
	{
		Memo1->Lines->Add("資料夾不存在");
	}
	//-----------------------------------------------------------------
	//-----------------------------------------------------------------
	// 資料夾刪除，TDirectory::Delete。
	//--
	// 1. 絕對路徑
	TDirectory::Delete("C:\\MyNewFolder1\\",true); //第二個參數帶true表示遞迴刪除內容
	if (TDirectory::Exists("C:\\MyNewFolder1\\"))
	{
		Memo1->Lines->Add("資料夾存在");
	}
	else
	{
		Memo1->Lines->Add("資料夾不存在");
	}
	//--
	// 2. 相對路徑
	TDirectory::Delete(".\\MyNewFolder2\\",true); //第二個參數帶true表示遞迴刪除內容
	if (TDirectory::Exists(".\\MyNewFolder2\\"))
	{
		Memo1->Lines->Add("資料夾存在");
	}
	else
	{
		Memo1->Lines->Add("資料夾不存在");
	}
	//-----------------------------------------------------------------
	//-----------------------------------------------------------------
	// 資料夾內檔案清單，TDirectory::GetFiles。
	//--
	// 1. 絕對路徑
	TStringDynArray temp_TStringDynArray_FileNameList = TDirectory::GetFiles(L"C:\\Windows");
	Memo1->Lines->Add("檔案數量="+String(temp_TStringDynArray_FileNameList.Length));
	for(int i = 0; i < temp_TStringDynArray_FileNameList.Length; i++)
	{
		Memo1->Lines->Add(temp_TStringDynArray_FileNameList[i]);
	}
	//--
	// 2. 相對路徑
	temp_TStringDynArray_FileNameList = TDirectory::GetFiles(L".\\");
	Memo1->Lines->Add("檔案數量="+String(temp_TStringDynArray_FileNameList.Length));
	for(int i = 0; i < temp_TStringDynArray_FileNameList.Length; i++)
	{
		Memo1->Lines->Add(temp_TStringDynArray_FileNameList[i]);
	}
	//-----------------------------------------------------------------
	Memo1->Lines->Add("--");
	//-----------------------------------------------------------------
	// 資料夾內檔案清單，TDirectory::GetFiles。指定過濾字串。
	//--
	// 1. 絕對路徑
	temp_TStringDynArray_FileNameList = TDirectory::GetFiles(L"C:\\Windows","*.exe");
	Memo1->Lines->Add("檔案數量="+String(temp_TStringDynArray_FileNameList.Length));
	for(int i = 0; i < temp_TStringDynArray_FileNameList.Length; i++)
	{
		Memo1->Lines->Add(temp_TStringDynArray_FileNameList[i]);
	}
	//--
	// 2. 相對路徑
	temp_TStringDynArray_FileNameList = TDirectory::GetFiles(L".\\","*.exe");
	Memo1->Lines->Add("檔案數量="+String(temp_TStringDynArray_FileNameList.Length));
	for(int i = 0; i < temp_TStringDynArray_FileNameList.Length; i++)
	{
		Memo1->Lines->Add(temp_TStringDynArray_FileNameList[i]);
	}
	//-----------------------------------------------------------------
    Memo1->Lines->Add("--");
	//-----------------------------------------------------------------
	// 資料夾內檔案清單，TDirectory::GetFiles。指定過濾字串+找子目錄。
	//--
	// 1. 絕對路徑
	temp_TStringDynArray_FileNameList = TDirectory::GetFiles(L"C:\\Windows","*.exe",TSearchOption::soAllDirectories);
	Memo1->Lines->Add("檔案數量="+String(temp_TStringDynArray_FileNameList.Length));
	for(int i = 0; i < temp_TStringDynArray_FileNameList.Length; i++)
	{
		Memo1->Lines->Add(temp_TStringDynArray_FileNameList[i]);
	}
	//--
	// 2. 相對路徑
	temp_TStringDynArray_FileNameList = TDirectory::GetFiles(L".\\","*.exe");
	Memo1->Lines->Add("檔案數量="+String(temp_TStringDynArray_FileNameList.Length));
	for(int i = 0; i < temp_TStringDynArray_FileNameList.Length; i++)
	{
		Memo1->Lines->Add(temp_TStringDynArray_FileNameList[i]);
	}
	//-----------------------------------------------------------------
     ```
