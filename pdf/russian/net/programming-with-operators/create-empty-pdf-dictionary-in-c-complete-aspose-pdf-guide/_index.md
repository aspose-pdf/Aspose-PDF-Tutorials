---
category: general
date: 2026-07-26
description: Создайте пустой словарь PDF с помощью Aspose.Pdf в C#. Узнайте пошагово,
  как добавить графическое состояние в словарь ExtGState для работы с PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty pdf dictionary
- Aspose.Pdf
- ExtGState dictionary
- CosPdfDictionary
- PDF graphics state
- C# PDF manipulation
language: ru
lastmod: 2026-07-26
og_description: Создайте пустой PDF‑словарь с помощью Aspose.Pdf для C#. Следуйте
  этому практическому руководству, чтобы изменять графические состояния в ваших PDF‑файлах.
og_image_alt: Diagram showing how to create empty PDF dictionary with Aspose.Pdf in
  C#
og_title: Создание пустого словаря PDF в C# – Полный учебник по Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: Create empty PDF dictionary with Aspose.Pdf in C#. Learn step‑by‑step
    how to add a graphics state to ExtGState dictionary for PDF manipulation.
  headline: Create Empty PDF Dictionary in C# – Complete Aspose.Pdf Guide
  type: TechArticle
tags:
- Aspose
- PDF
- C#
- GraphicsState
title: Создание пустого словаря PDF в C# – Полное руководство по Aspose.Pdf
url: /ru/net/programming-with-operators/create-empty-pdf-dictionary-in-c-complete-aspose-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание пустого PDF‑словаря в C# – Полное руководство по Aspose.Pdf

Когда‑то задавались вопросом, как **создать пустой PDF‑словарь** при настройке графического состояния PDF? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, пытаясь программно изменить непрозрачность или режимы наложения. В этом руководстве мы пройдем конкретное решение с использованием Aspose.Pdf для C#, показывая, как внедрить новое графическое состояние в словарь *ExtGState* существующего PDF.

Мы охватим всё, что вам нужно: загрузку PDF, доступ к словарю ресурсов, создание нового **CosPdfDictionary** и, наконец, сохранение изменений. К концу вы получите переиспользуемый шаблон для любых настроек *PDF graphics state*, которые вам могут понадобиться.

---

## Что вы узнаете

- Как **создать пустой PDF‑словарь** с помощью низкоуровневого API Aspose.Pdf.  
- Роль **словаря ExtGState** в управлении непрозрачностью обводки/заполнения и режимами наложения.  
- Практические советы по работе с PDF в C#, включая обработку крайних случаев, когда словарь отсутствует.  
- Полный, готовый к запуску пример кода, который можно скопировать и вставить в свой проект.

### Предварительные требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+).  
- Лицензированная копия **Aspose.Pdf for .NET** (бесплатная пробная версия подходит для тестирования).  
- Базовые знания C# и концепций PDF, таких как ресурсы и графические состояния.  

Если что‑то из этого вам незнакомо, не паникуйте — установите Aspose.Pdf через NuGet (`Install-Package Aspose.Pdf`), а остальное — обычный C#.

---

## Шаг 1 – Загрузка PDF‑документа

Первым делом нужен объект `Document`, представляющий файл, который вы хотите изменить. Оборачивание его в блок `using` гарантирует корректное освобождение ресурсов.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;   // for low‑level PDF objects
using Aspose.Pdf.Text;        // if you need to add text later

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // The rest of the workflow lives inside this block.
}
```

*Почему это важно*: Открывая файл, вы получаете доступ к внутренним объектам COS (Canonical Object Structure), где находится **CosPdfDictionary**. Без объекта документа вы не сможете достать словари ресурсов, содержащие записи **ExtGState**.

---

## Шаг 2 – Доступ к словарю ресурсов первой страницы

Страницы PDF хранят свои ресурсы (шрифты, изображения, графические состояния и т.д.) в отдельном словаре. Мы возьмём первую страницу для простоты, но тот же подход работает для любой страницы.

```csharp
// Step 2: Access the first page and its resource dictionary
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);
```

*Совет*: Если ваш PDF содержит несколько страниц с разными наборами ресурсов, повторите этот блок для каждой страницы, которую нужно изменить. Класс `DictionaryEditor` — удобный обёртка, позволяющая работать с COS‑словарем как с .NET‑словарем `Dictionary<string, object>`.

---

## Шаг 3 – Получение или инициализация словаря ExtGState

**Словарь ExtGState** хранит именованные объекты графических состояний (`GS0`, `GS1`, …). В некоторых PDF он уже присутствует, в других — нет. Мы безопасно получим его, создав новый пустой, если потребуется.

```csharp
// Step 3: Get the existing ExtGState dictionary (or create it if missing)
CosPdfDictionary extGState;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGState = resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and attach it to the resources
    extGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourceEditor.Add("ExtGState", extGState);
}
```

*Зачем это делаем*: Попытка добавить графическое состояние в несуществующий **словарь ExtGState** вызовет исключение. Эта проверка делает код надёжным для любого входного PDF.

---

## Шаг 4 – Создание нового графического состояния с CosPdfDictionary

Теперь к делу: **создание пустого PDF‑словаря**, определяющего пользовательское графическое состояние. Мы зададим непрозрачность обводки (`CA`), непрозрачность заливки (`ca`) и режим наложения (`BM`). Позже можно добавить и другие параметры — это лишь базовый набор.

```csharp
// Step 4: Create a new graphics state dictionary with desired parameters
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the parameters we want
KeyValuePair<string, ICosPdfPrimitive>[] parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),        // Fill opacity (semi‑transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))      // Blend mode
};

// Populate the dictionary
foreach (var p in parameters)
{
    newGraphicsState.Add(p);
}
```

*Пояснение*:  
- `CA` и `ca` — стандартные ключи PDF, управляющие непрозрачностью обводки и заливки соответственно.  
- `BM` выбирает режим наложения; «Normal» — значение по умолчанию, но можно использовать «Multiply», «Screen» и т.д., в зависимости от потребностей дизайна.  
- С помощью `CosPdfDictionary.CreateEmptyDictionary` мы **создаём пустой PDF‑словарь**, который затем заполняем парами ключ/значение.

---

## Шаг 5 – Вставка нового графического состояния в ExtGState

Когда графическое состояние готово, просто добавляем его в **словарь ExtGState** под уникальным именем (например, `GS0`). Если планируется добавить несколько состояний, просто увеличьте суффикс.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary
extGState.Add("GS0", newGraphicsState);
```

*Подсказка*: Перед добавлением стоит проверить, существует ли уже `GS0`, чтобы не перезаписать его. Быстрая проверка `if (!extGState.ContainsKey("GS0"))` решит задачу.

---

## Шаг 6 – Сохранение изменённого PDF

Все изменения находятся в памяти, пока вы их не сохраните. Выберите путь вывода, который подходит вашему рабочему процессу.

```csharp
// Step 6: Save the modified PDF
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Результат*: Откройте `output.pdf` в любом просмотрщике PDF и проверьте ресурсы страницы (например, с помощью инструмента‑инспектора PDF). Вы увидите новую запись в **ExtGState** под именем `GS0` с заданными параметрами.

---

## Полный рабочий пример

Объединив всё вместе, получаем полностью готовую к копированию и вставке программу:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Access first page resources
    Page firstPage = pdfDocument.Pages[1];
    DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

    // Ensure ExtGState dictionary exists
    CosPdfDictionary extGState;
    if (resourceEditor.ContainsKey("ExtGState"))
        extGState = resourceEditor["ExtGState"].ToCosPdfDictionary();
    else
    {
        extGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        resourceEditor.Add("ExtGState", extGState);
    }

    // Build new graphics state
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };
    foreach (var p in parameters) newGraphicsState.Add(p);

    // Insert into ExtGState
    if (!extGState.ContainsKey("GS0"))
        extGState.Add("GS0", newGraphicsState);

    // Save result
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**Ожидаемый результат**: `output.pdf` будет выглядеть точно так же, как оригинал, но любой контент, который позже сослётся на `GS0` (например, через оператор `gs` в потоке содержимого), получит заданные непрозрачность и режим наложения. Если такой ссылки пока нет, её можно добавить вручную или через более высокоуровневые API Aspose.

---

## Часто задаваемые вопросы и крайние случаи

| Вопрос | Ответ |
|----------|--------|
| *Что делать, если в PDF уже существует запись ExtGState с именем `GS0`?* | Проверьте `extGState.ContainsKey("GS0")` перед добавлением. Если она существует, либо намеренно перезапишите её (`extGState["GS0"] = newGraphicsState`), либо выберите новое имя, например `GS1`. |
| *Можно ли добавить больше параметров, например толщину линии (`LW`) или шаблон штриховки (`D`)?* | Конечно. Просто расширьте массив `parameters`, добавив дополнительные `KeyValuePair<string, ICosPdfPrimitive>` записи. |
| *Совместим ли этот подход с зашифрованными PDF?* | Да, при условии, что вы передадите правильный пароль при создании `Document` (`new Document(path, password)`). |
| *Нужно ли закрывать документ вручную?* | Блок `using` автоматически освобождает ресурсы, что также сбрасывает все ожидающие изменения. |
| *Чем этот метод отличается от использования высокоуровневого класса `Graphics`?* | Высокоуровневый API скрывает детали словарей, что удобно для простых задач. Однако когда требуется точный контроль над графическими состояниями — например, пользовательские режимы наложения — необходимо работать с низкоуровневым **CosPdfDictionary**, то есть напрямую **создавать пустой PDF‑словарь**. |

---

## Заключение

Мы продемонстрировали, как **создать пустой PDF‑словарь** с помощью Aspose.Pdf, внедрить пользовательское графическое состояние в **словарь ExtGState** и сохранить изменённый файл — всё это в чистом, идиоматическом C#. Этот шаблон открывает точный контроль над непрозрачностью, режимами наложения и другими параметрами графического состояния, определёнными спецификацией PDF.

Дальше вы можете:

- Применить новое графическое состояние к существующему содержимому страницы с помощью оператора `gs`.  
- Построить библиотеку переиспользуемых графических состояний для брендинга или водяных знаков.  
-  

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}