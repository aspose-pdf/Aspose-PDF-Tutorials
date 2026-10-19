---
title: Сравнение PDF, игнорируя определённые области, с использованием Aspose.Pdf for .NET
weight: 201
limit:
description: Научитесь сравнивать PDF бок о бок и игнорировать выбранные области с помощью Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Научитесь сравнивать PDF бок о бок и игнорировать выбранные области
    с помощью Aspose.Pdf for .NET.
  headline: Сравнение PDF, игнорируя определённые области, с использованием Aspose.Pdf
    for .NET
  type: TechArticle
- description: Научитесь сравнивать PDF бок о бок и игнорировать выбранные области
    с помощью Aspose.Pdf for .NET.
  name: Сравнение PDF, игнорируя определённые области, с использованием Aspose.Pdf
    for .NET
  steps:
  - name: Укажите пути к файлам двух исходных PDF и выходному PDF‑diff.
    text: Укажите пути к файлам двух исходных PDF и выходному PDF‑diff.
  - name: Проверьте, что оба исходных PDF‑файла существуют, и при отсутствии любого
      из них завершите работу с сообщением об ошибке.
    text: Проверьте, что оба исходных PDF‑файла существуют, и при отсутствии любого
      из них завершите работу с сообщением об ошибке.
  - name: Создайте массив, содержащий прямоугольную область, которую нужно игнорировать
      в первом PDF.
    text: Создайте массив, содержащий прямоугольную область, которую нужно игнорировать
      в первом PDF.
  - name: Создайте массив, содержащий прямоугольную область, которую нужно игнорировать
      во втором PDF.
    text: Создайте массив, содержащий прямоугольную область, которую нужно игнорировать
      во втором PDF.
  - name: Настройте сравнение бок о бок, присвоив массивы игнорируемых областей соответствующим
      свойствам.
    text: Настройте сравнение бок о бок, присвоив массивы игнорируемых областей соответствующим
      свойствам.
  - name: Загрузите оба PDF и выполните сравнение бок о бок, создав файл diff по указанному
      пути.
    text: Загрузите оба PDF и выполните сравнение бок о бок, создав файл diff по указанному
      пути.
  - name: Выведите подтверждающее сообщение, указывающее, что сравнение завершено,
      и где сохранён PDF‑diff.
    text: Выведите подтверждающее сообщение, указывающее, что сравнение завершено,
      и где сохранён PDF‑diff.
  type: HowTo
- questions:
  - answer: Координаты задаются в пунктах (1/72 дюйма) с началом в левом нижнем угле
      страницы, поэтому первые два числа — это X/Y левого нижнего угла, а последние
      два — X/Y правого верхнего угла.
    question: Какую систему координат используют значения `Rectangle` при определении
      зон игнорирования?
  - answer: Да — передайте несколько объектов `Aspose.Pdf.Rectangle` в массив `ExcludeAreas1`
      (или `ExcludeAreas2`); каждый прямоугольник будет исключён независимо во время
      сравнения.
    question: Можно ли игнорировать более одной прямоугольной области в одном документе?
  - answer: Нет. `ExcludeAreas1` применяется к первому PDF, а `ExcludeAreas2` — ко
      второму, поэтому можно задать разные координаты для каждого документа.
    question: Должны ли игнорируемые прямоугольники быть одинаковыми в обоих PDF?
  - answer: Aspose.Pdf тихо игнорирует прямоугольники, полностью находящиеся за пределами
      страницы; они не влияют на результат сравнения.
    question: Что происходит, если прямоугольник определён за пределами границ страницы?
  - answer: Массивы `ExcludeAreas` применяются к каждой странице, поэтому необходимо
      добавить одинаковый `Rectangle` в коллекцию каждой страницы (например, пройтись
      в цикле по `pdf.Pages` и присвоить массив) перед вызовом `SideBySidePdfComparer.Compare`.
    question: Как исключить одну и ту же область на каждой странице PDF?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Игнорирование областей при сравнении PDF
og_description: Посмотрите, как пропускать выбранные области при сравнении PDF бок о бок и получать чистый PDF‑diff.
og_image_alt: Руководство, показывающее сравнение PDF бок о бок с исключёнными прямоугольными областями с использованием Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Сравнение PDF, игнорируя определённые области, с использованием Aspose.Pdf
Этот учебник демонстрирует, как сравнивать два PDF‑документа бок о бок с помощью Aspose.Pdf for .NET, исключая из анализа заданные прямоугольные области. Определяя области исключения в каждом файле, создаваемый PDF‑diff выделяет только значимые изменения, упрощая фокусировку на релевантных различиях.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Какую систему координат используют значения `Rectangle` при определении зон игнорирования?**  
A: Координаты задаются в пунктах (1/72 дюйма) с началом в левом нижнем угле страницы, поэтому первые два числа — это X/Y левого нижнего угла, а последние два — X/Y правого верхнего угла.

**Q: Можно ли игнорировать более одной прямоугольной области в одном документе?**  
A: Да — передайте несколько объектов `Aspose.Pdf.Rectangle` в массив `ExcludeAreas1` (или `ExcludeAreas2`); каждый прямоугольник будет исключён независимо во время сравнения.

**Q: Должны ли игнорируемые прямоугольники быть одинаковыми в обоих PDF?**  
A: Нет. `ExcludeAreas1` применяется к первому PDF, а `ExcludeAreas2` — ко второму, поэтому можно задать разные координаты для каждого документа.

**Q: Что происходит, если прямоугольник определён за пределами границ страницы?**  
A: Aspose.Pdf тихо игнорирует прямоугольники, полностью находящиеся за пределами страницы; они не влияют на результат сравнения.

**Q: Как исключить одну и ту же область на каждой странице PDF?**  
A: Массивы `ExcludeAreas` применяются к каждой странице, поэтому необходимо добавить одинаковый `Rectangle` в коллекцию каждой страницы (например, пройтись в цикле по `pdf.Pages` и присвоить массив) перед вызовом `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}