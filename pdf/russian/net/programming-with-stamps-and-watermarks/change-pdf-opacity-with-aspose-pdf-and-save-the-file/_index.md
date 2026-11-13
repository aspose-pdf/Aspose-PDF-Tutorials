---
category: general
date: 2026-11-12
description: Узнайте, как изменить непрозрачность PDF с помощью Aspose.Pdf, добавить
  прозрачность, установить режим наложения и сохранить изменённый PDF в C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: ru
lastmod: 2026-11-12
og_description: Измените непрозрачность PDF с помощью Aspose.Pdf, узнайте, как добавить
  прозрачность, установить режим наложения и сохранить изменённые PDF‑файлы в C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Изменить непрозрачность PDF с помощью Aspose.Pdf — добавить прозрачность
  и сохранить
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Изменить непрозрачность PDF с помощью Aspose.Pdf и сохранить файл
url: /ru/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Изменение непрозрачности PDF с помощью Aspose.Pdf и сохранение файла

Если вам нужно **изменить непрозрачность PDF** в документе, Aspose.Pdf предоставляет простой API для настройки как прозрачности линий (stroke), так и заливки (fill). В этом руководстве показано, **как добавить прозрачность**, **как установить режим смешивания**, и **сохранить изменённые PDF** файлы всего несколькими строками кода на C#.

Вы пройдёте каждый шаг — от загрузки существующего PDF до определения нового графического состояния и сохранения изменений. К концу этого руководства вы сможете:

* Снизить видимость векторной графики или изображений.
* Применить пользовательский режим смешивания, такой как *Normal* или *Multiply*.
* Экспортировать обновлённый файл без потери любого другого содержимого.

Единственное требование — рабочая среда разработки .NET и ссылка на библиотеку Aspose.Pdf (версия 23.9 или новее). Внешние инструменты не требуются.

## Требования

| Требование | Почему это важно |
|-------------|----------------|
| .NET 6.0 SDK or later | Гарантирует совместимость с последними API Aspose.Pdf. |
| Aspose.Pdf for .NET NuGet package | Предоставляет классы `Document`, `CosPdfDictionary` и связанные, используемые в коде. |
| A PDF file to edit (e.g., `input.pdf`) | Служит источником для изменения непрозрачности. |

Install the NuGet package with:

```bash
dotnet add package Aspose.Pdf
```

## Изменение непрозрачности PDF с помощью Aspose.Pdf

### Шаг 1: Загрузка PDF‑документа

Начните с создания экземпляра `Document`, указывающего на ваш исходный файл. Конструктор считывает весь PDF в память, позволяя вам манипулировать его внутренними объектами.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Зачем этот шаг?** Загрузка файла создаёт управляемую объектную модель. Все последующие изменения применяются к этой представлению в памяти, гарантируя, что оригинальный файл остаётся нетронутым до тех пор, пока вы явно не сохраните его.

### Шаг 2: Доступ к ресурсам первой страницы

Каждая страница PDF хранит *словарь ресурсов*, содержащий объекты, такие как шрифты, изображения и графические состояния. Вам необходимо отредактировать этот словарь, чтобы добавить новую запись `ExtGState`.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Подсказка:** Если ваш PDF содержит несколько страниц, которым требуется одинаковая непрозрачность, повторите этот шаг для каждой страницы или используйте один `ExtGState` для всех страниц.

### Шаг 3: Убедитесь, что словарь ExtGState существует

`ExtGState`‑словарь хранит пользовательские графические состояния. Если он не существует, код создаст его автоматически.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Зачем этот шаг?** Без контейнера `ExtGState` любая попытка сослаться на новое графическое состояние завершится неудачей, и PDF будет игнорировать ваши настройки непрозрачности.

### Шаг 4: Определение нового графического состояния (ExtGState)

Графическое состояние определяет, как ведут себя операции рисования. Следующий словарь задаёт непрозрачность линий (`CA`), непрозрачность заливки (`ca`) и режим смешивания (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Как установить непрозрачность заливки:** Запись `ca` управляет непрозрачностью заполненных фигур (текст, контуры). Установите числовое значение от `0` (полностью прозрачно) до `1` (полностью непрозрачно), чтобы соответствовать требованиям вашего дизайна.  
> **Как установить режим смешивания:** Запись `BM` выбирает алгоритм композиции. Распространённые значения включают `Normal`, `Multiply`, `Screen` и `Overlay`. Выберите тот, который соответствует вашему визуальному замыслу.

### Шаг 5: Регистрация графического состояния в словаре ресурсов

Назовите новое состояние (например, `GS0`) и добавьте его в словарь `ExtGState`. Это имя будет использовано позже в потоке содержимого страницы.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Профессиональный совет:** При создании нескольких состояний используйте схему именования вроде `GS0`, `GS1`, … Это предотвращает конфликты имён и упрощает отладку.

### Шаг 6: Применение графического состояния к содержимому страницы

Чтобы увидеть эффект непрозрачности, вставьте оператор `/GS0 gs` перед командами рисования, которые вы хотите затронуть. Пример ниже рисует полупрозрачный прямоугольник.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Зачем операторы `q` и `Q`?** Они помещают и извлекают графическое состояние из стека, гарантируя, что изменение непрозрачности затронет только прямоугольник, а не остальную часть страницы.

### Шаг 7: Сохранение изменённого PDF

Наконец, запишите обновлённый документ на диск. Метод `Save` перезаписывает целевой файл или создаёт новый, если он не существует.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Как сохранить изменённый PDF:** Вызов `Save` записывает все изменения в памяти, включая новый `ExtGState`, по указанному пути. Вы также можете передать результат в `MemoryStream` для веб‑ответов.

## Полный рабочий пример

Ниже представлен единый, автономный пример программы, включающий каждый шаг, описанный выше. Скопируйте его в консольное приложение и запустите, чтобы проверить изменение непрозрачности.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## Что изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как сохранить изменённый PDF с помощью Aspose.Pdf и добавить прозрачность](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Как добавить прозрачность в PDF с использованием Aspose.PDF на C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Как добавить графическое состояние в PDF и управлять прозрачностью с помощью Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}