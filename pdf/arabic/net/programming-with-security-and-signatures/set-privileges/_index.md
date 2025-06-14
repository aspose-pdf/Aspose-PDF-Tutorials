---
"description": "تعرّف على كيفية ضبط صلاحيات PDF باستخدام Aspose.PDF لـ .NET من خلال هذا الدليل المفصل. وفّر الحماية لمستنداتك بفعالية."
"linktitle": "تعيين الامتيازات في ملف PDF"
"second_title": "مرجع Aspose.PDF لـ API .NET"
"title": "تعيين الامتيازات في ملف PDF"
"url": "/ar/net/programming-with-security-and-signatures/set-privileges/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تعيين الامتيازات في ملف PDF

## مقدمة

في عصرنا الرقمي، أصبحت إدارة أمان المستندات أكثر أهمية من أي وقت مضى. سواءً كنتَ تحمي بياناتك الحساسة أو تضمن الامتثال للوائح، فإن تحديد الصلاحيات المناسبة لملفات PDF أمرٌ بالغ الأهمية. سترشدك هذه المقالة خلال عملية تقييد الصلاحيات في ملف PDF باستخدام Aspose.PDF لـ .NET. إذا تساءلتَ يومًا عن كيفية منع التحرير أو الطباعة غير المصرح بها لمستند مع السماح للمستخدمين بقراءته، فأنتَ في المكان المناسب!

## المتطلبات الأساسية

قبل أن نتعمق في التفاصيل المتعلقة بإعداد الامتيازات، هناك بعض الأشياء التي ستحتاج إليها للبدء:

### 1. إطار عمل .NET

تأكد من أن لديك بيئة .NET تعمل. يدعم Aspose.PDF for .NET إصدارات مختلفة من .NET Framework، لذا تأكد من توافق مشروعك.

### 2. مكتبة Aspose.PDF لـ .NET

يجب تثبيت مكتبة Aspose.PDF. إذا لم تقم بذلك بعد، فتوجه إلى [إصدار Aspose PDF](https://releases.aspose.com/pdf/net/) الصفحة لتحميل الإصدار الأحدث.

### 3. وثيقة PDF المصدر

جهّز ملف PDF المصدر. لأغراض التوضيح، لنستخدم ملف إدخال باسم `input.pdf`يمكنك إنشاء ملف PDF بسيط باستخدام أي محرر نصوص أو تنزيل واحد.

### 4. بيئة التطوير الخاصة بك

تأكد من إعداد مشروعك في بيئة التطوير المتكاملة المفضلة لديك (يعمل Visual Studio بشكل رائع!) وتأكد من قدرتك على تشغيل تطبيقات .NET وتصحيح أخطائها.

## استيراد الحزم

لاستخدام مكتبة Aspose.PDF، ستحتاج أولًا إلى استيراد الحزم المطلوبة إلى مشروعك. مساحة الاسم الرئيسية التي ستعمل بها هي `Aspose.Pdf`.

إليك كيفية القيام بذلك:

1. افتح مشروعك في Visual Studio.
2. في مستكشف الحلول، انقر بزر الماوس الأيمن فوق مشروعك وحدد "إدارة حزم NuGet".
3. ابحث عن "Aspose.PDF" وقم بتثبيته.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
```

بمجرد حصولك على الحزمة في مكانها، فأنت جاهز لبدء الترميز!

الآن، لنُقسّم الأمر إلى خطوات عملية يُمكنك اتباعها. سيساعدك هذا النهج العملي على فهم كيفية ضبط الصلاحيات في مستندات PDF الخاصة بك بشكل كامل.

## الخطوة 1: تحديد دليل المستندات

أولاً، عليك تحديد مسار مجلد المستندات. هذا هو المكان الذي ستُحفظ فيه ملفات PDF المدخلة والمخرجة.

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
```
يستبدل `"YOUR DOCUMENTS DIRECTORY"` مع الدليل الفعلي على نظامك الذي قمت بتخزين بياناتك فيه `input.pdf`.

## الخطوة 2: تحميل ملف PDF المصدر

بعد تعيين الدليل، فإن الخطوة التالية هي تحميل مستند PDF الذي تريد تعديله.

```csharp
using (Document document = new Document(dataDir + "input.pdf"))
{
    // سوف يستمر الكود الخاص بك هنا
}
```
وهنا حيث نستخدم `using` بيان لإدارة الموارد. هذا سيضمن إغلاق مستندك بشكل صحيح والتخلص منه بعد الانتهاء من معالجته.

## الخطوة 3: إنشاء كائن امتيازات المستند

الآن بعد أن تم تحميل المستند، حان الوقت لإنشاء مثيل من `DocumentPrivilege` سيسمح لك هذا بتحديد الأذونات التي سيتم تعيينها.

```csharp
DocumentPrivilege documentPrivilege = DocumentPrivilege.ForbidAll;
```
افتراضيًا، جميع الصلاحيات محظورة. هذا يعني أنه لا يمكن لأي شخص تعديل أو طباعة أو نسخ المستند إلا بموافقتك الصريحة.

## الخطوة 4: تعيين الامتيازات المسموح بها

بعد ذلك، يمكنك تحديد الصلاحيات التي تريد السماح بها. في هذا المثال، سنسمح فقط بقراءة الشاشة.

```csharp
documentPrivilege.AllowScreenReaders = true;
```
يُتيح هذا الخط تحديدًا إمكانية الوصول إلى برامج قراءة الشاشة، وهو أمر بالغ الأهمية للمستخدمين ذوي الإعاقات البصرية. يمكنك تعديل الإعدادات الأخرى وفقًا لاحتياجاتك.

## الخطوة 5: تشفير ملف PDF

الآن يأتي الجزء الأكثر أهمية: تشفير المستند بكلمات مرور المستخدم والمالك.

```csharp
document.Encrypt("user", "owner", documentPrivilege, CryptoAlgorithm.AESx128, false);
```
يستبدل `"user"` و `"owner"` بكلمات مرور من اختيارك. سيحتاج المستخدم إلى كلمة مرور لعرض المستند، بينما تمنح كلمة مرور المالك التحكم الكامل في الصلاحيات. 

## الخطوة 6: حفظ المستند المحدث

وأخيرًا، بمجرد الانتهاء من إجراء كافة التعديلات، لا تنس حفظ ملف PDF المحدث.

```csharp
document.Save(dataDir + "SetPrivileges_out.pdf");
```
يحفظ هذا السطر التغييرات التي أجريتها على ملف جديد يسمى `SetPrivileges_out.pdf` في نفس الدليل. من الأفضل دائمًا الاحتفاظ بالأصل سليمًا!

## خاتمة

ها قد انتهيت! لقد نجحت في ضبط صلاحيات ملف PDF باستخدام Aspose.PDF لـ .NET. ببضعة أسطر برمجية فقط، يمكنك تأمين مستنداتك مع ضمان إمكانية الوصول إليها لمن يحتاجها. إن فهم كيفية إدارة صلاحيات المستندات لا يُعزز أمان مستنداتك فحسب، بل يُحسّن أيضًا تجربة المستخدم. 

## الأسئلة الشائعة

### ما هي امتيازات المستند في ملف PDF؟  
تحدد امتيازات المستند الإجراءات التي يمكن للمستخدمين تنفيذها على ملف PDF، مثل التحرير أو النسخ أو الطباعة.

### كيف أقوم بتثبيت مكتبة Aspose.PDF؟  
يمكنك تثبيته عبر NuGet في Visual Studio. ابحث عن "Aspose.PDF" في مدير حزم NuGet.

### هل يمكنني السماح بامتيازات متعددة في وقت واحد؟  
نعم، يمكنك تعيين أذونات متعددة عن طريق ضبط `DocumentPrivilege` الإعدادات وفقا لذلك.

### ما هي خوارزميات التشفير التي يدعمها Aspose؟  
يدعم Aspose.PDF خوارزميات مختلفة، بما في ذلك AES-128، وAES-256، وRC4 (40 بت و128 بت).

### هل هناك نسخة تجريبية من Aspose.PDF؟  
نعم، يمكنك الحصول على نسخة تجريبية مجانية من [نسخة تجريبية مجانية من Aspose PDF](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}