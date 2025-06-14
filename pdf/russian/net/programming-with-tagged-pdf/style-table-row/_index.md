---
"description": "Узнайте, как стилизовать строки таблицы в PDF-файле с помощью Aspose.PDF для .NET, с помощью пошагового руководства, которое поможет вам с легкостью улучшить форматирование документа."
"linktitle": "Стиль строки таблицы"
"second_title": "Справочник по API Aspose.PDF для .NET"
"title": "Стиль строки таблицы"
"url": "/ru/net/programming-with-tagged-pdf/style-table-row/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Стиль строки таблицы

## Введение

Когда дело доходит до создания хорошо структурированных и красиво отформатированных PDF-документов, Aspose.PDF для .NET — это решение, к которому стоит прибегнуть. Независимо от того, автоматизируете ли вы отчеты, счета-фактуры или создаете динамические таблицы, форматирование таблиц с различными стилями является ключом к безупречному документу. В этом уроке мы подробно рассмотрим стилизацию строки таблицы с помощью Aspose.PDF для .NET. И не волнуйтесь, я проведу вас шаг за шагом, как в хорошей беседе за чашкой кофе!

## Предпосылки

Прежде чем мы перейдем к сути, давайте убедимся, что у вас все в порядке. Вам понадобится:

1. Библиотека Aspose.PDF для .NET  
   Если у вас его еще нет, вы можете получить его здесь [здесь](https://releases.aspose.com/pdf/net/). Вы также можете получить [бесплатная пробная версия](https://releases.aspose.com/) для начала.
2. Среда разработки  
   Установите Visual Studio или любую C# IDE по вашему выбору. Вам также понадобится установленный .NET, но я предполагаю, что вы уже с ним знакомы.
3. Базовые знания C# и .NET  
   Хорошее понимание C# сделает этот урок легким. Но не волнуйтесь, я объясню каждый шаг подробно!

## Импортные пакеты

Прежде чем мы начнем работать с Aspose.PDF, нам нужно импортировать необходимые пространства имен. В вашем проекте C# убедитесь, что вы включили следующее:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Они необходимы для создания и оформления таблицы и, конечно же, для работы с тегированным контентом на предмет соответствия требованиям.

Теперь давайте разберем задачу шаг за шагом, чтобы вы могли оформить строки таблицы как профессионал!

## Шаг 1: Создайте новый PDF-документ

Сначала самое главное: давайте создадим совершенно новый PDF-документ. Этот документ будет содержать все стилизованные строки таблицы.

```csharp
// Путь к каталогу документов.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Создать документ
Document document = new Document();
```

Здесь мы просто инициализируем новый `Document` объект, который будет представлять наш PDF-файл. Обязательно укажите путь к каталогу, в котором вы будете сохранять выходные файлы.

## Шаг 2: Работа с тегированным контентом

Чтобы структурировать ваш PDF для доступности, мы будем работать с тегированным контентом. Это помогает в создании структурированных элементов, таких как таблицы, гарантируя их соответствие стандартам доступности, таким как PDF/UA.

```csharp
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table row style");
taggedContent.SetLanguage("en-US");
```

Здесь мы задаем заголовок и язык для помеченного содержимого PDF. Это как дать вашему PDF имя и указать ему, на каком языке он должен говорить!

## Шаг 3: Определите структуру таблицы

Далее, давайте определим структуру таблицы, которую мы собираемся создать. Каждая таблица нуждается в заголовке, теле и нижнем колонтитуле — как хорошо организованная запись в блоге!

```csharp
// Получить корневой элемент структуры
StructureElement rootElement = taggedContent.RootElement;

// Создать элемент структуры таблицы
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

Здесь мы создаем таблицу с заголовком (`THead`), тело (`TBody`) и нижний колонтитул (`TFoot`). Эти элементы будут удерживать наши ряды.

## Шаг 4: Добавьте строку заголовка таблицы

Таблицы без заголовков — как книги без названий. Давайте сначала создадим строку заголовка, чтобы обеспечить контекст для данных.

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText(String.Format("Head {0}", colIndex));
}
```

Здесь мы проходим цикл и добавляем три ячейки заголовка (`TableTHElement`), давая каждому из них описательный текст. Просто, не правда ли?

## Шаг 5: Добавьте стилизованные строки тела

Теперь самое интересное — стилизуем строки! Давайте создадим семь строк с пользовательскими стилями. Мы зададим цвета фона, границы, отступы и выравнивание текста.

```csharp
for (int rowIndex = 0; rowIndex < 7; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = String.Format("Row {0}", rowIndex);
    trElement.BackgroundColor = Color.LightGoldenrodYellow;
    trElement.Border = new BorderInfo(BorderSide.All, 0.75F, Color.DarkGray);
    trElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.Blue);
    trElement.MinRowHeight = 100.0;
    trElement.FixedRowHeight = 120.0;
    trElement.IsInNewPage = (rowIndex % 3 == 1);
    trElement.IsRowBroken = true;

    for (int colIndex = 0; colIndex < 3; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText(String.Format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}
```

- Цвет фона: мы использовали светло-золотистый оттенок для создания профессионального, но теплого оттенка.
- Границы: каждая строка имеет темно-серую внешнюю границу и синие границы ячеек для четкого вида.
- Высота и отступы: задается высота строк, а также добавляются отступы для придания четкого вида.
- Разрывы страниц: Чтобы сделать таблицу более удобной для чтения, каждая вторая строка начинается с новой страницы.

## Шаг 6: Добавьте строку нижнего колонтитула

Подобно заголовку, нижний колонтитул закрепляет таблицу. Давайте создадим его.

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText(String.Format("Foot {0}", colIndex));
}
```

Мы просто проходим по трем ячейкам нижнего колонтитула и добавляем немного текста. Альтернативный текст для нижнего колонтитула — «Foot Row», чтобы сделать его доступным.

## Шаг 7: Сохраните PDF-документ.

Теперь, когда стол накрыт, пришло время сохранить ваш шедевр!

```csharp
document.Save(dataDir + "StyleTableRow.pdf");
```

Вот так ваш PDF-файл сохраняется со всеми прекрасными строками таблицы, которые мы только что оформили.

## Шаг 8: Проверка соответствия PDF/UA

Чтобы гарантировать, что наш PDF-файл соответствует стандартам доступности, мы проверим его на соответствие PDF/UA.

```csharp
document = new Document(dataDir + "StyleTableRow.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableRow.xml", PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

Это гарантирует, что ваш PDF соответствует стандарту PDF/UA, делая его доступным для всех. Доступность — это название игры!

## Заключение

И вот оно! Всего несколько строк кода — и вы создали полностью оформленную таблицу в PDF-файле с помощью Aspose.PDF для .NET. От заголовков до нижних колонтитулов мы оформили каждую строку, добавили элементы доступности и даже проверили документ на соответствие. Работаете ли вы над корпоративными отчетами, презентациями или просто развлекаетесь с PDF-файлами, это руководство вам поможет. Теперь приступайте к оформлению таблиц как профессионал!

## Часто задаваемые вопросы

### Могу ли я изменить стиль шрифта таблицы?  
Да! Вы можете изменить стиль шрифта с помощью `TextState` объект для каждой ячейки, что обеспечивает полную настройку.

### Как добавить больше столбцов в таблицу?  
Просто отрегулируйте `colCount` переменную и добавьте больше ячеек в циклы для заголовков, основного текста и нижних колонтитулов.

### Что произойдет, если я не установлю высоту строки?  
Если вы не зададите высоту строки, таблица будет автоматически подстраиваться под содержимое.

### Могу ли я использовать это для динамического количества строк?  
Конечно! Вы можете извлекать данные из базы данных или любого другого источника и динамически корректировать количество строк и столбцов.

### Можно ли использовать Aspose.PDF для .NET бесплатно?  
Aspose.PDF для .NET — это лицензионный продукт, но вы можете попробовать его с помощью [бесплатная пробная версия](https://releases.aspose.com/) или получить [временная лицензия](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}