---
category: general
date: 2026-06-08
description: Обрезать изображение в PDF с помощью Aspose.PDF на C#. Узнайте, как создать
  PDF с изображением, сохранить PDF с изображением и добавить изображение в PDF всего
  за несколько строк кода.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: ru
og_description: Обрезать изображение в PDF с помощью Aspose.PDF на C#. Этот учебник
  показывает, как создать PDF с изображением, сохранить PDF с изображением и быстро
  добавить изображение в PDF.
og_title: Обрезка изображения в PDF с помощью Aspose.PDF – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Обрезка изображения в PDF с помощью Aspose.PDF – Полное руководство
url: /ru/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Обрезка изображения в PDF с помощью Aspose.PDF – Полное руководство

Вы когда‑нибудь задумывались, как **обрезать изображение в PDF** без использования графического редактора? Вы не одиноки. Во многих отчетах, счетах‑фактурах или электронных книгах вам нужен лишь кусок изображения — возможно, угол логотипа или фрагмент диаграммы — и вы хотите разместить его непосредственно в PDF.  

В этом руководстве мы покажем, как именно это сделать: мы **создадим PDF с изображением**, **добавим изображение в PDF**, а затем **обрежем изображение в PDF**, используя библиотеку Aspose.PDF для C#. В конце вы также узнаете, как **сохранить PDF с изображением**, чтобы отправить файл кому угодно.

---

## Что понадобится

- .NET 6.0 или новее (код также работает с .NET Framework 4.6+).  
- Лицензированная или пробная копия **Aspose.PDF for .NET** (установить через NuGet `Install-Package Aspose.PDF`).  
- Файл изображения (JPEG/PNG) на диске — будем называть его `image.jpg`.  
- Любая удобная IDE (Visual Studio, Rider, VS Code).

Вот и всё. Никаких дополнительных сервисов, никаких внешних инструментов.

---

## Шаг 1: Настройка проекта и импортов

Сначала создайте консольное приложение и подключите пространства имён, которые будем использовать. Операторы `using` делают код аккуратным и упрощают чтение последующих шагов.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Полезный совет:** Если вы используете Visual Studio, щёлкните правой кнопкой мыши по проекту → *Manage NuGet Packages* → найдите “Aspose.PDF” и установите. Библиотека обрабатывает как размещение изображения, так и его обрезку внутри, поэтому сторонние библиотеки для работы с изображениями не потребуются.

---

## Шаг 2: Создание PDF с изображением

Теперь мы действительно **создаём PDF с изображением**. Приведённый ниже фрагмент кода создаёт новый `Document`, добавляет пустую страницу и подготавливает поток изображения.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Выполнение этого кода создаст PDF, в котором всё изображение растянуто до указанных вами размеров. Это хороший способ убедиться в корректности перед тем, как начинать обрезку.

---

## Шаг 3: Как добавить изображение в PDF (и подготовить к обрезке)

Если вы уже знаете точный регион, который нужен, можете пропустить шаг с полным изображением и перейти сразу к части **как добавить изображение в PDF**. Метод `AddImage` принимает три параметра:

1. **Поток изображения** — необработанные байты вашего рисунка.  
2. **Прямоугольник размещения** — где на странице будет находиться изображение.  
3. **Прямоугольник обрезки** — часть изображения, которую вы действительно хотите отобразить.

Ниже представлена компактная версия, которая выполняет как размещение, **так и** обрезку в одном вызове.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Почему это работает:** Aspose.PDF внутренне сопоставляет прямоугольник обрезки с пиксельными размерами изображения, а затем рендерит только этот фрагмент внутри области `placement`. Дополнительная обработка битмапов не требуется, что позволяет сохранять небольшой размер PDF.

---

## Шаг 4: Как обрезать изображение в PDF — расширенные параметры

Иногда обрезка четверти недостаточна. Возможно, нужен пользовательский прямоугольник или вы хотите сохранить соотношение сторон изображения. Вот более гибкий подход:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Обработка крайних случаев:**  
- **Null‑потоки** — всегда оборачивайте `FileStream` в блок `using`, как показано, чтобы избежать утечек.  
- **Большие изображения** — если исходное изображение огромно, рассмотрите возможность уменьшения `placement`‑прямоугольника; Aspose автоматически выполнит даунсемплинг.  
- **Прозрачные PNG** — библиотека сохраняет альфа‑каналы, поэтому обрезанная область сохранит прозрачность.

---

## Шаг 5: Сохранение PDF с изображением (и проверка)

Наконец, мы **сохраняем PDF с изображением**. Метод `Save` записывает документ на диск. При необходимости вы также можете отправить его в виде потока веб‑клиенту, если разрабатываете API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

Когда вы откроете `output.pdf`, вы увидите только обрезанную часть `image.jpg`, расположенную точно там, где вы её задали. Если изображение выглядит растянутым, скорректируйте ширину/высоту `placement`‑прямоугольника, чтобы они соответствовали соотношению сторон прямоугольника обрезки.

---

## Часто задаваемые вопросы и подводные камни

| Question | Answer |
|----------|--------|
| **Можно ли обрезать несколько изображений на одной странице?** | Конечно. Вызывайте `page.AddImage` для каждого изображения, задавая свои прямоугольники размещения и обрезки. |
| **Что если моё изображение в другом формате (например, BMP)?** | Aspose.PDF поддерживает JPEG, PNG, BMP, GIF и TIFF «из коробки». Просто измените расширение файла. |
| **Нужна ли лицензия для использования в продакшене?** | Пробная версия работает до 5 страниц. Для реального развертывания приобретите лицензию, чтобы убрать водяной знак. |
| **Как повернуть обрезанное изображение?** | После добавления изображения получите объект `Image` и задайте его свойство `Rotate` (`Rotate = RotationAngle.Rotate90`). |
| **Можно ли обрезать с использованием процентов вместо абсолютных точек?** | Да — вычислите размеры прямоугольника на основе, например, `image.Width * 0.25` и затем преобразуйте их в пункты, как показано в Шаге 4. |

---

## Полный рабочий пример (готов к копированию и вставке)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Запустите программу, откройте `output.pdf`, и вы увидите только верхний‑левый квартал `image.jpg`, отрисованный в верхнем‑левом углу страницы. Изменяйте значения прямоугольника `crop`, чтобы поэкспериментировать с различными фрагментами.

---

## Заключение

Мы прошли весь процесс **обрезки изображения в PDF** с использованием Aspose.PDF для C#. Начиная с нового документа, мы **создаём PDF с изображением**, демонстрируем **как добавить изображение в PDF**, применяем пользовательский прямоугольник **как обрезать изображение в PDF**, и, наконец, **сохраняем PDF с изображением**.  

Теперь вы можете встраивать точно обрезанные изображения в любой генерируемый PDF — идеально для счетов, маркетинговых брошюр или автоматических отчётов. Далее можно добавить текстовые подписи (`TextFragment`) или нарисовать фигуры вокруг обрезанного изображения, чтобы выделить его.  

Есть другие сценарии, которые вас интересуют? Оставьте комментарий, и удачной разработки!

---

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, опирающиеся на техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как задать размер изображения в PDF с помощью Aspose.PDF для .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Как добавить штамп‑изображение в PDF с помощью Aspose.PDF для .NET: Полное руководство](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Как извлечь информацию об изображениях из PDF с помощью Aspose.PDF для .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}