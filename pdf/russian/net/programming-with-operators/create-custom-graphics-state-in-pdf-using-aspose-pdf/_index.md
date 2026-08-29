---
category: general
date: 2026-08-20
description: Создайте пользовательское графическое состояние в PDF с помощью Aspose.Pdf.
  Узнайте, как редактировать ресурсы PDF и добавить прозрачность в PDF всего за несколько
  шагов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: ru
lastmod: 2026-08-20
og_description: Создайте пользовательское графическое состояние в PDF с помощью Aspose.Pdf.
  Этот учебник показывает, как быстро редактировать ресурсы PDF и добавлять прозрачность.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Создание пользовательского графического состояния в PDF – руководство Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Создание пользовательского графического состояния в PDF с помощью Aspose.Pdf
url: /ru/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание пользовательского графического состояния в PDF с использованием Aspose.Pdf

Если вам нужно **создать пользовательское графическое состояние** в PDF, это руководство покажет, как сделать это с помощью Aspose.Pdf для .NET. К концу урока вы сможете **редактировать ресурсы PDF**, внедрить новый словарь графического состояния и **добавить прозрачный PDF** контент, не выходя из вашего проекта C#.

Вы увидите полностью готовый, исполняемый пример, объяснение, почему каждая строка важна, и советы по работе с многостраничными документами или различными режимами смешивания. Внешние инструменты не требуются — только библиотека Aspose.Pdf и базовая среда разработки .NET.

## Требования

Перед тем как начать, убедитесь, что у вас есть:

* .NET 6.0 или новее (код также работает с .NET Framework 4.7+)
* Лицензированную копию **Aspose.Pdf for .NET** (бесплатная пробная версия подходит для тестирования)
* PDF‑файл‑вход `input.pdf`, размещённый в папке, к которой можно обратиться из кода
* Visual Studio 2022 или любую IDE, поддерживающую разработку на C#

В руководстве предполагается, что вы знакомы с базовым синтаксисом C# и концепцией страниц PDF.

## Шаг 1: Загрузить исходный PDF и получить доступ к первой странице

Первая операция — открыть PDF‑файл и получить страницу, ресурсы которой вы хотите изменить. Aspose.Pdf представляет каждую страницу объектом `Page`, и каждая страница содержит **словарь ресурсов**, в котором хранятся графические состояния, шрифты, XObject и многое другое.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Почему это важно:* Класс `Document` загружает файл в память, а `Pages[1]` предоставляет прямой доступ к словарю ресурсов первой страницы, где находится графическое состояние.

## Шаг 2: Открыть словарь ресурсов для редактирования

Aspose.Pdf предоставляет вспомогательный класс `DictionaryEditor`, который позволяет обращаться к словарю ресурсов как к обычному .NET `Dictionary`. Это упрощает чтение, добавление или замену записей, таких как `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Почему это важно:* `DictionaryEditor` абстрагирует низкоуровневые COS‑объекты, позволяя работать с привычными парами ключ/значение, сохраняя при этом соответствие PDF.

## Шаг 3: Получить (или создать) словарь ExtGState

**Запись ExtGState** содержит все внешние объекты графического состояния для страницы. Если словарь не существует, Aspose.Pdf создаст пустой.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Почему это важно:* Отсутствующая запись `ExtGState` вызовет `KeyNotFoundException` позже. Эта проверка позволяет коду работать с PDF, в которых ранее не было определено пользовательское графическое состояние — важный элемент надёжности **редактирования ресурсов PDF**.

## Шаг 4: Сформировать словарь пользовательского графического состояния

Графическое состояние описывает, как отрисовываются операции рисования. Чтобы **добавить прозрачный PDF**, необходимо установить записи `ca` (прозрачность заливки) и `CA` (прозрачность обводки), а при желании — режим смешивания (`BM`). Следующий код создает новый словарь с этими параметрами.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Почему это важно:* Записи `ca` и `CA` управляют прозрачностью заливки и обводки соответственно. Установка `BM` позволяет экспериментировать с различными эффектами композитинга, что полезно, когда позже вы **добавляете прозрачный PDF** контент, например полупрозрачные фигуры или изображения.

## Шаг 5: Зарегистрировать новое графическое состояние под уникальным именем

Каждое графическое состояние в словаре `ExtGState` должно иметь уникальное имя (например, `GS0`, `GS1`). Вы можете выбрать любое имя, которое не конфликтует с существующими записями.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Почему это важно:* Вставляя новый словарь под именем `GS0`, вы делаете состояние доступным из потоков содержимого страницы. Условный блок гарантирует наличие записи `ExtGState` даже в PDF, которые изначально её не имели — ещё одна защита **редактирования ресурсов PDF**.

## Шаг 6: Использовать пользовательское графическое состояние в содержимом страницы (необязательно)

Предыдущие шаги только *определяют* графическое состояние. Чтобы увидеть эффект, необходимо сослаться на него в потоке содержимого страницы. Ниже приведён быстрый пример, рисующий полупрозрачный прямоугольник с использованием только что созданного состояния.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Почему это важно:* Оператор `SetExtGState` (`gs`) указывает рендереру PDF применить параметры, определённые в `GS0`. Прямоугольник будет отображаться с 50 % прозрачностью заливки, а обводка останется полностью непрозрачной.

## Шаг 7: Сохранить изменённый PDF

Наконец, запишите изменения обратно на диск. Вы можете перезаписать оригинальный файл или создать новый.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Когда вы откроете `output_with_custom_gs.pdf` в просмотрщике PDF, вы должны увидеть полупрозрачный прямоугольник на первой странице. Это подтверждает, что вы успешно **создали пользовательское графическое состояние**, **отредактировали ресурсы PDF** и **добавили прозрачный PDF** контент.

## Общие варианты и граничные случаи

| Ситуация | Что нужно изменить |
|-----------|----------------|
| **Несколько страниц нуждаются в одинаковом состоянии** | Зарегистрировать графическое состояние один раз (шаги 1‑5) и ссылаться на `GS0` в потоке содержимого любой страницы. |
| **Разная прозрачность для каждого элемента** | Определить дополнительные состояния (`GS1`, `GS2`, …) с различными значениями `ca`/`CA` и переключаться между ними с помощью `SetExtGState`. |
| **Режим смешивания, отличный от Normal** | Заменить `"Normal"` на `"Multiply"`, `"Screen"` или любой другой стандартный режим смешивания PDF в записи `BM`. |
| **Конфликт имён** | Перед добавлением проверьте `extGStateDict.ContainsKey(yourName)` и при необходимости выберите уникальный суффикс. |
| **PDF уже содержит словарь ExtGState** | Код в Шаге 3 уже переиспользует существующий словарь, поэтому дополнительная обработка не требуется. |

**Полезный совет:** При работе с большими PDF оборачивайте использование `Document` в блок `using` (как показано), чтобы быстро освобождать нативные ресурсы. Также рассмотрите возможность включения свойства `PdfCompliance` в Aspose.Pdf, если необходимо обеспечить соответствие PDF/A или PDF/X после редактирования ресурсов.

## Полный рабочий пример

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как создать PDF с Aspose – добавить поле формы и страницы](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Как создать пользовательские таблицы в PDF с использованием Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Создание пользовательских штампов PDF Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}