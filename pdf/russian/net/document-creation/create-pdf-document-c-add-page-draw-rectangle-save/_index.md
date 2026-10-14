---
category: general
date: 2026-02-14
description: 'Быстро создайте PDF‑документ на C#: добавьте страницу в PDF, нарисуйте
  прямоугольник и сохраните PDF в файл с помощью Aspose.Pdf в несколько строк кода.'
draft: false
keywords:
- create pdf document c#
- add page to pdf
- how to draw rectangle
- add shape to pdf
- save pdf to file
language: ru
og_description: Создайте PDF‑документ на C# за считанные минуты. Узнайте, как добавить
  страницу в PDF, нарисовать прямоугольник, добавить форму в PDF и сохранить PDF в
  файл с понятными примерами кода.
og_title: Создание PDF‑документа на C# – пошаговое руководство
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Создание PDF‑документа C# – добавить страницу, нарисовать прямоугольник и сохранить
url: /ru/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF документа C# – Добавление страницы, рисование прямоугольника и сохранение

Когда‑нибудь вам нужно было **create PDF document C#** с нуля и вы задавались вопросом, с чего начать? Вы не одиноки — многие разработчики сталкиваются с тем же препятствием, когда впервые берутся за программную генерацию PDF. Хорошая новость? С несколькими строками кода Aspose.Pdf вы можете добавить страницу в PDF, нарисовать прямоугольник и **save PDF to file** без усилий.

В этом руководстве мы пройдем всё, что вам нужно: инициализацию PDF, вставку новой страницы, рисование формы прямоугольника и, наконец, сохранение файла на диск. К концу вы получите готовое консольное приложение, которое создаст чётко очерченный синим контуром прямоугольник на новой странице PDF.

## Что понадобится

- **.NET 6 или новее** (в примере используются top‑level statements, но подойдёт любая современная версия .NET)
- **Aspose.Pdf for .NET** пакет NuGet  
  ```bash
  dotnet add package Aspose.Pdf
  ```
- Папка, в которую у вас есть права записи — в руководстве файл будет сохранён в `YOUR_DIRECTORY/shapes.pdf`.

Никакой дополнительной конфигурации, без XML, просто чистый C#.

## Создание PDF документа C# – Обзор

Первый шаг — создать объект `Document`. Считайте его пустым холстом; всё, что вы добавляете позже — страницы, текст, фигуры — будет привязано к этому единственному экземпляру.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document (the canvas)
using var pdfDocument = new Document();
```

> **Почему `using var`?**  
> Класс `Document` реализует `IDisposable`. Оборачивание его в оператор `using` гарантирует, что все неуправляемые ресурсы (дескрипторы файлов, нативные буферы) будут освобождены сразу после завершения работы, что особенно важно в длительно работающих сервисах.

## Добавление страницы в PDF

PDF без страниц — это как книга без листов, почти бесполезно. Добавление страницы происходит одним вызовом метода, но также возвращает объект `Page`, которым вы сможете управлять дальше.

```csharp
// Step 2: Add a fresh page to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **Подсказка:** Новая страница автоматически получает размер по умолчанию (A4). Если нужен пользовательский размер, вы можете задать `pdfPage.PageInfo.Width` и `Height` до добавления любого контента.

## Как нарисовать прямоугольник

А теперь — самая интересная часть: рисование прямоугольника. Aspose.Pdf использует класс `RectangleShape`, которому требуется объект `Rectangle` (x, y, width, height) с границами. Координаты отсчитываются от нижнего‑левого угла страницы.

```csharp
// Step 3: Define the rectangle bounds (x, y, width, height)
// This will be validated – an exception is thrown if the rectangle is out of bounds
var rectangleBounds = new Rectangle(50, 50, 200, 150);
```

> **Особый случай:** Если `x + width` превышает ширину страницы или `y + height` превышает её высоту, Aspose бросит `ArgumentException`. Всегда проверяйте размеры, особенно при генерации PDF для разных размеров страниц.

## Добавление фигуры в PDF

Когда границы готовы, мы создаём фигуру, задаём ей синюю обводку и помещаем её в коллекцию абзацев страницы.

```csharp
// Step 4: Create a rectangle shape with a blue stroke and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue,   // Outline color
    // FillColor = Color.LightGray, // Uncomment to add a fill
    // LineWidth = 2                // Adjust border thickness if needed
};
pdfPage.Paragraphs.Add(rectangleShape);
```

> **Почему добавлять в `Paragraphs`?**  
> В Aspose.Pdf визуальные элементы, такие как фигуры, рассматриваются как «абзацы», потому что они занимают прямоугольную область на странице. Такой подход сохраняет согласованность движка разметки между текстом и графикой.

## Сохранение PDF в файл

Последний шаг — сохранить документ. Укажите полный путь, и Aspose выполнит всю тяжёлую работу — сжатие, потоки объектов и таблицы перекрестных ссылок будут обработаны автоматически.

```csharp
// Step 5: Save the PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");
```

> **Pro tip:** Используйте `Path.Combine(Environment.CurrentDirectory, "shapes.pdf")`, если хотите разместить файл рядом с исполняемым файлом, или предварительно вызовите `Directory.CreateDirectory`, чтобы избежать `DirectoryNotFoundException`.

### Ожидаемый результат

Откройте `shapes.pdf` в любом PDF‑просмотрщике. Вы увидите одну страницу формата A4 с **blue‑bordered rectangle**, расположенным на 50 пунктов от левого и нижнего краёв, размером 200 × 150 пунктов. Текста нет, только фигура — идеально подходит для водяных знаков, полей формы или визуальных заполнителей.

![PDF document with a blue rectangle created using create pdf document c#](https://example.com/images/pdf-rectangle.png "PDF document with a blue rectangle created using create pdf document c#")

*Alt text:* *PDF document with a blue rectangle created using create pdf document c#.*

## Полный рабочий пример

Ниже представлен полностью готовый к копированию и вставке код программы. Он компилируется как консольное приложение (`dotnet new console`) и работает без какой‑либо дополнительной настройки, кроме пакета NuGet.

```csharp
// Program.cs
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

using var pdfDocument = new Document();               // Create PDF document
var pdfPage = pdfDocument.Pages.Add();                // Add a page

// Define rectangle bounds (x, y, width, height)
// Aspose validates the rectangle – out‑of‑bounds throws an exception
var rectangleBounds = new Rectangle(50, 50, 200, 150);

// Create the rectangle shape (blue stroke) and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue
};
pdfPage.Paragraphs.Add(rectangleShape);

// Save the document to disk
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");

// Inform the user
Console.WriteLine("PDF created successfully at YOUR_DIRECTORY/shapes.pdf");
```

Запустите программу, откройте сгенерированный файл, и вы увидите фигуру точно там, где её определили.

## Часто задаваемые вопросы и подводные камни

- **В:** *Что делать, если нужен заполненный прямоугольник?*  
  **О:** Раскомментируйте строку `FillColor` в инициализаторе `RectangleShape`. Aspose поддерживает сплошные цвета, градиенты и даже заливку изображениями.

- **В:** *Можно ли нарисовать несколько фигур на одной странице?*  
  **О:** Конечно. Просто создайте дополнительные объекты `RectangleShape`, `Ellipse` или `Polygon` и добавьте каждый в `pdfPage.Paragraphs`.

- **В:** *Всегда ли система координат нижний‑левый угол?*  
  **О:** Да, Aspose следует спецификации PDF, где начало координат (0,0) находится в нижнем‑левом углу. Если вам нужен верхний‑левый угол, вычисляйте `y = pageHeight - desiredY`.

- **В:** *Что произойдёт, если целевая папка не существует?*  
  **О:** `pdfDocument.Save` бросит `DirectoryNotFoundException`. Предварительно создайте папку с помощью `Directory.CreateDirectory`.

## Следующие шаги

Теперь, когда вы знаете, как **add page to PDF**, **how to draw rectangle**, **add shape to PDF** и **save PDF to file**, вы можете расширять эту основу:

- Вставлять текст, изображения или таблицы рядом с фигурами.  
- Использовать `Graphics` для свободного рисования (линии, дуги, пользовательские пути).  
- Изучать шифрование PDF или цифровые подписи, если важна безопасность.  

Все эти темы напрямую опираются на код, который мы только что рассмотрели, так что смело экспериментируйте.

---

**Итог:** Вы только что освоили полный рабочий процесс **create PDF document C#** с помощью Aspose.Pdf — инициализацию, добавление страницы, рисование прямоугольника и сохранение файла. Это надёжный строительный блок для счетов, отчётов, сертификатов или любых автоматических документов, которые нужно генерировать «на лету». Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}