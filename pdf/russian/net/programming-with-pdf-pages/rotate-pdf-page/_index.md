---
title: Повернуть одну страницу PDF на 180 градусов с помощью Aspose.PDF for .NET
weight: 260
limit:
description: Узнайте, как повернуть третью страницу PDF на 180° с помощью Aspose.PDF for .NET.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Узнайте, как повернуть третью страницу PDF на 180° с помощью Aspose.PDF
    for .NET.
  headline: Повернуть одну страницу PDF на 180 градусов с помощью Aspose.PDF for .NET
  type: TechArticle
- description: Узнайте, как повернуть третью страницу PDF на 180° с помощью Aspose.PDF
    for .NET.
  name: Повернуть одну страницу PDF на 180 градусов с помощью Aspose.PDF for .NET
  steps:
  - name: Файл содержит только пояснительные комментарии и не имеет исполняемого кода,
      служа в качестве заполнителя для оригинального примера.
    text: Файл содержит только пояснительные комментарии и не имеет исполняемого кода,
      служа в качестве заполнителя для оригинального примера.
  type: HowTo
- questions:
  - answer: Используйте коллекцию страниц SDK с нулевой индексацией, например `pdfDocument.Pages[2]`,
      поскольку индекс 2 соответствует третьей странице.
    question: Как указать третью страницу PDF для поворота?
  - answer: 'Свойство вращения принимает только четыре стандартных значения: 0, 90,
      180 и 270 градусов; любое другое значение округляется до ближайшего допустимого
      угла.'
    question: Можно ли повернуть страницу на угол, отличный от 180 градусов?
  - answer: Поворот применяется только к объекту `PdfDocument` в памяти; необходимо
      вызвать `pdfDocument.Save(\"output.pdf\")` (или аналогичный метод сохранения),
      чтобы записать изменения в новый файл, оставив исходный без изменений.
    question: Выполняет ли поворот страницы автоматическое изменение оригинального
      файла?
  - answer: SDK автоматически пересчитывает позиции аннотаций и полей формы, чтобы
      они оставались правильно выровненными относительно новой ориентации.
    question: Что происходит с аннотациями или полями формы после поворота страницы?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: Повернуть страницу PDF на 180° с помощью Aspose.PDF
og_description: Быстро переверните третью страницу вашего PDF вверх дном, используя несколько строк кода Aspose.PDF for .NET.
og_image_alt: Руководство, показывающее код, который поворачивает третью страницу PDF на 180 градусов с помощью Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Повернуть одну страницу PDF на 180 градусов с помощью Aspose.PDF
В этом учебнике вы узнаете, как повернуть третью страницу PDF‑документа на 180 градусов, используя Aspose.PDF for .NET. Пример пошагово показывает загрузку PDF, выбор страницы 3, применение поворота и сохранение обновлённого файла. Такой подход позволяет перевернуть конкретную страницу, не изменяя ориентацию остальных страниц.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: Как указать третью страницу PDF для поворота?**  
A: Используйте коллекцию страниц SDK с нулевой индексацией, например `pdfDocument.Pages[2]`, поскольку индекс 2 соответствует третьей странице.

**Q: Можно ли повернуть страницу на угол, отличный от 180 градусов?**  
A: Свойство вращения принимает только четыре стандартных значения: 0, 90, 180 и 270 градусов; любое другое значение округляется до ближайшего допустимого угла.

**Q: Выполняет ли поворот страницы автоматическое изменение оригинального файла?**  
A: Поворот применяется только к объекту `PdfDocument` в памяти; необходимо вызвать `pdfDocument.Save(\"output.pdf\")` (или аналогичный метод сохранения), чтобы записать изменения в новый файл, оставив исходный без изменений.

**Q: Что происходит с аннотациями или полями формы после поворота страницы?**  
A: SDK автоматически пересчитывает позиции аннотаций и полей формы, чтобы они оставались правильно выровненными относительно новой ориентации.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}