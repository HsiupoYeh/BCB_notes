# Application->MessageBox使用方法

### 使用範例
+ 
```cpp
Application->MessageBox(L" Hello\n world!",L"MB_ICONERROR",16);
```

+
```cpp
  AnsiString version_str="v20240420a";
	UnicodeString temp_UnicodeString_str="Author: HsiupoYeh.\nVersion: "+version_str;
	Application->MessageBox(temp_UnicodeString_str.c_str(),L"About Me",64);
```
