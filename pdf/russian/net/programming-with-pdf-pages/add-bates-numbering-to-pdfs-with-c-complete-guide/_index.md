---
category: general
date: 2026-06-24
description: Добавьте нумерацию Бейтса в PDF‑файлы с помощью C# и Aspose.PDF. Узнайте,
  как создавать пользовательскую нумерацию страниц, последовательную нумерацию страниц
  и нумерацию в верхних и нижних колонтитулах за несколько минут.
draft: false
keywords:
- add bates numbering
- custom page numbers
- sequential page numbers
- bates numbering pdf
- header footer numbering
language: ru
og_description: Добавьте нумерацию Бейтса в PDF‑файлы с помощью C# и Aspose.PDF. Освойте
  пользовательскую нумерацию страниц и нумерацию верхних и нижних колонтитулов за
  несколько простых шагов.
og_title: Добавьте нумерацию Бейтса в PDF с помощью C# – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  headline: Add Bates Numbering to PDFs with C# – Complete Guide
  type: TechArticle
- description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  name: Add Bates Numbering to PDFs with C# – Complete Guide
  steps:
  - name: Load the Source PDF Document
    text: First we need a `Document` object that represents the file we want to modify.
  - name: Configure Bates Numbering Options (custom page numbers)
    text: Now we set up a `BatesNumberingOptions` object. This is where you define
      **custom page numbers**, the font, colors, and margins.
  - name: Apply the Bates Numbering to the Entire Document
    text: With the options prepared, the actual insertion is a single method call.
  - name: Save the PDF with Bates Numbers Applied
    text: Finally, write the modified document back to disk.
  - name: Limiting the Page Range
    text: 'Sometimes you only want to number a subset, such as pages 3‑10 of a 25‑page
      contract. Adjust `StartingPage` and `EndingPage` accordingly:'
  - name: Changing the Placement to Footer
    text: 'If your workflow requires **header footer numbering** at the bottom left,
      tweak the `Margin`:'
  - name: Using a Different Format
    text: 'Legal teams sometimes use “2024‑A‑001”. Just change the format string:'
  - name: Handling Transparent Backgrounds
    text: The `BackgroundColor = Color.Transparent` ensures the number doesn’t obscure
      existing content. If you need a light gray box behind the text for readability,
      replace it with `Color.LightGray`.
  type: HowTo
- questions:
  - answer: Yes—load the document with the password first (`pdfDocument = new Document("file.pdf",
      new LoadOptions { Password = "pwd" })`) then apply the same steps.
    question: Will this work with password‑protected PDFs?
  - answer: You can run `AddBatesNumbering` twice with two separate `BatesNumberingOptions`,
      each targeting either odd (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count;
      PageSequence = PageSequence.Odd`) or even pages.
    question: Can I add different numbers to odd and even pages?
  - answer: A trial works for evaluation, but the trial adds a watermark. For production
      use you’ll need a valid license to get a clean **bates numbering pdf**.
    question: Do I need a license for Aspose.PDF?
  type: FAQPage
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Добавьте нумерацию Бейтса в PDF с помощью C# — Полное руководство
url: /ru/net/programming-with-pdf-pages/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление Bates‑нумерации в PDF с помощью C# – Полное руководство

Добавьте Bates‑нумерацию в ваши PDF‑файлы на C# всего несколькими строками кода. Если вам когда‑нибудь требовались пользовательские номера страниц для юридических документов или вы хотите последовательную нумерацию страниц в пакете контрактов, этот учебник вам поможет.

За несколько минут мы пройдём всё, что нужно знать: загрузка PDF, настройка стиля нумерации, применение номеров и, наконец, сохранение обновлённого файла. К концу вы сможете генерировать **bates numbering pdf**, выглядящий профессионально, независимо от того, обрабатываете ли вы один файл или целую папку документов.

## Что вам понадобится

Прежде чем приступить, убедитесь, что у вас есть следующие предварительные требования:

- **.NET 6.0 или новее** – код ориентирован на .NET 6, но работают и более ранние версии .NET Framework.
- **Aspose.PDF for .NET** – коммерческая библиотека (доступна бесплатная пробная версия), предоставляющая классы `Document` и `BatesNumberingOptions`, используемые в этом руководстве.
- **IDE для C#** (Visual Studio, Rider или VS Code) – любой редактор, способный компилировать .NET‑проекты, подойдёт.
- Входной PDF‑файл с именем `input.pdf`, размещённый в папке, к которой вы можете обратиться из кода.

Всё готово? Отлично — начнём.

## Добавление Bates‑нумерации – Обзор

Основная идея **add bates numbering** состоит в том, чтобы рассматривать PDF как холст и «рисовать» строку (например, “DOC‑001”) в заголовке или нижнем колонтитуле каждой страницы. Aspose.PDF делает всю тяжёлую работу: вы просто описываете формат, диапазон страниц и визуальный стиль, а библиотека пишет номера за вас.

Ниже приведён полностью готовый пример, который можно скопировать‑вставить в консольное приложение. Каждая строка объяснена, так что вы поймёте не только *что* писать, но и *почему* каждый элемент важен.

### Шаг 1: Загрузка исходного PDF‑документа

Сначала нам нужен объект `Document`, представляющий файл, который мы хотим изменить.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

// Load the source PDF (replace the path with your actual folder)
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Почему это важно:** Класс `Document` — точка входа для всех операций с PDF. Он загружает файл в память, предоставляя доступ к коллекции `Pages`, по которой мы позже будем проходить, добавляя номера.

### Шаг 2: Настройка параметров Bates‑нумерации (пользовательские номера страниц)

Теперь создаём объект `BatesNumberingOptions`. Здесь вы определяете **custom page numbers**, шрифт, цвета и отступы.

```csharp
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    NumberingFormat = "DOC-{0:D3}",          // e.g., DOC-001, DOC-002 …
    StartNumber = 1,
    StartingPage = 1,
    EndingPage = pdfDocument.Pages.Count,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
    ForegroundColor = Color.Black,
    BackgroundColor = Color.Transparent,
    Margin = new Margin(0, 20, 20, 0)        // top, right, bottom, left (points)
};
```

- **NumberingFormat** – плейсхолдер `{0:D3}` заставляет Aspose дополнять числа тремя цифрами.
- **StartNumber** – откуда начинается последовательность; измените, если добавляете номера к уже существующему пакету.
- **StartingPage / EndingPage** – задают диапазон страниц; можно ограничить 2‑5 для подмножества, получив **sequential page numbers** только там, где они нужны.
- **Font & Colors** – визуальный стиль **header footer numbering**; Helvetica хорошо подходит для юридических документов благодаря своей чистоте и читаемости.
- **Margin** – позиционирует текст на 20 pt от верхнего и правого краёв; измените эти значения, чтобы переместить номер вниз или влево при необходимости.

> **Pro tip:** Если нужны номера в нижнем колонтитуле вместо заголовка, поменяйте значения `Margin` на что‑то вроде `new Margin(0, 0, 20, 20)` (низ, левый).

### Шаг 3: Применение Bates‑нумерации ко всему документу

Имея готовые параметры, фактическое вставление происходит одной вызовом метода.

```csharp
// Apply the numbering to every page in the defined range
pdfDocument.AddBatesNumbering(batesOptions);
```

За кулисами Aspose проходит по выбранным страницам, формирует каждый номер согласно `NumberingFormat` и рисует строку на холсте страницы. Это и есть сердце **add bates numbering** — без ручных циклов.

### Шаг 4: Сохранение PDF с применёнными номерами

Наконец, запишем изменённый документ обратно на диск.

```csharp
// Save the output file (choose a different name to avoid overwriting the source)
pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");
```

Открыв `BatesNumbered.pdf`, вы увидите “DOC‑001”, “DOC‑002”, … в правом верхнем углу каждой страницы. Это полностью рабочий **bates numbering pdf**, готовый к подаче или e‑discovery.

## Ожидаемый результат

| Страница | Заголовок (пример) |
|----------|--------------------|
| 1        | DOC‑001 |
| 2        | DOC‑002 |
| …        | … |
| N        | DOC‑00N |

Номера появляются точно там, где их разместил `Margin`, используя шрифт Helvetica Bold 12 pt. Если открыть файл в Adobe Acrobat, вы заметите, что номера являются частью содержимого страницы, а не отдельной аннотацией — они сохраняются при печати и «flattening».

## Особые случаи и варианты

### Ограничение диапазона страниц

Иногда нужно пронумеровать только часть, например страницы 3‑10 из 25‑страничного контракта. Отрегулируйте `StartingPage` и `EndingPage` соответственно:

```csharp
batesOptions.StartingPage = 3;
batesOptions.EndingPage = 10;
batesOptions.StartNumber = 1; // reset numbering for the subset
```

### Перемещение в нижний колонтитул

Если ваш процесс требует **header footer numbering** в левом нижнем углу, измените `Margin`:

```csharp
batesOptions.Margin = new Margin(20, 0, 0, 20); // top, right, bottom, left
```

### Использование другого формата

Юридические команды иногда используют “2024‑A‑001”. Просто измените строку формата:

```csharp
batesOptions.NumberingFormat = "2024-A-{0:D3}";
```

### Обработка прозрачного фона

`BackgroundColor = Color.Transparent` гарантирует, что номер не будет закрывать существующее содержимое. Если нужен светло‑серый фон за текстом для лучшей читаемости, замените его на `Color.LightGray`.

## Часто задаваемые вопросы (Ответы)

- **Будет ли это работать с PDF, защищёнными паролем?**  
  Да — сначала загрузите документ с паролем (`pdfDocument = new Document("file.pdf", new LoadOptions { Password = "pwd" })`), затем выполните те же шаги.

- **Можно ли добавить разные номера на нечётные и чётные страницы?**  
  Да, запустите `AddBatesNumbering` дважды с двумя отдельными `BatesNumberingOptions`, каждый из которых нацелен либо на нечётные (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count; PageSequence = PageSequence.Odd`), либо на чётные страницы.

- **Нужна ли лицензия для Aspose.PDF?**  
  Пробная версия подходит для оценки, но она добавляет водяной знак. Для продакшн‑использования потребуется действующая лицензия, чтобы получить чистый **bates numbering pdf**.

## Полный рабочий пример (Готов к копированию)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Set up numbering options (custom page numbers, sequential page numbers)
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            NumberingFormat = "DOC-{0:D3}",
            StartNumber = 1,
            StartingPage = 1,
            EndingPage = pdfDocument.Pages.Count,
            Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
            ForegroundColor = Color.Black,
            BackgroundColor = Color.Transparent,
            Margin = new Margin(0, 20, 20, 0) // top, right, bottom, left
        };

        // 3️⃣ Apply the numbering (header footer numbering)
        pdfDocument.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the result
        pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Запустите программу, откройте полученный файл, и вы увидите номера точно там, где код указал Aspose разместить их. Никаких дополнительных циклов, никакого ручного рисования — только **add bates numbering** в четыре лаконичных шага.

## Заключение

Теперь у вас есть надёжный, готовый к продакшн способ **add bates numbering** в любой PDF с помощью C# и Aspose.PDF. От загрузки документа до настройки **custom page numbers**, применения **sequential page numbers** и сохранения чистого **bates numbering pdf** — весь процесс укладывается в один вызов метода.

Что дальше? Попробуйте комбинировать эту технику с другими возможностями Aspose — например, добавить логотип, объединить несколько PDF‑файлов или извлечь страницы на основе только что добавленных номеров. Исследование **header footer numbering** вместе с водяными знаками откроет новые возможности.

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Aspose.PDF .NET: Добавление номеров страниц в PDF с помощью FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Как добавить и настроить номера страниц в PDF с помощью Aspose.PDF for .NET | Руководство по работе с документами](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Добавление изображений и номеров страниц в PDF с помощью Aspose.PDF for .NET: Полное руководство](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}