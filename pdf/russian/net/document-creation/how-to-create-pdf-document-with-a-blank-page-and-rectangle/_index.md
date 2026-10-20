---
category: general
date: 2026-09-05
description: Создайте PDF‑документ на C#, добавив пустую страницу, нарисовав прямоугольник
  и сохранив файл PDF. Следуйте пошаговому примеру Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: ru
lastmod: 2026-09-05
og_description: Создайте PDF‑документ на C#, добавив пустую страницу, нарисовав прямоугольник
  и сохранив файл PDF. Следуйте этому полному примеру с Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Создание PDF‑документа с пустой страницей и прямоугольником – руководство
  по C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Как создать PDF‑документ с пустой страницей и прямоугольником
url: /ru/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать PDF‑документ с пустой страницей и прямоугольником

Если вам нужно **create PDF document** программно, это руководство показывает полное решение на C#. Вы узнаете, как добавить пустую страницу, нарисовать прямоугольник на этой странице и в конце сохранить PDF‑файл. В примере используется библиотека Aspose.PDF, которая работает с .NET 6+ и .NET Framework 4.5+.

Добавление пустой страницы и рисование фигур — распространённая потребность для счетов‑фактур, сертификатов или пользовательских отчётов. К концу этого руководства у вас будет исполняемый проект, который генерирует PDF, содержащий один прямоугольник, расположенный в точке (100, 100) и имеющий размер 200 × 200 пунктов.

## Предварительные требования

* Visual Studio 2022 (или любой IDE для C#)
* .NET 6 SDK или .NET Framework 4.5+
* Aspose.PDF for .NET NuGet package  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Разрешение на запись в каталог вывода

Дополнительная конфигурация не требуется; код работает сразу же.

## Создание PDF‑документа – обзор

Весь процесс состоит из четырёх логических шагов:

1. **Instantiate** объект `Document` – он представляет PDF‑файл.
2. **Add a blank page** – страница предоставляет холст для рисования.
3. **Draw a rectangle** – объект `Path` определяет форму.
4. **Save the PDF file** – сохраняет документ на диск.

Каждый шаг изолирован в отдельном разделе, чтобы вы могли переиспользовать или заменять части по мере необходимости.

![Диаграмма PDF с прямоугольником на пустой странице](https://example.com/placeholder-image.png){.img-fluid alt="Скриншот, показывающий PDF‑документ с нарисованным прямоугольником на пустой странице"}

## Добавление пустой страницы PDF

PDF должен содержать как минимум одну страницу, прежде чем можно разместить графику. Метод `Pages.Add()` создаёт пустую страницу с размерами по умолчанию (A4). Если нужен другой размер, передайте аргумент `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Why this step matters* – Объект страницы содержит коллекции текста, изображений и векторной графики. Без страницы любая попытка добавить прямоугольник вызовет исключение.

### Пограничный случай: пользовательский размер страницы

Если ваш макет требует страницу размером 6 × 9 дюймов, замените вызов по умолчанию на:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Рисование прямоугольника PDF

Рисование прямоугольника заключается в создании геометрии `Rectangle` и обёртывании её в `Path`. Вызов `ValidateBounds()` гарантирует, что фигура помещается внутри полей страницы, предотвращая обрезку.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Why this step matters* – Объект `Path` является низкоуровневой векторной примитивой, используемой Aspose.PDF. Проверяя границы, вы избегаете ошибок выполнения, когда прямоугольник выходит за пределы страницы.

### Профессиональный совет: стилизация прямоугольника

Вы можете изменить цвет обводки и толщину линии:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Это создаёт красную обводку толщиной 2 пункта.

## Сохранение PDF‑файла

Сохранение документа завершает запись файла на диск. Метод `Save` принимает путь к файлу или поток. Указание абсолютного пути делает расположение явным, что полезно для скриптов автоматизации.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Why this step matters* – Сохранение — единственный момент, когда представление в памяти превращается в физический файл. Если нужно вернуть PDF из веб‑API, замените путь к файлу на `MemoryStream`.

### Пограничный случай: перезапись существующих файлов

Aspose.PDF по умолчанию перезаписывает существующий файл. Чтобы защитить предыдущие результаты, сначала проверьте наличие файла:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Как добавить прямоугольник – лучшие практики

* **Keep coordinates within the page margins** – используйте `ValidateBounds()` или рассчитывайте поля вручную.
* **Reuse `GraphInfo` objects** при рисовании нескольких фигур; это уменьшает выделение памяти.
* **Dispose of the `Document` object** (как показано с `using var`) для своевременного освобождения нативных ресурсов.
* **Test with different DPI settings** если позже будете встраивать растровые изображения; векторные формы, такие как прямоугольники, остаются чёткими при любом разрешении.

## Полный рабочий пример

Ниже приведена полная программа, которую вы можете скопировать в консольное приложение. Она компилируется без изменений и создаёт `output.pdf` в папке проекта.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Ожидаемый результат

Запуск программы создаёт одностраничный PDF. При открытии `output.pdf` вы увидите пустую белую страницу с красным прямоугольником, расположенным на 100 пунктов от левого и нижнего краёв, размером 200 × 200 пунктов.

## Заключение

Теперь вы знаете, как **create PDF document**, **add blank page pdf**, **draw rectangle pdf** и **save pdf file** с помощью Aspose.PDF в C#. Пример охватывает основные вызовы API, объясняет, почему каждый вызов необходим, и даёт советы по распространённым вариантам, таким как пользовательские размеры страниц или стилизация прямоугольника.

Далее изучайте связанные темы, такие как **adding text**, **embedding images** или **creating multi‑page reports**. Та же схема — создать `Document`, манипулировать страницами, добавлять векторный или растровый контент, затем `Save` — применима ко всем этим сценариям. Не стесняйтесь экспериментировать с различными формами, цветами и макетами страниц, чтобы соответствовать потребностям вашего проекта.

## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создание PDF‑документа C# – Добавить страницу, нарисовать прямоугольник и сохранить](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Создание PDF‑документа с Aspose.PDF – Пошаговое руководство](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Создание PDF‑документа с Aspose – Добавить страницу, текстовое поле и форму](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}