---
category: general
date: 2026-02-12
description: Быстро создайте PDF‑документ на C#, добавив пустую страницу, проверив
  размер страницы, нарисовав прямоугольник и сохранив файл. Пошаговое руководство
  с Aspose.Pdf.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- save pdf file c#
- check pdf page size
language: ru
og_description: Создайте PDF‑документ на C# быстро, добавив пустую страницу, проверив
  размер страницы, нарисовав прямоугольник и сохранив файл. Полный учебник с кодом.
og_title: Создание PDF‑документа на C# – Добавление пустой страницы и рисование прямоугольника
tags:
- PDF
- C#
- Aspose.Pdf
- Document Generation
title: Создание PDF‑документа C# – добавить пустую страницу и нарисовать прямоугольник
url: /ru/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF-документа C# – Добавление пустой страницы и рисование прямоугольника

Когда‑нибудь вам нужно было **create PDF document C#** с нуля и вы задавались вопросом, как добавить пустую страницу, проверить размеры страницы, нарисовать фигуру и, наконец, сохранить её? Вы не одиноки. Многие разработчики сталкиваются с этой же проблемой при автоматизации отчетов, счетов‑фактур или любого другого печатного вывода.

В этом руководстве мы пройдем полный, готовый к запуску пример, который покажет вам, как именно **add blank page PDF**, **check PDF page size**, **draw rectangle PDF** и **save PDF file C#** с использованием библиотеки Aspose.Pdf. К концу вы получите готовый PDF‑файл с прямоугольником, обведённым синей линией, аккуратно размещённым на странице формата A4.

## Требования

- **.NET 6.0** или новее (код также работает на .NET Framework 4.6+).  
- **Aspose.Pdf for .NET**, установленный через NuGet (`Install-Package Aspose.Pdf`).  
- Базовое понимание синтаксиса C# — ничего сложного не требуется.  
- Любая IDE по вашему выбору (Visual Studio, Rider, VS Code и т.д.).

> **Pro tip:** Если вы используете Visual Studio, интерфейс NuGet Package Manager упрощает добавление Aspose.Pdf — просто выполните поиск “Aspose.Pdf” и нажмите Install.

## Шаг 1: Create PDF Document C# – Инициализация документа

Первое, что вам понадобится, — это новый объект `Document`. Считайте его пустым холстом, на котором каждая последующая операция будет наносить своё содержимое.

```csharp
using Aspose.Pdf;
using System;

// Step 1: Create a new PDF document
var pdfDocument = new Document();
```

> **Почему это важно:** Класс `Document` является точкой входа для любой операции с PDF. Его создание выделяет внутренние структуры, необходимые для управления страницами, ресурсами и метаданными.

## Шаг 2: Add Blank Page PDF – Добавление новой страницы

PDF без страниц — это как книга без листов — бессмысленно. Добавление пустой страницы даёт нам поверхность для рисования.

```csharp
// Step 2: Add a blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Что происходит за кулисами?** `Pages.Add()` создаёт страницу, наследующую размер по умолчанию (A4 для большинства настроек). При необходимости вы можете позже изменить её размеры, если нужен пользовательский размер.

## Шаг 3: Определение прямоугольника и проверка размера страницы PDF

Прежде чем рисовать, нам нужно определить, где будет располагаться прямоугольник, и убедиться, что он помещается на странице. Здесь в игру вступает ключевое слово **check PDF page size**.

```csharp
// Step 3: Define rectangle position and size (fits within a standard A4 page)
var rectangle = new Rectangle(50, 50, 550, 750);

// Step 3b: Verify that the rectangle fits inside the page boundaries
bool fitsWidth = page.PageInfo.Width >= rectangle.Width;
bool fitsHeight = page.PageInfo.Height >= rectangle.Height;

if (!fitsWidth || !fitsHeight)
{
    throw new InvalidOperationException(
        $"Rectangle (W:{rectangle.Width}, H:{rectangle.Height}) exceeds page size (W:{page.PageInfo.Width}, H:{page.PageInfo.Height}).");
}
```

> **Почему мы проверяем:** Некоторые PDF могут использовать пользовательские размеры страниц (Letter, Legal и т.д.). Если прямоугольник больше страницы, операция рисования будет обрезана или вызовет ошибку. Эта проверка делает код надёжным при любых будущих изменениях размеров страниц.

## Шаг 4: Draw Rectangle PDF – Рендеринг фигуры

Теперь самая интересная часть: фактическое рисование прямоугольника с синей рамкой и прозрачной заливкой. Это демонстрирует возможность **draw rectangle PDF**.

```csharp
// Step 4: Draw the rectangle with a blue border and a transparent fill
page.AddRectangle(
    rectangle,
    Color.Blue,          // Border color
    Color.Transparent    // Fill color (transparent)
);
```

> **Как это работает:** `AddRectangle` принимает три аргумента — геометрию прямоугольника, цвет обводки (stroke) и цвет заливки. Использование `Color.Transparent` гарантирует, что внутренность остаётся пустой, позволяя просвечивать любой подложенный контент.

## Шаг 5: Save PDF File C# – Сохранение документа на диск

Наконец, мы записываем документ в файл. Это шаг **save pdf file c#**, который завершает процесс.

```csharp
// Step 5: Save the PDF to a file
string outputPath = @"C:\Temp\shape.pdf"; // Adjust the path as needed
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved successfully to {outputPath}");
```

> **Совет:** Оберните весь процесс в блок `using` (или вызовите `pdfDocument.Dispose()`), чтобы быстро освобождать нативные ресурсы, особенно при генерации множества PDF в цикле.

## Полный, готовый к запуску пример

Собрав все части вместе, представляем полный код, который можно скопировать и вставить в консольное приложение:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // Add a blank page
            Page page = pdfDocument.Pages.Add();

            // Define rectangle (fits within a standard A4 page)
            var rectangle = new Rectangle(50, 50, 550, 750);

            // Ensure the rectangle fits inside the page boundaries
            if (page.PageInfo.Width >= rectangle.Width && page.PageInfo.Height >= rectangle.Height)
            {
                // Draw the rectangle with a blue border and a transparent fill
                page.AddRectangle(rectangle, Color.Blue, Color.Transparent);
            }
            else
            {
                Console.WriteLine("Rectangle does not fit on the page. Adjust dimensions.");
                return;
            }

            // Save the PDF to a file
            string outputPath = @"C:\Temp\shape.pdf"; // Change to your desired folder
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF created at: {outputPath}");
        }
    }
}
```

### Ожидаемый результат

Откройте `shape.pdf`, и вы увидите одну страницу формата A4 с прямоугольником, обведённым синей линией, расположенным на 50 pt от левого и нижнего краёв. Внутренняя часть прямоугольника прозрачна, поэтому фон страницы остаётся видимым.

![пример создания pdf документа c# с отображением прямоугольника](https://example.com/placeholder.png "пример создания pdf документа c#")

*(Текст альтернативного изображения: **пример создания pdf документа c# с отображением прямоугольника**)  

Если вы измените `Color.Blue` на `Color.Red` или подкорректируете координаты, прямоугольник отразит эти изменения — экспериментируйте.

## Часто задаваемые вопросы и крайние случаи

### Что делать, если нужен другой размер страницы?

Вы можете задать размеры страницы перед добавлением содержимого:

```csharp
Page customPage = pdfDocument.Pages.Add();
customPage.SetPageSize(PageSize.Letter.Width, PageSize.Letter.Height);
```

Не забудьте повторно выполнить логику **check PDF page size** после изменения размеров.

### Могу ли я рисовать другие фигуры?

Конечно. Aspose.Pdf предоставляет `AddCircle`, `AddEllipse`, `AddLine` и даже свободные формы `Path`. Применяется тот же шаблон — определить геометрию, проверить границы, затем вызвать соответствующий метод `Add*`.

### Как заполнить прямоугольник цветом?

Замените `Color.Transparent` на любой сплошной цвет:

```csharp
page.AddRectangle(rectangle, Color.Blue, Color.LightGray);
```

### Можно ли добавить текст внутри прямоугольника?

Конечно. После рисования прямоугольника добавьте `TextFragment`, расположенный внутри координат прямоугольника:

```csharp
var tf = new TextFragment("Hello, world!");
tf.Rect = new Rectangle(60, 60, 540, 730); // Slightly inset
page.Paragraphs.Add(tf);
```

## Заключение

Мы только что показали, как **create PDF document C#**, **add blank page PDF**, **check PDF page size**, **draw rectangle PDF** и, наконец, **save PDF file C#** — всё в лаконичном, сквозном примере. Код готов к запуску, объяснения раскрывают *почему* каждого шага, и теперь у вас есть прочная база для более сложных задач генерации PDF.

Готовы к следующему вызову? Попробуйте накладывать несколько фигур, вставлять изображения или генерировать таблицы — всё это следует тому же шаблону, который мы использовали. И если когда‑нибудь понадобится изменить размеры страниц или перейти на другую PDF‑библиотеку, концепции останутся теми же.

Удачной разработки, и пусть ваши PDF‑файлы всегда отображаются точно так, как вы задумали!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}