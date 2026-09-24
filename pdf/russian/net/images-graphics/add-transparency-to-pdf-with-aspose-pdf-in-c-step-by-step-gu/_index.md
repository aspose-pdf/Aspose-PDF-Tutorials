---
category: general
date: 2026-03-19
description: Добавьте прозрачность в PDF с помощью Aspose.PDF для C#. Узнайте, как
  установить прозрачность, режим смешивания и ExtGState всего в несколько строк кода.
draft: false
keywords:
- add transparency to pdf
- Aspose PDF transparency
- C# PDF graphics state
- PDF blend mode
- set PDF opacity
language: ru
og_description: Быстро добавьте прозрачность в PDF. Это руководство показывает, как
  управлять непрозрачностью и режимом наложения с помощью Aspose.PDF в C#.
og_title: Добавьте прозрачность в PDF с помощью Aspose PDF – Полный учебник по C#
tags:
- Aspose.PDF
- C#
title: Добавление прозрачности в PDF с помощью Aspose PDF в C# – пошаговое руководство
url: /ru/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление прозрачности в PDF с помощью Aspose PDF на C# – Полный учебник

Когда‑нибудь задавались вопросом **как добавить прозрачность в PDF**‑файлы, не вдаваясь в низкоуровневый синтаксис PDF? Вы не одиноки. Многие разработчики ищут быстрый способ сделать формы или текст полупрозрачными — подумайте о водяных знаках, наложенных графиках или тонких подсказках UI внутри документа.  

В этом руководстве мы пройдем через **полный, готовый к запуску пример**, который показывает, как установить непрозрачность заливки, непрозрачность обводки и режим смешивания с помощью Aspose.PDF для .NET. К концу вы получите PDF, где прямоугольник отображается с 50 % непрозрачностью, и поймёте, почему словарь ExtGState является ключом к достижению этого эффекта.

Мы охватим всё, что вам понадобится: требуемый пакет NuGet, сам код, объяснения каждой строки и несколько советов для особых случаев, таких как старые просмотрщики PDF. Никаких внешних ссылок — только автономное решение, которое можно скопировать, вставить и запустить уже сегодня.

## Что вам понадобится

- **Aspose.PDF for .NET** (v23.12 или новее). Установите через NuGet: `Install-Package Aspose.PDF`.
- Среда разработки .NET (Visual Studio, Rider или `dotnet` CLI).
- Пример PDF с именем `input.pdf`, помещённый в папку, которой вы управляете (в учебнике используется `YOUR_DIRECTORY/` как заполнитель).

И всё. Если у вас уже есть всё перечисленное, приступаем.

## Добавление прозрачности в PDF — Обзор

Суть создания прозрачного элемента в PDF — это **графическое состояние** (`ExtGState`). Добавив пользовательский объект графического состояния в словарь ресурсов страницы, можно задать:

| Свойство | Значение |
|----------|----------|
| `ca` | Непрозрачность заливки (0 = полностью прозрачно, 1 = непрозрачно). |
| `CA` | Непрозрачность обводки (та же шкала). |
| `BM` | Режим смешивания (например, `Normal`, `Multiply`). |

Мы создадим новое графическое состояние, вставим его в словарь `ExtGState` страницы, а затем будем ссылаться на него при последующем рисовании. Приведённый ниже фрагмент кода делает именно это.

![add transparency to pdf diagram](add_transparency_to_pdf.png){alt="добавить прозрачность в pdf"}

## Шаг 1: Настройка проекта и загрузка PDF

Сначала создаём простое консольное приложение (или любой проект C#) и загружаем исходный PDF.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;          // For low‑level PDF operators
using Aspose.Pdf.Text;               // Optional, if you want to add text later
using Aspose.Pdf.XObjects;          // For image handling, not needed here

// Define the folder that contains the PDF file
string inputDir = @"YOUR_DIRECTORY/";

// Load the PDF document
using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
{
    // All subsequent steps go inside this using block
```

**Почему это важно:**  
`Document` — точка входа для любой манипуляции PDF с помощью Aspose. Оборачивание его в оператор `using` гарантирует, что все ресурсы будут корректно сброшены при сохранении файла позже.

## Шаг 2: Доступ к первой странице и её ресурсам

Нужен словарь ресурсов первой страницы, потому что именно там находится коллекция `ExtGState`.

```csharp
    // Grab the first page (pages are 1‑based in Aspose)
    Page firstPage = pdfDocument.Pages[1];

    // Helper to edit dictionaries (resources, etc.)
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);

    // Retrieve the existing ExtGState dictionary, or create a new one if missing
    CosPdfDictionary extGStateDict;
    if (resourcesEditor.ContainsKey("ExtGState"))
    {
        extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
    }
    else
    {
        extGStateDict = new CosPdfDictionary(pdfDocument);
        resourcesEditor.Add("ExtGState", extGStateDict);
    }
```

**Объяснение:**  
Если у страницы уже есть запись `ExtGState`, мы её переиспользуем; иначе создаём новый словарь. Такой оборонительный подход предотвращает ошибки null‑reference при работе с PDF, в которых нет графических состояний.

## Шаг 3: Создание нового графического состояния с нужной непрозрачностью

Теперь задаём фактические значения прозрачности.

```csharp
    // Create an empty dictionary that will represent our new graphics state
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Stroke opacity – fully opaque (1.0)
    newGraphicsState.Add("CA", new CosPdfNumber(1));

    // Fill opacity – 50 % transparent (0.5)
    newGraphicsState.Add("ca", new CosPdfNumber(0.5));

    // Blend mode – Normal is the default, but you can experiment with Multiply, Screen, etc.
    newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**Зачем эти ключи?**  
- `CA` управляет непрозрачностью обводки (линий, границ).  
- `ca` управляет непрозрачностью заливки (сплошных фигур, текста).  
- `BM` выбирает, как прозрачный объект будет смешиваться с содержимым под ним. Использование `"Normal"` делает визуальный результат предсказуемым во всех просмотрщиках.

## Шаг 4: Регистрация графического состояния в ресурсах страницы

Мы даём нашему графическому состоянию имя (`GS0`) и добавляем его в словарь `ExtGState`.

```csharp
    // Add the graphics state to the ExtGState dictionary with a unique name
    extGStateDict.Add("GS0", newGraphicsState);
```

**Совет:**  
Если вам нужно несколько прозрачных объектов с разными уровнями непрозрачности, создайте дополнительные записи (`GS1`, `GS2`, …) и соответственно настройте значения `ca`/`CA`.

## Шаг 5: Рисуем прозрачный прямоугольник, используя новое графическое состояние

После того как графическое состояние готово, можно нарисовать объект, который действительно будет его использовать. Ниже мы добавляем полупрозрачный синий прямоугольник на страницу.

```csharp
    // Prepare a content stream for the page (adds to existing content)
    var canvas = new Aspose.Pdf.Drawing.Graphic(firstPage);

    // Set the graphics state we just created
    canvas.SetGraphicsState("GS0");

    // Choose a fill color (blue) and draw the rectangle
    canvas.SetColor(new Aspose.Pdf.Drawing.Color(0, 0, 255)); // RGB blue
    canvas.Rectangle(100, 500, 200, 100); // x, y, width, height

    // Close the canvas to flush commands
    canvas.Close();
```

**Что вы увидите:**  
Открыв полученный PDF, вы увидите синий прямоугольник в указанном месте, но содержимое страницы под ним останется видимым, потому что непрозрачность заливки равна 0.5. Если открыть PDF в инструменте вроде функции «Edit PDF» Adobe Acrobat, вы увидите объект `ExtGState` (`GS0`), привязанный к этому прямоугольнику.

## Шаг 6: Сохранение обновлённого PDF

Наконец, записываем изменённый документ обратно на диск.

```csharp
    // Save the document with a new name so the original stays untouched
    pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
}
```

Это весь процесс. Запустите консольное приложение, откройте `ExtGStateAdded.pdf` и убедитесь, что наложение действительно прозрачно.

---

## Полный рабочий пример (готов к копированию)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddTransparencyDemo
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF file
        string inputDir = @"YOUR_DIRECTORY/";

        // Step 2: Load the PDF document
        using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
        {
            // Step 3: Get the first page and its resource dictionary
            Page firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", extGStateDict);
            }

            // Step 4: Create a new graphics state with opacity and blend mode settings
            CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity (fully opaque)
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));       // fill opacity (50% transparent)
            newGraphicsState.Add("BM", new CosPdfName("Normal"));   // blend mode

            // Step 5: Add the new graphics state to the page resources
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 6: Draw a rectangle using the new graphics state
            var canvas = new Graphic(firstPage);
            canvas.SetGraphicsState("GS0");
            canvas.SetColor(new Color(0, 0, 255)); // blue fill
            canvas.Rectangle(100, 500, 200, 100);
            canvas.Close();

            // Step 7: Save the updated PDF document
            pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
        }

        Console.WriteLine("PDF with transparency created successfully.");
    }
}
```

**Ожидаемый результат:**  
Открытие `ExtGStateAdded.pdf` показывает синий прямоугольник в координатах (100, 500) с 50 % непрозрачностью заливки. Под прямоугольником остаются видимыми любые существующие тексты или изображения.

---

## Часто задаваемые вопросы и особые случаи

### Работает ли это со старыми просмотрщиками PDF?
Большинство современных просмотрщиков (Adobe Reader, Foxit, Chrome) поддерживают базовые ключи `ca`/`CA`. Очень старые программы могут их игнорировать и отрисовывать форму полностью непрозрачной.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}