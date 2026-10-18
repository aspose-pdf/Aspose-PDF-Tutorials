---
title: Сравнение PDF‑файлов и создание выделенного diff‑документа с помощью Aspose.PDF for .NET
weight: 101
limit:
description: Узнайте, как сравнить два PDF‑файла и создать выделенный diff‑PDF с помощью Aspose.PDF for .NET.
keywords: [pdf comparison, Aspose.PDF for .NET, compare pdf files, generate diff pdf, pdf diff highlighting, pdf document comparison]
url: /net/document-manipulation/compare-pdfs/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Узнайте, как сравнить два PDF‑файла и создать выделенный diff‑PDF с
    помощью Aspose.PDF for .NET.
  headline: Сравнение PDF‑файлов и создание выделенного diff‑документа с помощью Aspose.PDF
    for .NET
  type: TechArticle
- description: Узнайте, как сравнить два PDF‑файла и создать выделенный diff‑PDF с
    помощью Aspose.PDF for .NET.
  name: Сравнение PDF‑файлов и создание выделенного diff‑документа с помощью Aspose.PDF
    for .NET
  steps:
  - name: Объявите пути к файлам оригинального, изменённого и diff‑выходного PDF.
    text: Объявите пути к файлам оригинального, изменённого и diff‑выходного PDF.
  - name: Проверьте, что оба входных PDF‑файла существуют, и при отсутствии любого
      из них прервите выполнение с сообщением об ошибке.
    text: Проверьте, что оба входных PDF‑файла существуют, и при отсутствии любого
      из них прервите выполнение с сообщением об ошибке.
  - name: Загрузите оригинальный и изменённый PDF в объекты `Document` внутри блока
      `using`.
    text: Загрузите оригинальный и изменённый PDF в объекты `Document` внутри блока
      `using`.
  - name: Создайте экземпляр `ComparisonOptions` с настройками по умолчанию для сравнения.
    text: Создайте экземпляр `ComparisonOptions` с настройками по умолчанию для сравнения.
  - name: Выполните сравнение, создав diff‑PDF по пути `outputPath`, который выделяет
      различия между двумя документами.
    text: Выполните сравнение, создав diff‑PDF по пути `outputPath`, который выделяет
      различия между двумя документами.
  - name: Выведите подтверждающее сообщение, указывающее, что diff‑PDF был создан.
    text: Выведите подтверждающее сообщение, указывающее, что diff‑PDF был создан.
  - name: Закройте блок `using`, освободив объекты `Document` источника и назначения.
    text: Закройте блок `using`, освободив объекты `Document` источника и назначения.
  type: HowTo
- questions:
  - answer: Код проверяет `File.Exists` для `originalDocument.pdf` и `modifiedDocument.pdf`;
      если любой из файлов отсутствует, он выводит ошибку в `Console.Error` и завершает
      работу без создания diff‑PDF.
    question: Что произойдёт, если один из входных PDF‑файлов не существует?
  - answer: Нет, в текущей версии Aspose.Pdf.Comparison отсутствует флаг `TextComparisonOptions`
      для сравнения без учёта регистра, поэтому изменения регистра будут отображаться
      как различия в сгенерированном diff‑PDF.
    question: Можно ли настроить сравнение так, чтобы игнорировать различия регистра
      в тексте?
  - answer: '`TextPdfComparer.CompareFlatDocuments(sourceDoc, targetDoc, compareOpts,
      outputPath)` выполняет сравнение с использованием переданных `ComparisonOptions`
      и записывает выделенные различия в `diffOutput.pdf`.'
    question: Какой метод фактически выполняет сравнение PDF и создаёт diff‑файл?
  - answer: Операторы `using` автоматически вызывают `Dispose` для `sourceDoc` и `targetDoc`
      по завершении блока, поэтому дополнительный код для освобождения не требуется.
    question: Нужно ли вручную освобождать объекты `Document`?
  type: FAQPage
images:
- /net/document-manipulation/compare-pdfs/og-image.png
og_title: Создание diff‑PDF путём сравнения двух PDF‑файлов
og_description: Создайте выделенный diff‑PDF, чтобы увидеть изменения между двумя документами, используя Aspose.PDF for .NET.
og_image_alt: Руководство, показывающее, как сравнить два PDF‑файла и создать diff‑PDF, выделяющий изменения, с помощью Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Сравнение PDF‑файлов и создание выделенного diff‑документа с помощью Aspose.PDF
Этот учебный материал демонстрирует, как использовать Aspose.Pdf.Comparison для сравнения двух PDF‑файлов и создания diff‑PDF, который чётко выделяет различия. Вы узнаете, как загрузить оригинальный и изменённый документы, выполнить сравнение и сохранить полученный diff‑файл. Пошаговый код показывает точный процесс создания визуального отчёта о сравнении.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/compare-pdfs" >}}


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

**Q: Что произойдёт, если один из входных PDF‑файлов не существует?**  
A: Код проверяет `File.Exists` для `originalDocument.pdf` и `modifiedDocument.pdf`; если любой из файлов отсутствует, он выводит ошибку в `Console.Error` и завершает работу без создания diff‑PDF.

**Q: Можно ли настроить сравнение так, чтобы игнорировать различия регистра в тексте?**  
A: Нет, в текущей версии Aspose.Pdf.Comparison отсутствует флаг `TextComparisonOptions` для сравнения без учёта регистра, поэтому изменения регистра будут отображаться как различия в сгенерированном diff‑PDF.

**Q: Какой метод фактически выполняет сравнение PDF и создаёт diff‑файл?**  
A: `TextPdfComparer.CompareFlatDocuments(sourceDoc, targetDoc, compareOpts, outputPath)` выполняет сравнение с использованием переданных `ComparisonOptions` и записывает выделенные различия в `diffOutput.pdf`.

**Q: Нужно ли вручную освобождать объекты `Document`?**  
A: Операторы `using` автоматически вызывают `Dispose` для `sourceDoc` и `targetDoc` по завершении блока, поэтому дополнительный код для освобождения не требуется.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}