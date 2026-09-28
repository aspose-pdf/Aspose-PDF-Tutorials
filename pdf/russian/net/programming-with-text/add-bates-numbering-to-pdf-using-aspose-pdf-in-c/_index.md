---
category: general
date: 2026-09-27
description: Добавьте нумерацию Бейтса в PDF с помощью Aspose.PDF на C#. Узнайте,
  как загрузить PDF‑документ, установить параметры нумерации Бейтса и сохранить обновлённый
  файл.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: ru
lastmod: 2026-09-27
og_description: Добавьте нумерацию Бейтса в PDF с помощью Aspose.PDF на C#. Этот учебник
  покажет, как загрузить PDF‑документ, настроить нумерацию Бейтса и сохранить результат.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Добавление нумерации Бейтса в PDF с Aspose.PDF – руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Добавить нумерацию Бейтса в PDF с использованием Aspose.PDF на C#
url: /ru/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление нумерации Бейтса в PDF с помощью Aspose.PDF на C#

Если вам нужно **добавить нумерацию Бейтса** в PDF‑файл, это руководство покажет полностью готовое решение. Вы увидите, как **загрузить PDF‑документ**, настроить параметры нумерации Бейтса и записать пронумерованный файл обратно на диск — все с помощью Aspose.PDF for .NET.

Применение нумерации Бейтса часто используется в юридических, правоохранительных и архивных процессах. По окончании этого урока вы сможете добавить последовательный идентификатор на каждую страницу, настроить префикс и задать начальное значение счёта.

## Что вы узнаете

* Как **загрузить содержимое PDF‑документа** в объект `Aspose.Pdf.Document`.  
* Точные шаги **как добавить нумерацию Бейтса** с помощью `BatesNumberingOptions`.  
* Как сохранить изменённый файл, сохранив оригинальное расположение и качество.  

Никакие внешние инструменты не требуются — только пакет Aspose.PDF NuGet и среда разработки .NET (Visual Studio, VS Code или Rider).  

---

## Шаг 1: Установить Aspose.PDF для .NET

Откройте папку проекта в терминале и выполните:

```bash
dotnet add package Aspose.PDF
```

Пакет включает пространство имён `Aspose.Pdf`, которое предоставляет все классы, используемые в этом руководстве. После установки перезагрузите проект, чтобы IDE обнаружила новую ссылку.

## Шаг 2: Загрузить PDF‑документ

Загрузка исходного файла — это первая операция, потому что движок нумерации Бейтса работает с уже существующим экземпляром `Document`.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Почему это важно:** Класс `Document` разбирает структуру PDF, предоставляя доступ к страницам, аннотациям и метаданным. Без предварительной загрузки файла вы не сможете применить нумерацию.

## Шаг 3: Настроить параметры нумерации Бейтса

Создайте объект `BatesNumberingOptions` и задайте нужный префикс, стартовое число и необязательные параметры форматирования.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Почему это важно:** `BatesNumberingOptions` сообщает Aspose.PDF, как формировать метку для каждой страницы. `Prefix` помогает группировать связанные дела, а `StartNumber` позволяет продолжить последовательность от предыдущей партии.

## Шаг 4: Сохранить PDF с применённой нумерацией Бейтса

Передайте объект параметров в метод `Save`. Aspose.PDF записывает номера непосредственно на каждую страницу.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Почему это важно:** Перегрузка `Save(string, BatesNumberingOptions)` объединяет шаг рендеринга с процессом нумерации, гарантируя, что в выходном файле будут видимые идентификаторы.

## Полный пример — всё вместе

Ниже приведена единая, автономная программа, которую можно скопировать, вставить и запустить. Она демонстрирует **как добавить нумерацию Бейтса** от начала до конца.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Ожидаемый результат

Запуск программы создаёт `output.pdf`, где каждая страница отображает метку, похожую на:

```
CASE01-1
CASE01-2
CASE01-3
...
```

По умолчанию номера выводятся в нижнем колонтитуле, но их можно переместить, изменив свойство `Margin` в `BatesNumberingOptions`.

## Пограничные случаи и распространённые варианты

| Ситуация | Что нужно изменить |
|-----------|--------------------|
| **Разный префикс для каждой партии** | Измените `Prefix` перед вызовом `Save`. Можно выполнить цикл по нескольким документам с разными префиксами. |
| **Продолжить нумерацию от предыдущего файла** | Установите `StartNumber` в значение последнего использованного номера + 1. |
| **Разместить номера в верхнем колонтитуле** | Используйте `batesOptions.Margin = new Margin(20, 0, 0, 0);` (верхний отступ) или настройте `batesOptions.Position`. |
| **Свой шрифт или цвет** | Присвойте свойства `Font`, `FontSize` и `Color`, как показано в закомментированном разделе. |
| **Большие PDF (1000+ страниц)** | Операция экономична по памяти; однако перед сохранением можно вызвать `doc.OptimizeResources()`, чтобы уменьшить размер файла. |

**Совет:** Если ваш процесс требует разных схем нумерации для разных документов, вынесите логику в вспомогательный метод:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Заключение

Теперь вы знаете **как добавить нумерацию Бейтса** в любой PDF с помощью Aspose.PDF на C#. В руководстве рассмотрены загрузка PDF‑документа, настройка параметров нумерации и сохранение финального файла — всё в одной исполняемой программе.  

Дальше вы можете изучать связанные темы, такие как **добавление водяных знаков**, **объединение нескольких PDF** или **извлечение текста** с помощью Aspose.PDF. Экспериментируйте с различными шрифтами, цветами и позициями, чтобы соответствовать стандартам форматирования вашей организации.

Готовы автоматизировать рабочий процесс с юридическими документами? Добавьте код в конвейер сборки, запустите его для пакетов файлов и позвольте Aspose.PDF выполнить тяжёлую работу. Приятного кодинга!


## Что изучать дальше?


В следующих руководствах рассматриваются тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Создать PDF‑документ C# – Добавить нумерацию Бейтса](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Добавить нумерацию Бейтса в PDF – Пошаговое руководство по нумерации страниц PDF](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Вставить пустую страницу и обновить нумерацию Бейтса](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}