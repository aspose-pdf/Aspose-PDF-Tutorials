---
category: general
date: 2026-10-10
description: Создайте клиент OpenAI на C# и изучите, как суммировать PDF, преобразовать
  PDF в резюме и сохранить сгенерированное резюме PDF с помощью Aspose.Pdf.AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- how to summarize pdf
- how to save summary
- generate pdf summary
language: ru
lastmod: 2026-10-10
og_description: Создайте клиент OpenAI на C# и мгновенно узнайте, как суммировать
  PDF, преобразовать PDF в резюме и сохранить сгенерированное резюме PDF.
og_image_alt: Screenshot of C# code that creates an OpenAI client and generates a
  PDF summary
og_title: Создайте клиент OpenAI и сгенерируйте PDF‑резюме на C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  headline: How to create OpenAI client and generate a PDF summary in C#
  type: TechArticle
- description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  name: How to create OpenAI client and generate a PDF summary in C#
  steps:
  - name: '**Console output** – the plain‑text summary displayed on the screen.'
    text: '**Console output** – the plain‑text summary displayed on the screen.'
  - name: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
    text: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
  - name: Lower the `WithTemperature` to 0.2 for more deterministic output.
    text: Lower the `WithTemperature` to 0.2 for more deterministic output.
  - name: Increase the
    text: Increase the
  type: HowTo
tags:
- OpenAI
- C#
- PDF processing
- Aspose.Pdf.AI
title: Как создать клиент OpenAI и сгенерировать PDF‑резюме на C#
url: /ru/net/document-creation/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать клиент OpenAI и сгенерировать PDF‑резюме на C#

Если вам нужно **создать клиент OpenAI** в .NET‑приложении, этот учебник покажет, как это сделать, и как превратить любой PDF в лаконичное, сгенерированное ИИ резюме. Вы увидите, как **преобразовать PDF в резюме**, получить текст и **сохранить резюме** в новый PDF‑файл — всё с помощью Aspose.Pdf.AI.

Создание резюме PDF — распространённая задача в документоёмких процессах, таких как юридический аудит, агрегирование исследований или автоматическая генерация отчётов. К концу этого руководства вы сможете **программно генерировать PDF‑резюме**, не выходя из кода C#.

## Что вам понадобится

- .NET 6.0 или новее (пример ориентирован на .NET 6, но подойдёт любая современная версия .NET)
- NuGet‑пакет Aspose.Pdf.AI (`Aspose.Pdf.AI`) — упрощённый обёртка для вызовов OpenAI по работе с PDF‑контентом
- Действительный API‑ключ OpenAI (его можно получить в портале OpenAI)
- Пример PDF‑файла, который требуется резюмировать (например, `SampleDocument.pdf`)
- Visual Studio 2022, VS Code или любой IDE, поддерживающий разработку на C#

> **Pro tip:** Храните ваш API‑ключ в безопасном месте, например в [user‑secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) или Azure Key Vault. Никогда не встраивайте его напрямую в исходный код.

## Шаг 1: Установите NuGet‑пакет Aspose.Pdf.AI

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.Pdf.AI
```

Пакет подтягивает необходимый HTTP‑клиент, инструменты для работы с PDF и лёгкую обёртку вокруг API OpenAI. После установки восстановите проект, чтобы убедиться, что все зависимости доступны:

```bash
dotnet restore
```

## Шаг 2: **Создать клиент OpenAI** с вашим API‑ключом

Создание клиента — первый шаг к любой AI‑управляемой операции с PDF. `OpenAIClient` обрабатывает аутентификацию, ограничение запросов и пул соединений за вас.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    // Replace with your real key – never commit it to source control
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // ---- Step 2: create OpenAI client ----
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // The client is now ready for any Aspose.Pdf.AI operation.
        await SummarizePdfAsync(openAiClient);
    }
}
```

> **Почему это важно:** Оператор `using` гарантирует корректное освобождение клиента, освобождая сетевые ресурсы и предотвращая исчерпание сокетов в длительно работающих сервисах.

## Шаг 3: Настройте параметры резюме – **преобразовать PDF в резюме**

Объект `OpenAISummaryCopilotOptions` указывает ИИ, что нужно сделать. Вы можете задать температуру, ограничить количество токенов и, что самое главное, указать исходный PDF.

```csharp
private static async Task SummarizePdfAsync(OpenAIClient client)
{
    // ---- Step 3: set up summary options (convert PDF to summary) ----
    var summaryOptions = OpenAISummaryCopilotOptions
        .Create()
        .WithTemperature(0.5)                     // Balanced creativity vs. factuality
        .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

    // The options are immutable; each call returns a new instance.
```

### Почему температура 0.5?

Температура 0.5 даёт лаконичный, точный язык, позволяя модели при этом перефразировать предложения. Более высокие значения (например, 0.9) делают вывод более креативным, но могут отклоняться от исходного смысла — нежелательно для юридических или технических резюме.

## Шаг 4: **Как резюмировать PDF** – создать копилот и получить текст

Когда клиент и параметры готовы, создайте копилот резюме. Этот объект оркестрирует запрос к OpenAI и возвращает результат в нескольких форматах.

```csharp
    // ---- Step 4: instantiate the summary copilot (how to summarize PDF) ----
    var summaryCopilot = AICopilotFactory
        .CreateSummaryCopilot(client, summaryOptions);

    // Retrieve the generated summary as plain text
    string summaryText = await summaryCopilot.GetSummaryAsync();

    Console.WriteLine("=== Text Summary ===");
    Console.WriteLine(summaryText);
```

Метод `GetSummaryAsync` возвращает чистый текст без разметки, который можно встроить в UI, отправить по электронной почте или сохранить в базе данных.

## Шаг 5: Получить резюме в виде PDF‑документа

Если нужен портативный, печатаемый вариант, попросите копилот сгенерировать PDF‑документ. Этот шаг демонстрирует **генерацию PDF‑резюме** напрямую из модели ИИ.

```csharp
    // ---- Step 5: retrieve the summary as a PDF document (generate PDF summary) ----
    Document summaryDocument = await summaryCopilot.GetSummaryDocumentAsync();

    // Optionally, you can add a cover page or watermark here before saving.
```

Возвращаемый объект `Aspose.Pdf.Document` ведёт себя как любой другой PDF‑объект в экосистеме Aspose, что позволяет дальше редактировать страницы, добавлять метаданные или объединять с другими PDF‑файлами.

## Шаг 6: **Как сохранить резюме** – записать PDF на диск

Наконец, сохраните сгенерированное резюме в файловой системе. Вспомогательный метод `SaveSummaryAsync` объединяет получение и сохранение в один вызов, но мы также покажем явное сохранение для полноты картины.

```csharp
    // ---- Step 6: save the summary PDF (how to save summary) ----
    const string outputPath = "YOUR_DIRECTORY/Summary_out.pdf";

    // Direct helper method
    await summaryCopilot.SaveSummaryAsync(outputPath);

    // Or, save the Document object manually
    // summaryDocument.Save(outputPath);
    Console.WriteLine($"Summary PDF saved to: {outputPath}");
}
```

> **Подсказка:** Если необходимо соблюдать схему именования (например, файлы с меткой времени), сформируйте путь программно с помощью `DateTime.UtcNow:yyyyMMdd_HHmmss`.

### Полный рабочий пример

Объединив всё вместе, получаем автономную программу, которую можно скопировать в `Program.cs` и запустить:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // Create OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // Configure summary options (convert PDF to summary)
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

        // Instantiate the copilot (how to summarize PDF)
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // Get plain‑text summary
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Text Summary ===");
        Console.WriteLine(summaryText);

        // Get PDF version (generate PDF summary)
        Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // Save the PDF (how to save summary)
        const string outPath = "YOUR_DIRECTORY/Summary_out.pdf";
        await summaryCopilot.SaveSummaryAsync(outPath);
        Console.WriteLine($"Summary PDF saved to: {outPath}");
    }
}
```

Запуск программы создаёт два артефакта:

1. **Вывод в консоль** – текстовое резюме, отображаемое на экране.
2. **`Summary_out.pdf`** – загружаемый PDF, содержащий то же резюме, готовый к распространению.

## Распространённые варианты и граничные случаи

| Ситуация | Рекомендованное изменение |
|-----------|-------------------|
| **Большие PDF (> 10 MB)** | Разбейте документ на более мелкие части (например, по главам) и резюмируйте каждую часть отдельно. Объедините результаты с помощью `Document.AppendDocument`. |
| **Необходим пользовательский запрос** | Используйте `WithPrompt("Summarize the following legal contract in bullet points:")` перед вызовом `CreateSummaryCopilot`. |
| **PDF на неанглийском языке** | Установите `WithLanguage("es")` (или соответствующий ISO‑код), чтобы направить модель на обработку нужного языка. |
| **Ошибки ограничения скорости** | Увеличьте `WithRetryCount` или добавьте `Task.Delay` между вызовами. |
| **Сохранение в облачное хранилище** | Замените путь к файловой системе на поток (`MemoryStream`) и загрузите его в Azure Blob Storage или AWS S3. |

## Проверка результата

После завершения программы откройте `Summary_out.pdf` в любом PDF‑просмотрщике. Вы должны увидеть чистый документ одной (или нескольких) страниц, который отражает основные идеи `SampleDocument.pdf`. Сравните текстовое резюме, выведенное в консоль, с версией в PDF — оба должны совпадать дословно.

Если резюме выглядит неполным:

1. Понизьте `WithTemperature` до 0.2 для более детерминированного вывода.
2. Увеличьте ...

## Что изучать дальше?

Следующие учебники охватывают смежные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающие освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Learn How to Generate PDF Documents with Aspose.PDF for .NET](/pdf/english/net/document-creation/)
- [How to Create Tagged PDFs with Aspose.PDF for .NET – Enhance Accessibility](/pdf/english/net/bookmarks-navigation/tagged-pdf-creation-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}