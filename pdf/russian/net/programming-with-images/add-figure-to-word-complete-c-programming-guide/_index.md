---
category: general
date: 2026-04-12
description: Быстро добавляйте рисунок в Word с помощью C#. Узнайте, как позиционировать
  рисунок в Word, вставлять его в docx и добавлять пользовательский XML для продвинутого
  макета.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: ru
og_description: Быстро добавляйте рисунок в Word с помощью C#. Узнайте, как позиционировать
  рисунок в Word, вставлять его в docx и добавлять пользовательский XML для продвинутого
  оформления.
og_title: Добавить рисунок в Word – Полное руководство по программированию на C#
tags:
- C#
- Word Automation
- Document Generation
title: Добавление фигуры в Word – Полное руководство по программированию на C#
url: /ru/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавить рисунок в Word – Полное руководство по программированию на C#

Когда‑нибудь вам нужно было **add figure to Word**, но вы не знали, с чего начать? Вы не одиноки. Во многих проектах автоматизации офисных задач недостающим элементом является красиво размещённое изображение или диаграмма, находящиеся внутри пользовательской части XML. Это руководство покажет, как именно **position figure in Word**, вставить рисунок в файл *.docx* и даже подправить нижележащий пользовательский XML, чтобы объект вёл себя как любой нативный элемент Word.

Мы пройдём реальный пример с использованием библиотеки GemBox.Document (бесплатно для небольших файлов, коммерчески для больших нагрузок). К концу вы получите автономную, исполняемую программу, которая помещает рисунок в координатах X = 50, Y = 200 внутри контейнера с тегом. Никаких расплывчатых «см. документацию»‑шорткатов — только понятный код, объяснение, почему он работает, и советы, которые можно сразу скопировать в свой проект.

## Требования

- .NET 6.0 или новее (код также компилируется с .NET Core 3.1)
- NuGet‑пакет **GemBox.Document** (`Install-Package GemBox.Document`)
- Исходный файл Word (`input.docx`), уже содержащий пользовательский XML‑тег, где должен появиться рисунок
- Базовые знания C# (вы увидите, почему каждая строка важна)

> **Pro tip:** Если у вас нет предварительно помеченного документа, вы можете создать его в Word, вставив *Content Control* → *XML Mapping Pane* → сопоставив пользовательскую часть XML. Библиотека будет рассматривать этот элемент как `TaggedContent`.

## Шаг 1 – Загрузка исходного документа

Первое, что мы делаем, — открываем существующий файл *.docx*. `Document` является точкой входа для всех операций GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Почему?* Загрузка файла даёт нам доступ к его внутренним частям, включая любые контейнеры пользовательского XML. Без этого мы не смогли бы найти узел `TaggedContent`, который будет держать наш рисунок.

## Шаг 2 – Доступ к помеченному содержимому (контейнер пользовательского XML)

Пользовательский XML хранится внутри *content control* в Word. GemBox представляет его как `TaggedContent`.

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Если в документе несколько помеченных секций, `TaggedContent` возвращает **первую**. Вы также можете перечислить `doc.TaggedContents`, чтобы выбрать конкретный тег по имени.

## Шаг 3 – Создание элемента рисунка

`FigureElement` представляет изображение, диаграмму или любой визуальный объект, который Word рассматривает как *shape*. Мы создадим его внутри помеченного контейнера.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Зачем создавать рисунок здесь?* Привязывая его к узлу пользовательского XML, Word понимает, что рисунок принадлежит этой логической секции, что критично для последующего редактирования или рабочих процессов, основанных на content control.

## Шаг 4 – Точное позиционирование рисунка

Word использует пункты (1 pt ≈ 1/72 in) для позиционирования. Структура `PointF` позволяет легко задать координаты X/Y.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **How to position shape word:** Свойство `Position` принимает `PointF`, где первое значение — горизонтальное смещение (слева), а второе — вертикальное смещение (сверху) относительно полей страницы. Корректируйте эти числа, чтобы точно настроить размещение.

## Шаг 5 – Вставка рисунка в дерево помеченного содержимого

Теперь мы присоединяем рисунок к корневому элементу дерева пользовательского XML. Это физически добавляет форму в документ Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

На данном этапе рисунок уже находится в документе, но у него ещё нет источника изображения. Добавим простой PNG с диска.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Шаг 6 – Сохранение изменённого документа

Наконец, записываем изменения в новый файл *.docx*.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Когда вы откроете `output.docx` в Word, вы увидите изображение, расположенное точно в точке (50, 200) внутри пользовательского XML‑блока, который вы указали.

### Полный рабочий пример

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Expected result:** При открытии `output.docx` PNG будет размещён точно там, где вы указали, вложенный в часть пользовательского XML. Если вы исследуете XML документа (`.docx` → unzip → `word/document.xml`), вы увидите элемент `<w:pict>` с правильными координатами `<v:shape>`.

## Часто задаваемые вопросы и особые случаи

### Что делать, если в документе несколько помеченных секций?

Используйте `doc.TaggedContents` для перечисления и выбора по имени тега:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Как добавить подпись к рисунку?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Работает ли это с Word 2010 и новее?

Да. GemBox.Document ориентирован на стандарт Open XML, совместимый с Word 2007 + (включая 2010, 2013, 2016, 2019 и Microsoft 365).

### Как повернуть форму?

```csharp
figure.Rotation = 45; // degrees
```

### Как добавить векторную графику вместо растрового изображения?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro Tips & Pitfalls

- **File paths:** Используйте `Path.Combine`, чтобы избежать жёстко заданных разделителей, особенно на платформах, отличных от Windows.
- **License limits:** Бесплатная лицензия GemBox ограничивает размер документа 20 KB. Для больших файлов приобретайте коммерческий ключ.
- **Performance:** Повторное использование одного экземпляра `Document` для пакетной обработки значительно снижает нагрузку на память.
- **Shape overflow:** Если размеры рисунка превышают поля страницы, Word обрежет его. Регулируйте `figure.Width` и `figure.Height` соответственно.

## Заключение

Теперь вы знаете, **how to add figure to Word**, как **position figure in Word** с точностью, и как манипулировать нижележащим пользовательским XML, чтобы форма вела себя как любой нативный элемент. Полный, исполняемый пример демонстрирует каждый шаг — от загрузки документа, создания `FigureElement`, установки координат, прикрепления изображения и, наконец, сохранения обновлённого *.docx*.

Далее попробуйте поэкспериментировать с **insert figure into docx**, добавив несколько рисунков, используя циклы или генерируя диаграммы «на лету». Вы также можете изучить **how to add custom xml** для более богатых элементов управления или узнать **how to position shape word** в таблицах и колонтитулах. Возможностей бесконечно много, а с фундаментальными знаниями, изложенными здесь, вы готовы автоматизировать документы Word как профессионал.

Удачной разработки, и не стесняйтесь оставлять комментарии, если столкнётесь с трудностями!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}