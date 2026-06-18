---
category: general
date: 2026-03-24
description: Создайте PDF‑документ с помощью Aspose.PDF на C#. Узнайте, как быстро
  добавить текстовое поле формы PDF.
draft: false
keywords:
- create pdf document
- add text box pdf
- add form field pdf
- how to create pdf
- how to add textbox
language: ru
og_description: Создайте PDF‑документ с помощью Aspose.PDF на C#. Это руководство
  показывает, как добавить текстовое поле формы PDF и добавить поле формы PDF за считанные
  минуты.
og_title: Создать PDF‑документ с Aspose – Добавить текстовое поле
tags:
- Aspose.PDF
- C#
- PDF Forms
title: Создание PDF‑документа с Aspose – добавление текстового поля
url: /ru/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF‑документа с Aspose – Добавление поля текстового блока

Когда‑то вам нужно было **создать PDF‑документ** программно и вы задавались вопросом, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда их приложения должны собирать ввод пользователя без подключения тяжёлой UI‑библиотеки. Хорошая новость: с Aspose.PDF for .NET вы можете быстро создать PDF, разместить текстовое поле на любой странице и даже привязать одно и то же поле к нескольким страницам — всё в паре строк кода.

В этом руководстве мы пройдём весь процесс: от инициализации PDF, через **добавление текстового поля PDF** в форму, до **регистрации поля формы PDF**, и наконец покажем, как проверить, что всё работает. К концу вы будете знать, **как создавать PDF**‑файлы с интерактивными элементами, и увидите, **как добавить textbox**‑контролы, которые ведут себя точно так же, как нативные поля Acrobat.

---

## Что понадобится

- **ASP.NET Core** или любой проект .NET 6+ (код также работает на .NET Framework 4.6+).  
- **Aspose.PDF for .NET** пакет NuGet (версия 23.9 или новее).  
- Небольшой опыт работы с C# — ничего сложного, только базовые знания.  

Если у вас есть всё перечисленное, можно начинать. Никаких дополнительных инструментов, никаких внешних сервисов, только чистый C#‑код, который можно вставить в консольное приложение и запустить.

---

## Создание PDF‑документа и добавление поля текстового блока в форму

Первый шаг, как и следовало ожидать, — **создать PDF‑документ**. Представьте класс `Document` как чистый холст; как только он у вас есть, можно начинать «рисовать» страницы, фигуры и интерактивные элементы.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (the blank canvas)
using var document = new Document();

// Step 2: Add a new page where the text box will live
var page1 = document.Pages.Add();
```

> **Почему это важно:** Создание экземпляра `Document` без страниц приводит к исключению в момент попытки разместить виджет. Добавление страницы заранее гарантирует корректный индекс страницы (`Pages[1]`) для последующих шагов.

---

## Добавление текстового поля PDF‑формы на страницу 1

Теперь, когда у нас есть страница, давайте **добавим текстовое поле PDF**. Класс `TextBoxField` представляет собой один логический объект поля; его можно рассматривать как «имя» ввода, которое может отображаться в разных местах.

```csharp
// Step 3: Define the rectangle where the textbox will appear (x, y, width, height)
var textBoxRect = new Rectangle(100, 500, 300, 520);

// Step 4: Create the text box field on page 1
var textBoxField = new TextBoxField(document.Pages[1], textBoxRect)
{
    // This logical name is used later when you retrieve the value
    PartialName = "MultiWidget"
};
```

> **Полезный совет:** Прямоугольник задаётся в пунктах (1/72 дюйма). Подгоните координаты под ваш макет; начало координат (0,0) находится в левом нижнем углу страницы.

---

## Создание второго виджета на другой странице

Один логический объект поля может иметь несколько визуальных виджетов — идеально для многостраничных форм. Ниже показано, **как добавить textbox** на вторую страницу, используя то же имя поля.

```csharp
// Step 5: Add a second page for the extra widget
var page2 = document.Pages.Add();

// Step 6: Create a widget for the same field on page 2
var secondWidget = textBoxField.CreateWidget(new Rectangle(100, 400, 300, 420));
```

> **Зачем это нужно:** Пользователям часто требуется вводить одну и ту же информацию в разных разделах (например, «Имя» в шапке и ещё раз в сводке). При совместном использовании логического имени Aspose гарантирует синхронность всех виджетов.

---

## Регистрация поля формы в PDF

Создать объект поля недостаточно; его нужно добавить в коллекцию форм документа. Именно на этом этапе вы **добавляете поле формы PDF** во внутреннюю структуру.

```csharp
// Step 7: Register the field (with both widgets) in the document's form collection
document.Form.Add(textBoxField, "MultiWidget");

// Optional: Save the PDF to disk
document.Save("MultiWidgetExample.pdf");
```

> **Что происходит «под капотом»:** `Form.Add` записывает определение поля в словарь AcroForm, делая PDF интерактивным при открытии в Acrobat Reader или любом другом просмотрщике, поддерживающем формы.

---

## Запуск и проверка результата

Скомпилируйте и запустите консольное приложение. Откройте `MultiWidgetExample.pdf` в Adobe Acrobat (или любом просмотрщике, поддерживающем формы) — вы увидите два одинаковых текстовых поля на страницах 1 и 2. Введите что‑нибудь в одно поле — другое обновится мгновенно. Это и есть сила общего логического поля.

```text
Expected outcome:
- PDF with two pages.
- Each page shows a white rectangle (the text box).
- Editing one box updates the other automatically.
```

Если поля не отображаются, проверьте, что прямоугольники находятся внутри границ страницы и что документ был сохранён после добавления поля.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если нужен разный внешний вид на каждой странице?

Вы можете настроить каждый виджет после его создания:

```csharp
secondWidget.Rect = new Rectangle(150, 350, 350, 370); // reposition
secondWidget.Border = new Border(BorderStyle.Solid, 1, Color.Black);
secondWidget.BackgroundColor = Color.LightYellow;
```

### Можно ли задать значение по умолчанию?

Конечно — просто присвойте `Value` перед сохранением:

```csharp
textBoxField.Value = "Enter your name here";
```

Все виджеты отобразят это значение, пока пользователь не заменит его.

### Как сделать поле обязательным для заполнения?

```csharp
textBoxField.Required = true;
```

Acrobat предупредит пользователя, если он попытается отправить форму, не заполнив обязательное поле.

### Работает ли это с соответствием PDF/A?

Aspose.PDF поддерживает PDF/A‑1b, ‑2b, ‑3b. После завершения построения формы вы можете выполнить конвертацию:

```csharp
document.Convert(new PdfConversionOptions { Compliance = PdfCompliance.PdfA2b });
```

---

## Полный рабочий пример

Ниже приведена полностью готовая к копированию программа. Сохраните её как `Program.cs` в .NET‑консольном проекте, добавьте пакет Aspose.PDF из NuGet и запустите.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var document = new Document();

        // 2️⃣ Add two pages (page 1 will host the first widget, page 2 the second)
        var page1 = document.Pages.Add();
        var page2 = document.Pages.Add();

        // 3️⃣ Define the rectangle for the first widget
        var rect1 = new Rectangle(100, 500, 300, 520);

        // 4️⃣ Create the text box field (logical name = "MultiWidget")
        var textBoxField = new TextBoxField(document.Pages[1], rect1)
        {
            PartialName = "MultiWidget",
            Value = "Sample text",        // optional default value
            Required = true               // makes the field mandatory
        };

        // 5️⃣ Add a second widget on page

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}