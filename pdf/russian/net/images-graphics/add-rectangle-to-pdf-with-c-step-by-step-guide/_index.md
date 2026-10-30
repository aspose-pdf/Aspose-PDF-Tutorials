---
category: general
date: 2026-08-04
description: Добавьте прямоугольник в PDF с помощью C#. Узнайте, как рисовать фигуры
  в PDF на C# с Aspose.Pdf в понятном и полном примере.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: ru
lastmod: 2026-08-04
og_description: Добавьте прямоугольник в PDF с помощью C#. Этот учебник показывает,
  как быстро и надёжно рисовать фигуру в PDF на C#.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Добавление прямоугольника в PDF с C# — полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Добавление прямоугольника в PDF с помощью C# – пошаговое руководство
url: /ru/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавить прямоугольник в PDF с помощью C# – пошаговое руководство

Если вам нужно **add rectangle to PDF** файлы из C# приложения, это руководство покажет вам точно, как это сделать. Вы увидите полный, исполняемый пример, который рисует форму в PDF C# с использованием библиотеки Aspose.Pdf, и поймёте, почему каждая строка кода важна.

Рисование фигур в PDF‑файлах — распространённая потребность для генераторов отчётов, шаблонов счетов и фирменного оформления документов. К концу этого руководства вы сможете вставлять любые прямоугольные аннотации, менять их размер, цвет или позицию и сохранять изменённый документ, не теряя существующее содержимое.

**Что вы узнаете**

* Как загрузить существующий PDF с помощью Aspose.Pdf.
* Как задать границы прямоугольника и создать форму прямоугольника.
* Как добавить прямоугольник в коллекцию абзацев страницы.
* Как сохранить обновлённый PDF и проверить результат.
* Варианты для нескольких страниц, прозрачности и пользовательских стилей линий.

**Требования**

* .NET 6.0 или новее (код также работает с .NET Framework 4.7+).
* Visual Studio 2022 или любой IDE для C#.
* Ссылка NuGet на `Aspose.Pdf` (бесплатная пробная версия или лицензия).
* Входной PDF‑файл с именем `input.pdf`, размещённый в папке, которой вы управляете.

---

## Как нарисовать форму в PDF C# – настройка проекта

1. **Создайте новый консольный проект**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Добавьте пакет Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Поместите `input.pdf`** в каталог проекта (или любую папку, к которой вы будете обращаться позже).

Проект теперь готов к компиляции кода, который будет **add rectangle to PDF** файлы.

---

## Шаг 1: Загрузка PDF‑документа

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*Класс `Document` разбирает файл и предоставляет коллекцию `Pages`. Загрузка — первая необходимая операция перед любым рисованием.*

---

## Шаг 2: Выбор целевой страницы

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Если нужно добавить прямоугольник на другую страницу, замените индекс на требуемый номер страницы. Библиотека бросит исключение, если индекс выходит за пределы, поэтому убедитесь, что в PDF достаточно страниц.*

---

## Шаг 3: Определение границ прямоугольника

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Система координат использует пункты (1 pt = 1/72 дюйма). Пример создаёт прямоугольник шириной 250 pt и высотой 100 pt рядом с верхней частью страницы. Подкорректируйте числа под ваш макет.*

---

## Шаг 4: Создание формы прямоугольника

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*Класс `Rectangle` наследуется от `GraphicalObject`. Установка `FillColor` и `Border` необязательна, но демонстрирует, как управлять внешним видом, когда вы **how to draw shape in PDF C#** за пределами простого контура.*

---

## Шаг 5: Добавление прямоугольника на страницу

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Абзацы являются контейнером для любого рисуемого объекта. Вставляя форму в `Paragraphs`, Aspose.Pdf отрисует её при сохранении документа.*

---

## Шаг 6: Сохранение изменённого PDF

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Сохранение создаёт новый файл, поэтому оригинальный `input.pdf` остаётся без изменений. Вы можете перезаписать исходный файл, указав тот же путь, но хранить резервную копию — лучшая практика.*

---

## Полный исходный код (исполняемый)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Ожидаемый результат** – Откройте `output.pdf` в любом PDF‑просмотрщике. Вы должны увидеть прямоугольник, заполненный синим, в верхнем‑правом углу первой страницы, обведённый тёмно‑серой рамкой.

---

## Как нарисовать форму в PDF C# на нескольких страницах

Если нужно **add rectangle to PDF** на каждой странице, пройдитесь по коллекции `Pages`:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Этот шаблон использует одинаковые границы на каждой странице. При необходимости меняйте координаты для разных страниц.*

---

## Распространённые ошибки и рекомендации по лучшим практикам

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Прямоугольник выходит за пределы страницы | Координаты измеряются от нижнего‑левого угла; использование системы координат, ориентированной сверху, может вызвать путаницу. | Помните, что ось Y растёт вверх. Используйте значения, которые помещаются в размер страницы (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| Фигура невидима | Прозрачность заливки установлена в `0` или ширина границы в `0`. | Убедитесь, что `FillOpacity` больше `0`, а `Border.Width` минимум `0.5`. |
| При сохранении возникает `AccessDeniedException` | Выходной файл открыт в другой программе. | Закройте все просмотрщики перед запуском кода или сохраняйте в другой путь. |
| Прямоугольник перекрывает существующее содержимое | Не задан контроль слоёв. | Используйте свойство `ZIndex` (большие значения рисуются сверху), если нужно управлять порядком слоёв. |

---

## Расширение прямоугольника – градиенты, вращение и прозрачность

Aspose.Pdf поддерживает продвинутую графику. Чтобы создать вращающийся прямоугольник с линейным градиентом:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Тот же шаблон кода демонстрирует **how to draw shape in PDF C#** с более богатыми визуальными эффектами.*

---

## Программная проверка результата

Вы можете подтвердить добавление прямоугольника, проверив количество абзацев на странице:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Если количество увеличилось на один после вставки, операция прошла успешно.

---

## Заключение

Теперь вы знаете, как **add rectangle to PDF** файлы с помощью C#. В руководстве рассмотрены загрузка документа, определение границ, создание формы прямоугольника, вставка её в страницу и сохранение результата. Вы также увидели, как работать с несколькими страницами, избегать типичных ошибок и применять расширенное стилизование.

Далее изучайте связанные темы, такие как **how to draw shape in PDF C#** для кругов, многоугольников или произвольных путей, а также комбинируйте фигуры с текстом и изображениями для создания полнофункциональных PDF‑отчётов.

Счастливого кодинга!

## Что стоит изучить дальше?

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}