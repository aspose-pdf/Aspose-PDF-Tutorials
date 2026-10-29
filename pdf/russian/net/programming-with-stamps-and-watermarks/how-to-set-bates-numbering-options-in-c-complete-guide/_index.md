---
category: general
date: 2026-08-14
description: Как установить параметры нумерации Бейтса в C# с использованием GroupDocs.
  Следуйте этому пошаговому руководству, чтобы добавить пользовательские префиксы
  и начальные номера при конвертации Word в PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: ru
lastmod: 2026-08-14
og_description: Как быстро настроить параметры нумерации Бейтса в C#. Это руководство
  покажет, как добавить пользовательские префиксы и начальные номера при конвертации
  Word в PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Как настроить параметры нумерации Бейтса в C# – пошаговое руководство
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Как настроить параметры нумерации Бейтса в C# — полное руководство
url: /ru/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как установить параметры нумерации Бейтса в C# – полное руководство

Если вам нужно **how to set bates numbering options** в C#, это руководство проведёт вас через точные шаги. Вы узнаете, как настроить начальный номер, добавить префикс и применить нумерацию при конвертации документа Word в PDF с использованием GroupDocs API.

Обработка документов часто требует уникальных идентификаторов на каждой странице для юридических или архивных целей. К концу этого урока у вас будет переиспользуемый фрагмент кода, который можно вставить в любой .NET‑проект, будь то инструмент поддержки судебных процессов или автоматический генератор отчётов. Внешние инструменты не нужны — только библиотека GroupDocs.Conversion и несколько строк C#.

## Что вам понадобится

* .NET 6.0 SDK или более поздняя версия, установленная  
* Visual Studio 2022 (или любая IDE, поддерживающая .NET)  
* Действующая лицензия GroupDocs.Conversion (бесплатная пробная версия подходит для тестов)  
* Пример документа Word (`input.docx`), который нужно пронумеровать  

Эти предварительные условия гарантируют, что код будет работать без дополнительной настройки.

## Как установить параметры нумерации Бейтса – обзор

Суть **how to set bates numbering options** заключается в трёх объектах:

1. `Document` – загружает исходный файл.  
2. `BatesNumberingOptions` – хранит начальный номер, префикс и другие параметры форматирования.  
3. `AddBatesNumbering` – метод, который вставляет нумерацию на каждую страницу.

Понимание того, зачем нужен каждый элемент, поможет адаптировать решение к более сложным сценариям, например, с пользовательскими шрифтами или многоязычной нумерацией.

## Шаг 1: Установите пакет GroupDocs.Conversion NuGet

Откройте терминал в папке решения и выполните:

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API** предоставляет класс `Document` и метод‑расширение `AddBatesNumbering`, используемые далее в руководстве.

## Шаг 2: Загрузите исходный документ

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Почему этот шаг?*  
Загрузка файла создаёт представление в памяти, которое может обрабатывать движок конвертации. Без экземпляра `Document` вы не сможете применить нумерацию Бейтса или любую другую трансформацию.

## Шаг 3: Создайте параметры нумерации Бейтса

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Почему этот шаг?*  
`BatesNumberingOptions` инкапсулирует все настройки, которые могут понадобиться при **setting bates numbering options**. Настройка `StartNumber` и `Prefix` позволяет согласовать вывод с вашей системой управления делами. Свойство `Position` контролирует визуальное размещение, что часто является требованием соответствия.

## Шаг 4: Примените нумерацию Бейтса к документу

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

Метод `AddBatesNumbering` проходит по каждой странице загруженного `Document` и вставляет сконфигурированную строку. Поскольку метод работает с представлением в памяти, вы можете добавить дополнительные шаги обработки (например, водяные знаки) перед сохранением.

## Шаг 5: Конвертируйте и сохраните результат в PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Почему этот шаг?*  
Сохранение в PDF — распространённый финальный формат для юридических документов. Объект `PdfConvertOptions` позволяет тонко настроить вывод, но для базовой нумерации он не обязателен. Вызов `Save` записывает полностью пронумерованный PDF на диск.

## Полный, исполняемый пример

Объединив всё вместе, получаем автономное консольное приложение, которое можно собрать и запустить:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Ожидаемый результат**

Запуск программы создаёт `output.pdf`, где каждая страница содержит метку вроде `CASE-1000`, `CASE-1001` и т.д., расположенную в правом нижнем колонтитуле. Откройте PDF в любом просмотрщике, чтобы убедиться, что номера отображаются корректно.

## Распространённые проблемы и лучшие практики

| Проблема | Почему происходит | Как избежать |
|----------|-------------------|--------------|
| **Relative paths cause `FileNotFoundException`** | Рабочий каталог консольного приложения может отличаться от каталога Visual Studio. | Используйте абсолютные пути или `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Numbering overlaps existing footers** | Если в исходном документе уже есть содержимое в выбранной области нижнего колонтитула, новый номер может быть скрыт. | Выберите другое `Position` (например, `HeaderLeft`) или скорректируйте шаблон документа. |
| **Large documents are slow** | Нумерация Бейтса проходит по каждой странице; потребление памяти растёт с размером файла. | Обрабатывайте документ частями с помощью `Document.Split`, если количество страниц превышает 500. |
| **License expiration** | Бесплатная пробная версия GroupDocs истекает через 30 дней, вызывая исключение при `AddBatesNumbering`. | Примените действительный лицензионный ключ перед загрузкой документа: `License license = new License(); license.SetLicense("license.lic");`. |

**Pro tip:** Если нужен иной формат номера для каждого дела (например, `2023-CASE-001`), сформируйте префикс динамически перед созданием `BatesNumberingOptions`.

## Расширение решения

Тот же подход **Bates numbering C#** работает с другими исходными форматами, такими как `.txt`, `.html` или даже изображения. Просто измените расширение файла при создании объекта `Document`, и движок конвертации справится с остальным.

Вы также можете комбинировать **document conversion C#** с OCR для сканированных PDF:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Заключение

Теперь вы знаете **how to set bates numbering options** в C# от начала до конца. Создав объект `BatesNumberingOptions`, применив его через `AddBatesNumbering` и сохранив результат в PDF, вы можете автоматизировать создание юридически соответствующих, уникально идентифицированных документов.  

Далее вы можете изучать связанные темы, такие как **C# PDF generation**, **document conversion C#**, или продвинутые возможности **GroupDocs API**, например, водяные знаки и цифровые подписи. Экспериментируйте с различными префиксами, позициями и форматами номеров, чтобы подобрать оптимальный рабочий процесс.

Удачной разработки!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Add Bates Numbering PDF in C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step‑By‑Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}