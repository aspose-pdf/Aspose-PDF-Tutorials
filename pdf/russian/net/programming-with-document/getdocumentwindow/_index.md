---
"description": "Узнайте, как использовать функцию GetDocumentWindow Aspose.PDF для .NET для получения информации о свойствах окна PDF-документа."
"linktitle": "Получить окно документа"
"second_title": "Справочник по API Aspose.PDF для .NET"
"title": "Получить окно документа"
"url": "/ru/net/programming-with-document/getdocumentwindow/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Получить окно документа

# Введение

Вы работаете с PDF-файлами и хотите больше контроля над тем, как они выглядят при открытии? Будь то скрытие строки меню или изменение размера окна для соответствия первой странице, Aspose.PDF для .NET предоставляет вам все необходимые инструменты для настройки поведения PDF-файла при открытии в средстве просмотра. В этом руководстве мы разберем, как извлекать и изменять настройки окна документа в Aspose.PDF для .NET.


# Предпосылки

Прежде чем приступить к изучению руководства, убедитесь, что у вас выполнены следующие предварительные условия:

- Aspose.PDF для .NET, установленный в вашей среде разработки.
  - [Загрузить Aspose.PDF для .NET](https://releases.aspose.com/pdf/net/)
- Действующая лицензия на Aspose.PDF, или вы можете получить [бесплатная пробная версия](https://releases.aspose.com/) или [временная лицензия](https://purchase.aspose.com/temporary-license/).
- Базовые знания .NET и C#.
- Visual Studio или другая подходящая IDE.

# Импортные пакеты

Прежде чем начать писать какой-либо код, вам нужно будет импортировать необходимые пакеты. Откройте свой проект и в верхней части файла C# добавьте следующее пространство имен:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Это предоставит вам доступ ко всем классам и методам, необходимым для работы с PDF-документами с помощью Aspose.PDF для .NET.

Теперь давайте разберем процесс получения различных настроек окна документа. Для этого примера мы будем использовать образец файла PDF с именем `GetDocumentWindow.pdf`.

## Шаг 1: Укажите путь к каталогу документов

Прежде всего, нам нужно определить путь к нашему PDF-файлу. Крайне важно указать правильный путь к файлу, чтобы избежать ошибок во время выполнения.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Здесь замените `"YOUR DOCUMENT DIRECTORY"` с фактическим каталогом, где находится ваш PDF-файл. Это ваш рабочий каталог, из которого вы загрузите PDF-документ.

## Шаг 2: Откройте PDF-документ.

Теперь, когда путь к файлу задан, следующим шагом будет открытие документа PDF с помощью Aspose.PDF. Это загрузит документ в память, что позволит вам получить его свойства.

```csharp
Document pdfDocument = new Document(dataDir + "GetDocumentWindow.pdf");
```

С помощью этой простой строки кода вы успешно загрузили свой PDF-файл в `pdfDocument` объект, который теперь позволит вам получить доступ ко всем его свойствам.

## Шаг 3: Получение статуса центрирования окна

Далее давайте проверим, должно ли окно документа быть центрировано при открытии. Значение по умолчанию для этого: `false`.

```csharp
Console.WriteLine("CenterWindow : {0}", pdfDocument.CenterWindow);
```

Если выходной сигнал равен `true`, окно документа откроется в центре экрана. В противном случае оно откроется в своей позиции по умолчанию.

## Шаг 4: Проверьте направление текста

Другим важным аспектом внешнего вида PDF является направление текста, которое определяет, читается ли текст слева направо (L2R) или справа налево (R2L). Вы можете получить эту информацию, используя следующий код:

```csharp
Console.WriteLine("Direction : {0}", pdfDocument.Direction);
```

Выход будет `L2R` для текста слева направо и `R2L` для текста справа налево. Эта настройка особенно полезна для документов на таких языках, как арабский или иврит.

## Шаг 5: Отображение заголовка документа в окне

Следующее свойство позволяет вам контролировать, будет ли отображаться заголовок документа или имя файла в строке заголовка окна. По умолчанию это установлено в `false`, то есть будет показано имя файла.

```csharp
Console.WriteLine("DisplayDocTitle : {0}", pdfDocument.DisplayDocTitle);
```

Если вы хотите, чтобы вместо имени файла отображалось название документа, этот параметр необходимо включить.

## Шаг 6: Измените размер окна, чтобы оно вписывалось в первую страницу

Иногда вам может понадобиться, чтобы окно документа автоматически меняло свой размер, чтобы соответствовать первой странице PDF-файла при его открытии. Вот как проверить, включена ли эта функция:

```csharp
Console.WriteLine("FitWindow : {0}", pdfDocument.FitWindow);
```

По умолчанию установлено значение `false`, то есть размер окна останется прежним независимо от размера первой страницы.

## Шаг 7: Скройте строку меню

Для более целенаправленного чтения вы можете скрыть панель меню приложения-просмотрщика. Вы можете получить эту настройку с помощью следующей строки:

```csharp
Console.WriteLine("HideMenuBar : {0}", pdfDocument.HideMenubar);
```

Это вернётся `true` если строка меню скрыта, и `false` в противном случае.

## Шаг 8: Скройте панель инструментов

Аналогично, вы также можете захотеть скрыть панель инструментов в просмотрщике PDF для более чистого пользовательского интерфейса. Эту настройку можно получить следующим образом:

```csharp
Console.WriteLine("HideToolBar : {0}", pdfDocument.HideToolBar);
```

Если этот параметр включен, панель инструментов будет скрыта при открытии PDF-файла.

## Шаг 9: Скройте полосы прокрутки и элементы пользовательского интерфейса.

Если вы хотите отобразить только содержимое страницы без дополнительных элементов пользовательского интерфейса, таких как полосы прокрутки, этот параметр управляет таким поведением:

```csharp
Console.WriteLine("HideWindowUI : {0}", pdfDocument.HideWindowUI);
```

При установке на `true`, средство просмотра PDF-файлов скроет полосы прокрутки и другие элементы пользовательского интерфейса, оставив только содержимое документа.

## Шаг 10: Установите режим неполноэкранной страницы

Вы можете управлять тем, как будет выглядеть документ при выходе из полноэкранного режима, используя `NonFullScreenPageMode` свойство. Этот параметр полезен для определения того, как пользователь должен взаимодействовать с документом в неполноэкранном режиме.

```csharp
Console.WriteLine("NonFullScreenPageMode : {0}", pdfDocument.NonFullScreenPageMode);
```

Вывод можно настроить на различные режимы, такие как миниатюры, контуры или панель вложений.

## Шаг 11: Определите макет страницы

Эта настройка позволяет вам контролировать, как будут расположены страницы документа. Например, вы можете выбрать вид одной страницы или вид непрерывной колонки:

```csharp
Console.WriteLine("PageLayout : {0}", pdfDocument.PageLayout);
```

Это дает пользователям гибкость в том, как они читают или просматривают содержимое документа.

## Шаг 12: Укажите режим страницы

Наконец, `PageMode` свойство определяет, как документ должен отображаться при открытии. Варианты включают отображение миниатюр, переход в полноэкранный режим или отображение панели вложений.

```csharp
Console.WriteLine("PageMode : {0}", pdfDocument.PageMode);
```

В зависимости от ваших потребностей вы можете установить любой режим, соответствующий назначению вашего PDF-файла.

## Заключение

Как вы видите, Aspose.PDF для .NET предоставляет комплексные инструменты для управления тем, как ваши PDF-документы отображаются в различных средствах просмотра PDF. Хотите ли вы скрыть панель инструментов, центрировать окно или управлять направлением текста, Aspose.PDF предлагает гибкость для улучшения пользовательского опыта просмотра.

# Часто задаваемые вопросы

### Могу ли я настроить начальный уровень масштабирования PDF-файла?
Да, Aspose.PDF позволяет устанавливать уровень масштабирования при открытии документа.

### Как заблокировать размер окна PDF-файла?
Вы можете установить `FitWindow` свойство, предотвращающее изменение размера окна.

### Поддерживает ли Aspose.PDF различные режимы чтения?
Да, он поддерживает различные режимы, такие как полноэкранный режим, миниатюры и вложения.

### Можно ли скрыть полосы прокрутки в средстве просмотра PDF-файлов?
Конечно, вы можете скрыть полосы прокрутки, установив `HideWindowUI` собственность `true`.

### Можно ли расположить окно документа по центру при его открытии?
Да, вы можете контролировать это, установив `CenterWindow` свойство.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}