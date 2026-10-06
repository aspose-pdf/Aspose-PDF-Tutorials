---
category: general
date: 2026-03-24
description: Добавьте нумерацию Бейтса в PDF с помощью Aspose.Pdf на C#. Узнайте,
  как добавить новую страницу в PDF, применить номер Бейтса и эффективно обновлять
  нумерацию Бейтса.
draft: false
keywords:
- add bates numbering pdf
- add new page pdf
- apply bates number
- create pdf aspose
- update bates numbering
language: ru
og_description: Быстро добавьте нумерацию Бейтса в PDF. Это руководство показывает,
  как добавить новую страницу в PDF, применить номер Бейтса и обновить нумерацию Бейтса
  с помощью Aspose.Pdf.
og_title: Добавление нумерации Бейтса в PDF с помощью Aspose – Полное руководство
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Добавление нумерации Бейтса в PDF с помощью Aspose – Полное руководство
url: /ru/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление нумерации Бейтса в PDF с Aspose – Полное руководство

Когда‑то вам нужно было **добавить нумерацию Бейтса в PDF**‑файлы, но вы не знали, с чего начать? Вы не одиноки — юридические отделы, аудиторы и все, кто работает с большими пакетами документов, сталкиваются с этой задачей регулярно. Хорошая новость: с Aspose.Pdf для .NET это можно сделать в паре строк кода, и вы даже узнаете, как **добавить новую страницу PDF**, **применить номер Бейтса** и **обновить нумерацию Бейтса** позже.

В этом руководстве мы пройдем реальный сценарий: у вас есть исходный PDF, вы хотите вставить штамп Бейтса на новую страницу, а позже, возможно, перенумеровать весь документ. К концу вы сможете **создавать решения pdf aspose**, готовые к продакшну, и поймете, почему каждый шаг важен.

## Что вы получите

- Загрузите существующий PDF с помощью Aspose.Pdf.
- **Добавите новую страницу PDF** для штампа Бейтса.
- **Примените номер Бейтса** с помощью `TextStamp`.
- (Опционально) **Обновите нумерацию Бейтса** на всех страницах.
- Полный, готовый к запуску пример на C#, который можно вставить в любой .NET‑проект.

### Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).
- NuGet‑пакет Aspose.Pdf для .NET (`Install-Package Aspose.Pdf`).
- Исходный PDF‑файл (`source.pdf`), размещённый в известной папке.

Никакой сложной конфигурации не требуется — только библиотека и PDF для экспериментов.

![Пример добавления нумерации Бейтса в PDF](https://example.com/placeholder.png "Схема, показывающая добавление нумерации Бейтса на страницу PDF")

## Шаг 1 – Загрузка исходного PDF (Основа)

Прежде чем **добавить нумерацию Бейтса в PDF**, нужен объект документа. Представьте `Document` как холст; без него штамп поставить нельзя.

```csharp
using Aspose.Pdf;

// Load the existing PDF – replace the path with your actual file location
using var pdfDocument = new Document(@"C:\MyPdfs\source.pdf");

// Verify the document was loaded (optional but handy for debugging)
Console.WriteLine($"Document loaded: {pdfDocument.Pages.Count} pages found.");
```

*Почему это важно:* Загрузка файла даёт доступ к коллекции страниц, метаданным и настройкам безопасности. Если файл повреждён, Aspose бросит информативное исключение, избавив вас от тихих ошибок позже.

## Шаг 2 – **Добавить новую страницу PDF** для штампа Бейтса

Зачем помещать штамп на совершенно новую страницу? Во многих юридических процессах номер Бейтса размещают на отдельной титульной странице, чтобы оригинальное содержание осталось нетронутым. Добавить страницу в Aspose — это однострочник.

```csharp
// Create a fresh page at the end of the document
var newPage = pdfDocument.Pages.Add();

// Quick sanity check – print the new total page count
Console.WriteLine($"New page added. Total pages: {pdfDocument.Pages.Count}");
```

*Совет профессионала:* Если нужен штамп на каждой странице, можно пропустить добавление новой страницы и пройтись по `pdfDocument.Pages`. Здесь мы сознательно **добавляем новую страницу PDF**, чтобы продемонстрировать типичный шаблон «обложки».

## Шаг 3 – **Применить номер Бейтса** с помощью TextStamp

Сердце операции — `TextStamp`. Он позволяет точно позиционировать текст, задавать отступы и оформлять внешний вид.

```csharp
// Create a TextStamp that holds the Bates number
var batesStamp = new TextStamp("Bates: 001")
{
    // Align the stamp to the bottom‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    
    // Margin values are in points (1 point = 1/72 inch)
    Margin = new Margin(0, 0, 20, 20) // left, bottom, right, top
};

// Attach the stamp to the newly created page
newPage.AddStamp(batesStamp);
```

*Почему выбраны эти настройки:* Размещение в правом нижнем углу соответствует требованиям большинства судов. Отступ в 20 пунктов удерживает текст от края страницы, избегая обрезки принтером. Вместо строки `"Bates: 001"` можно подставить переменную, если нужны последовательные номера.

## Шаг 4 – Сохранение обновлённого PDF

Сохранить просто, но, возможно, вы захотите оставить оригинальный файл нетронутым. Запишем в новое место.

```csharp
string outputPath = @"C:\MyPdfs\output_with_bates.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved with Bates stamp at: {outputPath}");
```

На этом этапе вы успешно **добавили нумерацию Бейтса в PDF** документа и **добавили новую страницу PDF** для её размещения. Откройте файл в любом просмотрщике — штамп будет аккуратно расположен в правом нижнем углу последней страницы.

## Шаг 5 – (Опционально) **Обновить нумерацию Бейтса** на всех страницах

Что если позже понадобится вставить штампы на другие страницы? Aspose предоставляет вспомогательный метод, который автоматически увеличивает номер на каждой странице, избавляя от ручного формирования строк.

```csharp
// This will renumber all pages using the same stamp format
pdfDocument.Pages.UpdateBatesNumbering();
pdfDocument.Save(@"C:\MyPdfs\output_renumbered.pdf");
Console.WriteLine("All pages have been renumbered.");
```

*Когда использовать:* Идеально для больших пакетов, где каждой странице нужен уникальный идентификатор. Метод сохраняет исходные свойства `TextStamp`, поэтому выравнивание и отступы остаются одинаковыми.

## Полный рабочий пример – от начала до конца

Ниже полная программа, которую можно скопировать в консольное приложение. В ней собраны все шаги, обработка ошибок и комментарии.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path to the source PDF – adjust as needed
        const string sourcePath = @"C:\MyPdfs\source.pdf";
        const string resultPath = @"C:\MyPdfs\output_with_bates.pdf";

        try
        {
            // 1️⃣ Load the existing PDF
            using var pdfDocument = new Document(sourcePath);
            Console.WriteLine($"Loaded PDF with {pdfDocument.Pages.Count} pages.");

            // 2️⃣ Add a new blank page for the Bates stamp
            var newPage = pdfDocument.Pages.Add();
            Console.WriteLine($"Added new page. Total pages now: {pdfDocument.Pages.Count}");

            // 3️⃣ Create and configure the Bates TextStamp
            var batesStamp = new TextStamp("Bates: 001")
            {
                HorizontalAlignment = HorizontalAlignment.Right,
                VerticalAlignment   = VerticalAlignment.Bottom,
                Margin = new Margin(0, 0, 20, 20) // left, bottom, right, top
            };

            // 4️⃣ Place the stamp on the newly added page
            newPage.AddStamp(batesStamp);
            Console.WriteLine("Bates stamp applied to the new page.");

            // 5️⃣ Save the modified PDF
            pdfDocument.Save(resultPath);
            Console.WriteLine($"PDF saved successfully at {resultPath}");

            // Optional: Renumber all pages if you add more stamps later
            // pdfDocument.Pages.UpdateBatesNumbering();
            // pdfDocument.Save(@"C:\MyPdfs\output_renumbered.pdf");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Ожидаемый результат:** При открытии `output_with_bates.pdf` оригинальное содержание останется без изменений, появится новая последняя страница, а текст «Bates: 001» будет расположен в правом нижнем углу. Если раскомментировать строку `UpdateBatesNumbering`, каждая страница получит свой последовательный номер.

## Часто задаваемые вопросы и особые случаи

- **Можно ли изменить шрифт или цвет?**  
  Конечно. `TextStamp` наследуется от `Stamp`, поэтому можно задать `Font`, `FontSize`, `Color` и т.д. Пример: `batesStamp.Font = FontRepository.FindFont("Arial"); batesStamp.FontSize = 12; batesStamp.TextColor = Color.Red;`.

- **Что если мой PDF защищён паролем?**  
  Загружайте его с паролем: `new Document(sourcePath, new LoadOptions { Password = "mySecret" })`.

- **Нужно ли явно освобождать `Document`?**  
  При использовании конструкции `using` (как показано) объект освобождается автоматически, закрывая файловые дескрипторы.

- **В каких единицах измеряется отступ — пункты или пиксели?**  
  Пункты. Один пункт = 1/72 дюйма, это стандартная единица измерения в PDF.

- **Можно ли разместить штамп на первой странице вместо новой?**  
  Да — замените `newPage` на `pdfDocument.Pages[1]` (страницы нумеруются с 1).

## Заключение

Теперь у вас есть чёткий, сквозной рецепт **добавления нумерации Бейтса в PDF** с помощью Aspose.Pdf, включая как **добавить новую страницу PDF**, **применить номер Бейтса**, так и **обновить нумерацию Бейтса**, когда документ растёт. Код готов к вставке в любой C#‑проект, а пояснения помогут адаптировать его под собственные макеты, шрифты или пакетную обработку.

### Что дальше?

- Углубитесь в **create pdf aspose**, добавляя изображения, таблицы или цифровые подписи.  
- Автоматизируйте пакетную обработку: пройдитесь по папке с PDF‑файлами и проставьте штамп в каждом.  
- Исследуйте функции соответствия PDF/A в Aspose, если нужны архивируемые документы.

Попробуйте, поиграйте с выравниванием, экспериментируйте с разными текстами штампа, и позвольте библиотеке выполнить тяжёлую работу. Если возникнут проблемы, форумы сообщества Aspose — отличное место для вопросов. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}