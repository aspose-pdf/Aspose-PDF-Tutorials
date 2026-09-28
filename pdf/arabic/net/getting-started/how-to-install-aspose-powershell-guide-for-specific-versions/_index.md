---
category: general
date: 2026-02-10
description: كيفية تثبيت Aspose باستخدام PowerShell. تعلم تشغيل PowerShell كمسؤول،
  تثبيت نسخة محددة، وكيفية سرد الحزم.
draft: false
keywords:
- how to install aspose
- install specific version
- install nuget package powershell
- run powershell as administrator
- how to list packages
language: ar
og_description: كيفية تثبيت Aspose باستخدام PowerShell. يوضح هذا الدليل كيفية تشغيل
  PowerShell كمسؤول، وتثبيت نسخة محددة، وعرض الحزم.
og_title: كيفية تثبيت Aspose – دليل خطوة بخطوة لـ PowerShell
tags:
- powershell
- nuget
- aspose
- devops
title: كيفية تثبيت Aspose – دليل PowerShell للإصدارات المحددة
url: /ar/net/getting-started/how-to-install-aspose-powershell-guide-for-specific-versions/
---

as is. Yes.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تثبيت Aspose – دليل خطوة بخطوة باستخدام PowerShell

هل تساءلت يومًا **كيفية تثبيت aspose** على جهاز Windows جديد؟ أنت لست الوحيد. في العديد من مشاريع .NET حزمة Aspose.PDF NuGet هي المكتبة المفضلة لمعالجة ملفات PDF، لكن خطوة التثبيت قد تبدو غير واضحة—خاصة عندما تحتاج إلى إصدار معين أو تعمل من خادم مقفل.

المهم هو: يمكنك تشغيل Aspose في ثوانٍ، مباشرة من PowerShell. في هذا الدليل سنستعرض كيفية تشغيل PowerShell بالامتيازات المناسبة، سحب إصدار محدد من الحزمة، وتأكيد التثبيت عبر **كيفية سرد الحزم**. في النهاية ستحصل على سطر واحد قابل لإعادة الاستخدام يمكنك وضعه في سكريبتات CI، وستفهم السبب وراء كل خيار.

## المتطلبات المسبقة

- Windows 10/11 (or Windows Server) مع PowerShell 5.1+ مثبت.  
- اتصال بالإنترنت حتى يمكن الوصول إلى مصدر NuGet.  
- اختياري لكن مفيد: **موفر NuGet** (`Install-PackageProvider -Name NuGet -Force`) إذا لم يكن موجودًا بالفعل.  
- حقوق إدارية إذا كان بيئتك تقيد تثبيت الحزم على نطاق النظام.

إذا كان أي من ذلك غير مألوف لك، لا تقلق—معظم أجهزة المطورين تلبي هذه المتطلبات بالفعل. سنغطي أيضًا خطوة **run powershell as administrator**، تحسبًا لأي حاجة.

## الخطوة 1: فتح PowerShell بالحقوق المناسبة

> **نصيحة احترافية:** على محطة عمل مؤسسية قد تحتاج إلى رفع الصلاحيات لتجاوز قيود سياسة التنفيذ.

1. اضغط على **Start**, اكتب **PowerShell**, انقر بزر الماوس الأيمن على النتيجة, واختر **Run as administrator**.  
2. إذا كنت تفضل الاختصار, اضغط `Win + X` → **Windows PowerShell (Admin)**.

```powershell
# Verify you’re running as admin (will output True if elevated)
([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
    [Security.Principal.WindowsBuiltInRole]::Administrator)
```

تشغيل PowerShell كمستخدم مرتفع يضمن أن الحزمة تُثبت في مخزن الحزم العالمي، وهو ما تتوقعه معظم وكلاء البناء.

## الخطوة 2: تثبيت إصدار محدد من Aspose

السبب الرئيسي الذي يجعل المطورين يسألون “**كيفية تثبيت aspose**” هو أنهم يحتاجون إلى إصدار معروف ومستقر—ربما لأن شفرتهم تستهدف نسخة تم إصلاح الأخطاء فيها. أمر `Install-Package` يتيح لك تثبيت نسخة محددة باستخدام العلامة `-Version`.

```powershell
# Step 2: Install Aspose.PDF version 25.3
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Force
```

### لماذا العلامات مهمة

| Flag | Reason |
|------|--------|
| `-Version 25.3` | يضمن حصولك على الإصدار 25.3 بالضبط، متجنبًا التحديثات غير المقصودة. |
| `-ProviderName NuGet` | يخبر PowerShell صراحةً أي موفر يستخدم؛ يتجنب الغموض إذا كان لديك مصادر حزم أخرى. |
| `-Force` | يقمع الرسائل التي قد توقف سكريبتًا آليًا. |

> **حالة خاصة:** إذا كان لديك إصدار أحدث مثبتًا, سيُرفض PowerShell خفض الإصدار ما لم تضف `-AllowDowngrade`. استخدمه باعتدال:

```powershell
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Force -AllowDowngrade
```

## الخطوة 3: التحقق من التثبيت – كيفية سرد الحزم

بعد انتهاء التثبيت, سترغب في التأكد من أن الإصدار الصحيح وصل إلى المكان المتوقع. هنا يأتي دور **كيفية سرد الحزم**.

```powershell
# Step 3: List all installed packages named Aspose.PDF
Get-Package -Name Aspose.PDF
```

المخرجات النموذجية تبدو هكذا:

```
Name                     Version          Source
----                     -------          ------
Aspose.PDF               25.3             nuget.org
```

إذا رأيت إصدارًا مختلفًا, تحقق مرة أخرى من العلامة `-Version` التي استخدمتها مسبقًا, أو نفّذ `Get-PackageSource` لتتأكد من أنك تسحب من مصدر NuGet الصحيح.

### سرد الحزم في نطاق محدد

أحيانًا تريد فقط رؤية الحزم المثبتة للمستخدم الحالي:

```powershell
Get-Package -Name Aspose.PDF -Scope CurrentUser
```

أو, لتدقيق المخزن على مستوى النظام:

```powershell
Get-Package -Name Aspose.PDF -Scope AllUsers
```

هذه الاختيارات مفيدة عند استكشاف الأخطاء المتعلقة بالأذونات.

## الخطوة 4: اختياري – إضافة الحزمة إلى المشروع تلقائيًا

إذا كنت تعمل داخل مجلد حل, يمكن لـ PowerShell أيضًا تحديث ملف `.csproj` لك:

```powershell
# Add Aspose.PDF 25.3 to the current directory’s .csproj
dotnet add package Aspose.PDF --version 25.3
```

هذا الأمر يستخدم .NET CLI بدلاً من موفر NuGet الخاص بـ PowerShell, لكن النتيجة هي نفسها: إدخال مرجع في ملف المشروع. إنها طريقة سريعة للحفاظ على تزامن التحكم في المصدر مع الإصدار المحدد الذي قمت بتثبيته.

## الأخطاء الشائعة وكيفية تجنبها

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `Install-Package : No match was found for the specified search criteria` | موفر NuGet مفقود أو قديم | `Install-PackageProvider -Name NuGet -Force` then `Set-PSRepository -Name 'PSGallery' -InstallationPolicy Trusted` |
| `Access denied` عند التثبيت | عدم تشغيل كمسؤول | أعد فتح PowerShell مع **Run as administrator** |
| ظهور إصدار خاطئ في `Get-Package` | بيانات تعريف مخزنة مؤقتًا | نفّذ `Update-Module -Name PowerShellGet` ثم أعد المحاولة |
| الحزمة تظهر لكن VS لا يمكنه العثور عليها | المشروع لا يزال يستهدف إطار .NET أقدم | قم بترقية إطار الهدف أو ثبّت نسخة Aspose متوافقة |

## النص الكامل الذي يمكنك نسخه‑ولصقه

فيما يلي سكريبت PowerShell ملف واحد يجمع كل ما ناقشناه. احفظه باسم `Install-Aspose.ps1` وشغّله بصلاحيات المسؤول.

```powershell
<# 
.SYNOPSIS
Installs a specific version of Aspose.PDF via PowerShell and verifies the installation.

.DESCRIPTION
This script demonstrates how to run PowerShell as administrator, install a
specific version of the Aspose.PDF NuGet package, and list the installed
packages to confirm success. It also shows optional steps for adding the
package to a .NET project.

.AUTHOR
Your Name – 2026
#>

# 1️⃣ Ensure we are running elevated
if (-not ([Security.Principal.WindowsPrincipal] `
        [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
        [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Error "Please run this script from an elevated PowerShell session."
    exit 1
}

# 2️⃣ Install NuGet provider if missing
if (-not (Get-PackageProvider -Name NuGet -ErrorAction SilentlyContinue)) {
    Write-Host "NuGet provider not found – installing..."
    Install-PackageProvider -Name NuGet -Force | Out-Null
}

# 3️⃣ Install Aspose.PDF version 25.3
$desiredVersion = "25.3"
Write-Host "Installing Aspose.PDF version $desiredVersion ..."
Install-Package Aspose.PDF -Version $desiredVersion -ProviderName NuGet -Force

# 4️⃣ Verify installation
Write-Host "`nVerifying installation..."
$pkg = Get-Package -Name Aspose.PDF -ErrorAction SilentlyContinue
if ($pkg) {
    Write-Host "✅ Aspose.PDF $($pkg.Version) installed successfully."
} else {
    Write-Error "❌ Installation failed – package not found."
}

# 5️⃣ (Optional) Add to .csproj if present
$csproj = Get-ChildItem -Path . -Filter *.csproj -ErrorAction SilentlyContinue | Select-Object -First 1
if ($csproj) {
    Write-Host "`nAdding package reference to $($csproj.Name)..."
    dotnet add $csproj.FullName package Aspose.PDF --version $desiredVersion
}
```

شغّله كالتالي:

```powershell
.\Install-Aspose.ps1
```

سترى علامة تحقق خضراء تؤكد الإصدار, تليها تحديث اختياري للمشروع.

## الخلاصة

لقد غطينا **كيفية تثبيت aspose** باستخدام PowerShell من البداية حتى النهاية: تشغيل جلسة مرتفعة, سحب نسخة دقيقة, وتأكيد النتيجة باستخدام **كيفية سرد الحزم**. السكريبت أعلاه يجعل العملية قابلة لإعادة التكرار—مثالي لأنابيب CI أو لتدريب أعضاء فريق جدد.

بعد ذلك, قد تستكشف **install nuget package powershell** لمكتبات أخرى, أو تغوص في API الخاص بـ Aspose للبدء في إنشاء ملفات PDF. إذا واجهت مشكلة, راجع جدول “الأخطاء الشائعة”; معظم المشكلات تتعلق بالأذونات أو موفر قديم.

برمجة سعيدة, ولتكون تثبيتات NuGet خالية من الأخطاء إلى الأبد! 

![how to install aspose PowerShell screenshot](https://example.com/images/install-aspose-powershell.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}