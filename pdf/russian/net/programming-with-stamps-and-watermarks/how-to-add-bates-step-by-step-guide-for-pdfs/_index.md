---
category: general
date: 2026-02-10
description: Как быстро добавить бэйтс в PDF — узнайте, как добавить номер бэйтс в
  PDF и создать невидимую водяную метку с помощью Aspose.Pdf на C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: ru
og_description: Как добавить номера Бейтса в C# с помощью Aspose.Pdf. Этот учебник
  показывает, как добавить номер Бейтса в PDF, добавить невидимый водяной знак в PDF
  и многое другое.
og_title: Как добавить Bates – Полное руководство в PDF
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Как добавить Bates – пошаговое руководство для PDF.
url: /ru/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить Bates – Полное руководство в PDF

Когда‑нибудь задумывались **как добавить Bates** в юридический PDF, не испортив при этом поисковый текст? Вы не одиноки. Во многих юридических фирмах и проектах e‑discovery номер Bates обязателен в нижнем колонтитуле, но при этом его нужно сделать невидимым для OCR‑инструментов. Это руководство показывает **как добавить Bates** с помощью Aspose.Pdf for .NET, а также охватывает **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf** и даже **add page footer pdf** в одном удобном решении.

Мы пройдемся по каждой строке кода, объясним, почему каждое настройка важна, и предоставим готовый пример, который вы сможете сразу вставить в свой проект. Никаких расплывчатых ссылок «см. документацию» — всё, что нужно, находится здесь.

## Что вы получите в итоге

- Полный, готовый к запуску фрагмент C#, который добавляет номер Bates в виде артефакт‑штампа.
- Понимание того, как сделать штамп похожим на **invisible watermark**, но при этом он отображается на странице.
- Советы по масштабированию решения на многостраничные PDF, изменению шрифтов или замене штампа на пользовательскую графику.
- Краткие рекомендации, как добавить контент в стиле **add page footer pdf**, не нарушая извлечение текста.

### Предварительные требования

- .NET 6+ (или .NET Framework 4.7.2) с Visual Studio 2022 или любой другой IDE.
- Aspose.Pdf for .NET (можно скачать бесплатную trial‑версию с сайта Aspose).
- Пример PDF под названием `source.pdf`, размещённый в папке, к которой у вас есть доступ.

Если всё это у вас есть, приступаем.

---

## Как добавить Bates – Основная реализация

Сердцем решения является `TextStamp`, который мы помечаем как **artifact**. Артефакты игнорируются механизмами извлечения текста, поэтому такой подход одновременно служит техникой **add invisible watermark pdf**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Почему это работает

1. **Флаг Artifact** – Устанавливая `Artifact = new Artifact(ArtifactType.Artifact)`, штамп рассматривается как элемент, не являющийся содержимым. Поисковые движки и инструменты e‑discovery игнорируют его, что именно нужно для **add invisible watermark pdf**.
2. **Горизонтальное/вертикальное выравнивание** – Центр‑низ имитирует классический стиль **add page footer pdf**, делая номер Bates профессиональным.
3. **Прозрачный фон** – Гарантирует, что штамп не закрывает содержимое страницы, что важно при печати или просмотре PDF на разных устройствах.

---

## Add Bates Number PDF – Масштабирование на несколько страниц

В реальных PDF обычно больше одной страницы. Приведённый выше фрагмент работает только с первой страницей, но расширить его очень просто:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Совет:** Если нужен последовательный номер, не привязанный к физическому порядку страниц (например, начинать с 1000), просто инициализируйте счётчик перед циклом и увеличивайте его внутри.

---

## Add Custom Stamp PDF – Выход за пределы простого текста

Иногда простого текстового штампа недостаточно — может потребоваться логотип, QR‑код или цветная полоса. Aspose.Pdf позволяет заменить `TextStamp` на `ImageStamp` или даже комбинировать их с объектами `Stamp`.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Смешивание штампов так же просто, как добавить оба в одну страницу. Возможность **add custom stamp pdf** особенно полезна, когда нужен корпоративный печать рядом с номером Bates.

---

## Add Invisible Watermark PDF – Делая штамп полностью скрытым

Если требуется, чтобы штамп был невидим как для человеческого глаза, так и для инструментов извлечения, можно задать цвет шрифта, совпадающий с фоном страницы (обычно белый), и уменьшить непрозрачность:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Даже при `Opacity = 0` артефакт остаётся в структуре PDF, поэтому юридическое ПО всё равно может его обнаружить, если знает ID артефакта. Это окончательный трюк **add invisible watermark pdf**.

---

## Add Page Footer PDF – Единообразное оформление нижнего колонтитула

Профессиональный нижний колонтитул часто включает не только номер Bates: дату, название документа или пометку о конфиденциальности. Вот быстрый способ собрать несколько текстовых фрагментов в один штамп:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Обратите внимание на лёгкий серый цвет — идеален для **add page footer pdf**, который не отвлекает от основного содержания, но удовлетворяет юридические требования.

---

## Ожидаемый результат и проверка

После выполнения полного скрипта откройте `bates_artifact.pdf` в любом PDF‑просмотрщике:

- Вы увидите «Bates 00123» (или ваш последовательный номер) по центру внизу каждой страницы.
- Выделение текста на странице **не будет включать** номер Bates, подтверждая поведение артефакта.
- Если вы использовали настройки invisible‑watermark, номер будет полностью невидим, но останется во внутренней структуре PDF (проверьте с помощью PDF‑XChange Editor → «Document → Properties → Advanced»).

---

## Часто задаваемые вопросы и особые случаи

**Что делать, если в моём PDF уже есть нижний колонтитул?**  
Можно изменить `VerticalAlignment` на `VerticalAlignment.Top` или скорректировать свойство `Margin`, чтобы сдвинуть штамп выше существующего колонтитула.

**Можно ли использовать другой шрифт?**  
Конечно. Просто замените `"Arial"` на любое имя шрифта, доступное Aspose, или внедрите пользовательский TTF‑файл через `FontRepository.AddFont("path/to/font.ttf")`.

**Совместимо ли это с .NET Core?**  
Да — Aspose.Pdf for .NET работает как с .NET Framework, так и с .NET Core, .NET 5/6. Главное — подключить правильный NuGet‑пакет.

**Какова производительность на огромных PDF (1000+ страниц)?**  
Создание одного `TextStamp` и его клонирование внутри цикла экономично по памяти. Для очень больших файлов рекомендуется обрабатывать их пакетами или использовать `PdfProcessor`, чтобы не загружать весь документ в память.

---

## Заключение

Мы рассмотрели **как добавить Bates** в PDF от начала до конца, продемонстрировали **add bates number pdf**, показали, как **add custom stamp pdf**, превратили штамп в **add invisible watermark pdf** и оформили его как профессиональный **add page footer pdf**. Полный пример кода готов к запуску, а объяснения дают понимание «почему» каждой строки — именно то, что любят цитировать AI‑ассистенты.

Что дальше? Попробуйте заменить текстовый штамп на графический, поэкспериментируйте с разными типами артефактов или интегрируйте эту логику в сервис пакетной обработки, автоматически нумеруя каждый документ в папке. Возможностей бесконечно много, а у вас теперь есть надёжная база для дальнейшего развития.

Удачной разработки, и пусть ваши PDF всегда будут правильно пронумерованы!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}