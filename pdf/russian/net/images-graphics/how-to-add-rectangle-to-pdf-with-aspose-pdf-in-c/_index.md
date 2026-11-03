---
category: general
date: 2026-10-10
description: Узнайте, как добавить прямоугольник в PDF, нарисовать форму в PDF и сохранить
  изменённый PDF с помощью Aspose.PDF. Включает пошаговое руководство по доступу к
  конкретной странице PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: ru
lastmod: 2026-10-10
og_description: Добавьте прямоугольник в PDF с помощью Aspose.PDF на C#. Этот учебник
  показывает, как нарисовать форму в PDF, получить доступ к определённой странице
  PDF и сохранить изменённый PDF.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Добавьте прямоугольник в PDF с помощью Aspose.PDF – полное руководство по
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Как добавить прямоугольник в PDF с помощью Aspose.PDF на C#
url: /ru/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить прямоугольник в PDF с помощью Aspose.PDF на C#

Если вам нужно **добавить прямоугольник в PDF** программно, это руководство покажет, как это сделать. Вы научитесь **рисовать фигуру в PDF**, выбирать конкретную страницу и **сохранять изменённый PDF** без ошибок.

Работа с PDF‑документами часто требуется для отчётности, выставления счетов или аннотирования документов. К концу этого урока вы сможете уверенно **добавлять фигуру в PDF**, обрабатывать ошибки выхода за границы и интегрировать решение в любой проект .NET.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 SDK или более поздняя версия  
* Visual Studio 2022 (или любой IDE для C#)  
* Лицензия Aspose.PDF for .NET или бесплатный оценочный ключ — API работает одинаково в обоих режимах  
* PDF‑файл с именем `input.pdf`, размещённый в папке, к которой вы можете обратиться из кода  

Эти элементы — единственные внешние зависимости примера.

## Шаг 1: Установить пакет Aspose.PDF NuGet

Библиотека Aspose.PDF предоставляет классы `Document`, `Rectangle` и другие необходимые для рисования классы.

```bash
dotnet add package Aspose.PDF
```

Выполнение этой команды добавит последнюю стабильную версию Aspose.PDF в ваш проект, сделав классы PDF доступными для компиляции.

## Шаг 2: Загрузить PDF‑документ

Первой операцией является загрузка исходного файла. Это создаёт представление в памяти, которое можно изменять.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Почему это важно*: Загрузка документа даёт доступ к коллекции его страниц, что необходимо для **доступа к конкретной странице PDF** позже.

## Шаг 3: Получить вторую страницу (нумерация с нуля)

Страницы PDF индексируются с `0`. Чтобы разместить прямоугольник на второй странице, получите страницу с индексом `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Если в документе меньше двух страниц, будет выброшено `ArgumentOutOfRangeException`, указывающее на необходимость проверки в производственном коде.

## Шаг 4: Создать форму прямоугольника

Определите позицию и размер прямоугольника с помощью структуры `Rectangle`, затем оберните её в объект рисования Aspose.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Почему это важно*: Свойства `BorderInfo` и `FillColor` позволяют **рисовать фигуру в PDF** с видимым контуром и необязательной заливкой, делая прямоугольник заметным для читателей.

## Шаг 5: Добавить прямоугольник в коллекцию абзацев страницы

Aspose.PDF рассматривает объекты рисования как элементы абзацев. Добавление прямоугольника в коллекцию `Paragraphs` страницы отобразит его на странице.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

На данном этапе PDF‑документ в памяти уже содержит новую форму, но файл на диске остаётся неизменным, пока вы его не сохраните.

## Шаг 6: Сохранить изменённый PDF и обработать ошибки выхода за границы

Вызов `Save` записывает обновлённый документ в новый файл. Если прямоугольник выходит за пределы страницы, Aspose бросит `PdfException`. Перехват этой ошибки позволяет корректно сообщить о проблеме.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Почему это важно*: Блок `try/catch` гарантирует, что ваше приложение **сохраняет изменённый PDF** безопасно, а сообщение об ошибке помогает скорректировать координаты прямоугольника при необходимости.

## Полный рабочий пример

Объединив все шаги, получаем полностью готовую к запуску программу:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Ожидаемый вывод

Запуск программы выводит:

```
PDF saved successfully with rectangle added.
```

и создаёт `output.pdf`, в котором отображается оригинальное содержимое плюс синий прямоугольник в указанных координатах на второй странице.

Если прямоугольник будет больше страницы, вы увидите:

```
Shape out of bounds: The shape exceeds page margins.
```

## Часто задаваемые вопросы и особые случаи

### Что делать, если в PDF только одна страница?

Попытка обратиться к `pdfDocument.Pages[1]` бросит `ArgumentOutOfRangeException`. Защититесь, проверив `pdfDocument.Pages.Count` перед индексацией.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Как добавить несколько прямоугольников на разные страницы?

Повторите шаги 2‑4 для каждой целевой страницы, изменяя координаты прямоугольника по необходимости. Логику можно разместить внутри цикла, который перебирает `pdfDocument.Pages`.

### Можно ли использовать другие фигуры, такие как круги или многоугольники?

Да. Aspose.PDF предоставляет классы `Ellipse`, `Polygon` и `Polyline`, которые работают по той же схеме, что и `Rectangle`. Замените вызов `new Aspose.Pdf.Drawing.Rectangle` нужным классом фигуры.

### Поддерживает ли библиотека PDF‑файлы со страницами, повернутыми на угол?

Aspose.PDF автоматически учитывает поворот страницы при отрисовке фигур. Координаты прямоугольника интерпретируются в родной системе координат страницы, поэтому дополнительных преобразований не требуется.

## Соображения по производительности

* **Использование памяти** — загрузка большого PDF (сотни мегабайт) потребляет соответствующее количество памяти. Если нужно изменить только одну страницу, рассмотрите возможность использования `PdfFileInfo` для извлечения этой страницы, её изменения и последующего объединения.
* **Пакетная обработка** — при добавлении фигур во множество документов переиспользуйте один экземпляр `License`, чтобы избежать повторных проверок лицензии.

## Следующие шаги

Теперь, когда вы умеете **добавлять прямоугольник в PDF**, изучите связанные темы:

* **draw shape on PDF** — научитесь накладывать текст, изображения и водяные знаки  
* **add shape to PDF** — комбинируйте несколько фигур в один слой аннотаций  
* **save modified PDF** — используйте потоки (`MemoryStream`) для возврата PDF напрямую из веб‑API  
* **access specific PDF page** — реализуйте извлечение диапазонов страниц для пользовательских отчётов  

Экспериментируйте с разными цветами, стилями линий и уровнями прозрачности, чтобы соответствовать требованиям вашего бренда.

---

*Счастливого кодинга! Если этот урок помог вам **добавить прямоугольник в PDF**, поделитесь им с коллегами или внесите улучшения в сообщество.*

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}