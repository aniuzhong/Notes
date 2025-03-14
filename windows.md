Window 11
---------

1. Settings -> Personalisation -> Taskbar -> Taskbar behaviours -> Taskbar Alignment -> Left

2. Settings -> Personalisation -> Taskbar -> Taskbar items -> Search -> Hide

3. Settings -> Personalisation -> Taskbar -> Taskbar items -> Task view -> Off

4. Settings -> Personalisation -> Taskbar -> Taskbar items -> 
Widgets -> Off

5. Settings -> Privacy & security -> Search permissions -> More settings -> 
Show search highlights -> Off

6. Explorer -> View -> Group By -> (None)


Shortcuts
---------

[How to Switch Desktops Windows 11 Shortcut: A Step-by-Step Guide](https://www.solveyourtech.com/how-to-switch-desktops-windows-11-shortcut-a-step-by-step-guide)

Ctrl + Windows + Left/Right Arrow

Search: Windows + s


Applications
------------

[Everything](https://www.voidtools.com/downloads)

[Snipaste](https://www.snipaste.com)

[Bandzip](https://www.bandisoft.com/bandizip)

[Geek Uninstaller](https://geekuninstaller.com)

[Process Explorer](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer)

PowerToys

Windows Terminal

[SpaceSniffer](http://www.uderzo.it/main_products/space_sniffer)

[Rufus](https://rufus.ie/en) 

[MediaInfo](https://mediaarea.net/en/MediaInfo)

[DXVAChecker](https://bluesky-soft.com/en/DXVAChecker.html)

[Audacity](https://www.audacityteam.org)

WinMerge

RightMenuMgr

Docker Desktop

Github Desktop

WinDbg

Dependency Walker

[Autoclicker](https://autoclicker.io)

[Process Monitor](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon)

[RAMMap](https://learn.microsoft.com/en-us/sysinternals/downloads/rammap)


System Locale
-------------

Settings -> Time & language -> Language -> Related settings -> Administrative -> Administrative language settings

Or in Explorer

Control Panel\Clock and Region

Region -> Administrative -> Language for non-Unicode programs -> Change system locale

Beta: Use Unicode UTF-8 worldwide language support

When Windows and earlier operating systems like MS-DOS were developed, UTF-8 and Unicode were not widely adopted or standardized.
Code pages like CP 850 were already established for handling text in Western European languages.

| System locale | Default code page |
| --- | --- |
| English (United Kingdom) | CP850 |
| English (United States)  | CP437 | 

``` Powershell
systeminfo.exe | Select-String "Locale"
```

``` C++
#ifdef _WIN32
// #pragma execution_character_set("utf-8")
#include <Windows.h>
#endif

#include <iostream>

void wprint(std::wstring message)
{
    /*  wprint prints a string that can have any emoji or Unicode characters.
        When creating a wstring, put an L in front of it.
        For example, `wprint(L"Hi! 🔥");` prints `Hi! 🔥`.
        Your file must be saved in the UTF-8 (_with_ BOM/signature) encoding.
    */
#ifdef _WIN32
    HANDLE handle = GetStdHandle(STD_OUTPUT_HANDLE);
    DWORD n_written;
    WriteConsoleW(handle, message.c_str(), (DWORD)message.size(), &n_written, NULL);
#else
    std::wcout << message;
#endif
}

void print(const char8_t* message)
{
    UINT output_cp_old = ::GetConsoleOutputCP();
    UINT input_cp_old = ::GetConsoleCP();

    ::SetConsoleOutputCP(CP_UTF8);
    ::SetConsoleCP(CP_UTF8);

    std::cout << reinterpret_cast<const char*>(message);

    ::SetConsoleOutputCP(output_cp_old );
    ::SetConsoleCP(input_cp_old );
}

int main()
{
    std::cout << "Current Output Code Page: " << ::GetConsoleOutputCP() << '\n'
              << "Current Input Code Page: " << ::GetConsoleCP() << '\n';

    wprint(L"안녕하세요，世界，🌏！\n");
    print(u8"안녕하세요，世界，🌏！\n");

    std::cout << "Current Output Code Page: " << ::GetConsoleOutputCP() << '\n'
              << "Current Input Code Page: " << ::GetConsoleCP() << '\n';
}
```

Office Tool Plus
----------------

https://otp.landian.vip/en-us

https://baijiahao.baidu.com/s?id=1749263985039398754&wfr=spider&for=pc

一、下载软件

官方下载地址：https://otp.landian.vip/zh-cn/download.html

建议选择云图小镇和山东大学镜像的下载入口。

二、安装office

进入软件后为了确保我们电脑没有其他版本的office，需要对原本存在的Office程序或卸载残留进行清理。

点击左侧工具栏中的工具箱-移除Office-开始-是，等待操作完成即可。
开始安装Office，按照下图所示步骤依次点击或完成：

1. 点击左侧工具栏中的部署。
2. 选择自己所需的Office种类，这里选择Office2021批量许可证。
3. 按照自己需求选择所需的办公软件，这里选择经典办公三件套。
4. 语言选择简体中文。
5. 体系结构选择64位
6. 通道选择Office 2021企业长期版
7. 安装模块选择Office Tool Plus
8. 勾选下载后再部署，这样大大加快下载速度。
9. 点击开始部署，等待软件自动下载和安装完成。

三、安装许可证

软件安装完成后我们还需要设置产品许可证。我们只需要在Office Tool Plus里按照步骤找到我们下载的对应版本许可证点击安装等待完成即可。

1. 点击左侧工具栏中的激活。
2. 许可证管理 - 安装许可证 - 安装 - Office LTSC 专业增强版 2021 - 批量许可证 - 确定

四、激活office

(1) 自己有相关正版激活账号，且自己安装的也是对应的Office版本，则打开任意一个Office软件登陆账号即可激活。
(2) 安装的批量版本如“Office2024批量许可证”可使用KMS管理，推荐三个稳定可用的kms（中间用//进行分隔）：kms.loli.beer//kms.luochenzhimu.com//kms9.MSGuides.com。

按照下图流程进行：

1. 输入kms主机地址。
2. 保存设置。
3. 点击等待完成