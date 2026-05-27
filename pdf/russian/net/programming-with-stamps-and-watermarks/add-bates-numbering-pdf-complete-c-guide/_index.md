---
category: general
date: 2026-03-22
description: Быстро добавляйте нумерацию Бейтса в PDF с помощью Aspose.Pdf. Узнайте,
  как добавить нумерацию Бейтса, последовательные номера страниц, пользовательский
  нижний колонтитул в PDF и артефакт в PDF за считанные минуты.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: ru
og_description: Добавление нумерации Бейтса в PDF с помощью Aspose.Pdf. Это руководство
  показывает, как добавить нумерацию Бейтса, последовательные номера страниц, пользовательский
  нижний колонтитул и артефакт в PDF.
og_title: Добавление нумерации Бейтса в PDF – пошаговое руководство на C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Добавление нумерации Бейтса в PDF — Полное руководство по C#
url: /ru/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление Bates Numbering PDF – Полное руководство на C#

Когда‑нибудь вам нужно было **add bates numbering pdf** к партии юридических документов, но вы не знали, с чего начать? Вы не первый — многие разработчики сталкиваются с этим при создании инструментов управления делами. Хорошая новость? С Aspose.Pdf вы можете **add bates**, **add sequential page numbers**, и даже **add custom footer pdf** элементы всего в несколько строк кода.  

В этом руководстве мы пройдем весь процесс, от установки библиотеки до сохранения конечного файла, и добавим несколько советов о том, как **add artifact to pdf** файлы без нарушения существующего содержимого. К концу у вас будет готовый фрагмент кода, который можно вставить в любой проект .NET.

## Что понадобится

- .NET 6+ (код работает как на .NET Core, так и на .NET Framework)  
- Действительная лицензия Aspose.Pdf for .NET (можно начать с бесплатной оценки)  
- Входной PDF (`input.pdf`) размещённый в папке, к которой вы можете обратиться  
- Visual Studio, Rider или любой предпочитаемый вами редактор C#  

Это всё — никаких дополнительных пакетов NuGet, кроме Aspose.Pdf.

## Шаг 1: Установите Aspose.Pdf через NuGet

Сначала самое главное — получим библиотеку на ваш компьютер. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.Pdf
```

Или, если вы используете консоль диспетчера пакетов Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*Pro tip:* После установки убедитесь, что папка `Aspose.Pdf` появилась в разделе `Dependencies → Packages` в обозревателе решений.

## Шаг 2: Загрузите исходный PDF‑документ

Теперь мы создаём объект `Document`, представляющий PDF, который хотим пометить. Использование инструкции `using` гарантирует автоматическое освобождение дескриптора файла.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Зачем использовать `using var`? Это гарантирует освобождение ресурсов даже при возникновении исключения, предотвращая блокировку файла при попытке перезаписать его позже.

## Шаг 3: Создайте и настройте артефакт Bates Numbering

Номер Bates по сути является текстовым артефактом, находящимся в логической структуре PDF. Его можно рассматривать как **custom footer pdf**, поскольку он отображается на каждой странице, не будучи частью потока содержимого страницы.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Почему эти настройки важны

- **Prefix**: Полезно для различения типов документов (например, “INV‑” для счетов).  
- **Start**: Устанавливает первое число; его можно получать из базы данных, если нужна непрерывность между файлами.  
- **Format**: `"0000"` заставляет отображать четыре цифры, обеспечивая выравнивание при росте номеров.  
- **X/Y**: Координаты измеряются от нижнего левого угла, поэтому `Y = 20` размещает текст сразу над полем страницы. Измените `X`, если хотите выровнять номер по левому краю или по центру.

Если вам нужно **add sequential page numbers** вместо номеров Bates, просто опустите `Prefix` и измените `Format` на `"###"` или любой другой желаемый шаблон.

## Шаг 4: Примените артефакт ко всем страницам

Aspose.Pdf позволяет прикрепить артефакт к всему документу одним вызовом. Это самый эффективный способ **add artifact to pdf** без ручного перебора каждой страницы.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Внутри Aspose добавляет артефакт в словарь страниц каждой страницы, что делает нумерацию частью логической структуры PDF — идеально для последующего извлечения или поиска.

## Шаг 5: Сохраните обновлённый PDF

Наконец, запишите изменения обратно на диск. Вы можете перезаписать оригинал или сохранить в новый файл; второй вариант безопаснее во время разработки.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Когда вы откроете `output.pdf` в просмотрщике, вы увидите «INV‑1000», «INV‑1001», … в правом нижнем углу каждой страницы.

### Проверка результата

Откройте PDF в Adobe Acrobat или любом просмотрщике и найдите номера. Если нужно подтвердить программно, можно прочитать обратно артефакт:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Этот фрагмент выводит метку Bates каждой страницы — удобно для автоматических тестов.

## Особые случаи и часто задаваемые вопросы

### Что если в моём PDF уже есть нижний колонтитул?

Добавление артефакта не перезапишет существующие колонтитулы, поскольку артефакты находятся в отдельном слое. Однако если визуальное перекрытие вызывает беспокойство, отрегулируйте координату `Y` или увеличьте смещение `X`, чтобы переместить номер Bates.

### Можно ли использовать другой шрифт или цвет?

Конечно. `BatesNumberingArtifact` наследуется от `Artifact`, поэтому вы можете задать `Font`, `FontColor` и даже `Opacity`. Пример:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Как сбросить счётчик для нового документа?

Просто измените `Start` перед вызовом `AddArtifact`. Если вы генерируете множество PDF в цикле, храните текущий счётчик в логике вашего приложения.

### Совместим ли этот подход с зашифрованными PDF?

Aspose.Pdf может открыть зашифрованные PDF, если предоставить пароль:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

После расшифровки те же шаги добавления артефакта работают безупречно.

## Полный рабочий пример

Ниже приведена полная, готовая к запуску программа. Вставьте её в консольное приложение, скорректируйте пути и нажмите **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Ожидаемый вывод:** Консоль выводит «Bates numbering added successfully!», а `output.pdf` содержит последовательные метки вроде `INV‑1000`, `INV‑1001` и т.д., расположенные в правом нижнем углу каждой страницы.

## Краткое резюме

- **Primary goal:** **add bates numbering pdf** using Aspose.Pdf.  
- Мы рассмотрели **how to add bates**, **add sequential page numbers**, и **add custom footer pdf** элементы через один артефакт.  
- Руководство показало, как **add artifact to pdf**, обрабатывать особые случаи и проверять результат.  

## Что дальше?

- **Dynamic prefixes:** Получать значения из базы данных для генерации “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Conditional placement:** Использовать определение размера страницы (`page.MediaBox`) для центрирования номеров на альбомных страницах.  
- **Combine with watermarks:** Добавить полупрозрачный логотип рядом с номером Bates для брендинга.  

Не стесняйтесь экспериментировать — возможно, вы найдёте более умный способ пакетной обработки тысяч файлов. Если возникнут проблемы, оставьте комментарий или ознакомьтесь с официальной документацией Aspose (она удивительно понятна). Приятного кодинга!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}