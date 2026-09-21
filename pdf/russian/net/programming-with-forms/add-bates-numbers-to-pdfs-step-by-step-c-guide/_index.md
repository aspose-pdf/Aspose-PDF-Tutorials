---
category: general
date: 2026-02-12
description: Быстро добавляйте номера Бейтса в PDF‑файлы. Узнайте, как добавить текстовое
  поле в PDF, добавить поле формы в PDF и добавить номера страниц в PDF с помощью
  Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: ru
og_description: Добавьте номера Бейтса в PDF‑документы на C#. Это руководство показывает,
  как добавить текстовое поле в PDF, добавить поле формы в PDF и добавить номера страниц
  в PDF с помощью Aspose.PDF.
og_title: Добавьте номера Бейтса в PDF — Полный учебник по C#
tags:
- PDF
- C#
- Aspose.PDF
title: Добавление Bates‑номеров в PDF — пошаговое руководство на C#
url: /ru/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление Bates Numbers к PDF — Полное руководство на C#

Когда‑нибудь вам нужно было **add bates numbers** к набору юридических PDF, но вы не знали, с чего начать? Вы не одиноки. Во многих юридических фирмах и проектах e‑discovery проставление уникального идентификатора на каждой странице — ежедневная рутина, а делать это вручную — кошмар.  

Хорошие новости? С несколькими строками C# и Aspose.PDF вы можете автоматизировать весь процесс. В этом руководстве мы пройдемся по **how to add bates** numbers, добавим текстовое поле на каждую страницу и сохраним чистый, индексируемый PDF — без усилий.

> **What you’ll get:** полностью исполняемый пример кода, объяснения, почему каждая строка важна, советы по граничным случаям и быстрый чек‑лист для проверки результата.  

Мы также коснёмся связанных задач, таких как **add text field pdf**, **add form field pdf** и **add page numbers pdf**, чтобы у вас был набор инструментов для любой задачи автоматизации документов.

---

## Требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+)
- Visual Studio 2022 (или любой предпочитаемый IDE)
- Действительная лицензия Aspose.PDF for .NET (бесплатная пробная версия подходит для тестирования)
- Исходный PDF с именем `source.pdf`, размещённый в папке, к которой вы можете обратиться  

Если какой‑либо из пунктов вам незнаком, просто сделайте паузу и установите недостающий компонент перед тем, как продолжить. Ниже предполагается, что вы уже добавили пакет Aspose.PDF через NuGet:

```bash
dotnet add package Aspose.Pdf
```

---

## Как добавить bates numbers в PDF с помощью Aspose.PDF

Ниже представлен полностью готовый к копированию и вставке код. Он загружает PDF, создаёт **text box field** на каждой странице, записывает отформатированный Bates number и, наконец, сохраняет изменённый файл.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Почему это работает

- **`Document`** — точка входа; представляет весь PDF‑файл.  
- **`Rectangle`** определяет, где поле будет располагаться на странице. Числа задаются в пунктах (1 pt ≈ 1/72 in). При необходимости измените координаты, чтобы разместить номер в другом углу.  
- **`TextBoxField`** — *form field*, способный хранить любую строку. Присваивая `Value`, мы фактически **add page numbers pdf** с пользовательским префиксом.  
- **`pdfDocument.Form.Add`** регистрирует поле в AcroForm PDF, делая его видимым в просмотрщиках, таких как Adobe Acrobat.  

Если когда‑нибудь понадобится изменить внешний вид (шрифт, цвет, размер), вы можете подправить свойства `TextBoxField` — см. документацию Aspose по `DefaultAppearance` и `Border`.

---

## Добавление текстового поля на каждую страницу PDF (шаг “add text field pdf”)

Иногда нужен лишь видимый ярлык, а не интерактивное поле формы. В этом случае можно заменить `TextBoxField` на `TextFragment` и добавить его напрямую в коллекцию `Paragraphs` страницы. Вот быстрая альтернатива:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

Подход **add text field pdf** полезен, когда конечный документ будет только для чтения, тогда как метод **add form field pdf** оставляет номера редактируемыми позже.

---

## Сохранение PDF с Bates numbers (момент “add page numbers pdf”)

После завершения цикла вызов `pdfDocument.Save` записывает всё на диск. Если нужно сохранить оригинальный файл, просто измените путь вывода или используйте перегрузки `pdfDocument.Save`, чтобы потокировать результат напрямую в ответ веб‑API.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Это самая удобная часть — без временных файлов, без дополнительных библиотек, только Aspose, который берёт на себя тяжёлую работу.

---

## Ожидаемый результат и быстрая проверка

Откройте `bates.pdf` в любом PDF‑просмотрщике. Вы должны увидеть небольшое поле в левом нижнем углу каждой страницы со следующим содержимым:

```
BATES-00001
BATES-00002
…
```

Если посмотреть свойства документа, вы заметите AcroForm, содержащий поля с именами `Bates_1`, `Bates_2` и т.д. Это подтверждает, что шаг **add form field pdf** выполнен успешно.

---

## Распространённые ошибки и профессиональные советы

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Numbers appear off‑center | Rectangle coordinates are relative to the page’s lower‑left corner. | Flip the Y‑value (`pageHeight - marginTop`) or use `page.PageInfo.Height` to calculate a top‑margin placement. |
| Fields are invisible in Adobe Reader | The default border is set to “No”. | Set `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Large PDFs cause memory pressure | `using` disposes the document only after the loop finishes. | Process pages in chunks or use `pdfDocument.Save` with `SaveOptions` that enable streaming. |
| License not applied | Aspose prints a watermark on the first page. | Register your license early: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Расширение решения

- **Custom prefixes:** Replace `"BATES-"` with any string (`"DOC-"`, `"CASE-"`, …).  
- **Zero‑padding length:** Change `{pageNumber:D5}` to `{pageNumber:D3}` for three digits.  
- **Dynamic placement:** Use `pdfDocument.Pages[pageNumber].PageInfo.Width` to position the field on the right‑hand side.  
- **Conditional numbering:** Skip blank pages by checking `pdfDocument.Pages[pageNumber].IsBlank`.

Все эти варианты сохраняют основной шаблон **add bates numbers**, **add text field pdf** и **add form field pdf**.

---

## Полный рабочий пример (все в одном)

Ниже представлен финальная, готовая к запуску программа, включающая все вышеуказанные советы. Скопируйте её в новое консольное приложение и нажмите F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Запустите, откройте результат, и вы увидите профессионально выглядящий идентификатор на каждой странице — именно то, что ожидает специалист по поддержке судебных дел.

---

## Заключение

Мы только что продемонстрировали **how to add bates numbers** в любой PDF с помощью C# и Aspose.PDF. Создавая **text box field** на каждой странице, мы одновременно **add text field pdf**, **add form field pdf** и **add page numbers pdf** за один проход. Подход быстрый, масштабируемый и легко настраиваемый под пользовательские префиксы, разные макеты или условную логику.

Готовы к следующему вызову? Попробуйте внедрить QR‑код, который будет вести к оригинальному делу, или сгенерировать отдельную индексную страницу, перечисляющую все Bates numbers с соответствующими названиями страниц. Тот же API позволяет объединять PDF, извлекать страницы и даже редактировать конфиденциальные данные — возможности безграничны.

Если возникнут проблемы, оставьте комментарий ниже или обратитесь к официальной документации Aspose для более глубокого изучения. Приятного кодинга, и пусть ваши PDF всегда остаются правильно пронумерованными!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}