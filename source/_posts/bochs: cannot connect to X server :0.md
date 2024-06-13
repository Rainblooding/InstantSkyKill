---
abbrlink: ''
categories:
- - 系统
date: '2024-06-13T09:03:07.410722+08:00'
tags:
- X server
title: 'bochs: cannot connect to X server :0'
updated: '2024-06-13T09:03:09.628+08:00'
---
这个错误信息 "bochs: cannot connect to X server :0" 表示 Bochs 模拟器尝试使用图形界面，但无法连接到 X 服务器。X 服务器负责管理 Unix 类操作系统中的图形显示，包括在 Windows 子系统 Linux (WSL) 中运行的那些。

要解决这个问题，可以按照以下步骤操作：

### 1. 在 Windows 上安装 X 服务器

你需要在 Windows 上运行一个 X 服务器来处理来自 WSL 的图形应用程序。一个常用的选择是 **VcXsrv**。下面是安装和设置的步骤：

1. **下载并安装 VcXsrv**：
   * 从 [VcXsrv 的 SourceForge 页面]() 下载安装程序。
   * 运行安装程序并按照提示完成安装。
2. **启动 VcXsrv**：
   * 启动 VcXsrv，在配置窗口中选择 `Multiple windows` 模式。
   * 勾选 `Disable access control` 选项（这样做会允许所有连接，但在生产环境中要小心，因为这可能会带来安全风险）。

### 2. 配置 WSL 以使用 X 服务器

在 WSL 中，需要设置环境变量以告诉应用程序如何连接到 X 服务器。

1. **打开 WSL 终端**。
2. **设置 DISPLAY 环境变量**：
   * 临时设置（仅在当前会话中有效）：
     <pre><div class="dark bg-gray-950 rounded-md border-[0.5px] border-token-border-medium"><div class="flex items-center relative text-token-text-secondary bg-token-main-surface-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>sh</span><div class="flex items-center"><span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>复制代码</button></span></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-sh">export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0.0
     </code></div></div></pre>
   * 永久设置（在 `~/.bashrc` 或 `~/.zshrc` 文件中添加）：
     <pre><div class="dark bg-gray-950 rounded-md border-[0.5px] border-token-border-medium"><div class="flex items-center relative text-token-text-secondary bg-token-main-surface-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>sh</span><div class="flex items-center"><span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>复制代码</button></span></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-sh">echo "export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0.0" >> ~/.bashrc
     source ~/.bashrc
     </code></div></div></pre>

### 3. 运行 Bochs

现在，你可以尝试在 WSL 中运行 Bochs 了：

<pre><div class="dark bg-gray-950 rounded-md border-[0.5px] border-token-border-medium"><div class="flex items-center relative text-token-text-secondary bg-token-main-surface-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>sh</span><div class="flex items-center"><span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>复制代码</button></span></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-sh">bochs
</code></div></div></pre>

### 4. 排查问题

如果仍然无法连接到 X 服务器，可以检查以下几点：

* 确保 VcXsrv 正在运行，并且配置正确。
* 确保防火墙没有阻止 WSL 与 VcXsrv 之间的通信。
* 检查 WSL 中的 `DISPLAY` 变量是否正确配置。

通过以上步骤，应该可以解决 Bochs 不能连接到 X 服务器的问题。
