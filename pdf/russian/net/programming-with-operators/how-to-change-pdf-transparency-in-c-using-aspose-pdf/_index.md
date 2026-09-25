---
category: general
date: 2026-09-24
description: Узнайте, как изменить прозрачность PDF в C# с помощью Aspose.Pdf. Это
  пошаговое руководство охватывает непрозрачность PDF, режим наложения и редактирование
  графического состояния.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: ru
lastmod: 2026-09-24
og_description: Измените прозрачность PDF в C# с помощью Aspose.Pdf. Следуйте этому
  руководству, чтобы редактировать непрозрачность PDF, режим наложения и графическое
  состояние для профессионального вывода документов.
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: Изменение прозрачности PDF в C# – полное руководство по Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Как изменить прозрачность PDF в C# с помощью Aspose.Pdf
url: /ru/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как изменить прозрачность PDF в C# с помощью Aspose.Pdf

Если вам нужно **изменить прозрачность PDF** в проекте .NET, это руководство покажет, как сделать это с помощью Aspose.Pdf. Вы увидите полностью готовый, исполняемый пример, который изменяет непрозрачность PDF, задаёт режим наложения и обновляет словарь графического состояния страницы.

Изменение прозрачности PDF — распространённая задача, когда нужны водяные знаки, наложенные графические элементы или пользовательские визуальные эффекты. В этом уроке вы научитесь редактировать **графическое состояние Aspose.Pdf**, регулировать **непрозрачность PDF** и работать с настройками **blend mode PDF** — всё с помощью чистого кода C#.

## Prerequisites

Перед началом убедитесь, что у вас есть:

* .NET 6.0 или более поздняя версия  
* Лицензия Aspose.Pdf for .NET (или временный оценочный ключ)  
* PDF‑файл с именем `input.pdf` в папке, которую вы можете указать как `YOUR_DIRECTORY`  
* Базовые знания C# и Visual Studio (подойдёт любой IDE)

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Pdf`. Код работает на Windows, Linux и macOS, так как Aspose.Pdf кроссплатформенный.

## Изменение прозрачности PDF – шаг 1: открыть PDF‑документ

Первая операция — загрузить исходный PDF. Использование блока `using` гарантирует автоматическое освобождение дескриптора файла.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

Открытие документа — фундамент для любой задачи **манипуляции PDF на C#**. Если файл не найден, Aspose.Pdf бросит `FileNotFoundException`, поэтому дважды проверьте путь перед запуском кода.

## Доступ к ресурсам страницы с помощью графического состояния Aspose.Pdf

Далее получаем первую страницу и её словарь ресурсов. Словарь ресурсов содержит такие объекты, как шрифты, изображения и записи **ExtGState**, управляющие графическими параметрами.

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Класс `DictionaryEditor` предоставляет удобный обёртку для чтения и записи словарей PDF. Здесь мы сосредотачиваемся на словаре **ExtGState**, поскольку он хранит настройки прозрачности.

## Создание и настройка нового графического состояния для непрозрачности PDF

Теперь мы создаём новый словарь графического состояния. Этот словарь будет хранить параметры, определяющие непрозрачность обводки (`CA`), заполнения (`ca`) и режим наложения (`BM`).

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** управляет непрозрачностью операций обводки (линии, границы).  
* **`ca`** управляет непрозрачностью операций заполнения (закрашенные фигуры, текст).  
* **`BM`** выбирает режим наложения; `"Normal"` — значение по умолчанию, но можно использовать `"Multiply"` или `"Screen"` для художественных эффектов.

Эти настройки являются ядром манипуляций **непрозрачностью PDF**. Регулируйте числовые значения в соответствии с вашим визуальным дизайном — `0` означает полностью прозрачный, `1` — полностью непрозрачный.

## Вставка графического состояния и сохранение документа

После построения нового состояния мы добавляем его в существующий словарь **ExtGState** под уникальным именем (`GS0`). Затем сохраняем изменённый PDF.

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

Когда PDF откроется в просмотрщике, любой контент, ссылающийся на `GS0`, будет отрисован с заданной прозрачностью. Позже вы можете применить это графическое состояние к конкретным объектам, используя свойство `GraphicsState` у команд рисования (например, `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`).

## Проверка результата

Откройте `output.pdf` в Adobe Acrobat Reader, Foxit или любом PDF‑просмотрщике, поддерживающем прозрачность. Вы должны увидеть элементы заполнения первой страницы с непрозрачностью 50 %, тогда как обводка останется полностью непрозрачной. Если изменения не заметны, убедитесь, что страница действительно использует новое графическое состояние — иначе можно явно назначить `GS0` нужным объектам.

![Change PDF transparency in C# code example](path/to/image.png){: .img-responsive alt="Изменение прозрачности PDF в примере кода C#"}

*Изображение выше показывает полный исходный код C#, который изменяет прозрачность PDF.*

## Распространённые варианты и особые случаи

| Ситуация | Как адаптировать код |
|-----------|-----------------------|
| **Несколько страниц** | Пройдитесь в цикле по `document.Pages` и повторите шаги 2‑8 для каждой страницы. |
| **Другой режим наложения** | Замените `"Normal"` на `"Multiply"`, `"Screen"` или любое другое стандартное имя режима наложения PDF. |
| **Более высокая непрозрачность заполнения** | Измените `new CosPdfNumber(0.5)` на значение от `0` до `1`. |
| **Отсутствует ExtGState** | Если `resourcesEditor["ExtGState"]` возвращает `null`, создайте новый словарь: `var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

Эти варианты демонстрируют гибкость **модификации ресурсов PDF** с помощью Aspose.Pdf. Регулируя параметры, вы можете создавать водяные знаки, полупрозрачные наложения или пользовательские UI‑элементы внутри PDF.

## Полный, исполняемый пример

Ниже представлен полный код программы, который можно скопировать и вставить в новый проект консольного приложения. В нём присутствуют все необходимые директивы `using`, обработка ошибок и комментарии.



## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change PDF Opacity in C# – Complete Aspose Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}