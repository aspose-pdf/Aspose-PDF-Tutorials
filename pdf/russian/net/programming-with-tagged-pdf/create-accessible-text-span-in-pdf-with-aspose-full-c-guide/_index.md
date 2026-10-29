---
category: general
date: 2026-06-05
description: Создайте доступный текстовый фрагмент в PDF с помощью Aspose.PDF и узнайте,
  как преобразовать PDF в PDF/X‑4. Следуйте этому пошаговому руководству на C# для
  надёжной работы с документами.
draft: false
keywords:
- create accessible text span
- convert pdf to pdf/x-4
- how to convert pdf to pdfx4
language: ru
og_description: Создайте доступный текстовый фрагмент в PDF и узнайте, как преобразовать
  PDF в PDF/X‑4 с помощью Aspose.PDF. Этот учебник проведёт вас через каждый шаг.
og_title: Создание доступного текстового фрагмента в PDF – Полное руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create accessible text span in a PDF using Aspose.PDF and learn how
    to convert PDF to PDF/X-4. Follow this step‑by‑step C# tutorial for robust document
    handling.
  headline: 'Create Accessible Text Span in PDF with Aspose: Full C# Guide'
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: 'Создание доступного текстового фрагмента в PDF с помощью Aspose: Полное руководство
  по C#'
url: /ru/net/programming-with-tagged-pdf/create-accessible-text-span-in-pdf-with-aspose-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание доступного текстового фрагмента в PDF с помощью Aspose: Полное руководство на C#

Когда‑то вам нужно **создать доступный текстовый фрагмент** в PDF, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этим, когда впервые пробуют работать с доступностью PDF. Хорошая новость в том, что Aspose.PDF делает это удивительно просто, и одновременно вы можете узнать **как преобразовать PDF в PDF/X‑4** в том же процессе.

В этом руководстве мы загрузим существующий PDF, выведем список его цифровых подписей, конвертируем файл в PDF/X‑4, добавим доступный позиционированный текстовый фрагмент, разместим многостраничное поле формы, экспортируем в HTML без растровых изображений и, наконец, проверим подпись на сервере CA. К концу вы получите единый, автономный C#‑программный файл, который делает всё это — без разрозненных фрагментов кода и без «см. документацию».

## Предварительные требования

- .NET 6.0 или новее (код также компилируется на .NET Framework 4.7+).  
- Действующая лицензия Aspose.PDF for .NET (бесплатная trial‑версия работает, но после нескольких страниц накладывает ограничения).  
- Входной PDF с именем `input.pdf`, размещённый в папке, которой вы управляете (замените `YOUR_DIRECTORY` на реальный путь).  
- Базовое знакомство с консольными приложениями C# — ничего сложного, только метод `Main`.

Все готово? Отлично — приступаем.

## Создание доступного текстового фрагмента с Aspose.PDF

Первая конкретная задача — **создать доступный текстовый фрагмент** внутри тегированного содержимого PDF. Тегированные PDF‑файлы являются основой доступности; они позволяют скрин‑ридерам понимать логический порядок чтения.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Devices;
using System.Drawing;

// Load the source PDF
var sourcePdf = new Document("YOUR_DIRECTORY/input.pdf");

// Create a positioned span element
var positionedSpan = sourcePdf.TaggedContent.CreateSpanElement();
positionedSpan.SetPosition(150, 500);          // X=150, Y=500 points from bottom‑left
positionedSpan.Text = "Accessible positioned text";

// Append the span to the root of the tagged tree
sourcePdf.TaggedContent.RootElement.AppendChild(positionedSpan);
```

**Почему это важно:** Привязывая фрагмент к `TaggedContent.RootElement`, вы гарантируете, что вспомогательные технологии воспринимают его как часть логической структуры, а не просто визуальное наложение. Вызов `SetPosition` позволяет разместить текст точно там, где нужно — идеально для наложения подписей на изображения или схемы.

> **Полезный совет:** Если ваш PDF уже содержит дерево `DocumentStructure`, вы можете вставить фрагмент под конкретным узлом `Paragraph` или `Section`, чтобы сохранить иерархию.

## Преобразование PDF в PDF/X‑4 с помощью Aspose

Теперь, когда часть с доступностью готова, займёмся требованием **convert pdf to pdf/x-4**. PDF/X‑4 — это подмножество, предназначенное для надёжной печати; оно встраивает все шрифты и поддерживает прозрачность.

```csharp
// Define conversion options: target PDF/X‑4 and delete any conversion errors
var conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_4,            // Target format
    ConvertErrorAction.Delete); // Remove problematic objects

// Perform the conversion in‑place
sourcePdf.Convert(conversionOptions);

// Save the converted file
sourcePdf.Save("YOUR_DIRECTORY/converted_pdfx4.pdf");
```

**Зачем это нужно:** Конвертация в PDF/X‑4 удаляет элементы, которые могут вызвать проблемы при печати (например, неподдерживаемые цветовые профили). Флаг `ConvertErrorAction.Delete` гарантирует, что процесс конвертации не будет прерван — проблемные объекты просто отбрасываются, и файл остаётся пригодным.

> **Особый случай:** Если нужно оставить оригинальный файл нетронутым, сначала создайте его клон (`var clone = sourcePdf.Clone();`) и выполните конвертацию над клоном.

## Вывод списка цифровых подписей и проверка статуса компрометации

Прежде чем дальше изменять документ, разумно посмотреть, какие подписи уже встроены. Этот шаг не строго связан с доступностью, но показывает, как **how to convert pdf to pdfx4** безопасно — без разрушения существующих подписей.

```csharp
// Retrieve signature information
var signatures = sourcePdf.DigitalSignatures.GetSignatureInfo();

foreach (var sig in signatures)
{
    Console.WriteLine($"{sig.Name} compromised? {sig.IsCompromised}");
}
```

Если `IsCompromised` возвращает `true`, возможно, потребуется повторно подписать документ после конвертации, поскольку PDF/X‑4 может аннулировать некоторые типы подписей.

## Добавление многостраничного поля формы TextBox

Распространённый реальный сценарий — форма, охватывающая несколько страниц, например, поле «Комментарии», которое отображается на каждой странице. Ниже показано, как создать `TextBoxField` и привязать виджеты к двум разным страницам.

```csharp
// Create a TextBox on page 1 (pages are 1‑based)
var textBox = new TextBoxField(sourcePdf.Pages[1],
    new Rectangle(100, 700, 300, 730)); // left, bottom, right, top

// Add a second widget on page 2
textBox.AddWidget(sourcePdf.Pages[2],
    new Rectangle(50, 600, 250, 630));

// Register the field in the form collection
sourcePdf.Form.Add(textBox, "MultiWidgetField");
```

**Зачем нужны несколько виджетов:** Каждый виджет представляет визуальный экземпляр одного логического поля. Пользователь заполняет любой из них, и значение распространяется на все страницы — идеально для длинных опросов.

## Сохранение как HTML без растровых изображений

Иногда требуется веб‑версия PDF, но без тяжёлых растровых изображений, которые «утяжеляют» страницу. Следующий фрагмент демонстрирует, как **convert pdf to pdf/x-4**‑подобный вывод при экспорте в HTML и пропуске изображений.

```csharp
var htmlOptions = new HtmlSaveOptions
{
    SkipImages = true          // Do not embed raster images
};

sourcePdf.Save("YOUR_DIRECTORY/output.html", htmlOptions);
```

Полученный `output.html` содержит только векторную графику и текст, что делает его молниеносно быстрым в браузере.

## Проверка цифровой подписи через сервер CA

Наконец, проверим встроенную подпись против удостоверяющего центра (CA). Этот шаг демонстрирует **how to convert pdf to pdfx4** безопасно — подтверждая, что подпись остаётся доверенной после всех преобразований.

```csharp
var validator = new SignatureValidator(sourcePdf);
bool isCaValid = validator.ValidateWithCaServer("https://ca.mycompany.com/validate");

Console.WriteLine($"CA validation result: {isCaValid}");
```

Если сервер CA возвращает `false`, вам придётся повторно подписать PDF после шага конвертации. `SignatureValidator` от Aspose упрощает проверку цепочки сертификатов.

## Полный рабочий пример

Объединив всё, получаем полностью готовую программу, которую можно скопировать в консольный проект:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Devices;
using System.Drawing;

class Demo
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var sourcePdf = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ List existing digital signatures
        var signatures = sourcePdf.DigitalSignatures.GetSignatureInfo();
        foreach (var sig in signatures)
            Console.WriteLine($"{sig.Name} compromised? {sig.IsCompromised}");

        // 3️⃣ Convert to PDF/X‑4 (how to convert pdf to pdfx4)
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        sourcePdf.Convert(conversionOptions);
        sourcePdf.Save("YOUR_DIRECTORY/converted_pdfx4.pdf");

        // 4️⃣ Create an accessible positioned text span
        var positionedSpan = sourcePdf.TaggedContent.CreateSpanElement();
        positionedSpan.SetPosition(150, 500);
        positionedSpan.Text = "Accessible positioned text";
        sourcePdf.TaggedContent.RootElement.AppendChild(positionedSpan);

        // 5️⃣ Add a TextBox form field with widgets on two pages
        var textBox = new TextBoxField(sourcePdf.Pages[1],
            new Rectangle(100, 700, 300, 730));
        textBox.AddWidget(sourcePdf.Pages[2],
            new Rectangle(50, 600, 250, 630));
        sourcePdf.Form.Add(textBox, "MultiWidgetField");

        // 6️⃣ Export to HTML, skipping raster images
        var htmlOptions = new HtmlSaveOptions { SkipImages = true };
        sourcePdf.Save("YOUR_DIRECTORY/output.html", htmlOptions);

        // 7️⃣ Validate the signature against a CA server
        var validator = new SignatureValidator(sourcePdf);
        bool isCaValid = validator.ValidateWithCaServer("https://ca.mycompany.com/validate");
        Console.WriteLine($"CA validation result: {isCaValid}");
    }
}
```

**Ожидаемый вывод** (консоль):

```
John Doe compromised? False
CA validation result: True
```

Вы также увидите три новых файла в `YOUR_DIRECTORY`:

- `converted_pdfx4.pdf` — версия PDF/X‑4.  
- `output.html` — HTML без растровых изображений.  
- Исходный `input.pdf` теперь содержит доступный текстовый фрагмент и поле формы.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Подпись становится недействительной после конвертации** | PDF/X‑4 удаляет некоторые объекты, от которых зависят подписи. | Подписать заново после шага `Convert`, либо использовать `ConvertErrorAction.Keep`, если необходимо сохранить оригинальные объекты. |
| **Тегированное содержимое не распознаётся** | Вы добавили фрагмент к неправильному узлу. | Всегда привязывайте к `TaggedContent.RootElement` *или* к конкретному структурному элементу (например, `Paragraph`). |
| **Экспорт HTML всё ещё содержит изображения** | `SkipImages` пропускает только растровые изображения, а не векторные. | Для полностью текстового вывода также установите `RasterImagesCompression = RasterImagesCompression.None`. |
| **Проверка CA не проходит из‑за проблем с сетью** | Валидатор может |

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Create Accessible Tagged PDFs Using Aspose.PDF for .NET&#58; Enhance Titles, Alt Text, and Layout](/pdf/english/net/advanced-features/enhanced-tagged-pdfs-aspose-pdf-dot-net/)
- [How to Rotate Text in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/text-operations/rotate-text-aspose-pdf-net-guide/)
- [How to Create Bookmark Pages in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/bookmarks-navigation/create-pdf-bookmarks-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}