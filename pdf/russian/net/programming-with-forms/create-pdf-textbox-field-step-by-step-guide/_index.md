---
category: general
date: 2026-06-21
description: Создайте поле текста PDF с помощью C# и узнайте, как дублировать поле
  формы PDF или добавить текстовое поле в форму PDF всего за несколько строк кода.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: ru
og_description: Быстро создайте текстовое поле в PDF. Это руководство показывает,
  как дублировать поле формы PDF и добавить текстовое поле в форму PDF с использованием
  современной библиотеки PDF для C#.
og_title: Создание текстового поля PDF – Полный учебник по C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Создание текстового поля PDF – пошаговое руководство
url: /ru/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание текстового поля PDF – Полный учебник на C#

Когда‑нибудь вам нужно было **create PDF textbox field**, но вы не знали, какие вызовы API использовать? Вы не одиноки. Независимо от того, создаёте ли вы портал для подписания контрактов или простой лист захвата данных, добавление интерактивных текстовых полей в PDF — это базовый навык для любого разработчика автоматизации форм.  

В этом руководстве мы пройдём практический пример, который не только **adds textbox to PDF form**, но и показывает, как **duplicate PDF form field**, чтобы один и тот же ввод отображался на нескольких страницах. К концу вы получите исполняемую программу, которую можно добавить в любой проект .NET.

## Что вам понадобится

- .NET 6.0 или новее (код также работает с .NET Core)  
- Современная библиотека C# для работы с PDF — в примере ниже используется **PDFTron SDK**, но концепции применимы к iText 7, PdfSharp или другим библиотекам.  
- Visual Studio 2022 (или любая другая IDE по вашему выбору)  

И всё — никаких дополнительных сервисов, никаких obscure зависимостей. Если у вас уже есть PDF, который нужно расширить, просто укажите его в коде.

---

## Шаг 1: Настройка проекта и импорт SDK

First, create a console app:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Add the PDFTron NuGet package:

```bash
dotnet add package PDFTron.NET
```

Now open `Program.cs` and pull in the namespaces we’ll need:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** Если вы используете другую библиотеку, замените инструкции `using` на эквиваленты (например, `iText.Kernel.Pdf` для iText 7).

## Шаг 2: Инициализация PDF‑документа и формы

We’ll start with a fresh PDF that contains two pages – the source page for the original textbox and a target page for the duplicate.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

Объект `Form` — это место, где хранятся все интерактивные поля. Если в документе ещё нет формы, `GetForm()` создаст её для нас.

## Шаг 3: **Create PDF Textbox Field** на первой странице

Now comes the core of our tutorial – creating a textbox field. The rectangle coordinates are expressed in points (1 inch = 72 points). The example places the box near the top‑center of the first page.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Почему мы сразу задаём `Value`? Предзаполнение поля даёт пользователям подсказку о ожидаемом вводе и также демонстрирует, что поле полностью функционирует.

## Шаг 4: Добавление поля в форму – **Add Textbox to PDF Form**

Next, we register the field with the form using a logical name. This name is what you’ll reference later when you need to read or modify the field’s data programmatically.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Выбор понятного имени (например, `"multiBox"`) упрощает последующий код, особенно когда у вас десятки полей.

## Шаг 5: **Duplicate PDF Form Field** на другой странице

A common requirement is to show the same field on multiple pages – think of a “Customer Name” box that appears on every invoice page. PDFTron lets us clone the widget annotation, which is the visual representation of the field.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Клонированный widget использует те же базовые данные, что и оригинальное текстовое поле. Когда пользователь вводит текст в один экземпляр, другой обновляется автоматически — это магия **duplicate PDF form field**.

## Шаг 6: Сохранение документа и очистка

Finally, write the PDF to disk and shut down the PDFNet runtime.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Запуск программы создаёт двухстраничный PDF (`output.pdf`). Откройте его в Adobe Acrobat Reader, кликните по текстовому полю на странице 1, введите что‑нибудь, затем переключитесь на страницу 2 — тот же текст появится мгновенно. Это полностью рабочий пример **create pdf textbox field** с дублированным полем.

---

## Полный рабочий пример (готовый к копированию)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Expected output:** Файл с именем `output.pdf`, содержащий две страницы. Обе страницы показывают одно и то же редактируемое текстовое поле с меткой «Sample». Изменение в одном поле мгновенно обновляет другое.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если поле нужно разместить *на более чем двух* страницах?

Просто повторите шаги клонирования и добавления для каждой дополнительной страницы. Объект данных остаётся тем же, поэтому все widget‑ы синхронны.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Как изменить внешний вид (шрифт, границу, фон)?

Каждый `Widget` имеет методы `SetBorderColor`, `SetBorderWidth` и `SetBackgroundColor`. Вы также можете задать строку default appearance (`DA`), чтобы управлять шрифтом и размером.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Можно ли сделать поле только для чтения после заполнения пользователем?

Да. Установите флаг `ReadOnly` у поля после того, как соберёте данные, или переключайте его в зависимости от вашего рабочего процесса.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Что делать с PDF, которые уже содержат форму?

Если документ уже имеет AcroForm, `doc.GetForm()` просто возвращает её. Вы можете добавлять новые поля, не нарушая существующие. Главное — использовать уникальные имена полей.

---

## Советы для реальных проектов

- **Naming convention:** Добавляйте префикс к именам полей, указывая страницу или раздел (например, `invoice_customer_name`), чтобы избежать конфликтов.  
- **Validation:** Используйте JavaScript‑действия (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`), если нужна клиентская проверка.  
- **Performance:** При работе с большими PDF вызывайте `doc.Lock()` перед массовыми операциями, чтобы снизить нагрузку ввода‑вывода.  
- **Accessibility:** Установите свойство `AlternateName`, чтобы скрин‑ридеры могли описать поле.

---

## Заключение

Мы только что **created a PDF textbox field**, показали, как **duplicate PDF form field** на разных страницах, и продемонстрировали самый простой способ **add textbox to PDF form** с помощью C#. Полный исполняемый код находится выше, и вы можете расширять его стилизацией, валидацией или добавлением страниц по мере необходимости.

Готовы к следующему шагу? Попробуйте добавить выпадающий список (`ChoiceField`) или виджет подписи, либо изучите, как «сплющить» форму после ввода данных для архивных целей. PDFTron SDK (или любая сопоставимая библиотека) предоставляет строительные блоки — ваша фантазия определяет конечный результат.

Если возникнут трудности, оставьте комментарий ниже или ознакомьтесь с официальной документацией библиотеки; там полно примеров, дополняющих то, что мы рассмотрели здесь. Приятного кодинга, и пусть ваши формы всегда остаются синхронными!

## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как создать PDF с Aspose – добавить поле формы и страницы](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Добавить поле формы в PDF документ с помощью Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Добавить поле формы в PDF документ с помощью Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}