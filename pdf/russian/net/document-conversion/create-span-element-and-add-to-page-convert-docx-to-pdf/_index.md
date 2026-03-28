---
category: general
date: 2026-03-27
description: Создайте элемент span в C# и узнайте, как добавить span на страницу при
  конвертации DOCX в PDF и сохранении в PDF. Пошаговое руководство для разработчиков.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: ru
og_description: Создайте элемент span в C# и узнайте, как добавить span на страницу
  при конвертации DOCX в PDF, затем сохранить как PDF. Включён полный пример кода.
og_title: Создать элемент span и добавить на страницу – Конвертировать DOCX в PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Создать элемент <span> и добавить на страницу – Конвертировать DOCX в PDF
url: /ru/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание элемента span и добавление его на страницу – Конвертация DOCX в PDF

Создание **элемента span** в файле DOCX — распространённая задача, когда требуется точный контроль над расположением. В этом руководстве мы покажем, **как добавить span** на страницу, **конвертировать DOCX в PDF** и **сохранить как PDF** — всё в нескольких простых шагах.  

Если вы когда‑нибудь смотрели на документ Word и думали: «Хотелось бы разместить маленькую текстовую коробку в точных координатах», вы попали по адресу. Мы пройдём весь процесс от загрузки исходного файла до получения готового PDF‑файла.

## Что вы получите

К концу этого руководства вы сможете:

* Загрузить файл `.docx`, используя класс `Document` из библиотеки обработки документов.  
* **Создать элемент span** с помощью API `TaggedContent`.  
* Разместить этот span в точных координатах X/Y на выбранной странице.  
* **Добавить элемент на страницу** надёжно, даже если страница не первая.  
* **Конвертировать DOCX в PDF** и **сохранить как PDF** одним вызовом `Save`.

Никаких внешних инструментов, никаких загадочных настроек — просто чистый C#‑код, который можно скопировать и вставить в свой проект.

## Требования

* .NET 6+ (или любой современный .NET‑runtime, поддерживаемый вашей библиотекой).  
* SDK обработки документов, предоставляющий `Document`, `TaggedContent`, `Position` и т.д.  
* Базовое понимание синтаксиса C# — если вы умеете писать `Console.WriteLine`, вам достаточно.

> **Pro tip:** Держите версию SDK актуальной; последняя версия (v3.2 от марта 2026) включает улучшения производительности для операций на уровне страниц.

---

![Диаграмма, показывающая, как создать элемент span и разместить его на странице PDF](https://example.com/images/create-span-element.png "Диаграмма размещения элемента span")

## Создание элемента span – позиционирование и добавление на страницу

Ниже приведён полностью готовый к запуску код, который делает всё: от загрузки исходного DOCX до записи окончательного PDF. Скопируйте его в консольное приложение, поправьте пути и запустите.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Пошаговое объяснение

#### Шаг 1 – Загрузка документа DOCX  
Мы создаём объект `Document`, указывая файл `input.docx`. Этот объект представляет весь Word‑файл в памяти, предоставляя доступ к страницам, содержимому и метаданным.  

#### Шаг 2 – Создание элемента span  
Вызов `TaggedContent.CreateSpanElement()` возвращает лёгкий встроенный контейнер. Представьте его как крошечный невидимый ящик, способный держать текст, изображения или другие встроенные элементы. Добавление текста (`span.Text`) необязательно, но удобно для отладки.

#### Шаг 3 – Позиционирование span  
`new Position(50, 750)` задаёт левый верхний угол span в 50 пт от левого поля и 750 пт от верхнего края страницы. Эти значения абсолютные, поэтому вы можете разместить span где угодно — идеально для точных макетов.

#### Шаг 4 – Добавление span на целевую страницу  
`doc.Pages[1].Add(span)` вставляет span на вторую страницу. API использует нулевую индексацию, поэтому страница 0 — первая. Если нужно добавить на первую страницу, используйте `doc.Pages[0]`.

#### Шаг 5 – Конвертация DOCX в PDF и сохранение как PDF  
Вызов `doc.Save("output.pdf")` делает две вещи: записывает изменённый документ на диск **и** конвертирует содержимое в PDF благодаря расширению `.pdf`. Дополнительный шаг конвертации не требуется — это самый простой способ **сохранить как PDF**.

---

## Как добавить span на другую страницу (расширенный вариант)

Иногда номер страницы заранее неизвестен. Можно найти страницу по её номеру (человекочитаемому) или поиском по ключевому слову.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Почему это важно:** В отчётах, где количество страниц меняется, жёстко заданный `Pages[1]` может нарушить макет. Этот фрагмент демонстрирует надёжный шаблон для **динамического добавления span**.

---

## Распространённые ошибки и как их избежать

| Проблема | Что происходит | Как исправить |
|----------|----------------|----------------|
| **Span не виден** | Координаты находятся за пределами страницы или у span нулевая ширина/высота. | Проверьте значения `Position`; используйте линейку в PDF‑просмотрщике. |
| **Неправильный индекс страницы** | Вы добавляете на страницу 0, а ожидаете её на странице 2. | Помните, что API использует нулевую индексацию; к человеческому номеру добавляйте 1. |
| **Сохранение перезаписывает исходник** | `doc.Save("input.docx")` заменяет оригинальный файл. | Всегда сохраняйте в новый путь (`output.pdf`) при конвертации. |
| **Отсутствует ссылка на SDK** | Ошибка компиляции на классе `Document`. | Установите NuGet‑пакет: `dotnet add package DocumentProcessing.SDK`. |

---

## Проверка результата

После выполнения программы откройте `output.pdf` в любом PDF‑просмотрщике. Вы должны увидеть текст «Hello, world!», расположенный точно в точке (50, 750) на второй странице. Если текст отображается в другом месте, скорректируйте значения `Position` и запустите снова.  

Для автоматизированного тестирования можно использовать PDF‑парсер (например, iTextSharp), чтобы программно проверять координаты текста.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Следующие шаги

* **Стилизация span** — изучите свойства `span.Font`, `span.Color` и другие параметры оформления.  
* **Добавление изображений** — используйте `CreateImageElement()` вместо span для графики.  
* **Пакетная обработка** — перебирайте папку с DOCX‑файлами

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}