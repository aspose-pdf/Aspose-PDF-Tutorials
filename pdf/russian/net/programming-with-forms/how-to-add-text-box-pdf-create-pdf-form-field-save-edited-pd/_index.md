---
category: general
date: 2026-02-20
description: Как добавить текстовое поле в PDF с помощью C# – научитесь создавать
  поля формы PDF, конвертировать Word в форму PDF и быстро сохранять отредактированный
  PDF‑документ.
draft: false
keywords:
- how to add text box pdf
- create pdf form field
- convert word to pdf form
- save edited pdf document
language: ru
og_description: Как добавить текстовое поле в PDF? Этот учебник показывает, как создавать
  поля формы PDF, конвертировать Word в форму PDF и сохранять отредактированные PDF‑документы
  с помощью C#.
og_title: Как добавить текстовое поле в PDF – Полное руководство для разработчиков
  C#
tags:
- PDF
- C#
- Document Automation
title: Как добавить текстовое поле в PDF – создать поле формы PDF и сохранить отредактированный
  PDF‑документ
url: /ru/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить текстовое поле PDF – Полный пошаговый пример на C#

Когда‑нибудь задумывались **как добавить текстовое поле PDF** в файлы, не тратя часы на работу с графическими инструментами? Вы не одиноки. Преобразование документа Word в интерактивную PDF‑форму — задача, необходимая многим разработчикам, особенно при создании порталов для онбординга или автоматических генераторов отчетов.

В этом руководстве мы пройдем весь процесс: создание поля формы PDF, преобразование документа Word в PDF‑форму и, наконец, **сохранение отредактированного PDF‑документа**. К концу у вас будет готовый фрагмент кода C#, который можно вставить в любой проект .NET — без внешнего пользовательского интерфейса.

## Что вы узнаете

- Загрузить файл `.docx` и преобразовать его в объект PDF‑документа.  
- **Create PDF form field** объекты программно, включая текстовое поле.  
- Добавить несколько виджетов (визуальных представлений) для одного и того же поля на разных страницах.  
- **Save edited PDF document** обратно на диск.  

Никакой сложный сторонний UI не требуется; всё делается через код, что позволяет автоматизировать процесс в пакетных заданиях, веб‑службах или настольных приложениях.

> **Pro tip:** Если вы уже используете библиотеку Aspose.PDF for .NET (код ниже предполагает её наличие), вы получите встроенную поддержку конвертации Word‑в‑PDF и работы с формами без дополнительных зависимостей.

## Требования

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 или новее (или .NET Framework 4.7.2+) | Библиотека, которую мы используем, ориентирована на современные среды выполнения. |
| Aspose.PDF for .NET (NuGet `Aspose.PDF`) | Предоставляет `Document`, `FormField`, `TextBoxField` и т.д. |
| Пример файла Word (`input.docx`) | Это исходный файл, который мы превратим в PDF‑форму. |
| Базовые знания C# | Вы сможете понять фрагменты кода без глубокого погружения. |

> **Note:** Те же концепции применимы к другим PDF‑библиотекам (iTextSharp, PDFSharp). Замените классы соответственно, если предпочитаете другой стек.

## Шаг 1 – Загрузка документа Word и конвертация в PDF

Сначала нам нужен объект `Document`, представляющий PDF‑версию нашего файла Word. Aspose.PDF может читать `.docx` напрямую, поэтому отдельный шаг конвертации не нужен.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Drawing;

// Load the Word document and automatically convert it to PDF
Document doc = new Document("YOUR_DIRECTORY/input.docx");

// Verify that the conversion succeeded
Console.WriteLine($"Document loaded with {doc.Pages.Count} page(s).");
```

**Почему это важно:** Ранняя конвертация предоставляет нам PDF‑полотно, к которому можно прикреплять поля формы. Это также гарантирует, что размеры страниц соответствуют конечному PDF, что необходимо для точного позиционирования текстового поля.

## Шаг 2 – Создание текстового поля формы на первой странице

Теперь мы добавим элемент **text box PDF**, который пользователи смогут заполнять. Координаты прямоугольника задаются в пунктах (1/72 дюйма). В этом примере поле расположено рядом с верхним левым углом страницы 1.

```csharp
// Define the rectangle where the text box will appear (x‑min, y‑min, x‑max, y‑max)
Rectangle headerRect = new Rectangle(50, 750, 200, 770);

// Create the visual widget (TextBoxField) and give it a logical name
TextBoxField headerBox = new TextBoxField(doc.Pages[1], headerRect)
{
    PartialName = "Header" // This is the field’s internal identifier
};

// Add the widget to the document’s form collection and assign a field name
FormField headerField = doc.Form.Add(headerBox, "HeaderField");

// Optional: set default text or appearance properties
headerBox.Value = "Enter title here";
headerBox.Border = new Border(headerBox) { Width = 1, Color = Color.Black };
```

> **Почему мы используем `PartialName` и отдельное имя поля:** `PartialName` — это идентификатор, используемый PDF‑просмотрщиком, тогда как имя, которое вы передаёте в `Add` (`"HeaderField"`), является ключом, к которому вы будете обращаться при извлечении данных позже.

### Визуальная подсказка

![Пример добавления текстового поля PDF](/images/add-textbox-pdf.png "Скриншот, показывающий размещение текстового поля на первой странице PDF")

*Alt text:* *Как добавить текстовое поле PDF – иллюстрация текстового поля, размещённого на странице PDF.*

## Шаг 3 – Добавление второго виджета для того же поля на странице 2

Поля формы PDF могут иметь несколько визуальных представлений (виджетов). Это удобно, когда требуется одинаковая точка ввода данных на нескольких страницах — например, повторяющийся заголовок.

```csharp
// Define a second rectangle on page 2 (different position)
Rectangle secondRect = new Rectangle(50, 50, 200, 70);

// Attach the same logical field to page 2
headerField.AddWidget(secondRect, doc.Pages[2]);
```

**Почему это полезно:** Пользователи заполняют поле один раз, и значение автоматически появляется во всех виджетах. Это уменьшает дублирование и делает форму аккуратной.

## Шаг 4 – (Опционально) Преобразование дополнительного содержимого Word в элементы PDF‑формы

Если ваш исходный файл Word содержит другие заполнители (например, `{{Name}}`), вы можете программно заменить их полями формы. Ниже показан быстрый шаблон:

```csharp
// Example: replace a placeholder text with a new text box field
foreach (Page page in doc.Pages)
{
    foreach (TextFragment fragment in page.TextFragments)
    {
        if (fragment.Text.Contains("{{Name}}"))
        {
            // Remove placeholder
            fragment.Text = fragment.Text.Replace("{{Name}}", string.Empty);

            // Create a new text box at the placeholder’s location
            Rectangle nameRect = fragment.Rectangle;
            TextBoxField nameBox = new TextBoxField(page, nameRect) { PartialName = "Name" };
            doc.Form.Add(nameBox, "NameField");
        }
    }
}
```

> **Edge case:** Некоторые PDF‑файлы хранят текст как отдельные фрагменты по символу, поэтому может потребоваться объединять фрагменты или использовать более надёжный алгоритм поиска для сложных документов.

## Шаг 5 – Сохранение отредактированного PDF‑документа

Наконец, запишите изменённый PDF обратно на диск. Вы можете выбрать любой формат вывода, поддерживаемый библиотекой (PDF, XPS и т.д.). Здесь мы остаёмся с PDF.

```csharp
// Save the final PDF that now contains interactive text boxes
doc.Save("YOUR_DIRECTORY/output.pdf");

Console.WriteLine("PDF saved successfully at YOUR_DIRECTORY/output.pdf");
```

**Что проверить:** Откройте `output.pdf` в Adobe Acrobat Reader или любом PDF‑просмотрщике, поддерживающем формы. Вы должны увидеть два одинаковых текстовых поля — одно на странице 1 и другое на странице 2 — оба редактируемы и синхронизированы.

## Полный рабочий пример

Ниже приведена полная, автономная программа, которую можно скопировать и вставить в консольное приложение. Она включает все вышеописанные шаги и минимальную обработку ошибок.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load Word and convert to PDF
            Document doc = new Document("YOUR_DIRECTORY/input.docx");
            Console.WriteLine($"Loaded document with {doc.Pages.Count} page(s).");

            // 2️⃣ Create a text box on page 1
            Rectangle rect1 = new Rectangle(50, 750, 200, 770);
            TextBoxField txtBox = new TextBoxField(doc.Pages[1], rect1)
            {
                PartialName = "Header"
            };
            FormField headerField = doc.Form.Add(txtBox, "HeaderField");
            txtBox.Value = "Enter header";
            txtBox.Border = new Border(txtBox) { Width = 1, Color = Color.DarkGray };

            // 3️⃣ Add a second widget on page 2
            Rectangle rect2 = new Rectangle(50, 50, 200, 70);
            headerField.AddWidget(rect2, doc.Pages[2]);

            // 4️⃣ (Optional) Replace placeholders with fields – omitted for brevity

            // 5️⃣ Save the edited PDF
            string outputPath = "YOUR_DIRECTORY/output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved successfully at {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Ожидаемый результат:** После запуска программы `output.pdf` содержит два синхронизированных текстовых поля с меткой «Header». Любой введённый в одно поле текст автоматически появляется в другом.

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| *Могу ли я добавить текстовое поле в существующий PDF (без исходного Word)?* | Да — пропустите шаг конвертации Word и загрузите PDF напрямую (`new Document("file.pdf")`). |
| *Что делать, если индекс страницы выходит за пределы?* | Aspose.PDF генерирует `IndexOutOfRangeException`. Всегда проверяйте `doc.Pages.Count` перед доступом к `doc.Pages[n]`. |
| *Нужно ли устанавливать свойство `ReadOnly` у поля?* | Только если вы хотите запретить редактирование. Установите `txtBox.ReadOnly = true;`. |
| *Как позже извлечь введённые данные?* | Используйте `doc.Form["HeaderField"].Value` после того, как пользователь сохранит форму. |
| *Является ли начало системы координат в левом нижнем углу?* | Верно — (0,0) находится в левом нижнем углу страницы. Соответственно корректируйте значения Y. |

## Следующие шаги

Теперь, когда вы знаете **как добавить текстовое поле PDF** программно, вы можете изучить следующее:

- **Create PDF form field** типы полей, кроме текстовых (чекбоксы, радиокнопки, выпадающие списки).  
- **Convert Word to PDF form** с более сложной обработкой макета (таблицы, изображения).  
- **Save edited PDF document** в облачное хранилище (Azure Blob, AWS S3) для распределённых рабочих процессов.  
- **Validate form input** на стороне сервера перед обработкой.  

Каждая из этих тем опирается на изложенный здесь фундамент, позволяя создавать полнофункциональные автоматизированные решения с PDF.

---

*Удачной разработки! Если возникнут проблемы, оставьте комментарий ниже — разберём их вместе.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}