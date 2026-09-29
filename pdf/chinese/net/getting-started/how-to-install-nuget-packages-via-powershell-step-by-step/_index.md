---
category: general
date: 2026-02-20
description: 学习如何使用 PowerShell 安装 NuGet 包、以管理员身份运行 PowerShell、列出已安装的包并在几分钟内验证已安装的包。
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: zh
og_description: 如何使用 PowerShell 安装 NuGet 包，管理员身份运行 PowerShell，列出已安装的包并验证已安装的包——完整教程。
og_title: 如何通过 PowerShell 安装 NuGet 包 – 快速指南
tags:
- PowerShell
- NuGet
- Package Management
title: 如何通过 PowerShell 安装 NuGet 包 – 步骤指南
url: /zh/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何通过 PowerShell 安装 NuGet 包 – 步骤详解

是否曾想过 **如何安装 NuGet** 包而不打开 Visual Studio？你并不孤单。在许多 CI 流水线或全新机器上，最快的方式就是进入 PowerShell——最好 **以管理员身份运行 PowerShell**——让包管理器自行工作。

在本教程中，我们将完整演示整个过程：打开正确的控制台、下载特定版本的库，最后确认包确实已安装到系统中。结束时，你将能够 **列出已安装的包**、了解 **如何验证包** 的完整性，并确信 **验证已安装的包** 步骤每次都成功。

## 你将学到

- 如何以正确的权限启动 PowerShell。  
- NuGet 的 `Install-Package` 命令完整语法。  
- 如何 **列出已安装的包** 并确认版本号。  
- 常见陷阱（缺少管理员权限、版本不匹配）以及规避方法。  

无需任何 NuGet 经验，只需一台可用的 Windows 机器和一点好奇心。

---

## 使用 PowerShell 安装 NuGet 包的方法

> **专业提示：** 如果你经常添加相同的包，考虑将它们写入脚本文件并使用 `-File` 运行。这样可以避免一次又一次地输入相同的命令。

### 步骤 1：以必要的权限打开 PowerShell

首先要做的就是 **以管理员身份运行 PowerShell**。没有提升的权限，`Install-Package` cmdlet 可能会悄悄失败或弹出你不想处理的确认提示。

1. 点击开始按钮。  
2. 输入 **PowerShell**。  
3. 右键单击 *Windows PowerShell*，选择 **以管理员身份运行**。  

会出现 UAC 提示，点击 **是**。现在你拥有了一个具备特权的会话，可用于安装包。

> *为什么需要管理员？*  
> NuGet 会将文件写入全局包文件夹（默认是 `C:\Program Files\PackageManagement\NuGet\Packages`）。该位置受保护，只有提升的进程才能写入。

### 步骤 2：安装所需的 NuGet 包及其版本

打开控制台后，核心命令非常简单：

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` 是 PowerShell 对 NuGet 客户端的包装。  
- `-Version` 用于锁定你需要的确切构建，防止意外升级。  

如果省略 `-Version`，PowerShell 将获取最新的稳定版本——有时这样可以，但有时你需要恰好测试过的那个版本。

#### 实际内部发生了什么？

PowerShell 会联系已配置的包源（默认是 `https://www.nuget.org/api/v2`），下载 `.nupkg` 文件。随后将 DLL 解压到全局包文件夹，并在本地包提供程序中注册该包。整个过程通常在几秒钟内完成，除非网络很慢。

### 步骤 3：验证包是否成功安装

包已经落盘后，你可能会问，**“如何验证包？”** 答案就在一个简单的查询中：

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

运行后会返回类似下面的内容：

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

该输出确认了两点：

1. 包 **Aspose.PDF** 已存在。  
2. 其版本与您指定的相匹配，满足 **验证已安装的包** 的要求。

如果想查看机器上的 *所有* 包，去掉 `-Name` 过滤器即可：

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

这个 **列出已安装的包** 视图在审计或清理旧库时非常实用。

### 步骤 4：可选 – 处理边缘情况

#### a) 未找到包或版本不匹配

如果 PowerShell 返回 *“Package not found”* 或 *“Version not available”*，请再次检查拼写和版本号。NuGet 对大小写不敏感，但多余的空格会导致命令失败。

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) 未以管理员身份运行

如果忘记 **以管理员身份运行 PowerShell**，cmdlet 会抛出权限错误。解决办法只需关闭窗口并以提升权限重新打开——无需重新安装任何东西。

#### c) 使用自定义源

在企业环境中，你可能会使用内部 NuGet 源：

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

验证步骤保持不变，只需在安装时记得加入 `-Source` 参数。

---

## 快速参考表

| 操作                                 | PowerShell 命令                                          | 重要原因 |
|--------------------------------------|----------------------------------------------------------|----------|
| 打开提升权限的控制台                | *Run PowerShell as Administrator*                        | 需要全局安装 |
| 安装特定版本                         | `Install-Package <pkg> -Version <x.y.z>`                 | 确保可复现的构建 |
| 列出单个包                           | `Get-Package -Name <pkg>`                                 | 确认 **如何验证包** |
| 列出所有 NuGet 包                    | `Get-Package \| Where-Object {$_.ProviderName -eq 'NuGet'}`| 便于 **列出已安装的包** |
| 查询可用的所有版本                  | `Find-Package <pkg> -AllVersions`                        | 当版本未知时有帮助 |

---

## 结论

我们已经完整演示了 **如何安装 NuGet** 包的全过程——从 **以管理员身份运行 PowerShell** 打开控制台、下载特定版本，到最后 **列出已安装的包** 以 **验证已安装的包**。掌握这些命令后，你可以在任何 Windows 机器上自动化库管理，无论是为 CI 流水线编写脚本，还是仅仅修复开发机器上缺失的 DLL。

下一步？尝试将多个包写入同一个脚本，探索 `-Scope` 参数以在项目本地安装，或结合 `Invoke-Expression` 为团队构建轻量级安装器。如果遇到问题，记得使用 **如何验证包** 步骤——在 `Get-Package` 中查看版本往往是最快定位问题的方法。

祝你 PowerShell 使用愉快！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}