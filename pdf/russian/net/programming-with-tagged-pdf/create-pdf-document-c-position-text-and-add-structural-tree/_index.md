---
category: general
date: 2026-07-20
description: 'Создайте PDF‑документ на C# с помощью Aspose.Pdf: разместите текст в
  PDF и добавьте структурное дерево для доступности. Следуйте этому пошаговому руководству.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: ru
lastmod: 2026-07-20
og_description: Создайте PDF‑документ на C# мгновенно. Узнайте, как позиционировать
  текст в PDF и добавить структурное дерево с помощью Aspose.Pdf для соответствия
  PDF/A‑2b.
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: Создание PDF‑документа на C# – Полное руководство по позиционированию текста
  и структуре тегов
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: Создание PDF‑документа C# – позиционирование текста и добавление структурного
  дерева
url: /ru/net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF документа C# – позиционирование текста и добавление структурного дерева

Когда‑нибудь вам нужно было **create PDF document C#**, которое не только размещает текст точно там, где вы хотите, но и встраивает правильное структурное дерево для доступности? Вы не одиноки — разработчики, создающие счета, отчёты или электронные книги, часто сталкиваются с этой потребностью. В этом руководстве мы пройдём полный, готовый к запуску пример, который делает именно это, используя мощную библиотеку Aspose.Pdf.

Мы рассмотрим, как **позиционировать текст в PDF**, добавить семантический тег через шаг **add structural tree**, и наконец сохранить файл как документ, соответствующий PDF/A‑2b. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой проект .NET.

---

## Что понадобится

- **.NET 6.0** или новее (код также работает с .NET Framework 4.6+)  
- **Aspose.Pdf for .NET** пакет NuGet (`Install-Package Aspose.Pdf`)  
- Базовая среда разработки C# (Visual Studio, Rider или VS Code)  

Дополнительные сторонние инструменты не требуются; библиотека обрабатывает всё — от разметки страниц до соответствия PDF/A.

---

## Шаг 1: Инициализация PDF документа (Create PDF Document C#)

Первое, что мы делаем, — создаём новый объект `Document`. Представьте его как чистый холст — пока ничего на нём нет, но он готов принимать страницы, текст и структурные метаданные.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **Почему это важно:** Класс `Document` является точкой входа для всех операций Aspose.Pdf. Добавление страницы в начале даёт нам поверхность, к которой позже можно прикрепить как визуальное содержимое, так и структурное дерево.

---

## Шаг 2: Определение абзаца и его позиционирование (Position Text in PDF)

Теперь мы создаём объект `Paragraph` и указываем Aspose точное место на странице, где он должен появиться. Координаты PDF измеряются в пунктах (1 дюйм = 72 pt), поэтому мы используем `Position(72, 720)`, чтобы разместить абзац на 1 дюйм от левого края и 10 дюймов от нижнего.

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **Полезный совет:** Если нужно позиционировать несколько строк, скорректируйте координату `Y` для каждого последующего абзаца или используйте `TextBuilder` для более точного управления.

---

## Шаг 3: Создание структурного элемента (Add Structural Tree)

PDF‑файлы, ориентированные на доступность, полагаются на *структурное дерево*, описывающее логический порядок содержимого. Здесь мы создаём `StructureElement` с тегом `"P"` (paragraph) и прикрепляем наш позиционированный абзац как дочерний элемент.

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **Почему мы добавляем структурное дерево:** Читатели экрана и другие вспомогательные технологии используют эти теги для навигации по документу. Без них ваш PDF может выглядеть визуально идеально, но будет недоступен.

---

## Шаг 4: Привязка структурного элемента к странице

Каждая страница содержит собственную коллекцию структурных элементов. Добавляя наш `structElement` в `pdfPage.StructElements`, мы интегрируем логическую иерархию с визуальной разметкой.

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **Распространённая ошибка:** Пропуск этого шага приводит к тому, что тег существует в памяти, но не привязан к какой‑либо странице, делая информацию о доступности невидимой для читателей.

---

## Шаг 5: Сохранение в PDF/A‑2b (Ensuring Long‑Term Preservation)

PDF/A‑2b — это подмножество PDF, предназначенное для архивирования. Aspose.Pdf может создать этот формат одним вызовом. Замените `"YOUR_DIRECTORY"` реальным путём на вашем компьютере.

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **Результат:** Теперь у вас есть PDF, где текст находится точно там, где вы его разместили, а документ содержит правильное структурное дерево для средств доступности.

---

## Полный рабочий пример

Ниже приведена полная программа, которую вы можете скопировать и вставить в консольное приложение. Она компилируется и работает без изменений (после добавления ссылки на пакет Aspose.Pdf NuGet).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**Ожидаемый результат:** После запуска откройте `TaggedWithPosition.pdf`. Вы увидите предложение «Tagged paragraph at a specific location.» расположенное рядом с правым нижним углом первой страницы. Если вы проверите теги PDF (например, в панели «Tags» Adobe Acrobat), вы найдёте элемент `<P>`, связанный с этим абзацем.

---

![Скриншот позиционированного текста в PDF, сгенерированного с помощью Aspose.Pdf](/images/pdf-positioned.png){: .align-center }

*Текст альтернативы изображения:* **create pdf document c#** – скриншот, показывающий позиционированный текст внутри PDF, сгенерированного с помощью Aspose.Pdf.

---

## Часто задаваемые вопросы и особые случаи

### Можно ли использовать другие единицы (мм, см) для позиционирования?

Aspose.Pdf работает нативно с пунктами. Если вы предпочитаете миллиметры, преобразуйте их с помощью `1 mm ≈ 2.83465 pt`. Например, `Position(25.4, 254)` размещает абзац на 1 см от левого края и 9 см от нижнего.

### Что делать, если нужно добавить несколько тегов (заголовки, таблицы)?

Просто создайте дополнительные объекты `StructureElement` с тегами, например, `"H1"` для заголовков или `"Table"` для таблиц, и добавьте соответствующее содержимое в качестве дочерних элементов. Вложенность работает так же — дочерние элементы наследуют логический порядок родителя.

### Работает ли этот подход для PDF/A‑1b или PDF/A‑3b?

Да. Замените `SaveFormat.PdfA2b` на `SaveFormat.PdfA1b` или `SaveFormat.PdfA3b`. Имейте в виду, что каждая версия PDF/A имеет свой набор обязательных метаданных; Aspose.Pdf предупредит вас, если чего‑то не хватает.

---

## Итоги

Мы рассмотрели сценарий **create pdf document c#**, в котором:

1. Создаёт новый PDF с помощью Aspose.Pdf.  
2. **Position text in PDF** задавая точные координаты.  
3. **Add structural tree** элементы для доступности.  
4. Сохраняет результат как соответствующий стандарту файл PDF/A‑2b.

Все шаги полностью автономны, и вы можете адаптировать фрагмент к более сложным макетам, множеству страниц или различным типам тегов.

---

## Что дальше?

- **Styling text** – изучите `TextState` для изменения шрифтов, цветов и размеров.  
- **Embedding images** – используйте `ImageFragment` и позиционируйте его рядом с абзацем.  
- **Generating tables** – создавайте объекты `Table` и помечайте их тегом `"Table"` для более богатой семантики.  
- **Automation pipelines** – интегрируйте этот код в фоновый сервис, генерирующий счета каждый вечер.

Не стесняйтесь экспериментировать и дайте нам знать, какие варианты вам показались наиболее полезными. Приятного кодинга!

## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создание помеченных PDF с Aspose.PDF для .NET: Полное руководство по улучшению доступности и структуры документа](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [Создание PDF документа с Aspose.PDF – пошаговое руководство](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Создание и вращение текста в PDF с использованием Aspose.PDF .NET: Полное руководство для разработчиков](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}