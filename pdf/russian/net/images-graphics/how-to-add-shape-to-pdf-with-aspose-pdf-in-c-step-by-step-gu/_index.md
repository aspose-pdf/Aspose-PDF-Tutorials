---
category: general
date: 2026-06-18
description: Как добавить форму в PDF с помощью Aspose.PDF в C# – загрузить PDF, нарисовать
  прямоугольник и сохранить его.
draft: false
keywords:
- how to add shape to pdf
- load pdf document in c#
- how to draw shapes in pdf
- aspose pdf add rectangle
language: ru
og_description: Как добавить форму в PDF с помощью Aspose.PDF на C#. Узнайте, как
  загрузить PDF‑документ, нарисовать прямоугольник и сохранить обновлённый файл.
og_title: Как добавить фигуру в PDF с помощью Aspose.PDF на C#
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  headline: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  type: TechArticle
- description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  name: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  steps:
  - name: What if I need to draw on multiple pages?
    text: Simply loop over `pdfDoc.Pages` and call `AddRectangle` (or any other shape)
      for each page. Remember to adjust coordinates if pages have different sizes.
  - name: Can I fill the rectangle with a color?
    text: Absolutely. Change `FillColor` from `Transparent` to any `Color` you like,
      e.g., `Color.Yellow`. The shape will appear as a solid block.
  - name: Does this work with password‑protected PDFs?
    text: 'Aspose.PDF can open encrypted files if you supply the password:'
  - name: How to add a rectangle with rounded corners?
    text: Use the `RoundedRectangle` class instead of `Rectangle`. The rest of the
      steps stay identical.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Как добавить фигуру в PDF с помощью Aspose.PDF на C# — пошаговое руководство
url: /ru/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить форму в PDF с помощью Aspose.PDF на C# – Полный учебник

Вы когда‑нибудь задумывались **как добавить форму в PDF** без борьбы с низкоуровневыми потоками байтов? Во многих реальных приложениях вам нужно выделить область, подчеркнуть пункт или просто нарисовать ограничивающий прямоугольник для поля подписи. Хорошая новость в том, что Aspose.PDF делает это проще простого. В этом руководстве мы загрузим PDF‑документ на C#, нарисуем прямоугольник и сохраним результат — ничего лишнего, ничего недостающего.

Мы пройдемся по каждой строке кода, объясним *почему* каждый элемент важен и даже покажем быстрый способ проверить, что форма действительно оказалась там, где вы ожидаете. К концу вы будете уверенно знать **как рисовать формы в PDF** файлах, и у вас будет переиспользуемый фрагмент, который можно вставить в любой .NET‑проект.

## Требования

- **.NET 6.0** (или любую недавнюю версию .NET), установленную на вашем компьютере.  
- **Действительная лицензия Aspose.PDF for .NET** (или бесплатный ключ оценки).  
- Visual Studio 2022, Rider или любой предпочитаемый вами редактор.  
- Существующий PDF‑файл (`input.pdf`), размещённый в папке, к которой вы можете обратиться.

> **Совет:** Если вы просто тестируете, бесплатная оценочная версия полностью подходит — она добавляет небольшой водяной знак, но в остальном работает как полноценный продукт.

## Шаг 1: Настройка проекта и импорт пространств имён

Сначала создайте новый консольный проект (или добавьте в существующий) и подключите необходимые пространства имён.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;   // Required for shape classes
```

Почему это важно: `Aspose.Pdf` предоставляет основную модель документа, а `Aspose.Pdf.Drawing` содержит класс формы `Rectangle`, который мы будем использовать позже. Без последнего компилятор будет жаловаться, что `Rectangle` не определён.

## Шаг 2: Загрузка PDF‑документа в C#

Теперь мы действительно **загружаем PDF‑документ в C#**. Это первая операция, которую вы всегда выполняете, когда собираетесь изменить существующий файл.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";
Document pdfDoc = new Document(inputPath);
Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");
```

*Объяснение*:  
- `Document` — представление Aspose всего файла.  
- Передача полного пути в конструктор считывает файл в память.  
- Строка `Console.WriteLine` необязательна, но удобна для отладки — если количество страниц равно нулю, вы сразу знаете, что что‑то пошло не так.

## Шаг 3: Определение формы Rectangle

Здесь мы подходим к сути **как добавить форму в PDF**. Мы создаём объект `Rectangle`, который задаёт позицию и размер, используя систему координат, где (0,0) — левый нижний угол страницы.

```csharp
// Step 3: Define a rectangle (left, bottom, right, top)
Rectangle rect = new Rectangle(0, 0, 200, 100)
{
    // Optional styling – you can tweak these as needed
    FillColor = Color.Transparent,          // No fill, just the border
    Border = new Border(BorderStyle.Solid, 2, Color.Red)
};
```

Почему мы устанавливаем `FillColor` в прозрачный: в большинстве случаев нужен лишь контур (подумайте о выделяющем прямоугольнике). Свойство `Border` позволяет задать толщину и цвет; красный делает прямоугольник заметным на обычной белой странице.

## Шаг 4: Проверка, что форма помещается внутри границ страницы

Прежде чем **добавлять прямоугольник**, полезно убедиться, что форма не выходит за пределы страницы. Aspose предоставляет `ValidateShapeBounds` именно для этой цели.

```csharp
// Step 4: Validate that the rectangle fits on the first page
bool fits = pdfDoc.Pages[1].ValidateShapeBounds(rect);
if (!fits)
{
    Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
    // Simple fallback: shrink to fit the page width
    rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
    rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
}
```

*Почему*: попытка рисовать за пределами страницы может вызвать артефакты отображения или даже бросить исключение. Эта проверка делает руководство надёжным для PDF любого размера.

## Шаг 5: Добавление прямоугольника на нужную страницу

Теперь мы наконец **добавляем форму в PDF**. Метод `AddRectangle` присоединяет форму к коллекции аннотаций страницы, что означает, что PDF‑просмотрщики отобразят её как любой другой рисунок.

```csharp
// Step 5: Add the rectangle to the first page
pdfDoc.Pages[1].AddRectangle(rect);
Console.WriteLine("Rectangle added to page 1.");
```

Если нужно обратиться к другой странице, просто замените индекс `1` на нужный номер страницы (Aspose использует индексацию, начинающуюся с 1).

## Шаг 6: Сохранение изменённого PDF

Последний шаг — записать изменения обратно на диск. Вы можете перезаписать оригинальный файл или создать новый — здесь мы создадим `output.pdf`.

```csharp
// Step 6: Save the updated PDF
string outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved as {outputPath}");
```

*Что ожидать*: откройте `output.pdf` в Adobe Reader или любом другом просмотрщике, и вы увидите чёткий красный прямоугольник, привязанный к левому нижнему углу первой страницы.

![Diagram showing rectangle added to PDF](https://example.com/rectangle-diagram.png "пример как добавить форму в pdf")

*Alt text*: "как добавить форму в pdf – прямоугольник, нарисованный на первой странице PDF‑файла"

## Шаг 7: Полный рабочий пример (готовый к копированию)

Ниже полная программа, которую можно сразу скомпилировать и запустить. Не забудьте заменить `YOUR_DIRECTORY` на реальный путь к папке на вашем компьютере.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;   // For color definitions

namespace PdfShapeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the PDF document in C#
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document pdfDoc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");

            // Define the rectangle shape
            Rectangle rect = new Rectangle(0, 0, 200, 100)
            {
                FillColor = Color.Transparent,
                Border = new Border(BorderStyle.Solid, 2, Color.Red)
            };

            // Validate bounds on the first page
            if (!pdfDoc.Pages[1].ValidateShapeBounds(rect))
            {
                Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
                rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
                rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
            }

            // Add the rectangle (how to add shape to pdf)
            pdfDoc.Pages[1].AddRectangle(rect);
            Console.WriteLine("Rectangle added to page 1.");

            // Save the modified PDF
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved as {outputPath}");
        }
    }
}
```

Запустите программу, откройте `output.pdf`, и вы увидите красный прямоугольник точно там, где мы его разместили. Если нужна другая форма — эллипс, линия или полигон — просто замените `Rectangle` на `Ellipse`, `Line` или `Polygon`, сохранив тот же процесс. Это по сути **как рисовать формы в pdf** с помощью Aspose.

## Часто задаваемые вопросы и особые случаи

### Что если нужно рисовать на нескольких страницах?
Просто пройдитесь в цикле по `pdfDoc.Pages` и вызовите `AddRectangle` (или любую другую форму) для каждой страницы. Не забудьте скорректировать координаты, если размеры страниц различаются.

```csharp
foreach (Page page in pdfDoc.Pages)
{
    page.AddRectangle(rect);
}
```

### Можно ли заполнить прямоугольник цветом?
Конечно. Измените `FillColor` с `Transparent` на любой `Color`, который вам нужен, например `Color.Yellow`. Форма будет выглядеть как сплошной блок.

### Работает ли это с PDF, защищёнными паролем?
Aspose.PDF может открыть зашифрованные файлы, если вы предоставите пароль:

```csharp
Document pdfDoc = new Document(inputPath, new LoadOptions { Password = "mySecret" });
```

### Как добавить прямоугольник со скруглёнными углами?
Используйте класс `RoundedRectangle` вместо `Rectangle`. Остальные шаги остаются теми же.

## Итоги

Мы рассмотрели **как добавить форму в PDF** с помощью Aspose.PDF на C#. Процесс сводится к:

1. **Загрузить PDF‑документ в C#** — создать объект `Document`.  
2. **Определить прямоугольник** (или любую другую форму).  
3. **Проверить границы** чтобы избежать выхода за пределы.  
4. **Добавить прямоугольник** на целевую страницу.  
5. **Сохранить** изменённый файл.

Это весь рабочий процесс для **aspose pdf add rectangle**, и теперь у вас есть шаблон, который можно адаптировать под круги, линии или пользовательские полигоны.

## Что дальше?

- **Изучить другие primitives рисования**: `Ellipse`, `Line`, `Polygon`.  
- **Добавить текстовые аннотации** рядом с вашими формами для более интерактивного опыта.  
- **Комбинировать с полями формы PDF**, если вы создаёте заполняемый контракт.  
- **Ознакомиться с функциями конвертации PDF от Aspose**, чтобы превратить аннотированные PDF в изображения для миниатюр предварительного просмотра.

Не стесняйтесь экспериментировать — возможно, нарисовать водяной знак, выделить ячейку таблицы или обвести поле подписи. API гибок, и теперь вы знаете основы.

Счастливого кодинга, и пусть ваши PDF всегда выглядят именно так, как вы задумали!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создать PDF‑документ с Aspose.PDF – добавить страницу, форму и сохранить](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Как добавить и настроить номера страниц в PDF с помощью Aspose.PDF для .NET | Руководство по манипуляции документами](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Как добавить гиперссылки в PDF с помощью Aspose.PDF для .NET: Полное руководство](/pdf/english/net/bookmarks-navigation/add-hyperlinks-pdf-aspose-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}