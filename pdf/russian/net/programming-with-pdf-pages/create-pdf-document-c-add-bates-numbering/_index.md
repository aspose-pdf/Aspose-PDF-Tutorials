---
category: general
date: 2026-03-03
description: Создайте PDF‑документ на C# с нумерацией Бейтса — узнайте, как добавить
  номера Бейтса, добавить последовательные номера страниц и сгенерировать нумерацию
  Бейтса за несколько шагов.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: ru
og_description: Создайте PDF‑документ на C# с нумерацией Бейтса. Это руководство показывает,
  как добавить нумерацию Бейтса, добавить последовательные номера страниц и быстро
  сгенерировать нумерацию Бейтса.
og_title: Создать PDF‑документ на C# – добавить нумерацию Бейтса
tags:
- C#
- PDF
- Bates numbering
title: Создание PDF‑документа на C# – Добавление нумерации Бейтса
url: /ru/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF‑документа C# – Добавление нумерации Бейтса

Когда‑то вам нужно **создать PDF‑документ C#**, а затем пометить каждую страницу уникальным идентификатором для юридических или архивных целей? Вы не одиноки — юридические фирмы, суды и крупные корпорации постоянно задают вопрос: «Как автоматически добавить нумерацию Бейтса в мои PDF‑файлы?» Хорошая новость в том, что несколькими строками кода можно сгенерировать PDF, нанести нумерацию Бейтса на каждую страницу и сохранить результат, не открывая редактор.

В этом руководстве мы пройдем практический, сквозной пример, показывающий **как добавить Бейтс**, как **добавить последовательную нумерацию страниц**, а также как **сгенерировать Бейтс** с пользовательскими префиксами. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой .NET‑проект.

## Что понадобится

- **.NET 6+** (код также работает на .NET Framework 4.6+)
- **Aspose.Pdf for .NET** — коммерческая библиотека с чистым API для работы с PDF. Бесплатная оценочная версия подходит для тестов.
- Базовые знания C# (вы, вероятно, уже уверенно используете `using`‑операторы и объекты).

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Pdf`. Если вы ещё не установили её, выполните:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Держите вашу версию Aspose в актуальном состоянии; в последнем релизе 23.x добавлены оптимизации производительности для больших документов.

## Шаг 1: Открыть (или создать) исходный PDF‑документ

Сначала нам нужен PDF‑файл. В реальных сценариях у вас уже есть входной файл — например, отсканированный контракт. Для примера откроем существующий файл `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Почему это важно:** Открытие документа внутри блока `using` гарантирует своевременное освобождение файлового дескриптора, что предотвращает блокировку файла при последующей попытке перезаписать его.

## Шаг 2: Определить параметры нумерации Бейтса

Нумерация Бейтса состоит из **префикса** (часто идентификатор дела) и **начального номера**. Также можно задать количество цифр, расположение на странице и стиль шрифта. Здесь мы используем ключевое слово **add bates numbering pdf**, настраивая объект `BatesNumberingOptions`.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **Как добавить bates:** Изменяя свойства `Prefix` и `Start`, вы задаёте точную строку, которая будет отображаться на каждой странице. Свойство `NumberOfDigits` обеспечивает одинаковую ширину, что удобно для юридических подач.

## Шаг 3: Применить нумерацию Бейтса ко всем страницам

Теперь основная операция — добавление номеров. Метод `AddBatesNumbering` проходит по каждой странице, рисует текст и учитывает заданные параметры.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Внутри Aspose рендерит текст как элемент *content*, то есть номера становятся частью PDF и не могут быть отключены в просмотрщике. Это именно то, что нужно, когда вы хотите **add sequential page numbers**, которые нельзя изменить.

### Пограничные случаи и варианты

- **Несколько префиксов:** Если нужны разные префиксы для разных разделов, создайте отдельные `BatesNumberingOptions` и вызовите `AddBatesNumbering` для диапазона страниц (`pdfDocument.Pages[1..5]`).
- **Контроль нулевого заполнения:** Опустите `NumberOfDigits` для номера переменной длины, либо задайте большее значение, чтобы добавить ведущие нули.
- **Пользовательское позиционирование:** Используйте `Margin` для смещения номера от края или переключите `HorizontalAlignment` на `Center` для размещения внизу посередине.

## Шаг 4: Сохранить изменённый PDF

Наконец, запишите обновлённый документ на диск. Можно перезаписать оригинал или создать новый файл.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

После выполнения этой строки `output.pdf` будет содержать исходное содержимое плюс видимую метку Бейтса на каждой странице — именно то, что ожидается при **how to generate bates** для файлов дела.

## Полный, готовый к запуску пример

Собрав всё вместе, получаем полный фрагмент, который можно скопировать в консольное приложение:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Ожидаемый результат

Откройте `output.pdf` в любом просмотрщике (Adobe Reader, Edge и т.д.). Вы увидите, что каждая страница помечена, например, **CASE-001000**, **CASE-001001**, … до последней страницы. Номера расположены в правом нижнем углу, согласно заданным параметрам.

## Часто задаваемые вопросы и устранение неполадок

- **«Что если мой PDF защищён паролем?»**  
  Загружайте его с паролем: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **«Можно ли добавить нумерацию Бейтса в только что созданный PDF?»**  
  Конечно. Сначала создайте документ (`var doc = new Document();`), затем выполните шаги 2‑4 перед сохранением.

- **«Шрифт всегда встраивается?»**  
  Aspose автоматически встраивает шрифт, если его нет в PDF. При необходимости конкретного семейства шрифтов задайте `options.Font`.

- **«Какова производительность при файлах в 10 000 страниц?»**  
  Библиотека обрабатывает страницы потоково, поэтому потребление памяти остаётся умеренным. Тем не менее, стоит увеличить `PdfSaveOptions.CompressionMode` для ускорения ввода‑вывода.

## Советы для продакшн‑использования

1. **Пакетная обработка:** Оберните вышеописанную логику в цикл, проходящий по папке с PDF‑файлами. Используйте `Directory.GetFiles("*.pdf")` и обрабатывайте каждый файл отдельно.
2. **Логирование:** Записывайте первый и последний номера Бейтса в лог‑файл — это помогает аудиторам убедиться в непрерывности нумерации.
3. **Обработка ошибок:** Оберните весь блок в `try/catch` и выводите понятное сообщение, если исходный PDF отсутствует или повреждён.
4. **Гибкость нулевого заполнения:** Если нужен динамический подсчёт цифр в зависимости от общего количества страниц, вычислите `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Заключение

Мы продемонстрировали, как **create PDF document C#** и без проблем **add Bates numbering** — от начальной загрузки до финального сохранения. Краткий пример показывает **how to add bates**, **add sequential page numbers** и **how to generate bates** с пользовательскими префиксами и нулевым заполнением. С небольшими изменениями вы сможете адаптировать этот шаблон под пакетные задачи, разные макеты или даже интегрировать его в веб‑API, возвращающее сразу пронумерованный PDF по запросу.

Готовы к следующему шагу? Попробуйте сочетать это с функцией **watermark** от Aspose или сгенерировать индекс, где каждому номеру Бейтса сопоставлено краткое описание содержимого страницы. Возможностей бесконечно много, а полученный код — надёжный фундамент для любой автоматизации работы с документами.

Happy coding, and may your PDFs always be perfectly numbered! 

![Скриншот PDF‑просмотрщика, показывающий create pdf document c# с применёнными номерами Бейтса](image-placeholder.png "create pdf document c# with Bates numbers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}