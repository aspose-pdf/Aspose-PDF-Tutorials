---
category: general
date: 2026-07-20
description: Как добавить нумерацию Бейтса в PDF с помощью Aspose.Pdf. Узнайте, как
  быстро и надёжно добавить номера Бейтса в PDF и поставить штамп на каждую страницу.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: ru
lastmod: 2026-07-20
og_description: Как добавить нумерацию Бейтса в PDF с помощью Aspose.Pdf. Это руководство
  покажет, как добавить номера Бейтса в PDF и поставить штамп на каждую страницу всего
  в несколько строк кода C#.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: Как добавить нумерацию Бейтса в PDF – Полный учебник Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: Как добавить нумерацию Бейтса в PDF с помощью Aspose – пошаговое руководство
url: /ru/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить нумерацию Бейтса в PDF с помощью Aspose – Пошаговое руководство

Когда‑нибудь задавались вопросом, **как добавить нумерацию бейтса** в юридический документ без траты часов в графическом интерфейсе? Вы не одиноки. Во многих юридических фирмах, государственных учреждениях и даже крупных корпорациях проставление уникального идентификатора на каждую страницу — ежедневная рутина, но одна строка кода на C# делает это простым делом.

В этом руководстве мы пройдем полный, исполняемый пример, который покажет вам точно, **как добавить нумерацию бейтса** с помощью библиотеки Aspose.Pdf. К концу вы также узнаете, как **добавлять номера бейтса в pdf** файлы и **добавлять штамп на каждую страницу** всего несколькими строками кода. Никакой магии, только ясные рассуждения и практические советы.

## Что вы узнаете

- Загрузить существующий PDF с помощью Aspose.Pdf.
- Создать `BatesNumberingStamp` и настроить его внешний вид.
- Пройтись по каждой странице и автоматически **добавлять штамп на каждую страницу**.
- Сохранить результат как новый PDF, содержащий профессиональную нумерацию Бейтса на каждом листе.

### Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).
- Действительная лицензия Aspose.Pdf for .NET (или временный оценочный ключ).
- Исходный PDF‑файл, который вы хотите пронумеровать (мы будем называть его `Original.pdf`).

Если вы соответствуете этим трём пунктам, вы готовы приступить.

---

## Шаг 1: Настройте проект и установите Aspose.Pdf

Сначала создайте новый консольный проект (или добавьте код в существующий). Затем загрузите пакет NuGet:

```bash
dotnet add package Aspose.Pdf
```

> **Совет:** Если вы работаете в корпоративной сети, убедитесь, что ваш источник NuGet настроен для доступа к `https://www.nuget.org`.

## Шаг 2: Загрузите исходный PDF‑документ

Загрузка PDF так же проста, как указать Aspose путь к файлу. Класс `Document` представляет весь файл.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

Зачем мы выводим количество страниц в журнал? Потому что нумерация Бейтса должна быть последовательной по *всем* страницам, и удобно убедиться, что вы случайно не загрузили другой файл.

## Шаг 3: Создайте штамп нумерации Бейтса

Сердцем операции является `BatesNumberingStamp`. Он позволяет задать префикс, разделитель, количество цифр и даже то, следует ли рассматривать штамп как *артефакт* (т.е. невидимый для инструментов извлечения текста).

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**Почему такие настройки?**  
- `StartingNumber = 1000` имитирует типичный юридический реестр, уже имеющий накопившиеся дела.  
- `NumberOfDigits = 5` гарантирует, что номера вроде `01000`, `01001` и т.д. будут выровнены.  
- `Artifact = true` необходимо, когда PDF будет передаваться в OCR или e‑discovery процессы; номера остаются видимыми для людей, но игнорируются поисковыми системами текста.

## Шаг 4: Добавьте штамп на каждую страницу

Теперь мы проходим по `document.Pages` и применяем один и тот же штамп к каждой странице. Aspose автоматически увеличивает номер.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **Распространённый вопрос:** *Могу ли я контролировать место появления штампа?*  
> Конечно. `BatesNumberingStamp` наследуется от `Stamp`, поэтому вы можете задать свойства такие как `HorizontalAlignment`, `VerticalAlignment`, `XIndent` и `YIndent` перед циклом. Для краткости мы оставим позицию по умолчанию — нижний правый угол.

## Шаг 5: Сохраните изменённый PDF

Наконец, зафиксируйте изменения. Вы можете перезаписать оригинальный файл или записать в новое место — здесь мы сохраняем обе копии.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

Когда вы откроете `BatesNumbered.pdf`, каждая страница покажет штамп, похожий на:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

где `00123` — общее количество страниц, а префикс `ABC-` остаётся постоянным.

---

## Полный рабочий пример

Скопируйте весь блок ниже в новый файл `Program.cs` и запустите его. Скорректируйте пути к файлам под вашу среду.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**Ожидаемый вывод в консоли:**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

Откройте сохранённый файл, и вы увидите последовательные номера на каждой странице — именно то, что вы ожидаете, когда **добавляете номера бейтса в pdf**.

---

## Расширенные настройки (по желанию)

| Goal | How to achieve it |
|------|-------------------|
| **Изменить цвет штампа** | Установите `batesStamp.Color = Color.FromRgb(255, 0, 0);` before the loop. |
| **Разместить штамп в заголовке** | Отрегулируйте свойства `HorizontalAlignment` и `VerticalAlignment`, как показано в закомментированном коде. |
| **Пропустить определённые страницы** | Добавьте условие `if (page.Number % 2 == 0) continue;` внутри `foreach`. |
| **Использовать пользовательский шрифт** | Назначьте `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **Сделать штамп видимым для OCR** | Установите `Artifact = false`. |

Эти варианты позволяют вам **добавлять штамп на каждую страницу**, при этом сохраняя основную логику упорядоченной.

---

## Часто задаваемые вопросы

**Q: Работает ли это с PDF‑файлами, защищёнными паролем?**  
A: Да. Загрузите документ с помощью объекта `PdfLoadOptions`, который содержит пароль, а затем действуйте точно так же, как показано.

**Q: Что делать, если нужны разные префиксы для разных дел?**  
A: Создайте несколько экземпляров `BatesNumberingStamp`, настройте каждый со своим `Prefix` и применяйте их только к соответствующим диапазонам страниц.

**Q: Бесплатна ли библиотека?**  
A: Aspose.Pdf предлагает 30‑дневную пробную версию. Для использования в продакшене понадобится лицензия, но набор API остаётся тем же.

---

## Заключение

Мы только что рассмотрели **как добавить нумерацию бейтса** в любой PDF с помощью Aspose.Pdf, продемонстрировали, как **добавлять номера бейтса в pdf** чисто и повторяемо, и показали самый простой способ **добавлять штамп на каждую страницу** с помощью одного цикла. Код полностью автономный, выполняется за секунды и может быть интегрирован в более крупные конвейеры обработки документов без изменений.

Готовы к следующему вызову? Попробуйте сгенерировать титульную страницу, перечисляющую диапазон Бейтса, или внедрить QR‑код рядом с каждым штампом. Возможностей бесконечно, и тот же шаблон, который вы изучили сегодня, будет полезен везде, где нужно автоматизировать метаданные PDF.

Если этот гид оказался полезным, поделитесь им, оставьте комментарий или изучите наши другие руководства по объединению PDF, водяным знакам и цифровым подписям. Счастливого кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как добавить штампы страниц в PDF с помощью Aspose.PDF for .NET: Полное руководство](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Как добавить штампы номеров страниц в PDF с помощью Aspose.PDF for .NET | Водяные знаки и фоны](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Как добавить и настроить номера страниц в PDF с помощью Aspose.PDF for .NET | Руководство по манипуляции документами](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}