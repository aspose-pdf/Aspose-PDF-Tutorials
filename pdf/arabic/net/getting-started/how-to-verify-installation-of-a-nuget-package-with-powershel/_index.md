---
category: general
date: 2026-03-03
description: كيفية التحقق من تثبيت حزمة NuGet في PowerShell. تعلّم تشغيل PowerShell
  كمسؤول، تثبيت نسخة محددة، وإدارة الحزم بفعالية.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: ar
og_description: كيفية التحقق من تثبيت حزمة NuGet في PowerShell. يوضح لك هذا الدليل
  خطوة بخطوة كيفية تشغيل PowerShell كمسؤول، وتثبيت نسخة محددة، وتأكيد وجود الحزمة.
og_title: كيفية التحقق من تثبيت حزمة NuGet باستخدام PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: كيفية التحقق من تثبيت حزمة NuGet باستخدام PowerShell
url: /ar/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التحقق من تثبيت حزمة NuGet باستخدام PowerShell

التحقق من تثبيت حزمة NuGet في PowerShell هو مهمة شائعة لمسؤولي Windows. إذا تساءلت يومًا ما إذا كانت الحزمة قد تم تثبيتها فعليًا على نظامك، فإن هذا الدليل يوضح لك بالضبط كيفية التحقق من التثبيت—بدون أي تخمين.  

في الدقائق القليلة القادمة سنستعرض تشغيل PowerShell كمسؤول، سحب نسخة محددة من الحزمة، وأخيرًا تأكيد وجود الحزمة على جهازك. ستحصل أيضًا على بعض النصائح لإدارة حزم **PowerShell package management** اليومية التي تحافظ على بيئتك مرتبة.  

قبل أن نبدأ، تأكد من أن لديك جهاز Windows مع PowerShell 7 (أو Windows PowerShell 5.1) واتصال بالإنترنت. لا تحتاج إلى أدوات إضافية؛ كل شيء يعمل مباشرةً من موفر PackageManagement المدمج.

---

![لقطة شاشة لنافذة PowerShell مرتفعة مع أمر Get-Package](/images/verify-installation.png "لقطة شاشة توضح كيفية التحقق من التثبيت في نافذة PowerShell مرتفعة")

## الخطوة 1: تشغيل PowerShell كمسؤول  

تشغيل PowerShell بصلاحيات إدارية هو خط الدفاع الأول ضد المشكلات المتعلقة بالأذونات. عندما **تشغل PowerShell كمسؤول**، يمكن لأمر `Install-Package` كتابة إلى مجلد Program Files وتسجيل الحزمة في الفهرس على مستوى النظام.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **نصيحة احترافية:** قم بتثبيت اختصار “Windows PowerShell (Admin)” على شريط المهام. نقرة واحدة وستكون جاهزًا للانطلاق.

### لماذا الرفع مهم  

بدون الرفع، قد يعود `Install-Package` صامتًا إلى موقع مخصص للمستخدم، مما قد يربك `Get-Package` لاحقًا لأنه يبحث في نطاق النظام افتراضيًا. الرفع يضمن ظهور الحزمة في المكان الذي تتوقعه معظم السكريبتات.

---

## الخطوة 2: تثبيت نسخة محددة من حزمة NuGet  

غالبًا لا تريد أحدث إصدار بل نسخة معروفة جيدة تم اختبار مشروعك معها. نمط **install specific version** بسيط باستخدام العلامة `-Version`.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### تفصيل الأمر  

| المعامل | ما يفعله | لماذا تحتاجه |
|-----------|--------------|-----------------|
| `-Version 25.3` | يثبت رقم البناء الدقيق | يضمن بناءً قابلاً لإعادة الإنتاج |
| `-ProviderName NuGet` | يخبر PowerShell أي موفر يستخدم | يتجنب الغموض إذا تم تسجيل موفرات متعددة |
| `-Scope AllUsers` | يثبت لكل حساب على الجهاز | يعمل مع استعلامات `Get-Package` على مستوى النظام |
| `-Force` | يقمع المطالبات (مفيد في السكريبتات) | يحافظ على سلاسة الأتمتة |

> **احذر:** إذا حذفت `-Version`، سيجلب PowerShell أحدث حزمة، مما قد يسبب تغييرات كسرية.

---

## الخطوة 3: التحقق من التثبيت  

الآن يأتي لحظة الحقيقة: **كيفية التحقق من التثبيت**. الطريقة الأكثر مباشرة هي طلب PowerShell لإظهار الحزمة التي قمت بتثبيتها للتو.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

يجب أن ترى مخرجات مشابهة لـ:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

إذا لم يُرجع الأمر أي شيء، جرّب الاستعلام بنطاق المستخدم:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### طرق التحقق البديلة  

1. **تحقق من مجلد الوحدة** – تُخزن الحزم تحت `C:\Program Files\PackageManagement\Packages\`. ابحث عن مجلد باسم `Aspose.PDF.25.3`.  
2. **استخدم `Find-Package`** – يبحث هذا في المستودع ويمكنه تأكيد توفر النسخة:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **تحقق باستخدام .NET** – حمّل التجميع في PowerShell للتأكد من أن DLL قابل للتحميل:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

إذا نجح أي من هذه الفحوصات، فقد قمت **بالتحقق من التثبيت** بنجاح.

---

## الأخطاء الشائعة وكيفية تجنبها  

- **مزوّد NuGet مفقود** – شغّل `Install-PackageProvider -Name NuGet -Force` أولاً.  
- **حجب ExecutionPolicy** – اضبط مؤقتًا `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` للجلسة.  
- **مشكلات بروكسي الشبكة** – استخدم معلمات `-Proxy` و `-ProxyCredential` إذا كان بيئتك خلف بروكسي مؤسسي.  
- **تعارض الإصدارات** – عندما توجد إصدارات متعددة، حدد `-RequiredVersion` في `Get-Package` لتوضيح الاختيار.

---

## تجميع كل شيء معًا – سكريبت كامل  

فيما يلي سكريبت جاهز للتنفيذ يجمع الخطوات الثلاث، ويتضمن معالجة الأخطاء، ويطبع رسالة نجاح ودية.

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

تشغيل السكريبت ينتج سطرًا واضحًا “✅ Successfully verified installation…”، مؤكدًا أن **كيفية التحقق من التثبيت** تعمل من البداية إلى النهاية.

---

## الخلاصة  

أنت الآن تعرف **كيفية التحقق من التثبيت** لأي حزمة NuGet باستخدام PowerShell، بدءًا من تشغيل جلسة مرتفعة إلى تثبيت نسخة مستهدفة وأخيرًا تأكيد وجود الحزمة. إتقان هذه الخطوات يمنحك الثقة في سير عمل **PowerShell package management** الخاص بك ويمنع الصداع الناتج عن “يبدو أنه مثبت لكنه ليس كذلك” الذي يزعج مطوري Windows غالبًا.  

ما التالي؟ جرّب استبدال `Aspose.PDF` بمكتبة أخرى، جرب `-Scope CurrentUser`، أو اكتب سكريبت لتثبيت مجموعة من الحزم دفعة واحدة لجهاز عمل جديد. وإذا واجهت أي شذوذ، تذكر نصائح استكشاف الأخطاء أعلاه—خصوصًا فحوصات الموفر وExecution‑Policy.  

سcripting سعيد، ولتكن تثبيتاتك دائمًا قابلة للتحقق!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}