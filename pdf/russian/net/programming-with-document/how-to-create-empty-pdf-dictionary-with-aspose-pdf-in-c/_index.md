---
category: general
date: 2026-09-18
description: Научитесь создавать пустой PDF‑словарь в C# с помощью Aspose.PDF. Это
  пошаговое руководство охватывает ExtGState, графическое состояние и работу с CosPdfDictionary.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: ru
lastmod: 2026-09-18
og_description: Создайте пустой словарь PDF в C# с помощью Aspose.PDF. Следуйте этому
  подробному руководству, чтобы редактировать словари ExtGState и графических состояний.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: Создание пустого словаря PDF в C# — полное руководство по Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Как создать пустой словарь PDF с помощью Aspose.PDF в C#
url: /ru/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать пустой PDF‑словарь с помощью Aspose.PDF в C#

Если вам нужно **создать пустой PDF‑словарь** при обработке PDF‑файла, это руководство покажет, как сделать это с помощью Aspose.PDF для .NET. Независимо от того, регулируете ли вы прозрачность, режимы наложения или любое пользовательское графическое состояние, нижеописанные шаги позволят безопасно и эффективно изменить словарь `ExtGState`.

В этом учебнике вы научитесь:

* Загружать PDF‑документ с помощью Aspose.PDF.
* Получать ресурсы первой страницы и существующий словарь `ExtGState`.
* Создавать новый пустой `CosPdfDictionary` и заполнять его записями графического состояния.
* Сохранять изменённый PDF без потери оригинального содержимого.

Решение работает с любым PDF, содержащим хотя бы одну страницу, и требует только библиотеки Aspose.PDF (версия 23.10 или новее).

## Требования

* .NET 6.0 или новее (код также работает на .NET Framework 4.8).
* Ссылка на пакет **Aspose.PDF** из NuGet.
* Входной PDF‑файл, расположенный по пути `YOUR_DIRECTORY/input.pdf`.
* Базовые знания C# и концепций PDF, таких как ресурсы и графическое состояние.

> **Pro tip:** При работе с большими PDF‑файлами оборачивайте объект `Document` в блок `using`, чтобы обеспечить своевременное освобождение всех файловых дескрипторов.

## Шаг 1: Загрузка PDF‑документа

Первая операция открывает исходный файл. Aspose.PDF считывает весь документ в память, позволяя редактировать внутренние объекты.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Почему это важно*: Загрузка документа создаёт изменяемую модель объектов. Без этого шага вы не сможете получить доступ к ресурсам страницы, необходимым для работы со словарём.

## Шаг 2: Получение ресурсов первой страницы

Каждая страница хранит словарь `Resources`, содержащий шрифты, изображения и графические состояния. Доступ к нему даёт вам `DictionaryEditor`, упрощающий операции чтения/записи.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Почему это важно*: Словарь `ExtGState` находится внутри ресурсов страницы. Изменение неправильного словаря не повлияет на рендеринг.

## Шаг 3: Поиск существующего словаря ExtGState

Запись `ExtGState` может уже содержать объекты графического состояния. Мы получаем её как `CosPdfDictionary`, чтобы добавить новые записи.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Если запись `ExtGState` отсутствует, Aspose.PDF автоматически создаст пустой словарь, когда вы позже присвоите новый.

## Шаг 4: **Создать пустой PDF‑словарь** для нового графического состояния

Здесь мы создаём совершенно новый `CosPdfDictionary` — ядро операции **create empty PDF dictionary**. Затем заполняем его стандартными ключами графического состояния:

* `CA` — непрозрачность штриха.
* `ca` — непрозрачность заливки.
* `BM` — режим наложения.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Почему это важно*: Явно определяя каждую запись, вы контролируете, как объекты на странице будут смешиваться и отображаться. Словарь **пустой**, пока вы не добавите эти ключи, что удовлетворяет требованию **create empty PDF dictionary** перед их заполнением.

## Шаг 5: Добавление нового графического состояния в словарь ExtGState

Каждое графическое состояние должно иметь уникальное имя (например, `GS0`). Мы вставляем только что построенный словарь под этим именем.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

Если требуется несколько состояний, продолжайте добавлять записи типа `GS1`, `GS2` и т.д., убедившись, что каждое имя уникально в пределах словаря `ExtGState`.

## Шаг 6: Сохранение обновлённого PDF‑документа

Наконец, записываем изменения на диск. Исходный файл остаётся нетронутым, потому что мы сохраняем в новый путь.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

Полученный `output.pdf` теперь содержит дополнительное графическое состояние (`GS0`), которое можно использовать в любом потоке содержимого страницы с помощью оператора `/GS0`.

## Полный рабочий пример

Собрав все шаги вместе, получаем автономную программу, готовую к запуску.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Ожидаемый результат**: После выполнения программы `output.pdf` будет содержать тот же визуальный контент, что и `input.pdf`. При просмотре PDF в инструментах вроде Adobe Acrobat или PDF‑Tron вы увидите новую запись `GS0` в словаре `ExtGState` первой страницы.

## Распространённые варианты и граничные случаи

| Ситуация | Что нужно изменить |
|-----------|-------------------|
| **Отсутствует запись ExtGState** | Замените `resourcesEditor["ExtGState"]` на `new CosPdfDictionary(pdfDocument)` и присвойте её обратно в `firstPage.Resources["ExtGState"]`. |
| **Несколько страниц нуждаются в одинаковом состоянии** | Добавьте ту же запись `GS0` в `ExtGState` каждой страницы или сослаться на словарь из общего объекта ресурсов. |
| **Другой режим наложения** | Измените значение `CosPdfName` с `"Normal"` на `"Multiply"`, `"Screen"` и т.д., в зависимости от требуемого эффекта. |
| **Более высокие значения непрозрачности** | Используйте `new CosPdfNumber(0.8)` для `ca` или `CA`, чтобы увеличить непрозрачность заливки или штриха. |
| **Использование оператора потока** | В потоке содержимого запишите `"/GS0 gs"` перед операциями рисования, чтобы применить новое графическое состояние. |

## Соображения по производительности

* **Использование памяти** — загрузка очень большого PDF требует памяти, пропорциональной количеству страниц. Если нужно изменить только первую страницу, рассмотрите возможность удаления остальных с помощью `pdfDocument.Pages.Delete(pageNumber)` после обработки, чтобы освободить ресурсы.
* **Потокобезопасность** — объекты Aspose.PDF не являются потокобезопасными. Выполняйте изменения словарей в одном потоке или создавайте отдельные экземпляры `Document` для каждого потока.

## Заключение

Теперь вы знаете, как **create empty PDF dictionary** с помощью Aspose.PDF, заполнять его записями графического состояния и прикреплять к словарю `ExtGState` страницы. Эта техника даёт тонкий контроль над непрозрачностью, режимом наложения и другими параметрами рендеринга непосредственно из C#.

Далее изучайте связанные темы, такие как **PDF manipulation C#**, добавление пользовательских записей **ExtGState dictionary** для продвинутых эффектов прозрачности или использование **CosPdfDictionary** для изменения других типов ресурсов, например шрифтов или XObject‑ов. Экспериментируйте с несколькими графическими состояниями, чтобы создавать сложные визуальные эффекты в ваших PDF‑файлах.

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Создание и заполнение прямоугольников в PDF с помощью Aspose.PDF для .NET: пошаговое руководство](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [Как создать пунктирные линии в PDF с помощью Aspose.PDF для .NET: пошаговое руководство](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Как добавить пустую страницу в конец PDF с помощью Aspose.PDF для .NET | пошаговое руководство](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}