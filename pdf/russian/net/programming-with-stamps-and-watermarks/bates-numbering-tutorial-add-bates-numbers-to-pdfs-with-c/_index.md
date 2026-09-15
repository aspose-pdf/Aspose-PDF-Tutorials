---
category: general
date: 2026-02-25
description: Учебник по нумерации Бейтса — узнайте, как добавить номера страниц в
  PDF и применить пользовательскую нумерацию Бейтса с помощью Aspose.Pdf на C#. Пошаговое
  руководство с полным кодом.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: ru
og_description: Учебник по нумерации Бейтса показывает, как добавить номера страниц
  в PDF и пользовательскую нумерацию Бейтса на C#. Полный код, объяснения и советы.
og_title: Учебник по нумерации Бейтса – Добавьте номера Бейтса в PDF с помощью C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Учебник по нумерации Бейтса: добавление номеров Бейтса в PDF с помощью C#'
url: /ru/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Руководство по нумерации Бейтса – Добавление номеров Бейтса в PDF на C#

Задумывались когда‑нибудь, как добавить номера страниц в PDF, одновременно внедрив юридический номер Бейтса? Вы не одиноки. В этом **bates numbering tutorial** мы пройдемся по всему, что нужно знать, чтобы поставить штамп на каждую страницу PDF с пользовательским префиксом, ведущими нулями и точным позиционированием — используя Aspose.Pdf for .NET.

Хорошая новость? Это довольно просто, как только вы поймёте основные концепции. К концу этого руководства у вас будет исполняемая программа, которая берёт *input.pdf* и выдаёт *bates_out.pdf* с аккуратной меткой в стиле “ABC‑01000” на каждой странице. Давайте начнём.

## Что понадобится

- **Aspose.Pdf for .NET** (версия 23.10 или новее). Библиотека коммерческая, но бесплатный пробный период отлично подходит для обучения.
- .NET 6+ SDK (любая современная версия подойдет).
- Базовая среда разработки C# — Visual Studio, VS Code или Rider.
- PDF‑файл для экспериментов (любой многостраничный документ продемонстрирует эффект).

Дополнительные пакеты NuGet, помимо Aspose.Pdf, не требуются, и код работает на Windows, Linux или macOS без изменений.

## Шаг 1: Загрузка исходного PDF‑документа (bates numbering tutorial – initialization)

Сначала мы создаём объект `Document`, представляющий PDF, который нужно изменить. Представьте его как загрузку пустого холста, на котором можно рисовать.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Почему это важно:** Без загрузки файла нечего аннотировать. Проверка на корректность предотвращает тихий сбой позже, когда вы пытаетесь добавить артефакты в несуществующую коллекцию страниц.

## Шаг 2: Определение артефакта нумерации Бейтса (how to add bates)

*BatesNumberingArtifact* указывает Aspose, где и как нарисовать идентификатор. Вы можете управлять префиксом, начальным номером, заполнением нулями, размером шрифта и точными координатами X/Y.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Почему это важно:** Свойство `LeadingZeros` гарантирует, что каждая метка имеет одинаковую длину, что критично для юридических документов, где важна выравненность. Отрегулируйте `X` и `Y`, чтобы переместить штамп в правый верхний, левый нижний угол или куда требует ваш процесс.

## Шаг 3: Присоединение артефакта к каждой странице (add page numbers pdf)

Теперь мы проходим по каждой странице и присоединяем тот же артефакт. Здесь реализуется требование *add page numbers pdf* — каждая страница автоматически получает свою последовательную метку.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Почему это важно:** Добавляя артефакт в коллекцию `Artifacts`, а не рисуя текст вручную, мы позволяем Aspose управлять логикой нумерации, ведущими нулями и рендерингом. Это уменьшает количество ошибок и делает код лаконичным.

## Шаг 4: Сохранение изменённого PDF (add bates numbering)

Наконец, мы сохраняем изменения в новый файл. Хорошая привычка — записывать в другое имя файла, чтобы оригинал остался нетронутым.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Почему это важно:** Метод `Save` записывает весь PDF, внедряя артефакты как часть потока содержимого страницы. Полученный файл можно открыть в любом PDF‑просмотрщике, и он отобразит номера Бейтса точно так, как указано.

## Полный рабочий пример (Все шаги вместе)

Ниже представлен полный готовый к запуску пример программы. Скопируйте‑вставьте его в проект консольного приложения, замените пути‑заполнители и нажмите **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Ожидаемый результат

Откройте *bates_out.pdf* в Adobe Reader, Foxit или любом другом просмотрщике. Вы должны увидеть метку вроде **ABC‑01000** на первой странице, **ABC‑01001** на второй и т.д., расположенную на 50 pt от левого края и 30 pt от нижнего. Числа выровнены по правому краю благодаря ведущим нулям, что придаёт документу чистый, профессиональный вид.

## Общие варианты и граничные случаи

| Сценарий | Как изменить |
|----------|---------------|
| **Другой префикс** | Измените `Prefix = "XYZ"` в определении артефакта. |
| **Начать с пользовательского номера** | Установите `Start = 5000` (или любое целое число). |
| **Разместить номер в правом верхнем углу** | Используйте `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Изменить размер шрифта для больших документов** | Измените `FontSize = 12` (или любой размер). |
| **Добавить фон в виде прямоугольника** | Создайте `RectangleArtifact` и добавьте его перед `BatesNumberingArtifact`. |
| **Пропустить определённые страницы** | Внутри цикла `foreach` добавьте `if (page.Number % 2 == 0) continue;` чтобы пропустить чётные страницы. |

**Совет:** Всегда сначала тестируйте на коротком PDF. Так быстрее проверить позиционирование, прежде чем запускать скрипт на 200‑страничном деле.

## Часто задаваемые вопросы

- **Работает ли это с зашифрованными PDF?**  
  Aspose.Pdf может открывать файлы, защищённые паролем, если передать пароль через `Document(string, string)`. Артефакт Бейтса всё равно будет применён после расшифровки.

- **Можно ли добавить одновременно номера Бейтса и обычные номера страниц?**  
  Да. Добавьте `PageNumberArtifact` рядом с `BatesNumberingArtifact`. Каждый артефакт ведёт собственный счётчик.

- **Что если мой PDF имеет разные размеры страниц?**  
  Значения `Position` задаются в абсолютных точках. Для документов со смешанными размерами вычисляйте позицию для каждой страницы внутри цикла, используя `page.PageInfo.Width` и `page.PageInfo.Height`.

## Следующие шаги и связанные темы

Теперь, когда вы освоили **bates numbering tutorial**, вы можете изучить:

- **Добавление водяных знаков** — аналогичный подход с артефактами через `TextArtifact`.
- **Объединение нескольких PDF** — используйте `Document.AppendDocument`.
- **Извлечение текста для индексации поиска** — класс `TextAbsorber`.
- **Автоматизация пакетной обработки** — переберите папку с PDF и примените тот же артефакт.

Все эти темы опираются на те же концепции, которые вы только что изучили, поэтому вы хорошо подготовлены к расширению своего набора инструментов для автоматизации PDF.

*Счастливого кодинга! Если столкнётесь с проблемами или у вас есть идеи для дальнейшей кастомизации, смело оставляйте комментарий ниже. Мир манипуляций с PDF огромен, но имея прочное **bates numbering tutorial** в арсенале, вы уже опережаете остальных.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}