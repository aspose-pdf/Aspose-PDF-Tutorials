---
"description": "Узнайте, как искать и извлекать текст со всех страниц PDF-документа с помощью Aspose.PDF для .NET."
"linktitle": "Поиск и получение текста"
"second_title": "Справочник по API Aspose.PDF для .NET"
"title": "Поиск и получение текста"
"url": "/ru/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Поиск и получение текста

## Введение

Вам когда-нибудь требовалось извлечь определенный текст из PDF-файла, но вы находили это сложным? PDF-файлы иногда могут казаться заблокированными контейнерами, что затрудняет получение нужной вам информации. Но вот и хорошие новости: с Aspose.PDF для .NET вы можете легко искать и извлекать текст из любого PDF-файла. Эта мощная библиотека предоставляет все необходимое для работы с PDF-файлами в ваших приложениях .NET, что упрощает извлечение текста. В этом руководстве мы проведем вас через процесс поиска и извлечения текста из PDF-файла с помощью Aspose.PDF для .NET. Независимо от того, создаете ли вы инструмент для анализа текста или просто хотите автоматизировать извлечение данных из отчетов PDF, вы находитесь в правильном месте!

## Предпосылки

Прежде чем перейти к коду, давайте убедимся, что у вас все настроено:

1. Aspose.PDF для .NET: Вам нужно будет скачать и установить Aspose.PDF для .NET. Вы можете получить его на странице загрузки [здесь](https://releases.aspose.com/pdf/net/).
2. Среда .NET: Убедитесь, что на вашем компьютере для разработки установлены .NET Framework или .NET Core.
3. Базовые знания C##: рекомендуется некоторое знакомство с C# и работа с проектами .NET.
4. PDF Document: Образец PDF-файла, из которого мы будем извлекать текст. В этом примере мы будем использовать `SearchAndGetTextFromAll.pdf`.

## Импортные пакеты

Перед написанием кода вам необходимо импортировать необходимые пространства имен в свой проект для работы с Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Эти пространства имен обеспечивают доступ к объектной модели документа PDF и позволяют нам манипулировать текстом в файле.

Давайте разобьем процесс на простые шаги, чтобы вам было легче его выполнять.

## Шаг 1: Укажите каталог документов

Прежде всего, вам нужно указать путь к каталогу, где находится ваш PDF. Это поможет приложению найти файл, из которого вы будете извлекать текст.

```csharp
// Путь к каталогу документов.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- The `dataDir` переменная должна указывать на каталог, где находится ваш `SearchAndGetTextFromAll.pdf` файл сохранен.
- Заменять `"YOUR DOCUMENT DIRECTORY"` с реальным путем на вашем компьютере.

## Шаг 2: Откройте PDF-документ.

Далее мы откроем PDF-документ с помощью Aspose.PDF `Document` объект.

```csharp
// Открыть документ
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- Мы создаем новый экземпляр `Document` класс, передавая полный путь к файлу PDF.
- Это загрузит PDF-файл в память и подготовит его к обработке.

## Шаг 3: Создайте поглотитель текста

The `TextFragmentAbsorber` объект используется для поиска определенного текста в PDF. В этом случае мы будем искать слово «текст».

```csharp
// Создайте объект TextAbsorber для поиска всех вхождений введенной поисковой фразы.
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- The `TextFragmentAbsorber` инициализируется строкой `"text"`. Это означает, что он будет искать любые вхождения слова «текст» в документе PDF.

## Шаг 4: Примите Поглотитель для всех страниц

Теперь мы дадим команду PDF-документу принять поглотитель и выполнить поиск текста на всех его страницах.

```csharp
// Принять поглотитель для всех страниц
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- The `Accept` Метод применяется к страницам документа. Это позволит выполнить поиск указанного текста на всех страницах.

## Шаг 5: Извлечение фрагментов текста

После того как поглотитель отсканирует документ, мы можем извлечь извлеченные фрагменты текста.

```csharp
// Получить извлеченные фрагменты текста
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- The `TextFragments` собственность `TextFragmentAbsorber` возвращает коллекцию всех текстовых фрагментов, соответствующих поисковому запросу.

## Шаг 6: Просмотрите фрагменты текста

Теперь, когда у нас есть коллекция текстовых фрагментов, мы пройдемся по ним и извлечем детали.

```csharp
// Просмотрите фрагменты
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- The `foreach` цикл проходит через каждый `TextFragment` в коллекции.
- Мы печатаем различные свойства каждого фрагмента, такие как сам текст, его положение на странице, сведения о шрифте и его размер.
- The `XIndent` и `YIndent` Свойства задают точные координаты фрагмента текста в PDF-файле.

## Заключение

И вот оно! Всего несколькими строками кода мы успешно выполнили поиск и извлекли текст из PDF-файла с помощью Aspose.PDF для .NET. Гибкость Aspose.PDF позволяет вам манипулировать PDF-файлами множеством способов, что делает его отличным выбором для разработчиков, которым нужны надежные решения для PDF в средах .NET. Вы можете легко расширить этот пример для поиска других слов, извлечения дополнительных сведений или даже манипулирования содержимым PDF-файла в соответствии с вашими потребностями. Надеюсь, это руководство дало вам ясный и понятный подход к работе с PDF-файлами. Попробуйте сделать это со своими собственными PDF-файлами!

## Часто задаваемые вопросы

### Могу ли я искать несколько слов одновременно?  
Да, вы можете изменить `TextFragmentAbsorber` для поиска нескольких фраз, соответствующим образом изменив строку поиска.

### А что, если текст занимает несколько строк?  
Aspose.PDF все равно распознает и извлечет текст, даже если он занимает несколько строк. Вы можете обрабатывать эти фрагменты по отдельности.

### Как сохранить извлеченный текст в файл?  
Вы можете записать извлеченный текст в файл, используя стандартные операции ввода-вывода файлов C#, такие как `StreamWriter`.

### Поддерживает ли Aspose.PDF извлечение текста из отсканированных PDF-файлов?  
Aspose.PDF не поддерживает OCR. Для сканированных PDF-файлов вам понадобится инструмент OCR для распознавания текста.

### Как работать с зашифрованными PDF-файлами?  
Если ваш PDF-файл защищен паролем, вы можете разблокировать его с помощью Aspose.PDF, указав пароль при загрузке документа.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}