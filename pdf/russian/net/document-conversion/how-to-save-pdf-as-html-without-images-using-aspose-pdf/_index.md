---
category: general
date: 2026-10-10
description: Узнайте, как сохранить PDF в формате HTML с помощью Aspose.PDF, пропуская
  растровые изображения. Это руководство охватывает преобразование PDF в HTML и эффективное
  сохранение документа в формате HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- convert pdf to html
- aspose pdf to html
- save pdf without images
- save document as html
language: ru
lastmod: 2026-10-10
og_description: Сохраните PDF в формате HTML с помощью Aspose.PDF, пропуская растровые
  изображения. Следуйте этому полному руководству, чтобы преобразовать PDF в HTML
  и сохранить документ в формате HTML.
og_image_alt: Screenshot showing PDF saved as HTML without images using Aspose.PDF
og_title: Сохранить PDF в HTML без изображений — пошаговое руководство Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save PDF as HTML with Aspose.PDF, skipping raster images.
    This guide covers convert PDF to HTML and save document as HTML efficiently.
  headline: How to save PDF as HTML without images using Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- HTML conversion
title: Как сохранить PDF в HTML без изображений с помощью Aspose.PDF
url: /ru/net/document-conversion/how-to-save-pdf-as-html-without-images-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить PDF в HTML без изображений с помощью Aspose.PDF

Если вам нужно **сохранить PDF в HTML**, при этом исключив все растровые графики, этот учебник покажет вам, как это сделать. Настраивая `HtmlSaveOptions`, вы можете эффективно преобразовать PDF в HTML и сохранить вывод лёгким — идеально для веб‑дружественной документации или SEO‑оптимизированных страниц.  

Помимо удаления изображений, руководство также демонстрирует более общий процесс **convert PDF to HTML**, так что вы получите чистый HTML‑файл, сохраняющий текст, векторную графику и макет. Внешние инструменты не требуются; всё работает внутри стандартного проекта .NET.

## Требования

* .NET 6.0 или новее (код также работает с .NET Framework 4.6+)
* Действительная лицензия Aspose.PDF for .NET (или бесплатный оценочный ключ)
* Входной PDF‑файл, расположенный в известной директории
* Visual Studio 2022 (или любой C# IDE)

Эти элементы достаточны для компиляции и выполнения примера кода, показанного ниже.

## Шаг 1: Установите пакет Aspose.PDF NuGet

Первое, что нужно сделать, — добавить библиотеку Aspose.PDF в ваш проект:

```bash
dotnet add package Aspose.PDF
```

Выполнение этой команды восстановит последнюю стабильную версию Aspose.PDF, которая включает класс `HtmlSaveOptions`, необходимый для преобразования.

## Шаг 2: Загрузите исходный PDF‑документ

Загрузка PDF проста с помощью класса `Document`. Этот класс представляет весь PDF‑файл в памяти.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Saving;

// Step 2: Load the source PDF document
Document doc = new Document(@"C:\MyFiles\input.pdf");
```

*Почему этот шаг важен:*  
`Document` разбирает структуру PDF, предоставляя доступ к страницам, шрифтам и ресурсам. Без предварительной загрузки файла вы не сможете применить параметры сохранения.

## Шаг 3: Настройте параметры сохранения HTML, чтобы пропустить растровые изображения

Объект `HtmlSaveOptions` позволяет точно настроить вывод HTML. Установка `SkipRasterImages` в `true` сообщает Aspose.PDF игнорировать все растровые изображения (JPEG, PNG, GIF) во время преобразования.

```csharp
// Step 3: Configure HTML save options to skip raster images
HtmlSaveOptions htmlOpts = new HtmlSaveOptions
{
    // Exclude all raster (bitmap) images from the output HTML
    SkipRasterImages = true,

    // Optional: embed fonts as Base64 to avoid external font files
    EmbedFonts = true,

    // Optional: preserve the original layout as closely as possible
    FixedLayout = true
};
```

*Почему этот шаг важен:*  
Растровые изображения часто занимают большую часть размера файла. Пропуская их, вы получаете более лёгкий HTML‑файл, который загружается быстрее и легче индексируется поисковыми системами. Дополнительные параметры (`EmbedFonts`, `FixedLayout`) показаны для полноты; они не требуются для удаления изображений.

## Шаг 4: Сохраните документ в HTML без изображений

Теперь вы можете записать преобразованное содержимое на диск. Перегрузка `Save` принимает путь назначения, желаемый `SaveFormat` и ранее настроенные параметры.

```csharp
// Step 4: Save the document as HTML without raster images
doc.Save(@"C:\MyFiles\no_images.html", SaveFormat.Html, htmlOpts);
```

После завершения вызова файл `no_images.html` будет содержать текстовое содержимое, векторные формы и CSS, восстанавливающие оригинальный макет PDF — без каких-либо растровых изображений.

### Ожидаемый результат

Откройте `no_images.html` в браузере. Вы должны увидеть:

* Все заголовки, абзацы и таблицы из оригинального PDF.
* Векторную графику (например, SVG‑формы), отображённую корректно.
* Отсутствие тегов `<img>`, ссылающихся на растровые файлы; эти теги полностью опущены.

Если вы просмотрите исходный код HTML, вы заметите отсутствие элементов `<img src="...">`, что подтверждает, что `SkipRasterImages` сработал как задумано.

## Полный, исполняемый пример

Ниже представлено автономное консольное приложение, объединяющее все шаги. Скопируйте код в новый консольный проект .NET и запустите его.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Saving;

namespace PdfToHtmlNoImages
{
    class Program
    {
        static void Main(string[] args)
        {
            // Input and output paths – adjust to your environment
            string inputPath = @"C:\MyFiles\input.pdf";
            string outputPath = @"C:\MyFiles\no_images.html";

            // 1. Load the PDF document
            Document doc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF: {inputPath}");

            // 2. Set up HTML save options to omit raster images
            HtmlSaveOptions htmlOpts = new HtmlSaveOptions
            {
                SkipRasterImages = true,
                EmbedFonts = true,
                FixedLayout = true
            };
            Console.WriteLine("Configured HtmlSaveOptions to skip raster images.");

            // 3. Save as HTML
            doc.Save(outputPath, SaveFormat.Html, htmlOpts);
            Console.WriteLine($"PDF saved as HTML without images at: {outputPath}");
        }
    }
}
```

**Запуск программы** выводит сообщения о прогрессе в консоль и создаёт `no_images.html`. Проверьте файл, открыв его в любом современном браузере.

## Распространённые варианты и особые случаи

| Ситуация | Как адаптировать код |
|-----------|-----------------------|
| **Сохранить растровые изображения** | Установите `SkipRasterImages = false` (или опустите свойство). |
| **Преобразовать только диапазон страниц** | Используйте `doc.Pages.Delete(pageNumber)`, чтобы удалить ненужные страницы перед сохранением, или задайте `htmlOpts.PageIndex` и `htmlOpts.PageCount`. |
| **Сохранить каждую страницу PDF в отдельный HTML‑файл** | Установите `htmlOpts.SplitIntoPages = true`; библиотека сгенерирует `output_page1.html`, `output_page2.html` и т.д. |
| **Сжать полученный HTML** | После сохранения запустите минификатор файла или установите `htmlOpts.Compress = true` (доступно в более новых версиях Aspose). |
| **Обрабатывать PDF, защищённые паролем** | Передайте пароль конструктору `Document`: `new Document(inputPath, new LoadOptions { Password = \"secret\" })`. |

## Профессиональные советы

* **Лицензировать заранее** – Зарегистрируйте вашу лицензию Aspose.PDF перед загрузкой документа, чтобы избежать водяных знаков оценки.  
* **Производительность** – Для больших PDF‑файлов переиспользуйте один экземпляр `HtmlSaveOptions` и рассмотрите возможность включения `htmlOpts.UseZOrder = true` для ускорения отрисовки перекрывающихся элементов.  
* **Тестирование** – Сравните размер HTML‑файла с изображениями и без них, чтобы оценить выгоду от использования `SkipRasterImages`.  

## Заключение

Теперь вы знаете, как **сохранить PDF в HTML**, удаляя растровую графику с помощью Aspose.PDF для .NET. Полный процесс — загрузка PDF, настройка `HtmlSaveOptions` с `SkipRasterImages` и сохранение результата — охватывает основной сценарий **convert PDF to HTML** и может быть расширен для конвертации диапазона страниц, вывода по отдельным страницам или дополнительных оптимизаций.  

Далее вы можете изучить **save document as HTML** с встроенным CSS или поэкспериментировать с классом `SvgSaveOptions` для генерации масштабируемой векторной графики вместо HTML. Оба подхода дополнительно уменьшают размер файлов и повышают отзывчивость современных веб‑приложений. Счастливого кодинга!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, опирающиеся на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Конвертировать PDF в HTML в .NET с помощью Aspose.PDF без сохранения изображений](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [Конвертация PDF в HTML с использованием Aspose.PDF .NET: Сохранить изображения как внешние PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)
- [Сохранить PDF в HTML с Aspose.PDF — Быстрое руководство C#](/pdf/english/net/conversion-export/save-pdf-as-html-with-aspose-pdf-quick-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}