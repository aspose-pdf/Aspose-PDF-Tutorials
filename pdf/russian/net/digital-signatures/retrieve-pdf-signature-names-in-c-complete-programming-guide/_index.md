---
category: general
date: 2026-02-25
description: Быстро получайте имена подписей PDF в C#. Узнайте, как читать подписи
  PDF, перечислять подписи PDF и отображать подписи PDF с помощью Aspose.PDF.
draft: false
keywords:
- retrieve pdf signature names
- read pdf signatures
- list pdf signatures
- how to list signatures
- display pdf signatures
language: ru
og_description: Быстро получайте имена подписей PDF в C#. Это руководство показывает,
  как читать подписи PDF, перечислять подписи PDF и отображать подписи PDF с понятными
  примерами кода.
og_title: Получение имён подписей PDF в C# – пошаговое руководство
tags:
- pdf
- csharp
- aspnet
- digital-signature
title: Получить имена подписей PDF в C# – Полное руководство по программированию
url: /ru/net/digital-signatures/retrieve-pdf-signature-names-in-c-complete-programming-guide/
---



{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Получение имён подписей PDF в C# – Полное руководство по программированию

Нужно **получить имена подписей PDF** из подписанного документа? Вы не один задаётесь этим вопросом. Во многих приложениях с жёсткими требованиями к соответствию необходимо *читать подписи PDF*, чтобы проверить, кто что подписал, и самый быстрый способ в .NET — перечислить поля подписей с помощью Aspose.PDF.  

В этом руководстве мы пройдём реальный пример, который **получает имена подписей PDF**, покажет, как **перечислить подписи PDF**, и даже продемонстрирует, как **отобразить подписи PDF** в консоли. К концу вы получите автономный фрагмент кода, который можно вставить в любой проект C# — без «см. документацию» ссылок.

## Что понадобится

- **.NET 6.0** или новее (код также работает на .NET Framework 4.6+).  
- NuGet‑пакет **Aspose.PDF for .NET** (`Aspose.PDF`) — библиотека, предоставляющая классы `Document` и `PdfFileSignature`.  
- **Подписанный PDF** файл, к которому можно обратиться (назовём его `signed.pdf`).  
- Любая IDE по вашему выбору (Visual Studio, Rider, VS Code — решать вам).

> **Pro tip:** Если у вас нет готового подписанного PDF, его можно создать в Adobe Acrobat или воспользоваться собственным API подписи Aspose; логика извлечения остаётся той же.

## Обзор процесса

1. **Открыть** PDF‑документ безопасно внутри блока `using`.  
2. **Создать экземпляр** `PdfFileSignature`, фасад, который умеет работать с подписями.  
3. **Вызвать** `GetSignatureNames()`, чтобы получить каждый идентификатор подписи.  
4. **Пройтись** по полученной коллекции и **отобразить** каждое имя в консоли.

Это весь процесс — ничего лишнего, ничего недостающего. Приступим к каждому шагу.

---

## Получение имён подписей PDF – пошагово

Ниже приведена **полная, готовая к запуску программа**. Скопируйте её в новый консольный проект и нажмите **F5**.

```csharp
// ---------------------------------------------------------------
// Retrieve PDF signature names with Aspose.PDF for .NET
// ---------------------------------------------------------------
using System;
using Aspose.Pdf;               // Core PDF classes
using Aspose.Pdf.Facades;       // Signature façade

namespace PdfSignatureDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 1: Open the signed PDF document
            // Replace the path with your actual file location.
            using (var pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf"))
            {
                // 👉 Step 2: Create a signature handler for the document
                using (var pdfSignature = new PdfFileSignature(pdfDocument))
                {
                    // 👉 Step 3: Retrieve all signature names present in the PDF
                    var signatureNames = pdfSignature.GetSignatureNames();

                    // 👉 Step 4: Output each signature name to the console
                    Console.WriteLine("=== PDF Signature Names ===");
                    foreach (var signatureName in signatureNames)
                    {
                        Console.WriteLine($"- {signatureName}");
                    }

                    // Edge case handling: no signatures found
                    if (signatureNames.Count == 0)
                    {
                        Console.WriteLine("No signatures were detected in this PDF.");
                    }
                }
            }

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

### Пояснение к каждому блоку

| Шаг | Что происходит | Почему это важно |
|------|----------------|------------------|
| **Шаг 1** | `new Document("…/signed.pdf")` загружает файл в память. | Открытие внутри `using` гарантирует освобождение файлового дескриптора, предотвращая блокировку файла в Windows. |
| **Шаг 2** | `PdfFileSignature` оборачивает документ и раскрывает методы, связанные с подписями. | Этот фасад абстрагирует низкоуровневые детали PDF, позволяя **читать подписи PDF** одним вызовом. |
| **Шаг 3** | `GetSignatureNames()` возвращает `StringCollection` со всеми идентификаторами полей подписей. | Коллекция содержит *имена*, которые понадобятся, когда вы захотите **перечислить подписи PDF** или проверить конкретную. |
| **Шаг 4** | Простой `foreach` выводит каждое имя. | Вывод имён упрощает отладку и удовлетворяет требование «**отобразить подписи PDF**». |

#### Особые случаи и советы

- **Зашифрованные PDF** — если ваш PDF защищён паролем, передайте пароль в конструктор `Document`: `new Document(path, new LoadOptions { Password = "secret" })`.  
- **Отсутствие подписей** — в примере уже проверяется `signatureNames.Count == 0` и пользователь получает соответствующее сообщение.  
- **Большие PDF** — загрузка огромного файла может потребовать много памяти; рассмотрите использование `LoadOptions` с `MemoryUsageSetting` для потоковой загрузки вместо полной.  

---

## Чтение подписей PDF с Aspose.PDF

Если вам интересно *как читать подписи PDF* помимо их имён, тот же класс `PdfFileSignature` может предоставить **детали подписи** (имя подписанта, время подписи, сертификат). Вот быстрый фрагмент:

```csharp
foreach (var name in signatureNames)
{
    // Retrieve the signature object for deeper inspection
    var signature = pdfSignature.GetSignature(name);
    Console.WriteLine($"Signature: {name}");
    Console.WriteLine($"  Signer: {signature.Signer}");
    Console.WriteLine($"  Signing Time: {signature.SignTime}");
    Console.WriteLine($"  Reason: {signature.Reason}");
}
```

> **Почему это важно:** В аудиторских журналах часто требуется не только имя поля, но и **кто**, **когда** и **почему**. Эта дополнительная информация помогает формировать отчёты о соответствии без привлечения сторонних библиотек.

---

## Безопасное перечисление подписей PDF — типичные подводные камни

При **перечислении подписей PDF** учитывайте следующие нюансы:

1. **Дублирующиеся имена полей** — в некоторых PDF одно и то же логическое имя может встречаться на разных страницах. `GetSignatureNames()` возвращает каждый уникальный идентификатор только один раз, поэтому двойного подсчёта не будет.  
2. **Отсоединённые подписи** — поле подписи может существовать без прикреплённой криптографической подписи. В этом случае `signature.IsSigned` будет `false`.  
3. **Совместимость версий** — старые PDF (до 1.5) могут хранить подписи нестандартным способом. Aspose.PDF обрабатывает большинство случаев, но тестировать на наследуемых файлах всё же рекомендуется.

---

## Отображение подписей PDF — делаем вывод удобным

Консольный вывод выше рабочий, но вы можете захотеть **красивую таблицу** для UI‑приложений. Вот небольшой помощник, использующий форматирование `Console.WriteLine`:

```csharp
Console.WriteLine("\n{0,-30} {1,-20} {2,-25}", "Signature Name", "Signer", "Signing Time");
Console.WriteLine(new string('-', 80));

foreach (var name in signatureNames)
{
    var sig = pdfSignature.GetSignature(name);
    Console.WriteLine("{0,-30} {1,-20} {2,-25}",
        name,
        sig.Signer ?? "N/A",
        sig.SignTime?.ToString("u") ?? "N/A");
}
```

Получающаяся таблица:

```
Signature Name                 Signer               Signing Time             
--------------------------------------------------------------------------------
Signature1                     Alice                2024-11-03 14:22:01Z     
Signature2                     Bob                  2024-11-04 09:15:45Z     
```

Это чистый способ **отобразить подписи PDF** в консоли или файле журнала.

---

## Полный рабочий пример в обзоре

Объединив всё, окончательная программа выглядит так (включая необязательное детальное перечисление):

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace PdfSignatureDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            using (var pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf"))
            using (var pdfSignature = new PdfFileSignature(pdfDocument))
            {
                var signatureNames = pdfSignature.GetSignatureNames();

                Console.WriteLine("=== PDF Signature Names ===");
                foreach (var name in signatureNames)
                    Console.WriteLine($"- {name}");

                if (signatureNames.Count == 0)
                {
                    Console.WriteLine("No signatures were detected in this PDF.");
                }
                else
                {
                    // Detailed listing (optional)
                    Console.WriteLine("\n{0,-30} {1,-20} {2,-25}", "Signature Name", "Signer", "Signing Time");
                    Console.WriteLine(new string('-', 80));

                    foreach (var name in signatureNames)
                    {
                        var sig = pdfSignature.GetSignature(name);
                        Console.WriteLine("{0,-30} {1,-20} {2,-25}",
                            name,
                            sig.Signer ?? "N/A",
                            sig.SignTime?.ToString("u") ?? "N/A");
                    }
                }
            }

            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Ожидаемый вывод** (при наличии двух подписей):

```
=== PDF Signature Names ===
- Signature1
- Signature2

Signature Name                 Signer               Signing Time             
--------------------------------------------------------------------------------
Signature1                     Alice                2024-11-03 14:22:01Z     
Signature2                     Bob                  2024-11-04 09:15:45Z     
```

Если в PDF **нет подписей**, вы увидите:

```
=== PDF Signature Names ===
No signatures were detected in this PDF.
```

---

## Часто задаваемые вопросы

**В: Работает ли это с PDF, подписанными по PAdES?**  
О: Да. Aspose.PDF проверяет как классические PKCS#7, так и PAdES подписи. Объект `GetSignature` раскрывает цепочку сертификатов для дальнейшей верификации.

**В: Что делать, если PDF защищён паролем?**  
О: Передайте пароль через `LoadOptions` при создании экземпляра `Document`:

```csharp
var loadOpts = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("signed.pdf", loadOpts);
```

**В: Можно ли получать подписи из потока, а не из файла?**  
О: Конечно. Используйте перегрузку `new Document(Stream)` и оберните поток в блок `using`.

---

## Следующие шаги и смежные темы

Теперь, когда вы умеете **получать имена подписей PDF**, вы можете перейти к более продвинутым сценариям: проверка целостности, извлечение сертификатов, построение отчётов о соответствии и т.д.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}