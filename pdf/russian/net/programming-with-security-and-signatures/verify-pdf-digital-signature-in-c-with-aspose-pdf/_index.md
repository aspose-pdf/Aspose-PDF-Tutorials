---
category: general
date: 2026-03-24
description: Узнайте, как проверять цифровую подпись PDF с помощью Aspose.Pdf для
  C#. Также посмотрите, как перечислять подписи и проверять их действительность в
  несколько простых шагов.
draft: false
keywords:
- verify pdf digital signature
- how to verify signature
- check pdf signature validity
- how to list signatures
language: ru
og_description: Проверьте цифровую подпись PDF в C# с помощью Aspose.Pdf. Следуйте
  этому пошаговому руководству, чтобы вывести список подписей и проверить их действительность.
og_title: Проверка цифровой подписи PDF в C# – Полное руководство
tags:
- Aspose.Pdf
- C#
- Digital Signature
title: Проверка цифровой подписи PDF в C# с помощью Aspose.Pdf
url: /ru/net/programming-with-security-and-signatures/verify-pdf-digital-signature-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Проверка цифровой подписи PDF в C# – Полное руководство

Когда‑то вам нужно было **verify PDF digital signature**, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с этим при работе с подписанными PDF в автоматизированных процессах. Хорошая новость? С Aspose.Pdf для .NET вы можете перечислить каждую подпись в документе и проверить её действительность всего несколькими строками кода.  

В этом руководстве мы пройдем весь процесс — от загрузки подписанного PDF, перечисления его подписей, до проверки каждой из них и интерпретации результатов. К концу вы не только узнаете **how to verify signature** программно, но и поймёте **how to list signatures** и **check PDF signature validity** для крайних сценариев, таких как неподписанные файлы или PDF, защищённые паролем.

## Что вы узнаете

- Как загрузить PDF, содержащий одну или несколько цифровых подписей.  
- Точные вызовы API, необходимые для **list signatures** с использованием `PdfFileSignature.GetSignNames()`.  
- Как вызвать `VerifySignature` и прочитать детальные данные `SignatureInfo`, включая причины компрометации.  
- Советы по работе с несколькими подписями, неподписанными PDF и зашифрованными документами.  
- Готовый к запуску пример кода, который можно вставить в любой проект .NET.

> **Prerequisites** – Вам нужен .NET 6+ (или .NET Framework 4.7.2+) и действующая лицензия Aspose.Pdf для .NET (или временный оценочный ключ). Другие сторонние библиотеки не требуются.

---

## Шаг 1: Установите Aspose.Pdf и подготовьте проект  

Сначала добавьте пакет Aspose.Pdf в ваш проект. Если вы используете .NET CLI, выполните:

```bash
dotnet add package Aspose.Pdf
```

Или в менеджере пакетов NuGet в Visual Studio найдите **Aspose.Pdf** и нажмите *Install*.  

> **Pro tip:** Держите пакет в актуальном состоянии. По состоянию на март 2026 последняя стабильная версия — **23.11**, которая включает улучшения производительности при работе с подписями.

---

## Шаг 2: Загрузите подписанный PDF  

Теперь откроем PDF, который нужно проанализировать. Класс `Document` представляет весь файл, и мы передаём путь к файлу в его конструктор.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Replace with the actual path to your signed PDF
string pdfPath = @"C:\Docs\signed.pdf";

using var pdfDocument = new Document(pdfPath);
```

> **Why this matters:** Загрузка документа внутри блока `using` гарантирует своевременное освобождение файлового дескриптора, предотвращая проблемы с блокировкой файла в длительно работающих сервисах.

---

## Шаг 3: Создайте объект PdfFileSignature  

`PdfFileSignature` — это шлюз ко всем операциям, связанным с подписями. Он требует экземпляр `Document`, который мы только что создали.

```csharp
// Step 3: Initialize the signature helper
var pdfSignature = new PdfFileSignature(pdfDocument);
```

Считайте `PdfFileSignature` как специализированный набор инструментов, умеющий читать, проверять и манипулировать цифровыми подписями, встроенными в PDF.

---

## Шаг 4: Перечислите все имена подписей  

PDF может содержать несколько подписей, каждая из которых имеет уникальное имя. Чтобы **list signatures**, вызовите `GetSignNames()` и пройдитесь по результату.

```csharp
// Step 4: Retrieve every signature name in the document
IEnumerable<string> signatureNames = pdfSignature.GetSignNames();

Console.WriteLine("Found signatures:");
foreach (var name in signatureNames)
{
    Console.WriteLine($"- {name}");
}
```

Если в PDF нет подписей, `GetSignNames()` возвращает пустую коллекцию — идеально для корректной обработки случая «без подписи».

---

## Шаг 5: Проверьте каждую подпись и извлеките детали  

Вот сердце руководства: **check PDF signature validity** для каждого имени, которое мы только что перечислили. Метод `VerifySignature` возвращает Boolean, указывающий на валидность, и заполняет out‑параметр объектом `SignatureDetails`.

```csharp
// Step 5: Verify each signature and print detailed info
foreach (var signatureName in signatureNames)
{
    // Verify the signature; the method also outputs detailed info
    bool isValid = pdfSignature.VerifySignature(signatureName, out var signatureDetails);

    // Optional: grab the compromise reason if the signature is invalid
    string compromiseReason = signatureDetails?.SignatureInfo?.CompromiseReason ?? "None";

    Console.WriteLine(
        $"Signature '{signatureName}' valid: {isValid}, Compromise Reason: {compromiseReason}");
}
```

### Что означает вывод  

- **`isValid`** – `true`, если криптографическая проверка прошла успешно и цепочка сертификатов доверена (в соответствии с системным хранилищем по умолчанию).  
- **`CompromiseReason`** – Заполняется только при неудачной проверке подписи; типичные значения включают *«Certificate revoked»* или *«Hash mismatch»*.  

Если нужно углубиться — например, изучить сертификат подписи, метку времени или время подписи — `signatureDetails.SignatureInfo` содержит эти поля.

---

## Шаг 6: Обработка распространённых граничных случаев  

### 6.1 Не найдено подписей  

```csharp
if (!signatureNames.Any())
{
    Console.WriteLine("The PDF does not contain any digital signatures.");
    // You might decide to abort or continue with unsigned‑PDF logic here.
}
```

### 6.2 PDF, защищённый паролем  

Если PDF зашифрован, сначала загрузите его с паролем:

```csharp
var loadOptions = new LoadOptions { Password = "yourPassword" };
using var protectedDoc = new Document(pdfPath, loadOptions);
var protectedSignature = new PdfFileSignature(protectedDoc);
```

### 6.3 Несколько подписей с разным статусом проверки  

Возможно, одна подпись будет валидна, а другая — нет (например, более старая подпись была изменена позже). Перебор всех имён, как показано в Шаге 5, гарантирует, что вы учтёте каждый случай.

---

## Шаг 7: Полный рабочий пример  

Ниже представлено самостоятельное консольное приложение, которое можно сразу собрать и запустить. Замените `pdfPath` на путь к вашему подписанному PDF.

```csharp
// ------------------------------------------------------------
// Verify PDF Digital Signature – Complete Console Sample
// ------------------------------------------------------------
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF (add password here if needed)
        string pdfPath = @"C:\Docs\signed.pdf";
        using var doc = new Document(pdfPath);

        // 2️⃣ Create the signature helper
        var signatureHelper = new PdfFileSignature(doc);

        // 3️⃣ Get all signature names
        IEnumerable<string> names = signatureHelper.GetSignNames();

        // 4️⃣ If none, inform the user
        if (!names.Any())
        {
            Console.WriteLine("No digital signatures detected in the PDF.");
            return;
        }

        // 5️⃣ Verify each signature
        foreach (var name in names)
        {
            bool valid = signatureHelper.VerifySignature(name, out var details);
            string reason = details?.SignatureInfo?.CompromiseReason ?? "None";

            Console.WriteLine(
                $"Signature '{name}' valid: {valid}, Compromise Reason: {reason}");
        }
    }
}
```

**Ожидаемый вывод в консоли (пример):**

```
Signature 'Signature1' valid: True, Compromise Reason: None
Signature 'Signature2' valid: False, Compromise Reason: Certificate revoked
```

Если PDF не подписан, вы увидите сообщение «No digital signatures detected».

---

## Часто задаваемые вопросы (FAQ)

**Q: Работает ли это с PDF, подписанными в Adobe Acrobat?**  
A: Абсолютно. Aspose.Pdf следует спецификации PDF 1.7, поэтому любая подпись, соответствующая стандарту, включая созданные в Adobe, будет распознана.

**Q: Могу ли я проверять подпись против пользовательского хранилища доверенных сертификатов?**  
A: Да. Вызовите `PdfFileSignature.SetTrustedCertificates()` перед `VerifySignature`. Передайте коллекцию объектов `X509Certificate2`, представляющих ваши доверенные корневые сертификаты.

**Q: Что если нужно игнорировать проверку метки времени?**  
A: Установите `SignatureVerificationOptions.IgnoreTimestamp = true` у экземпляра `PdfFileSignature`.

**Q: Есть ли способ извлечь адрес электронной почты подписанта?**  
A: Свойство `SignatureInfo.SignerInfo.Email` содержит эту информацию, если сертификат подписанта её включает.

---

## Заключение  

Теперь у вас есть полный, готовый к продакшену рецепт для **verify PDF digital signature** с помощью Aspose.Pdf в C#. Следуя семи шагам выше, вы сможете **list signatures**, **check PDF signature validity** и корректно обрабатывать несколько или отсутствующие подписи.  

Дальше вы можете исследовать **how to verify signature** против корпоративного PKI или углубиться в **how to list signatures** в сервисе пакетной обработки, сканирующем сотни PDF каждую ночь. В любом случае полученные концепции станут надёжной основой.

Есть дополнительные вопросы или хотите поделиться интересным кейсом? Оставьте комментарий ниже или напишите мне в Git

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}