---
category: general
date: 2026-08-04
description: Как использовать Aspose для извлечения текста из отсканированных PDF
  и преобразования PDF в текст с помощью C#. Узнайте, как читать отсканированные PDF‑файлы
  и получать надёжные результаты OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: ru
lastmod: 2026-08-04
og_description: Как использовать Aspose для чтения отсканированных PDF‑файлов, извлечения
  текста из отсканированных PDF и конвертации PDF в текст с полным, готовым к запуску
  примером.
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Как использовать Aspose – извлекать текст из отсканированных PDF в C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: Как использовать Aspose для извлечения текста из отсканированного PDF – пошаговое
  руководство
url: /ru/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать Aspose для извлечения текста из отсканированного PDF – пошаговое руководство

Если вам нужно **как использовать Aspose** для OCR, это руководство покажет, как извлечь текст из отсканированного PDF за несколько строк кода на C#. Независимо от того, создаёте ли вы сервис архивирования документов или поисковый индекс для устаревших бумаг, решение работает с любым отсканированным PDF, который вы передаёте сервису Aspose.Pdf.AI.

В этом учебнике вы:

* Создадите OCR‑копилот, который читает отсканированный PDF.
* Асинхронно извлечёте распознанный текст.
* Отобразите или дальше обработаете полученную строку.

Единственное требование — активная подписка Aspose.Pdf.AI и среда разработки .NET 6 (или новее).

## Требования

| Требование | Почему это важно |
|-------------|----------------|
| .NET 6 SDK или новее | Предоставляет `async Main` и современные возможности языка. |
| NuGet‑пакет Aspose.Pdf.AI (`Aspose.Pdf.AI`) | Содержит `AICopilotFactory` и параметры OCR. |
| Действительный экземпляр Aspose.Pdf.AI `client` (API‑ключ) | Аутентифицирует ваши запросы к облачному сервису. |
| Отсканированный PDF‑файл (например, `Scanned.pdf`) | Исходный документ, из которого будет извлечён текст. |

Установите пакет с помощью .NET CLI:

```bash
dotnet add package Aspose.Pdf.AI
```

## Шаг 1: Настройка клиента Aspose.Pdf.AI

Прежде чем вы сможете вызвать любой OCR‑эндпоинт, необходимо создать клиент, содержащий ваши учётные данные API. Клиент потокобезопасен и может использоваться повторно для нескольких документов.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**Почему этот шаг необходим** – Сервис Aspose проверяет каждый запрос в соответствии с вашей подпиской. Создание клиента один раз избавляет от повторных сетевых рукопожатий и делает код чище.

## Шаг 2: Создание OCR‑копилота для отсканированного PDF‑документа

`AICopilotFactory` создаёт специализированный OCR‑копилот, который знает, как обрабатывать указанный файл. Вы передаёте `client` и объект `OpenAIOcrOptions`, указывающий путь к PDF.

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Объяснение** – `CreateOcrCopilot` инкапсулирует все низкоуровневые HTTP‑вызовы. Метод `WithDocument` сообщает сервису, какой файл анализировать; при необходимости можно передать `Stream`, если PDF находится в памяти.

## Шаг 3: Асинхронное извлечение распознанного текста

Вызов `GetTextAsync` запускает OCR‑операцию в облаке и возвращает результат в виде простого текста. Поскольку операция может занимать несколько секунд, метод асинхронный.

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Почему асинхронно?** – Сетевые задержки и время обработки OCR непредсказуемы. Использование `await` предотвращает блокировку главного потока вашего приложения, что особенно важно для UI‑приложений или веб‑сервисов.

## Шаг 4: Использование извлечённого текста

На данном этапе у вас есть обычный .NET `string`, содержащий полную транскрипцию отсканированного PDF. Вы можете вывести его в консоль, сохранить в базе данных или передать в поисковый движок.

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### Ожидаемый вывод

Если `Scanned.pdf` содержит одну страницу с предложением «Hello, world!», консоль покажет:

```
=== OCR Result ===
Hello, world!
```

Для многостраничных документов вывод объединяет текст каждой страницы, сохраняя разрывы строк.

## Полный, готовый к запуску пример

Ниже приведена полная программа, которую можно вставить в новый консольный проект (`dotnet new console`). Она демонстрирует **как использовать Aspose** от начала до конца, включая обработку ошибок, типичных для подобных сценариев.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**Ключевые моменты примера**

* `await` обеспечивает неблокирующее выполнение.
* Блок `try/catch` выводит сетевые или сервисные ошибки, что критично при **чтении отсканированных PDF** файлов в масштабе.
* Замените `YOUR_API_KEY` и `YOUR_DIRECTORY/Scanned.pdf` реальными значениями перед запуском.

## Обработка граничных случаев и рекомендации по лучшим практикам

| Ситуация | Рекомендуемый подход |
|-----------|----------------------|
| **Большие PDF ( > 50 MB )** | Разбейте документ на более мелкие части на клиенте и обрабатывайте каждую часть отдельным копилотом. Это уменьшит нагрузку на память и повысит надёжность. |
| **Низкокачественные сканы** | Улучшите качество OCR, добавив `.WithLanguage("eng")` или `.WithEnhanceImage(true)` к `OpenAIOcrOptions`. Сервис поддерживает подсказки языка, повышающие точность. |
| **Несколько языков** | Укажите список через запятую, например `.WithLanguage("eng,spa")`. OCR‑движок обнаружит и транскрибирует оба языка. |
| **Не‑PDF изображения** | Сначала преобразуйте изображение в PDF (библиотека `Aspose.Pdf`) или используйте `OpenAIOcrOptions.WithImage` для отправки изображения напрямую. |
| **Превышен лимит запросов** | Реализуйте экспоненциальную задержку и повторные попытки; Aspose API возвращает HTTP 429 при превышении квоты. |

### Профессиональный совет

Кешируйте результат `ocrText`, если планируете использовать его повторно. Операция OCR — самая затратная часть рабочего процесса, и повторное использование строки избавит от лишних вызовов API и сэкономит кредиты.

## Часто задаваемые вопросы

**В: Работает ли это с PDF, защищёнными паролем?**  
О: Да. Добавьте `.WithPassword("yourPassword")` к построителю параметров перед созданием копилота.

**В: Можно ли извлечь текст в структурированном формате (например, JSON с номерами страниц)?**  
О: Используйте `GetTextStructureAsync()` вместо `GetTextAsync()`. Метод возвращает JSON‑payload, включающий индексы страниц, ограничивающие рамки и оценки уверенности.

**В: Что делать, если PDF содержит таблицы?**  
О: Извлечение простого текста «сплющивает» таблицы в строки, разделённые переводами строки. Для более богатых данных запросите конвертацию PDF‑в‑HTML (`GetHtmlAsync`) и распарсите элементы HTML‑таблицы.

## Заключение

Теперь вы знаете **как использовать Aspose** для чтения отсканированного PDF, извлечения текста из отсканированного PDF и **конвертации PDF в текст** с помощью минимальной программы на C#. Процесс состоит из создания OCR‑копилота, вызова `GetTextAsync` и обработки полученной строки. Следуя рекомендациям по граничным случаям, вы сможете масштабировать решение для больших пакетов документов, многоязычного контента и защищённых PDF.

Далее вы можете изучить:

* **Как извлечь текст** с сохранением разметки (`GetHtmlAsync`).
* Использование Aspose.Pdf.AI для **извлечения таблиц** и экспорта их в CSV.
* Интеграцию вывода OCR с Azure Cognitive Search для поисковых архивов документов.

Приятного кодинга и наслаждайтесь точностью OCR на базе AI от Aspose в ваших рабочих процессах с отсканированными PDF!

## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Extract Text from PDF Files Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [How to Extract Text from Specific Regions in PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [How to Extract Highlighted Text from PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}