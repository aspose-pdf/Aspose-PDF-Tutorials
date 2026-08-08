---
category: general
date: 2026-03-29
description: Конвертировать PDF в PDF/X‑1a и экспортировать страницу PDF в PNG в одном
  потоке — также узнать, как добавить текстовый штамп в PDF с помощью Aspose.Pdf (C#).
draft: false
keywords:
- convert pdf to pdf/x-1a
- export pdf page png
- add text stamp pdf
- Aspose.Pdf conversion
- PDF/X‑1a workflow
language: ru
og_description: Конвертировать PDF в PDF/X‑1a и экспортировать страницу PDF в PNG,
  добавляя текстовый штамп PDF — полное руководство по C# с Aspose.Pdf.
og_title: конвертировать pdf в pdf/x-1a, экспортировать страницу в png и добавить
  текстовый штамп
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Конвертировать PDF в PDF/X-1a, экспортировать страницу в PNG и добавить текстовый
  штамп
url: /ru/net/conversion-export/convert-pdf-to-pdf-x-1a-export-page-png-add-text-stamp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# конвертировать pdf в pdf/x-1a, экспортировать страницу png и добавить текстовый штамп – Полное руководство C#

Когда‑то вам **нужно было конвертировать pdf в pdf/x-1a**, но при этом захотелось быстро получить PNG‑превью первой страницы и добавить пользовательский текстовый штамп в тот же документ? Вы не одиноки. Во многих производственных конвейерах — например, при подготовке к печати или автоматической генерации отчётов — часто встречается именно такая комбинация требований.

В этом уроке мы пройдём сквозной рабочий процесс, который последовательно делает три вещи: **конвертировать pdf в pdf/x-1a**, **экспортировать страницу pdf в png** и **добавить текстовый штамп в pdf**. Код использует библиотеку Aspose.Pdf для .NET, поэтому вы получаете профессиональное решение без необходимости вникать в низкоуровневую структуру PDF. К концу вы получите готовую программу на C#, которую можно вставить в любой консольный проект, Azure Function или шаг CI.

> **Что вы получите** — полный исходный файл, пошаговые объяснения, советы по типичным подводным камням и быстрый способ проверить результат.

## Требования

- .NET 6.0 или новее (API также работает с .NET Framework 4.x).  
- NuGet‑пакет Aspose.Pdf for .NET (`Aspose.Pdf`) — версия 23.10 актуальна на момент написания.  
- Входной PDF (`input.pdf`) и файл ICC‑профиля (`Coated_Fogra39L_VIGC_300.icc`), размещённые в папке, которой вы управляете.  
- Базовые знания C# и Visual Studio (или любой другой IDE).

Если что‑то из перечисленного вам незнакомо, просто установите NuGet‑пакет командой:

```bash
dotnet add package Aspose.Pdf --version 23.10.0
```

А теперь приступим.

## Шаг 1: Загрузка исходного PDF‑документа

Первым делом открываем PDF, с которым будем работать. Класс `Document` из Aspose.Pdf представляет весь файл и загружает содержимое «лениво», поэтому вы не платите за производительность, пока не начнёте обращаться к страницам.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;
using Aspose.Pdf.Conversion;

// Adjust these paths to match your environment
string baseDir = @"C:\MyProjects\PdfDemo\";
string inputPath = Path.Combine(baseDir, "input.pdf");

// Load the PDF – this is where any file‑not‑found errors will surface
Document pdfDoc = new Document(inputPath);
```

*Почему это важно*: ранняя загрузка документа даёт один объект, который можно передавать дальше для конвертации, рендеринга и штамповки. Если пропустить явную загрузку и попытаться работать с несуществующим файлом, позже вы получите непонятное `FileNotFoundException`.

## Шаг 2: Конвертация документа в PDF/X‑1a с пользовательским ICC‑профилем

PDF/X‑1a — де‑факто стандарт для готовых к печати PDF‑файлов. На этапе конвертации также можно внедрить **Output Intent** (ICC‑профиль), чтобы последующие RIP‑системы точно знали, как интерпретировать цвета.

```csharp
// Prepare conversion options – we ask Aspose to delete any objects that would break PDF/X‑1a compliance
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // Drop non‑compliant objects automatically
{
    IccProfileFileName = Path.Combine(baseDir, "Coated_Fogra39L_VIGC_300.icc"),
    OutputIntent = new OutputIntent("FOGRA39") // Human‑readable name for the intent
};

// Perform the conversion in‑place
pdfDoc.Convert(conversionOptions);
```

*Совет профи*: если нужен более строгий контроль ошибок, замените `ConvertErrorAction.Delete` на `ConvertErrorAction.Throw`. Тогда конвертация прервётся при первой проблеме совместимости, что удобно для автоматических QA‑конвейеров.

## Шаг 3: Экспорт первой страницы в PNG с анализом шрифтов

PNG‑превью часто требуется для быстрой визуальной проверки или создания миниатюр. Включив `AnalyzeFonts`, Aspose гарантирует корректную растеризацию встроенных шрифтов, избегая неожиданного отсутствия глифов.

```csharp
// Configure the PNG device – you can tweak resolution, color depth, etc.
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions
    {
        AnalyzeFonts = true,          // Guarantees faithful text rendering
        Resolution = 300              // 300 DPI is a good trade‑off for quality vs. size
    }
};

// Export the first page (index is 1‑based)
string pngPath = Path.Combine(baseDir, "page1.png");
pngDevice.Process(pdfDoc.Pages[1], pngPath);
```

После выполнения вы найдёте `page1.png` рядом с исходными файлами. Откройте его в любом просмотрщике изображений, чтобы убедиться, что конверсия прошла правильно.

## Шаг 4: Добавление текстового штампа с автоматической подгонкой размера шрифта

**Текстовый штамп** — удобный способ добавить водяной знак или аннотацию в PDF без изменения основных потоков содержимого. Установка `AutoAdjustFontSizeToFitStampRectangle` заставит библиотеку уменьшать или увеличивать текст так, чтобы он никогда не выходил за пределы заданного прямоугольника.

```csharp
// Create a stamp with the desired text
TextStamp autoSizeStamp = new TextStamp("Auto‑size")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    Width = 400,        // Width of the stamp rectangle (points)
    Height = 200,       // Height of the stamp rectangle (points)
    // Optional: position the stamp – here we center it on the page
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Center,
    // Optional: give it a semi‑transparent background for readability
    Background = new BackgroundInfo(Color.FromRgb(255, 255, 0), 0.3f)
};

// Attach the stamp to the first page (you could loop over all pages if needed)
pdfDoc.Pages[1].AddStamp(autoSizeStamp);
```

*Зачем авто‑размер?* Если позже вы измените текст штампа на более длинный (например, динамический тайм‑стамп), вам не придётся вручную пересчитывать размеры шрифта — штамп адаптируется «на лету».

## Шаг 5: Сохранение обновлённого PDF‑документа

Наконец, записываем всё обратно на диск. Можно перезаписать оригинальный файл или создать новый; в примере ниже создаётся `output.pdf`.

```csharp
string outputPath = Path.Combine(baseDir, "output.pdf");
pdfDoc.Save(outputPath);
```

После завершения сохранения у вас будет:

1. Файл, соответствующий **PDF/X‑1a** (`output.pdf`).  
2. **PNG‑превью** первой страницы (`page1.png`).  
3. **Текстовый штамп**, идеально вписанный в свой прямоугольник.

### Быстрый чек‑лист проверки

| ✅ Проверка | Как проверить |
|------------|----------------|
| Соответствие PDF/X‑1a | Откройте `output.pdf` в Adobe Acrobat → *Print Production* → *Preflight* и выберите “PDF/X‑1a:2001”. |
| PNG выглядит правильно | Откройте `page1.png` в Windows Photo Viewer или любом графическом редакторе. |
| Штамп отображается | Прокрутите `output.pdf` — текст “Auto‑size” должен быть по центру страницы 1. |

![convert pdf to pdf/x-1a preview](image.png "convert pdf to pdf/x-1a preview showing stamped page")

*Текст альтернативы изображения*: **convert pdf to pdf/x-1a preview with auto‑size text stamp** – демонстрирует окончательный PDF после всех шагов.

## Распространённые варианты и граничные случаи

- **Несколько страниц** — если нужно штамповать каждую страницу, пройдитесь в цикле по `pdfDoc.Pages` и вызывайте `AddStamp` внутри цикла.  
- **Другой формат вывода** — замените `PdfFormat.PDF_X_1A` на `PdfFormat.PDF_A_1B` для архивных PDF.  
- **PNG более высокого разрешения** — установите `Resolution = 600` в `RenderingOptions` для миниатюр печатного качества.  
- **Свой шрифт для штампа** — присвойте `autoSizeStamp.Font = FontRepository.FindFont("Arial")` перед добавлением штампа.  
- **Обработка ошибок** — оберните каждый крупный шаг в `try/catch` и логируйте `ConversionException` или `FileNotFoundException` для упрощения отладки.

## Полный рабочий пример (готовый к копированию)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;
using Aspose.Pdf.Conversion;
using Aspose.Pdf.Color; // For BackgroundInfo color

class PdfX1aWorkflow
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Setup paths
        // -----------------------------------------------------------------
        string baseDir = @"C:\MyProjects\PdfDemo\";
        string inputPdf = Path.Combine(baseDir, "input.pdf");
        string iccProfile = Path.Combine(baseDir, "Coated_Fogra39L_VIGC_300.icc");
        string pngOutput = Path.Combine(baseDir, "page1.png");
        string finalPdf = Path.Combine(baseDir, "output.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Load the source document
        // -----------------------------------------------------------------
        Document pdfDoc = new Document(inputPdf);

        // -----------------------------------------------------------------
        // 3️⃣ Convert to PDF/X‑1a (print‑ready)
        // -----------------------------------------------------------------
        PdfFormatConversionOptions convOpts = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = iccProfile,
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDoc.Convert(convOpts);

        // -----------------------------------------------------------------
        // 4️⃣ Export first page as PNG (export pdf page png)
        // -----------------------------------------------------------------
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions
            {
                AnalyzeFonts = true,
                Resolution = 300
            }
        };
        pngDevice.Process(pdfDoc.Pages[1], pngOutput);

        // -----------------------------------------------------------------
        // 5️⃣ Add auto‑sizing text stamp (add text stamp pdf)
        // -----------------------------------------------------------------
        TextStamp stamp = new TextStamp("Auto‑size")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Width = 400,
            Height = 200,
            HorizontalAlignment = HorizontalAlignment.Center,
            VerticalAlignment = VerticalAlignment.Center,
            Background = new BackgroundInfo(Color.From

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}