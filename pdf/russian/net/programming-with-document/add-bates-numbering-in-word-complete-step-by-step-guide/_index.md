---
category: general
date: 2026-06-21
description: Быстро добавляйте нумерацию Бейтса в Word. Узнайте, как добавить её,
  применять нумерацию Бейтса к юридическим документам и автоматизировать нумерацию
  с помощью C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: ru
og_description: Добавьте нумерацию Бейтса в Word с помощью C#. Это руководство показывает,
  как добавить нумерацию Бейтса, применить её к юридическим документам и автоматизировать
  процесс.
og_title: Добавление нумерации Бейтса в Word – Полный программный разбор
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Добавьте нумерацию Бейтса в Word – полное пошаговое руководство
url: /ru/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление Bates‑нумерации в Word – Полное пошаговое руководство

Задумывались ли вы когда‑нибудь, как добавить Bates‑нумерацию в файл Word без ручного ввода каждого номера? Вы не одиноки. Многие юристы, параюристы и специалисты по e‑discovery нуждаются в надёжном способе **add Bates numbering** к сотням страниц, а делать это вручную — настоящий кошмар.

В этом руководстве мы пройдём чистое C#‑решение, которое **applies Bates numbering** к файлу `.docx`, объяснит, почему важна каждая строка, и покажет, как настроить код под юридические нужды. К концу вы сможете за секунды создать идеально пронумерованный документ — без дополнительных плагинов.

## Что вы узнаете

- Точный код, необходимый для **add Bates numbering** в документ Word.  
- Как работает класс `BatesNumberingOptions` и почему вы можете изменить префикс или начальное значение.  
- Советы по использованию этого подхода для больших дел, включая соображения по памяти.  
- Краткий обзор предварительных требований, чтобы вы могли скопировать‑вставить решение и запустить его сегодня.

**Prerequisites**  
- .NET 6+ (или .NET Framework 4.7.2+, если вы предпочитаете более старый рантайм).  
- Ссылка на библиотеку Aspose.Words for .NET (или любой аналогичный API, предоставляющий `AddBatesNumbering`).  
- Базовое знакомство с C# и Visual Studio (или вашей любимой IDE).

Если вы с этим комфортно, давайте погрузимся.

## Шаг 1: Настройте проект и импортируйте библиотеку

Сначала создайте новое консольное приложение (или интегрируйте в существующий сервис). Затем добавьте пакет NuGet Aspose.Words:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Используйте бесплатную оценочную лицензию для тестирования; она добавляет небольшой водяной знак, но в остальном работает точно так же, как полная версия.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Эти директивы `using` импортируют классы `Document` и `BatesNumberingOptions` в область видимости, что необходимо для шага **apply bates numbering** позже.

## Шаг 2: Загрузите исходный документ

Вам понадобится файл Word для работы. Ниже приведён код, который загружает `input.docx` из указанной вами папки. Замените `"YOUR_DIRECTORY"` на фактический путь на вашем компьютере.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Зачем сначала загружать файл? Объект `Document` разбирает весь пакет Word в память, позволяя нам изменять колонтитулы и макеты страниц перед сохранением. Если файл огромный (например, 10 000 страниц), рассмотрите возможность использования `LoadOptions` с `LoadFormat.Docx` для потоковой загрузки разделов вместо полной загрузки.

## Шаг 3: Настройте параметры Bates‑нумерации

Здесь происходит магия. Вы указываете библиотеке, какой префикс использовать (`"ABC-"` в примере) и с какого номера начинать счёт (`1000`). Оба значения полностью настраиваемы.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Why a prefix?** В юридической практике префиксы часто идентифицируют дело или сторону‑производителя (`"ABC-"` может означать *Acme Bank Corp.*). Начало с `1000` распространено, поскольку многие фирмы резервируют первые 999 номеров для внутренних черновиков.

Если вы работаете с **Bates numbering for legal** документами, вы также можете установить `batesOptions.Position` в `Header` или `Footer` и скорректировать выравнивание в соответствии с правилами суда. Библиотека поддерживает эти настройки из коробки.

## Шаг 4: Примените Bates‑нумерацию ко всему документу

Теперь мы действительно вставляем номера. Метод `AddBatesNumbering` проходит по каждой странице, вставляет отформатированную строку и обновляет внутренний счёт страниц документа.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Внутри Aspose.Words создаёт скрытое поле на каждой странице, которое отображается как `ABC-1000`, `ABC-1001` и т.д. Поскольку это поле, вы позже можете изменить префикс или начальный номер без повторной генерации всего файла — удобно для **how to add bates** после изменения запроса на раскрытие.

## Шаг 5: Сохраните изменённый документ

Наконец, запишите результат в новый файл. Сохранение оригинала нетронутым — лучшая практика, особенно при работе с доказательствами, которые должны оставаться неизменными.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Теперь у вас есть `output.docx` с последовательными Bates‑номерами, добавленными к каждой странице. Откройте его в Word, и вы увидите номера точно там, где указали (по умолчанию в нижнем колонтитуле). Размер файла может немного увеличиться из‑за дополнительных полей, но это несущественно по сравнению с преимуществами.

### Ожидаемый вывод

| Page | Bates Number |
|------|--------------|
| 1    | ABC-1000     |
| 2    | ABC-1001     |
| …    | …            |
| N    | ABC‑(1000 + N‑1) |

Если открыть представление «Коды полей» документа (`Alt+F9` в Word), вы увидите что‑то вроде `{ BATES \* MERGEFORMAT ABC-1000 }` на каждой странице.

## Пограничные случаи и часто задаваемые вопросы

### Что если документ уже содержит номера страниц?

Метод `AddBatesNumbering` **не** перезапишет существующие поля номеров страниц; он просто добавит новое поле. Если вы хотите заменить существующие номера, сначала удалите их или установите `batesOptions.Position` в то же место, что и текущие номера страниц.

### Можно ли пропустить страницы (например, исключить титульный лист)?

Да. Используйте перегрузку, принимающую `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Это полезно, когда вам нужна **bates numbering for legal** справка, начинающаяся после титульной страницы.

### Как изменить формат нумерации (римские цифры, буквы)?

Класс `BatesNumberingOptions` поддерживает свойство `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Установите его перед вызовом `AddBatesNumbering`. Эта гибкость помогает, когда суд требует определённый стиль.

### Что насчёт производительности при работе с огромными файлами?

Загрузка Word‑файла размером 2 ГБ может потребовать много ОЗУ. Чтобы смягчить это, обрабатывайте документ частями, используя утилиту `DocumentSplitter`, применяйте Bates‑нумерацию к каждой части, а затем объединяйте их обратно. Такой подход удерживает использование памяти под контролем, одновременно позволяя **apply bates numbering** эффективно.

## Полный рабочий пример

Объединив всё вместе, вот готовая к запуску консольная программа:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Запустите программу, откройте `output.docx`, и вы увидите чистую последовательность номеров, готовую к подаче, раскрытию или представлению в суд.

## Заключение

Теперь вы точно знаете **how to add Bates** в документ Word с помощью C#. Шаги — загрузка, настройка, применение и сохранение — просты, но достаточно гибки, чтобы удовлетворить **Bates numbering for legal** рабочие процессы, пользовательские префиксы и даже масштабную пакетную обработку.

Если вы готовы пойти дальше, рассмотрите:

- Интеграцию кода в веб‑API, чтобы коллеги могли загружать файлы и мгновенно получать пронумерованные PDF.  
- Добавление обработки ошибок для отсутствующих файлов или проблем с правами доступа (быстрый `try/catch` вокруг `Document.Load`).  
- Изучение других возможностей Aspose.Words, таких как водяные знаки или редактирование, для полного набора инструментов e‑discovery.

Не стесняйтесь экспериментировать с разными префиксами, начальными номерами или даже комбинировать несколько схем нумерации в одном документе. Мир **apply bates numbering** удивительно гибок, как только у вас под контролем основная логика.

Есть вопросы или сложный сценарий? Оставьте комментарий ниже, и мы разберёмся вместе. Счастливого кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}