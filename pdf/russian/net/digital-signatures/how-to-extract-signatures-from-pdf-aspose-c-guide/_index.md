---
category: general
date: 2026-04-02
description: Узнайте, как извлекать подписи, добавлять поле, добавлять пустую страницу
  в PDF, как добавлять виджет и сохранять прозрачность PDF с помощью Aspose.Pdf на
  C#.
draft: false
keywords:
- how to extract signatures
- how to add field
- add blank page pdf
- how to add widget
- preserve transparency pdf
language: ru
og_description: Как извлечь подписи из PDF и выполнить связанные задачи, такие как
  добавление полей, пустых страниц, виджетов и сохранение прозрачности с помощью Aspose.Pdf.
og_title: Как извлечь подписи из PDF – руководство Aspose C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Как извлечь подписи из PDF – руководство Aspose C#
url: /ru/net/digital-signatures/how-to-extract-signatures-from-pdf-aspose-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь подписи из PDF – Руководство Aspose C#  

**Как извлечь подписи из PDF** – это распространённая задача при автоматизации обработки контрактов, согласования счетов или любого рабочего процесса, зависящего от цифровых подписей.  
В этом руководстве мы также рассмотрим **how to add field**, **add blank page PDF**, **how to add widget** и **preserve transparency PDF**, используя библиотеку Aspose.Pdf для .NET.

Представьте, что каждую ночь вы получаете десятки подписанных PDF‑файлов; открывать каждый файл вручную для проверки подписей было бы кошмаром. С помощью нескольких строк кода на C# вы можете программно получить имена подписей, сохранить оригинальную графику нетронутой и даже обогатить документ новыми полями формы — всё без нарушения существующей прозрачности или цветовых профилей.

> **Что вы получите:** полностью готовый, исполняемый пример, который конвертирует PDF в PDF/X‑4 (сохраняя прозрачность), извлекает все встроенные имена подписей, добавляет пустую страницу и создаёт текстовое поле формы, отображающееся в двух местах на одной странице.

## Предварительные требования

- .NET 6.0 или новее (код также работает с .NET Framework)  
- Aspose.Pdf for .NET **v25.2** или новее (необходимо для `GetSignatureNames()`)  
- Проект Visual Studio или любой другой IDE для C#  
- Три образца PDF в папке, которой вы управляете:  
  - `source.pdf` – любой PDF, который вы хотите конвертировать, сохраняя прозрачность  
  - `signed.pdf` – PDF, уже содержащий цифровые подписи  
  - (необязательно) пустая папка для файлов вывода  

> **Pro tip:** Если у вас ещё нет лицензированной копии, вы можете запросить бесплатную временную лицензию на сайте Aspose. Бесплатный режим подходит для тестирования, но добавляет водяной знак.

## Шаг 1 – Сохранить прозрачность PDF, конвертируя в PDF/X‑4

Прозрачность и встроенные цветовые профили часто теряются при «уплощении» PDF. Конвертация в **PDF/X‑4** сохраняет эти визуальные элементы, что критично для документов, готовых к печати.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// 1️⃣ Convert source.pdf → PDF/X‑4 (preserves transparency & color profiles)
var conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_4,          // Target format
    ConvertErrorAction.Delete  // Remove pages that cause conversion errors
);

using (var sourceDoc = new Document("YOUR_DIRECTORY/source.pdf"))
{
    sourceDoc.Convert(conversionOptions);
    sourceDoc.Save("YOUR_DIRECTORY/toPdfX4.pdf");
}
```

**Почему это важно:**  
PDF/X‑4 — это ISO‑стандарт для графических PDF, сохраняющих живую прозрачность. Используя `PdfFormatConversionOptions`, вы избегаете распространённой ошибки растеризации прозрачных объектов, что может резко увеличить размер файла и ухудшить качество.

## Шаг 2 – Как извлечь подписи из PDF

Aspose внедрила `GetSignatureNames()` в версии 25.2, делая извлечение подписей однострочным вызовом. Метод возвращает массив логических имён, присвоенных каждому полю цифровой подписи.

```csharp
using Aspose.Pdf;

// 2️⃣ Pull out every signature name from signed.pdf
using (var signedDoc = new Document("YOUR_DIRECTORY/signed.pdf"))
{
    // Returns strings like "Signature1", "EmployeeSignature", etc.
    string[] signatureNames = signedDoc.GetSignatureNames();   // new method in 25.2

    // Show the names in the console – you could store them in a DB instead
    Console.WriteLine("Found signatures: " + string.Join(", ", signatureNames));
}
```

**Что ожидать:** Если `signed.pdf` содержит две подписи с именами *ManagerSig* и *ClientSig*, консоль выведет:

```
Found signatures: ManagerSig, ClientSig
```

**Обработка граничных случаев:**  
- Если в PDF нет подписей, `GetSignatureNames()` возвращает пустой массив — исключение не генерируется.  
- Для PDF с повреждёнными полями подписи вы можете обернуть вызов в `try/catch` и записать ошибку, не прерывая весь процесс.

## Шаг 3 – Добавить пустую страницу PDF и создать TextBox с несколькими виджетами

Добавление новой страницы простое, но **how to add field** и **how to add widget** вместе требуют небольшого уточнения. *Виджет* — это визуальное представление поля формы; к одному логическому полю можно привязать несколько виджетов, позволяя одинаковым данным отображаться в разных местах.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// 3️⃣ Build a fresh document, add a blank page, then a textbox with two widgets
using (var newDoc = new Document())
{
    // ---- Add a blank page -------------------------------------------------
    var page = newDoc.Pages.Add();   // This is the "add blank page pdf" step

    // ---- Define the primary widget (the actual appearance) ---------------
    var textBox = new TextBoxField(page, new Rectangle(100, 600, 300, 650))
    {
        PartialName = "Comments",               // logical name of the field
        Value = "Enter your comment here"       // default value
    };

    // ---- Add a second widget at a different location ----------------------
    var secondWidget = new WidgetAnnotation(page, new Rectangle(100, 500, 300, 550));
    textBox.Widgets.Add(secondWidget); // This is the "how to add widget" part

    // ---- Register the field with the document's form collection -----------
    newDoc.Form.Add(textBox, "Comments");

    // ---- Save the result --------------------------------------------------
    newDoc.Save("YOUR_DIRECTORY/TextBoxMultipleWidgets.pdf");
}
```

**Зачем использовать несколько виджетов?**  
Предположим, вам нужно, чтобы один и тот же комментарий отображался и на лицевой, и на обратной стороне контракта. Привязав два виджета к одному полю, любое изменение, сделанное пользователем в одном месте, автоматически обновит другое.

**Распространённые подводные камни:**  
- Если забыть добавить поле в `newDoc.Form`, виджет будет невидим в PDF‑просмотрщиках.  
- Использование одинаковых координат прямоугольника для обоих виджетов наложит их друг на друга — убедитесь, что значения `Rectangle` различаются.

## Шаг 4 – Собираем всё вместе: полный, исполняемый пример

Ниже представлен единый программный файл, который последовательно выполняет каждый из описанных шагов. Скопируйте его в новый консольный проект, скорректируйте пути и запустите.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;

namespace AsposePdfDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Preserve transparency by converting to PDF/X‑4
            // -----------------------------------------------------------------
            var conversionOptions = new PdfFormatConversionOptions(
                PdfFormat.PDF_X_4,
                ConvertErrorAction.Delete);

            using (var sourceDoc = new Document("YOUR_DIRECTORY/source.pdf"))
            {
                sourceDoc.Convert(conversionOptions);
                sourceDoc.Save("YOUR_DIRECTORY/toPdfX4.pdf");
                Console.WriteLine("✅ PDF/X‑4 conversion complete (transparency preserved).");
            }

            // -----------------------------------------------------------------
            // 2️⃣ Extract signature names
            // -----------------------------------------------------------------
            using (var signedDoc = new Document("YOUR_DIRECTORY/signed.pdf"))
            {
                string[] signatureNames = signedDoc.GetSignatureNames(); // new in 25.2
                if (signatureNames.Length == 0)
                    Console.WriteLine("⚠️ No signatures found.");
                else
                    Console.WriteLine("🔍 Found signatures: " + string.Join(", ", signatureNames));
            }

            // -----------------------------------------------------------------
            // 3️⃣ Add a blank page and a textbox with two widgets
            // -----------------------------------------------------------------
            using (var newDoc = new Document())
            {
                // Add a blank page – “add blank page pdf”
                var page = newDoc.Pages.Add();

                // Primary widget for the textbox
                var textBox = new TextBoxField(page, new Rectangle(100, 600, 300, 650))
                {
                    PartialName = "Comments",
                    Value = "Enter your comment here"
                };

                // Second widget – “how to add widget”
                textBox.Widgets.Add(new WidgetAnnotation(page, new Rectangle(100, 500, 300, 550)));

                // Register the field – “how to add field”
                newDoc.Form.Add(textBox, "Comments");

                // Save the final document
                newDoc.Save("YOUR_DIRECTORY/TextBoxMultipleWidgets.pdf");
                Console.WriteLine("✅ Blank page added and textbox with two widgets created.");
            }

            Console.WriteLine("\nAll tasks completed successfully!");
        }
    }
}
```

### Ожидаемый вывод

При запуске программы вы должны увидеть что‑то вроде:

```
✅ PDF/X‑4 conversion complete (transparency preserved).
🔍 Found signatures: ManagerSig, ClientSig
✅ Blank page added and textbox with two widgets created.

All tasks completed successfully!
```

Откройте `TextBoxMultipleWidgets.pdf` в Adobe Acrobat Reader; вы заметите два одинаковых текстовых поля с меткой **Comments** — одно в верхней части, другое чуть ниже. Ввод текста в одно поле мгновенно обновит другое.

## Часто задаваемые вопросы (FAQ)

| Вопрос | Ответ |
|----------|--------|
| **Можно ли извлечь фактические байты подписи?** | `GetSignatureNames()` возвращает только логические имена. Чтобы получить сертификат или значение подписи, нужно работать с объектами `SignatureField` (`document.Form["fieldName"] as SignatureField`). |
| **Работает ли конвертация в PDF/X‑4 с зашифрованными PDF?** | Да, при условии, что вы передаёте пароль через `Document.Open(file, password)`. |
| **Что делать, если нужно более двух виджетов?** | Просто вызывайте `textBox.Widgets.Add()` для каждого дополнительного `WidgetAnnotation`. |
| **Наследует ли пустая страница размер оригинального PDF?** | Новая страница использует размер по умолчанию (A4). При необходимости можно передать объект `Page` с пользовательскими размерами. |
| **Совместим ли код с .NET Core?** | Абсолютно — Aspose.Pdf кросс‑платформенный. Достаточно добавить NuGet‑пакет в ваш проект .NET Core. |

## Заключение

В этом руководстве мы продемонстрировали **how to extract signatures from PDF** и одновременно рассмотрели **how to add field**, **add blank page PDF**, **how to add widget** и **preserve transparency PDF**, используя Aspose.Pdf для C#. Теперь у вас есть надёжное сквозное решение, которое можно внедрить в любой конвейер обработки документов.

Готовы к следующему вызову? Попробуйте комбинировать эти техники с модулем OCR от Aspose, чтобы читать текст со сканированных  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}