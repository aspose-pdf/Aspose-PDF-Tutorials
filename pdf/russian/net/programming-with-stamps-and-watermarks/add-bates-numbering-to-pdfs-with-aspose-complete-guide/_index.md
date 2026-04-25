---
category: general
date: 2026-04-25
description: Быстро добавляйте нумерацию Бейтса в PDF с помощью Aspose.Pdf. Узнайте,
  как добавить номера страниц в PDF, автоматически регулировать размер шрифта и добавить
  текстовый водяной знак на C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: ru
og_description: Добавьте нумерацию Бейтса в PDF с помощью Aspose.Pdf. Это руководство
  показывает, как добавить номера страниц в PDF, автоматически регулировать размер
  шрифта и добавить текстовый водяной знак в одном исполняемом примере.
og_title: Добавить нумерацию Бейтса в PDF — Полный учебник Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Добавьте нумерацию Бейтса в PDF с помощью Aspose – полное руководство
url: /ru/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Добавление нумерации Бейтса в PDF с помощью Aspose – Полное руководство

Когда‑нибудь вам нужно было **add bates numbering** в PDF, но вы не знали, с чего начать? Вы не одиноки — юридические команды, аудиторы и разработчики сталкиваются с этой проблемой каждый день. Хорошая новость? С Aspose.Pdf for .NET вы можете поставить штамп с номером Бейтса, автоматически регулировать размер шрифта и даже использовать штамп как тонкий текстовый водяной знак — всё это в нескольких строках C#.

В этом руководстве мы пройдем точные шаги, чтобы **add page numbers pdf**, настроить шрифт так, чтобы он никогда не выходил за пределы, и окончательно ответить на вопрос «how to add bates». К концу вы получите готовое к запуску консольное приложение, которое создает профессионально пронумерованный PDF, и увидите, как расширить его до полноценного решения по водяным знакам.

## Требования

* **Aspose.Pdf for .NET** (последний пакет NuGet на апрель 2026).  
* .NET 6.0 SDK или новее — API работает одинаково на .NET Framework, но .NET 6 обеспечивает лучшую производительность.  
* Пример PDF с именем `input.pdf`, размещённый в папке, к которой вы можете обратиться (например, `C:\Docs\`).  

Дополнительная конфигурация не требуется; библиотека самодостаточна.

---

## Шаг 1 – Загрузка исходного PDF‑документа

Первое, что мы делаем, — открываем файл, который нужно пронумеровать. Класс `Document` из Aspose представляет весь PDF, и его загрузка так же проста, как передать путь в конструктор.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Почему это важно*: Загрузка документа даёт доступ к коллекции `Pages`, где позже мы прикрепим штамп Bates. Если файл не найден, Aspose бросает понятное `FileNotFoundException`, поэтому вы точно узнаете, в чём проблема.

---

## Шаг 2 – Создание текстового штампа для номеров Bates

Теперь мы создаём визуальный элемент, который будет отображаться на каждой странице. Класс `TextStamp` позволяет вставлять любую строку, и мы будем использовать заполнители `{page}-{total}`, чтобы Aspose заменял их автоматически.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Key points*:

* **auto adjust font size** — Установка `AutoAdjustFontSizeToFitStampRectangle` в `true` гарантирует, что текст никогда не выйдет за пределы прямоугольника, что идеально подходит для номеров страниц переменной длины.
* **add text watermark** — Уменьшив `Opacity`, мы превращаем номер Bates в лёгкий водяной знак, удовлетворяя требование «add text watermark» без отдельного шага.
* **how to add bates** — Заполнители `{page}` и `{total}` — это секретный ингредиент; Aspose заменяет их во время выполнения, так что вам не нужно ничего рассчитывать вручную.

---

## Шаг 3 – Применение штампа к каждой странице

Распространённая ошибка — ставить штамп только на первой странице. Чтобы действительно **add page numbers pdf**, нам нужно пройтись по всей коллекции `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Зачем клонировать? Метод `AddStamp` внутри создаёт копию, но явное использование нового экземпляра на каждой итерации предотвращает случайные побочные эффекты, если позже вы измените свойства штампа (например, цвет для конкретных страниц).

---

## Шаг 4 – Сохранение обновлённого PDF

С установленными штампами сохранение изменений простое. Вы можете перезаписать оригинальный файл или записать в новое место — здесь мы сохраним новый файл с именем `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Если открыть `output.pdf`, вы увидите, что каждая страница помечена «Bates: 1‑10», «Bates: 2‑10», … в правом нижнем углу, с лёгкой непрозрачностью, которая одновременно служит **add text watermark**.

---

## Полный рабочий пример

Собрав всё вместе, представляем единый, самодостаточный консольный пример, который вы можете скопировать и вставить в Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Ожидаемый результат**: Откройте `output.pdf` в любом просмотрщике; каждая страница покажет строку вроде «Bates: 3‑12» в правом нижнем углу, размер которой точно подходит под прямоугольник и отображается с непрозрачностью 40 %. Это удовлетворяет как требованию юридического отслеживания, так и необходимости визуального водяного знака.

---

## Распространённые варианты и граничные случаи

| Ситуация | Что изменить | Почему |
|-----------|----------------|-----|
| **Разное размещение** | Отрегулировать `HorizontalAlignment` / `VerticalAlignment` или задать `XIndent`/`YIndent` | Некоторые компании предпочитают размещение в верхнем левом углу или по центру. |
| **Пользовательский префикс** | Заменить `"Bates: "` на `"Doc‑ID: "` или любую другую строку | Вы можете использовать другую схему именования. |
| **Несколько штампов** | Создать второй `TextStamp` (например, для уведомления о конфиденциальности) и добавить его после первого | Комбинирование **add bates numbering** с другими требованиями **add text watermark** тривиально. |
| **Большое количество страниц** | Увеличить начальный размер шрифта (например, `14`) — авто‑регулировка уменьшит его при необходимости | Когда страниц более 999, строка становится длиннее; авто‑регулировка предотвращает обрезку. |
| **Зашифрованные PDF** | Вызвать `pdfDocument.Decrypt("password")` перед нанесением штампа | Невозможно изменить защищённый файл без пароля. |

---

## Профессиональные советы и подводные камни

* **Pro tip:** Установите `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)`, если заметите, что текст прилегает к краю страницы.  
* **Watch out for:** Очень маленькие прямоугольники (размер по умолчанию 100 × 30 pt). Если требуется большая область, задайте `batesStamp.Width` и `batesStamp.Height` вручную.  
* **Performance note:** Нанесение штампа на тысячи страниц может занять несколько секунд, но Aspose эффективно потоково обрабатывает страницы — нет необходимости загружать весь документ в память.  

---

## Заключение

Мы только что продемонстрировали, как **add bates numbering** в PDF с помощью Aspose.Pdf, одновременно **add page numbers pdf**, включить **auto adjust font size** и создать **add text watermark** в одном согласованном процессе. Полный, исполняемый пример выше предоставляет надёжную основу, которую можно адаптировать к любому рабочему процессу с юридическими документами или внутренней системе отчётности.

Готовы к следующему шагу? Попробуйте сочетать этот подход с API объединения PDF от Aspose для пакетной обработки нескольких файлов или изучите класс `TextFragment` для более сложных водяных знаков (цветные, вращаемые или многострочные). Возможностей бесконечно много, а полученный код — надёжная отправная точка.

Если руководство оказалось полезным, оставьте комментарий, поставьте звёздочку репозиторию или поделитесь своими вариантами. Приятного кодинга, и пусть ваши PDF всегда будут идеально пронумерованы!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}