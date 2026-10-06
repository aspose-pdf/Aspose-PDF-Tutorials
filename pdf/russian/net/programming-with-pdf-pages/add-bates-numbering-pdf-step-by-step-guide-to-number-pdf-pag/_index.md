---
category: general
date: 2026-03-03
description: Быстро добавляйте нумерацию Бейтса в PDF и узнайте, как нумеровать страницы
  PDF или добавить последовательные номера PDF с помощью Aspose.Pdf в C#.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: ru
og_description: Добавьте нумерацию Бейтса в PDF на C# для нумерации страниц PDF и
  добавления последовательных номеров PDF. Полный код, объяснения и лучшие практики.
og_title: Добавление нумерации Бейтса в PDF – Полный учебник по C#
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: Добавление нумерации Бейтса в PDF – пошаговое руководство по нумерации страниц
  PDF
url: /ru/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление Bates Numbering PDF – Полный учебник C#

Когда‑нибудь вам нужно было **add bates numbering pdf** файлы, но вы не знали, с чего начать? Вы не одиноки — юридические отделы, аудиторы и архивисты сталкиваются с той же проблемой. Хорошая новость? С несколькими строками C# и библиотекой Aspose.Pdf вы можете автоматически **number pdf pages**, а также получите гибкость **add sequential pdf numbers** с пользовательскими префиксами, суффиксами и размещением.

В этом руководстве мы пройдём реальный пример, объясним, почему каждый параметр важен, и покажем, как подстроить код под особые случаи, такие как разные размеры страниц или пользовательское количество цифр. К концу вы получите готовый к запуску фрагмент, который добавит Bates‑номера к любому PDF‑файлу, и поймёте «почему» за каждой опцией.

## Предварительные требования

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+)
- Действующая лицензия Aspose.Pdf for .NET (или бесплатный оценочный ключ)
- Visual Studio 2022 (или любой предпочитаемый редактор C#)
- Исходный PDF с именем `source.pdf` в папке, к которой вы можете обратиться

Это всё — никаких дополнительных пакетов NuGet, кроме Aspose.Pdf.

## Шаг 1 – Открытие исходного PDF‑документа

Первое, что нужно сделать, — загрузить PDF, который вы хотите проставить. Использование блока `using` гарантирует корректное освобождение дескриптора файла, что предотвращает проблемы с блокировкой позже.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Почему это важно:** Открытие документа внутри `using` гарантирует детерминированное освобождение ресурсов. Если пропустить это, файл может оставаться заблокированным, и последующие попытки сохранить или удалить PDF завершатся неудачей — то, что я часто видел в производственных конвейерах.

## Шаг 2 – Настройка параметров Bates Numbering

Теперь мы говорим Aspose, как должны выглядеть Bates‑номера. Каждый параметр напрямую соответствует визуальному элементу на странице.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### Быстрые советы по параметрам

| Свойство | Что делает | Когда менять |
|----------|------------|--------------|
| **Prefix / Suffix** | Добавляет статический текст перед/после числовой части. | Используйте идентификатор дела, код проекта или «CONF‑» для конфиденциальных документов. |
| **Start** | Первое число в серии. | Если вы продолжаете схему нумерации из предыдущей партии, задайте соответствующее значение. |
| **NumberOfDigits** | Управляет заполнением нулями. | Для юридических дел часто требуется ровно 6 цифр; установите `6`. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | Выбирайте в зависимости от макета документа; BottomRight — самый распространённый вариант для Bates‑номеров. |

> **Pro tip:** Если вам нужно **number pdf pages** в нескольких колонках, вы можете вызвать `pdfDocument.AddBatesNumbering` дважды с разными значениями `Placement` и различными строками `Prefix`.

## Шаг 3 – Применение Bates Numbering к документу

С готовыми параметрами проставление происходит одной вызванной функцией. Aspose internally обрабатывает пагинацию, вращение и расчёт отступов.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Почему один вызов работает:** Внутри Aspose проходит по `pdfDocument.Pages`, создаёт `TextFragment` для каждой страницы и позиционирует его согласно выбранному `Placement`. Эта абстракция избавляет вас от написания ручного цикла и работы с преобразованием координат.

## Шаг 4 – Сохранение обновлённого PDF

Наконец, запишите изменённый файл на диск. Можно перезаписать оригинал или создать новый — пример ниже создаёт копию.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

Если вам нужно **add sequential pdf numbers** в поток (например, при отправке файла через API), замените путь к файлу на `MemoryStream`:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## Полный рабочий пример

Объединив всё вместе, получаем полностью готовую к запуску программу:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### Ожидаемый результат

- Появляется новый файл `bates_numbered.pdf` в `C:\MyDocs`.
- На каждой странице отображается что‑то вроде `2025-05000-A`, `2025-05001-A`, … в правом нижнем углу.
- Числа дополнены нулями до пяти цифр, согласно настройке `NumberOfDigits`.

## Обработка распространённых вариантов

### 1. Разные размеры страниц

Если ваш PDF содержит как портретные, так и альбомные страницы, номер может обрезаться на более широкой стороне. Чтобы исправить, включите свойство `AutoFit`:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. Пользовательский шрифт или цвет

По умолчанию Bates‑номера черные, 12‑pt Times New Roman. Измените внешний вид, получив доступ к `TextState`:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. Пропуск страниц

Предположим, вы хотите **number pdf pages**, но пропустить титульную страницу. Используйте диапазон страниц:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. Добавление нескольких схем нумерации

Юридические отделы иногда требуют одновременно Bates‑номер и конфиденциальный водяной знак. Выполните два отдельных вызова `AddBatesNumbering` с разными значениями `Placement`:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## Часто задаваемые вопросы

**Q: Работает ли это с PDF, в которых уже есть существующий текст?**  
**A:** Да. Aspose добавляет Bates‑номер как отдельный слой, поэтому существующее содержание остаётся нетронутым. Если вам нужно, чтобы номера отображались *за* существующим текстом (редко), придётся вручную манипулировать потоками содержимого страницы.

**Q: Что делать, если PDF защищён паролем?**  
**A:** Сначала загрузите его с паролем: `new Document(path, new LoadOptions { Password = "secret" })`. После проставления номера можно снова применить шифрование через `pdfDocument.Encrypt(...)`.

**Q: Можно ли использовать это в консольном приложении .NET Core?**  
**A:** Конечно. Тот же код работает в .NET Core, .NET 5+, и .NET Framework. Достаточно добавить соответствующий пакет Aspose.Pdf NuGet.

## Заключение

Мы только что рассмотрели, как **add bates numbering pdf** файлы, как **number pdf pages**, и как **add sequential pdf numbers** с полным контролем над форматированием, размещением и обработкой особых случаев. Краткий фрагмент кода выше делает основную работу, а дополнительные параметры позволяют адаптировать решение под любой юридический, архивный или комплаенс‑процесс.

Готовы к следующему шагу? Попробуйте сочетать этот подход с:

- **Batch processing** — проход по папке PDF‑файлов и применение единой схемы нумерации.
- **Dynamic prefixes** — вытягивание идентификаторов дел из базы данных и подстановка их в каждый документ.
- **PDF/A compliance** — после нумерации вызвать `pdfDocument.Convert(..., PdfFormat.PdfA2b)`, чтобы обеспечить долговременное хранение.

Не стесняйтесь экспериментировать, делиться результатами или задавать вопросы в комментариях. Приятного кодинга, и пусть ваши PDF‑файлы всегда остаются идеально проиндексированными! 

![Screenshot of a PDF page with Bates numbers in the bottom‑right corner](https://example.com/images/bates-numbered.png "add bates numbering pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}