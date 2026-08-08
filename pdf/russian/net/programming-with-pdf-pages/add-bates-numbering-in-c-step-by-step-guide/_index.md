---
category: general
date: 2026-03-27
description: Быстро добавляйте нумерацию Бейтса на C#. Узнайте, как добавить пользовательские
  номера страниц, последовательную нумерацию страниц и пользовательские номера в документы
  Word.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: ru
og_description: Добавьте нумерацию Бейтса в C# с понятным примером. Это руководство
  показывает, как добавить пользовательскую нумерацию страниц, добавить последовательную
  нумерацию страниц и многое другое.
og_title: Добавление нумерации Бейтса в C# – Полный учебник
tags:
- C#
- Document Processing
- Bates Numbering
title: Добавление нумерации Бейтса в C# – пошаговое руководство
url: /ru/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление Bates нумерации в C# – Пошаговое руководство

Вы когда‑нибудь задумывались, как **add bates numbering** в документ Word, не теряя волосы? Вы не одиноки. Во многих юридических или комплаенс‑проектах каждая страница требует уникального идентификатора, а делать это вручную — настоящий кошмар.  

В этом руководстве мы пройдем полный, исполняемый пример, который **adds bates numbering**, показывает вам **how to add bates** в несколько строк, а также охватывает, как **add custom page numbers** и **add sequential page numbers**, когда это необходимо. К концу вы получите файл .docx, помеченный выбранными вами номерами — без сторонних инструментов.

## Что вы узнаете

- Загрузить DOCX‑файл с помощью Aspose.Words for .NET API (или любой совместимой библиотеки).  
- Настроить **add custom numbers**, такие как префикс, начальное значение и размер шрифта.  
- Применить нумерацию ко всем страницам одним вызовом.  
- Сохранить результат и проверить, что номера отображаются как ожидалось.  

Предыдущий опыт работы с Bates нумерацией не требуется; достаточно базовой настройки C# и копии исходного документа. Давайте начнём.

## Предварительные требования

- .NET 6+ (код работает как на .NET Core, так и на .NET Framework).  
- Aspose.Words for .NET, установленный через NuGet (`Install-Package Aspose.Words`).  
- Документ Word с именем `input.docx`, размещённый в папке, к которой вы можете обратиться (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code или любой понравившийся вам IDE для C#.

> **Pro tip:** Если вы используете другую библиотеку (например, Open XML SDK), концепции остаются теми же — просто замените вызовы API.

## Шаг 1: Загрузка исходного документа

Сначала нам нужно загрузить файл Word в память.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Почему это важно:* Загрузка файла создаёт объект `Document`, который даёт доступ к страницам, разделам и низкоуровневому дереву узлов. Без него вы не сможете добавить нумерацию.

## Шаг 2: Настройка параметров Bates нумерации

Теперь мы определяем, как именно должны выглядеть номера. Здесь вы **add custom page numbers** или **add sequential page numbers**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Почему это важно:* `Prefix` позволяет **add custom numbers**, например идентификатор дела, а `Start` определяет начальное значение счётчика. Изменение `FontSize` гарантирует, что номера не перекрывают поля страницы.

## Шаг 3: Применение Bates нумерации ко всем страницам

Когда параметры готовы, мы просим библиотеку проставить номер на каждой странице.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Почему это важно:* Метод `AddBatesNumbering` проходит по внутренней коллекции страниц и вставляет текстовое поле в правый нижний угол (место по умолчанию). Это суть **how to add bates**, без необходимости писать цикл вручную.

## Шаг 4: Сохранение обновлённого документа

Наконец, мы записываем изменённый файл обратно на диск.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Почему это важно:* Сохранение создаёт новый `output.docx`, который можно открыть в Word, LibreOffice или любом просмотрщике, чтобы убедиться, что номера отображаются.

## Ожидаемый результат

Откройте `output.docx`. На каждой странице должно отображаться что‑то вроде:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Если открыть предварительный просмотр печати документа, вы увидите номера в правом нижнем углу, соответствующие установленному размеру шрифта.

## Пограничные случаи и варианты

| Ситуация | Что изменить | Почему |
|-----------|----------------|-----|
| **Не нужен префикс** | `Prefix = string.Empty` | Удаляет часть “ABC‑”, оставляя только числовую последовательность. |
| **Начать с 1** | `Start = 1` | Полезно для простого **add sequential page numbers** без пользовательского префикса. |
| **Большие документы (>10 000 страниц)** | Increase `FontSize` or adjust `Location` (use overloads of `AddBatesNumbering`) | Предотвращает перекрытие с колонтитулами. |
| **Только для чтения исходный файл** | Open with `LoadOptions` that allow write access, or copy the file first | В противном случае `document.Save` вызовет исключение. |
| **Другое расположение** | Use `batesOptions.Position = BatesNumberingPosition.TopLeft` (or other enum) | Некоторые фирмы требуют номера в верхней части страницы. |

> **Note:** Не все библиотеки предоставляют класс `BatesNumberingOptions`. С Open XML SDK вам придётся вручную вставлять `TextBox` — тот же принцип, но больше кода.

## Полный рабочий пример

Вот вся программа в одном месте. Скопируйте‑вставьте её в консольное приложение и запустите.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Запустите программу, откройте `output.docx`, и вы увидите нумерацию точно там, где ожидали. 🎉

## Часто задаваемые вопросы

**Q: Можно ли изменить цвет номеров?**  
A: Да. После вызова `AddBatesNumbering` вы можете получить сгенерированные объекты `Shape` и установить их свойство `FillColor`.

**Q: Что делать, если нужны номера слева вместо справа?**  
A: Используйте `batesOptions.Position = BatesNumberingPosition.BottomLeft` (или `TopLeft`, `TopRight`). API поддерживает все четыре угла.

**Q: Работает ли это с выводом в PDF?**  
A: Абсолютно. После добавления нумерации вызовите `document.Save("output.pdf")`. Номера будут отрисованы в PDF так же, как в Word.

## Заключение

Теперь вы знаете **how to add bates numbering** в файл Word с помощью C#. Руководство охватило загрузку документа, настройку **add custom numbers**, применение **add sequential page numbers** и сохранение окончательного результата. С полным примером кода вы можете добавить его в любой проект и сразу начать проставлять номера в документах.

Готовы к следующему вызову? Попробуйте объединить это с пакетным процессором, который проходит по папке файлов, или изучите **add custom page numbers** в заголовке/колонтитуле для более изысканного вида. В любом случае у вас есть прочная база для любой задачи в области legal‑tech или автоматизации комплаенса.

Есть вопросы или интересный пример использования? Оставьте комментарий ниже, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}