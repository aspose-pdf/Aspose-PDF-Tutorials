---
category: general
date: 2026-06-08
description: Добавьте нумерацию Бейтса в PDF с помощью Aspose.Pdf на C#. Узнайте,
  как добавить Бейтс, добавить номера страниц в PDF, добавить последовательные номера
  в PDF, и посмотрите пример PDF с нумерацией Бейтса.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: ru
og_description: Добавьте нумерацию Бейтс в PDF на C#. Этот учебник показывает, как
  добавить Бейтс, добавить номера страниц в PDF и добавить последовательные номера
  в PDF с полным примером нумерации Бейтс.
og_title: Добавление нумерации Бейтса в PDF – Полное руководство с Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Добавление нумерации Бейтса в PDF – Полное руководство с Aspose
url: /ru/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление нумерации Бейтса в PDF – Полное руководство по программированию

Когда‑нибудь нужно было **add bates numbering pdf**, но вы не знали, с чего начать? Если вы задавались вопросом *how to add bates* в юридический документ, вы попали по адресу. В этом руководстве мы пошагово пройдем через практический пример от начала до конца, который не только добавляет нумерацию Бейтса, но и показывает, как **add page numbers pdf**, **add sequential numbers pdf**, а также предоставляет готовый к запуску **bates number pdf example**.

Мы будем использовать библиотеку Aspose.Pdf для .NET, потому что она скрывает низкоуровневые детали PDF, предоставляя при этом тонкую настройку. К концу этого руководства у вас будет переиспользуемый фрагмент кода, который можно вставить в любой C#‑проект, и вы поймёте, почему каждая строка важна.

## Что понадобится

- **.NET 6.0** или новее (код также работает на .NET Framework 4.6+).  
- **Лицензия** Aspose.Pdf или бесплатный временный ключ оценки.  
- Пример PDF‑файла `input.pdf`, размещённый в папке, к которой вы можете обратиться.  
- Visual Studio, Rider или любой другой C#‑редактор по вашему выбору.

И всё — никаких дополнительных инструментов, никаких командных трюков. Готовы? Поехали.

## Add Bates Numbering PDF – пошаговая реализация

Ниже процесс разбит на шесть логических шагов. Каждый шаг включает короткий фрагмент кода, объяснение *почему* мы это делаем, и совет, который может пригодиться.

### Шаг 1: Установите NuGet‑пакет Aspose.Pdf

Сначала добавьте библиотеку в ваш проект. Откройте Package Manager Console и выполните:

```powershell
Install-Package Aspose.Pdf
```

> **Pro tip:** Если вы работаете с .NET Core, можно также использовать `dotnet add package Aspose.Pdf`.

Установка пакета даёт доступ к классу `Aspose.Pdf.Facades.BatesNumbering`, который является «рабочей лошадкой» для **add bates numbering pdf**.

### Шаг 2: Откройте исходный PDF‑документ

Теперь загрузим PDF, который будем штамповать. Оператор `using` гарантирует, что файл будет закрыт корректно, даже если возникнет исключение.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

Почему именно `Aspose.Pdf.Document`? Он представляет весь PDF в памяти, позволяя манипулировать страницами, шрифтами и метаданными без изменения оригинального файла на диске.

### Шаг 3: Создайте фасад Bates Numbering

Паттерн *facade* скрывает сложность внутренней структуры PDF. Вот как мы его инстанцируем:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

Этот объект позже будет сконфигурирован с префиксом, начальным номером и параметрами форматирования. По сути, это «двигатель», который **add page numbers pdf** в соответствии с требованиями Бейтса.

### Шаг 4: Настройте начальный номер и префикс

Номера Бейтса часто включают префикс, специфичный для дела. Также можно задать количество цифр, разделитель и позицию на странице.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**Почему такие настройки?**  
- `StartNumber` позволяет продолжить предыдущую серию.  
- `NumberOfDigits` гарантирует одинаковую длину, что критично для юридической индексации.  
- `Location` определяет, где будет отображаться **add sequential numbers pdf**; при желании можно переместить его в правый верхний угол.

### Шаг 5: Примените нумерацию Бейтса к документу

После настройки фасада мы штампуем каждую страницу:

```csharp
bates.AddBatesNumbering(doc);
```

Под капотом Aspose проходит по всем страницам, рисует текст в указанном месте и учитывает уже существующее содержимое. Эта единственная строка действительно **add bates numbering pdf** в ваш файл.

### Шаг 6: Сохраните изменённый PDF

Наконец, запишем результат на диск:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

Теперь у вас есть PDF, где каждая страница несёт уникальный идентификатор Бейтса, готовый к использованию в процессе раскрытия или в суде.

#### Полный рабочий пример (Bates Number PDF Example)

Собрав всё вместе, получаем полностью автономную программу, которую можно скомпилировать и запустить:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **Expected output:** Откройте `output.pdf`, и вы увидите «CASE‑01000», «CASE‑01001», … в левом нижнем углу каждой страницы.

![Скриншот страницы PDF с нумерацией Бейтса в левом нижнем углу – add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "add bates numbering pdf example")

*(Текст альтернативного описания изображения: *пример добавления нумерации Бейтса в PDF* – показывает, как нумерация Бейтса применена к образцу PDF.)*

## Как добавить Бейтс – понимание фасада

Возможно, вы задаётесь вопросом **how to add bates** без фасада Aspose. Альтернатива — вручную рисовать текст на каждой странице, используя низкоуровневые PDF‑операторы, но такой подход склонен к ошибкам и требует глубоких знаний спецификации PDF. Фасад абстрагирует эти детали, позволяя сосредоточиться на *что* вы хотите (префикс, начальный номер), а не на *как* это отрисовать.

Если вам когда‑нибудь понадобится **add page numbers pdf** в стиле, не связанном с Бейтсом (например, «Страница 3 из 12»), вы можете переиспользовать тот же класс `BatesNumbering` — просто задайте пустой `Prefix` и измените `Location`. Подлежащий движок остаётся тем же, что обеспечивает единообразную отрисовку в обоих сценариях.

## Add Page Numbers PDF – настройка положения и стиля

Юридические команды часто требуют номер страницы в шапке, тогда как специалисты по поддержке судебных дел предпочитают нижний колонтитул. Вот быстрый трюк:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

Тот же вызов `AddBatesNumbering` теперь **add page numbers pdf** в верхней части каждой страницы. Поскольку фасад работает с объектом документа, переключаться между нумерацией Бейтса и обычной нумерацией страниц можно, меняя несколько свойств — без переписывания цикла.

## Add Sequential Numbers PDF – расширенное форматирование

Предположим, вам нужен формат `2023-CASE-00123`. Можно комбинировать префикс даты с текущими настройками:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

Теперь каждая страница будет отображать `2023-CASE-00123`, `2023-CASE-00124` и т.д. Это демонстрирует, насколько легко можно **add sequential numbers pdf**, удовлетворяющие сложным правилам именования.

## Пограничные случаи и распространённые подводные камни

| Situation | What to watch out for | Suggested fix |
|-----------|----------------------|---------------|
| **Very large PDFs ( > 500 MB )** | Memory consumption can spike because the whole document is loaded into RAM. | Use `Document` with `MemoryManagement` settings or process the file in chunks with `PdfFileEditor`. |
| **Existing page numbers** | Существующая нумерация страниц |  |

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}