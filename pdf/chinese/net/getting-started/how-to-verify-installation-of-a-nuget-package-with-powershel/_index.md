---
category: general
date: 2026-03-03
description: 如何在 PowerShell 中验证 NuGet 包的安装。学习以管理员身份运行 PowerShell、安装特定版本，并高效管理包。
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: zh
og_description: 如何在 PowerShell 中验证 NuGet 包的安装。此一步一步的指南向您展示如何以管理员身份运行 PowerShell、安装特定版本，并确认该包已存在。
og_title: 如何使用 PowerShell 验证 NuGet 包的安装
tags:
- PowerShell
- NuGet
- Package Management
title: 如何使用 PowerShell 验证 NuGet 包的安装
url: /zh/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 PowerShell 验证 NuGet 包的安装

如何在 PowerShell 中验证 NuGet 包的安装是 Windows 管理员的常见任务。如果你曾经想知道包是否真的已经落地到系统中，本指南将手把手教你如何验证安装——无需猜测。  

接下来几分钟，我们将演示以管理员身份运行 PowerShell、拉取特定版本的包，最后确认该包已存在于机器上。你还会学到一些日常 **PowerShell 包管理** 的小技巧，帮助保持环境整洁。  

在开始之前，请确保你拥有一台装有 PowerShell 7（或 Windows PowerShell 5.1）的 Windows 机器，并且已连接互联网。无需额外工具；所有操作均由内置的 PackageManagement 提供程序完成。

---

![提升权限的 PowerShell 窗口截图，显示 Get-Package 命令](/images/verify-installation.png "展示如何在提升权限的 PowerShell 窗口中验证安装的截图")

## 步骤 1：以管理员身份运行 PowerShell  

以管理员权限运行 PowerShell 是防止权限相关问题的第一道防线。当你 **以管理员身份运行 PowerShell** 时，`Install-Package` cmdlet 能够写入 Program Files 文件夹并在系统范围目录中注册包。

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **小贴士：** 将 “Windows PowerShell (Admin)” 快捷方式固定到任务栏。点击一次即可开始使用。

### 为什么需要提升权限  

如果不提升权限，`Install-Package` 可能会悄悄回退到用户范围的位置，这会导致 `Get-Package` 默认在系统范围查找时出现混淆。提升权限可确保包出现在大多数脚本期望的位置。

---

## 步骤 2：安装 NuGet 包的特定版本  

通常你并不想要最新的发布版，而是想要一个已知可靠、项目已通过测试的版本。使用 `-Version` 参数的 **安装特定版本** 模式非常直接。

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### 命令拆解  

| 参数 | 功能说明 | 为什么需要 |
|-----------|--------------|-----------------|
| `-Version 25.3` | 锁定确切的构建号 | 确保可复现的构建 |
| `-ProviderName NuGet` | 指定 PowerShell 使用的提供程序 | 当注册了多个提供程序时避免歧义 |
| `-Scope AllUsers` | 为机器上的所有账户安装 | 与 `Get-Package` 的系统范围查询配合使用 |
| `-Force` | 抑制提示（脚本中常用） | 保持自动化流畅 |

> **注意：** 如果省略 `-Version`，PowerShell 将获取最新的包，这可能会引入破坏性更改。

---

## 步骤 3：验证安装  

现在到了关键时刻：**如何验证安装**。最直接的方式是让 PowerShell 查询你刚刚安装的包。

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

你应该会看到类似以下的输出：

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

如果该命令没有返回任何内容，请尝试用户范围的查询：

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### 其他验证方法  

1. **检查模块文件夹** – 包存放在 `C:\Program Files\PackageManagement\Packages\` 下。查找名为 `Aspose.PDF.25.3` 的文件夹。  
2. **使用 `Find-Package`** – 该命令会搜索仓库并确认该版本是否可用：  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **使用 .NET 验证** – 在 PowerShell 中加载程序集，以确保 DLL 可被加载：

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

只要上述任意检查通过，即表示你已经成功 **验证了安装**。

---

## 常见陷阱及规避方法  

- **缺少 NuGet 提供程序** – 首先运行 `Install-PackageProvider -Name NuGet -Force`。  
- **ExecutionPolicy 限制** – 临时使用 `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` 为当前会话解除限制。  
- **网络代理问题** – 如处于公司代理环境，使用 `-Proxy` 和 `-ProxyCredential` 参数。  
- **版本冲突** – 当存在多个版本时，在 `Get-Package` 中使用 `-RequiredVersion` 进行明确指定。

---

## 综合示例 – 完整脚本  

下面是一段可直接运行的脚本，封装了上述三步，包含错误处理，并在成功后打印友好的提示信息。

```powershell
<# 
.SYNOPSIS
    Installs a specific version of a NuGet package and verifies the installation.
.DESCRIPTION
    Demonstrates how to run PowerShell as admin, install a specific version, 
    and confirm that the package is present using Get-Package.
#>

# Ensure we are running elevated
if (-not ([Security.Principal.WindowsPrincipal] `
        [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
        [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Warning "Please run this script in an elevated PowerShell session."
    exit 1
}

$packageName = 'Aspose.PDF'
$packageVersion = '25.3'

try {
    Write-Host "Installing $packageName version $packageVersion..."
    Install-Package $packageName -Version $packageVersion `
        -ProviderName NuGet -Scope AllUsers -Force -ErrorAction Stop

    Write-Host "Installation completed. Verifying..."
    $pkg = Get-Package -Name $packageName -ProviderName NuGet -ErrorAction Stop

    if ($pkg.Version -eq $packageVersion) {
        Write-Host "`n✅ Successfully verified installation of $packageName $packageVersion."
    } else {
        Write-Error "Version mismatch: Expected $packageVersion but got $($pkg.Version)."
    }
}
catch {
    Write-Error "An error occurred: $_"
}
```

运行脚本后会出现明确的 “✅ Successfully verified installation…” 行，表明 **如何验证安装** 已实现端到端的完整流程。

---

## 结论  

现在你已经掌握了使用 PowerShell 验证任意 NuGet 包安装的完整方法，从启动提升权限的会话、安装目标版本，到最终确认包的存在。熟练这些步骤后，你的 **PowerShell 包管理** 工作流将更加可靠，避免 “看似已安装却不可用” 的常见困扰。

接下来可以尝试将 `Aspose.PDF` 换成其他库，实验 `-Scope CurrentUser`，或为新工作站批量安装多个包。如果遇到奇怪的问题，请回顾上面的故障排除技巧——尤其是提供程序和 ExecutionPolicy 的检查。

祝你脚本编写愉快，愿你的安装始终可验证！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}