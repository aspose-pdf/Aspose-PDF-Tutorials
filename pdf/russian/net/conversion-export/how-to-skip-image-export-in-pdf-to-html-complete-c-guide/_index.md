---
category: general
date: 2026-07-20
description: Как пропустить экспорт изображений при конвертации PDF в HTML с помощью
  Aspose.PDF для .NET — узнайте, как преобразовать PDF в HTML без изображений всего
  за три шага.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to skip image export in pdf to html
- convert pdf to html without images
- aspose pdf html conversion
- disable raster images
- pdf to html conversion c#
language: ru
lastmod: 2026-07-20
og_description: Как пропустить экспорт изображений при конвертации PDF в HTML с помощью
  Aspose.PDF для .NET. Это руководство покажет, как эффективно преобразовать PDF в
  HTML без изображений.
og_image_alt: C# code screenshot converting PDF to HTML without images using Aspose.PDF
og_title: Как пропустить экспорт изображений при конвертации PDF в HTML – быстрый
  урок C#
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to skip image export in PDF to HTML using Aspose.PDF for .NET –
    learn to convert PDF to HTML without images in just three steps.
  headline: How to Skip Image Export in PDF to HTML – Complete C# Guide
  type: TechArticle
- description: How to skip image export in PDF to HTML using Aspose.PDF for .NET –
    learn to convert PDF to HTML without images in just three steps.
  name: How to Skip Image Export in PDF to HTML – Complete C# Guide
  steps:
  - name: Why `RasterImages = false` Does the Trick
    text: '- **Raster images** are the bitmap pictures embedded in the PDF (JPEG,
      PNG, etc.). When you set `RasterImages` to `false`, Aspose simply omits the
      step that extracts and writes those bitmaps to the HTML folder. - The rest of
      the PDF—fonts, vector shapes, tables, and layout information—still gets tra'
  - name: 1️⃣ Load Your PDF Document
    text: We use the `Document` class, which parses the PDF structure in memory. No
      extra configuration is needed unless you’re dealing with encrypted files.
  - name: 2️⃣ Tweak the Save Options
    text: '`HtmlSaveOptions` is a flexible container. Besides `RasterImages`, you
      could also tweak `SplitIntoPages`, `EmbedFonts`, or `CssStyleSheetType`. For
      our purpose, the single line `RasterImages = false` does all the heavy lifting.'
  - name: 3️⃣ Write Out the HTML
    text: The `Save` method writes a single HTML file (plus a folder for any auxiliary
      resources like CSS). Because we disabled raster images, the resources folder
      will be empty or contain only CSS files.
  - name: Expected Result
    text: 'Open `NoImages.html` in a browser. You should see:'
  type: HowTo
tags:
- pdf
- html
- csharp
- aspose
- conversion
title: Как пропустить экспорт изображений при конвертации PDF в HTML – полное руководство
  по C#
url: /ru/net/conversion-export/how-to-skip-image-export-in-pdf-to-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как пропустить экспорт изображений при конвертации PDF в HTML – Полное руководство на C#

Когда‑нибудь задумывались **как пропустить экспорт изображений при конвертации PDF в HTML**, если вам нужен только текстовый макет? Возможно, вы создаёте лёгкий веб‑просмотр, а тяжёлые растровые изображения лишь утяжеляют его. Хорошая новость: не нужно изобретать велосипед — Aspose.PDF for .NET предоставляет удобный переключатель для **конвертации PDF в HTML без изображений** мгновенно.

В этом руководстве мы пройдём все шаги, объясним, почему эта опция работает, и покажем готовый пример, который можно сразу запустить. К концу вы получите чистый HTML‑файл, отражающий структуру исходного PDF, но без всех растровых картинок.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6 или новее (код также работает с .NET Framework 4.7+)
- Visual Studio 2022 (или любой другой предпочитаемый редактор)
- Лицензированная копия **Aspose.PDF for .NET** (бесплатная пробная версия подходит для тестов)
- PDF‑файл, который вы хотите конвертировать — желательно с несколькими тяжёлыми изображениями, чтобы увидеть разницу

Это всё. Дополнительных пакетов NuGet, кроме Aspose.PDF, не требуется.

## Как пропустить экспорт изображений при конвертации PDF в HTML – Настройка и код

Ниже представлен полный, автономный пример программы. Вставьте его в новый консольный проект, замените пути‑заполнители и нажмите **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.HtmlSaveOptions;

namespace PdfToHtmlNoImages
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF. Adjust the path to point at your file.
            string sourcePdf = @"C:\Docs\HeavyImages.pdf";
            Document pdfDocument = new Document(sourcePdf);

            // 2️⃣ Configure HTML save options.
            //    Setting RasterImages = false tells Aspose to skip raster image export.
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                RasterImages = false // <-- This is the key line for skipping images
            };

            // 3️⃣ Save the PDF as HTML. The output will contain text and vector graphics only.
            string outputHtml = @"C:\Docs\NoImages.html";
            pdfDocument.Save(outputHtml, htmlOptions);

            Console.WriteLine("Conversion complete! HTML saved to: " + outputHtml);
        }
    }
}
```

### Почему `RasterImages = false` Работает

- **Raster images** — это битовые картинки, встроенные в PDF (JPEG, PNG и т.д.). Когда вы устанавливаете `RasterImages` в `false`, Aspose просто пропускает шаг, который извлекает и записывает эти битмапы в папку HTML.
- Остальная часть PDF — шрифты, векторные фигуры, таблицы и информация о макете — всё равно переводится в HTML/CSS, поэтому страница выглядит *почти* идентично, но легче.
- Эта опция особенно полезна для сценариев **convert pdf to html without images**, таких как SEO‑дружественные превью, фрагменты email‑рассылок или mobile‑first дизайны, где важна пропускная способность.

## Пошагово: Конвертация PDF в HTML без изображений

### 1️⃣ Загрузка PDF‑документа

Мы используем класс `Document`, который парсит структуру PDF в памяти. Дополнительная конфигурация не требуется, если только вы не работаете с зашифрованными файлами.

### 2️⃣ Настройка параметров сохранения

`HtmlSaveOptions` — гибкий контейнер. Помимо `RasterImages` вы также можете менять `SplitIntoPages`, `EmbedFonts` или `CssStyleSheetType`. Для нашей задачи единственная строка `RasterImages = false` делает всю тяжёлую работу.

### 3️⃣ Сохранение HTML

Метод `Save` записывает один HTML‑файл (плюс папку для вспомогательных ресурсов, таких как CSS). Поскольку растровые изображения отключены, папка ресурсов будет пустой или будет содержать только CSS‑файлы.

### Ожидаемый результат

Откройте `NoImages.html` в браузере. Вы должны увидеть:

- Все заголовки, абзацы и таблицы сохранены.
- Нет тегов `<img>`, ссылающихся на JPEG/PNG файлы.
- Значительно меньший размер файла — обычно **70‑90 % уменьшение** по сравнению с полной экспортой изображений.

Если сравнить страницу бок о бок с HTML‑версией, включающей изображения, макет будет практически идентичным, просто без визуального контента.

## Распространённые подводные камни и профессиональные советы

- **Отсутствуют шрифты?** Если PDF использует пользовательские шрифты, задайте `htmlOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`, чтобы текст отображался корректно.
- **Векторная графика всё ещё появляется:** Aspose конвертирует векторные рисунки в SVG. Если вам нужен действительно *только текст*, можно также установить `htmlOptions.VectorGraphics = false`.
- **Большие PDF:** Для массивных документов рассмотрите потоковую загрузку PDF (`Document.Load(stream)`), чтобы избежать загрузки всего файла в память.
- **Пути к файлам:** Используйте `Path.Combine` для кросс‑платформенной надёжности, особенно если позже планируете запуск в Linux‑контейнерах.

## Полный рабочий пример — повторение

Вот весь код программы ещё раз, на этот раз с небольшим обработчиком ошибок для надёжности:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.HtmlSaveOptions;

namespace PdfToHtmlNoImages
{
    class Program
    {
        static void Main()
        {
            try
            {
                string sourcePdf = Path.Combine(Environment.CurrentDirectory, "HeavyImages.pdf");
                string outputHtml = Path.Combine(Environment.CurrentDirectory, "NoImages.html");

                Document pdfDocument = new Document(sourcePdf);

                HtmlSaveOptions htmlOptions = new HtmlSaveOptions
                {
                    RasterImages = false,
                    // Optional: keep vector graphics if you need them
                    // VectorGraphics = false
                };

                pdfDocument.Save(outputHtml, htmlOptions);
                Console.WriteLine($"✅ Success! HTML saved to {outputHtml}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Conversion failed: {ex.Message}");
            }
        }
    }
}
```

Запустите его, откройте полученный HTML, и вы сразу увидите преимущество **пропуска экспорта изображений**.

## Что дальше? Расширяем рабочий процесс

Теперь, когда вы умеете **convert PDF to HTML without images**, вы можете:

- **Пост‑обработать HTML**, вставив lazy‑loaded заглушки там, где были удалены изображения.
- **Скомбинировать с безголовым браузером** (например, Puppeteer) для генерации PDF из полученного HTML — полезно для создания «только‑текстовой» версии оригинала.
- **Интегрировать в веб‑API**, чтобы пользователи могли загружать PDF и мгновенно получать лёгкие HTML‑превью.

Все эти сценарии опираются на один и тот же основной принцип: управлять `HtmlSaveOptions`, подстраивая вывод под свои нужды.

---

*Счастливого кодинга! Если возникнут проблемы, оставляйте комментарий ниже — разберём вместе.*

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Convert PDF to HTML in .NET Using Aspose.PDF Without Saving Images](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [PDF to HTML Conversion Using Aspose.PDF .NET&#58; Save Images as External PNGs](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)
- [Convert PDF to HTML in .NET with Custom Image Paths Using Aspose.PDF](/pdf/english/net/conversion-export/convert-pdf-html-custom-image-paths-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}