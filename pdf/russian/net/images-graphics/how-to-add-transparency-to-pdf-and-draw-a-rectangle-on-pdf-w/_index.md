---
category: general
date: 2026-09-12
description: Узнайте, как добавить прозрачность в PDF, нарисовать прямоугольник в
  PDF и сохранить PDF с прозрачностью, используя Aspose.PDF на C# — пошаговое руководство.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: ru
lastmod: 2026-09-12
og_description: Добавьте прозрачность в PDF, нарисуйте прямоугольник в PDF и сохраните
  PDF с прозрачностью, используя Aspose.PDF в C#. Следуйте этому полному руководству.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Добавление прозрачности в PDF и рисование прямоугольника в PDF – полное
  руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Как добавить прозрачность в PDF и нарисовать прямоугольник в PDF с помощью
  Aspose.PDF
url: /ru/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить прозрачность в PDF и нарисовать прямоугольник в PDF с помощью Aspose.PDF

Если вам нужно **добавить прозрачность в PDF** файлы, это руководство покажет, как сделать это в C#. Вы также узнаете, как **нарисовать прямоугольник в PDF** и, наконец, **сохранить PDF с прозрачностью**, чтобы результат можно было использовать в отчетах, счетах‑фактурах или любом рабочем процессе автоматизации документов.

В этом руководстве вы:

* Загрузите существующий PDF‑документ.
* Создадите пользовательское графическое состояние, определяющее непрозрачность обводки и заливки.
* Примените это графическое состояние к холсту и нарисуете прямоугольник.
* Сохраните изменённый файл, сохранив настройки прозрачности.

Никакие внешние инструменты не требуются, кроме библиотеки Aspose.PDF for .NET, и каждая строка кода объяснена, чтобы вы понимали *почему* каждый шаг важен.

## Требования

* .NET 6.0 или новее (код также работает с .NET Framework 4.7+).
* Лицензированная или оценочная копия **Aspose.PDF for .NET**. Установите её через NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Входной PDF (`input.pdf`), размещённый в папке, к которой вы можете обратиться из проекта.

## Шаг 1: Загрузка PDF-документа

Первая операция — открыть исходный файл. Использование инструкции `using` гарантирует корректное освобождение документа, что предотвращает проблемы с блокировкой файла при последующей попытке сохранить его.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Почему это важно*: Загрузка документа даёт доступ к коллекции страниц, словарям ресурсов и объектам холста, необходимым для рисования.

## Шаг 2: Доступ к словарю ресурсов первой страницы

Каждая страница PDF имеет **словарь ресурсов**, в котором хранятся такие объекты, как шрифты, изображения и графические состояния. Чтобы добавить новое настройку прозрачности, нам нужно отредактировать запись `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Почему это важно*: `DictionaryEditor` позволяет читать и изменять низкоуровневые объекты PDF без нарушения структуры документа.

## Шаг 3: Создание пользовательского графического состояния с параметрами прозрачности

Графическое состояние (`ExtGState`) управляет тем, как отрисовываются операции рисования. Мы определяем два параметра непрозрачности:

* **CA** – непрозрачность обводки (контур фигур).
* **ca** – непрозрачность заливки (внутренняя часть фигур).

Мы также задаём режим смешивания (`BM`) как “Normal”, что является самым распространённым способом композитинга.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Почему это важно*: Добавив `GS0` в словарь `ExtGState`, мы создаём переиспользуемую ссылку, которую холст может активировать перед рисованием. Непрозрачность заливки `0.5` делает прямоугольник полупрозрачным, достигая цели **добавить прозрачность в PDF**.

## Шаг 4: Применение графического состояния и рисование прямоугольника

Теперь мы указываем холсту страницы использовать только что созданное графическое состояние, после чего рисуем прямоугольник. Координаты следуют системе координат PDF (начало в левом нижнем углу).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Почему это важно*: `SetGraphicsState("GS0")` переключает контекст рисования на ранее определённые параметры прозрачности. Метод `Rectangle` задаёт форму, а `Stroke` отрисовывает контур с указанной непрозрачностью. Если нужен также залитый прямоугольник, замените `Stroke()` на `FillAndStroke()`.

## Шаг 5: Сохранение измененного PDF с сохранением прозрачности

Наконец, записываем документ обратно на диск. Выходной файл содержит новое графическое состояние, нарисованный прямоугольник и информацию о прозрачности.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Почему это важно*: Сохранение документа фиксирует все изменения. Полученный файл можно открыть в любом PDF‑просмотрщике, и прямоугольник будет отображаться с 50 % непрозрачностью заливки.

### Ожидаемый результат

При открытии `output_with_extgstate.pdf` вы должны увидеть прямоугольник, у которого контур полностью непрозрачен, а внутренняя часть полупрозрачна, позволяя просвечивать любой подлежащий контент страницы.

## Пограничные случаи и практические советы

| Ситуация | Рекомендуемая корректировка |
|-----------|------------------------|
| **Multiple pages** | Loop over `pdfDocument.Pages` and repeat steps 2‑4 for each target page. |
| **Different opacity values** | Change the `CosPdfNumber` values for `CA` (stroke) and `ca` (fill) to any number between `0` (fully transparent) and `1` (fully opaque). |
| **Custom blend modes** | Replace `"Normal"` with `"Multiply"`, `"Screen"`, or any PDF‑standard blend mode supported by your viewer. |
| **Filled rectangle** | Call `canvas.FillAndStroke()` instead of `canvas.Stroke()` to apply both fill and outline. |
| **Re‑using the same graphics state** | You can call `canvas.SetGraphicsState("GS0")` before drawing any number of shapes on the same page. |

**Pro tip:** Always inspect the resource dictionary after adding a new `ExtGState`. If the dictionary does not exist, create it first:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Полный, исполняемый пример

Ниже приведена автономная программа, которую можно скопировать в консольное приложение и запустить сразу (замените `YOUR_DIRECTORY` на реальный путь).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Запуск программы создаёт `output_with_extgstate.pdf`, демонстрирующий **add transparency to PDF**, **draw rectangle on PDF** и **save PDF with transparency** в одном процессе.

## Заключение

Теперь вы знаете, как **добавить прозрачность в PDF** файлы, **нарисовать прямоугольник в PDF** и **сохранить PDF с прозрачностью** с помощью Aspose.PDF for .NET. Процесс основан на создании пользовательского `ExtGState`, его применении к холсту и сохранении изменений. С этими строительными блоками вы можете расширить технику на другие формы, несколько страниц или динамические значения непрозрачности.

**Следующие шаги**

* Исследуйте другие primitives рисования, такие как `canvas.Ellipse`, `canvas.Path` или `canvas.TextFragment`, переиспользуя то же графическое состояние.
* Сочетайте прозрачность с наложением изображений для создания водяных знаков (`canvas.Image` + custom `ExtGState`).
* Ознакомьтесь с документацией Aspose.PDF по **graphics state parameters** для продвинутых эффектов композитинга.

Счастливого кодинга и наслаждайтесь визуальной гибкостью, которую прозрачность привносит в ваши PDF‑рабочие процессы!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}