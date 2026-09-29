---
title: Добавление помечённой внешней ссылки с подсказкой в PDF с помощью Aspose.Pdf for .NET
weight: 440
limit:
description: Узнайте, как добавить помеченную внешнюю гиперссылку с отображаемым текстом и подсказкой в PDF с помощью Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Узнайте, как добавить помеченную внешнюю гиперссылку с отображаемым
    текстом и подсказкой в PDF с помощью Aspose.Pdf for .NET.
  headline: Добавление помечённой внешней ссылки с подсказкой в PDF с помощью Aspose.Pdf
    for .NET
  type: TechArticle
- description: Узнайте, как добавить помеченную внешнюю гиперссылку с отображаемым
    текстом и подсказкой в PDF с помощью Aspose.Pdf for .NET.
  name: Добавление помечённой внешней ссылки с подсказкой в PDF с помощью Aspose.Pdf
    for .NET
  steps:
  - name: Определите пути к исходному PDF и файлу результата.
    text: Определите пути к исходному PDF и файлу результата.
  - name: Проверьте, существует ли исходный PDF, и прервите выполнение, если он не
      найден.
    text: Проверьте, существует ли исходный PDF, и прервите выполнение, если он не
      найден.
  - name: Откройте PDF‑документ внутри блока using, чтобы обеспечить корректное освобождение
      ресурсов.
    text: Откройте PDF‑документ внутри блока using, чтобы обеспечить корректное освобождение
      ресурсов.
  - name: Получите менеджер помеченного содержимого (tagged‑content manager) для открытого
      документа.
    text: Получите менеджер помеченного содержимого (tagged‑content manager) для открытого
      документа.
  - name: Установите язык документа на English (US) и задайте PDF‑заголовок, полученный
      из имени файла.
    text: Установите язык документа на English (US) и задайте PDF‑заголовок, полученный
      из имени файла.
  - name: Получите корневой элемент дерева логической структуры, в который будут добавляться
      новые элементы.
    text: Получите корневой элемент дерева логической структуры, в который будут добавляться
      новые элементы.
  - name: Создайте объект LinkElement, задайте его отображаемый текст, целевой URL
      и заголовок всплывающей подсказки, затем вставьте его в структуру документа.
    text: Создайте объект LinkElement, задайте его отображаемый текст, целевой URL
      и заголовок всплывающей подсказки, затем вставьте его в структуру документа.
  - name: Сохраните обновлённый PDF в указанный файл результата.
    text: Сохраните обновлённый PDF в указанный файл результата.
  - name: Выведите сообщение подтверждения, указывающее, куда был сохранён изменённый
      PDF.
    text: Выведите сообщение подтверждения, указывающее, куда был сохранён изменённый
      PDF.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` возвращает существующее помеченное содержимое,
      если документ уже помечен; он не создаёт дублирующее дерево.'
    question: Что если исходный PDF уже помечен — создаст ли вызов `pdfDoc.TaggedContent`
      новое дерево тегов или переиспользует существующее?
  - answer: Да — найдите нужный `StructureElement` (например, `Div` или `Paragraph`
      на странице) через дерево логической структуры и вызовите `AppendChild(externalLink)`
      у этого элемента.
    question: Можно ли разместить гиперссылку на конкретной странице, а не добавлять
      её к корневому элементу?
  - answer: Подсказка отображается только если `externalLink.Title` установлен до
      `pdfDoc.Save`; установка после сохранения не влияет на уже записанный PDF.
    question: Требуется ли свойство `Title` у `LinkElement` для отображения подсказки,
      и можно ли установить его после вызова `Save`?
  - answer: Назначьте `FileSpecification` (например, `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`)
      свойству `externalLink.Hyperlink` вместо использования `WebHyperlink`.
    question: Как создать ссылку на локальный файл вместо веб‑URL?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Вставка помечённой внешней ссылки с подсказкой в PDF
og_description: Внедрите доступную гиперссылку с видимым текстом и подсказкой в ваш PDF с помощью Aspose.Pdf for .NET.
og_image_alt: Руководство, показывающее, как добавить помеченную внешнюю гиперссылку с подсказкой в PDF с помощью Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Добавление помечённой внешней ссылки с подсказкой в PDF с помощью Aspose.Pdf
В этом руководстве показано, как открыть существующий PDF с помощью Aspose.Pdf for .NET, создать помеченную внешнюю гиперссылку, включающую видимый отображаемый текст и заголовок всплывающей подсказки, вставить ссылку в логическую структуру документа и сохранить обновлённый файл. Следуя этим шагам, вы получите доступный PDF, где ссылка является частью иерархии тегов и предоставляет дополнительный контекст читателям.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: Что если исходный PDF уже помечен — создаст ли вызов `pdfDoc.TaggedContent` новое дерево тегов или переиспользует существующее?**  
A: `pdfDoc.TaggedContent` возвращает существующее помеченное содержимое, если документ уже помечен; он не создаёт дублирующее дерево.

**Q: Можно ли разместить гиперссылку на конкретной странице, а не добавлять её к корневому элементу?**  
A: Да — найдите нужный `StructureElement` (например, `Div` или `Paragraph` на странице) через дерево логической структуры и вызовите `AppendChild(externalLink)` у этого элемента.

**Q: Требуется ли свойство `Title` у `LinkElement` для отображения подсказки, и можно ли установить его после вызова `Save`?**  
A: Подсказка отображается только если `externalLink.Title` установлен до `pdfDoc.Save`; установка после сохранения не влияет на уже записанный PDF.

**Q: Как создать ссылку на локальный файл вместо веб‑URL?**  
A: Назначьте `FileSpecification` (например, `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`) свойству `externalLink.Hyperlink` вместо использования `WebHyperlink`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}