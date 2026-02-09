---
category: general
date: 2026-02-09
description: Сохранить PDF как PNG в C# с использованием Aspose PDF, затем экспортировать
  PDF в HTML, добавить водяной знак‑штамп в PDF и узнать, как конвертировать PDFX‑1a
  для конвертации PDF в ASP.NET.
draft: false
keywords:
- save pdf as png
- export pdf to html
- add watermark stamp pdf
- how to convert pdfx-1a
- asp.net pdf conversion
language: ru
og_description: Сохраните PDF как PNG в C# с помощью Aspose PDF, затем экспортируйте
  PDF в HTML, добавьте водяной знак‑штамп в PDF и узнайте, как конвертировать PDFX‑1a
  для конвертации PDF в ASP.NET.
og_title: Сохранить PDF как PNG и конвертировать в PDF/X‑1a с помощью Aspose PDF
tags:
- aspnet
- pdf
- csharp
title: Сохранить PDF как PNG и преобразовать в PDF/X‑1a с помощью Aspose PDF
url: /ru/net/conversion-export/save-pdf-as-png-and-convert-to-pdf-x-1a-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сохранить PDF как PNG и конвертировать в PDF/X‑1a с помощью Aspose PDF

Когда‑то задумывались, как **сохранить PDF как PNG** без лишних нервов? Вы не одиноки — разработчики постоянно ищут быстрый способ растеризовать страницу, оставив оригинальный PDF нетронутым. В этом руководстве мы пройдём именно этот процесс, а также покажем, как **экспортировать PDF в HTML**, добавить **водяной знак PDF**, и даже **конвертировать в PDFX‑1a** для надёжного **ASP.NET PDF conversion** конвейера.

Что вы получите из этого урока — готовая к копированию программа на C#, которая загружает PDF, конвертирует его в файл, соответствующий PDF/X‑1a, рендерит первую страницу в PNG, добавляет динамический текстовый штамп и, наконец, выводит HTML‑версию с учётом кодировки шрифтов. Никаких расплывчатых ссылок, только конкретный код и объяснение «почему» каждой строки.

## Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+)
- NuGet‑пакет Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- Файл ICC‑профиля (`profile.icc`), если нужна совместимость с PDF/X‑1a
- Исходный PDF (`input.pdf`), который вы хотите преобразовать

И всё — никаких дополнительных библиотек, никаких скрытых шагов. Если у вас есть всё перечисленное, можно начинать.

## Шаг 1: Загрузка исходного PDF‑документа

Прежде чем что‑то делать, нужно загрузить PDF в память.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load the PDF you’ll be working with
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

**Почему это важно:** `Document` — основной объект; он даёт доступ к страницам, шрифтам и метаданным. Однократная загрузка ускоряет остальную часть конвейера.

## Шаг 2: Конвертация в PDF/X‑1a (Как конвертировать PDFX‑1a)

PDF/X‑1a — стандарт де‑факто для файлов, готовых к печати. Конвертация гарантирует встраивание всех шрифтов и определённость цветов.

```csharp
// Set up conversion options for PDF/X‑1a
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // What to do on errors
{
    IccProfileFileName = "YOUR_DIRECTORY/profile.icc", // External ICC profile
    OutputIntent = new OutputIntent("FOGRA39")        // Output intent for printing
};

// Perform the conversion
pdfDocument.Convert(conversionOptions);
```

**Совет:** Если не указать ICC‑профиль, Aspose встроит профиль по умолчанию, но использование точного профиля, ожидаемого вашим принтером, избавит от неприятных цветовых сдвигов.

## Шаг 3: Сохранение PDF/X‑1a‑совместимого файла

Теперь, когда документ соответствует спецификации PDF/X‑1a, сохраняем его.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");
```

Вы заметите, что размер файла может увеличиться — дополнительные ресурсы встраиваются, что именно то, что нужно для надёжного печатного вывода.

## Шаг 4: Рендер первой страницы в PNG (Save PDF as PNG)

Здесь проявляется основной запрос: мы **сохраняем PDF как PNG** для миниатюр или веб‑отображения.

```csharp
// Configure PNG device with font analysis (helps with text extraction later)
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
};

// Render only the first page
pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");
```

![Сохранить PDF как PNG пример](https://example.com/images/save-pdf-as-png.png "Пример сохранённой страницы PDF в PNG")

Флаг `AnalyzeFonts` заставляет Aspose включать информацию о шрифте в метаданные PNG, что удобно, если позже понадобится сопоставить изображение с оригинальным текстом.

## Шаг 5: Добавление водяного знака PDF

Добавить **watermark stamp PDF** проще простого с помощью `TextStamp` от Aspose. Мы сделаем штамп автоматически подгоняющимся под заданный прямоугольник.

```csharp
// Create a text stamp that auto‑adjusts its font size
TextStamp textStamp = new TextStamp("Important notice")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,
    Width = 400,               // Width of the stamp rectangle
    Height = 200,              // Height of the stamp rectangle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
};

// Place the stamp on the first page
pdfDocument.Pages[1].AddStamp(textStamp);
```

**Почему авто‑регулировка?** Разные страницы имеют разную плотность; позволив API вычислить оптимальный размер шрифта, мы гарантируем, что текст никогда не выйдет за пределы прямоугольника.

## Шаг 6: Сохранение PDF с штампом

После наложения штампа сохраняем изменения.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");
```

Откройте `stamped.pdf` в любом просмотрщике, и вы увидите блок «Important notice», аккуратно центрированный — без ручных правок.

## Шаг 7: Экспорт PDF в HTML (Export PDF to HTML)

Наконец, **export PDF to HTML**, отдавая предпочтение CMap для кодировки шрифтов. Это гарантирует, что сгенерированный HTML использует Unicode там, где это возможно, делая текст поисковым.

```csharp
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
};

// Save the HTML representation
pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);
```

Полученный `cmap.html` содержит элементы `<canvas>` для сложной графики и корректные теги `<span>` для текста, готовый к SEO‑дружественным веб‑страницам.

## Полный рабочий пример

Ниже представлена полная программа, которую можно вставить в консольное приложение. Просто замените пути‑заполнители, и всё готово.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Convert to PDF/X‑1a (how to convert pdfx‑1a)
        PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = "YOUR_DIRECTORY/profile.icc",
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDocument.Convert(conversionOptions);

        // 3️⃣ Save the PDF/X‑1a file
        pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");

        // 4️⃣ Render first page as PNG (save pdf as png)
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
        };
        pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");

        // 5️⃣ Add a dynamic watermark stamp (add watermark stamp pdf)
        TextStamp textStamp = new TextStamp("Important notice")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            Width = 400,
            Height = 200,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
        };
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 6️⃣ Save the stamped PDF
        pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");

        // 7️⃣ Export to HTML (export pdf to html)
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
        };
        pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);

        Console.WriteLine("All operations completed successfully.");
    }
}
```

**Ожидаемый результат**

- `pdfx1a.pdf` — готовый к печати файл PDF/X‑1a
- `page1.png` — растровое изображение первой страницы (идеально для миниатюр)
- `stamped.pdf` — оригинальный PDF с масштабируемым водяным знаком «Important notice»
- `cmap.html` — веб‑дружелюбная HTML‑версия с Unicode‑шрифтами

## Часто задаваемые вопросы и особые случаи

- **Что делать, если исходный PDF зашифрован?**  
  Загрузите его с паролем: `new Document("input.pdf", new LoadOptions { Password = "secret" })`.

- **Нужен ли ICC‑профиль для каждой конвертации?**  
  Не обязательно — Aspose подставит общий профиль, но для строгой совместимости с PDF/X‑1a рекомендуется использовать именно тот профиль, который требует ваша типография.

- **Можно ли рендерить более одной страницы в PNG?**  
  Конечно. Пройдитесь в цикле по `pdfDocument.Pages` и вызывайте `pngDevice.Process(page, $"page{page.Number}.png")`.

- **Является ли HTML‑вывод мобильным?**  
  Сгенерированный HTML использует адаптивные элементы `<canvas>`. Если нужен чисто CSS‑текст, установите `htmlOptions.SplitIntoPages = false` и настройте `htmlOptions.PartsEmbeddingMode`.

## Советы для ASP.NET PDF Conversion

Интегрируя этот код в контроллер ASP.NET Core, не забудьте:

1. **Передавать результат потоково**, а не записывать на диск — используйте `MemoryStream` и возвращайте `FileResult`.
2. **Освобождать** объекты `Document` и устройства с помощью `using`  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}