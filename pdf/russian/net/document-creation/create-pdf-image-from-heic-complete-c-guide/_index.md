---
category: general
date: 2026-06-08
description: Создайте PDF‑изображение в C#, преобразуя HEIC в PDF. Узнайте, как добавить
  изображение в PDF и сгенерировать PDF из изображения с пошаговым кодом.
draft: false
keywords:
- create pdf image
- convert heic to pdf
- add image to pdf
- generate pdf from image
- how to read heic
language: ru
og_description: Создайте PDF‑изображение в C#, преобразовав HEIC в PDF. Следуйте этому
  руководству, чтобы добавить изображение в PDF и быстро сгенерировать PDF из изображения.
og_title: Создание PDF‑изображения из HEIC – Полный учебник по C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  headline: Create PDF Image from HEIC – Complete C# Guide
  type: TechArticle
- description: Create PDF image in C# by converting HEIC to PDF. Learn how to add
    image to PDF and generate PDF from image with step‑by‑step code.
  name: Create PDF Image from HEIC – Complete C# Guide
  steps:
  - name: What if the HEIC file is corrupted?
    text: The `HeicImage.Load` method throws a `HeicException`. Wrap the call in a
      try/catch (as shown) and log the error. In production you might fall back to
      a default placeholder image.
  - name: Can I batch‑process multiple HEIC files?
    text: Absolutely. Just move the core logic into a method like `ConvertHeicToPdf(string
      input, string output)` and iterate over a directory with `Directory.GetFiles("*.heic")`.
  - name: Does this approach preserve EXIF metadata?
    text: No, Aspose.Pdf does not automatically copy EXIF data into the PDF. If you
      need metadata, extract it with `HeicImage.Metadata` and add it to the PDF using
      `Document.Info` properties.
  - name: What about memory usage for huge images?
    text: For images larger than 10 MP, consider down‑sampling before creating `BitmapInfo`.
      You can use `HeicImage.Resize` (if supported) or a third‑party bitmap library
      to reduce dimensions.
  type: HowTo
tags:
- C#
- Aspose.Pdf
- HEIC
- ImageConversion
title: Создать PDF‑изображение из HEIC – Полное руководство по C#
url: /ru/net/document-creation/create-pdf-image-from-heic-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF‑изображения из HEIC – Полное руководство на C#

Когда‑нибудь задавались вопросом, как **создать PDF‑изображение** из файла HEIC, не теряя волосы? Вы не одиноки. Во многих мобильных приложениях камера сохраняет изображения в формате HEIC, однако устаревшие системы всё ещё нуждаются в привычном PDF. В этом руководстве показано, как **конвертировать HEIC в PDF**, добавить изображение на новую страницу PDF и, наконец, **создать PDF из изображения** с помощью Aspose.Pdf.

Мы пройдёмся по каждой строке кода, объясним, почему каждый элемент важен, и предоставим готовый к запуску пример. К концу вы сможете помещать HEIC в папку и получать чёткий PDF — без внешних инструментов.

## Что вы узнаете

* Как **читать HEIC** файлы в C# с помощью декодера `FileFormat.Heic`.
* Точные шаги для **конвертации HEIC в PDF** с Aspose.Pdf.
* Способы **добавления изображения в PDF** и управления форматом пикселей.
* Советы по работе с большими изображениями и распространёнными подводными камнями.
* Полностью готовая к компиляции программа, которую можно скопировать и вставить.

*Prerequisites*: .NET 6+ (или .NET Framework 4.6+), Aspose.Pdf for .NET и пакет NuGet `FileFormat.Heic`. Если вы никогда не использовали эти библиотеки, не переживайте — установка описана в первом шаге.

---

## Шаг 0: Установка необходимых пакетов

Прежде чем погрузиться в код, убедитесь, что обе библиотеки подключены к вашему проекту:

```powershell
dotnet add package Aspose.Pdf
dotnet add package FileFormat.Heic
```

Оба пакета бесплатны для разработки и поддерживают .NET Standard, поэтому они работают в консольных приложениях, ASP.NET или даже Unity.

---

## Шаг 1: Как читать HEIC – загрузка файла как потока

Чтение файла HEIC похоже на открытие любого бинарного файла, но требуется декодер, понимающий контейнер HEIC. Библиотека `FileFormat.Heic` предоставляет удобный статический метод `Load`.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using FileFormat.Heic.Decoder;

// ...

// Open the HEIC file safely with a using block
using (FileStream heicStream = new FileStream(
           @"C:\Images\input.heic", FileMode.Open, FileAccess.Read))
{
    // Decode the HEIC image into a HeicImage object
    HeicImage heicImage = HeicImage.Load(heicStream);
```

**Почему поток?**  
Поток позволяет декодеру читать файл лениво, что снижает нагрузку на память при работе с огромными изображениями. Оператор `using` также гарантирует освобождение файлового дескриптора, предотвращая ошибки блокировки файла позже.

---

## Шаг 2: Конвертация HEIC в PDF – извлечение пиксельных данных

Aspose.Pdf ожидает необработанные данные bitmap, а не объект HEIC. Поэтому мы извлекаем байты пикселей в формате, который он понимает — `Rgb24` подходит для большинства случаев.

```csharp
    // Grab the raw RGB24 pixel array from the HEIC image
    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);

    // Capture image dimensions for later use
    int width  = (int)heicImage.Width;
    int height = (int)heicImage.Height;
```

**Примечание к граничному случаю:** Если ваш исходный HEIC содержит альфа‑канал, `Rgb24` его отбрасывает. Для прозрачности следует переключиться на `Rgba32` и соответственно скорректировать `BitmapInfo`.

---

## Шаг 3: Добавление изображения в PDF – создание объекта Aspose Image

Теперь мы упаковываем необработанные байты в `Aspose.Pdf.Image`. Конструктор `BitmapInfo` сообщает Aspose о шаге строки, размере и формате пикселей.

```csharp
    // Create an Aspose PDF Image using the pixel buffer
    Image pdfImage = new Image
    {
        BitmapInfo = new BitmapInfo(
            pixelData,
            width,
            height,
            BitmapInfo.PixelFormat.Rgb24)
    };
```

**Pro tip:** Если планируется встраивание множества изображений в один документ, переиспользуйте один экземпляр `Document` и создавайте новые объекты `Image` только для каждой страницы. Это экономит накладные расходы на создание объектов.

---

## Шаг 4: Генерация PDF из изображения – сборка документа

Когда изображение готово, мы создаём новый PDF‑документ, добавляем страницу и размещаем изображение на ней. Коллекция `Paragraphs` в Aspose делает это тривиальным.

```csharp
    // Initialize a new PDF document
    Document pdfDoc = new Document();

    // Add a blank page to the document
    Page page = pdfDoc.Pages.Add();

    // Insert the image into the page's paragraph collection
    page.Paragraphs.Add(pdfImage);
```

Если необходимо позиционировать изображение (по центру, масштабировать и т.д.), можно обернуть его в `ImageStamp` или скорректировать `pdfImage.Margin`. Для большинства одно‑к‑одному конвертаций стандартное размещение работает отлично.

---

## Шаг 5: Сохранение результата – запись PDF на диск

Последний шаг — просто сохранить PDF‑файл. Aspose поддерживает множество форматов; здесь мы используем классический `.pdf`.

```csharp
    // Define the output path and save the PDF
    string outputPath = @"C:\Images\output.pdf";
    pdfDoc.Save(outputPath);
}
```

**Ожидаемый результат:** Открытие `output.pdf` в любом просмотрщике покажет оригинальное изображение HEIC в его нативном разрешении. Потери качества не будет, кроме исходного сжатия HEIC.

---

## Полный рабочий пример

Ниже представлен полностью готовая программа, которую можно скопировать в консольное приложение. В ней включены все директивы `using` и обработка ошибок для ощущения готового к продакшну кода.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using FileFormat.Heic.Decoder;

namespace HeicToPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath  = @"C:\Images\input.heic";
            string outputPath = @"C:\Images\output.pdf";

            try
            {
                // 1️⃣ Open the HEIC file as a stream
                using (FileStream heicStream = new FileStream(
                           inputPath, FileMode.Open, FileAccess.Read))
                {
                    // 2️⃣ Load the HEIC image from the stream
                    HeicImage heicImage = HeicImage.Load(heicStream);

                    // 3️⃣ Extract pixel data in RGB24 format
                    byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);
                    int width  = (int)heicImage.Width;
                    int height = (int)heicImage.Height;

                    // 4️⃣ Create an Aspose.Pdf.Image using the pixel data
                    Image pdfImage = new Image
                    {
                        BitmapInfo = new BitmapInfo(
                            pixelData,
                            width,
                            height,
                            BitmapInfo.PixelFormat.Rgb24)
                    };

                    // 5️⃣ Add the image to a new PDF page
                    Document pdfDoc = new Document();
                    Page page = pdfDoc.Pages.Add();
                    page.Paragraphs.Add(pdfImage);

                    // 6️⃣ Save the resulting PDF
                    pdfDoc.Save(outputPath);
                }

                Console.WriteLine($"✅ Success! PDF saved to: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Error: {ex.Message}");
            }
        }
    }
}
```

Запустите программу, и вы увидите сообщение в консоли, подтверждающее создание PDF. Откройте файл, и изображение должно выглядеть идентично оригинальному HEIC.

---

## Часто задаваемые вопросы и подводные камни

### Что делать, если файл HEIC повреждён?

Метод `HeicImage.Load` бросает `HeicException`. Оберните вызов в try/catch (как показано) и запишите ошибку в журнал. В продакшене можно переключиться на изображение‑заполнитель по умолчанию.

### Можно ли пакетно обрабатывать несколько файлов HEIC?

Конечно. Просто вынесите основную логику в метод, например `ConvertHeicToPdf(string input, string output)`, и пройдитесь по каталогу с помощью `Directory.GetFiles("*.heic")`.

### Сохраняет ли этот подход метаданные EXIF?

Нет, Aspose.Pdf автоматически не копирует EXIF‑данные в PDF. Если нужны метаданные, извлеките их через `HeicImage.Metadata` и добавьте в PDF с помощью свойств `Document.Info`.

### Как насчёт использования памяти при огромных изображениях?

Для изображений более 10 МП рекомендуется выполнить уменьшение разрешения перед созданием `BitmapInfo`. Можно воспользоваться `HeicImage.Resize` (если поддерживается) или сторонней библиотекой bitmap для снижения размеров.

---

## Заключение

Теперь вы знаете, как **создать PDF‑изображение** из источника HEIC, эффективно **конвертировать HEIC в PDF** и **добавлять изображение в PDF** с помощью Aspose.Pdf в C#. Шаги — чтение HEIC, извлечение пиксельных данных, обёртка их в PDF‑изображение и сохранение — просты, но достаточно мощны для производственных конвейеров.

Далее попробуйте расширить скрипт: генерировать много‑страничный PDF, где каждая страница содержит разный HEIC, или внедрять OCR‑текстовые слои для поисковых PDF. Вы также можете исследовать другие форматы изображений (`jpeg`, `png`) тем же шаблоном, укрепляя навык **генерации PDF из изображения**.

Не стесняйтесь экспериментировать, делиться результатами или задавать вопросы в комментариях. Счастливого кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом пособии. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как добавить заголовок‑изображение в PDF с помощью Aspose.PDF для .NET&#58; пошаговое руководство](/pdf/english/net/images-graphics/add-image-header-pdf-aspose-dotnet/)
- [Как добавить штамп‑изображение в PDF с помощью Aspose.PDF для .NET&#58; пошаговое руководство](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Как добавить штамп‑изображение в нижний колонтитул PDF с помощью Aspose.PDF .NET&#58; пошаговое руководство](/pdf/english/net/document-manipulation/add-image-stamp-pdf-footer-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}