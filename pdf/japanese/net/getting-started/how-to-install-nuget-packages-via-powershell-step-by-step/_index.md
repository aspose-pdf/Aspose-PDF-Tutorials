---
category: general
date: 2026-02-20
description: PowerShell を使用して NuGet パッケージをインストールする方法、管理者として PowerShell を実行する方法、インストール済みパッケージを一覧表示する方法、そして数分でインストールされたパッケージを確認する方法を学びましょう。
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: ja
og_description: PowerShell を使用して NuGet パッケージをインストールする方法、PowerShell を管理者として実行する方法、インストール済みパッケージを一覧表示し、インストールされたパッケージを確認する方法—完全な手順解説。
og_title: PowerShellでNuGetパッケージをインストールする方法 – クイックガイド
tags:
- PowerShell
- NuGet
- Package Management
title: PowerShell を使用して NuGet パッケージをインストールする方法 – ステップバイステップ
url: /ja/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerShell を使用した NuGet パッケージのインストール方法 – ステップバイステップ

Visual Studio を開かずに **how to install nuget** パッケージをインストールする方法を考えたことがありますか？ あなたは一人ではありません。多くの CI パイプラインや新しいマシンでは、最速の方法は PowerShell に入ることです—できれば *run powershell as admin* —そしてパッケージマネージャに任せます。

このチュートリアルでは、全工程を順に解説します：正しいコンソールを開くこと、特定バージョンのライブラリを取得すること、そして最終的にパッケージがシステムに正しくインストールされたことを確認します。最後までに、**list installed packages** ができ、**how to verify package** の整合性を確認でき、**verify installed package** 手順が毎回成功したことに自信が持てるようになります。

## 学習内容

- 正しい権限で PowerShell を起動する方法。  
- `Install-Package` コマンドの正確な構文（NuGet 用）。  
- **list installed packages** の方法とバージョン番号の確認方法。  
- 一般的な落とし穴（管理者権限がない、バージョン不一致）とその回避方法。  

NuGet の事前経験は不要です。動作する Windows マシンと少しの好奇心があれば始められます。

---

## PowerShell を使用した NuGet パッケージのインストール方法

> **Pro tip:** 同じパッケージを頻繁に追加する場合は、スクリプト ファイルにまとめて `-File` で実行することを検討してください。同じ行を何度も入力する手間が省けます。

### 手順 1: 必要な権限で PowerShell を開く

最初に行うべきことは **run powershell as admin** です。権限が昇格していないと、`Install-Package` コマンドレットは黙って失敗したり、対処したくない確認を求めたりすることがあります。

1. スタート ボタンをクリックします。  
2. **PowerShell** と入力します。  
3. *Windows PowerShell* を右クリックし、**Run as administrator** を選択します。  

UAC のプロンプトが表示されますので、**Yes** をクリックします。これでパッケージ インストール用の特権セッションが準備できました。

> *Why admin?*  
> NuGet はデフォルトでグローバル パッケージ フォルダー (`C:\Program Files\PackageManagement\NuGet\Packages`) にファイルを書き込みます。その場所は保護されているため、昇格したプロセスだけが書き込めます。

### 手順 2: 必要な NuGet パッケージとバージョンをインストールする

コンソールが開いたら、基本コマンドはシンプルです：

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- "`Install-Package` は NuGet クライアントの PowerShell ラッパーです。"  
- "`-Version` は必要な正確なビルドを固定し、偶発的なアップグレードを防ぎます。"  

`-Version` を省略すると、PowerShell は最新の安定版リリースを取得します—場合によっては問題ありませんが、テストした正確なバージョンが必要なこともあります。

#### 背景で何が起きているか？

PowerShell は設定されたパッケージ ソース（デフォルトは `https://www.nuget.org/api/v2`）に接続し、`.nupkg` ファイルをダウンロードします。その後、DLL をグローバル パッケージ フォルダーに展開し、ローカル パッケージ プロバイダーにパッケージを登録します。通常、この一連の処理は数秒で完了しますが、ネットワークが遅い場合は例外です。

### 手順 3: パッケージが正常にインストールされたことを確認する

パッケージがディスクに配置されたので、たぶん **“How do I verify the package?”** と尋ねるでしょう。その答えはシンプルなクエリにあります：

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

このコマンドを実行すると、次のような結果が返ります：

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

その出力は次の 2 点を確認します：

1. パッケージ **Aspose.PDF** が存在すること。  
2. バージョンが要求したものと一致し、**verify installed package** の要件を満たしていること。  

マシン上の *すべて* のパッケージを確認したい場合は、`-Name` フィルターを外します：

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

この **list installed packages** ビューは、監査や古いライブラリのクリーンアップが必要なときに便利です。

### 手順 4: オプション – エッジケースの処理

#### a) パッケージが見つからない、またはバージョンが一致しない

PowerShell が *“Package not found”* または *“Version not available”* と返した場合は、スペルとバージョン番号を再確認してください。NuGet は大文字小文字を区別しませんが、余分なスペースがコマンドを破壊します。

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) 管理者権限なしで実行する場合

**run powershell as admin** を忘れた場合、コマンドレットは権限エラーを投げます。対処法はウィンドウを閉じて、昇格した権限で再度開くだけです—再インストールは不要です。

#### c) カスタム ソースの使用

企業環境では内部 NuGet フィードがあるかもしれません：

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

検証手順は同じです。インストール時に `-Source` を付けることを忘れないでください。

---

## クイックリファレンステーブル

| Action                              | PowerShell command                                          | Why it matters |
|-------------------------------------|-------------------------------------------------------------|----------------|
| 昇格したコンソールを開く               | *Run PowerShell as Administrator*                           | グローバル インストールに必要 |
| 特定のバージョンをインストールする          | `Install-Package <pkg> -Version <x.y.z>`                    | 再現可能なビルドを保証 |
| 単一パッケージを一覧表示する               | `Get-Package -Name <pkg>`                                    | **how to verify package** を確認 |
| すべての NuGet パッケージを一覧表示する      | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| **list installed packages** に便利 |
| 利用可能なバージョンを検索する           | `Find-Package <pkg> -AllVersions`                           | バージョンが不明な場合に役立つ |

## 結論

PowerShell を使用した **how to install nuget** パッケージのインストール手順を最初から最後までカバーしました—コンソールを **run powershell as admin** で開き、特定のバージョンを取得し、最終的に **list installed packages** で **verify installed package** を行います。これらのコマンドがツールボックスにあれば、任意の Windows マシンでライブラリ管理を自動化できます。CI パイプラインのスクリプト化でも、開発環境で欠落した DLL を修正するだけでも活用できます。

次のステップは？ 複数のパッケージを1つのスクリプトに追加してみたり、プロジェクトごとにローカルインストールするための `-Scope` パラメーターを試したり、`Invoke-Expression` と組み合わせてチーム向けの軽量インストーラを作成したりしてください。また、問題が発生した場合は **how to verify package** 手順を思い出してください—`Get-Package` でバージョンを確認するのが問題発見の最速手段です。

PowerShell を楽しんでください！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}