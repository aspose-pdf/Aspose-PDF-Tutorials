---
"description": "Узнайте, как создавать элементы структуры ссылок в PDF с помощью Aspose.PDF для .NET. Пошаговое руководство по добавлению доступных ссылок, изображений и проверке соответствия."
"linktitle": "Элементы структуры ссылок"
"second_title": "Справочник по API Aspose.PDF для .NET"
"title": "Элементы структуры ссылок"
"url": "/ru/net/programming-with-tagged-pdf/link-structure-elements/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Элементы структуры ссылок

## Введение

Создание и управление элементами структуры ссылок в PDF может иметь решающее значение для документов, требующих доступности и плавной навигации. В этом руководстве мы расскажем вам, как это сделать с помощью Aspose.PDF для .NET. Если вы новичок в Aspose.PDF или манипуляциях с PDF в целом, не волнуйтесь. Я подробно объясню каждый шаг, чтобы вы могли легко следовать!

## Предпосылки  

Прежде чем погрузиться в кодирование, давайте сначала разберемся с несколькими вещами. Это основные требования, которые обеспечат плавный процесс разработки.

1. Aspose.PDF для .NET: Вы можете загрузить последнюю версию [здесь](https://releases.aspose.com/pdf/net/).
2. Среда разработки .NET: будь то Visual Studio или любая совместимая с .NET среда IDE, установите ее и подготовьте к работе.
3. Лицензия Aspose: Вы можете использовать бесплатную пробную версию Aspose.PDF [здесь](https://releases.aspose.com/) или приобретите [временная лицензия](https://purchase.aspose.com/temporary-license/).
4. Базовые знания C#: мы будем работать с кодом C#, поэтому понимание основ значительно упростит задачу.

## Импортные пакеты

Вам нужно будет импортировать несколько пакетов, прежде чем писать код для элементов структуры ссылок. Начните со ссылки на необходимые библиотеки Aspose.PDF в вашем проекте:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Этот импорт позволяет нам работать с PDF-документами, добавлять теги и управлять элементами структуры.

Сейчас мы создадим PDF-документ с различными типами структур ссылок, и каждый шаг будет разбит на этапы, чтобы помочь вам полностью понять процесс.

## Шаг 1: Инициализация документа  

Начнем с создания нового PDF-документа и настройки тегированного контента для обеспечения доступности.

```csharp
// Путь к каталогу документов.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "LinkStructureElements_Output.pdf";
string logFile = dataDir + "46035_log.xml";
string imgFile = dataDir + "google-icon-512.png";

// Создать новый PDF-документ
Document document = new Document(); 

// Получить интерфейс TaggedContent
ITaggedContent taggedContent = document.TaggedContent;
```
  
Здесь мы инициализируем `Document` объект, который представляет наш PDF-файл. Мы также извлекаем `TaggedContent` интерфейс, позволяющий добавлять элементы структуры, такие как абзацы, ссылки и изображения.

## Шаг 2: Укажите название и язык  

Каждый PDF-файл должен иметь заголовок и настройки языка, особенно если вы стремитесь к соблюдению стандартов PDF/UA.

```csharp
// Установите название документа и язык
taggedContent.SetTitle("Link Elements Example");
taggedContent.SetLanguage("en-US");
```
  
Этот шаг гарантирует, что ваш PDF-файл будет иметь осмысленное название и установит язык на английский (`en-US`). Это имеет решающее значение для доступности и гарантирует, что программы чтения с экрана или другие вспомогательные технологии смогут правильно интерпретировать ваш документ.

## Шаг 3: Создание и добавление абзацев  

На этом этапе мы добавим абзацы для размещения элементов ссылок.

```csharp
// Создать корневой элемент
StructureElement rootElement = taggedContent.RootElement;

// Создайте абзац и добавьте его в корневой элемент.
ParagraphElement p1 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p1);
```
  
Мы создаем корневой элемент структуры, который по сути является контейнером верхнего уровня для всех остальных элементов. Затем мы создаем абзац (`p1`) и добавить его к корневому элементу.

## Шаг 4: Добавьте простую ссылку  

Теперь давайте добавим простую гиперссылку, указывающую на Google.

```csharp
// Создайте элемент ссылки и добавьте его в абзац.
LinkElement link1 = taggedContent.CreateLinkElement();
p1.AppendChild(link1);

// Установить гиперссылку и текст для ссылки
link1.Hyperlink = new WebHyperlink("http://google.com");
link1.SetText("Google");
link1.AlternateDescriptions = "Link to Google";
```
  
На этом этапе мы создали элемент ссылки, установили его гиперссылку на "http://google.com" и предоставили текст ("Google") для ссылки. Мы также добавили альтернативное описание для обеспечения доступности.

## Шаг 5: Добавление ссылки с помощью Span  

Мы также можем создавать ссылки с различным объемом текста.

```csharp
// Создать еще один абзац
ParagraphElement p2 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p2);

// Создать ссылку с элементом span
LinkElement link2 = taggedContent.CreateLinkElement();
p2.AppendChild(link2);
link2.Hyperlink = new WebHyperlink("http://google.com");

SpanElement span2 = taggedContent.CreateSpanElement();
span2.SetText("Google");
link2.AppendChild(span2);

link2.AlternateDescriptions = "Link to Google";
```
  
Здесь мы использовали элемент span, чтобы заключить часть текста в ссылку, что позволяет нам настраивать внешний вид определенных частей ссылки.

## Шаг 6: Многострочная ссылка  

Что делать, если текст ссылки слишком длинный? Не беспокойтесь, вы можете разбить его на несколько строк.

```csharp
ParagraphElement p4 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p4);

LinkElement link4 = taggedContent.CreateLinkElement();
p4.AppendChild(link4);
link4.Hyperlink = new WebHyperlink("http://google.com");
link4.SetText("The multiline link: Google Google Google Google Google...");
link4.AlternateDescriptions = "Link to Google (multiline)";
```
  
В этом случае мы создали многострочную ссылку, просто задав длинное текстовое значение, и текст будет автоматически переноситься на несколько строк.

## Шаг 7: Добавьте изображение к ссылке  

Наконец, вы также можете добавлять изображения внутри ссылки.

```csharp
// Создайте новый абзац и элемент ссылки
ParagraphElement p5 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p5);

LinkElement link5 = taggedContent.CreateLinkElement();
p5.AppendChild(link5);
link5.Hyperlink = new WebHyperlink("http://google.com");

// Добавить изображение к ссылке
FigureElement figure5 = taggedContent.CreateFigureElement();
figure5.SetImage(imgFile, 1200);
figure5.AlternativeText = "Google icon";
link5.AppendChild(figure5);

link5.AlternateDescriptions = "Link to Google";
```
  
Этот шаг демонстрирует, как можно улучшить ссылки с помощью изображения. В этом случае мы добавили значок Google внутри ссылки. Мы также обеспечили доступность, установив альтернативный текст для изображения.

## Шаг 8: Проверка PDF на соответствие требованиям  

Если вы стремитесь к соответствию PDF/UA (стандарт доступности), хорошей практикой будет проверка вашего документа.

```csharp
// Сохраните PDF-документ
document.Save(outFile);

// Проверить документ на соответствие PDF/UA
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```
  
Мы сохранили документ и проверили его на соответствие стандарту PDF/UA, что гарантирует соответствие PDF-файла требованиям доступности.

## Заключение  

В этом руководстве мы рассмотрели, как создавать структурированные PDF-документы с помощью Aspose.PDF для .NET. От добавления базовых гиперссылок до более сложных структур, таких как интервалы, многострочные ссылки и даже изображения, это руководство обеспечивает прочную основу для управления элементами ссылок в ваших PDF-файлах. Благодаря дополнительному преимуществу соответствия PDF/UA вы теперь готовы создавать доступные и навигируемые PDF-файлы.

## Часто задаваемые вопросы

### Могу ли я добавлять более сложные структуры, например таблицы, внутри ссылок?  
Нет, ссылки предназначены в первую очередь для текста и изображений, но вы можете встраивать сложные элементы рядом.

### Является ли проверка PDF/UA обязательной?  
Не всегда, но это настоятельно рекомендуется, если вас беспокоит доступность.

### Что произойдет, если путь к файлу изображения неверен?  
Документ не будет отображать изображение, и может возникнуть ошибка во время рендеринга.

### Могу ли я изменить стиль текста в ссылке?  
Да, вы можете применять стили текста с помощью элементов span.

### Можно ли создавать внутренние ссылки на документы?  
Конечно! Вы можете ссылаться на определенные разделы в одном документе.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}