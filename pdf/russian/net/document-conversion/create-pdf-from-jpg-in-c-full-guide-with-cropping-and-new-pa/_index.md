---
category: general
date: 2026-04-06
description: Быстро создавайте PDF из JPG и узнайте, как обрезать изображение в PDF,
  добавить новую страницу PDF и конвертировать JPG в PDF с обрезкой с помощью C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: ru
og_description: Создайте PDF из JPG и обрежьте изображение в PDF с помощью C#. Узнайте,
  как добавить новую страницу PDF и преобразовать JPG в PDF с обрезкой.
og_title: Создание PDF из JPG в C# – пошаговое руководство
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Создание PDF из JPG в C# – Полное руководство с обрезкой и новыми страницами
url: /ru/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF из JPG в C# – Полное руководство с обрезкой и новыми страницами

Когда‑нибудь вам нужно было **create PDF from JPG**, но вы не были уверены, как оставить только нужную часть? Вы не одиноки. Во многих приложениях — подумайте о счетах‑фактурах, чеках или фотокнигах — разработчики должны превратить изображение в PDF, отбрасывая ненужные края.  

В этом руководстве мы пройдем полный, готовый к запуску пример, который **creates PDF from JPG**, показывает, как **crop image in PDF**, и демонстрирует **how to add new pdf page**, когда требуется более одной картинки. К концу вы также узнаете, как **convert JPG to PDF with crop** и **insert image into PDF C#** с использованием библиотеки Aspose.Pdf.

## Что вы узнаете

- Настроить Aspose.Pdf в .NET‑проекте (без сложной конфигурации).  
- Загрузить JPEG, определить область, которую нужно оставить, и обрезать её при вставке на страницу PDF.  
- Добавить дополнительные страницы в тот же документ, позволяя создавать много‑страничные PDF из множества изображений.  
- Сохранить итоговый файл и проверить результат.  

**Prerequisites:** .NET 6+ (или .NET Framework 4.6+), Visual Studio 2022 или любой другой редактор, и ссылка NuGet на `Aspose.Pdf`. Другие внешние сервисы не требуются.

![Create PDF from JPG example](image.jpg){: .align-center alt="Пример создания PDF из JPG, показывающий обрезанное изображение, размещённое на странице PDF"}

---

## Шаг 1: Установить Aspose.Pdf и подготовить проект

Для начала добавьте пакет Aspose.Pdf. Откройте терминал в папке решения и выполните:

```bash
dotnet add package Aspose.Pdf
```

Эта единственная строка подтягивает всё необходимое: классы `Document`, `Rectangle` и `Page`, которые мы будем использовать позже. По моему опыту, способ через NuGet — самый простой способ оставаться в актуальном состоянии без возни с DLL.

> **Pro tip:** Если вы нацелены на .NET Framework, используйте пакет `Aspose.Pdf.NET`; API идентичен.

---

## Шаг 2: Загрузить JPEG и задать размер страницы

Нужен холст, соответствующий размерам, которые мы хотим для финальной страницы PDF. Ниже приведён код, создающий новый `Document` и открывающий исходное изображение как поток.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Зачем прямоугольник? В Aspose.Pdf `Rectangle` представляет как размеры страницы, так и область изображения, которую вы хотите отобразить. Разделяя *страницу* и *область обрезки*, вы получаете точный контроль над тем, что окажется в PDF.

---

## Шаг 3: Выбрать область обрезки (верхний‑левый квартал)

Предположим, вам нужен только верхний‑левый квартал фотографии. Мы вычисляем эту область относительно размеров страницы:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

`Rectangle` конструктор принимает значения **нижний‑левый X/Y** и **верхний‑правый X/Y**. Добавив половину высоты к `LLY`, мы сдвигаем нижнюю границу обрезки вверх, эффективно отбрасывая нижнюю половину изображения. При необходимости скорректируйте эти расчёты для другой части.

> **Why crop before adding?**  
> Обрезка на стороне PDF избавляет от создания временного bitmap‑файла на диске, экономя как ввод‑вывод, так и память. Aspose выполняет вычисления за вас, и результат — чистый PDF, дружелюбный к векторам.

---

## Шаг 4: Добавить новую страницу и вставить обрезанное изображение

Теперь мы действительно размещаем изображение на странице PDF. Здесь ключевое слово **how to add new pdf page** проявляет свою силу.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` принимает три аргумента:

1. **Stream** — исходный JPEG.  
2. **Page rectangle** — определяет размер страницы (наш `pageBounds`).  
3. **Crop rectangle** — указывает Aspose, какую часть изображения отобразить.

Если нужны дополнительные страницы, просто повторите шаблон `Add` + `AddImage` с новым `imageStream` каждый раз. Это удовлетворяет требованию **how to add new pdf page**, сохраняя код аккуратным.

---

## Шаг 5: Сохранить PDF и проверить результат

Последний шаг — однострочник, но не недооценивайте его — сохранение по правильному пути гарантирует, что файл откроется в любом PDF‑просмотрщике.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

Когда вы откроете `cropped_image.pdf`, вы должны увидеть одну страницу, содержащую только верхний‑левый квартал оригинального JPEG, идеально центрированный на странице размером 600 × 800.

---

## Полный рабочий пример (все шаги вместе)

Ниже полная программа, которую можно скопировать и вставить в консольное приложение. Она компилируется как есть, при условии, что вы установили Aspose.Pdf и разместили JPEG по указанному пути.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Ожидаемый результат

- **File:** `cropped_image.pdf` (≈ 30 KB).  
- **Content:** Одна страница, 600 × 800 пунктов, показывающая верхний‑левый квартал `photo.jpg`.  
- **Behavior:** Без искажений; изображение сохраняет исходное разрешение в пределах обрезанных границ.

---

## Часто задаваемые вопросы и особые случаи

### Что если нужно сохранить всё изображение, а не только квартал?

Просто установите `cropArea` равным `pageBounds`:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### Можно ли использовать другой размер страницы (например, A4)?

Конечно. Замените значения `pageBounds` на размеры страницы A4 в пунктах (595 × 842):

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

Прямоугольник обрезки может оставаться тем же или быть пересчитанным, чтобы соответствовать новому соотношению сторон.

### Как добавить несколько изображений, каждое на своей странице?

Пройдитесь по коллекции путей к файлам:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### Что насчёт прозрачности или PNG‑изображений?

Aspose.Pdf обрабатывает PNG так же, как JPEG. Если источник имеет альфа‑канал, PDF сохранит его, при условии, что версия PDF поддерживает прозрачность (по умолчанию поддерживается).

### Работает ли это на .NET Core в Linux?

Да. Aspose.Pdf кросс‑платформенный; просто убедитесь, что `imageStream` указывает на действительный путь к файлу в целевой ОС. Windows‑специфичные API не используются.

## Советы и лучшие практики

- **Memory Management:** Всегда оборачивайте потоки в конструкции `using` (как показано), чтобы избежать блокировок файлов.  
- **Performance:** Если вы обрабатываете десятки изображений, рассмотрите возможность повторного использования одного экземпляра `Document` и вызова `pdfDocument.Pages.Add()` для каждого изображения.  
- **Error Handling:** Оберните всю процедуру в блок `try/catch` и логируйте `PdfException` для отладки.  
- **Quality Control:** Aspose.Pdf позволяет задавать разрешение изображения через `ImageFragment`. Для сканов с высоким DPI установите `ImageFragment.Resolution = 300;`.  
- **Security:** Если PDF будет распространяться внешне, вы можете добавить шифрование с помощью `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

## Заключение

Мы только что рассмотрели, как **create PDF from JPG** в C#, **crop image in PDF** и **add new PDF page** для создания много‑страничных документов. Та же схема позволяет **convert JPG to PDF with crop** и **insert image into PDF C#** в любой ситуации — от простых чеков до сложных фотокниг.  

Попробуйте: измените логику обрезки, поэкспериментируйте с страницами A4 или соедините несколько изображений подряд. Библиотека Aspose.Pdf делает эти задачи простыми, а приведённый выше код — надёжным, пригодным для цитирования примером, который можно вставить в любой проект.

### Что дальше?

- **Add text annotations** к PDF (например, подписи под каждым изображением).  
- **Create a table of contents** автоматически для много‑страничных PDF.  
- **Merge multiple PDFs** с помощью `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

Каждая из этих тем опирается на основы, которые вы только что освоили, поэтому вы хорошо подготовлены к их изучению

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}