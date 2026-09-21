---
category: general
date: 2026-03-03
description: Создайте PDF с несколькими страницами и добавьте текстовое поле в форму
  PDF с помощью Aspose.PDF на C#. Узнайте, как добавить текстовое поле, создать поле
  формы PDF и быстро добавить несколько страниц в PDF.
draft: false
keywords:
- create pdf with pages
- add text box pdf
- how to add textbox
- create pdf form field
- add multiple pages pdf
language: ru
og_description: Создайте PDF с страницами с помощью Aspose.PDF. Это руководство показывает,
  как добавить текстовые поля PDF, создать поле формы PDF и добавить несколько страниц
  PDF в C#.
og_title: Создание PDF с помощью Pages – Полный учебник по C#
tags:
- pdf
- csharp
- aspose
title: Создание PDF с страницами и текстовыми полями – Полное руководство по C#
url: /ru/net/programming-with-forms/create-pdf-with-pages-and-text-box-fields-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF с страницами и полями текстовых коробок – Полное руководство на C#  

Когда‑нибудь вам нужно было **создать pdf с страницами**, позволяющий пользователям вводить заметки? Возможно, вы создаёте портал контрактов, форму обратной связи или простой опросник. В этом случае вам понадобится PDF, который не только имеет несколько страниц, но и содержит переиспользуемое текстовое поле. Хорошие новости: с Aspose.PDF for .NET вы можете сделать всё это в нескольких строках.

В этом руководстве мы пройдёмся по **how to add textbox** элементам управления, зарегистрируем **create pdf form field**, и, наконец, **add multiple pages pdf**, чтобы получить отшлифованный интерактивный документ. Без лишних слов — только код, который можно скопировать‑вставить, плюс объяснение «почему» за каждым решением. К концу вы получите PDF с именем `TextBoxTwoWidgets.pdf`, содержащий одинаковое текстовое поле на двух разных страницах.

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+).  
- Aspose.PDF for .NET NuGet‑пакет (`Install-Package Aspose.PDF`).  
- Базовое понимание классов C# и освобождения объектов (мы будем использовать блок `using`).  

> **Pro tip:** Если вы используете Visual Studio, включите *nullable reference types* для более чистого опыта, но это не требуется для данного примера.

## Шаг 1: Создание PDF с страницами — настройка документа

Первое, что нужно сделать, — создать пустой PDF‑документ. Считайте класс `Document` свежей тетрадью; позже вы добавите в неё страницы.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

using (var pdfDocument = new Document())
{
    // The document is now ready for pages and form fields.
```

*Почему блок `using`?* Он гарантирует, что все неуправляемые ресурсы (дескрипторы файлов, буферы памяти) будут освобождены сразу после завершения работы, предотвращая утечки — особенно важно, когда вы генерируете множество PDF в веб‑службе.

## Шаг 2: Добавление PDF‑поля Text Box на первую страницу

Теперь, когда документ существует, нам нужна хотя бы одна страница, чтобы разместить поле формы. Мы добавим **две страницы**, потому что хотим, чтобы одно и то же текстовое поле появилось на обеих.

```csharp
    // Add the first page
    var firstPage = pdfDocument.Pages.Add();

    // Add the second page (will host the widget copy)
    var secondPage = pdfDocument.Pages.Add();

    // Create a TextBoxField on the first page
    var notesField = new TextBoxField(
        firstPage,
        new Rectangle(50, 700, 300, 750))   // left, bottom, right, top
    {
        Name = "Notes",
        Value = "Type here..."
    };
```

Координаты прямоугольника следуют системе координат PDF (начало в левом нижнем углу). Свойство `Name` — это внутренний идентификатор; позже вы будете использовать его, когда получите значение после заполнения формы пользователем.

## Шаг 3: Как добавить виджет Textbox на вторую страницу

*Виджет* — это визуальное представление поля формы. По умолчанию поле получает один виджет на той странице, где оно было создано. Если вам нужен тот же текстовый блок на другой странице, добавьте ещё одну аннотацию‑виджет.

```csharp
    // Place a second widget of the same field on the second page
    notesField.AddWidgetAnnotation(
        secondPage,
        new Rectangle(50, 500, 300, 550));
```

Обратите внимание на разные координаты Y — так второй текстовый блок располагается ниже на странице. Конечно, вы можете использовать тот же прямоугольник, если хотите идентичное размещение.

## Шаг 4: Создание PDF‑поля формы и его регистрация

Несмотря на то, что мы уже создали объект `notesField`, его всё равно нужно зарегистрировать в коллекции `Form` документа. Этот шаг делает поле частью интерактивной структуры формы.

```csharp
    // Register the field with the PDF form
    pdfDocument.Form.Add(notesField, notesField.Name);
```

Если пропустить эту строку, текстовое поле будет отображаться визуально, но не будет сохранено как поле формы, что означает, что его содержимое не будет отправлено при обработке PDF.

## Шаг 5: Сохранение PDF и проверка PDF с несколькими страницами

Наконец, мы записываем документ на диск. Имя файла произвольное; просто убедитесь, что папка существует и у вашего приложения есть права на запись.

```csharp
    // Save the resulting PDF
    pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
}
```

Когда вы откроете `TextBoxTwoWidgets.pdf` в Adobe Acrobat Reader, вы увидите две страницы, каждая из которых содержит одинаковое текстовое поле «Notes». Введите что‑нибудь на первой странице, перейдите ко второй — оба поля остаются независимыми, потому что они используют один и тот же объект данных.

### Ожидаемый результат

- **Page 1:** Textbox at coordinates (50, 700) with placeholder “Type here…”.  
- **Page 2:** Identical textbox positioned lower (50, 500).  
- Both pages belong to a **single PDF form** named “Notes”.  

Вы можете протестировать форму, экспортировав данные (Acrobat → Tools → Prepare Form → Export Data) и увидеть одну запись для `Notes`.

## Общие варианты и граничные случаи

| Scenario | What to Change | Why |
|----------|----------------|-----|
| **Different default text per page** | Create two separate `TextBoxField` objects with distinct `Name` values. | Each widget must belong to its own field to hold independent values. |
| **Read‑only textbox** | Set `notesField.ReadOnly = true;` before adding the widget. | Prevents users from editing the field while still showing information. |
| **Multi‑line textbox** | Set `notesField.Multiline = true;` and increase the rectangle height. | Allows longer notes without scrolling. |
| **Password‑protected PDF** | After saving, call `pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AESx128);`. | Secures the document while preserving form fields. |

## Профессиональные советы по работе с формами Aspose.PDF

- **Batch creation:** If you need dozens of identical widgets, loop over `pdfDocument.Pages` and call `AddWidgetAnnotation` inside the loop.  
- **Field naming conventions:** Use a prefix like `txt_` or `fld_` to avoid collisions when merging PDFs later.  
- **Performance:** Reuse a single `Rectangle` instance when possible; the library copies the values internally, so you won’t hit a memory bottleneck.  

## Полный рабочий пример (готов к копированию‑вставке)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // 2️⃣ Add two pages – we’ll place a widget on each
            var firstPage = pdfDocument.Pages.Add();
            var secondPage = pdfDocument.Pages.Add();

            // 3️⃣ Define the textbox field (add text box pdf)
            var notesField = new TextBoxField(
                firstPage,
                new Rectangle(50, 700, 300, 750))
            {
                Name = "Notes",
                Value = "Type here..."
            };

            // 4️⃣ Add a second widget on the second page (how to add textbox)
            notesField.AddWidgetAnnotation(
                secondPage,
                new Rectangle(50, 500, 300, 550));

            // 5️⃣ Register the field (create pdf form field)
            pdfDocument.Form.Add(notesField, notesField.Name);

            // 6️⃣ Save the file (add multiple pages pdf)
            pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
        }

        System.Console.WriteLine("PDF created successfully!");
    }
}
```

Запустите программу, откройте полученный файл, и вы увидите точно то, что описано в руководстве.

## Заключение

Мы только что **created pdf with pages**, содержащий переиспользуемый элемент формы **add text box pdf**, продемонстрировали **how to add textbox** виджеты на нескольких страницах и зарегистрировали корректный **create pdf form field**. Финальный документ доказывает, что вы можете **add multiple pages pdf**, сохраняя форму интерактивной и лёгкой.

Что дальше? Попробуйте добавить флажки, переключатели или даже JavaScript‑действия, чтобы сделать PDF действительно динамичным. Вы также можете изучить объединение нескольких таких PDF в один отчёт — Aspose.PDF делает это проще простого.

Есть вопросы или интересный сценарий использования, которым хотите поделиться? Оставьте комментарий ниже, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}