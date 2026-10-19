---
category: general
date: 2026-06-21
description: Рисуем прямоугольник в PDF с помощью C#. Узнайте, как загрузить PDF‑документ,
  создать чёрную аннотацию‑прямоугольник и эффективно сохранить изменённый PDF.
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: ru
og_description: Нарисовать прямоугольник в PDF на C#, загрузив PDF‑документ, создав
  чёрную аннотацию‑прямоугольник и сохранив изменённый PDF. Полный код включён.
og_title: Рисуем прямоугольник в PDF с помощью C# – полный учебник по программированию
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: Рисуем прямоугольник в PDF с помощью C# – пошаговое руководство
url: /ru/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Нарисовать прямоугольник в PDF с помощью C# – Полный учебный материал

Когда‑нибудь вам нужно было **draw rectangle on PDF** файлы из .NET приложения, но вы не знали, с чего начать? Вы не одиноки. Будь то выделение раздела, редактирование конфиденциальных данных или просто добавление визуального указателя, изучение того, как *draw rectangle on PDF* программно, может сэкономить вам часы ручного редактирования.

В этом руководстве мы пройдём практический пример, который **loads a PDF document**, **creates a black rectangle**, а затем **saves the modified PDF**. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой C#‑проект — без загадок, только чистый код и объяснения.

## Что рассматривается в этом руководстве

- Как **load pdf document** с помощью библиотеки Aspose.PDF for .NET  
- Определение координат прямоугольника и проверка, что он находится внутри границ страницы  
- Использование метода **add black rectangle** для аннотирования страницы  
- **Save modified pdf** в новое место файла  
- Обработка граничных случаев (многостраничные документы, прямоугольники за пределами, пользовательские цвета)  

Никаких внешних инструментов, никаких расплывчатых ссылок — только полноценный, исполняемый пример, который можно скопировать‑вставить.

## Предварительные требования

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

1. .NET 6.0 SDK (или любая современная версия .NET) установлен  
2. Ссылка на **Aspose.PDF for .NET** (доступно через NuGet: `Install-Package Aspose.PDF`)  
3. Существующий PDF‑файл (`input.pdf`) в папке, к которой у вас есть права чтения/записи  

Вот и всё. Если вы знакомы с базовым синтаксисом C#, вы готовы к работе.

## Шаг 1: Загрузка PDF‑документа

Первое, что нам нужно, — это вызов **load pdf document**. Класс `Document` из Aspose.PDF принимает путь к файлу и читает весь документ в память.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*Why this matters*: Загрузка PDF даёт доступ к его страницам, метаданным и поверхности рисования. Без этого шага вы не сможете разместить какие‑либо фигуры.

## Шаг 2: Выбор целевой страницы

Страницы PDF в Aspose нумеруются с 1, поэтому первая страница имеет индекс 1. Получите страницу, которую хотите аннотировать — обычно это первая страница для быстрой демонстрации.

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

Если нужно работать с другой страницей, просто измените индекс. Не забудьте проверить, что указанный индекс существует, чтобы избежать `ArgumentOutOfRangeException`.

## Шаг 3: Определение геометрии прямоугольника

Прямоугольник задаётся координатами нижнего‑левого (X,Y) и верхнего‑правого (X,Y) углов. Структура `Rectangle` хранит их как `LLX`, `LLY`, `URX`, `URY`.

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

Не стесняйтесь менять эти числа — `100,100` размещает нижний‑левый угол на 100 пунктов от левого и нижнего краёв, а `300,300` задаёт верхний‑правый угол на 300 пунктов от краёв.

## Шаг 4: Проверка, что прямоугольник помещается на странице

Попытка нарисовать за пределами страницы будет либо проигнорирована, либо вызовет исключение, в зависимости от версии библиотеки. Быстрая проверка делает ваш код надёжнее.

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*Pro tip*: Если планируется поддержка PDF‑файлов разных размеров, вычисляйте прямоугольник на основе процента от ширины/высоты страницы, а не абсолютных пунктов.

## Шаг 5: Добавление чёрной аннотации‑прямоугольника

Теперь самая интересная часть — **add black rectangle** на страницу. Aspose предоставляет `AddRectangle`, который принимает геометрию и `Color`. Мы используем `Color.Black`, чтобы **create black rectangle**.

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

Эта единственная строка делает основную работу: создаёт объект аннотации, задаёт цвет границы чёрным и вставляет его в коллекцию аннотаций страницы.

Если когда‑нибудь понадобится иной заливка или стиль границы, изучите перегрузку, принимающую объект `Annotation`, где можно настроить толщину линии, пунктирный шаблон или даже непрозрачность.

## Шаг 6: Сохранение изменённого PDF

Наконец, сохраняем изменения с помощью **save modified pdf**. Можно перезаписать оригинал или записать в новый файл — здесь мы создаём выходной файл.

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

Это весь процесс. Запустите программу и откройте `output.pdf`; вы должны увидеть сплошной чёрный прямоугольник в указанном месте.

## Полный рабочий пример

Ниже представлено автономное консольное приложение, объединяющее все шаги. Скопируйте его в новый `.csproj` и нажмите **Run**.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**Expected output** в консоли:

```
Successfully drew rectangle on PDF and saved the file.
```

Откройте `output.pdf`, и вы увидите чёрный прямоугольник, расположенный по заданным координатам.

## Обработка распространённых вариантов

| Ситуация | Что изменить | Почему |
|-----------|----------------|-----|
| **Multiple pages** | Loop through `pdfDocument.Pages` and apply the same logic to each `Page` object. | Позволяет выполнять пакетную аннотацию по всему документу. |
| **Different colors** | Replace `Color.Black` with `Color.Red` or any `System.Drawing.Color`. | Полезно для выделения, а не для редактирования. |
| **Transparent fill** | Use `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }`. | Создаёт полупрозрачный налёт вместо сплошного блока. |
| **Dynamic rectangle size** | Compute `URX` and `URY` based on `PageInfo.Width * 0.5` etc. | Делает прямоугольник адаптивным к различным размерам страниц. |
| **Error handling** | Wrap the whole block in `try…catch` and log `Aspose.Pdf.IOException`. | Предотвращает падения, когда исходный файл отсутствует или заблокирован. |

Эти настройки показывают, как можно **create black rectangle** аннотации в разных контекстах без переписывания основной логики.

## Полезные советы и подводные камни

- **Dispose the Document**: Хотя Aspose.PDF реализует `IDisposable`, шаблон `using` не обязателен для короткоживущих консольных приложений. В длительно работающих сервисах оберните `Document` в `using`, чтобы своевременно освобождать нативные ресурсы.  
- **Coordinate System**: Координаты PDF начинаются в нижнем‑левом углу. Если вы привыкли к системе с началом в верхнем‑левом (например, WinForms), потребуется инвертировать ось Y: `pageHeight - y`.  
- **Performance**: Добавление аннотаций в очень большие PDF может потреблять много памяти. Рассмотрите обработку страниц порциями или использование `PdfFileEditor` для более лёгких правок.  
- **Legal**: Убедитесь, что у вас есть права на изменение исходного PDF — некоторые документы защищены от редактирования.

## Заключение

Мы только что продемонстрировали, как **draw rectangle on PDF** с помощью C# — начиная с **load pdf document**, определяя геометрию, **add black rectangle** и, наконец, **save modified pdf**. Пример полностью готов, исполняем и адаптируем к реальным сценариям, таким как пакетная обработка или пользовательское стилизование.

Дальше вы можете попробовать добавлять другие типы аннотаций (текст, выделения) или объединять несколько PDF после аннотирования. Шаги **load pdf document** и **save modified pdf** остаются теми же, так что вы можете уверенно расширять эту схему.

Есть свой вариант? Поделитесь в комментариях, и удачной разработки!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, показанные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create Filled Rectangle Object in PDF using Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}