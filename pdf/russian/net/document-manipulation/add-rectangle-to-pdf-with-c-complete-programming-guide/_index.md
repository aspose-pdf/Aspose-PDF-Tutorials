---
category: general
date: 2026-06-05
description: Добавьте прямоугольник в PDF с помощью Aspose.Pdf на C#. Узнайте, как
  загрузить существующий PDF, отредактировать страницу PDF и вставить форму в PDF
  за несколько минут.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- load existing pdf
- edit pdf page
- insert shape into pdf
language: ru
og_description: Быстро добавить прямоугольник в PDF. Этот учебник показывает, как
  загрузить существующий PDF, отредактировать страницу PDF и нарисовать прямоугольник
  в PDF с помощью Aspose.Pdf.
og_title: Добавить прямоугольник в PDF с помощью C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  headline: Add Rectangle to PDF with C# – Complete Programming Guide
  type: TechArticle
- description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  name: Add Rectangle to PDF with C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.6+). - Aspose.Pdf
      for .NET NuGet package (`Install-Package Aspose.Pdf`). - Basic familiarity with
      C# syntax (no deep PDF knowledge required).'
  - name: Why loading matters
    text: Before you can draw anything, the PDF must be in memory. The `Document`
      constructor reads the file, parses its internal structure, and gives you an
      object model to work with. If the file is locked or corrupted, Aspose will throw
      a descriptive exception—so you know exactly what went wrong.
  - name: Code
    text: '```csharp Document doc = new Document("YOUR_DIRECTORY/input.pdf"); ```'
  - name: Why page selection is crucial
    text: PDFs are page‑oriented; each page has its own coordinate system. Aspose
      uses a **1‑based** index, which trips up developers coming from 0‑based collections.
      Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies
      an unintended page.
  - name: Code
    text: '```csharp Page page = doc.Pages[1]; // First page ```'
  - name: Understanding the rectangle coordinates
    text: A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and
      upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left**
      of the page, with X increasing to the right and Y increasing upward. This is
      opposite of many UI frameworks, so keep an eye on the axes.
  - name: Code to add the shape
    text: '```csharp Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500,
      700); page.AddRectangle(rect); ```'
  - name: Why saving is the final step
    text: All manipulations stay in memory until you persist them. `Document.Save`
      writes the new content to disk (or stream). Overwriting the original file is
      possible, but keeping a backup (`output.pdf`) is safer.
  - name: Code
    text: '```csharp doc.Save("YOUR_DIRECTORY/output.pdf"); ```'
  type: HowTo
- questions:
  - answer: Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each
      `Page` object.
    question: Can I add the rectangle to every page automatically?
  - answer: Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods.
      The same rectangle logic applies for bounding boxes.
    question: What if I need to draw a circle or a polygon?
  - answer: 'Compute the center coordinates:'
    question: Is there a way to position the rectangle relative to the page center?
  - answer: Aspose loads pages lazily, but if you’re processing thousands of pages,
      consider using `PdfExtractor` to work on subsets or stream the file to reduce
      memory footprint.
    question: Performance concerns for large PDFs?
  type: FAQPage
tags:
- pdf
- csharp
- aspose
- shape-manipulation
title: Добавление прямоугольника в PDF с помощью C# – Полное руководство по программированию
url: /ru/net/document-manipulation/add-rectangle-to-pdf-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавить прямоугольник в PDF с C# – Полное руководство по программированию

Когда‑нибудь вам нужно было **add rectangle to pdf**, но вы не знали, какой вызов API использовать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда впервые пытаются программно редактировать PDF. Хорошая новость? С несколькими строками C# и мощной библиотекой Aspose.Pdf вы можете нарисовать прямоугольник на любой странице существующего документа за мгновение.

В этом руководстве мы пройдем процесс загрузки существующего PDF, выбора нужной страницы, определения подходящего прямоугольника и, наконец, вставки фигуры в PDF. К концу вы получите переиспользуемый фрагмент кода, который можно добавить в любой .NET‑проект. О, и мы также коснёмся нюансов **draw rectangle on pdf**, о которых вы могли не задумываться.

## Что вы получите

- Чёткое пошаговое решение, работающее «из коробки».
- Понимание того, как безопасно **load existing pdf** файлы.
- Советы по **edit pdf page** без повреждения документа.
- Стратегии **insert shape into pdf** помимо простых прямоугольников.
- Готовый к запуску C#‑код, который можно сразу скопировать и вставить.

### Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.6+).
- NuGet‑пакет Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`).
- Базовое знакомство с синтаксисом C# (глубокие знания PDF не требуются).

Если всё это у вас есть, давайте погрузимся.

![Пример добавления прямоугольника в PDF](add-rectangle-to-pdf.png "Снимок экрана, показывающий добавление прямоугольника на страницу PDF – add rectangle to pdf")

## Добавление прямоугольника в PDF – пошаговый обзор

Ниже приведён полностью готовый к выполнению пример, который следует точно в том порядке, о котором мы будем говорить:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF file
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Select the first page (pages are 1‑based)
        Page page = doc.Pages[1];

        // 3️⃣ Define a rectangle that fits inside the page bounds
        //    (xLL, yLL, xUR, yUR) – lower‑left & upper‑right corners
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);

        // 4️⃣ Add the rectangle to the page – this draws the shape
        page.AddRectangle(rect);

        // 5️⃣ Save the modified PDF to a new file
        doc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Теперь разберём каждую строку, чтобы вы понимали **почему** мы делаем то, что делаем, а не только **что**.

## Загрузка существующего PDF‑документа

### Почему загрузка важна

Прежде чем что‑либо рисовать, PDF должен находиться в памяти. Конструктор `Document` читает файл, разбирает его внутреннюю структуру и предоставляет объектную модель для работы. Если файл заблокирован или повреждён, Aspose выбросит описательное исключение — вы сразу узнаете, в чём проблема.

### Код

```csharp
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

- Замените `YOUR_DIRECTORY` на абсолютный или относительный путь к вашему исходному файлу.
- Путь может быть URL, если включить удалённую загрузку Aspose (расширенный сценарий).
- **Tip:** Оберните этот код в блок `try/catch`, чтобы корректно обрабатывать `FileNotFoundException` или `PdfException`.

```csharp
try
{
    Document doc = new Document("input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load PDF: {ex.Message}");
    return;
}
```

## Выбор и подготовка страницы

### Почему выбор страницы имеет решающее значение

PDF‑файлы ориентированы на страницы; у каждой страницы своя система координат. Aspose использует **1‑based** индексацию, что часто сбивает с толку разработчиков, привыкших к 0‑based коллекциям. Выбор неправильной страницы приводит к `ArgumentOutOfRangeException` или к изменению нежелательной страницы.

### Код

```csharp
Page page = doc.Pages[1]; // First page
```

Если вам нужна страница 3, просто измените индекс на `3`. Для динамических сценариев можно использовать цикл:

```csharp
foreach (Page pg in doc.Pages)
{
    // Apply rectangle to every page
}
```

## Определение и рисование прямоугольника в PDF

### Understanding the rectangle coordinates

Прямоугольник в Aspose.Pdf определяется нижним‑левым (`xLL`, `yLL`) и верхним‑правым (`xUR`, `yUR`) углами. Система координат начинается в **левом‑нижнем** углу страницы: X растёт вправо, а Y — вверх. Это противоположно многим UI‑фреймворкам, поэтому следите за осями.

- `0,0` — левый‑нижний угол страницы.
- Ширина = `xUR - xLL`; Высота = `yUR - yLL`.

Если задать прямоугольник больше страницы, `AddRectangle` бросит исключение. Чтобы этого избежать, можно запросить размер страницы:

```csharp
double pageWidth  = page.PageInfo.Width;
double pageHeight = page.PageInfo.Height;
```

Затем ограничьте ваш прямоугольник:

```csharp
double rectWidth  = Math.Min(500, pageWidth);
double rectHeight = Math.Min(700, pageHeight);
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectWidth, rectHeight);
```

### Код для добавления фигуры

```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);
page.AddRectangle(rect);
```

- `AddRectangle` автоматически рисует тонкую чёрную границу.
- Хотите заполненный прямоугольник? Используйте `page.AddAnnotation(new SquareAnnotation(page, rect) { FillColor = Color.Yellow });`.
- Нужно изменить толщину линии? Установите `rect.LineWidth = 2;` перед добавлением.

#### Edge case: multiple rectangles

Если вы вызываете `AddRectangle` несколько раз, каждый вызов добавляет новую фигуру. Чтобы избежать наложения, сместите последующие прямоугольники:

```csharp
for (int i = 0; i < 3; i++)
{
    var offset = i * 20;
    var r = new Aspose.Pdf.Rectangle(offset, offset, 500 + offset, 700 + offset);
    page.AddRectangle(r);
}
```

## Сохранение изменённого PDF

### Почему сохранение — последний шаг

Все изменения находятся в памяти, пока вы их не запишете. `Document.Save` сохраняет новое содержимое на диск (или в поток). Перезаписать оригинальный файл можно, но безопаснее сохранять копию (`output.pdf`).

### Код

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

- Вы также можете сохранить в `MemoryStream`, если нужно отправить PDF по HTTP:

```csharp
using var ms = new MemoryStream();
doc.Save(ms);
byte[] pdfBytes = ms.ToArray();
// return File(pdfBytes, "application/pdf");
```

## Полный рабочий пример (готовый к копированию и вставке)

Собрав всё вместе, получаем окончательную программу, которую можно запустить прямо сейчас:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

class AddRectangleDemo
{
    static void Main()
    {
        const string inputPath  = "input.pdf";
        const string outputPath = "output.pdf";

        // Load the existing PDF
        Document doc;
        try
        {
            doc = new Document(inputPath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading PDF: {ex.Message}");
            return;
        }

        // Ensure the document has at least one page
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("PDF contains no pages.");
            return;
        }

        // Select the first page (1‑based index)
        Page page = doc.Pages[1];

        // Get page dimensions to avoid overflow
        double pageW = page.PageInfo.Width;
        double pageH = page.PageInfo.Height;

        // Define rectangle size (clamp to page bounds)
        double rectW = Math.Min(500, pageW);
        double rectH = Math.Min(700, pageH);
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectW, rectH);

        // Optional: set line width and color
        rect.LineWidth = 2;
        rect.Color = Color.Blue;

        // Add rectangle to the page
        page.AddRectangle(rect);

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"Rectangle added and saved to {outputPath}");
    }
}
```

**Expected output:** Откройте `output.pdf`, и вы увидите прямоугольник с синей границей, привязанный к левому‑нижнему углу первой страницы, размером до 500 × 700 пунктов (или меньше, если страница небольшая).

## Часто задаваемые вопросы и профессиональные советы

- **Can I add the rectangle to every page automatically?**  
  Да — пройдитесь циклом по `doc.Pages` и повторите вызов `AddRectangle` для каждого объекта `Page`.

- **What if I need to draw a circle or a polygon?**  
  Aspose предоставляет методы `AddCircle`, `AddPolygon` и `AddPolyline`. Та же логика с прямоугольником применяется для ограничивающих рамок.

- **Is there a way to position the rectangle relative to the page center?**  
  Вычислите координаты центра:  
  ```csharp
  double centerX = pageW / 2;
  double centerY = pageH / 2;
  double halfW = rectW / 2;
  double halfH = rectH / 2;
  var centeredRect = new Aspose.Pdf.Rectangle(centerX - halfW, centerY - halfH,
                                              centerX + halfW, centerY + halfH);
  page.AddRectangle(centeredRect);
  ```

- **Performance concerns for large PDFs?**  
  Aspose загружает страницы «лениво», но если вы обрабатываете тысячи страниц, рассмотрите использование `PdfExtractor` для работы с подмножествами или потоковую передачу файла, чтобы снизить потребление памяти.

## Заключение

Теперь вы знаете **how to add rectangle** в PDF‑документ.

## Что изучить дальше?

- [Создать PDF‑документ с Aspose.PDF – добавить страницу, форму и сохранить](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Как добавить штампы на страницы PDF с помощью Aspose.PDF for .NET: полное руководство](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Добавление изображений и номеров страниц в PDF с помощью Aspose.PDF for .NET: полное руководство](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}