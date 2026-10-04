---
category: general
date: 2026-10-04
description: Узнайте, как изменить прозрачность PDF с помощью Aspose.Pdf в C#. Это
  пошаговое руководство добавляет пользовательское графическое состояние для настройки
  непрозрачности и режима смешивания.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity C#
- ExtGState dictionary
- blend mode PDF
language: ru
lastmod: 2026-10-04
og_description: Измените прозрачность PDF в C# с помощью Aspose.Pdf. Следуйте этому
  краткому руководству, чтобы изменить непрозрачность, режим наложения и графическое
  состояние в ваших PDF‑файлах.
og_image_alt: Screenshot of a PDF page before and after changing transparency with
  Aspose.Pdf
og_title: Изменение прозрачности PDF с помощью Aspose.Pdf – полное руководство по
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to change PDF transparency with Aspose.Pdf in C#. This step‑by‑step
    guide adds a custom graphics state to adjust opacity and blend mode.
  headline: How to change PDF transparency using Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- graphics state
title: Как изменить прозрачность PDF с помощью Aspose.Pdf в C#
url: /ru/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как изменить прозрачность PDF с помощью Aspose.Pdf на C#

Если вам нужно **изменить прозрачность PDF** в проекте .NET, это руководство покажет, как сделать это с помощью Aspose.Pdf. К концу урока у вас будет PDF, в котором выбранные объекты используют пользовательскую непрозрачность и режим наложения, без необходимости в сторонних инструментах.

Работа с непрозрачностью PDF часто требуется для водяных знаков, наложения графики или тонких визуальных эффектов. Ниже приведены все шаги — от загрузки документа до редактирования **ExtGState dictionary**, создания нового графического состояния и сохранения результата.

## Требования

* **Aspose.Pdf for .NET** (версия 23.12 или новее). Вы можете установить его через NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Среда разработки .NET (Visual Studio, VS Code или `dotnet` CLI).
* PDF‑файл‑вход, расположенный в известном каталоге (в примере используется `input.pdf`).

Дополнительные библиотеки не требуются.

## Шаг 1: Загрузка PDF‑документа

Первая операция — открыть существующий PDF. Использование блока `using` гарантирует автоматическое освобождение файлового дескриптора.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;

// ...

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Почему это важно*: Загрузка документа создает представление в памяти, которое вы можете изменять. Класс `Document` также предоставляет доступ к низкоуровневым объектам COS, что необходимо для изменения прозрачности PDF.

## Шаг 2: Доступ к ресурсам первой страницы

Графические состояния хранятся в словаре ресурсов страницы. Мы получаем первую страницу и оборачиваем её ресурсы в `DictionaryEditor`, чтобы удобно их редактировать.

```csharp
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Explanation*: `DictionaryEditor` абстрагирует работу со словарём COS, позволяя читать и записывать записи вроде `ExtGState`, не имея дело с сырой PDF‑синтаксисом.

## Шаг 3: Получить (или создать) словарь ExtGState

**ExtGState dictionary** хранит именованные объекты графических состояний. Если он уже существует, мы переиспользуем его; иначе создаём новый.

```csharp
CosPdfDictionary extGStateDict;

// Try to fetch an existing ExtGState entry
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and add it to the resources
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Почему этот шаг*: Без записи `ExtGState` движок PDF не знает, где искать пользовательские настройки непрозрачности. Добавление словаря делает страницу осведомлённой о новых графических состояниях, которые вы определяете.

## Шаг 4: Определить новое графическое состояние с непрозрачностью и режимом наложения

Графическое состояние — это набор параметров рендеринга PDF. Здесь мы задаём:

* **CA** – непрозрачность обводки (1 = полностью непрозрачна)
* **ca** – непрозрачность заливки (0.5 = 50 % прозрачна)
* **BM** – режим наложения (`Normal` по умолчанию, но можно экспериментировать с `Multiply`, `Screen` и др.)

```csharp
// Create an empty dictionary that will become the new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Prepare the entries
var graphicsStateEntries = new KeyValuePair<string, ICosPdfPrimitive>[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

// Populate the dictionary
foreach (var entry in graphicsStateEntries)
{
    graphicsState.Add(entry);
}
```

*Insight*: Значения `CosPdfNumber` — числа с плавающей точкой от 0 до 1. Их изменение позволяет точно настроить, насколько прозрачными выглядят обводки и заливки. Режим наложения определяет, как прозрачный контент взаимодействует с графикой под ним.

## Шаг 5: Зарегистрировать графическое состояние в ExtGState

Мы даём новому состоянию имя (`GS0`). Позже, при рисовании объектов, вы будете ссылаться на это имя в потоке содержимого.

```csharp
extGStateDict.Add("GS0", graphicsState); // "GS0" becomes the identifier you’ll use later
```

*Best practice*: Используйте понятную схему именования (`GS0`, `GS_Watermark` и т.д.), чтобы управлять несколькими состояниями без путаницы.

## Шаг 6: Применить графическое состояние к содержимому страницы (необязательно)

Если нужно применить новую непрозрачность к существующим элементам страницы, необходимо изменить поток содержимого страницы. Ниже простой пример, который добавляет полупрозрачный прямоугольник поверх страницы.

```csharp
// Build a content stream that sets the graphics state and draws a rectangle
var contentBuilder = new Aspose.Pdf.Operators.ContentBuilder(pdfDocument);
contentBuilder.SetGraphicsState("GS0");
contentBuilder.SetFillColor(Color.FromRgb(255, 0, 0)); // red fill
contentBuilder.Rectangle(100, 500, 200, 100); // x, y, width, height
contentBuilder.FillPath();

firstPage.Contents.Add(contentBuilder);
```

*Why it works*: Оператор `SetGraphicsState` сообщает интерпретатору PDF использовать параметры, определённые в `GS0`, для всех последующих команд рисования. Прямоугольник появляется с 50 % непрозрачностью заливки, при этом обводка остаётся полностью непрозрачной.

## Шаг 7: Сохранить изменённый PDF

Наконец, запишите изменения обратно на диск.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Полученный `output.pdf` содержит новое графическое состояние, и любой контент, ссылающийся на `GS0`, будет отображаться с заданной прозрачностью.

---

![Diagram showing PDF transparency change](/images/pdf-transparency-before-after.png "PDF page before and after applying custom graphics state")
*Текст alt изображения (для SEO и доступности):* **пример изменения прозрачности PDF – оригинальная и изменённая страница**

## Полный рабочий пример

Объединив всё вместе, получаем единый исполняемый пример, который изменяет прозрачность PDF и добавляет полупрозрачный прямоугольник.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;
using System.Collections.Generic;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;

class ChangePdfTransparency
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // Create a new graphics state (opacity + blend mode)
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) graphicsState.Add(e);

            // Register the graphics state as GS0
            extGStateDict.Add("GS0", graphicsState);

            // OPTIONAL: draw a semi‑transparent rectangle using GS0
            var builder = new ContentBuilder(pdfDocument);
            builder.SetGraphicsState("GS0");
            builder.SetFillColor(Color.FromRgb(255, 0, 0)); // red
            builder.Rectangle(100, 500, 200, 100);
            builder.FillPath();
            firstPage.Contents.Add(builder);

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF transparency changed and saved to output.pdf");
    }
}
```

### Ожидаемый результат

* Файл `output.pdf` создаётся в указанной папке.
* При открытии PDF вы увидите красный прямоугольник, заливка которого 50 % прозрачна, а граница остаётся полностью непрозрачной.
* Любые другие объекты, ссылающиеся на `GS0` (например, водяные знаки), унаследуют ту же непрозрачность и режим наложения.

## Часто задаваемые вопросы и обработка граничных случаев

| Question | Answer |
|----------|--------|
| **Можно ли изменить только непрозрачность обводки?** | Установите `CA` в нужное значение и оставьте `ca` равным `1`. |
| **Какие режимы наложения поддерживаются?** | Все стандартные режимы наложения PDF (`Normal`, `Multiply`, `Screen`, `Overlay` и т.д.) принимаются через запись `BM`. |
| **Нужно ли очищать словарь после использования?** | Нет. Объекты `CosPdfDictionary` управляются Aspose.Pdf и записываются в файл при вызове `Save`. |
| **Как это работает с зашифрованными PDF?** | Загрузите документ с правильным паролем (`new Document(path, password)`). Манипуляции с графическим состоянием работают так же после расшифровки документа в памяти. |
| **Можно ли применить одно и то же графическое состояние к нескольким страницам?** | Да. Добавьте запись `GS0` в словарь `ExtGState` каждой страницы, либо создайте один общий словарь в глобальных ресурсах документа и ссылаться на него с каждой страницы. |

## Советы и лучшие практики

* **Pro tip:** Делайте имена графических состояний короткими, но описательными (`GS_Watermark`, `GS_Overlay`). Это предотвращает конфликты имён и упрощает отладку.
* **Watch out for:** Случайное перезаписывание существующей записи `ExtGState`. Всегда проверяйте `resourcesEditor.ContainsKey("ExtGState")` перед созданием нового словаря.
* **Performance note:** Модификация низкоуровневых объектов COS происходит быстро, но если нужно обработать тысячи страниц, рассмотрите пакетную обработку изменений, чтобы снизить нагрузку на память.

## Следующие шаги

Теперь, когда вы знаете, как **изменять прозрачность PDF**, можете изучить смежные темы, такие как:

* Добавление **водяных знаков** с пользовательской непрозрачностью (`PDF opacity C#`).
* Использование **разных режимов наложения** для художественных эффектов (`blend mode PDF`).
* Создание переиспользуемых **библиотек графических состояний** для масштабной генерации документов (`Aspose.Pdf graphics state`).

Экспериментируйте с различными значениями `ca` и `CA`, либо замените красный прямоугольник изображением или текстовым наложением. Принципы остаются теми же — просто ссылаться на графическое состояние `GS0` перед рисованием нового контента.

---

*Вы научились изменять прозрачность PDF с помощью Aspose.Pdf в C#. Применяйте эти техники для улучшения отчётов, счетов‑фактур или любого PDF‑вывода, где важны визуальные нюансы.*

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Изменить непрозрачность PDF с помощью Aspose.PDF – Полное руководство C#](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Изменить непрозрачность PDF в C# – Полное руководство Aspose](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Добавить прозрачность в PDF с помощью Aspose – Полное руководство C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}