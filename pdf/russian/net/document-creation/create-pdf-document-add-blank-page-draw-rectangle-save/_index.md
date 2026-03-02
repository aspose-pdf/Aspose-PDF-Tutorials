---
category: general
date: 2026-03-01
description: Создайте PDF‑документ с помощью Aspose.PDF в C#. Узнайте, как добавить
  пустую страницу, нарисовать прямоугольник в PDF и быстро сохранить файл PDF.
draft: false
keywords:
- create pdf document
- add blank page
- draw rectangle pdf
- add rectangle pdf
- save pdf file
language: ru
og_description: Создайте PDF‑документ с помощью Aspose.PDF. Пошаговое руководство
  по добавлению пустой страницы, рисованию прямоугольника в PDF и эффективному сохранению
  PDF‑файла.
og_title: Создать PDF‑документ – добавить пустую страницу, нарисовать прямоугольник
  и сохранить
tags:
- pdf
- csharp
- aspose
- document-generation
title: Создать PDF‑документ – добавить пустую страницу, нарисовать прямоугольник и
  сохранить
url: /ru/net/document-creation/create-pdf-document-add-blank-page-draw-rectangle-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать PDF‑документ – добавить пустую страницу, нарисовать прямоугольник и сохранить

Когда‑то вам нужно **создать PDF‑документ** на C#, но вы не знаете, с чего начать? Вы не одиноки — многие разработчики сталкиваются с тем же самым, когда впервые автоматизируют генерацию отчётов. Хорошая новость: с Aspose.PDF вы можете за несколько строк кода создать PDF, добавить пустую страницу, нарисовать форму‑прямоугольник и, наконец, сохранить файл PDF.

В этом руководстве мы пройдём каждый шаг, объясним **почему** каждый вызов важен и предоставим готовый к запуску пример кода. К концу вы будете знать, как **добавить пустую страницу**, **нарисовать прямоугольник PDF** и **сохранить PDF‑файл**, не просеивая бесконечные документы.

## Требования

- .NET 6.0 или новее (подойдёт любой современный рантайм)
- NuGet‑пакет Aspose.PDF for .NET (`Install-Package Aspose.PDF`)
- Базовое понимание синтаксиса C# (никаких продвинутых трюков)

Если всё это уже есть — отлично, приступаем.

## Шаг 1 – Создать PDF‑документ

Первое, что нужно сделать, — создать экземпляр класса `Document`. Представьте его как открытие чистой тетради, в которой позже будут находиться все добавленные страницы.

```csharp
using Aspose.Pdf;

// Step 1: Create a new PDF document
var pdfDocument = new Document();
```

> **Почему это важно:** `Document` — корневой объект; без него нельзя добавить страницы или графику. Создание документа также выделяет внутренние структуры, необходимые Aspose для эффективного управления ресурсами.

## Шаг 2 – Добавить пустую страницу

PDF без страниц — всё равно что книга без листов, то есть совершенно бесполезна. Добавление **пустой страницы** даёт вам холст для рисования.

```csharp
// Step 2: Add a blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Совет:** Метод `Add()` возвращает только что созданный объект `Page`, поэтому вы можете сразу выполнять дальнейшие операции без отдельного поиска.

## Шаг 3 – Определить форму прямоугольника

Теперь задаём координаты прямоугольника. Aspose использует систему координат, где начало (0,0) находится в левом нижнем углу страницы.

```csharp
// Step 3: Define a rectangle shape (left, bottom, right, top)
Rectangle rectangle = new Rectangle(50, 50, 550, 800);
```

> **Что означают числа:**  
> - **Left** = 50 пунктов от левого края  
> - **Bottom** = 50 пунктов от нижнего края  
> - **Right** = 550 пунктов от левого края (ширина ≈ 500)  
> - **Top** = 800 пунктов от нижнего края (высота ≈ 750)

Если представить это на стандартной странице формата A4, прямоугольник окажется удобно в центре, оставив приятные отступы со всех сторон.

![Диаграмма, показывающая прямоугольник внутри PDF‑страницы](image-placeholder.png){: .align-center alt="пример создания pdf документа с прямоугольником"}

## Шаг 4 – Проверить, помещается ли прямоугольник на страницу

Прежде чем рисовать, разумно убедиться, что форма находится внутри границ страницы. Это предотвращает исключения во время выполнения и сохраняет аккуратность макета.

```csharp
// Step 4: Verify the rectangle fits inside the page boundaries
if (page.IsInside(rectangle))
{
    // Continue only if the rectangle is fully inside the page
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page bounds.");
}
```

> **Пограничный случай:** Если позже вы переключитесь на пользовательский размер страницы, эта проверка автоматически подстроится, избавив вас от загадочных ошибок обрезки.

## Шаг 5 – Нарисовать прямоугольник в PDF

После проверки мы можем **нарисовать прямоугольник PDF** с синей обводкой. Aspose позволяет передать `Color` напрямую, делая вызов лаконичным.

```csharp
// Step 5: Draw the rectangle on the page using a blue outline
page.AddRectangle(rectangle, Color.Blue);
```

> **Почему синяя обводка?** Это просто наглядный пример. Вы можете заменить `Color.Blue` на любой другой `Color`, либо заполнить форму, используя `page.AddRectangle(rectangle, Color.Blue, Color.LightGray)`.

## Шаг 6 – Сохранить PDF‑файл

Последний шаг — записать документ на диск. Здесь происходит операция **save PDF file**.

```csharp
// Step 6: Save the PDF to a file
pdfDocument.Save(@"C:\Temp\shape.pdf");
```

> **Подсказка:** Во время тестирования используйте абсолютный путь, а при развертывании в веб‑ или облачной среде переключитесь на относительный путь или поток.

### Полный рабочий пример

Объединив всё вместе, получаем полностью готовую к запуску программу:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Graphics; // Needed for Color

class Program
{
    static void Main()
    {
        // 1️⃣ Create PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Add a blank page
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Define rectangle (left, bottom, right, top)
        Rectangle rectangle = new Rectangle(50, 50, 550, 800);

        // 4️⃣ Verify it fits inside the page
        if (!page.IsInside(rectangle))
        {
            Console.WriteLine("Rectangle does not fit the page.");
            return;
        }

        // 5️⃣ Draw rectangle with a blue outline
        page.AddRectangle(rectangle, Color.Blue);

        // 6️⃣ Save PDF file
        pdfDocument.Save(@"C:\Temp\shape.pdf");

        Console.WriteLine("PDF created successfully at C:\\Temp\\shape.pdf");
    }
}
```

**Ожидаемый результат:** Откройте `shape.pdf` — вы увидите одну страницу с прямоугольником, обведённым синей линией, центрированным, с отступом в 50 пунктов слева и снизу, а также 50 пунктов справа и сверху.

## Часто задаваемые вопросы и варианты

### Что если нужно **добавить прямоугольник PDF** с цветом заливки?
Замените вызов `AddRectangle` на перегрузку, принимающую цвет заливки:

```csharp
page.AddRectangle(rectangle, Color.Blue, Color.LightYellow);
```

### Можно ли **добавлять пустую страницу** несколько раз?
Конечно. Вызывайте `pdfDocument.Pages.Add()` столько раз, сколько требуется. Каждый вызов возвращает новый объект `Page`, которым можно управлять независимо.

### Как изменить размер страницы перед рисованием?
Установите свойство `PageSize`, когда создаёте страницу:

```csharp
Page page = pdfDocument.Pages.Add();
page.PageInfo.Width = 595;   // A4 width in points
page.PageInfo.Height = 842;  // A4 height in points
```

Не забудьте повторно выполнить проверку границ (`IsInside`) после изменения размеров.

### Есть ли способ **сохранить PDF‑файл** в поток памяти для веб‑ответов?
Да — замените путь к файлу на `MemoryStream`:

```csharp
using var ms = new MemoryStream();
pdfDocument.Save(ms);
byte[] pdfBytes = ms.ToArray(); // send this over HTTP
```

## Заключение

Мы только что продемонстрировали, как **создать PDF‑документ**, **добавить пустую страницу**, **нарисовать прямоугольник PDF**, **добавить прямоугольник PDF** и, наконец, **сохранить PDF‑файл** с помощью Aspose.PDF for .NET. Шаги предельно просты, чтобы вы могли скопировать‑вставить, запустить и сразу увидеть результат.

Дальше вы можете исследовать добавление текста, изображений или даже таблиц на ту же страницу — каждый процесс следует той же схеме «создать → добавить → проверить → нарисовать → сохранить». Экспериментируйте с разными цветами, толщиной линий или ориентацией страниц, чтобы PDF стал действительно вашим.

Если возникнут трудности, проверьте, что версия NuGet‑пакета Aspose.PDF соответствует целевой платформе, и убедитесь, что папка вывода существует перед вызовом `Save`. Приятного создания PDF!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}