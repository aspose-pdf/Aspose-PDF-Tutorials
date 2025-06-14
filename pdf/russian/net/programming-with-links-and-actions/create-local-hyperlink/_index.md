---
"description": "Узнайте, как легко создавать локальные гиперссылки в PDF-файлах с помощью Aspose.PDF для .NET, следуя нашему пошаговому руководству."
"linktitle": "Создать локальную гиперссылку в PDF-файле"
"second_title": "Справочник по API Aspose.PDF для .NET"
"title": "Создать локальную гиперссылку в PDF-файле"
"url": "/ru/net/programming-with-links-and-actions/create-local-hyperlink/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Создать локальную гиперссылку в PDF-файле

## Введение

В этом руководстве мы проведем вас через процесс создания локальных гиперссылок в файле PDF с помощью Aspose.PDF для .NET. Мы четко разберем каждый шаг, гарантируя, что даже если вы новичок в мире манипуляций с PDF, вы сможете без труда разобраться.

## Предпосылки

Прежде чем погрузиться в код, давайте убедимся, что у вас есть все необходимое:

1. Visual Studio: Вам понадобится это для разработки ваших .NET приложений. Загрузите его с [веб-сайт](https://visualstudio.microsoft.com/).
2. Aspose.PDF для .NET: Вы можете загрузить эту библиотеку через [ссылка для скачивания здесь](https://releases.aspose.com/pdf/net/). Он поставляется с богатым набором функций для работы с PDF-файлами.
3. Базовые знания C#: небольшое знакомство с программированием на C# не помешает, но не волнуйтесь; мы рассмотрим код строка за строкой.
4. .NET Framework: Убедитесь, что на вашем компьютере установлен .NET Framework. Вы можете проверить требования на Aspose.PDF [документация](https://reference.aspose.com/pdf/net/).

Выполнив эти предварительные условия, вы готовы научиться создавать локальные гиперссылки в ваших PDF-документах!

## Импортные пакеты

Теперь, когда вы все подготовили, пришло время импортировать необходимые пакеты в ваш проект C#. Библиотека Aspose.PDF содержит все необходимые нам классы. Вот как это сделать:

### Откройте свой проект

Откройте существующий проект .NET или создайте новый в Visual Studio. Если вы начинаете с нуля, выберите «Создать новый проект» на стартовом экране.

### Добавить ссылку на Aspose.PDF

Щелкните правой кнопкой мыши на «Зависимости» в папке вашего проекта в Solution Explorer. Выберите «Управление пакетами NuGet», затем найдите `Aspose.PDF`. Установите последнюю доступную версию. Это принесет все инструменты, необходимые для создания и обработки PDF-файлов.

### Импорт пространств имен

В верхней части файла .cs добавьте директивы using для библиотеки Aspose.PDF, например:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Таким образом, вы сможете получить доступ к функциям библиотеки.

Давайте разберем процесс создания локальных гиперссылок на простые шаги. Каждый шаг будет подробно объяснен, чтобы помочь вам понять логику, стоящую за ним.

## Шаг 1: Настройка экземпляра документа

На этом этапе вы создадите новый экземпляр класса Document, представляющий PDF-файл, с которым вы будете работать.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Установите каталог документов
Document doc = new Document(); // Создать экземпляр документа
```
The `dataDir` переменная — это место, где будет находиться ваш новый PDF-файл. Вам нужно будет заменить `"YOUR DOCUMENT DIRECTORY"` с реальным путем в вашей системе. `Document` класс создает новый PDF-документ, в который мы можем добавлять страницы и ссылки.

## Шаг 2: Добавьте страницу в документ

Далее вам нужно добавить страницу в ваш PDF-документ. 

```csharp
Page page = doc.Pages.Add(); // Добавить страницу в коллекцию страниц
```
The `Pages.Add()` Метод добавляет новую страницу в документ. Здесь будет находиться весь ваш контент.

## Шаг 3: Создайте фрагмент текста

Теперь давайте создадим фрагмент текста, который будет действовать как кликабельная ссылка.

```csharp
Aspose.Pdf.Text.TextFragment text = new Aspose.Pdf.Text.TextFragment("link page number test to page 7");
```
The `TextFragment` представляет собой фрагмент текста в PDF. Здесь мы создаем ссылку, которая сообщает пользователям, что она перенесет их на страницу 7.

## Шаг 4: Создание локальной гиперссылки

Вот тут-то и происходит волшебство! Вам нужно создать локальную гиперссылку, которая укажет фрагменту текста, куда ему следует указывать.

```csharp
Aspose.Pdf.LocalHyperlink link = new Aspose.Pdf.LocalHyperlink(); // Создать локальную гиперссылку
link.TargetPageNumber = 7; // Установить целевую страницу для экземпляра ссылки
text.Hyperlink = link; // Установить гиперссылку TextFragment
```
The `LocalHyperlink` класс — это то, что позволяет нам указывать на другие страницы в том же документе. Устанавливая `TargetPageNumber` до 7, вы указываете гиперссылке перейти на определенную страницу при нажатии.

## Шаг 5: Добавьте фрагмент текста на страницу.

После настройки гиперссылки пришло время добавить наш текстовый фрагмент на созданную нами страницу.

```csharp
page.Paragraphs.Add(text); // Добавить текст в коллекцию абзацев страницы
```
Эта строка добавляет ваш кликабельный текст в коллекцию абзацев страницы.

## Шаг 6: Создайте еще один фрагмент текста (необязательно)

Давайте добавим еще одну гиперссылку для перехода обратно на страницу 1.

```csharp
text = new TextFragment("link page number test to page 1"); // Создать новый TextFragment
text.IsInNewPage = true; // Добавить на новую страницу
```
Создание нового `TextFragment` для второй ссылки мы устанавливаем `IsInNewPage` значение true, указывающее, что этот текст будет размещен на новой странице.

## Шаг 7: Настройте вторую локальную гиперссылку

Как и прежде, вы создадите еще одну локальную гиперссылку для страницы 1.

```csharp
link = new LocalHyperlink(); // Создать еще один экземпляр локальной гиперссылки
link.TargetPageNumber = 1; // Установить целевую страницу для второй гиперссылки
text.Hyperlink = link; // Установить ссылку для второго TextFragment
```
Эта гиперссылка ведет на страницу 1, позволяя пользователям вернуться назад, когда они достигнут второй страницы.

## Шаг 8: Добавьте второй фрагмент текста на новую страницу.

Теперь давайте добавим этот текст на его страницу.

```csharp
page.Paragraphs.Add(text); // Добавить текст в коллекцию абзацев объекта страницы
```
Подобно шагу 5, эта строка добавляет новый текст гиперссылки на вновь созданную страницу.

## Шаг 9: Сохраните документ

Наконец, пришло время сохранить результаты вашего упорного труда! 

```csharp
dataDir = dataDir + "CreateLocalHyperlink_out.pdf"; // Укажите имя выходного файла
doc.Save(dataDir); // Сохранить обновленный документ
Console.WriteLine("\nLocal hyperlink created successfully.\nFile saved at " + dataDir);
```
Это объединяет ваш путь к каталогу с именем файла. `Save()` метод сохраняет ваш документ, и подтверждающее сообщение даст вам знать, что все прошло гладко!

## Заключение

Создание локальных гиперссылок в файлах PDF с помощью Aspose.PDF для .NET — это не просто крутой трюк; это практическая функция, которая улучшает навигацию и пользовательский опыт. Теперь вы вооружены знаниями, чтобы направить своих читателей прямо к нужной им информации. Просто вспомните нашу первоначальную аналогию — больше никаких потерянных душ, блуждающих по бесконечным страницам.

## Часто задаваемые вопросы

### Что такое Aspose.PDF для .NET?
Aspose.PDF для .NET — это библиотека, которая позволяет разработчикам создавать, изменять и конвертировать PDF-документы программным способом с использованием платформы .NET.

### Могу ли я создавать гиперссылки на внешние веб-страницы?
Да, Aspose.PDF также поддерживает создание гиперссылок на внешние URL-адреса, помимо локальных гиперссылок внутри PDF-файла.

### Существует ли бесплатная пробная версия Aspose.PDF?
Конечно! Вы можете получить доступ к бесплатной пробной версии из [сайт](https://releases.aspose.com/).

### Какие языки программирования поддерживает Aspose?
Aspose предлагает библиотеки для различных языков программирования, включая Java, C++ и Python, а также другие.

### Как получить поддержку по продуктам Aspose?
Вы можете обратиться за поддержкой через [Форум Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}