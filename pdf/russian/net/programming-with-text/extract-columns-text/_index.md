---
"description": "Узнайте, как извлекать столбцы текста из файлов PDF с помощью Aspose.PDF для .NET. Это руководство разбирает каждый шаг с примерами кода и пояснениями."
"linktitle": "Извлечь текст столбцов в файл PDF"
"second_title": "Справочник по API Aspose.PDF для .NET"
"title": "Извлечь текст столбцов в файл PDF"
"url": "/ru/net/programming-with-text/extract-columns-text/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Извлечь текст столбцов в файл PDF

## Введение

Работаете ли вы с файлами PDF и вам нужно извлечь текст в определенном формате столбцов? Обрабатываете ли вы счета-фактуры, отчеты или любые структурированные документы, точное извлечение текста из PDF может быть сложным делом. Вот где Aspose.PDF для .NET вступает в игру, чтобы упростить процесс. В этом руководстве мы покажем вам, как легко извлекать столбцы текста из файла PDF. 

## Предпосылки

Прежде чем погрузиться в код, давайте рассмотрим основные вещи, которые вам понадобятся:

- Aspose.PDF для .NET: Убедитесь, что у вас установлена последняя версия Aspose.PDF для .NET. Если нет, вы можете [скачать здесь](https://releases.aspose.com/pdf/net/).
- Среда разработки: для работы с кодом вам понадобится Visual Studio или другая среда разработки .NET.
- PDF-документ: Имейте под рукой образец PDF-документа, желательно со столбцами текста, так как мы будем извлекать из него текст.

Если вы еще не установили Aspose.PDF для .NET, вы можете скачать [бесплатная пробная версия](https://releases.aspose.com/) или [купить лицензию](https://purchase.aspose.com/buy) для полных функций. Вы также можете подать заявку на [временная лицензия](https://purchase.aspose.com/temporary-license) если необходимо.

## Импорт пространств имен

Чтобы использовать Aspose.PDF для .NET в своем проекте, вам необходимо импортировать следующие пространства имен:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## Пошаговое руководство: извлечение столбцов текста из PDF-файла

Теперь давайте разберем каждую часть кода, чтобы лучше понять, как он работает. Следуйте за нами, шаг за шагом объясняя каждый сегмент процесса.

## Шаг 1: Загрузите PDF-документ

Первое, что вам нужно сделать, это загрузить ваш PDF-файл в `Document` объект. Вот как Aspose.PDF взаимодействует с вашим документом.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "ExtractTextPage.pdf");
```

На этом этапе мы просто определяем каталог, в котором хранится ваш PDF-документ. Заменить `"YOUR DOCUMENT DIRECTORY"` с путем к вашему локальному PDF-файлу. `Document` объект загружает PDF-файл в память, делая его доступным для дальнейшей обработки.

## Шаг 2: Настройка поглотителя фрагментов текста

Далее мы будем использовать `TextFragmentAbsorber` для поглощения или захвата всего текста из файла PDF. Этот класс абсорбера предназначен для извлечения фрагментов текста из определенных областей в вашем PDF, что делает его идеальным для извлечения столбцов текста.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
pdfDocument.Pages.Accept(tfa);
TextFragmentCollection tfc = tfa.TextFragments;
```

Здесь мы создаем экземпляр `TextFragmentAbsorber` и применить его ко всем страницам PDF-файла с помощью `Accept()`. `TextFragmentCollection` сохраняет извлеченный текст, и из этой коллекции мы можем манипулировать или извлекать текст по мере необходимости.

## Шаг 3: Настройте размер шрифта извлеченного текста.

После того, как вы захватили фрагменты текста, вы можете захотеть уменьшить размер шрифта, особенно если исходный текст слишком большой. В этом примере мы уменьшаем размер шрифта на 70%.

```csharp
foreach (TextFragment tf in tfc)
{
    // Уменьшить размер шрифта на 70%
    tf.TextState.FontSize = tf.TextState.FontSize * 0.7f;
}
```

Этот код проходит по каждому `TextFragment` в коллекции и уменьшает размер шрифта на 70%. Регулировка размера шрифта может облегчить управление извлеченным текстом, особенно если вы форматируете его для разных целей.

## Шаг 4: Сохраните документ в потоке памяти

После изменения текста мы сохраняем PDF-файл в `MemoryStream`. Это позволяет нам сохранять документ в памяти для дальнейшей обработки без необходимости записывать его обратно на диск.

```csharp
Stream st = new MemoryStream();
pdfDocument.Save(st);
pdfDocument = new Document(st);
```

Здесь мы сохраняем PDF в поток памяти, а затем перезагружаем документ. Этот метод полезен, когда вы работаете с большими файлами и хотите избежать ненужных дисковых операций.

## Шаг 5: Извлеките весь текст с помощью Text Absorber

Теперь, когда мы подготовили PDF, пришло время извлечь текст. Мы будем использовать `TextAbsorber` чтобы извлечь весь текст из документа.

```csharp
TextAbsorber textAbsorber = new TextAbsorber();
pdfDocument.Pages.Accept(textAbsorber);
String extractedText = textAbsorber.Text;
```

На этом этапе `TextAbsorber` поглощает весь текст из PDF-файла, и извлеченный текст сохраняется в `extractedText` string. Вот тут-то и происходит волшебство — ваши столбцы текста теперь в формате обычного текста!

## Шаг 6: Сохраните извлеченный текст в файл.

Наконец, мы сохраняем извлеченный текст в `.txt` файл для легкого доступа и дальнейшего использования.

```csharp
dataDir = dataDir + "ExtractColumnsText_out.txt";
System.IO.File.WriteAllText(dataDir, extractedText);
Console.WriteLine("\nColumns text extracted successfully from Pages of PDF Document.\nFile saved at " + dataDir);
```

Этот код записывает извлеченный текст в новый `.txt` файл и сохраняет его в указанном вами каталоге. В консоли отображается сообщение, подтверждающее, что процесс прошел успешно.

## Заключение

Вот и все! Извлечение столбцов текста из файла PDF с помощью Aspose.PDF для .NET проще, чем вы могли бы подумать. С помощью всего нескольких строк кода вы можете загрузить PDF, извлечь определенный текст, настроить форматирование и сохранить результаты в текстовом файле.

Эта техника невероятно полезна для обработки структурированных документов, таких как таблицы, отчеты или любой контент, организованный в столбцы. Если вам нужно автоматизировать извлечение данных или обрабатывать пакетные документы, Aspose.PDF предоставляет инструменты, чтобы сделать это эффективно.

## Часто задаваемые вопросы

### Можно ли извлечь текст с определенных страниц PDF-файла?  
Да! Вы можете изменить `TextFragmentAbsorber` для таргетинга определенных страниц с помощью `pdfDocument.Pages[pageIndex].Accept(tfa);` метод.

### Можно ли извлечь текст только из одного столбца в многостолбцовом PDF-файле?  
Да, но вам нужно будет работать с координатами фрагментов текста, используя `TextFragment.Rectangle` для нацеливания на определенные области документа.

### Как можно повысить точность извлечения текста?  
Для большей точности убедитесь, что структура PDF-файла четко определена, и избегайте документов со сложными макетами. Вы также можете настроить `TextFragmentAbsorber` для извлечения текста на основе стилей шрифтов, размеров или регионов.

### Поддерживает ли Aspose.PDF извлечение текста из отсканированных документов?  
Да, но вам нужно будет использовать технологию OCR (оптическое распознавание символов). Aspose также предоставляет инструменты для этого.

### Как работать с большими PDF-файлами, содержащими тысячи страниц?  
Для больших PDF-файлов обрабатывайте документ по частям, извлекая текст из нескольких страниц за раз, чтобы избежать высокого использования памяти.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}