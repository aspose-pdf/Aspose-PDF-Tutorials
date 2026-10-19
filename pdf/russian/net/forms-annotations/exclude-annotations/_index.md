---
title: Сравнение PDF бок о бок с исключением аннотаций с помощью Aspose.Pdf for .NET
weight: 101
limit:
description: Пошаговое руководство по сравнению PDF‑файлов и исключению областей аннотаций с использованием Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Пошаговое руководство по сравнению PDF‑файлов и исключению областей
    аннотаций с использованием Aspose.Pdf for .NET.
  headline: Сравнение PDF бок о бок с исключением аннотаций с помощью Aspose.Pdf for
    .NET
  type: TechArticle
- description: Пошаговое руководство по сравнению PDF‑файлов и исключению областей
    аннотаций с использованием Aspose.Pdf for .NET.
  name: Сравнение PDF бок о бок с исключением аннотаций с помощью Aspose.Pdf for .NET
  steps:
  - name: Укажите пути к файлам для основного PDF, вторичного PDF и выходного diff
      PDF.
    text: Укажите пути к файлам для основного PDF, вторичного PDF и выходного diff
      PDF.
  - name: Проверьте, что оба входных PDF‑файла существуют, и при отсутствии любого
      из них завершите работу с сообщением об ошибке.
    text: Проверьте, что оба входных PDF‑файла существуют, и при отсутствии любого
      из них завершите работу с сообщением об ошибке.
  - name: Откройте два PDF‑файла как объекты Document (pdfA и pdfB) внутри блока using,
      чтобы они автоматически освобождались.
    text: Откройте два PDF‑файла как объекты Document (pdfA и pdfB) внутри блока using,
      чтобы они автоматически освобождались.
  - name: Соберите ограничивающие прямоугольники всех аннотаций в pdfA и сохраните
      их в ignoredRectsA.
    text: Соберите ограничивающие прямоугольники всех аннотаций в pdfA и сохраните
      их в ignoredRectsA.
  - name: Соберите ограничивающие прямоугольники всех аннотаций в pdfB и сохраните
      их в ignoredRectsB.
    text: Соберите ограничивающие прямоугольники всех аннотаций в pdfB и сохраните
      их в ignoredRectsB.
  - name: Создайте объект SideBySideComparisonOptions и присвойте ранее собранные
      прямоугольники аннотаций свойствам ExcludeAreas1 и ExcludeAreas2, чтобы эти
      области игнорировались при сравнении.
    text: Создайте объект SideBySideComparisonOptions и присвойте ранее собранные
      прямоугольники аннотаций свойствам ExcludeAreas1 и ExcludeAreas2, чтобы эти
      области игнорировались при сравнении.
  - name: Запустите сравнение PDF бок о бок, используя два объекта Document и настроенные
      параметры, записав результат в outputPdf.
    text: Запустите сравнение PDF бок о бок, используя два объекта Document и настроенные
      параметры, записав результат в outputPdf.
  - name: Освободите объекты Document и выйдите из блока using.
    text: Освободите объекты Document и выйдите из блока using.
  - name: Выведите подтверждающее сообщение, указывающее, что сравнение завершено,
      и где сохранён diff PDF.
    text: Выведите подтверждающее сообщение, указывающее, что сравнение завершено,
      и где сохранён diff PDF.
  type: HowTo
- questions:
  - answer: Да. Код просто не добавляет прямоугольники в соответствующий список `ignoredRects`,
      поэтому `ExcludeAreas1`/`ExcludeAreas2` получают пустой массив, и сравниватель
      обрабатывает всю страницу.
    question: Что произойдёт, если на странице PDF нет аннотаций – будет ли сравнение
      работать?
  - answer: Установите `ExcludeAreas1` (или `ExcludeAreas2`) в собранные прямоугольники
      и оставьте другое свойство пустым массивом; сравниватель будет игнорировать
      области только в указанном документе.
    question: Можно ли исключить аннотации только из одного документа, оставив аннотации
      другого в diff‑файле?
  - answer: Перекрывающиеся прямоугольники объединяются внутри сравнивателя, поэтому
      границы перекрывающихся аннотаций безопасно исключаются без двойного учёта.
    question: Вызывают ли перекрывающиеся прямоугольники аннотаций какие‑либо проблемы
      с `ExcludeAreas`?
  - answer: Да, установите `compareOpts.ExcludeTables = true;` — этот флаг работает
      вместе с `ExcludeAreas1`/`ExcludeAreas2`, чтобы также игнорировать области таблиц.
    question: Можно ли исключить таблицы в дополнение к аннотациям, используя тот
      же объект параметров?
  - answer: Код проверяет `if (a != null && a.Rect != null)` перед добавлением в список,
      поэтому null‑прямоугольники просто пропускаются и исключение не выбрасывается.
    question: Что если свойство `Rect` у аннотации равно null – вызовет ли код исключение?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Сравнение PDF без аннотаций
og_description: Выполните сравнение PDF бок о бок, которое пропускает все метки аннотаций.
og_image_alt: Руководство, показывающее сравнение PDF бок о бок с исключением областей аннотаций с помощью Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Сравнение PDF бок о бок с исключением аннотаций с помощью Aspose.Pdf
В этом учебнике показано, как сравнивать два PDF‑файла с помощью Aspose.Pdf for .NET, игнорируя содержимое аннотаций. Он извлекает ограничивающие рамки всех аннотаций из каждого документа, передаёт эти области в SideBySideComparisonOptions и затем выполняет сравнение бок о бок. В результате получается diff PDF, в котором выделены только изменения, не связанные с аннотациями.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: Что произойдёт, если на странице PDF нет аннотаций – будет ли сравнение работать?**  
A: Да. Код просто не добавляет прямоугольники в соответствующий список `ignoredRects`, поэтому `ExcludeAreas1`/`ExcludeAreas2` получают пустой массив, и сравниватель обрабатывает всю страницу.

**Q: Можно ли исключить аннотации только из одного документа, оставив аннотации другого в diff‑файле?**  
A: Установите `ExcludeAreas1` (или `ExcludeAreas2`) в собранные прямоугольники и оставьте другое свойство пустым массивом; сравниватель будет игнорировать области только в указанном документе.

**Q: Вызывают ли перекрывающиеся прямоугольники аннотаций какие‑либо проблемы с `ExcludeAreas`?**  
A: Перекрывающиеся прямоугольники объединяются внутри сравнивателя, поэтому границы перекрывающихся аннотаций безопасно исключаются без двойного учёта.

**Q: Можно ли исключить таблицы в дополнение к аннотациям, используя тот же объект параметров?**  
A: Да, установите `compareOpts.ExcludeTables = true;` — этот флаг работает вместе с `ExcludeAreas1`/`ExcludeAreas2`, чтобы также игнорировать области таблиц.

**Q: Что если свойство `Rect` у аннотации равно null – вызовет ли код исключение?**  
A: Код проверяет `if (a != null && a.Rect != null)` перед добавлением в список, поэтому null‑прямоугольники просто пропускаются и исключение не выбрасывается.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}