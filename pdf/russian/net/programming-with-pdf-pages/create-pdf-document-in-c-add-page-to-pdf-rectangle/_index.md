---
category: general
date: 2026-02-10
description: Создайте PDF‑документ на C# с помощью Aspose.Pdf. Узнайте, как добавить
  страницу в PDF и как безопасно добавить прямоугольник в PDF, используя проверку
  границ.
draft: false
keywords:
- create pdf document
- add page to pdf
- how to add rectangle pdf
language: ru
og_description: Создайте PDF‑документ на C# с помощью Aspose.Pdf. Это руководство
  показывает, как добавить страницу в PDF и как добавить прямоугольник в PDF, проверяя
  границы.
og_title: Создание PDF‑документа в C# – добавление страницы в PDF и прямоугольника
tags:
- pdf
- csharp
- aspose
title: Создание PDF‑документа в C# – добавление страницы в PDF и прямоугольника
url: /ru/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/
---

content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF‑документа в C# – Добавление страницы в PDF и прямоугольника

Когда‑то вам нужно **create pdf document** в C#, но вы не знаете, с чего начать? Вы не одиноки — большинство разработчиков сталкиваются с тем же препятствием, когда впервые пробуют библиотеки генерации PDF. Хорошая новость в том, что с Aspose.Pdf вы можете быстро создать PDF, добавить страницу в PDF и даже нарисовать фигуры, такие как прямоугольник, без особых усилий.

В этом руководстве мы пройдём полный, готовый к запуску пример, который не только **creates a PDF document**, но и демонстрирует **how to add rectangle PDF** объекты безопасно, включив глобальную проверку границ. К концу вы будете уверенно пользоваться API, поймёте, почему каждый шаг важен, и увидите ожидаемый результат.

## Что понадобится

- .NET 6+ (или .NET Framework 4.6+). Код работает одинаково в обеих средах.  
- NuGet‑пакет Aspose.Pdf for .NET (`Aspose.Pdf`) — установите его через `dotnet add package Aspose.Pdf`.  
- Любой редактор C# (Visual Studio, VS Code, Rider… выбирайте сами).

Дополнительная конфигурация не требуется; библиотека поставляется со всем необходимым для мгновенного создания PDF‑файлов.

## Шаг 1: Создать PDF‑документ и включить проверку границ

Первое, что мы делаем, — создаём объект `Document`. Считайте его чистым холстом для вашего **create pdf document** приключения. Сразу после этого включаем глобальную настройку, заставляющую библиотеку проверять, что каждый графический объект остаётся внутри области страницы. Это критично, когда позже вы будете рисовать фигуры, которые могут выходить за пределы.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Initialise a new PDF document
using var document = new Document();

// Step 1b: Turn on boundary checking for all graphics objects
document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;
```

*Зачем включать проверку границ?*  
Если вы случайно разместите прямоугольник за пределами страницы, Aspose бросит `PdfException`. Раннее обнаружение такой ошибки спасает от повреждённых PDF, которые некоторые просмотрщики отказываются открывать.

## Шаг 2: Добавить страницу в PDF

PDF без страниц — как книга без листов, совершенно бесполезна. Добавить страницу можно простым вызовом `Pages.Add()`. Метод возвращает объект `Page`, который вы будете использовать для размещения содержимого.

```csharp
// Step 2: Add a new page (this is the “add page to pdf” part)
Page page = document.Pages.Add();
```

> **Pro tip:** Размер страницы по умолчанию в Aspose — 595 × 842 пункта (A4). Если нужен другой размер, задайте `page.PageInfo.Width` и `page.PageInfo.Height` до добавления контента.

## Шаг 3: Определить прямоугольник, который будет выходить за границы

Теперь переходим к основной части **how to add rectangle pdf** объектов. Мы намеренно создаём прямоугольник, превышающий размеры страницы, чтобы увидеть исключение в действии. Конструктор `Rectangle` принимает четыре аргумента: *нижний‑левый X, нижний‑левый Y, верхний‑правый X, верхний‑правый Y*.

```csharp
// Step 3: Create a rectangle that goes beyond the page edges
// Page size: 595x842, so X=800 and Y=900 are out of bounds
var outOfBoundsRect = new Rectangle(400, 750, 800, 900);
```

Если запустить код с отключённой проверкой границ, прямоугольник просто будет обрезан. При включённой проверке Aspose выдаст ошибку, что именно нам нужно для надёжных конвейеров генерации PDF.

## Шаг 4: Сформировать фигуру и задать видимую рамку

Прямоугольник сам по себе невидим, если не добавить рамку или заливку. Здесь мы оборачиваем `Rectangle` в объект формы `Rectangle` (да, название класса немного сбивает с толку) и задаём тонкую чёрную рамку.

```csharp
// Step 4: Turn the rectangle into a shape and add a border
var rectangleShape = new Rectangle(outOfBoundsRect)
{
    Border = new BorderInfo(BorderSide.All, 1f)   // 1‑point black border
};
```

*Зачем нужна рамка?*  
Без рамки вы ничего не увидите на странице, что усложняет отладку. Тонкая рамка также явно показывает, когда фигура выходит за границы.

## Шаг 5: Добавить фигуру на страницу — ожидать исключения

Теперь действительно размещаем фигуру на странице. Поскольку прямоугольник превышает пределы страницы и мы включили проверку границ, Aspose бросит `PdfException`. Мы оборачиваем вызов в блок `try/catch`, чтобы продемонстрировать корректную обработку ошибок.

```csharp
// Step 5: Attempt to add the shape – this will raise an exception
try
{
    page.Paragraphs.Add(rectangleShape);
}
catch (PdfException ex)
{
    Console.WriteLine("Caught PdfException: " + ex.Message);
    // Handle the error – maybe adjust the rectangle or log the issue
}
```

Если закомментировать строку `CheckGraphicsObjectBoundaries` в Шаге 1, код выполнится успешно, а прямоугольник будет обрезан по краям страницы. Такое поведение удобно для быстрых прототипов, но в продакшене обычно нужен защитный механизм.

## Шаг 6: Сохранить PDF

Наконец, сохраняем документ на диск. Файл будет создан в указанной папке; убедитесь, что путь существует, или используйте `Path.Combine` с `Environment.CurrentDirectory`.

```csharp
// Step 6: Save the resulting PDF
string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
document.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Когда откроете `checked_shapes.pdf`, вы увидите пустую страницу (потому что прямоугольник был отклонён). Если отключить проверку границ, вы увидите частично нарисованный прямоугольник, обрезанный справа и сверху.

---

![Пример создания PDF‑документа, показывающий проверку границ прямоугольника](https://example.com/images/checked_shapes.png "Пример создания PDF‑документа с проверкой границ прямоугольника")

*Скриншот выше иллюстрирует PDF после выполнения руководства с отключённой проверкой границ (прямоугольник обрезан). При включённой проверке фигура отсутствует, а исключение записывается в лог.*

## Итоги: Полный рабочий пример

Объединяя всё вместе, получаем полностью готовую к запуску программу:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise document and enable boundary checking
        using var document = new Document();
        document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;

        // 2️⃣ Add a page (add page to pdf)
        Page page = document.Pages.Add();

        // 3️⃣ Define an out‑of‑bounds rectangle (how to add rectangle pdf)
        var outOfBoundsRect = new Rectangle(400, 750, 800, 900);

        // 4️⃣ Create shape with a visible border
        var rectangleShape = new Rectangle(outOfBoundsRect)
        {
            Border = new BorderInfo(BorderSide.All, 1f)
        };

        // 5️⃣ Try to add the shape – expect an exception
        try
        {
            page.Paragraphs.Add(rectangleShape);
        }
        catch (PdfException ex)
        {
            Console.WriteLine("Caught PdfException: " + ex.Message);
        }

        // 6️⃣ Save the PDF
        string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
        document.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

Запустите программу, и в консоли появится сообщение, подтверждающее, что исключение было перехвачено. Откройте сгенерированный PDF, чтобы убедиться в результате.

## Часто задаваемые вопросы и особые случаи

- **А что если нужен другой размер страницы?**  
  Задайте `page.PageInfo.Width` и `page.PageInfo.Height` перед добавлением фигур. Проверка границ автоматически использует новые размеры.

- **Можно ли отключить проверку границ только для одной фигуры?**  
  Не напрямую. Настройка глобальная, но вы можете временно выключить её, добавить фигуру, затем снова включить — только помните, что в этот момент теряется защита.

- **Полезно ли сообщение об исключении?**  
  Да, Aspose включает координаты, вызвавшие ошибку, так что вы можете программно скорректировать прямоугольник или записать подробную диагностику.

- **Будет ли работать на .NET Core в Linux?**  
  Абсолютно. Aspose.Pdf платформенно‑независим; просто убедитесь, что используемые шрифты доступны в целевой ОС.

## Следующие шаги

Теперь, когда вы знаете **how to add rectangle pdf** объекты и как **add page to pdf**, можно продолжить исследовать:

- Добавление других графических типов (эллипсы, линии) с теми же проверками границ.  
- Вставку текста, изображений или таблиц — у Aspose есть богатый набор API для каждого.  
- Использование перегрузок `Document.Save` для вывода напрямую в `MemoryStream` в веб‑API.

Экспериментируйте с различными координатами прямоугольника, рамками и цветами заливки. Чем больше вы играете, тем лучше понимаете, как работает Aspose.P

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}