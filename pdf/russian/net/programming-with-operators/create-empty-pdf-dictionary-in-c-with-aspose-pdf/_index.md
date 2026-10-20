---
category: general
date: 2026-08-14
description: Создайте пустой словарь PDF в C# с помощью Aspose.Pdf — узнайте, как
  добавить графическое состояние в коллекцию ExtGState и программно изменять PDF‑файлы.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: ru
lastmod: 2026-08-14
og_description: Создайте пустой словарь PDF в C# с помощью Aspose.Pdf. Следуйте этому
  полному руководству, чтобы добавить пользовательское графическое состояние в коллекцию
  ExtGState PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Создание пустого словаря PDF в C# – пошаговое руководство Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Создать пустой PDF‑словарь в C# с Aspose.Pdf
url: /ru/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание пустого PDF‑словаря в C# с Aspose.Pdf

Если вам нужно **create empty PDF dictionary** объекты при работе с PDF‑файлами, это руководство покажет, как сделать это в C# с использованием библиотеки Aspose.Pdf. Независимо от того, создаёте ли вы пользовательское графическое состояние, добавляете новый ресурс или готовите шаблон для последующего использования, приведённые ниже шаги предоставят полное, готовое к выполнению решение.

Вы узнаете, как загрузить PDF, получить доступ к словарю ресурсов первой страницы, создать совершенно новый `CosPdfDictionary` и вставить его в коллекцию `ExtGState`. К концу руководства у вас будет рабочий `output.pdf`, содержащий только что созданный словарь.

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+)
- Visual Studio 2022 или любой предпочитаемый вами C# IDE
- Лицензия Aspose.Pdf for .NET (или временный ключ оценки)
- Пример PDF с именем **input.pdf**, размещённый в папке, которой вы управляете (путь к папке будет использоваться как `dataDir`)

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Pdf`.

## Шаг 1: Настройте проект и подключите Aspose.Pdf

1. Создайте новый проект **Console App** в Visual Studio.  
2. Откройте **NuGet Package Manager** и установите `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Добавьте следующие директивы `using` в начало `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Почему эти пространства имён?* `Aspose.Pdf` содержит основной класс `Document`, а `Aspose.Pdf.Operators.Gfx` предоставляет `CosPdfDictionary`, `CosPdfNumber` и связанные низкоуровневые PDF‑объекты, необходимые для **create empty PDF dictionary** структур.

## Шаг 2: Загрузите исходный PDF

Первая операция — загрузить существующий PDF‑файл в экземпляр `Document`. Это даёт доступ ко всем страницам, ресурсам и низкоуровневым словарям.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Объяснение*: `Document` читает файл в память и подготавливает внутренние структуры. Оператор `using` гарантирует освобождение дескриптора файла после завершения обработки.

## Шаг 3: Доступ к словарю ресурсов первой страницы

Каждая страница PDF имеет словарь **Resources**, который группирует шрифты, изображения, объекты ExtGState и другие общие ресурсы. Чтобы вставить новое графическое состояние, нам нужно отредактировать этот словарь.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` — вспомогательный класс, позволяющий работать со словарём PDF как с C# `Dictionary<string, object>`.

## Шаг 4: Получить (или создать) коллекцию ExtGState

`ExtGState` хранит объекты графического состояния, такие как непрозрачность, режим наложения и ширина линии. Если исходный PDF уже содержит запись `ExtGState`, мы переиспользуем её; иначе создаём новый пустой словарь.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Зачем эта проверка?* Некоторые PDF‑файлы полностью опускают запись `ExtGState`. Обрабатывая оба случая, руководство остаётся надёжным для любого входного файла.

## Шаг 5: **Create empty PDF dictionary** для нового графического состояния

Теперь мы действительно **create empty PDF dictionary** объекты, определяющие параметры графического состояния. Словарь начинается пустым, и мы добавляем необходимые ключи:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Что делает каждая запись

| Ключ | Тип | Значение |
|-----|------|---------|
| **CA** | `CosPdfNumber` | Непрозрачность обводки (диапазон 0‑1). |
| **ca** | `CosPdfNumber` | Непрозрачность заливки (диапазон 0‑1). |
| **BM** | `CosPdfName`   | Режим наложения; `"Normal"` — наиболее распространённый. |

Поскольку мы начали с **empty PDF dictionary**, у нас есть полный контроль над тем, какие записи добавляются. При необходимости вы можете расширить этот словарь дополнительными параметрами графического состояния, такими как `LW` (ширина линии) или `LC` (закругление конца линии).

## Шаг 6: Вставьте новое графическое состояние в ExtGState

Словарь `ExtGState` работает как карта, где каждая запись идентифицируется именем (например, `GS0`, `GS1`). Мы добавляем наш только что построенный словарь под уникальным ключом.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Если планируется добавить несколько состояний, увеличьте суффикс (`GS1`, `GS2`, …), чтобы избежать конфликтов имён.

## Шаг 7: Сохраните изменённый PDF

Наконец, запишите изменения обратно на диск. Метод `Save` автоматически сериализует обновлённые словари.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Откройте `output.pdf` в любом PDF‑просмотрщике и проверьте запись **Resources → ExtGState** (большинство просмотрщиков скрывают её, но такие инструменты, как Adobe Acrobat Preflight или PDF‑Tron, могут её показать). Вы должны увидеть запись `GS0`, содержащую значения непрозрачности и режима наложения, которые вы задали.

## Полный рабочий пример

Объединив все части, представляем полный код программы, который можно скопировать‑вставить в `Program.cs` и запустить:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Ожидаемый вывод** — консоль выводит строку подтверждения, а `output.pdf` содержит новую запись `GS0` в `ExtGState`. При отрисовке страницы, ссылающейся на `GS0` (например, через оператор потока содержимого `gs`), линии будут полностью непрозрачными, а заливки — 50 % прозрачными.

## Часто задаваемые вопросы и обработка граничных случаев

| Вопрос | Ответ |
|----------|--------|
| *Что если PDF содержит несколько страниц?* | Пример ориентирован на первую страницу (`Pages[1]`). Чтобы затронуть все страницы, пройдитесь в цикле по `pdfDocument.Pages` и повторите шаги 3‑5 для ресурсов каждой страницы. |
| *Могу ли я добавить словарь на страницу, где уже существует запись ExtGState с именем “GS0”?* | Да, но необходимо использовать другой ключ (`GS1`, `GS2`, …), чтобы не перезаписать существующую запись. |
| *Безопасно ли изменять словарь после сохранения?* | После вызова `Save` представление в памяти отделяется от файла. Вы можете продолжать редактировать объект `Document` и снова вызвать `Save`, если это необходимо. |
| *Нужна ли лицензия для Aspose.Pdf, чтобы использовать ` |

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогающие освоить дополнительные возможности API и изучить альтернативные подходы к реализации в ваших проектах.

- [Как создать пунктирные линии в PDF с помощью Aspose.PDF for .NET: пошаговое руководство](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Как удалить графику из PDF с помощью Aspose.PDF .NET: полное руководство](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Как создать многослойные PDF с помощью Aspose.PDF for .NET: всестороннее руководство](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}