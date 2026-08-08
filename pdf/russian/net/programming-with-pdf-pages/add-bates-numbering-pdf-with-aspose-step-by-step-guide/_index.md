---
category: general
date: 2026-08-08
description: Добавьте нумерацию Бейтса в PDF с помощью Aspose.Pdf на C#. Этот учебник
  также показывает, как добавить пустую страницу в PDF и генерировать PDF программно.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: ru
lastmod: 2026-08-08
og_description: Добавьте нумерацию Бейтса в PDF с помощью Aspose.Pdf на C#. Узнайте,
  как добавить пустую страницу в PDF, генерировать PDF программно и сохранять готовый
  документ за считанные минуты.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Добавление нумерации Бейтса в PDF с Aspose — полное руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Добавление нумерации Бейтса в PDF с помощью Aspose – пошаговое руководство
url: /ru/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add bates numbering pdf with Aspose – пошаговое руководство

Добавление bates numbering pdf с Aspose.Pdf довольно простое, как только вы поймёте основные шаги. Если вам также нужно добавить blank page pdf или генерировать pdf программно, это руководство охватывает всё необходимое.

В этом учебнике вы:

* Создадите новый PDF‑документ с нуля.  
* Добавите blank page pdf, который будет содержать номера Бейтса.  
* Настроите артефакт BatesNumberingArtifact с пользовательским префиксом.  
* Сохраните PDF, чтобы номера отобразились в сгенерированном файле.  

К концу вы получите полностью рабочее консольное приложение C#, которое создаёт PDF с номерами Бейтса, например **CASE‑1000**, **CASE‑1001**, … – типичное требование для юридических и e‑discovery процессов.

## Требования

* .NET 6.0 SDK или новее (код также работает с .NET Framework 4.8).  
* Visual Studio 2022 или любой совместимый с C# IDE.  
* Действительная лицензия Aspose.Pdf for .NET (или бесплатный оценочный ключ).  
* Базовое знакомство с синтаксисом C#.

> **Pro tip:** Если запустить код без лицензии, Aspose добавит небольшую водяную метку в выходной PDF.

## Шаг 1: Настройка проекта и импорт Aspose.Pdf

Создайте новый консольный проект и добавьте пакет Aspose.Pdf NuGet:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Необходимые директивы `using` для примера:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Эти пространства имён дают доступ к классам `Document`, `Page` и `BatesNumberingArtifact`, которые будут использованы позже.

## Шаг 2: Добавление blank page pdf

Номер Бейтса должен быть привязан к странице, поэтому сначала создаём пустую страницу, которая получит артефакт нумерации.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

Класс `Document` представляет весь PDF‑файл, а `Pages.Add()` вставляет новую пустую страницу в конец коллекции страниц документа. Поскольку документ изначально пуст, этот вызов также создаёт первую страницу.

## Шаг 3: Настройка BatesNumberingArtifact

Теперь определим, как должны выглядеть номера Бейтса. `BatesNumberingArtifact` позволяет задать стартовый номер, префикс, суффикс и параметры форматирования.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Почему это важно:**  
Установка `StartNumber` в **1000** соответствует типичным конвенциям юридических дел. `Prefix` гарантирует, что каждый номер будет выглядеть как **CASE‑1000**, **CASE‑1001**, …, что упрощает поиск и сортировку.

## Шаг 4: Привязка артефакта к странице

Артефакт необходимо добавить в коллекцию `Artifacts` страницы, чтобы Aspose отрисовал его на каждой странице при сохранении.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

При сохранении документа Aspose автоматически повторяет артефакт на всех страницах, увеличивая номер для каждой последующей страницы.

## Шаг 5: (Опционально) Добавление дополнительных страниц

Если нужны дополнительные страницы, просто повторите `pdfDocument.Pages.Add()`. Прикреплённый в предыдущем шаге артефакт BatesNumberingArtifact автоматически появится на каждой новой странице.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Шаг 6: Сохранение PDF – генерация pdf программно

Наконец, сохраняем документ на диск. В этот момент номера Бейтса отрисовываются на страницах.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Ожидаемый результат:**  
Откройте *BatesNumberedDocument.pdf* — вы увидите трёхстраничный PDF. Каждая страница отображает номер Бейтса в правом нижнем углу:

* Страница 1 → **CASE‑1000**  
* Страница 2 → **CASE‑1001**  
* Страница 3 → **CASE‑1002**

Номера автоматически инкрементируются, потому что артефакт привязан к коллекции страниц.

## Полный, исполняемый пример

Объединив всё вместе, получаем полностью готовую консольную программу, которую можно скопировать, вставить и запустить:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Запустите программу командой `dotnet run`. После выполнения найдите файл на рабочем столе и проверьте номера Бейтса.

![Пример добавления bates numbering pdf](/images/bates-numbering.png "Пример добавления bates numbering pdf")

## Часто задаваемые вопросы и особые случаи

### Что если мне нужен другой шрифт или позиция?

`BatesNumberingArtifact` раскрывает свойства, такие как `FontSize`, `FontColor`, `HorizontalAlignment` и `VerticalAlignment`. Например:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Как исключить конкретную страницу из нумерации?

Создайте отдельный `BatesNumberingArtifact` для страниц, которые нужно пронумеровать, и добавьте его только к этим страницам. Страницы без прикреплённого артефакта останутся ненумерованными.

### Работает ли это с существующими PDF?

Да. Вместо `new Document()` загрузите существующий файл:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Затем привяжите артефакт к нужным страницам и сохраните.

## Заключение

Теперь вы знаете, как **add bates numbering pdf** с помощью Aspose.Pdf, как **add blank page pdf**, и как **generate pdf programmatically** в чистом, переиспользуемом решении на C#. Подход работает с любым количеством страниц, пользовательскими префиксами и параметрами стиля, предоставляя полный контроль над конечным документом.

Следующие шаги, которые вы можете изучить:

* Use **create pdf as

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}