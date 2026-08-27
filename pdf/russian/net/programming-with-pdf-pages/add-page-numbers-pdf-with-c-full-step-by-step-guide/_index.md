---
category: general
date: 2026-01-02
description: Быстро добавляйте номера страниц в PDF с помощью Aspose.Pdf на C#. Узнайте,
  как добавить нумерацию Бейтса, текст в нижний колонтитул, пользовательский водяной
  знак и пройтись по страницам PDF в одном скрипте.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: ru
og_description: Мгновенно добавляйте номера страниц в PDF с помощью Aspose.Pdf. В
  этом руководстве также рассматривается добавление нумерации Бейтса, текста в нижний
  колонтитул, пользовательского водяного знака и перебор страниц PDF.
og_title: Добавление номеров страниц в PDF с помощью C# – Полный учебный курс по программированию
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Добавление номеров страниц в PDF с помощью C# – Полное пошаговое руководство
url: /ru/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление номеров страниц в PDF с помощью C# – Полный учебный курс

Когда‑то вам нужно было **добавить номера страниц в PDF**‑файлы, но вы не знали, с чего начать? Вы не одиноки — разработчики постоянно спрашивают, как проставить номера, нижние колонтитулы или даже идентификатор в стиле Bates на каждой странице PDF.  

В этом руководстве вы увидите готовый к запуску пример на C#, который **перебирает страницы PDF**, ставит нижний колонтитул с номером страницы и (при желании) добавляет пользовательский водяной знак. Мы также покажем, как переключить штамп на номер Bates, что по‑прежнему означает «добавить нумерацию Bates» для юридических или судебных документов. К концу вы получите один переиспользуемый метод, который справится со всеми этими задачами без усилий.

## Добавление номеров страниц в PDF – Обзор

Прежде чем погрузиться в код, разберём, что именно означает «add page numbers pdf» в мире Aspose.Pdf. Библиотека рассматривает любой кусок текста, размещённый на странице, как **TextStamp**. Создав один штамп с заполнителем страницы (`{page}`) и применив его к каждой странице, вы автоматически получаете последовательную нумерацию. Тот же штамп может содержать дополнительный текст, так что вы можете **add footer text** вроде «Confidential» или специфичного идентификатора дела.

> **Почему использовать штамп вместо редактирования потока содержимого PDF?**  
> Штампы — это объекты высокого уровня, которые учитывают поля страницы, её поворот и существующую графику. Их также гораздо проще поддерживать — измените несколько свойств и запустите скрипт заново.

## Перебор страниц PDF для применения штампов

Первый практический шаг — открыть исходный PDF и пройтись по его страницам. Это классический шаблон **loop through pdf pages**, который используют большинство примеров Aspose.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Pro tip:** Если ваш PDF огромный (сотни страниц), рассмотрите обработку его пакетами, чтобы снизить потребление памяти. Aspose.Pdf лениво читает страницы, так что сам цикл уже довольно эффективен.

## Добавление нумерации Bates и текста нижнего колонтитула

Теперь, когда мы можем пройтись по каждой странице, создадим **reusable TextStamp**, который будет содержать как номер страницы, так и необязательный текст нижнего колонтитула. Заполнитель `{page}` автоматически заменяется текущим номером страницы.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Почему это работает

* **`Bates-{page}`** – Aspose заменяет `{page}` реальным номером страницы, автоматически получая классический номер Bates.
* **`Confidential`** – Это часть **add footer text**. Вы можете заменить её любой строкой, даже вытягивая данные из базы.
* **Стилизация** – С помощью `TextState` можно настроить цвет, непрозрачность и даже поворот, не трогая внутренние потоки PDF.

Если нужны только простые цифры, уберите префикс «Bates‑» и лишний текст:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Добавление пользовательского водяного знака (опционально)

Иногда требуется не только нижний колонтитул — нужен полупрозрачный логотип или наложение «DRAFT» на всю страницу. Здесь вступает в игру **add custom watermark**. Тот же класс `TextStamp` можно переиспользовать, просто изменив выравнивание и непрозрачность.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Note:** Порядок имеет значение. Сначала добавьте водяной знак, чтобы номера страниц оставались читаемыми поверх полупрозрачного текста.

## Сохранение PDF и проверка результатов

После штамповки последний шаг — записать изменения на диск. Вызов `Save`, который мы разместили ранее, делает основную работу, но добавим быстрый фрагмент проверки, который откроет новый файл и выведет количество обработанных страниц.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Когда вы запустите полную программу, вы увидите PDF, где каждая страница заканчивается чем‑то вроде **«Bates‑3 – Confidential»** (или просто «3», если использовался простой штамп) и, если вы включили водяной знак, лёгким «DRAFT» посередине.

### Ожидаемый вывод

| Страница | Нижний колонтитул (пример) |
|----------|---------------------------|
| 1        | Bates‑1 – Confidential |
| 2        | Bates‑2 – Confidential |
| …        | … |
| N        | Bates‑N – Confidential |

Если открыть файл в просмотрщике, номера будут располагаться на 20 pt от левого и нижнего полей, что соответствует типичным юридическим требованиям.

## Полный рабочий пример (готов к копированию)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Сохраните его как `AddPageNumbers.cs`, восстановите пакет Aspose.Pdf через NuGet (`Install-Package Aspose.Pdf`) и запустите. Вы получите **add page numbers pdf**‑файл, который также демонстрирует **add bates numbering**, **add footer text**, **add custom watermark** и классический **loop through pdf pages**‑шаблон — всё в одном аккуратном скрипте.

![пример добавления номеров страниц pdf](https://example.com/images/add-page-numbers-pdf.png "Скриншот, показывающий нумерованные страницы PDF с нижним колонтитулом и водяным знаком")

## Заключение

Мы рассмотрели всё, что нужно для **add page numbers pdf**‑файлов с помощью Aspose.Pdf в C#. От перебора каждой страницы, штамповки номеров Bates, добавления пользовательского текста нижнего колонтитула до наложения полупрозрачного водяного знака — код достаточно компактен, чтобы его можно было вставить в любой существующий проект.  

Далее вы можете исследовать более продвинутые сценарии — например, вытягивать текст нижнего колонтитула из базы данных, применять разные шрифты для разных разделов или генерировать отдельный индексный PDF со списком всех номеров Bates. Все эти расширения опираются на те же базовые идеи, которые мы показали, так что вы готовы расширять решение по мере роста требований.  

Попробуйте, подправьте стили и дайте знать в комментариях, как у вас всё получилось. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}