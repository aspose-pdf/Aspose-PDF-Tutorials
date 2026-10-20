---
category: general
date: 2026-03-06
description: Создайте PDF‑документ на C# и легко добавьте номера Бейтса. Узнайте,
  как добавить пустую страницу в PDF, разместить штамп на странице и реализовать нумерацию
  Бейтса.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: ru
og_description: Создайте PDF‑документ на C# и добавьте номер Бейтса. Это руководство
  показывает, как добавить пустую страницу PDF, разместить штамп на странице и применить
  нумерацию Бейтса.
og_title: Создание PDF‑документа с нумерацией Бейтса – учебник C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Создание PDF‑документа с нумерацией Бейтса в C# – Полное руководство
url: /ru/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF‑документа с нумерацией Бейтса в C#

Когда‑нибудь вам нужно было **создать PDF‑документ** на C# и вы задавались вопросом, как добавить нумерацию Бейтса, не теряя волосы? Вы не одиноки — юридические фирмы, суды и даже некоторые корпоративные команды по соблюдению норм сталкиваются с этой задачей каждый день. Хорошая новость? С несколькими строками кода Aspose.Pdf вы можете создать совершенно новый PDF, добавить пустую страницу и нанести правильный номер Бейтса в одном плавном процессе.

В этом руководстве мы пройдем весь процесс: от настройки проекта, до добавления пустой PDF‑страницы, до выяснения **how to add bates numbering**, и, наконец, **place stamp on page** и сохранения результата. К концу у вас будет готовый фрагмент кода, который можно вставить в любое приложение .NET. Никаких расплывчатых ссылок, только полный, исполняемый пример.

## Что понадобится

- **.NET 6+** (или .NET Framework 4.6+ – Aspose.Pdf работает с обоими)
- **Aspose.Pdf for .NET** пакет NuGet (`Install-Package Aspose.Pdf`)
- Хорошая IDE (Visual Studio, Rider или VS Code с расширением C#)

Вот и всё. Никаких дополнительных DLL, никаких внешних сервисов. Погрузимся.

## Шаг 1: Создание PDF‑документа – начальная настройка

Сначала нам нужен новый объект `Document`. Представьте его как пустой холст, на котором будет размещено всё остальное.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Почему это важно:** Класс `Document` является точкой входа для любой операции Aspose. Его создание дает доступ к коллекции `Pages`, метаданным и настройкам безопасности — всем строительным блокам профессионального PDF.

## Шаг 2: Добавление пустой страницы PDF

PDF без страниц — как книга без листов, довольно бесполезно. Добавление пустой страницы простое, и оно предоставляет поверхность для нанесения номера Бейтса.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Полезный совет:** Если нужны несколько страниц, просто вызывайте `pdfDocument.Pages.Add()` в цикле. Каждый вызов возвращает новый объект `Page`, который можно настраивать независимо.

## Шаг 3: Как добавить нумерацию Бейтса – создание TextStamp

Теперь переходим к сути: **Bates number**. В Aspose.Pdf это просто `TextStamp` со специальным флагом артефакта.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Почему мы устанавливаем `Artifact`**: Некоторые PDF‑просмотрщики показывают номера Бейтса как поисковые метаданные. Пометка штампа как артефакта `BatesNumbering` гарантирует, что последующие инструменты автоматически распознают его.

## Шаг 4: Размещение штампа на странице

С готовым штампом мы теперь **place stamp on page**. Это шаг, на котором визуальный номер действительно появляется в PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Особый случай:** Если нужно, чтобы номер увеличивался на каждой странице, следует пройтись по `pdfDocument.Pages` в цикле и обновлять `batesStamp.Value` перед вызовом `AddStamp`. В данном примере используется простое статическое значение “Bates‑001”.

## Шаг 5: Сохранение и проверка результата

Наконец, сохраняем PDF на диск. Выберите папку, в которую у вас есть права записи; иначе возникнет `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Когда откроете `BatesStamped.pdf` в любом просмотрщике, вы должны увидеть крошечный “Bates‑001”, аккуратно размещённый в правом нижнем углу пустой страницы.

> **Ожидаемый результат:**  
> ![PDF with Bates number stamp](image-placeholder.png "PDF with Bates number stamp")  
> *Alt text: PDF с штампом номера Бейтса в правом нижнем углу.*

Если номер не отображается, проверьте значения отступов и убедитесь, что размер страницы не слишком мал (по умолчанию A4 подходит). Также убедитесь, что флаг `Artifact` не удаляется какими‑либо инструментами пост‑обработки.

## Полный рабочий пример

Ниже приведена полная, готовая к копированию программа. Она включает все директивы `using` и комментарии, чтобы вы не потерялись.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Запустите программу, откройте PDF, и вы увидите номер Бейтса точно там, где мы указали. 🎉

## Распространённые варианты и подводные камни

| Сценарий | Что изменить | Почему |
|----------|----------------|-----|
| **Несколько страниц, увеличивающиеся номера** | Пройтись по `pdfDocument.Pages`, установить `batesStamp.Value = $"Bates-{i:D3}"` перед `AddStamp` | Даёт каждой странице уникальный идентификатор, типично для юридических пакетов |
| **Другой расположение (верх‑лево)** | Изменить `HorizontalAlignment = HorizontalAlignment.Left` и `VerticalAlignment = VerticalAlignment.Top` | Некоторые организации предпочитают номер в заголовке вместо нижнего колонтитула |
| **Пользовательский шрифт или цвет** | Установить `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Повышает читаемость или соответствует требованиям бренда |
| **Добавление существующего PDF в качестве фона** | Загрузить исходный PDF с помощью `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Полезно, когда нужно нанести штамп поверх заранее сгенерированной формы |

## Подведение итогов

Мы только что показали, как **create PDF document**, **add blank page pdf**, и **add bates number** с помощью Aspose.Pdf for .NET, затем **place stamp on page** и сохранить файл. Код намеренно компактный, чтобы вы могли адаптировать его к более крупным рабочим процессам — будь то пакетная обработка десятков файлов или интеграция в веб‑сервис.

Если вы готовы пойти дальше, рассмотрите:

- Автоматизировать логику увеличения для больших дел.
- Встроить генерацию PDF в API ASP.NET Core.
- Добавить безопасность (защиту паролем) с помощью `pdfDocument.Encrypt(...)`.

Не стесняйтесь экспериментировать, ломать вещи и задавать вопросы в комментариях. Приятного кодинга, и пусть ваши PDF‑файлы всегда будут идеально проставлены!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}