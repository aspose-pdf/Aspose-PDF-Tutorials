---
category: general
date: 2026-04-10
description: Добавьте нумерацию Бейтса в PDF с помощью C# за считанные минуты. Узнайте,
  как добавить пользовательские номера страниц, как нумеровать PDF‑файлы и эффективно
  применять нумерацию Бейтса.
draft: false
keywords:
- add bates numbering
- add custom page numbers
- how to number pdf
- how to add bates
- apply bates numbering
language: ru
og_description: Добавьте нумерацию Бейтса в PDF с помощью C# за считанные минуты.
  Это руководство показывает, как добавить пользовательские номера страниц, как нумеровать
  PDF‑файлы и как пошагово применить нумерацию Бейтса.
og_title: Добавьте нумерацию Бейтса в PDF с помощью C# – Полное руководство
tags:
- PDF
- C#
- Bates numbering
title: Добавьте нумерацию Бейтса в PDF с помощью C# – Полное руководство
url: /ru/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление нумерации Бейтса к PDF с помощью C# – Полное руководство

Когда‑нибудь вам нужно было **add bates numbering** в PDF, но вы не знали, с чего начать? Вы не одиноки — юридические команды, аудиторы и все, кто работает с большими наборами документов, регулярно сталкиваются с этой проблемой. Хорошая новость? С несколькими строками кода на C# вы можете автоматически ставить штамп на каждую страницу с пользовательским идентификатором, и вы также узнаете **how to add custom page numbers** по ходу.

В этом руководстве мы пройдем всё необходимое: требуемый пакет NuGet, настройку параметров нумерации, применение номеров и проверку результата. К концу вы будете знать **how to number PDF** файлы программно, и сможете настроить префикс, суффикс, размер шрифта или даже выбрать конкретные страницы.

## Предварительные требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.7+)
- Visual Studio 2022 (или любой предпочитаемый IDE)
- Библиотека **Aspose.PDF for .NET** (бесплатная пробная версия подходит для обучения)
- Пример PDF с именем `source.pdf`, размещённый в папке, которой вы управляете

Если все пункты выполнены, давайте погрузимся.

## Шаг 1: Установить и подключить Aspose.PDF

Сначала добавьте пакет Aspose.PDF в ваш проект:

```bash
dotnet add package Aspose.PDF
```

Или используйте интерфейс NuGet Package Manager. После установки добавьте пространство имён в начало вашего файла:

```csharp
using Aspose.Pdf;
```

> **Совет:** Держите пакеты в актуальном состоянии; последняя версия (по состоянию на апрель 2026) добавляет несколько улучшений производительности для больших документов.

## Шаг 2: Открыть исходный PDF‑документ

Открыть файл просто. Мы используем блок `using`, чтобы дескриптор файла освобождался автоматически.

```csharp
// Step 2: Open the source PDF document
using (var sourceDocument = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // The rest of the workflow lives inside this block.
}
```

Класс `Document` представляет весь PDF, предоставляя доступ к страницам, аннотациям и, конечно же, нумерации Бейтса.

## Шаг 3: Определить настройки нумерации Бейтса

Теперь переходим к сути — настройке параметров **add bates numbering**. Вы можете управлять начальным номером, префиксом, суффиксом, размером шрифта, отступом и даже указать, какие страницы получат штамп.

```csharp
// Step 3: Define Bates numbering settings
var batesOptions = new BatesNumberingOptions
{
    StartNumber = 1,                 // First number in the sequence
    Prefix = "ABC-",                 // Text before the number
    Suffix = "-2024",                // Text after the number
    FontSize = 12,                   // Size of the numbering font
    Margin = 10,                     // Distance from the page edge (points)
    PageNumbers = new[] { 1, 2, 3 }  // Pages to which numbering is applied
};
```

### Почему эти настройки важны

- **StartNumber** позволяет продолжить последовательность с предыдущей партии.
- **Prefix/Suffix** удобны для идентификаторов дел или отметок года.
- **FontSize** и **Margin** влияют на читаемость; слишком маленький шрифт может быть не заметен при печати.
- **PageNumbers** — это место, где вы **apply bates numbering** выборочно. Опустите этот массив, чтобы нумеровать все страницы.

Если вам нужно **add custom page numbers**, которые не последовательны, вы можете создать список вроде `{5, 10, 15}` и передать его сюда.

## Шаг 4: Применить нумерацию Бейтса к выбранным страницам

С подготовленными параметрами библиотека делает всю тяжелую работу. Метод `AddBatesNumbering` вставляет штамп на каждую целевую страницу.

```csharp
// Step 4: Apply the Bates numbering to the selected pages
sourceDocument.AddBatesNumbering(batesOptions);
```

Внутри Aspose.PDF создает текстовый фрагмент для каждой страницы, позиционирует его согласно отступу и учитывает выбранный размер шрифта. Это гарантирует, что номера появятся точно там, где вы ожидаете, независимо от того, просматриваете вы PDF на экране или печатаете его.

## Шаг 5: Сохранить изменённый документ

Наконец, сохраните изменения в новый файл, чтобы оригинал остался нетронутым.

```csharp
// Step 5: Save the modified document with Bates numbers
sourceDocument.Save("YOUR_DIRECTORY/bates.pdf");
```

Теперь у вас есть `bates.pdf` с проставленными штампами. Откройте его в любом PDF‑просмотрщике, и вы увидите что‑то вроде:

```
ABC-1-2024   (on page 1, top‑right)
ABC-2-2024   (on page 2, top‑right)
ABC-3-2024   (on page 3, top‑right)
```

### Проверка результата

Быстрая проверка — программно считать текст первой страницы:

```csharp
using (var doc = new Document("YOUR_DIRECTORY/bates.pdf"))
{
    var text = doc.Pages[1].ExtractText();
    Console.WriteLine(text.Contains("ABC-1-2024") ? "Bates number applied!" : "Oops, something went wrong.");
}
```

Если консоль выводит *Bates number applied!*, всё в порядке.

## Пограничные случаи и распространённые варианты

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **Нумеровать каждую страницу** | Опустить `PageNumbers` или установить его в `null` | API по умолчанию применяет нумерацию ко всем страницам, если массив не указан. |
| **Разный отступ по сторонам** | Использовать `Margin = new MarginInfo { Top = 15, Right = 10 }` (требуется Aspose > 23.3) | Позволяет точно управлять размещением. |
| **Большие документы (> 500 страниц)** | Установить `batesOptions.StartNumber` на более высокое значение и рассмотреть `batesOptions.FontSize = 10` во избежание наложения | Сохраняет читаемость штампа без захламления страницы. |
| **Требуется другой шрифт** | Установить `batesOptions.Font = FontRepository.FindFont("Arial")` | Некоторые юридические фирмы требуют определённый шрифт. |

> **Осторожно:** Если вы укажете номер страницы, которой не существует (например, `PageNumbers = new[] { 999 }`), Aspose.PDF тихо пропустит её. Всегда проверяйте диапазон, если формируете список динамически.

## Полный рабочий пример

Ниже представлен полный готовый к запуску пример. Вставьте его в консольное приложение, скорректируйте пути и нажмите **F5**.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        // Open the source PDF
        using (var sourceDocument = new Document(sourcePath))
        {
            // Configure Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1,
                Prefix = "ABC-",
                Suffix = "-2024",
                FontSize = 12,
                Margin = 10,
                PageNumbers = new[] { 1, 2, 3 } // Change or remove to number all pages
            };

            // Apply the numbering
            sourceDocument.AddBatesNumbering(batesOptions);

            // Save the new PDF
            sourceDocument.Save(outputPath);
        }

        // Verify the first page contains the expected stamp
        using (var doc = new Document(outputPath))
        {
            string extracted = doc.Pages[1].ExtractText();
            bool success = extracted.Contains("ABC-1-2024");
            Console.WriteLine(success
                ? "Bates numbering added successfully!"
                : "Numbering failed – check your options.");
        }
    }
}
```

Выполнение этого кода создаст `bates.pdf` с тремя проставленными страницами, показанными ранее. Откройте файл, и вы увидите номера, выровненные по правому краю, на расстоянии 10 пунктов от края, шрифтом 12 пунктов.

## Визуальный предварительный просмотр

![предпросмотр добавления нумерации Бейтса](/images/bates-numbering-sample.png)

*Скриншот выше демонстрирует, как выглядит вывод **add bates numbering** после выполнения скрипта.*

## Заключение

Мы только что рассмотрели, как **add bates numbering** в PDF с помощью C#. Настроив `BatesNumberingOptions`, применив штамп и сохранив документ, вы получили повторяемое решение, которое также может **add custom page numbers**, **how to number pdf** файлы и **apply bates numbering** в любом проекте. 

Следующие шаги? Попробуйте сочетать это с пакетным процессором, который проходит по папке с PDF, или поэкспериментировать с разными префиксами для каждого типа дел. Вы также можете изучить объединение нескольких PDF после нумерации — это полезно для создания комплексных наборов дел.

Есть вопросы о пограничных случаях или хотите увидеть, как встроить номера в нижний колонтитул вместо верхнего? Оставьте комментарий, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}