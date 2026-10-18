---
category: general
date: 2026-08-04
description: Создайте новый PDF‑документ на C# и быстро добавьте нумерацию Бейтса
  в PDF с помощью Aspose.Pdf — узнайте, как добавить пустую страницу в PDF и пользовательские
  номера страниц.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: ru
lastmod: 2026-08-04
og_description: Создайте новый PDF‑документ на C# и автоматически добавьте нумерацию
  Бейтса в PDF для управления юридическими делами — включён полный пример кода.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Создать новый PDF‑документ с нумерацией Бейтса в C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Создать новый PDF‑документ с нумерацией Бейтса в C#
url: /ru/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание нового PDF‑документа с нумерацией Бейтса в C#

Если вам нужно **создать новый PDF‑документ** на C#, это руководство покажет, как **добавить нумерацию Бейтса в PDF** с помощью Aspose.Pdf. Вы узнаете, как **добавить пустую страницу в PDF**, настроить **добавление пользовательских номеров страниц** и сохранить итоговый файл.

В руководстве рассматривается каждый шаг — от установки библиотеки до генерации PDF, соответствующего требованиям юридических дел. К концу вы сможете создать PDF, вставить пустую страницу, применить нумерацию Бейтса и настроить формат нумерации — всё в одной исполняемой программе.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 SDK или более поздняя версия  
* Visual Studio 2022 (или любая IDE для C#)  
* Действующая лицензия Aspose.Pdf for .NET или бесплатный ключ оценки  

Дополнительные пакеты NuGet не требуются; руководство установит всё автоматически.

## Шаг 1: Установка Aspose.Pdf через NuGet

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.Pdf
```

Эта команда добавит последнюю стабильную версию Aspose.Pdf в ваш проект, предоставив классы `Document`, `BatesNumbering` и другие классы для работы с PDF.

## Шаг 2: Создание нового PDF‑документа – начальная настройка

Создание PDF‑файла является основой для всех последующих операций. Класс `Document` представляет весь контейнер PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Почему это важно*: Создание экземпляра `Document` выделяет внутренние структуры, необходимые для страниц, шрифтов и графики. Использование `using var` гарантирует корректное освобождение ресурсов после сохранения файла.

## Шаг 3: Добавление пустой страницы в PDF

PDF‑документ должен содержать хотя бы одну страницу, прежде чем вы сможете разместить на ней содержимое. Добавление пустой страницы дает чистый холст для номеров Бейтса.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

Метод `Pages.Add()` добавляет новую, пустую страницу в конец коллекции страниц документа. При необходимости вы можете вызвать его несколько раз, чтобы добавить больше страниц и **добавить пользовательские номера страниц** на нескольких листах.

## Шаг 4: Настройка нумерации Бейтса – как добавить нумерацию

Нумерация Бейтса — это последовательный идентификатор, часто используемый в юридических документах. Настраивается она через класс `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Почему это важно*: `StartNumber` задаёт первое число, `Prefix` добавляет читаемую метку, а `Increment` определяет шаг. Также можно изменить `HorizontalAlignment`, `VerticalAlignment`, `FontSize` и `Margins`, чтобы контролировать внешний вид номера на каждой странице.

## Шаг 5: Применение нумерации Бейтса к странице

После настройки параметров нумерации примените их к странице (или ко всему документу).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Вызов `Apply` вставляет отформатированный номер в нижний колонтитул страницы по умолчанию. Если требуется разместить номер в другом месте, задайте `bates.Position` перед вызовом `Apply`.

## Шаг 6: Сохранение PDF с применённой нумерацией Бейтса

Наконец, запишите документ из памяти на диск.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Сохранённый файл теперь содержит одну страницу с номером Бейтса **CaseA-1000**, отображаемым внизу. Откройте PDF в любом просмотрщике, чтобы проверить нумерацию.

## Ожидаемый результат

При открытии `BatesNumbered.pdf` вы должны увидеть:

* Одна пустая страница (или больше, если вы добавили дополнительные)  
* Текст **CaseA-1000**, расположенный в нижней части страницы (позиция по умолчанию)  

Если вы добавите ещё страниц и будете использовать тот же экземпляр `BatesNumbering`, номера будут автоматически увеличиваться (CaseA-1001, CaseA-1002, …).

## Совет профессионала: Добавление пользовательских номеров страниц вместе с нумерацией Бейтса

Иногда требуется одновременно использовать номера Бейтса и традиционные номера страниц. Их можно комбинировать, добавив `TextFragment` после применения нумерации Бейтса:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Этот фрагмент демонстрирует **добавление пользовательских номеров страниц**, сохраняя метку Бейтса.

## Особый случай: Применение нумерации Бейтса к нескольким страницам

Если ваш документ содержит несколько страниц, вы можете применить один и тот же экземпляр `BatesNumbering` к каждой странице в цикле:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Цикл гарантирует, что каждая страница получит последовательный номер в соответствии с заданными `StartNumber` и `Increment`.

## Распространённые ошибки и способы их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Номера смещены от центра | Выравнивание по умолчанию может не соответствовать вашему макету | Явно задайте `bates.HorizontalAlignment` и `bates.VerticalAlignment` |
| Номера перекрывают существующее содержимое | Не определён отступ | Отрегулируйте `bates.Margin` или используйте `bates.Position` для смещения номера |
| Исключение лицензии во время выполнения | Ограничения версии оценки | Примените действующую лицензию Aspose.Pdf перед созданием документа (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Полный рабочий пример

Ниже представлена автономная программа, которую можно скопировать, вставить и запустить.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Создать новый PDF‑документ
        using var doc = new Document();

        // 2. Добавить пустую страницу pdf
        Page page = doc.Pages.Add();

        // 3. Настроить нумерацию Бейтса – как добавить нумерацию
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Что следует изучить дальше?


Ниже перечислены руководства, охватывающие смежные темы, которые расширяют техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}