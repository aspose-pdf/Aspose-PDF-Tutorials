---
category: general
date: 2026-02-20
description: 學習如何使用 PowerShell 安裝 nuget 套件、以系統管理員身分執行 PowerShell、列出已安裝的套件，並在數分鐘內驗證已安裝的套件。
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: zh-hant
og_description: 如何使用 PowerShell 安裝 NuGet 套件、以管理員身分執行 PowerShell、列出已安裝的套件並驗證已安裝的套件——完整教學.
og_title: 如何透過 PowerShell 安裝 NuGet 套件 – 快速指南
tags:
- PowerShell
- NuGet
- Package Management
title: 如何透過 PowerShell 安裝 NuGet 套件 – 步驟說明
url: /zh-hant/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---





{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何透過 PowerShell 安裝 NuGet 套件 – 步驟說明

有沒有想過 **如何在不開啟 Visual Studio 的情況下安裝 NuGet** 套件？你並不孤單。在許多 CI 流程或全新機器上，最快的方式就是直接進入 PowerShell——最好 **以系統管理員身分執行 PowerShell**——讓套件管理員自行處理。

在本教學中，我們會一步步說明整個流程：開啟正確的主控台、下載特定版本的函式庫，最後確認套件真的已安裝到系統上。完成後，你將能 **列出已安裝的套件**、了解 **如何驗證套件** 完整性，並確信 **驗證已安裝套件** 的步驟每次都成功。

## 你將學會

- 如何以正確的權限啟動 PowerShell。  
- NuGet 的 `Install-Package` 指令語法。  
- 如何 **列出已安裝的套件** 並確認版本號。  
- 常見的陷阱（缺少管理員權限、版本不符）以及避免方式。  

不需要任何 NuGet 使用經驗，只要有一台可運作的 Windows 電腦與一點好奇心即可。

---

## 使用 PowerShell 安裝 NuGet 套件的方法

> **小技巧：** 若你經常安裝相同的套件，可將指令寫入腳本檔，使用 `-File` 參數執行。這樣就不必一次又一次手動輸入相同指令。

### 步驟 1：以必要的權限開啟 PowerShell

首先必須 **以系統管理員身分執行 PowerShell**。若未提升權限，`Install-Package` Cmdlet 可能會靜默失敗或要求你確認，而這些都不在我們的預期之內。

1. 點擊「開始」按鈕。  
2. 輸入 **PowerShell**。  
3. 右鍵點擊 *Windows PowerShell*，選擇 **以系統管理員身分執行**。  

會出現 UAC 提示，點選 **是**。此時你已取得具備安裝套件權限的會話。

> *為什麼需要管理員？*  
> NuGet 會將檔案寫入全域套件資料夾（預設為 `C:\Program Files\PackageManagement\NuGet\Packages`）。此路徑受保護，只有提升權限的程序才能寫入。

### 步驟 2：安裝指定的 NuGet 套件與版本

開啟主控台後，核心指令非常簡單：

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` 是 PowerShell 包裝 NuGet 客戶端的指令。  
- `-Version` 用來鎖定你需要的確切版本，避免意外升級。  

若省略 `-Version`，PowerShell 會下載最新的穩定版——有時候這樣沒問題，但有時候你需要的是已測試過的特定版本。

#### 背後發生了什麼？

PowerShell 會連線至已設定的套件來源（預設為 `https://www.nuget.org/api/v2`），下載 `.nupkg` 檔案，然後將 DLL 解壓至全域套件資料夾，並在本機套件提供者中註冊。整個流程通常只要幾秒鐘，除非網路速度很慢。

### 步驟 3：驗證套件是否成功安裝

套件已寫入磁碟後，你可能會問 **「我要怎麼驗證套件？」** 答案就在一個簡單的查詢指令裡：

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

執行後會得到類似以下的結果：

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

此輸出確認了兩件事：

1. 套件 **Aspose.PDF** 已存在。  
2. 其版本與你指定的相符，滿足 **驗證已安裝套件** 的需求。

若想查看機器上 **所有** 套件，只要移除 `-Name` 篩選：

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

這個 **列出已安裝的套件** 檢視方式在稽核或清理舊函式庫時非常實用。

### 步驟 4：可選 – 處理例外情況

#### a) 找不到套件或版本不符

如果 PowerShell 回傳 *「Package not found」* 或 *「Version not available」*，請再次確認套件名稱與版本號。NuGet 不分大小寫，但多餘的空格會導致指令失效。

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) 未以管理員身分執行

若忘記 **以系統管理員身分執行 PowerShell**，Cmdlet 會拋出權限錯誤。只要關閉視窗，重新以提升權限開啟即可，無需重新安裝任何套件。

#### c) 使用自訂來源

在企業環境中，你可能會使用內部 NuGet Feed：

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

驗證步驟仍然相同，只是安裝時記得加入 `-Source` 參數。

---

## 快速參考表

| 操作                                 | PowerShell 指令                                           | 為什麼重要 |
|--------------------------------------|-----------------------------------------------------------|------------|
| 開啟提升權限的主控台                 | *Run PowerShell as Administrator*                         | 需要全域安裝 |
| 安裝特定版本                         | `Install-Package <pkg> -Version <x.y.z>`                  | 確保可重現的建置 |
| 列出單一套件                         | `Get-Package -Name <pkg>`                                  | 確認 **如何驗證套件** |
| 列出所有 NuGet 套件                  | `Get-Package \| Where-Object {$_.ProviderName -eq 'NuGet'}`| 方便 **列出已安裝的套件** |
| 搜尋可用的所有版本                   | `Find-Package <pkg> -AllVersions`                         | 當版本未知時有助於查找 |

---

## 結論

我們已完整說明 **如何透過 PowerShell 安裝 NuGet 套件**——從 **以系統管理員身分執行 PowerShell**、下載特定版本，到最後 **列出已安裝的套件** 以 **驗證已安裝套件**。掌握這些指令後，你可以在任何 Windows 機器上自動化函式庫管理，無論是為 CI 流程編寫腳本，或是為開發機修復缺少的 DLL。

接下來的建議？試著將多個套件寫入同一腳本，探索 `-Scope` 參數以在專案本地安裝，或結合 `Invoke-Expression` 來打造輕量級的團隊安裝程式。若遇到問題，別忘了 **如何驗證套件** 步驟——在 `Get-Package` 中看到正確的版本號往往是最快找出問題的方法。

祝你 PowerShell 使用愉快！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}