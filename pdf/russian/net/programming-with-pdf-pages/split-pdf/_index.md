---
title: Разделить PDF после десятой страницы с помощью Aspose.Pdf for .NET
weight: 360
limit:
description: Пошаговый код для разделения PDF‑документа сразу после десятой страницы с Aspose.Pdf for .NET.
keywords: [pdf split, Aspose.Pdf for .NET, split PDF after page, extract pages from PDF, c# pdf split, pdf pagination]
url: /net/programming-with-pdf-pages/split-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Пошаговый код для разделения PDF‑документа сразу после десятой страницы
    с Aspose.Pdf for .NET.
  headline: Разделить PDF после десятой страницы с помощью Aspose.Pdf for .NET
  type: TechArticle
- description: Пошаговый код для разделения PDF‑документа сразу после десятой страницы
    с Aspose.Pdf for .NET.
  name: Разделить PDF после десятой страницы с помощью Aspose.Pdf for .NET
  steps:
  - name: В заголовочных комментариях объясняется цель примера, отмечается, что полный
      код был перемещён, и предоставлена ссылка на актуальный источник.
    text: В заголовочных комментариях объясняется цель примера, отмечается, что полный
      код был перемещён, и предоставлена ссылка на актуальный источник.
  - name: Эта заглушка не выполняет никаких действий и существует только для того,
      чтобы оригинальный URL оставался рабочим.
    text: Эта заглушка не выполняет никаких действий и существует только для того,
      чтобы оригинальный URL оставался рабочим.
  type: HowTo
- questions:
  - answer: Aspose.Pdf не выдаст ошибку; метод `Split` просто вернёт оригинальный
      документ без изменений, поскольку после десятой страницы нет страниц для начала
      новой части.
    question: Что произойдёт, если исходный PDF содержит менее десяти страниц?
  - answer: Вы вызываете `PdfDocument.Split(pageNumber)` у экземпляра `PdfDocument`,
      передавая `10` в качестве `pageNumber`, чтобы создать два отдельных документа.
    question: Какой класс и метод используются для разделения PDF на десятой странице?
  - answer: Да, Aspose.Pdf сохраняет все объекты уровня страниц (закладки, аннотации,
      поля формы и т.д.) в полученных разделённых документах, оставляя их привязанными
      к страницам, откуда они исходят.
    question: Остаются ли закладки, аннотации и поля формы на своих оригинальных страницах
      после разделения?
  - answer: После вызова `Split` вы получаете два объекта `PdfDocument`; вам нужно
      вызвать `Save(\"FirstPart.pdf\")` для первого и `Save(\"SecondPart.pdf\")` для
      второго, указав собственные уникальные имена файлов.
    question: Как мне назвать выходные файлы для двух частей, созданных при разделении?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/split-pdf/og-image.png
og_title: Разделить PDF после страницы 10
og_description: Краткий учебник по разделению PDF на странице 10 с использованием Aspose.Pdf for .NET.
og_image_alt: Руководство, показывающее, как разделить PDF после десятой страницы с помощью Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Разделить PDF после десятой страницы с помощью Aspose.Pdf
Разделение PDF на отдельные документы может упростить их распространение и обработку. Этот учебник пошагово покажет, как с помощью Aspose.Pdf for .NET разделить PDF сразу после десятой страницы, создав два отдельных файла. Следуйте пошаговому коду, чтобы извлечь первые десять страниц и оставшиеся страницы, используя всего несколько строк C#.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/split-pdf" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Что произойдёт, если исходный PDF содержит менее десяти страниц?**  
A: Aspose.Pdf не выдаст ошибку; метод `Split` просто вернёт оригинальный документ без изменений, поскольку после десятой страницы нет страниц для начала новой части.

**Q: Какой класс и метод используются для разделения PDF на десятой странице?**  
A: Вы вызываете `PdfDocument.Split(pageNumber)` у экземпляра `PdfDocument`, передавая `10` в качестве `pageNumber`, чтобы создать два отдельных документа.

**Q: Остаются ли закладки, аннотации и поля формы на своих оригинальных страницах после разделения?**  
A: Да, Aspose.Pdf сохраняет все объекты уровня страниц (закладки, аннотации, поля формы и т.д.) в полученных разделённых документах, оставляя их привязанными к страницам, откуда они исходят.

**Q: Как мне назвать выходные файлы для двух частей, созданных при разделении?**  
A: После вызова `Split` вы получаете два объекта `PdfDocument`; вам нужно вызвать `Save(\"FirstPart.pdf\")` для первого и `Save(\"SecondPart.pdf\")` для второго, указав собственные уникальные имена файлов.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}