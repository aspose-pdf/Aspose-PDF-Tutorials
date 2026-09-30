---
category: general
date: 2026-02-20
description: تعلم كيفية تثبيت حزم nuget باستخدام PowerShell، تشغيل PowerShell كمسؤول،
  سرد الحزم المثبتة والتحقق من الحزمة المثبتة في دقائق.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: ar
og_description: كيفية تثبيت حزم NuGet باستخدام PowerShell، تشغيل PowerShell كمسؤول،
  سرد الحزم المثبتة والتحقق من الحزمة المثبتة — دليل كامل.
og_title: كيفية تثبيت حزم NuGet عبر PowerShell – دليل سريع
tags:
- PowerShell
- NuGet
- Package Management
title: كيفية تثبيت حزم NuGet عبر PowerShell – خطوة بخطوة
url: /ar/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---




{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تثبيت حزم nuget عبر PowerShell – خطوة بخطوة

هل تساءلت يومًا **كيفية تثبيت nuget** الحزم دون فتح Visual Studio؟ أنت لست وحدك. في العديد من خطوط CI أو على الأجهزة الجديدة، أسرع طريقة هي الانتقال إلى PowerShell—يفضل *run powershell as admin*—وترك مدير الحزم يقوم بعمله.

في هذا الدرس سنستعرض العملية بالكامل: فتح وحدة التحكم الصحيحة، تنزيل نسخة محددة من مكتبة، وأخيرًا التأكد من أن الحزمة تم تثبيتها فعليًا على نظامك. في النهاية ستتمكن من **list installed packages**, تعرف **how to verify package**, وتشعر بالثقة أن خطوة **verify installed package** نجحت في كل مرة.

## ما ستتعلمه

- كيفية تشغيل PowerShell بالأذونات الصحيحة.  
- الصياغة الدقيقة لأمر `Install-Package` لـ NuGet.  
- طرق **list installed packages** وتأكيد أرقام الإصدارات.  
- المشكلات الشائعة (غياب صلاحيات المسؤول، عدم تطابق الإصدارات) وكيفية تجنّبها.  

لا تحتاج إلى خبرة سابقة مع NuGet، فقط جهاز Windows يعمل وقليل من الفضول.

---

## كيفية تثبيت حزم NuGet باستخدام PowerShell

> **نصيحة احترافية:** إذا كنت تضيف نفس الحزم بشكل متكرر، فكر في إضافتها إلى ملف سكريبت وتشغيله باستخدام `-File`. سيوفر عليك كتابة السطر نفسه مرارًا وتكرارًا.

### الخطوة 1: فتح PowerShell بالأذونات اللازمة

أول شيء تحتاج إلى القيام به هو **run powershell as admin**. بدون صلاحيات مرتفعة قد يفشل الأمر `Install-Package` بصمت أو يطلب تأكيدًا لا ترغب في التعامل معه.

1. انقر على زر **Start**.  
2. اكتب **PowerShell**.  
3. انقر بزر الماوس الأيمن على *Windows PowerShell* واختر **Run as administrator**.  

ستظهر لك نافذة UAC؛ انقر **Yes**. الآن لديك جلسة ذات صلاحيات جاهزة لتثبيت الحزم.

> *لماذا المسؤول؟*  
> يكتب NuGet الملفات إلى مجلد الحزم العالمي (`C:\Program Files\PackageManagement\NuGet\Packages` بشكل افتراضي). هذا الموقع محمي، لذا فقط عملية ذات صلاحيات مرتفعة يمكنها الكتابة هناك.

### الخطوة 2: تثبيت حزمة NuGet المطلوبة والإصدار

With the console open, the core command is straightforward:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` هو الغلاف PowerShell لعميل NuGet.  
- `-Version` يحدد النسخة الدقيقة التي تحتاجها، مما يمنع الترقيات غير المقصودة.  

إذا حذفت `-Version`، سيقوم PowerShell بجلب أحدث إصدار ثابت—أحيانًا يكون ذلك مناسبًا، وأحيانًا تريد النسخة الدقيقة التي اختبرت معها.

#### ماذا يحدث خلف الكواليس؟

يتواصل PowerShell مع مصدر الحزمة المكوَّن (افتراضيًا `https://www.nuget.org/api/v2`) ويحمِّل ملف `.nupkg`. ثم يستخرج ملفات DLL إلى مجلد الحزم العالمي ويسجِّل الحزمة مع موفر الحزم المحلي. عادةً ما تنتهي العملية خلال بضع ثوانٍ ما لم تكن على شبكة بطيئة.

### الخطوة 3: التحقق من أن الحزمة تم تثبيتها بنجاح

الآن بعد أن أصبحت الحزمة على القرص، ربما تسأل، **"كيف أتحقق من الحزمة؟"** الجواب يكمن في استعلام بسيط:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

تشغيل هذا يعيد شيئًا مثل:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

هذا الإخراج يؤكد شيئين:

1. الحزمة **Aspose.PDF** موجودة.  
2. نسختها تطابق ما طلبته، مما يلبي متطلب **verify installed package**.

إذا أردت رؤية *كل* حزمة على الجهاز، احذف عامل تصفية `-Name`:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

هذا العرض **list installed packages** مفيد للمراجعات أو عندما تحتاج إلى تنظيف المكتبات القديمة.

### الخطوة 4: اختياري – معالجة الحالات الخاصة

#### أ) الحزمة غير موجودة أو عدم تطابق الإصدار

إذا رد PowerShell بـ *"Package not found"* أو *"Version not available"*، تحقق مرة أخرى من التهجئة ورقم الإصدار. NuGet غير حساس لحالة الأحرف، لكن وجود مساحة زائدة سيكسر الأمر.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### ب) التشغيل بدون صلاحيات المسؤول

إذا نسيت **run powershell as admin**، سيظهر الخطأ بسبب عدم وجود صلاحيات. الحل هو إغلاق النافذة وإعادة فتحها بصلاحيات مرتفعة—لا حاجة لإعادة تثبيت أي شيء.

#### ج) استخدام مصدر مخصص

في بيئات الشركات قد يكون لديك مصدر NuGet داخلي:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

خطوة التحقق تظل كما هي؛ فقط تذكر تضمين `-Source` عند التثبيت.

---

## جدول مرجع سريع

| الإجراء                              | PowerShell command                                          | سبب الأهمية |
|-------------------------------------|-------------------------------------------------------------|----------------|
| فتح وحدة تحكم مرتفعة               | *Run PowerShell as Administrator*                           | مطلوب للتثبيت العالمي |
| تثبيت نسخة محددة                    | `Install-Package <pkg> -Version <x.y.z>`                    | يضمن بناءً قابلًا لإعادة الإنتاج |
| قائمة حزمة واحدة                    | `Get-Package -Name <pkg>`                                    | يؤكد **how to verify package** |
| قائمة جميع حزم NuGet                | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| مفيد لـ **list installed packages** |
| البحث عن الإصدارات المتاحة           | `Find-Package <pkg> -AllVersions`                           | يساعد عندما يكون الإصدار غير معروف |

## الخاتمة

لقد غطينا **how to install nuget** الحزم باستخدام PowerShell من البداية إلى النهاية—فتح وحدة التحكم **run powershell as admin**، تنزيل نسخة محددة، وأخيرًا **list installed packages** لـ **verify installed package**. مع هذه الأوامر في صندوق أدواتك يمكنك أتمتة إدارة المكتبات على أي جهاز Windows، سواء كنت تكتب سكريبتًا لخط أنابيب CI أو فقط تصلح DLL مفقودًا على جهاز التطوير الخاص بك.

الخطوات التالية؟ جرّب إضافة عدة حزم إلى سكريبت واحد، استكشف معامل `-Scope` لتثبيت محلي لمشروع، أو اجمع هذه الأوامر مع `Invoke-Expression` لبناء مثبت خفيف لفريقك. وإذا واجهت مشكلة، تذكر خطوة **how to verify package**—رؤية الإصدار في `Get-Package` غالبًا ما تكون أسرع طريقة لاكتشاف المشكلة.

استمتع باستخدام PowerShell! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}