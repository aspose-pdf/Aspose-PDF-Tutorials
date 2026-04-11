---
category: general
date: 2026-04-10
description: Быстро создайте PDF‑документ на C#. Узнайте, как добавить пустую страницу
  в PDF, нарисовать прямоугольник, добавить форму прямоугольника и вставить его в
  PDF с понятным кодом.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- add rectangle shape
- add rectangle to pdf
language: ru
og_description: Создайте PDF‑документ на C# за считанные минуты. Это руководство показывает,
  как добавить пустую страницу PDF, нарисовать прямоугольник в PDF и добавить форму
  прямоугольника с помощью простого кода.
og_title: Создание PDF‑документа C# – Полный учебник
tags:
- C#
- PDF
- Aspose.PDF
- Document Generation
title: Создание PDF‑документа на C# – Пошаговое руководство по добавлению пустой страницы
  и рисованию прямоугольника
url: /ru/net/document-creation/create-pdf-document-c-step-by-step-guide-to-add-a-blank-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF документа C# – Полный пошаговый гид

Когда‑нибудь вам нужно было **create PDF document C#** для функции отчётности, но вы не знали, с чего начать? Вы не одиноки. Во многих проектах первая преграда — получить чистый PDF с пустой страницей, а затем нарисовать простую графику, например прямоугольник.  

В этом руководстве мы сразу решим эту задачу: вы увидите, как добавить пустую страницу PDF, нарисовать rectangle PDF и, наконец, добавить форму прямоугольника в файл — всё это с помощью нескольких строк C#. К концу у вас будет готовый к использованию `shapes.pdf`, который можно открыть в любом просмотрщике.

## Чего вы научитесь

- Как инициализировать PDF документ с помощью Aspose.PDF for .NET.  
- Точные шаги для **add blank page pdf** и позиционирования прямоугольника внутри него.  
- Почему класс `Rectangle` — правильный выбор для рисования фигур.  
- Распространённые подводные камни, такие как несоответствие размеров страниц, и как их избежать.  

Никаких внешних инструментов, никакой магии — только чистый C# код, который можно скопировать и вставить в консольное приложение.

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+).  
- Пакет NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`).  
- Базовое понимание синтаксиса C# (переменные, операторы `using` и т.д.).  

> **Pro tip:** Если вы используете Visual Studio, менеджер пакетов NuGet позволяет установить Aspose.PDF одним щелчком.

## Шаг 1: Инициализация PDF документа

Создание PDF начинается с объекта `Document`. Считайте его холстом, который будет содержать каждую страницу, изображение или форму, которую вы добавите позже.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Initialise a new PDF document – this is the core of create pdf document c#
var pdfDocument = new Document();
```

Класс `Document` предоставляет доступ к коллекции `Pages`, где мы позже **add blank page pdf**.

## Шаг 2: Добавление пустой страницы в документ

PDF без страниц по сути пуст. Добавление страницы так же просто, как вызов `pdfDocument.Pages.Add()`. Новая страница наследует размер по умолчанию (A4), если не указано иное.

```csharp
// Add a fresh, blank page – this satisfies the add blank page pdf requirement
Page page = pdfDocument.Pages.Add();
```

> **Почему это важно:** Сначала добавив страницу, вы гарантируете, что любые последующие команды рисования будут иметь поверхность для отрисовки. Пропуск этого шага приведёт к ошибке выполнения при попытке нарисовать прямоугольник.

## Шаг 3: Определение границ прямоугольника

Теперь мы **draw rectangle pdf**, создавая объект `Rectangle`. Конструктор принимает координаты нижнего‑левого угла X/Y, а затем ширину и высоту. В нашем примере мы хотим прямоугольник, который удобно вписывается в страницу, оставляя небольшой отступ.

```csharp
// Rectangle coordinates: (0,0) is the lower‑left corner of the page
// Width = 500, Height = 700 – fits comfortably on an A4 page
var rectangle = new Rectangle(0, 0, 500, 700);
```

Если нужен другой размер, просто измените значения ширины/высоты. Начало координат прямоугольника (0,0) совпадает с левым нижним углом страницы, что часто сбивает с толку новичков.

## Шаг 4: Добавление формы прямоугольника на страницу

Когда объект прямоугольника готов, мы можем **add rectangle shape** на страницу. Метод `AddRectangle` рисует контур, используя текущее состояние графики (по умолчанию — тонкая чёрная линия).

```csharp
// Add the rectangle shape – this completes the add rectangle to pdf step
page.AddRectangle(rectangle);
```

Вы можете настроить внешний вид, изменив объект `Graphics` перед вызовом `AddRectangle`, например, задав `LineWidth` или `Color`. Для заливки используйте `page.AddAnnotation(new SquareAnnotation(...))`, но это выходит за рамки данного простого руководства.

## Шаг 5: Сохранение PDF файла

Наконец, сохраняем документ на диск. Выберите папку, в которую у вас есть права записи, и дайте файлу осмысленное имя, например `shapes.pdf`.

```csharp
// Save the PDF – you’ll find shapes.pdf in the specified directory
pdfDocument.Save(@"C:\Temp\shapes.pdf");
```

> **Note:** Оператор `using` из оригинального фрагмента здесь не обязателен, потому что `Document` реализует `IDisposable`. Тем не менее, обёртывание его в `using` — хорошая привычка для очистки ресурсов, особенно в больших приложениях.

## Полный рабочий пример

Собрав всё вместе, получаем автономную консольную программу, которую можно сразу запустить:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Step 2: Add a blank page to the document
                Page page = pdfDocument.Pages.Add();

                // Step 3: Define a rectangle that fits inside the page bounds (0,0 to 500,700)
                var rectangle = new Rectangle(0, 0, 500, 700);

                // Step 4: Add the rectangle shape to the page
                page.AddRectangle(rectangle);

                // Step 5: Save the PDF file
                string outputPath = @"C:\Temp\shapes.pdf";
                pdfDocument.Save(outputPath);

                Console.WriteLine($"PDF created successfully at {outputPath}");
            }
        }
    }
}
```

**Ожидаемый результат:** После запуска программы откройте `C:\Temp\shapes.pdf`. Вы увидите одну страницу с чёрным контуром прямоугольника, расположенного в левом нижнем углу, размером ровно 500 × 700 пунктов.

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| *Могу ли я изменить размер страницы перед добавлением прямоугольника?* | Да. Создайте `Page` с пользовательскими размерами: `var page = pdfDocument.Pages.Add(); page.PageInfo.Width = 600; page.PageInfo.Height = 800;` |
| *Что делать, если нужен заполненный прямоугольник?* | Используйте объект `Graphics`: `page.Canvas.Rectangle(rectangle, Color.Blue, Color.LightBlue);` |
| *Aspose.PDF бесплатен?* | Он предлагает **free trial** с полной функциональностью; для использования в продакшене требуется коммерческая лицензия. |
| *Как добавить несколько прямоугольников?* | Просто повторите шаги 3‑4 с разными экземплярами `Rectangle` или измените координаты. |

## Следующие шаги

Теперь, когда вы знаете, как **create pdf document c#**, **add blank page pdf** и **draw rectangle pdf**, вы можете изучить:

- Добавление текста внутри прямоугольника (`TextFragment`, `page.Paragraphs.Add`).  
- Вставка изображений (`page.Resources.Images.Add`) для создания более насыщенных отчётов.  
- Экспорт PDF в другие форматы, такие как PNG или DOCX, с помощью API конвертации Aspose.  

Все эти темы естественно вытекают из основы **add rectangle to pdf**, которую мы построили здесь.

---

*Happy coding!* Если возникнут проблемы, оставляйте комментарий ниже. И помните — как только вы освоите основы, генерация сложных PDF станет проще простого.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}