---
category: general
date: 2026-06-08
description: Создайте многостраничную форму на C# с использованием Aspose.Pdf. Узнайте,
  как добавить текстовое поле в PDF, создать поле формы PDF и сохранить обновлённый
  PDF с понятными примерами кода.
draft: false
keywords:
- create multi page form
- add textbox to pdf
- create pdf form field
- how to save pdf
- save updated pdf
language: ru
og_description: Создайте многостраничную форму на C# с Aspose.Pdf. Это руководство
  показывает, как добавить текстовое поле в PDF, создать поле формы PDF и сохранить
  обновлённый PDF за считанные минуты.
og_title: Создание многостраничной формы в C# – Полное руководство по Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  headline: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  type: TechArticle
- description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  name: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  steps:
  - name: '**Load** the existing PDF.'
    text: '**Load** the existing PDF.'
  - name: '**Create** a `TextBoxField` on the first page – this is our form field.'
    text: '**Create** a `TextBoxField` on the first page – this is our form field.'
  - name: '**Add** a widget annotation on the second page so the same field appears
      there too.'
    text: '**Add** a widget annotation on the second page so the same field appears
      there too.'
  - name: '**Save** the modified document as a new file.'
    text: '**Save** the modified document as a new file.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF Forms
title: Создание многостраничной формы в C# с Aspose.Pdf – пошаговое руководство
url: /ru/net/programming-with-forms/create-multi-page-form-in-c-with-aspose-pdf-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание многостраничной формы в C# с Aspose.Pdf – Полное руководство

Вы когда‑нибудь задумывались, как **создать многостраничную форму** в C# без борьбы с низкоуровневыми спецификациями PDF? Вы не одиноки. Независимо от того, создаёте ли вы портал для подачи заявок на работу или мастер заполнения налоговой декларации, многостраничная PDF‑форма может сделать сбор данных гладким и профессиональным.

В этом руководстве мы пройдём реальный пример, который **добавляет текстовое поле в pdf**, **создаёт поле формы pdf** и, наконец, **сохраняет обновлённый pdf**. К концу вы получите полностью рабочую двухстраничную форму, которую можно внедрить в любой проект .NET.

> **Совет:** Aspose.Pdf работает на .NET 6+, .NET Framework 4.6+ и даже .NET Core, так что вы покрыты независимо от того, используете Windows или Linux.

## Что понадобится

- **Aspose.Pdf for .NET** (пакет NuGet `Aspose.Pdf`).  
- Простой PDF‑файл (`input.pdf`), который уже содержит как минимум две страницы.  
- Visual Studio 2022 или любой редактор, поддерживающий C#.  
- Папка, к которой у вас есть права чтения/записи – мы будем ссылаться на неё как `YOUR_DIRECTORY`.

Больше никаких зависимостей. Готовы? Погрузимся.

![Пример создания многостраничной формы в C# с использованием Aspose.Pdf](image.png "Пример создания многостраничной формы")

## Создание многостраничной формы – Обзор

Прежде чем начнём писать код, давайте очертим общий процесс:

1. **Load** существующий PDF.  
2. **Create** `TextBoxField` на первой странице — это наше поле формы.  
3. **Add** аннотацию‑виджет на второй странице, чтобы то же поле появилось и там.  
4. **Save** изменённый документ как новый файл.

Каждый шаг намеренно изолирован, чтобы вы могли заменять части (например, изменить размер прямоугольника или добавить больше страниц), не ломая всё целое.

## Шаг 1 – Загрузка PDF‑документа

Первое, что вы делаете при работе с любой PDF‑библиотекой, — открываете исходный файл. Aspose.Pdf делает это в одну строку.

```csharp
// Step 1: Load the PDF document from disk
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document(@"YOUR_DIRECTORY\input.pdf");
```

*Почему это важно:* Загрузка документа даёт доступ к коллекции `Pages`, где мы позже прикрепим наше поле формы и виджет. Если файл не найден, будет выброшено исключение, поэтому убедитесь, что путь указан правильно.

## Шаг 2 – Создание текстового поля формы (add textbox to pdf)

Теперь мы действительно **создаём поле формы pdf** — `TextBoxField`. Считайте его контейнером данных, который будет хранить всё, что вводит пользователь.

```csharp
// Step 2: Instantiate a TextBoxField on page 1
Aspose.Pdf.Forms.TextBoxField commentsField = new Aspose.Pdf.Forms.TextBoxField(
    pdfDocument.Pages[1],                                   // target page (1‑based index)
    new Aspose.Pdf.Rectangle(100, 100, 300, 120));         // position & size (LLX, LLY, URX, URY)
```

Несколько замечаний:

- Координаты прямоугольника задаются в пунктах (1 pt = 1/72 in). Отрегулируйте их под ваш макет.
- `pdfDocument.Pages[1]` указывает на **первую** страницу, поскольку Aspose использует коллекцию, нумерация которой начинается с 1.
- Создавая поле на странице 1, мы также задаём ему внешний вид по умолчанию, который будем повторно использовать на странице 2.

## Шаг 3 – Установка имени поля и начального значения

Каждому полю формы нужен идентификатор. Это строка, к которой вы позже обратитесь при извлечении ввода пользователя.

```csharp
// Step 3: Assign a name and an empty default value
commentsField.Name = "Comments";   // unique field name
commentsField.Value = "";          // start with a blank textbox
```

*Почему назвать его “Comments”?* Это описательно, но вы можете назвать его как угодно (`"Address"`, `"PhoneNumber"`). Главное — чтобы имя было уникальным во всём PDF; дублирующиеся имена вызывают конфликты данных при отправке формы.

## Шаг 4 – Добавление аннотации‑виджета на второй странице

*Виджет* — это визуальное представление поля формы на конкретной странице. По умолчанию созданное нами поле существует только на странице 1. Чтобы то же текстовое поле появилось на странице 2, мы добавляем аннотацию‑виджет.

```csharp
// Step 4: Place the same TextBoxField on page 2 via a widget
commentsField.Widgets.Add(
    new Aspose.Pdf.Forms.WidgetAnnotation(
        pdfDocument.Pages[2],                               // second page
        new Aspose.Pdf.Rectangle(50, 50, 250, 70)));       // widget rectangle
```

Зачем нужен виджет? Потому что PDF‑формы разделяют **определение поля** (данные) и **внешний вид виджета** (что видит пользователь). Добавление виджета позволяет пользователю заполнять одно и то же поле на нескольких страницах — классическое требование для многостраничных форм.

### Совет для особых случаев

Если ваш исходный PDF содержит более двух страниц и вы хотите разместить текстовое поле на каждой странице, пройдитесь в цикле по `pdfDocument.Pages` и добавьте виджет для каждой. Просто помните, что размер прямоугольника должен соответствовать макету каждой страницы.

## Шаг 5 – Сохранение обновлённого PDF (how to save pdf)

Наконец мы сохраняем наши изменения. Aspose.Pdf предоставляет простой метод `Save`, который перезаписывает или создаёт новый файл.

```csharp
// Step 5: Save the updated PDF to a new file
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

*Почему не перезаписывать `input.pdf`?* Сохранение оригинала нетронутым упрощает отладку и позволяет сравнивать результаты до и после. Если действительно нужно заменить исходный файл, просто вызовите `Save` с тем же путём.

## Полный рабочий пример

Собрав всё вместе, представляем полный готовый к запуску пример программы.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // Load the existing PDF (make sure the file exists)
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Create a TextBoxField on the first page
        TextBoxField commentsField = new TextBoxField(
            pdfDocument.Pages[1],
            new Rectangle(100, 100, 300, 120));

        // Configure the field
        commentsField.Name = "Comments";
        commentsField.Value = ""; // blank by default

        // Add a widget on the second page so the same field appears there
        commentsField.Widgets.Add(
            new WidgetAnnotation(
                pdfDocument.Pages[2],
                new Rectangle(50, 50, 250, 70)));

        // Save the modified PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        // Optional: inform the user
        System.Console.WriteLine("Multi‑page form created successfully!");
    }
}
```

### Ожидаемый результат

When you open `output.pdf` in Adobe Acrobat Reader:

- Страница 1 показывает пустое текстовое поле с координатами (100, 100)‑(300, 120).  
- Страница 2 показывает то же текстовое поле с координатами (50, 50)‑(250, 70).  
- Оба поля имеют **имя поля** `Comments`, что означает, что данные, введённые на любой странице, синхронно обновляются.

## Часто задаваемые вопросы и подводные камни

| Question | Answer |
|----------|--------|
| *Могу ли я добавить более одного текстового поля?* | Конечно. Просто повторите шаги 2‑4 с новым экземпляром `TextBoxField` и уникальным `Name`. |
| *Что если в PDF нет второй страницы?* | Код выбросит `ArgumentOutOfRangeException`. Защитите его проверкой `if (pdfDocument.Pages.Count >= 2) { … }`. |
| *Нужно ли задавать шрифты?* | Aspose использует шрифт Helvetica по умолчанию. Для пользовательских шрифтов задайте `commentsField.DefaultAppearance.Font` перед сохранением. |
| *Можно ли печатать поле?* | Да — Aspose помечает виджеты как печатаемые по умолчанию. При необходимости можно переключить `WidgetAnnotation.Flags`. |
| *Как позже извлечь введённое значение?* | После того как пользователи заполнят форму и вы получите PDF, вызовите `pdfDocument.Form["Comments"].Value`, чтобы прочитать данные. |

## Следующие шаги

Теперь, когда вы знаете **как сохранить pdf** после добавления текстового поля, вы можете изучить:

- Добавление **чекбоксов** или **радиокнопок** (`CheckBoxField`, `RadioButtonField`).  
- Использование действий **JavaScript** для клиентской валидации (`commentsField.Actions.OnMouseUp = "…"`).  
- **Плоское** (flatten) преобразование формы, чтобы предотвратить дальнейшее редактирование (`pdfDocument.Form.Flatten()`).  

Все это опирается на те же концепции, которые мы рассмотрели при **создании многостраничной формы**.

**Итог:** Вы только что узнали, как **создать многостраничную форму** в C# с Aspose.Pdf, как **добавить текстовое поле в pdf**, как **создать поле формы pdf**, и какие конкретные шаги **сохранить обновлённый pdf**. Не стесняйтесь менять размеры прямоугольников, добавлять новые поля или проходить по всем страницам для действительно динамического решения.

Есть свой вариант, которым хотите поделиться? Оставьте комментарий ниже, и удачной разработки!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как создать PDF с Aspose – добавить поле формы и страницы](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Создать PDF‑документ с Aspose – добавить страницу, текстовое поле и форму](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [Как добавить и извлечь поля формы PDF с помощью Aspose.PDF для .NET: полное руководство](/pdf/english/net/forms-annotations/manage-pdf-form-fields-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}