---
category: general
date: 2026-07-03
description: Узнайте, как добавить водяной знак в PDF с помощью Aspose.PDF и добавить
  пользовательское текстовое наложение в PDF всего за несколько строк кода на C#.
draft: false
keywords:
- how to add watermark pdf
- add text overlay pdf
- how to use aspose pdf
- add custom text pdf
language: ru
og_description: Как добавить водяной знак в PDF с помощью Aspose.PDF на C#. Пошаговое
  руководство, показывающее, как добавить пользовательский текстовый водяной знак
  в PDF.
og_title: Как добавить водяной знак в PDF – Краткое руководство Aspose
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to add watermark PDF using Aspose.PDF and add custom text
    PDF overlay in just a few lines of C# code.
  headline: How to Add Watermark PDF – Add Text Overlay PDF with Aspose
  type: TechArticle
- description: Learn how to add watermark PDF using Aspose.PDF and add custom text
    PDF overlay in just a few lines of C# code.
  name: How to Add Watermark PDF – Add Text Overlay PDF with Aspose
  steps:
  - name: 4‑a. Add to the First Page Only (quick demo)
    text: '```csharp // Add the stamp to the first page pdfDocument.Pages[1].AddStamp(textStamp);
      ```'
  - name: 4‑b. Add to Every Page (real‑world watermark)
    text: '```csharp // Uncomment the following block to watermark every page /* foreach
      (Page page in pdfDocument.Pages) { page.AddStamp(textStamp); } */ ```'
  - name: Expected Output
    text: Open `stamp.pdf` in any PDF viewer. You should see the semi‑transparent
      text **“Auto‑fit”** slanted at a 45° angle, centered within a 400 × 200‑point
      rectangle. The rest of the page content remains untouched.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Как добавить водяной знак в PDF – добавить текстовое наложение в PDF с Aspose
url: /ru/net/programming-with-stamps-and-watermarks/how-to-add-watermark-pdf-add-text-overlay-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить водяной знак в PDF – наложить текстовый оверлей в PDF с помощью Aspose

Когда‑то задумывались **как добавить водяной знак в PDF** без поиска тяжёлого редактора? Вы не одиноки. Во многих проектах — например, при автоматической генерации отчётов или пакетной обработке счетов — тонкий водяной знак или пользовательский текстовый оверлей могут стать разницей между профессиональным результатом и беспорядочным набором страниц.

Хорошая новость? С **Aspose.PDF for .NET** вы можете добавить водяной знак в любой PDF за несколько строк кода. В этом руководстве мы пройдёмся по точному коду, объясним, почему важна каждая настройка, и даже покажем, как **добавить текстовый оверлей PDF** и **добавить пользовательский текст PDF** для тонкой бренд‑идентичности.

---

## Что вы создадите

К концу этого руководства у вас будет небольшое консольное приложение, которое:

1. Загружает существующий PDF (`input.pdf`).
2. Создаёт текстовый штамп, автоматически подгоняющий размер под текст водяного знака.
3. Размещает штамп на первой странице (или на всех страницах, если захотите).
4. Сохраняет результат как `stamp.pdf`.

Никаких внешних инструментов, никаких ручных кликов в UI — только чистый C#‑код, который можно вставить в любой проект .NET 6+.

---

## Предварительные требования

- **Aspose.PDF for .NET** (NuGet‑пакет `Aspose.Pdf`). Бесплатная trial‑версия отлично подходит для тестов.
- .NET 6 SDK или более новая версия.
- Пример PDF (`input.pdf`) в папке, к которой у вас есть доступ.
- Базовые знания C# и Visual Studio (или вашей любимой IDE).

> **Pro tip:** Если вы целитесь в .NET Framework вместо .NET Core, тот же код будет работать; просто скорректируйте файл проекта.

---

## Шаг 1: Создайте проект и установите Aspose.PDF

Сначала создайте консольный проект:

```bash
dotnet new console -n PdfWatermarkDemo
cd PdfWatermarkDemo
dotnet add package Aspose.Pdf
```

> **Почему это важно:** Добавление NuGet‑пакета подтягивает всю низкоуровневую логику парсинга PDF, так что вам не придётся изобретать велосипед.

---

## Шаг 2: Загрузите исходный PDF‑документ

Открыть PDF так же просто, как вызвать конструктор `Document`. Оберните его в блок `using`, чтобы файловый дескриптор освобождался автоматически.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Step 2: Load the source PDF document
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // The rest of the steps go here...
        }
    }
}
```

> **Что происходит?** Класс `Document` парсит файл и создаёт в памяти представление страниц, шрифтов и ресурсов. Это фундамент для любой дальнейшей манипуляции.

---

## Шаг 3: Создайте текстовый штамп с включённым авто‑подбором размера

*Штамп* в Aspose — это переиспользуемый объект, который может содержать текст, изображения или даже страницы PDF. Для водяного знака мы используем `TextStamp` с `AutoAdjustFontSizeToFitStampRectangle = true`. Это гарантирует, что текст масштабируется под заданный прямоугольник.

```csharp
// Step 3: Create a text stamp (watermark) with auto‑fit enabled
var textStamp = new TextStamp("Auto‑fit")
{
    // Auto‑adjust the font size so the text always fits the rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Define the rectangle size (in points; 1 point = 1/72 inch)
    Width = 400,
    Height = 200,
    // Optional: rotate the watermark for a classic diagonal look
    Rotate = RotationAngle.FromDegrees(45),
    // Optional: set opacity (0 = fully transparent, 1 = opaque)
    Opacity = 0.3,
    // Optional: choose a font and color that matches your brand
    TextState = new TextState
    {
        FontSize = 72,               // initial size; will be auto‑adjusted
        Font = FontRepository.FindFont("Arial"),
        FontStyle = FontStyles.Bold,
        ForegroundColor = Color.FromRgb(200, 200, 200) // light gray
    }
};
```

> **Зачем авто‑подгонка?** Если позже изменить текст водяного знака (например, с «Draft» на «Confidential»), тот же прямоугольник подстроится под новую длину без ручного изменения размеров. Это и есть преимущество **add custom text pdf**.

---

## Шаг 4: Позиционируйте штамп на нужных страницах

Штамп можно добавить на одну страницу или пройтись по всем страницам в цикле. Здесь показаны оба подхода.

### 4‑a. Добавить только на первую страницу (быстрая демонстрация)

```csharp
// Add the stamp to the first page
pdfDocument.Pages[1].AddStamp(textStamp);
```

### 4‑b. Добавить на каждую страницу (реальный водяной знак)

```csharp
// Uncomment the following block to watermark every page
/*
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(textStamp);
}
*/
```

> **Замечание по дизайну:** Добавление на каждую страницу — типичный сценарий **add text overlay pdf** для корпоративного брендинга. Цикл лёгок — Aspose берёт на себя всю тяжёлую работу.

---

## Шаг 5: Сохраните изменённый PDF

Наконец, запишите изменения. Можно перезаписать исходный файл или сохранить в новое место.

```csharp
// Step 5: Save the modified PDF with the stamp applied
pdfDocument.Save("YOUR_DIRECTORY/stamp.pdf");
Console.WriteLine("Watermark applied successfully! Check YOUR_DIRECTORY/stamp.pdf");
```

Запуск программы сейчас создаст `stamp.pdf`, где слово «Auto‑fit» будет расположено по диагонали на первой странице (или на всех, если включён цикл).

---

## Полный рабочий пример

Собрав всё вместе, получаем полностью готовый к запуску код:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Create a text stamp with auto‑fit enabled
            var textStamp = new TextStamp("Auto‑fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                Width = 400,
                Height = 200,
                Rotate = RotationAngle.FromDegrees(45),
                Opacity = 0.3,
                TextState = new TextState
                {
                    FontSize = 72,
                    Font = FontRepository.FindFont("Arial"),
                    FontStyle = FontStyles.Bold,
                    ForegroundColor = Color.FromRgb(200, 200, 200)
                }
            };

            // Add the watermark to the first page (or loop for all pages)
            pdfDocument.Pages[1].AddStamp(textStamp);
            // foreach (Page page in pdfDocument.Pages) { page.AddStamp(textStamp); }

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/stamp.pdf");
            Console.WriteLine("Watermark applied successfully!");
        }
    }
}
```

### Ожидаемый результат

Откройте `stamp.pdf` в любом PDF‑просмотрщике. Вы должны увидеть полупрозрачный текст **«Auto‑fit»**, наклонённый под углом 45°, центрированный в прямоугольнике 400 × 200 пунктов. Остальное содержимое страниц остаётся нетронутым.

---

## Добавление дополнительного пользовательского текста — больше, чем простой водяной знак

Если нужно **add custom text PDF** помимо обычного водяного знака, просто измените аргумент конструктора `TextStamp`:

```csharp
var customStamp = new TextStamp("Confidential – For Internal Use Only")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    Width = 500,
    Height = 250,
    Rotate = RotationAngle.FromDegrees(30),
    Opacity = 0.2,
    TextState = new TextState
    {
        FontSize = 60,
        Font = FontRepository.FindFont("Times New Roman"),
        FontStyle = FontStyles.Italic,
        ForegroundColor = Color.FromRgb(255, 0, 0) // bright red for emphasis
    }
};
```

Затем добавьте `customStamp` на нужные страницы так же, как и раньше. Такая гибкость — причина, по которой многие разработчики выбирают Aspose для **how to use Aspose PDF** в производственных конвейерах.

---

## Распространённые ошибки и советы

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Водяной знак появляется позади существующего контента** | По умолчанию Aspose добавляет штампы **над** содержимым страницы, но у некоторых PDF есть слои, которые его скрывают. | Установите `StampAlignment` в `StampAlignment.Center` *и* уменьшите `Opacity`, чтобы увидеть сквозь него. |
| **Текст обрезается** | Прямоугольник (`Width`/`Height`) слишком мал для выбранного размера шрифта. | Включите `AutoAdjustFontSizeToFitStampRectangle` (уже сделано) или увеличьте размеры прямоугольника. |
| **Замедление при больших PDF** | Обход тысяч страниц добавляет накладные расходы. | Создайте один экземпляр `TextStamp` и переиспользуйте его; избегайте создания нового внутри цикла. |
| **Шрифт не найден** | Указанный шрифт не установлен на сервере. | Используйте `FontRepository.FindFont("Arial")`, который переключится на встроенный шрифт, или внедрите пользовательский TTF через `FontRepository |

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Add and Align Text Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET: Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}