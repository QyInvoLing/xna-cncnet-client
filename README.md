# XNA CnCNet Client for macOS CrossOver

基于 [2.6.11.1](https://github.com/CnCNet/xna-cncnet-client/releases?page=5#release-2.6.11.1) 版本的 XNA CnCNet 客户端制作的适用于 macOS+CrossOver 的制作器，用于启动《心灵终结》。按原项目要求，采用 GPL v3 协议开源。
A build for macOS + CrossOver based on version [2.6.11.1](https://github.com/CnCNet/xna-cncnet-client/releases?page=5#release-2.6.11.1) of the XNA CnCNet client, used to launch Mental Omega. In accordance with the original project's requirements, it is open-sourced under GPL v3.

原有的 CnCNet 客户端有一个问题：
The original CnCNet client has an issue:

  > CnCNet 客户端，在加入 CnCNet 大厅时，先在 `GetServerListSortedByLatency` 里同时 Ping 11 台 GameSurge IRC 服务器，用来挑延迟最低的一台。它在 Ping 外面只捕获 `PingException`（见 Connection.cs），而Wine Mono 抛出的是未经包装的 `SocketException`，使得程序崩溃。
  > When joining the CnCNet lobby, the CnCNet client first pings 11 GameSurge IRC servers simultaneously inside `GetServerListSortedByLatency` to choose the one with the lowest latency. Outside the ping function call  it only catches `PingException` (see Connection.cs), whereas Wine Mono throws an unwrapped `SocketException`, causing the program to crash.

  这导致在我完成下文的绝大部分配置步骤后，仍无法正常加入 CnCNet 大厅。因此我修改了一小部分代码解决了这个 bug。希望大家都可以愉快地在 macOS 上游玩《心灵终结》。
  As a result, after completing most of the configuration steps below, I still could not join the CnCNet lobby normally. Therefore, I modified a small portion of the code to fix this bug. I hope everyone can enjoy playing Mental Omega on macOS.

  ## 为你的 macOS 配置《心灵终结》运行环境

  ## Set Up the Mental Omega Runtime Environment for Your macOS

  经过两天的研究，我在我的 MacBook Neo 上使用 CrossOver 成功配置了可正常运行《心灵终结》的容器。遭遇战、战役和多人联机均无问题。
  After two days of research, I successfully configured a container on my MacBook Neo using CrossOver that can run Mental Omega normally. Skirmish, campaign, and multiplayer all work without issues.

  - 安装CrossOver。本文基于 CrossOver 26编写，未在其他版本进行过测试。
    Install CrossOver. This article is based on CrossOver 26 and has not been tested on other versions.
  - 新建一个 Windows 10 64位容器，将你的《心灵终结》安装至该容器内。
    Create a new Windows 10 64-bit container and install your copy of Mental Omega into it.
  - 前往[这里](https://github.com/FunkyFr3sh/cnc-ddraw/releases#release-v7.1.0.0)下载 cnc-ddraw.zip，将其中的内容解压到《心灵终结》的根目录内。
    Go [here](https://github.com/FunkyFr3sh/cnc-ddraw/releases#release-v7.1.0.0) to download cnc-ddraw.zip and extract its contents into the root directory of Mental Omega.
  - 在 CrossOver 中查看当前容器，将图形API设为`D3DMetal`并打开`MSync`。然后，使用`控制面板（注意不是 Windows 控制面板） - Wine 配置 - 函数库`内的`新增函数库顶替`功能添加`ddraw.dll`。
    In CrossOver, view the current container, set the graphics API to `D3DMetal`, and enable `MSync`. Then use the `Add Library Override` feature under `Control Panel (note: not the Windows Control Panel) - Wine Configuration - Libraries`to add `ddraw.dll`.
  - 使用[此项目](https://github.com/QyInvoLing/xna-cncnet-client)提供的构建产物替换`Resources`目录下的文件。
    Replace the files in the `Resources` directory with the build artifacts provided by [this project](https://github.com/QyInvoLing/xna-cncnet-client).
  - 特别地，如果你是使用非英语语言包的玩家：请使用 XCCMixer 提取`expandmo98.mix`中的`stringtable09.csf`和`stringtable11.csf`，将它们分别改名为`stringtable01.csf`和`stringtable02.csf`，置于《心灵终结》的根目录下。本条解决方案来自[百度贴吧](https://tieba.baidu.com/p/10691738740)。
    In particular, if you are using a non-English language pack: use XCCMixer to extract `stringtable09.csf` and `stringtable11.csf` from `expandmo98.mix`, rename them to `stringtable01.csf` and `stringtable02.csf` respectively, and place them in the root directory of Mental Omega. This solution comes from [this tieba post](https://tieba.baidu.com/p/10691738740).
  - 令容器启动`Resources/clientdx.exe`。选择`CnC-DDraw`这一渲染补丁。
    Make the container launch `Resources/clientdx.exe`. Select the `CnC-DDraw` renderer patch.
  - Enjoy！

本文也同步发布于[我的博客](https://qyinv.icu)。