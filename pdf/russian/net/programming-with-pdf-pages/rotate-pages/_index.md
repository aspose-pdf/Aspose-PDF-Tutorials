---
title: Повернуть каждую страницу PDF на 180° с помощью Aspose.Pdf для .NET
weight: 260
limit:
description: Пошаговое руководство по повороту всех страниц PDF на 180 градусов с помощью Aspose.Pdf для .NET.
keywords: [rotate pdf pages .net, Aspose.Pdf for .NET, rotate all pages 180 degrees, pdf page rotation, c# pdf manipulation]
url: /net/programming-with-pdf-pages/rotate-pages/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Пошаговое руководство по повороту всех страниц PDF на 180 градусов
    с помощью Aspose.Pdf для .NET.
  headline: Повернуть каждую страницу PDF на 180° с помощью Aspose.Pdf для .NET
  type: TechArticle
- description: Пошаговое руководство по повороту всех страниц PDF на 180 градусов
    с помощью Aspose.Pdf для .NET.
  name: Повернуть каждую страницу PDF на 180° с помощью Aspose.Pdf для .NET
  steps:
  - name: Объявите пути к исходному и целевому файлам PDF.
    text: Объявите пути к исходному и целевому файлам PDF.
  - name: Проверьте, существует ли исходный файл, и при его отсутствии прервите выполнение
      с выводом сообщения об ошибке.
    text: Проверьте, существует ли исходный файл, и при его отсутствии прервите выполнение
      с выводом сообщения об ошибке.
  - name: Создайте объект Document для исходного PDF внутри блока using, чтобы управлять
      ресурсами.
    text: Создайте объект Document для исходного PDF внутри блока using, чтобы управлять
      ресурсами.
  - name: Пройдитесь по каждому объекту Page в pdfDoc.Pages и установите его свойство
      Rotate в Rotation.on180, тем самым перевернув каждую страницу вверх дном.
    text: Пройдитесь по каждому объекту Page в pdfDoc.Pages и установите его свойство
      Rotate в Rotation.on180, тем самым перевернув каждую страницу вверх дном.
  - name: Сохраните изменённый Document в целевой файл, сохранив выполненные повороты.
    text: Сохраните изменённый Document в целевой файл, сохранив выполненные повороты.
  - name: Выведите подтверждающее сообщение в консоль, указывающее, что операция завершена.
    text: Выведите подтверждающее сообщение в консоль, указывающее, что операция завершена.
  type: HowTo
- questions:
  - answer: Код проверяет `File.Exists(sourceFile)` и записывает ошибку в `Console.Error`
      перед возвратом, поэтому исключение не выбрасывается, и программа завершается
      корректно.
    question: Что произойдёт, если исходный PDF‑файл не существует?
  - answer: Да, замените `Rotation.on180` другим значением перечисления, например
      `Rotation.on90` (по часовой стрелке) или `Rotation.on270` (против часовой стрелки),
      чтобы применить иной поворот.
    question: Могу ли я повернуть страницы на другой угол, например, на 90° по часовой
      стрелке?
  - answer: Коллекция `Pages` в Aspose.Pdf имеет индексацию, начинающуюся с 1, но
      итератор `foreach` скрывает это, проходя по каждому объекту `Page` независимо
      от базового индекса.
    question: Является ли коллекция страниц нулевой индексацией? Как работает цикл
      `foreach`?
  - answer: Вызов `pdfDoc.Save(destinationFile)` перезапишет любой существующий файл
      с таким именем, поэтому используйте другое имя файла или сделайте резервную
      копию оригинала, если нужно его сохранить.
    question: Будет ли оригинальный PDF перезаписан, если я использую то же имя файла
      для `destinationFile`?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pages/og-image.png
og_title: Повернуть каждую страницу PDF на 180°
og_description: Узнайте, как перевернуть все страницы PDF вверх дном всего в несколько строк кода на C#.
og_image_alt: Руководство, показывающее, как повернуть каждую страницу PDF на 180 градусов с использованием Aspose.Pdf для .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Повернуть каждую страницу PDF на 180° с помощью Aspose.Pdf для .NET
Этот учебный материал показывает, как повернуть каждую страницу существующего PDF‑документа на 180 градусов с помощью класса Aspose.Pdf Document. Применяя поворот всей страницы, вы можете быстро исправить перевёрнутые сканы или переориентировать документы без их повторного создания. Пример написан на C# и работает на платформе .NET.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pages" >}}


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

**Q: Что произойдёт, если исходный PDF‑файл не существует?**  
A: Код проверяет `File.Exists(sourceFile)` и записывает ошибку в `Console.Error` перед возвратом, поэтому исключение не выбрасывается, и программа завершается корректно.

**Q: Могу ли я повернуть страницы на другой угол, например, на 90° по часовой стрелке?**  
A: Да, замените `Rotation.on180` другим значением перечисления, например `Rotation.on90` (по часовой стрелке) или `Rotation.on270` (против часовой стрелки), чтобы применить иной поворот.

**Q: Является ли коллекция страниц нулевой индексацией? Как работает цикл `foreach`?**  
A: Коллекция `Pages` в Aspose.Pdf имеет индексацию, начинающуюся с 1, но итератор `foreach` скрывает это, проходя по каждому объекту `Page` независимо от базового индекса.

**Q: Будет ли оригинальный PDF перезаписан, если я использую то же имя файла для `destinationFile`?**  
A: Вызов `pdfDoc.Save(destinationFile)` перезапишет любой существующий файл с таким именем, поэтому используйте другое имя файла или сделайте резервную копию оригинала, если нужно его сохранить.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}