---
category: general
date: 2026-08-04
description: Создайте AI Copilot для генерации описаний изображений в PDF‑файлах.
  Узнайте, как настроить параметры изображений OpenAI и эффективно извлекать их описания.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: ru
lastmod: 2026-08-04
og_description: Создайте AI Copilot для генерации описания изображений в PDF‑файлах.
  Этот учебник покажет, как настроить параметры изображений OpenAI, запустить копилот
  и извлечь описание изображения на C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Создайте AI‑копилот для описания изображений в PDF — полное руководство
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: Создайте AI‑копилот для описания изображений в PDF — пошаговое руководство
url: /ru/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создайте AI Copilot для описания изображений PDF – полное руководство

Если вам нужно **создать AI Copilot**, который автоматически пишет описания для изображений, встроенных в PDF, это руководство покажет, как это сделать. Вы узнаете, как настроить параметры изображения OpenAI, запустить copilot и **извлечь описание изображения** без выхода из вашего проекта C#.

Генерация текстового контента для изображений в PDF часто требуется для доступности, индексации контента и автоматической отчетности. К концу этого урока у вас будет переиспользуемый компонент, который **генерирует описание изображения** для любого PDF‑документа, который вы укажете.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

* .NET 6.0 или более поздняя версия, установленная  
* Лицензия Aspose.Pdf.AI (или бесплатная пробная версия)  
* Ключ API OpenAI, который может использовать клиент Aspose  
* Visual Studio 2022 (или любая IDE, поддерживающая C#)  

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Pdf.AI`.

## Шаг 1: Настройте клиент Aspose.Pdf.AI

Первый шаг – создать клиент AI с вашими данными аутентификации. Клиент обрабатывает связь с сервисом OpenAI «за кулисами».

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Почему это важно:** `AiClient` инкапсулирует все настройки уровня запроса (ключ API, тайм‑аут, политика повторов). Создание его один раз и повторное использование в разных экземплярах copilot уменьшает нагрузку и обеспечивает единообразную аутентификацию.

## Шаг 2: Создайте copilot для описания изображений

Теперь вы создаёте **AI copilot**, который будет читать PDF и генерировать описание для каждого изображения. Фабричный метод `CreateImageDescriptionCopilot` принимает клиент и набор параметров, определяющих, как будет генерироваться описание.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Почему это важно:**  
* `OpenAIImageDescriptionOptions` ( **параметры изображения OpenAI**) позволяют точно настроить языковую модель. Регулировка temperature или модели может улучшить релевантность для технических схем против естественных фотографий.  
* Указание пути к документу сообщает copilot, какой PDF сканировать. Copilot извлекает каждое растровое изображение, отправляет его модели и возвращает читаемое человеком описание.

## Шаг 3: Асинхронно получить сгенерированное описание

Copilot работает асинхронно, потому что может потребоваться загрузить несколько мегабайт данных изображения и ждать ответа модели. Используйте `await`, чтобы гарантировать завершение вызова перед доступом к результату.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Почему это важно:** Метод возвращает `Dictionary<int, string>`, где каждому номеру страницы (или индексу изображения) сопоставлено описание. Обработка `AiException` позволяет отобразить сетевые ошибки или ошибки квоты вместо падения приложения.

## Шаг 4: Вывести или сохранить описание

Вы можете вывести описания в консоль, записать их в лог‑файл или внедрить обратно в PDF как alt‑text для доступности. Ниже простой пример, который сохраняет вывод в JSON‑файл для последующего использования.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Почему это важно:** Сохранение вывода в JSON сохраняет связь между каждой страницей и её описанием, что упрощает потребление данных downstream‑процессами (поисковая индексация, отображение в UI и т.д.).

## Обработка нескольких изображений на странице

Если на странице несколько изображений, copilot возвращает объединённое описание, разделённое переводами строк. Чтобы разделить их, проанализируйте сырый результат и разбейте по `\n\n` (двойной перевод строки). Вот вспомогательный метод:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Затем можно перебрать каждое отдельное описание изображения и при необходимости сохранить их отдельно.

## Пограничный случай: большие PDF и управление тайм‑аутом

Обработка PDF размером более 100 МБ может превысить стандартные HTTP‑тайм‑ауты. Отрегулируйте параметр тайм‑аута клиента при создании `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Увеличение тайм‑аута предотвращает преждевременное завершение, пока сервис обрабатывает множество изображений высокого разрешения.

## Профессиональный совет: кэшировать результаты для снижения затрат

OpenAI взимает плату за токен, а описания изображений могут повторяться в разных версиях одного и того же отчёта. Кэшируйте JSON‑вывод и переиспользуйте его, когда хеш PDF совпадает с ранее обработанным файлом. Такая практика экономит деньги и ускоряет последующие запуски.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Сохраняйте хеш рядом с JSON‑файлом; если хеш совпадает при следующем запуске, пропустите вызов AI.

## Полный исполняемый пример

Объединив всё вместе, получаем автономное консольное приложение, которое можно вставить в новый .NET‑проект.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Ожидаемый вывод (усечённый)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Программа читает `AnnualReport.pdf`, создаёт **AI copilot** и записывает JSON‑файл, сопоставляющий каждую страницу с её сгенерированным описанием.

## Часто задаваемые вопросы

* **Работает ли это с зашифрованными PDF?**  
  Да, но необходимо передать пароль при создании copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Можно ли ограничить обработку определёнными страницами?**  
  Используйте `imageOptions.WithPageRange(1, 10)`, чтобы ограничить copilot страницами 1‑10.

* **Что если изображение содержит текст?**  
  Модель пытается описать визуальное содержание; для извлечения текста в стиле OCR следует использовать `CreateTextExtractionCopilot`.

## Заключение

Теперь вы знаете, как **создать AI Copilot**, который **генерирует описание изображения** для PDF‑файлов, настроить **параметры изображения OpenAI** и **программно извлекать описание изображения** в C#. Полный пример демонстрирует лучшие практики, такие как асинхронная обработка, управление ошибками и кэширование результатов.

Далее вы можете изучить:

* Добавление сгенерированных описаний обратно в PDF как alt‑text для улучшения доступности (`PdfDocument` → `PdfImage.AlternativeText`).  
* Использование того же паттерна copilot для **генерации PDF‑отчётов с описаниями изображений** при пакетной обработке.  
* Эксперименты с различными моделями OpenAI или настройками temperature для тонкой настройки стиля описания.

Не стесняйтесь адаптировать код, экспериментировать с большими документами и интегрировать вывод в ваш конвейер индексации. Приятного кодинга!

## Что изучать дальше?

Следующие уроки охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Создать PDF с помеченным изображением на Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Создать PDF с помеченным изображением](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Создать помеченное изображение PDF в .NET](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}