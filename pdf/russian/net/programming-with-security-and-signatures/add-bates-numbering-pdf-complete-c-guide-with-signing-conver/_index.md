---
category: general
date: 2026-06-21
description: Добавьте нумерацию Бейтса в PDF и узнайте, как добавить номера Бейтса,
  конвертировать PDF в PDF/X‑4, конвертировать PDF в PDF/A‑4 и цифрово подписать PDF
  на C# в одном руководстве.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: ru
og_description: Добавить нумерацию Бейтса в PDF, узнать, как добавить номера Бейтса,
  конвертировать PDF в PDF/X‑4, конвертировать PDF в PDF/A‑4 и цифрово подписать PDF
  на C# с помощью Aspose.Pdf.
og_title: Добавление нумерации Бейтса в PDF – пошаговое руководство на C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: Добавление нумерации Бейтса в PDF – Полное руководство по C# с подписанием
  и конвертацией
url: /ru/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление нумерации Бейтса в PDF – Полное руководство на C# с подписью и конвертацией

Когда‑то задумывались, как **add bates numbering pdf** без лишних нервов? Вы не одиноки. Юридические отделы, аудиторы и все, кому нужны отслеживаемые документы, постоянно спрашивают, *как добавить нумерацию Бейтса* в PDF, а затем требуют, чтобы файл соответствовал стандартам PDF/X‑4 или PDF/A‑4 и был цифрово подписан.  

В этом руководстве мы шаг за шагом покажем, как с помощью Aspose.Pdf for .NET **add bates numbering pdf**, продемонстрируем **how to add bates numbers**, **convert pdf to pdf/x-4**, **convert pdf to pdfa-4**, а в конце **digitally sign pdf c#**. К концу вы получите готовую к запуску программу, которая создаст три отшлифованных PDF‑файла: версию PDF/X‑4, файл с нумерацией Бейтса и файл с цифровой подписью.

![пример добавления нумерации Бейтса в PDF](image-placeholder.png "Скриншот, показывающий работу add bates numbering pdf")

## Что понадобится

- **.NET 6+** (или .NET Framework 4.6+). Aspose.Pdf поддерживает оба варианта.  
- **Действующая лицензия Aspose.Pdf for .NET** (можно использовать оценочную версию, но в ней будут водяные знаки).  
- **Файл сертификата PKCS#7** (`.pfx`) и его пароль для подписи.  
- **Исходный PDF**, который нужно преобразовать (разместите его в удобной папке).  
- Visual Studio, Rider или любой другой IDE для C#.

Это всё — никаких дополнительных пакетов NuGet, кроме `Aspose.Pdf`. Если библиотеку ещё не добавляли, выполните:

```bash
dotnet add package Aspose.Pdf
```

А теперь перейдём к коду.

## Шаг 1: Загрузка исходного PDF‑документа

Сначала нужно загрузить оригинальный файл в память. Это база для всех последующих операций.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Почему это важно:** При загрузке PDF создаётся объект `Document`, представляющий весь файл и дающий доступ к API конвертации, форм и безопасности.

## Шаг 2: Конвертация PDF в PDF/X‑4 (соответствие PDF/A‑4)

Если ваш процесс требует архивного качества, выбирайте PDF/X‑4 (подмножество PDF/A‑4). Ниже показано, как **convert pdf to pdf/x-4** с помощью Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Подсказка:** Флаг `ConvertErrorAction.Delete` удаляет любой контент, который мог бы нарушить соответствие, обеспечивая чистый вывод PDF/X‑4.

## Шаг 3: Сохранение версии PDF/X‑4

Теперь, когда документ соответствует PDF/X‑4, сохраняем его на диск.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

У вас появился файл, совместимый с **convert pdf to pdfa-4** (PDF/X‑4 входит в семью PDF/A‑4). Откройте его в Acrobat, чтобы убедиться в наличии значка соответствия.

## Шаг 4: Добавление нумерации Бейтса – ядро «Add Bates Numbering PDF»

Нумерация Бейтса – это последовательный идентификатор, размещаемый на каждой странице. Это точный ответ на вопрос *how to add bates numbers* программным способом.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Почему это работает:** `AddBatesNumbering` проходит по каждой странице и ставит номер в стандартное место (внизу‑справа). При необходимости позицию можно изменить через `BatesNumberingOptions`.

## Шаг 5: Сохранение PDF с нумерацией Бейтса

После того как мы **add bates numbering pdf**, нужен отдельный файл, сохраняющий номера.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Откройте файл — внизу каждой страницы должны появиться «CASE‑5000», «CASE‑5001» и т.д.

## Шаг 6: Цифровая подпись PDF – «Digitally Sign PDF C#» в действии

Цифровая подпись гарантирует подлинность и целостность. Ниже мы **digitally sign pdf c#** с использованием хеша SHA‑384.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Профессиональный совет:** `Rectangle` задаёт область, где будет отображаться видимая подпись. Если визуальный индикатор не нужен, установите `signatureAppearance` в `false`.

## Шаг 7: Сохранение подписанного PDF

Наконец, сохраняем подписанный документ на диск.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Теперь у вас есть файл **digitally sign pdf c#**, который можно проверить в любом PDF‑просмотрщике, поддерживающем цифровые подписи.

## Полный исходный код – всё в одном решении

Ниже представлен полностью готовый к запуску пример, объединяющий все шаги. Скопируйте‑вставьте, поправьте пути и нажмите **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### Ожидаемый результат

| Файл | Назначение | Ключевая особенность |
|------|------------|----------------------|
| `sample_pdfx4.pdf` | Версия PDF/X‑4 | Соответствует требованиям PDF/A‑4 |
| `sample_bates.pdf` | PDF с нумерацией Бейтса | Применён **add bates numbering pdf** |
| `sample_signed.pdf` | Подписанный PDF | **digitally sign pdf c#** с SHA‑384 |

Откройте любой из трёх файлов в Adobe Acrobat Reader — на втором вы увидите номера Бейтса, а на третьем — поле подписи.

## Часто задаваемые вопросы (FAQ)

**В: Можно ли изменить позицию номеров Бейтса?**  
О: Да. Используйте свойства `BatesNumberingOptions`, такие как `Location` и `FontSize`, чтобы точно настроить размещение.

**В: Что если нужен PDF/A‑4 вместо PDF/X‑4?**  
О: Замените `PdfFormat.PDF_X_4` на `PdfFormat.PDFA_4` в параметрах конвертации. Это удовлетворит требование **convert pdf to pdfa-4**.

**В: Мой сертификат использует другой алгоритм хеширования — можно ли применить SHA‑256?**  
О: Конечно. Замените `DigestHashAlgorithm.Sha384` на `DigestHashAlgorithm.Sha256` (или любой поддерживаемый алгоритм).

**В: Нужно ли вызывать `document.Save` после каждого шага?**  
О: Не обязательно. В данном потоке мы сохраняем после конвертации и после нумерации, чтобы получить промежуточные файлы. При желании можно отложить сохранение до самого конца, выполнив одну запись.

## Итоги

Мы продемонстрировали практическое, сквозное решение, которое **add bates numbering pdf**, объясняет **how to add bates numbers**, показывает **convert pdf to pdf/x-4**, охватывает

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}