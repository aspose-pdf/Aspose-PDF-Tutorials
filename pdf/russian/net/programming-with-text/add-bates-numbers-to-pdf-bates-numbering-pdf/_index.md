---
category: general
date: 2026-01-15
description: Быстро добавляйте номера Бейтса в ваш PDF с помощью Aspose.Pdf. Узнайте,
  как добавить нижний колонтитул в PDF, добавить номера страниц в PDF и настроить
  пользовательскую нумерацию страниц.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: ru
og_description: Быстро добавляйте номера Бейтса в ваш PDF с помощью Aspose.Pdf. Узнайте,
  как добавить нижний колонтитул в PDF, добавить номера страниц в PDF и настроить
  пользовательскую нумерацию страниц.
og_title: Добавить номера Бейтса в PDF – нумерация Бейтса PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Добавить номера Бейтса в PDF – нумерация Бейтса PDF
url: /ru/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление номеров Бейтса в PDF – Полное руководство

Когда‑нибудь вам нужно было **add bates numbers** в PDF, но вы не знали, с чего начать? Вы не одиноки — юридические команды, аудиторы и все, кто работает с огромными наборами документов, сталкиваются с этой проблемой каждый день. Хорошая новость? С Aspose.Pdf для .NET вы можете добавить эти номера на каждую страницу всего за несколько строк кода.

В этом руководстве мы пройдем весь процесс: от подключения библиотеки Aspose.Pdf, загрузки исходного файла, настройки *BatesNumberingArtifact*, прикрепления его в качестве нижнего колонтитула и, наконец, сохранения результата. К концу вы также узнаете, как **add footer to pdf**, **add page numbers pdf**, и даже **add custom page numbering** для сложных случаев.

## Что понадобится

- .NET 6+ (или .NET Framework 4.8, если вы всё ещё используете классический стек)  
- Ссылка на пакет NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- PDF‑файл, который вы хотите пометить (назовём его `source.pdf`)  

Это всё — никаких дополнительных инструментов, никаких тяжёлых PDF‑редакторов. Приступим.

![пример добавления номеров Бейтса](https://example.com/images/add-bates-numbers.png "пример добавления номеров Бейтса")

## Шаг 1: Добавление номеров Бейтса — загрузка PDF‑документа

Сначала нам нужен объект `Document`, представляющий PDF, который мы собираемся изменить. Считайте это открытием Word‑документа перед началом ввода.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Почему это важно:** Загрузка файла даёт доступ к его коллекции `Pages`, где мы позже прикрепим артефакт нумерации Бейтса. Если файл не найден, Aspose выбросит понятное исключение `FileNotFoundException`, поэтому дважды проверьте путь.

## Шаг 2: Настройка параметров нумерации Бейтса в PDF

Теперь мы определяем *как* должны выглядеть номера. `BatesNumberingArtifact` позволяет задать префикс, начальный номер, заполнение цифрами, суффикс и расположение. Это ядро **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Совет:** Если вам нужно, чтобы номера отображались в заголовке, замените `BottomCenter` на `TopCenter`. Перечисление размещения также поддерживает `BottomLeft`, `BottomRight` и т.д., предоставляя гибкость для различных стилей **add footer to pdf**.

## Шаг 3: Добавление номеров страниц в PDF — прикрепление артефакта к каждой странице

Когда артефакт готов, мы проходим по каждой странице и добавляем его в коллекцию `Artifacts`. Это шаг, который действительно **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Что происходит за кулисами?** Коллекция `Artifacts` рендерится после основного содержимого страницы, гарантируя, что номер Бейтса находится поверх любого существующего текста, но ниже аннотаций. Если вам нужен номер позади содержимого (редко), используйте `page.Artifacts.Insert(0, batesArtifact)`.

## Шаг 4: Добавление пользовательской нумерации страниц — сохранение обновлённого PDF

Наконец, мы записываем изменённый документ на диск. Выходной файл будет содержать номера Бейтса как постоянную часть каждой страницы.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Совет по проверке:** Откройте `bates_out.pdf` в любом просмотрщике. Вы должны увидеть что‑то вроде `CASE-01000-A`, центрированное внизу каждой страницы. Если номера отсутствуют, дважды проверьте, что свойство `Placement` соответствует желаемому расположению.

## Полный рабочий пример

Объединив всё вместе, представляем полностью готовую к запуску программу:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Ожидаемый результат

- **File:** `bates_out.pdf` в той же папке, что и `source.pdf`
- **Visual:** Текст внизу‑по‑центру `CASE-01000-A`, `CASE-01001-A`, … для каждой последующей страницы
- **Behaviour:** Номера постоянно внедрены; они сохраняются при печати, уплощении и дальнейшем редактировании.

## Распространённые варианты и особые случаи

| Ситуация | Как изменить |
|-----------|---------------|
| **Другой начальный номер** | Измените `StartNumber` на любое целое число (например, `StartNumber = 500`). |
| **Буквенные суффиксы для тома** | Используйте цикл для изменения `Suffix` на каждой странице или создайте несколько артефактов с разными суффиксами. |
| **Нумерация по правому краю** | Установите `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Большие документы (10 000+ страниц)** | Рассмотрите пакетную обработку страниц или увеличение `NumberDigits`, чтобы избежать переполнения. |
| **Необходимо скрыть номера на некоторых страницах** | Пропустите эти страницы в цикле `foreach` (например, `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Осторожно:** Использование `Prefix` или `Suffix`, содержащих недопустимые символы для имён файлов (например, `*` или `?`). Aspose всё равно внедрит их, но они могут вызвать проблемы при последующем извлечении текста.

## Профессиональные советы для продакшн‑использования

- **Кешируйте артефакт**, если вы обрабатываете много PDF подряд; создание его один раз экономит несколько миллисекунд на каждый файл.  
- **Потокобезопасность:** Экземпляр `BatesNumberingArtifact` не является потокобезопасным, поэтому каждому потоку следует использовать свою копию.  
- **Производительность:** Для огромных пакетов отключите сжатие PDF (`pdfDocument.Compress = false`) перед сохранением, а затем при необходимости включите его снова.  
- **Тестирование:** Всегда проводите быструю визуальную проверку первого сгенерированного PDF, чтобы убедиться, что расположение соответствует требованиям вашей юридической команды.  

## Заключение

Теперь у вас есть надёжный, сквозной рецепт, как **add bates numbers** в любой PDF с помощью Aspose.Pdf, включая варианты **add footer to pdf**, **add page numbers pdf** и **add custom page numbering**. Код полностью автономный, работает с .NET 6 и новее, и его можно внедрить в любой существующий конвейер автоматизации.

Что дальше? Попробуйте заменить расположение `BottomCenter` на стиль заголовка, поэкспериментируйте с динамическими префиксами (например, идентификаторами дел из базы данных) или объедините это с функциями извлечения текста Aspose, чтобы создать поисковый индекс ваших только что пронумерованных документов. Возможности безграничны, и вы только что получили мощный инструмент для управления документами.

Удачной разработки, и пусть ваши PDF всегда остаются идеально пронумерованными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}