---
category: general
date: 2026-08-14
description: Быстро нарисовать прямоугольник в PDF с помощью C#. Узнайте, как задать
  размеры прямоугольника и добавить фигуры на страницу PDF всего за несколько строк.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: ru
lastmod: 2026-08-14
og_description: Нарисуйте прямоугольник в PDF с помощью C# за считанные секунды. Это
  руководство показывает, как задать размеры прямоугольника, добавить форму и проверить
  границы страницы для надёжной графики PDF.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: Рисуем прямоугольник в PDF – полный учебник по C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Рисуем прямоугольник в PDF – пошаговое руководство по C#
url: /ru/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# рисование прямоугольника в pdf – полный учебник C#

Если вам нужно **draw rectangle on pdf** с использованием C#, это руководство покажет вам лаконичное, готовое к продакшену решение. Вы увидите точно **how to define rectangle dimensions**, проверите, что фигура помещается, и добавите её на страницу одним вызовом метода.

Учебник охватывает всё от создания PDF‑документа до отрисовки прямоугольника, так что вы можете скопировать‑вставить код в свой проект и увидеть результаты мгновенно. Внешняя документация не требуется — просто следуйте шагам ниже.

## Предварительные требования

* .NET 6.0 или новее (код также работает с .NET Framework 4.7+)
* Пакет NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
* Базовое понимание синтаксиса C#
* IDE, например Visual Studio или VS Code

> **Pro tip:** Используйте бесплатную оценочную лицензию Aspose.PDF для быстрых экспериментов; она добавляет небольшой водяной знак, но позволяет протестировать все функции.

## Как нарисовать прямоугольник в PDF с помощью C#

Суть задачи — создать `RectangleShape`, задать его размер и обводку, и прикрепить к `Page`. Следующий заголовок H2 содержит основной ключевой запрос, удовлетворяя требованиям SEO.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Пояснение каждого шага

| Step | Зачем это нужно |
|------|-----------------|
| **1️⃣ Create a new PDF document** | Инициализирует контейнер, который будет хранить страницы и графику. |
| **2️⃣ Add a blank page** | Вам нужен объект `Page`, потому что фигуры привязываются к странице, а не напрямую к документу. |
| **3️⃣ Define the rectangle bounds** | Здесь вы **how to define rectangle dimensions**. Конструктор `Rectangle` принимает `x`, `y`, `width` и `height` в пунктах (1 pt = 1/72 in). |
| **4️⃣ Create the rectangle shape** | `RectangleShape` — класс Aspose, который отрисовывает прямоугольник. Установка `StrokeColor` задаёт контур; также можно задать `FillColor` для сплошного заполнения. |
| **5️⃣ Verify page boundaries** | `CheckShapeBoundary` бросает исключение, если прямоугольник превышает размер страницы, предотвращая повреждённые PDF. |
| **6️⃣ Add the shape to the page** | Фигура становится частью потока содержимого страницы. |
| **7️⃣ Save the PDF** | Сохраняет документ в файл, который можно открыть в любом PDF‑просмотрщике. |

Полученный `RectangleDemo.pdf` содержит чёрный прямоугольник, расположенный в верхнем левом углу страницы, шириной ровно 500 pt и высотой 700 pt.

![пример рисования прямоугольника в pdf](https://example.com/rectangle-demo.png "пример рисования прямоугольника в pdf")

*Текст alt изображения: пример рисования прямоугольника в pdf, показывающий чёрный прямоугольник в верхнем левом углу страницы PDF.*

## Как задать размеры прямоугольника для разных размеров страниц

В приведённом выше фрагменте используются фиксированные значения (`500 x 700`). В реальных приложениях часто требуется, чтобы прямоугольник адаптировался к ширине и высоте страницы.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Ключевые моменты:**

* Используйте `page.PageInfo.Width` и `Height` для чтения фактического размера страницы.
* Умножение на коэффициент (например, `0.8f`) позволяет задавать размеры в процентах от страницы.
* Центрирование достигается вычитанием размеров прямоугольника из размеров страницы и делением остатка пополам.

## Распространённые подводные камни и как их избежать

| Подводный камень | Почему происходит | Решение |
|------------------|-------------------|---------|
| Прямоугольник выходит за пределы страницы | Жёстко заданные размеры больше размера страницы. | Вызовите `page.CheckShapeBoundary` **до** добавления фигуры; при возникновении исключения скорректируйте размеры. |
| Контур не виден | `StrokeColor` оставлен по умолчанию (`Color.Empty`). | Явно задайте `StrokeColor` (например, `Color.Black`). |
| Прямоугольник появляется за пределами видимой области | Координаты в PDF начинаются с нижнего левого угла; использование координат в стиле экрана (верхний‑левый) приводит к инверсии. | Помните, что начало координат `(0,0)` находится в нижнем левом углу. Скорректируйте `y` соответственно или используйте `pageHeight - desiredY`. |
| Неожиданная толщина линии | Ширина линии по умолчанию может быть слишком тонкой для печати. | Установите `rectangleShape.LineWidth = 2;` чтобы увеличить толщину. |

## Расширение примера

Как только вы сможете **draw rectangle on pdf**, вы легко сможете добавить другие фигуры:

* **EllipseShape** – для кругов или овалов.
* **PolygonShape** – для пользовательских многоугольников.
* **TextFragment** – для подписи ваших прямоугольников.

Все фигуры используют один и тот же рабочий процесс: задайте границы, настройте внешний вид, проверьте границы, затем добавьте на страницу.

## Полный, исполняемый пример

Ниже представлена полная программа, объединяющая базовый прямоугольник и пример динамического масштабирования. Скопируйте её в новый консольный проект, восстановите пакет NuGet `Aspose.PDF` и запустите.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Ожидаемый результат:**  
Откройте `CombinedRectangles.pdf`. Вы увидите чёрный прямоугольник, привязанный к нижнему левому углу, и центрированный тёмно‑синий прямоугольник со светло‑жёлтой заливкой. Оба прямоугольника учитывают поля страницы.

## Заключение

Теперь вы знаете, как **draw rectangle on pdf** с помощью C# и точно **how to define rectangle dimensions** для фиксированных и адаптивных макетов. Подход использует `RectangleShape` из Aspose.PDF, проверку границ и простую арифметику для адаптации к любому размеру страницы.

Далее вы можете изучить:

* Добавление **fill colors** и **line styles** (пунктирные, точечные) – вторичный запрос: how to define rectangle dimensions with style.
* Объединение нескольких фигур в один `Page` для создания диаграмм или форм.
* Экспорт PDF в поток для веб‑API вместо сохранения на диск.

Экспериментируйте с различными размерами, цветами и позициями, чтобы освоить графику PDF в ваших .NET‑приложениях. Приятного кодинга!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в ваших проектах.

- [Как настроить PDF с помощью Aspose.PDF for .NET: установить поля страницы и рисовать линии](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Как добавить штампы страниц в PDF с помощью Aspose.PDF for .NET: полное руководство](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Как добавить штампы номеров страниц в PDF с помощью Aspose.PDF for .NET | Водяные знаки и фоны](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}