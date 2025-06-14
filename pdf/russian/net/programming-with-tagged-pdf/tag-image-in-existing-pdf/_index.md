---
"description": "Узнайте, как помечать изображения в существующих PDF-файлах с помощью Aspose.PDF для .NET. Пошаговое руководство по улучшению доступности с соответствием PDF/UA."
"linktitle": "Тег изображения в существующем PDF-файле"
"second_title": "Справочник по API Aspose.PDF для .NET"
"title": "Тег изображения в существующем PDF-файле"
"url": "/ru/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Тег изображения в существующем PDF-файле

## Введение

В этом руководстве мы покажем вам, как пометить изображение в существующем PDF-файле с помощью Aspose.PDF для .NET. К концу этого руководства вы сможете задать альтернативный текст для изображений, настроить атрибуты макета и убедиться, что ваш PDF-файл соответствует стандартам доступности.

## Предпосылки

Прежде чем мы начнем, давайте рассмотрим, что вам понадобится для начала работы:

- Aspose.PDF для .NET: убедитесь, что вы загрузили и установили последнюю версию Aspose.PDF для .NET. [Скачать здесь](https://releases.aspose.com/pdf/net/).
- .NET Framework: убедитесь, что у вас настроена среда разработки .NET, например Visual Studio.
- Базовое понимание структуры PDF-файла: знакомство с элементами структуры PDF-файла, такими как абзацы, интервалы, таблицы и изображения.
- Действующая лицензия: вы можете купить лицензию [здесь](https://purchase.aspose.com/buy) или используйте временный [здесь](https://purchase.aspose.com/temporary-license/).

## Импортные пакеты

Чтобы начать кодирование, вам нужно импортировать необходимые пространства имен из Aspose.PDF для .NET. Это даст вам доступ к необходимым классам и методам для управления документом PDF.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Теперь, когда мы подготовили почву, давайте разобьем процесс маркировки изображения на несколько этапов.

## Шаг 1: Загрузите существующий PDF-документ

Первый шаг — загрузить PDF-файл, с которым вы хотите работать. Это может быть любой PDF-файл с изображением, которое вы хотите пометить.

```csharp
// Путь к каталогу документов.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// Открыть документ
Document document = new Document(inFile);
```

- Заменять `"YOUR DOCUMENT DIRECTORY"` с фактическим путем к вашему файлу.
- The `Document` класс позволяет вам загрузить существующий PDF. Вы будете изменять этот PDF, чтобы пометить изображение.

## Шаг 2: Доступ к тегированному контенту и корневому элементу структуры

После открытия PDF-файла следующим шагом будет доступ к тегированному контенту и определение корневого элемента структуры. Это важно, поскольку позволяет перемещаться по элементам PDF-файла и вносить изменения.

```csharp
// Получить помеченный контент и корневой элемент структуры
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` обеспечивает доступ к структурированным элементам в PDF-файле.
- The `RootElement` — это самый верхний элемент структуры, от которого можно перейти к другим элементам, таким как абзацы, таблицы и изображения.

## Шаг 3: Задайте заголовок для помеченного PDF-документа

Добавление заголовка к помеченному PDF-документу гарантирует, что ваш документ будет правильно помечен, что полезно для обеспечения доступности и соответствия PDF/UA.

```csharp
// Установить заголовок для помеченного PDF-документа
taggedContent.SetTitle("Document with images");
```

- Установка заголовка для вашего PDF-файла с тегами улучшает доступность и повышает ясность документа для программ чтения с экрана и вспомогательных технологий.

## Шаг 4: Найдите и отметьте изображение

Теперь давайте найдем элемент изображения (называемый `FigureElement` в Aspose.PDF), задайте для него альтернативный текст и настройте атрибуты его макета.

```csharp
// Пройтись по всем элементам Figure (изображениям) и задать альтернативный текст и атрибуты макета
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // Установить альтернативный текст для рисунка
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // Создать и задать атрибут BBox (ограничительный прямоугольник)
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // Установить атрибуты макета для рисунка
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- Этот код проходит по всем `FigureElement` объекты в корневой структуре, представляющие собой изображения.
- Он задает альтернативный текст для обеспечения доступности (программы чтения с экрана будут использовать его для описания изображения).
- Ограничивающая рамка (`BBox`) задает координаты макета изображения, обеспечивая его правильное отображение в документе.

## Шаг 5: Измените элементы Span в таблице

В некоторых случаях вам может потребоваться изменить элементы span в таблице. Здесь мы покажем, как найти `SpanElement` и перенесите его в абзац.

```csharp
// Найдите элементы table, span и paragraph.
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// Переместить элемент span в абзац
spanElement.ChangeParentElement(paragraph);
```

- Здесь мы находим `TableElement`, `SpanElement`, и `ParagraphElement` в PDF-файле.
- Используя `ChangeParentElement` Метод заключается в том, что мы перемещаем span в абзац, чтобы обеспечить правильную разметку и структуру.

## Шаг 6: Сохраните документ и проверьте его соответствие PDF/UA

После внесения всех изменений последним шагом будет сохранение обновленного PDF-файла и проверка его соответствия стандартам PDF/UA.

```csharp
// Сохраните обновленный PDF-документ.
document.Save(outFile);

// Проверить соответствие PDF/UA
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- The `Validate` Метод проверяет PDF-документ на соответствие стандартам PDF/UA и регистрирует результаты.
- Обеспечение соответствия помогает улучшить доступность и выполнить нормативные требования к публикации документов.

## Заключение

В этом уроке мы показали вам, как помечать изображения в существующем PDF-файле с помощью Aspose.PDF для .NET. Задавая альтернативный текст, настраивая атрибуты макета и проверяя документ на соответствие PDF/UA, вы можете гарантировать, что ваши PDF-файлы доступны и соответствуют современным стандартам. Aspose.PDF упрощает работу со структурированными элементами, предоставляя вам контроль над макетом и доступностью вашего документа.

## Часто задаваемые вопросы

### Для чего используется Aspose.PDF для .NET?
Aspose.PDF для .NET — мощная библиотека, используемая для программного создания, редактирования и обработки PDF-документов в среде .NET.

### Как обеспечить соответствие требованиям PDF/UA?
Вы можете использовать Aspose.PDF `Validate` метод проверки соответствия PDF/UA после внесения изменений в документ.

### Что такое альтернативный текст в PDF-файлах?
Альтернативный текст — это описание, добавляемое к изображениям в PDF-файлах для улучшения доступности, особенно для пользователей, использующих программы чтения с экрана.

### Могу ли я манипулировать таблицами и диапазонами в PDF-файле с помощью Aspose.PDF?
Да, Aspose.PDF позволяет вам манипулировать таблицами, диапазонами и другими структурированными элементами в документе PDF.

### Где можно скачать Aspose.PDF для .NET?
Вы можете загрузить последнюю версию Aspose.PDF для .NET [здесь](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}