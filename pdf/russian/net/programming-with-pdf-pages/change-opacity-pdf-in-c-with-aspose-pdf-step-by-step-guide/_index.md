---
category: general
date: 2026-08-11
description: Измените непрозрачность PDF с помощью Aspose.Pdf в C#. Узнайте, как добавить
  прозрачность к страницам PDF, установить графическое состояние и быстро сохранить
  результат.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change opacity PDF
- how to add transparency
- add pdf transparency
language: ru
lastmod: 2026-08-11
og_description: Измените непрозрачность PDF с помощью Aspose.Pdf в C#. Следуйте этому
  руководству, чтобы узнать, как добавить прозрачность в любой PDF‑документ, настроить
  графические состояния и экспортировать результат.
og_image_alt: Screenshot illustrating change opacity PDF example in C# code
og_title: Изменить непрозрачность PDF в C# – полный учебник по Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  headline: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  name: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
    text: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
  - name: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
    text: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
  - name: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
    text: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
  - name: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
    text: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Изменение непрозрачности PDF в C# с Aspose.Pdf – пошаговое руководство
url: /ru/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Изменение прозрачности PDF в C# с Aspose.Pdf – пошаговое руководство

Если вам нужно **изменять прозрачность PDF** файлов программно, этот учебник покажет вам, как это сделать. С помощью Aspose.Pdf for .NET вы можете управлять прозрачностью графических объектов, текста и изображений, не выходя из вашего кода C#.

В последующих разделах вы узнаете **как добавить прозрачность** к странице PDF, что означают базовые объекты состояния графики и как сохранить изменённый документ. Руководство также охватывает распространённые подводные камни при **добавлении прозрачности PDF** и предлагает советы для реальных сценариев.

## Что вы достигнете

К концу этого руководства вы сможете:

* Загрузить существующий PDF‑документ.
* Создать новый словарь состояния графики, определяющий значения прозрачности.
* Вставить состояние графики в словарь ресурсов страницы.
* Сохранить документ с обновлённым эффектом **изменения прозрачности PDF**.

Внешние инструменты не требуются — достаточно библиотеки Aspose.Pdf for .NET (версии 23.10 или новее) и среды разработки .NET.

## Требования

* .NET 6.0 (или .NET Framework 4.7.2+) установлен.
* Visual Studio 2022 или любой совместимый с C# IDE.
* Ссылка на пакет NuGet `Aspose.Pdf`.
* Входной PDF‑файл (`input.pdf`) находится в доступном для записи каталоге.

> **Совет:** При тестировании изменений прозрачности используйте PDF, уже содержащий векторную графику или текст; растровые изображения игнорируют параметры `ca` и `CA`, если они не находятся внутри группы прозрачности.

## Изменение прозрачности PDF с помощью Aspose.Pdf

Суть решения заключается в изменении словаря **ExtGState** (external graphics state) страницы. Этот словарь хранит параметры, такие как **ca** (прозрачность линий) и **CA** (прозрачность заливки). Добавив новую запись, вы сможете ссылаться на неё позже в потоках содержимого.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;

class ChangeOpacityPdfExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        using (var document = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 2: Access the first page and its resource dictionary
            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Step 3: Create a new graphics state dictionary with desired opacity values
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                // Fill opacity (CA) – 1.0 means fully opaque
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                // Stroke opacity (ca) – 0.5 makes lines semi‑transparent
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                // Blend mode (BM) – Normal is the default blend mode
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // Step 4: Add the new graphics state to the ExtGState dictionary
            // “GS0” is the identifier you will reference later in the content stream
            extGState.Add("GS0", newGraphicsState);

            // Optional: Demonstrate usage by drawing a semi‑transparent rectangle
            // This part shows how the new graphics state affects drawing commands.
            var canvas = new Aspose.Pdf.Drawing.Graphic(page);
            canvas.SetGraphicsState("GS0"); // Apply the opacity settings
            canvas.Rectangle(100, 500, 200, 600);
            canvas.FillColor = Color.FromRgb(255, 0, 0); // Red fill
            canvas.StrokeColor = Color.FromRgb(0, 0, 255); // Blue border
            canvas.Draw();

            // Step 5: Save the modified PDF
            document.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF saved with changed opacity.");
    }
}
```

### Почему это работает

* **ExtGState** — это ресурс PDF, который хранит переиспользуемые параметры графики. Добавив пользовательскую запись (`GS0`), вы создаёте переиспользуемую конфигурацию прозрачности.
* Ключ **ca** управляет прозрачностью операций обводки (линии, границы). Ключ **CA** управляет прозрачностью заливки (цветные фигуры, текст). Установка `ca = 0.5` делает обводку на 50 % прозрачной, тогда как `CA = 1` оставляет заливку полностью непрозрачной.
* Вызов `SetGraphicsState("GS0")` сообщает Aspose.Pdf вывести оператор `/GS0 gs` в поток содержимого, активируя новые настройки прозрачности для всех последующих команд рисования.

## Как добавить прозрачность к существующему содержимому

Если на странице уже есть текст или изображения, и вы хотите сделать их полупрозрачными без перерисовки, вы можете вставить оператор **gs** перед существующим содержимым. Ниже приведённый фрагмент демонстрирует, как добавить оператор в начало потока содержимого страницы.

```csharp
// Retrieve the existing content stream
var content = page.Contents[1];
var originalBytes = content.ToByteArray();

// Build the new content with the graphics state applied
var gsOperator = System.Text.Encoding.ASCII.GetBytes("/GS0 gs\n");
var newBytes = new List<byte>(gsOperator);
newBytes.AddRange(originalBytes);

// Replace the page content
page.Contents[1].Replace(newBytes.ToArray());
```

### Пограничные случаи и соображения

| Ситуация | Рекомендуемое решение |
|-----------|----------------------|
| **Несколько страниц** | Пройдите цикл по `document.Pages` и повторите шаги 2‑4 для каждой страницы, которую нужно изменить. |
| **Разная прозрачность для каждого элемента** | Создайте дополнительные состояния графики (`GS1`, `GS2`, …) с различными значениями `ca`/`CA` и применяйте их выборочно. |
| **PDF с существующими записями ExtGState** | Безопасно используйте `dictEditor["ExtGState"]`; если ключ отсутствует, создайте новый `CosPdfDictionary` и присвойте его `page.Resources`. |
| **Группы прозрачности** | Для сложного композитинга (например, перекрывающихся изображений) задайте словарь `/Group` с `S /Transparency` и `CS /DeviceRGB`. Это выходит за рамки базового **изменения прозрачности PDF**, но может потребоваться для сложных макетов. |

## Добавление прозрачности PDF к векторной графике

Помимо прямоугольников, вы можете применить то же состояние графики к любой векторной отрисовке — линиям, кривым или даже тексту. Ниже быстрый пример, который выводит полупрозрачный текст:

```csharp
var textFragment = new TextFragment("Transparent text")
{
    Position = new Position(100, 400),
    TextState = { FontSize = 36, ForegroundColor = Color.Black }
};
page.Paragraphs.Add(textFragment);

// Apply the graphics state to the text fragment
textFragment.TextState.GraphicsState = "GS0";
```

Свойство `GraphicsState` объекта `TextState` указывает движку PDF отрисовывать текст с использованием прозрачности, определённой в `GS0`. Это самый простой способ **добавить прозрачность PDF** к текстовому содержимому.

## Распространённые подводные камни при изменении прозрачности PDF

1. **Отсутствует словарь ExtGState** – Некоторые PDF по умолчанию не содержат запись `ExtGState`. В этом случае создайте её:
   ```csharp
   if (!dictEditor.ContainsKey("ExtGState"))
       dictEditor.Add("ExtGState", new CosPdfDictionary(document));
   ```
2. **Неправильное имя ресурса** – Имя, которое вы используете в `SetGraphicsState`, должно точно соответствовать ключу, который вы добавили (`GS0`). Ошибка в написании приводит к использованию значения по умолчанию, полностью непрозрачного.
3. **Перезапись существующих состояний графики** – Добавление новой записи не заменяет существующие. Если вы повторно используете имя, которое уже существует, вы можете непреднамеренно изменить другие элементы страницы, ссылающиеся на него.
4. **Совместимость с просмотрщиками** – Старые PDF‑просмотрщики (до версии 1.4) могут игнорировать прозрачность. Убедитесь, что ваша целевая аудитория использует современный просмотрщик, такой как Adobe Reader DC или встроенный в Chrome PDF‑просмотрщик.

## Полный рабочий пример

Ниже представлена полная, автономная программа, которую вы можете скопировать, вставить и запустить. Она включает все необходимые директивы `using`, обработку ошибок и комментарии.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Text;
using System.Drawing; // For Color

class ChangeOpacityPdfFull
{
    static void Main()
    {
        const string inputPath = "YOUR_DIRECTORY/input.pdf";
        const string outputPath = "YOUR_DIRECTORY/output.pdf";

        // Load the PDF
        using (var document = new Document(inputPath))
        {
            // Ensure the first page exists
            if (document.Pages.Count == 0)
                throw new InvalidOperationException("The PDF contains no pages.");

            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);

            // Create ExtGState dictionary if it does not exist
            if (!dictEditor.ContainsKey("ExtGState"))
                dictEditor.Add("ExtGState", new CosPdfDictionary(document));

            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Define a new graphics state with 50 % stroke opacity
            var opacityState = CosPdfDictionary.CreateEmptyDictionary(document);
            opacityState.Add("CA", new CosPdfNumber(1));   // Fill opacity = 100 %
            opacityState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity = 50 %
            opacityState.Add("BM", new CosPdfName("Normal"));

            // Add the state under the name "


## Что вам следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как добавить текстовый штамп в PDF с помощью Aspose.PDF .NET: Полное руководство](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Как добавить штампы страниц в PDF с помощью Aspose.PDF for .NET: Полное руководство](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Как добавить штампы страниц в PDF с помощью Aspose.PDF for .NET | Руководство по водяным знакам и фону](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}