---
category: general
date: 2026-03-24
description: Как добавить штамп в PDF с помощью Aspose.Pdf на C#. Узнайте, как разместить
  штамп в PDF и добавить текстовый штамп в PDF с автоматическим масштабированием за
  несколько простых шагов.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: ru
og_description: Как добавить штамп в PDF на C#? Это руководство покажет, как разместить
  штамп в PDF и добавить текстовый штамп в PDF с автоматическим масштабированием шрифта,
  используя Aspose.Pdf.
og_title: Как добавить штамп в PDF с помощью Aspose.Pdf – Краткое руководство
tags:
- pdf
- csharp
- aspose
- stamping
title: Как добавить штамп в PDF с помощью Aspose.Pdf – пошаговое руководство
url: /ru/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить штамп в PDF с помощью Aspose.Pdf – пошаговое руководство

**Как добавить штамп** в PDF — это распространённая потребность, когда нужно брендировать, заверить или просто прокомментировать документ. Задумывались ли вы, как проще всего разместить штамп в PDF, не возясь с низкоуровневой графикой? В этом руководстве мы пройдёмся по полностью готовому решению, которое не только показывает **как добавить штамп**, но и объясняет *почему* каждая строка кода важна.

Вы узнаете, как **разместить штамп PDF** на любой странице, как **добавить текстовый штамп PDF**, который автоматически уменьшается, чтобы вписаться в свой прямоугольник, и какие подводные камни следует избегать, когда текст слишком длинный. К концу вы получите один файл C#, который можно добавить в проект и сразу начинать штамповать PDF‑файлы.

## Предварительные требования

Прежде чем приступить, убедитесь, что у вас есть:

* .NET 6.0 или новее (код работает и с .NET Core, и с .NET Framework).
* NuGet‑пакет Aspose.Pdf for .NET (`Aspose.Pdf`) установлен.
* PDF‑файл с именем `input.pdf` в папке, к которой вы можете обратиться (подойдёт любой простой одностраничный PDF).

Дополнительная конфигурация не требуется — Aspose.Pdf берёт на себя всю тяжёлую работу.

## Шаг 1: Настройка проекта и загрузка исходного PDF

Первое, что нам нужно, — объект `Document`, представляющий PDF, который мы хотим аннотировать. Представьте его как пустой холст, на который позже нанесём штамп.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Почему это важно:** `Document` — точка входа для любой работы с PDF в Aspose.Pdf. Используя паттерн `using`, мы гарантируем освобождение файлового дескриптора, что предотвращает блокировку файла при последующей попытке сохранить изменённый PDF.

## Шаг 2: Создание текстового штампа с автоматической настройкой размера шрифта

Теперь создаём `TextStamp`. Хитрость, выделяющая этот пример, — флаг `AutoAdjustFontSizeToFitStampRectangle`: он заставляет Aspose уменьшать текст, пока он не впишется в заданный прямоугольник.

```csharp
// Create a text stamp that will automatically resize to fit its rectangle
var textStamp = new TextStamp("Long text that must fit")
{
    // Let Aspose shrink the text if it overflows
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Precision of the auto‑adjust algorithm (lower = more accurate)
    AutoAdjustFontSizePrecision = 0.01f,
    // Define the stamp's bounding box (in points)
    Width = 300,
    Height = 100,
    // Word‑wrap by whole words so we don’t split in the middle of a word
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    // Optional: set background color or opacity if you want a visible box
    Background = new Background()
    {
        Color = Color.LightGray,
        Opacity = 0.5
    }
};
```

> **Совет:** Если вместо текста нужен логотип или изображение, используйте `ImageStamp` — та же логика автоматической настройки применяется и к масштабированию изображения.

## Шаг 3: Выбор места **размещения штампа PDF** — первая страница, последняя или произвольный индекс

Aspose.Pdf хранит страницы в коллекции, нумерация которой начинается с 1 (`pdfDocument.Pages[1]` — первая страница). Вы можете **разместить штамп PDF** на любой странице, изменив индекс.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **Почему это гибко:** Поскольку коллекция `Pages` изменяема, вы можете пройтись циклом по всем страницам и добавить один и тот же штамп к каждой, либо выбрать конкретную страницу в зависимости от бизнес‑логики (например, только обложку).

## Шаг 4: Сохранение изменённого документа

После штампования необходимо записать изменения на диск. Можно перезаписать исходный файл или создать новый — на ваш выбор.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

Когда вы откроете `output-stamped.pdf`, вы увидите светло‑серый прямоугольник на первой странице с текстом «Long text that must fit». Если текст будет длиннее, Aspose автоматически уменьшит его, пока он не поместится полностью в прямоугольник размером 300 × 100 pt.

## Полный рабочий пример

Ниже приведена полная программа, которую можно скопировать в консольное приложение (`Program.cs`). В ней собраны все обсуждаемые части, плюс небольшой помощник для проверки, что штамп действительно появился.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;   // Needed for Background and Color

namespace PdfStampDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the source PDF
            using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Create a text stamp with auto‑adjusting font size
            var textStamp = new TextStamp("Long text that must fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                Width = 300,
                Height = 100,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Background = new Background()
                {
                    Color = Color.LightGray,
                    Opacity = 0.5
                }
            };

            // 3️⃣ Place the stamp on the first page (you can change the index)
            pdfDocument.Pages[1].AddStamp(textStamp);

            // 4️⃣ Save the result
            string outputPath = "YOUR_DIRECTORY/output-stamped.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Stamp added successfully! Check the file at: {outputPath}");
        }
    }
}
```

### Ожидаемый результат

* PDF открывается с полупрозрачным серым полем на первой странице.
* Внутри поля предоставленный текст помещается идеально, даже если заменить его более длинным предложением.
* Нет необходимости вручную рассчитывать размер шрифта — Aspose делает всю тяжёлую работу.

## Частые проблемы при **размещении штампа PDF**

| Признак | Возможная причина | Решение |
|---------|-------------------|---------|
| Текст обрезан | `AutoAdjustFontSizeToFitStampRectangle` **false** или прямоугольник слишком мал. | Включите флаг и увеличьте `Width`/`Height` или сократите длину текста. |
| Штамп смещён | Значения `HorizontalAlignment`/`VerticalAlignment` по умолчанию `Left`/`Top`. | Установите `HorizontalAlignment = HorizontalAlignment.Center` и `VerticalAlignment = VerticalAlignment.Center`. |
| Штамп не виден в некоторых просмотрщиках | Прозрачность фона установлена в 0 или цвет штампа совпадает с фоном страницы. | Используйте контрастный `Background.Color` или задайте `Opacity` > 0.3. |
| Несколько штампов накладываются друг на друга | Добавление штампов в цикле без смещения координат. | Используйте `textStamp.XIndent` и `textStamp.YIndent` для смещения каждого штампа. |

Решение этих вопросов на ранних этапах экономит массу времени на отладку позже.

## Расширение примера: добавление изображения‑штампа

Если вам нужно **добавить текстовый штамп PDF** *и* изображение (например, логотип компании), их можно комбинировать:

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    Width = 100,
    Height = 50,
    XIndent = 400,          // Position to the right of the text stamp
    YIndent = 20,
    Background = new Background()
    {
        Color = Color.Transparent
    }
};

pdfDocument.Pages[1].AddStamp(imageStamp);
```

Теперь страница отображает одновременно динамический текстовый штамп и статический изображение‑штамп рядом.

## Тестирование реализации

1. Запустите консольное приложение.  
2. Откройте `output-stamped.pdf` в Adobe Reader, Edge или любом другом PDF‑просмотрщике.  
3. Убедитесь, что прямоугольник штампа присутствует и текст полностью виден.  
4. Замените текст на более длинную фразу, запустите снова и проверьте, что шрифт автоматически уменьшился.

Если что‑то выглядит неправильно, ещё раз проверьте размеры прямоугольника и настройку `AutoAdjustFontSizePrecision`.

## Заключение

Теперь вы знаете **как добавить штамп** в PDF с помощью Aspose.Pdf, как **разместить штамп PDF** на конкретной странице и как **добавить текстовый штамп PDF**, который автоматически подстраивает размер шрифта. Полный, готовый к запуску пример выше устраняет догадки и даёт прочную основу для более сложных сценариев штампования — например, пакетной обработки десятков файлов или условного добавления водяных знаков.

Готовы к следующему шагу? Попробуйте штамповать каждую страницу в цикле, поэкспериментируйте с разными шрифтами или комбинируйте изображение и текст, чтобы создать профессиональную печать. Возможности безграничны, а с Aspose.Pdf у вас под капотом надёжный движок.

Если столкнулись с трудностями, оставьте комментарий или обратитесь к документации Aspose.Pdf для более глубокой кастомизации. Счастливого штампования!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}