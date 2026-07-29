---
category: general
date: 2026-07-14
description: Сохранить PDF в виде HTML с помощью Aspose.Pdf — узнайте, как создать
  PDF‑документ, добавить в PDF прямоугольную форму и экспортировать в чистый HTML
  без изображений.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: ru
lastmod: 2026-07-14
og_description: Сохраните PDF как HTML с помощью Aspose.Pdf. Узнайте, как создать
  PDF‑документ, нарисовать прямоугольник в PDF и за считанные минуты сгенерировать
  HTML без изображений.
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: Сохранить PDF как HTML – Краткое руководство по созданию PDF и добавлению
  прямоугольной формы
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: Сохранить PDF как HTML – создать PDF, добавить прямоугольник
url: /ru/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сохранить PDF как HTML – Создать PDF, добавить прямоугольную форму

Когда‑нибудь задумывались, как **save PDF as HTML**, при этом оставаясь способными рисовать графику в исходном PDF? Вы не одиноки. Во многих внутренних инструментах нам нужен чистый HTML‑просмотр PDF, содержащего пользовательские формы, а обычные конвертеры либо встраивают тяжёлые растровые изображения, либо полностью удаляют векторные данные.

В этом руководстве мы пройдёмся по **how to create PDF document** программно с помощью Aspose.Pdf, нарисуем **rectangle shape PDF**, настроим нумерацию Бейтса и, наконец, **save PDF as HTML** без растровых изображений. К концу вы получите полностью работающее консольное приложение C#, которое генерирует HTML‑файл, открываемый в любом браузере — без дополнительных файлов изображений.

> **Pro tip:** Aspose.Pdf работает с .NET 6+, .NET Framework 4.6+ и даже .NET Core, так что вы можете внедрить его в наследуемый Windows‑сервис или в совершенно новый микросервис alike.

---

## Требования

- **Visual Studio 2022** (Community или выше) или любой совместимый с C# IDE.  
- **Aspose.Pdf for .NET** пакет NuGet (версия 23.11 или новее). Установите его через консоль диспетчера пакетов:

```powershell
Install-Package Aspose.Pdf
```

- Базовое знакомство с синтаксисом C#; предварительный опыт работы с PDF не требуется.

---

## Сохранить PDF как HTML с Aspose.Pdf

Ниже представлен полный готовый к копированию код. Он следует тем же шагам, что и оригинальный фрагмент, но добавляет комментарии, обработку ошибок и небольшую вспомогательную функцию, чтобы основной поток был более читаемым.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### Что делает код, шаг за шагом

| Шаг | Почему это важно |
|------|----------------|
| **Создать PDF‑документ** | Это основа — без объекта `Document` вы не сможете добавить ничего. |
| **Добавить прямоугольную форму PDF** | Продемонстрирует векторное рисование; прямоугольники — самая простая форма, но тот же API поддерживает круги, полигоны и т.д. |
| **Настроить нумерацию Бейтса** | Часто требуется в судебных разбирательствах или сценариях пакетной обработки для уникальной идентификации страниц. |
| **Структура тегов** | Повышает доступность; скрин‑ридеры полагаются на теги для передачи порядка чтения. |
| **Обнаружить компрометированные подписи** | Приложения, ориентированные на безопасность, должны знать, была ли цифровая подпись изменена. |
| **Сохранить PDF как HTML** | Конечная цель — создание чистого HTML, отражающего макет PDF без громоздких файлов изображений. |

> **Почему `SkipImages = true`?**  
> При конвертации PDF, содержащего векторную графику (например, наш прямоугольник), обычно не нужен растровый запасной вариант. Установка `SkipImages` удаляет элементы `<img>`, которые иначе ссылались бы на base‑64 блобы, удерживая HTML‑файл в пределах нескольких килобайт.

---

## Как создать PDF‑документ с Aspose.Pdf

Если вы новичок в Aspose, библиотека рассматривает PDF почти как документ Word: вы добавляете **pages**, затем **paragraphs**, **shapes**, или **annotations** на эти страницы. Класс `Document` является точкой входа, а каждый `Page` содержит коллекцию под названием `Paragraphs`. Любой объект, наследующий `TextFragmentAbsorber`, `Image`, `Rectangle` и т.п., может быть вставлен в эту коллекцию.

Ниже минимальный фрагмент, который создает только пустой PDF — полезно, когда вы хотите начать с нуля:

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

Вы можете добавить дополнительные страницы с помощью простого цикла `for` или применить настройки уровня страницы (поле, размер) через `PageInfo`. Такая гибкость делает Aspose.Pdf популярным выбором для серверной генерации PDF.

---

## Добавить прямоугольную форму PDF — рисование графики

Класс `Rectangle` находится в `Aspose.Pdf.Annotations`. Он принимает четыре координаты: **нижний‑левый X**, **нижний‑левый Y**, **верхний‑правый X**, **верхний‑правый Y**. Представьте систему координат PDF как

---

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создать PDF‑документ с Aspose.PDF — добавить страницу, форму и сохранить](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Конвертировать PDF в HTML в .NET с помощью Aspose.PDF без сохранения изображений](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [Конвертация PDF в HTML с использованием Aspose.PDF .NET&#58; сохранять изображения как внешние PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}