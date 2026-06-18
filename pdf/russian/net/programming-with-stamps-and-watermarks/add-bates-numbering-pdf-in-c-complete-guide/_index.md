---
category: general
date: 2026-05-27
description: Добавьте нумерацию Бейтса в PDF с помощью Aspose.Pdf на C#. Узнайте,
  как быстро добавить нумерацию Бейтса, настроить формат и автоматизировать маркировку
  юридических документов.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: ru
og_description: Добавьте нумерацию Бейтса в PDF с помощью Aspose.Pdf на C#. Это руководство
  показывает, как добавить нумерацию Бейтса, настроить префиксы и сохранить результат.
og_title: Добавление нумерации Бейтса в PDF на C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Добавление нумерации Бейтса в PDF на C# – Полное руководство
url: /ru/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление нумерации Бейтса в PDF на C# – Полное руководство

Когда‑то задавались вопросом, **как добавить нумерацию Бейтса** в PDF, не тратя часы на ручные инструменты? Вы не одиноки — юридические команды, аудиторы и специалисты по e‑discovery нуждаются в надёжном способе **добавить нумерацию Бейтса PDF** программно.  

В этом руководстве мы пройдём через лаконичное, сквозное решение с использованием Aspose.Pdf для .NET, чтобы вы могли нанести номера Бейтса на любой документ всего несколькими строками кода C#.

## Что вы узнаете

- Как открыть существующий PDF с помощью Aspose.Pdf  
- Как создать артефакт нумерации Бейтса и точно настроить его формат  
- Как прикрепить артефакт к каждой странице (или только к первой)  
- Как сохранить обновлённый файл и проверить результат  

Предыдущий опыт работы с Aspose не требуется — достаточно базовых знаний C# и .NET. К концу вы получите переиспользуемый фрагмент кода, который можно скопировать‑вставить в любой проект.

## Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+)  
- NuGet‑пакет Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)  
- Исходный PDF‑файл, который нужно пометить (разместите его в папке, к которой у вас есть доступ)

> **Pro tip:** Если у вас ещё нет лицензии, Aspose предлагает бесплатный временный ключ, который удаляет водяные знаки оценки.

## Шаг 1 – Открытие исходного PDF‑документа  

Сначала нам нужен объект `Document`, представляющий файл на диске. Представьте, что это загрузка чистого холста, на который мы позже нанесём номера Бейтса.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Почему это важно:** Открытие документа внутри блока `using` гарантирует своевременное освобождение всех неуправляемых ресурсов, что особенно критично для больших PDF‑файлов.

## Шаг 2 – Создание артефакта нумерации Бейтса  

*BatesNumberingArtifact* — это способ Aspose описать, как должны выглядеть номера. Можно задать префикс, начальный номер, шаг и даже пользовательскую строку формата.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Почему вы можете изменить эти значения:**  
- **Prefix** полезен для идентификаторов дел («CASE‑», «DOC‑»).  
- **StartNumber** позволяет продолжить предыдущую серию.  
- **Increment** можно установить в 2, если нужна нечётная/чётная нумерация.  
- **Format** поддерживает любой .NET‑композитный формат; `{0:D5}` гарантирует пять цифр с ведущими нулями.

## Шаг 3 – Прикрепление артефакта к нужным страницам  

Артефакт можно добавить к одной странице, диапазону или ко всему документу. Для большинства юридических процессов мы прикрепляем его к *каждой* странице, но в примере ниже показан минимальный случай — добавление к первой странице.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Если нужно охватить все страницы, выполните цикл:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Почему этот шаг критичен:** Артефакты отрисовываются *после* содержимого страницы, поэтому номера появляются поверх существующего текста, не меняя оригинальную разметку.

## Шаг 4 – Сохранение изменённого PDF  

Наконец, запишите изменения обратно на диск. Можно перезаписать оригинал или создать новый файл — здесь мы генерируем свежую копию под именем `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Когда откроете `bates.pdf`, вы увидите «ABC01000» (или любой выбранный вами формат) в стандартном месте — обычно в правом нижнем углу.

## Полный рабочий пример  

Объединяя всё вместе, получаем полную программу, которую можно собрать и запустить:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Ожидаемый вывод

При запуске программы в консоли будет выведено:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Открытие `bates.pdf` показывает префикс «ABC», за которым следует пятизначная последовательность с нулями на каждой странице — точно то, что вы задали в коде.

## Часто задаваемые вопросы и особые случаи

### Можно ли разместить номер Бейтса в другом месте?

Да. Используйте свойство `Location` у `BatesNumberingArtifact` (например, `Location = new Position(10, 10)`) для указания пользовательских координат X/Y. Также можно задать `HorizontalAlignment` и `VerticalAlignment` для более гибкого позиционирования.

### Что делать, если мой PDF содержит тысячи страниц?

Aspose.Pdf эффективно потоково обрабатывает страницы, но всё‑равно рекомендуется обрабатывать их пакетами, если вы сталкиваетесь с ограничениями памяти. Класс `Document` также поддерживает `PdfConverter` для инкрементного сохранения.

### Как изменить шрифт или цвет?

Обёрните артефакт в объект `TextState`:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Нужна ли лицензия для использования в продакшене?

Лицензированная версия убирает водяные знаки оценки и открывает полную производительность. Бесплатная пробная версия подходит для тестов и прототипов.

## Проверка — быстрый визуальный контроль  

Если предпочитаете автоматическую проверку, Aspose может извлечь текст страницы и подтвердить наличие префикса:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Выполнение этого после шага сохранения выведет `Bates number verified.` при успешном завершении.

## Заключение  

Теперь вы знаете, **как добавить нумерацию Бейтса PDF** файлов с помощью Aspose.Pdf в C#. От открытия документа до настройки артефакта, его прикрепления к страницам и сохранения результата — процесс прост и полностью скриптуем.  

Что дальше? Попробуйте поэкспериментировать с:

- Различными значениями `Prefix` для нескольких партий дел  
- Пользовательскими `Location` и `TextState` для брендинга  
- Добавлением префиксов, специфичных для каждой страницы (например, «VOL‑1‑», «VOL‑2‑») путём изменения `StartNumber` в каждой итерации цикла  

Эти настройки позволяют адаптировать решение под почти любой юридический или архивный процесс.  

Есть дополнительные вопросы о **том, как добавить нумерацию Бейтса** для многоязычных PDF или зашифрованных файлов? Оставляйте комментарий ниже, и удачной разработки!

## Похожие руководства

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Different Headers in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}