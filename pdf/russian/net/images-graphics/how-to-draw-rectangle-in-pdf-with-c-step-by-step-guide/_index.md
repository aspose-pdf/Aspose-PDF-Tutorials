---
category: general
date: 2026-03-27
description: Узнайте, как рисовать прямоугольник в PDF с помощью Aspose.Pdf для C#.
  Добавьте прямоугольник в PDF, добавьте форму в PDF и нарисуйте форму в PDF с понятными
  примерами кода.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: ru
og_description: Освойте, как рисовать прямоугольник в PDF с помощью Aspose.Pdf. Этот
  учебник покажет, как добавить прямоугольник в PDF, добавить форму в PDF и нарисовать
  форму в PDF шаг за шагом.
og_title: Как нарисовать прямоугольник в PDF с помощью C# – Полное руководство
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Как нарисовать прямоугольник в PDF с помощью C# – пошаговое руководство
url: /ru/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как нарисовать прямоугольник в PDF с помощью C# – пошаговое руководство

Когда‑нибудь задавались вопросом **how to draw rectangle** в PDF без борьбы с низкоуровневым синтаксисом PDF? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда им нужно визуализировать ограничивающий блок, выделенную область или простой декоративный элемент внутри сгенерированного документа. Хорошая новость? С Aspose.Pdf for .NET процесс прост как раз.

В этом руководстве мы пройдем всё, что вам нужно, чтобы **add rectangle to PDF**, **add shape to PDF**, и в конечном итоге **draw rectangle in PDF** с использованием чистого, идиоматичного C#. К концу вы получите исполняемую программу, которая генерирует PDF‑файл, содержащий чёткий прямоугольник — без необходимости во внешних инструментах.

## Требования

- .NET 6.0 или новее (код работает также с .NET Core и .NET Framework)
- NuGet‑пакет Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- Базовая среда разработки C# (Visual Studio, VS Code, Rider и т.д.)

Другие библиотеки не требуются; всё остальное обрабатывается самим Aspose.Pdf.

## Шаг 1: Настройка проекта и импорт пространств имён

Сначала создайте новое консольное приложение и подключите пространство имён Aspose.Pdf.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Почему это важно:** Импорт `Aspose.Pdf.Drawing` предоставляет доступ к классу формы `Rectangle`, который мы будем использовать для **draw shape on PDF**. Сохранение чистоты точки входа упрощает последующие шаги.

## Шаг 2: Создание нового PDF‑документа и страницы

PDF без страниц бессмыслен, поэтому мы начинаем с создания объекта документа и добавления единственной страницы.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Объяснение:** Класс `Document` представляет весь файл, а `Pages.Add()` возвращает новый объект `Page`, куда мы позже **add rectangle to PDF**. Размер A4 по умолчанию подходит для большинства случаев, но при необходимости можно задать ширину/высоту для пользовательского холста.

## Шаг 3: Определение формы Rectangle

Теперь переходим к сути **how to draw rectangle** — определению её позиции и размеров.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Почему мы задаём эти свойства:**  
- `BorderColor` и `BorderWidth` управляют контуром, делая прямоугольник видимым.  
- `FillColor` задаёт нежный фон, полезный, когда нужно выделить область.  
- Конструктор `(x, y, width, height)` позволяет **draw rectangle in PDF** точно там, где это необходимо.

## Шаг 4: Добавление прямоугольника на страницу

Когда форма готова, мы теперь **add shape to PDF**, присоединив её к коллекции `Annotations` страницы. Aspose.Pdf автоматически проверяет границы, так что вам не о чем беспокоиться.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Что происходит за кулисами:** Коллекция `Annotations` рассматривает прямоугольник как векторную графику. При рендеринге PDF библиотека преобразует наши координаты в поток содержимого PDF.

## Шаг 5: Сохранение документа

Наконец, запишите PDF на диск, чтобы открыть его в любом просмотрщике.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Результат:** При открытии `RectangleDemo.pdf` отображается светло‑серый прямоугольник с чёрной рамкой, расположенный на 100 pt от левого края и 500 pt от нижнего края страницы. Это полное решение для **how to draw rectangle** в PDF с использованием C#.

## Полный рабочий пример

Собрав все части вместе, представляем полный, готовый к запуску код:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Ожидаемый результат:** Файл с именем `RectangleDemo.pdf`, содержащий одну страницу с центрированным светло‑серым прямоугольником, обведённым чёрной линией. Вы можете открыть его в Adobe Reader, Chrome или любом PDF‑просмотрщике.

## Распространённые варианты и граничные случаи

### 1. Рисование нескольких прямоугольников

Если вам нужно **add rectangle to PDF** более одного раза, просто создайте дополнительные объекты `Rectangle` и добавьте каждый в `page.Annotations`. Перебор коллекции координат делает это тривиальным.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Использование разных единиц измерения

Aspose.Pdf работает в пунктах (1 pt = 1/72 дюйма). Если вы предпочитаете миллиметры, сначала выполните преобразование:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Добавление прямоугольника как поля формы

Когда требуется интерактивный прямоугольник (например, кликабельная область), используйте `LinkAnnotation` вместо простого `Rectangle`. Код похож, но добавляет URL или действие JavaScript.

### 4. Проблемы совместимости

Версия Aspose.Pdf 23.9 (выпущена в начале 2026) полностью поддерживает показанные выше API. Более старые версии могут требовать `page.AddAnnotation(rectangleShape)` вместо `page.Annotations.Add`. Всегда проверяйте примечания к выпуску, если столкнётесь с ошибками компиляции.

## Профессиональные советы и подводные камни

- **Pro tip:** Установите `FillColor = Color.Transparent`, если нужен только контур. Это немного уменьшит размер файла.
- **Watch out for:** Использование координат, выходящих за пределы страницы. Aspose.Pdf будет тихо обрезать форму, что может сбивать с толку при отладке.
- **Performance note:** Добавление тысяч прямоугольников допустимо, но при генерации больших отчётов рассмотрите группировку фигур в один объект `Graphics` для снижения нагрузки.

## Визуальная ссылка

Ниже представлен быстрый скриншот сгенерированного PDF (прямоугольник выделен светло‑серым). Текст alt включает основной ключевой запрос для SEO.

![how to draw rectangle in PDF example](https://example.com/images/rectangle-demo.png "how to draw rectangle in PDF example")

## Заключение

Мы рассмотрели **how to draw rectangle** в PDF с помощью Aspose.Pdf для C#. Создав `Document`, добавив `Page`, определив форму `Rectangle` и, наконец, **adding shape to PDF**, вы можете генерировать векторную графику всего несколькими строками кода. Независимо от того, нужно ли вам **add rectangle to pdf** для выделения, отладки макета или наложения UI, такой подход масштабируется без проблем.

Далее вы можете изучить **draw shape on pdf** помимо прямоугольников — подумайте о кругах, полилиниях или даже пользовательских SVG‑путях. Или погрузиться в рендеринг текста, вставку изображений и работу с формами PDF, чтобы создавать полнофункциональные отчёты. Библиотека Aspose.Pdf предоставляет богатый API, и с учётом изложенных здесь основ вы готовы к экспериментам.

Счастливого кодинга, и пусть ваши PDF всегда выглядят точно так, как вы себе представляете!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}