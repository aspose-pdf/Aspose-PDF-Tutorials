---
category: general
date: 2026-10-26
description: Научитесь создавать пустой словарь PDF и редактировать ресурсы PDF с
  помощью Aspose.PDF для C#. Пошаговое руководство с полным примером кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: ru
lastmod: 2026-10-26
og_description: Создайте пустой словарь PDF и отредактируйте ресурсы PDF с помощью
  Aspose.PDF для C#. Следуйте этому полному руководству, чтобы изменить графические
  состояния в PDF.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Создание пустого словаря PDF и редактирование ресурсов PDF в C# — руководство
  Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Как создать пустой словарь PDF и редактировать ресурсы PDF с помощью Aspose.PDF
  в C#
url: /ru/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать пустой словарь PDF и редактировать ресурсы PDF с помощью Aspose.PDF в C#

Если вам нужно **создать пустой словарь PDF** и затем **редактировать ресурсы PDF** в приложении C#, это руководство покажет точные шаги. Вы увидите полностью готовый, исполняемый пример, который добавляет пользовательское графическое состояние на первую страницу существующего PDF.

Работа с объектами PDF низкого уровня может показаться сложной, но Aspose.PDF предоставляет понятный API для манипуляций со словарями. К концу этого урока вы поймёте, почему каждое действие важно, и как адаптировать код для других типов ресурсов.

## Prerequisites

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 (или новее) установлен.
* Лицензированная копия **Aspose.PDF for .NET** – бесплатная пробная версия подходит для тестирования.
* IDE, например Visual Studio 2022.
* PDF‑файл с именем `input.pdf`, размещённый в папке, к которой вы сможете обратиться из кода.

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Pdf`.

## Step 1: Set up the project and import namespaces

Создайте новый консольный проект и добавьте пакет Aspose.PDF:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

В `Program.cs` импортируйте необходимые пространства имён:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Эти импорты открывают классы `Document`, `DictionaryEditor` и COS (Canonical Object Structure), которые позволяют **создавать пустой словарь PDF** и изменять существующие словари ресурсов.

## Step 2: Define the folder that contains the PDF files

Укажите каталог, в котором находится `input.pdf`. Использование абсолютного пути избавляет от неоднозначности, когда программа запускается из другой рабочей директории.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

Замените `C:\PdfDemo\` на путь в вашей системе. Хранение пути в переменной упрощает повторное использование его для входных и выходных файлов.

## Step 3: Open the source PDF document

Загрузите PDF, который нужно изменить, внутри блока `using`, чтобы дескриптор файла освобождался автоматически.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

Открытие документа даёт доступ к коллекции страниц, словарям ресурсов и объектам COS низкого уровня.

## Step 4: Access the first page and its resource dictionary

Первая страница имеет индекс `1` (страницы PDF нумеруются с 1). Получите словарь `Resources` страницы и оберните его в `DictionaryEditor` для безопасного редактирования.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` абстрагирует внутреннюю структуру COS, позволяя читать или создавать записи без риска повредить PDF.

## Step 5: **Create empty PDF dictionary** for a new graphics state

Графическое состояние управляет прозрачностью, режимом смешивания и другими параметрами рисования. Чтобы добавить пользовательское состояние, сначала нужен пустой словарь, затем его нужно заполнить требуемыми записями.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

Вызов `CreateEmptyDictionary` — ядро процесса **создания пустого словаря PDF**. Он возвращает COS‑словарь, принадлежащий тому же документу, что гарантирует целостность кросс‑ссылок.

### Populate the graphics state entries

Добавьте стандартные ключи:

* `CA` — постоянная альфа для обводки (диапазон 0 – 1).
* `ca` — постоянная альфа для заливки.
* `BM` — имя режима смешивания.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Каждая запись добавляется в только что созданный пустой словарь. Разделяя определение и цикл вставки, код остаётся читаемым и легко расширяется дополнительными ключами.

### Register the new graphics state in the resource dictionary

Назовите состояние (`GS0`) и добавьте его в словарь `ExtGState`, который находится внутри ресурсов страницы.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Теперь словарь ресурсов страницы содержит ссылку на пользовательское графическое состояние, которое позже можно применить к потокам содержимого.

## Step 6: Save the updated PDF

Наконец, запишите изменённый документ в новый файл. Сохранение оригинала нетронутым помогает проверить изменения.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

Когда откроете `output.pdf` в просмотрщике, поддерживающем инспекцию графических состояний (например, Adobe Acrobat Pro), вы увидите, что словарь `ExtGState` содержит запись с именем `GS0` и заданными значениями.

## Full source code

Собрав все части вместе, получаем автономную программу:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Expected output

Запуск программы выводит:

```
PDF updated successfully.
```

и создаёт `output.pdf` в той же папке. Открытие файла показывает новую запись в **Resources → ExtGState → GS0** с указанными параметрами.

## Common variations and edge cases

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Multiple pages** need the same graphics state | Create the dictionary once, then add the same `GS0` reference to each page’s `ExtGState` dictionary. |
| **Different blend mode** (e.g., `Multiply`) | Change the `CosPdfName("Normal")` value to `CosPdfName("Multiply")`. |
| **No existing ExtGState dictionary** | Before accessing `resourcesEditor["ExtGState"]`, check `resourcesEditor.ContainsKey("ExtGState")`. If missing, create a new empty dictionary and add it to `firstPage.Resources`. |
| **Large PDFs** cause memory pressure | Use `PdfDocument.Load` overload that streams pages, or process pages one at a time inside the `using` block. |
| **Need to edit other resources** (fonts, XObjects) | Replace `"ExtGState"` with `"Font"` or `"XObject"` in the `resourcesEditor` lookup, then follow the same pattern of creating an empty dictionary and populating it. |

Эти варианты демонстрируют, как тот же шаблон **создания пустого словаря PDF** применяется к любому типу ресурса, который вы хотите **редактировать ресурсы PDF**.

## Pro tips

* **Validate the result** — после сохранения откройте PDF в инструменте, способном отобразить сырой словарь ресурсов (например, PDF‑Box `PDFDebugger`), чтобы убедиться, что запись присутствует.
* **Reuse dictionaries** — если одно и то же графическое состояние добавляется на многие страницы, храните словарь в переменной и используйте ссылку, а не создавайте его каждый раз.
* **Version compatibility** — код работает с Aspose.PDF 23.12 и новее. Более ранние версии могут требовать `CosDictionary` вместо `CosPdfDictionary`.

## Conclusion

Теперь вы знаете, как **создавать пустой словарь PDF** и **редактировать ресурсы PDF** с помощью Aspose.PDF для C#. В уроке рассмотрено открытие документа, доступ к словарю ресурсов страницы, построение пользовательского графического состояния, его регистрация и сохранение результата. Дальше вы можете экспериментировать с другими типами ресурсов, комбинировать несколько графических состояний или интегрировать эту технику в более крупный конвейер обработки PDF.

---

*Готовы исследовать дальше? Попробуйте добавить пользовательский **ExtGState** в поток содержимого или изменить словарь **Font**, чтобы внедрить новые шрифты. Оба подхода используют тот же процесс создания пустого словаря и редактирования ресурсов PDF.*

## What Should You Learn Next?

Следующие руководства охватывают близкие темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и изучить альтернативные подходы в ваших проектах.

- [Редактирование словаря ресурсов PDF с Aspose.PDF – руководство C#](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Создание пользовательского графического состояния в PDF с помощью Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Как создать пустое графическое состояние в PDF с C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}