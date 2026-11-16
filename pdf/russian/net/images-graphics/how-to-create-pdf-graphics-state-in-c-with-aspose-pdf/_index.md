---
category: general
date: 2026-11-16
description: Узнайте, как создать графическое состояние PDF в C# с помощью Aspose.Pdf.
  Это руководство охватывает непрозрачность, режим наложения и полный пример кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: ru
lastmod: 2026-11-16
og_description: Создайте графическое состояние PDF в C# с помощью Aspose.Pdf. Следуйте
  этому полному руководству, чтобы программно установить непрозрачность и режим наложения.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Создание графического состояния PDF в C# — пошаговое руководство Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Как создать графическое состояние PDF в C# с помощью Aspose.Pdf
url: /ru/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать графическое состояние PDF в C# с Aspose.Pdf

Если вам нужно **создать графическое состояние PDF** в проекте .NET, этот учебник покажет, как сделать это с помощью Aspose.Pdf. Хотите ли вы управлять непрозрачностью, менять режим наложения или переиспользовать пользовательское графическое состояние на разных страницах — нижеописанные шаги дадут вам готовое решение, готовое к запуску.

В этом руководстве вы узнаете, как получить доступ к ресурсам страницы, добавить запись **ExtGState** и сохранить изменения в новый файл. Пример работает с Aspose.Pdf 23.12 (или новее) и ориентирован на .NET 6+, но концепции применимы и к более ранним версиям.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* Visual Studio 2022 (или любая IDE для C#) с установленным .NET 6 SDK.  
* Лицензия Aspose.Pdf for .NET или временный ключ оценки.  
* PDF‑файл с именем `input.pdf`, размещённый в папке, к которой вы можете обратиться из кода.  

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Pdf`.

## Что покрывает учебник

* Загрузка существующего PDF‑документа.  
* Переход к словарю ресурсов первой страницы.  
* Создание нового словаря графического состояния, определяющего непрозрачность обводки (`CA`), непрозрачность заливки (`ca`) и режим наложения (`BM`).  
* Добавление нового графического состояния в коллекцию **ExtGState** с пользовательским именем (`GS0`).  
* Сохранение обновлённого PDF, чтобы последующие команды рисования могли ссылаться на новое состояние.

К концу учебника вы сможете программно **создавать объекты графического состояния PDF** и переиспользовать их в любых операциях рисования.

## Шаг 1: Настройка проекта и импорт пространств имён

Создайте новое консольное приложение (или интегрируйте код в существующий проект). Добавьте ссылку на Aspose.Pdf и подключите необходимые пространства имён:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro tip:** Если вы используете бесплатную оценочную версию, добавьте `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` перед загрузкой документа, чтобы избавиться от сообщений о водяных знаках.

## Шаг 2: Загрузка PDF‑документа

Открыть файл просто. Класс `Document` представляет весь PDF и даёт доступ к его страницам и ресурсам.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Размещение кода внутри блока `using` гарантирует освобождение файлового дескриптора после операции, что критично для **C# PDF manipulation** в производственных сервисах.

## Шаг 3: Получение словаря ресурсов первой страницы

Каждая страница PDF имеет словарь *Resources*, где хранятся шрифты, изображения и графические состояния. Нам нужен `DictionaryEditor` для редактирования этой структуры.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Если PDF уже содержит запись `ExtGState`, `resourcesEditor["ExtGState"]` вернёт её; иначе Aspose.Pdf создаст пустой словарь, когда мы добавим первую запись.

## Шаг 4: Доступ к словарю ExtGState или его создание

Словарь **ExtGState** хранит именованные объекты графических состояний. Мы либо получаем существующий, либо создаём новый контейнер.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Когда `ExtGState` отсутствует, `resourcesEditor["ExtGState"]` автоматически возвращает новый пустой словарь, обеспечивая работу кода с любым PDF.

## Шаг 5: Формирование нового словаря графического состояния

Графическое состояние — это `CosPdfDictionary` со следующими ключами:

* `CA` – непрозрачность обводки (0‑1)  
* `ca` – непрозрачность заливки (0‑1)  
* `BM` – режим наложения (`Normal`, `Multiply` и т.д.)

Мы создаём пустой словарь, заполняем его и затем добавляем в `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Вы можете изменить `0.5` на любое значение от `0` до `1`, чтобы настроить непрозрачность заливки, или заменить `"Normal"` на `"Multiply"` для другого **PDF blend mode**. Такая гибкость делает **create PDF graphics state** мощной техникой в работе с **Aspose.Pdf graphics state**.

## Шаг 6: Регистрация графического состояния под именем

Потоки содержимого PDF ссылаются на графические состояния по имени. Здесь мы используем `GS0`, но подойдёт любое уникальное имя.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Если требуется несколько состояний, повторите шаг создания с другими параметрами и добавьте их как `GS1`, `GS2` и т.д. Такой подход хорошо масштабируется для сложных документов, где нужны разные настройки непрозрачности или наложения на разных слоях.

## Шаг 7: Сохранение изменённого PDF

Наконец, запишите обновлённый документ в новый файл. Сохранение оригинала нетронутым упрощает отладку.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

После выполнения `output.pdf` будет содержать запись `ExtGState` с именем `GS0`. Любой последующий оператор рисования может обратиться к нему через оператор `gs` (например, `GS0 gs` в потоке содержимого).  

> **Почему это важно:** Создавая переиспользуемое графическое состояние, вы избегаете повторения настроек непрозрачности и наложения для каждой команды рисования, что повышает производительность и облегчает поддержку.

## Использование нового графического состояния в потоке содержимого (опционально)

Если хотите сразу увидеть эффект, добавьте простой прямоугольник, использующий только что созданное состояние:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

Прямоугольник будет нарисован с 50 % непрозрачностью заливки, тогда как обводка останется полностью непрозрачной, точно как определено в словаре **create PDF graphics state**.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Запись `ExtGState` не найдена | Некоторые PDF‑файлы полностью опускают этот словарь. | `DictionaryEditor` автоматически создаёт его при добавлении первой записи, поэтому дополнительная проверка не нужна. |
| Значения непрозрачности > 1 или < 0 | Спецификация PDF ограничивает непрозрачность диапазоном `[0,1]`. | Ограничьте значения перед созданием `CosPdfNumber`. |
| Ошибка в названии режима наложения | Имена режимов чувствительны к регистру. | Используйте точные имена, такие как `"Normal"`, `"Multiply"`, `"Screen"`. |
| Водяной знак лицензии | Оценочная версия добавляет водяной знак на первую страницу. | Примените действительный файл лицензии перед открытием документа. |

Учёт этих нюансов гарантирует, что ваша реализация **create PDF graphics state** будет надёжно работать с различными PDF‑источниками.

## Полный, готовый к запуску пример

Ниже представлена самостоятельная программа, которую можно скопировать, вставить и запустить. Замените `YOUR_DIRECTORY` на реальный путь к папке на вашем компьютере.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## Что стоит изучить дальше?


В следующих учебниках рассматриваются тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}