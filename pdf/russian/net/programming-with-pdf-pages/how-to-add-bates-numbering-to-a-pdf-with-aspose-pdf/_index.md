---
category: general
date: 2026-10-07
description: Узнайте, как добавить нумерацию Бейтса в PDF с помощью C#. Это пошаговое
  руководство также охватывает нумерацию страниц PDF и другие трюки с нумерацией.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: ru
lastmod: 2026-10-07
og_description: Быстро добавьте нумерацию Бейтса в PDF. Следуйте этому руководству,
  чтобы освоить нумерацию страниц PDF, нумеровать страницы PDF и автоматизировать
  отслеживание документов.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Добавьте нумерацию Бейтса в PDF‑файлы на C# — полное руководство Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Как добавить нумерацию Бейтса в PDF с помощью Aspose.Pdf
url: /ru/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить нумерацию Бейтса в PDF с помощью Aspose.Pdf

Если вам нужно **добавить нумерацию Бейтса** в PDF, это руководство покажет, как сделать это на C#. Независимо от того, готовите ли вы юридические досье, управляете делами или просто хотите надёжную **нумерацию страниц PDF**, ниже приведён полный, готовый к запуску пример.

В этом учебнике вы узнаете, как:

* Загрузить существующий PDF‑файл.
* Настроить параметры нумерации Бейтса, такие как префикс, начальный номер, количество цифр, разделитель и суффикс.
* Применить нумерацию ко всем страницам.
* Сохранить обновлённый документ.

Никакие внешние инструменты не требуются, кроме библиотеки Aspose.Pdf для .NET, а код работает как с .NET 6+, так и с .NET Framework 4.7.2+.  

---

## Требования

Прежде чем начать, убедитесь, что у вас есть:

| Требование | Почему это важно |
|-------------|-------------------|
| **Aspose.Pdf for .NET** (NuGet‑пакет `Aspose.Pdf`) | Предоставляет классы `Document` и `BatesNumberingOptions`, используемые в коде. |
| **.NET SDK** (рекомендовано 6.0 или новее) | Позволяет компилировать и запускать консольное приложение C#. |
| **Исходный PDF**, который нужно пронумеровать | В примере используется `source.pdf`; замените путь на свой файл. |
| **Права записи** в папку вывода | Метод `Save` требует возможности записать новый файл. |

Установить библиотеку можно следующей командой CLI:

```bash
dotnet add package Aspose.Pdf
```

---

## Шаг 1: Создать новый консольный проект

Откройте терминал и выполните:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Это создаст минимальный проект C#, в который мы добавим код для **добавления нумерации Бейтса**.

---

## Шаг 2: Добавить необходимые директивы `using`

Откройте `Program.cs` и добавьте пространства имён в начале файла:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` даёт доступ к классу `Document` для загрузки и сохранения PDF‑файлов.  
* `Aspose.Pdf.Text` содержит `BatesNumberingOptions` — объект, определяющий внешний вид номеров.

---

## Шаг 3: Загрузить исходный PDF

Первая исполняемая строка загружает PDF, который нужно пронумеровать. Замените `"YOUR_DIRECTORY/source.pdf"` реальным путём к вашему файлу.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Если файл не найден, Aspose бросит `FileNotFoundException`. Чтобы избежать этого, можно предварительно проверить путь:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Шаг 4: Определить параметры нумерации Бейтса

`BatesNumberingOptions` позволяет управлять каждым визуальным элементом нумерации. Ниже показана типичная конфигурация для юридических дел:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Значение каждой свойства**

| Свойство | Назначение |
|----------|------------|
| `Prefix` | Позволяет группировать документы по проекту, клиенту или делу. |
| `StartNumber` | Устанавливает начальное значение счётчика; полезно, если у вас уже есть пронумерованные файлы. |
| `Digits` | Обеспечивает одинаковую ширину номера, упрощая сортировку. |
| `Separator` | Улучшает читаемость, особенно при комбинировании префикса и суффикса. |
| `Suffix` | Позволяет добавить год, версию или любой завершающий идентификатор. |

Вы также можете задать расположение (верх, низ, левый, правый) и стиль шрифта, используя `batesOptions.Position` и `batesOptions.Font`. Для большинства сценариев подходят значения по умолчанию (нижний‑правый угол, 12‑pt Times New Roman).

---

## Шаг 5: Применить нумерацию ко всем страницам

Вызов `pdf.BatesNumbering.Add` вставляет номера на каждую страницу в порядке их следования.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Если нужно **нумеровать страницы PDF** только в части документа (например, пропустить титульную страницу), можно передать `PageCollection`:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Шаг 6: Сохранить обновлённый PDF

Наконец, запишите изменённый документ на диск. Имя файла обычно указывает, что PDF теперь содержит номера Бейтса.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Если папка вывода не существует, Aspose создаст её автоматически. Однако убедитесь, что у вас есть права записи, чтобы избежать `UnauthorizedAccessException`.

---

## Полный, готовый к запуску пример

Объединив всё вместе, получаем полную программу, которую можно скопировать, вставить и запустить:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Ожидаемый вывод** (консоль):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Откройте `bates_numbered.pdf` — вы увидите, что каждая страница помечена, например, `CASE-001000-2025`, `CASE-001001-2025` и т.д., в нижнем‑правом углу по умолчанию.

---

## Часто задаваемые вопросы (FAQ)

### 1. Можно ли изменить расположение номеров?
Да. Установите `batesOptions.Position = new Position(10, 10, 10, 10);`, где четыре значения представляют отступы от верхнего, нижнего, левого и правого краёв. Aspose также предоставляет предопределённые перечисления, такие как `BatesNumberingPosition.BottomCenter`.

### 2. Что если в моём PDF уже есть номера страниц?
Добавление номеров Бейтса **наложит** их поверх существующих. Чтобы избежать визуального захламления, либо скройте оригинальные номера (если они находятся в текстовом слое), либо скорректируйте размер шрифта и позицию в `batesOptions`.

### 3. Работает ли это с зашифрованными PDF?
Aspose может открыть PDF, защищённый паролем, если вы передадите пароль:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

Нумерация Бейтса будет применена тем же способом.

### 4. Как **нумеровать страницы PDF** простым последовательным счётчиком (без префикса/суффикса)?
Просто задайте `Prefix = string.Empty` и `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Можно ли использовать этот подход в ASP.NET Core для динамической выдачи PDF?
Определённо. Загрузите документ, примените нумерацию, затем запишите поток в HTTP‑ответ:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Особые случаи и рекомендации по лучшим практикам

| Ситуация | Рекомендованный подход |
|-----------|------------------------|
| **Большие PDF (сотни страниц)** | Вызывайте `pdf.BatesNumbering.Add` **после** всех преобразований уровня страниц, чтобы избежать повторной обработки одних и тех же страниц. |
| **Пользовательские шрифты** | Установите `batesOptions.Font = FontRepository.FindFont("Arial")` и скорректируйте `batesOptions.FontSize` для лучшей читаемости сканированных документов. |
| **Батч‑задачи, критичные к производительности** | Переиспользуйте один экземпляр `Document` при обработке множества файлов в цикле; освобождайте его после каждой итерации, чтобы экономить память. |
| **Международные символы** | Используйте шрифты с поддержкой Unicode (например, `Times New Roman Unicode`), чтобы префикс или суффикс отображались корректно. |
| **Совместимость версий** | Код работает с Aspose.Pdf 23.10 и новее. При работе со старой версией проверьте справочник API на предмет изменений имён свойств. |

---

## Заключение

Теперь вы знаете, как **добавить нумерацию Бейтса** в PDF с помощью Aspose.Pdf для .NET. В руководстве рассмотрены загрузка PDF, настройка `BatesNumberingOptions`, применение номеров к каждой странице и сохранение результата. На основе этих блоков вы также сможете реализовать общую **нумерацию страниц PDF**, **нумеровать страницы PDF** с пользовательскими форматами и интегрировать процесс в более крупные автоматизированные конвейеры.

**Следующие шаги**

* Изучите API **bates numbering pdf** подробнее, чтобы настроить шрифт, цвет и позицию.  
* Скомбинируйте эту технику с **цифровыми подписями**, создавая юридически защищённые досье.  
* Ознакомьтесь с возможностями **слияния PDF** в Aspose, если нужно объединить несколько дел перед нумерацией.

Экспериментируйте с различными префиксами, суффиксами и длиной цифр, чтобы соответствовать стандартам вашей организации. Приятного кодинга!

## Что стоит изучить дальше?

Следующие учебники охватывают близкие темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}