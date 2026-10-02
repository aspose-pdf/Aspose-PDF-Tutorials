---
category: general
date: 2026-03-29
description: Как подписать PDF цифровой подписью и добавить обрезанное изображение
  в C#. Узнайте, как добавить цифровую подпись в PDF, обрезать изображение для PDF
  и легко вставить изображение в PDF.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: ru
og_description: Как подписать PDF цифровой подписью и вставить обрезанное изображение
  с помощью Aspose.Pdf в C#. Следуйте этому руководству для полного решения.
og_title: Как подписать PDF и добавить изображения – пошаговое руководство на C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Как подписать PDF и добавить изображения – полное руководство по C#
url: /ru/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как подписать PDF и добавить изображения – Полное руководство на C#

Когда‑нибудь задавались вопросом, **как подписать PDF** файлы программно, одновременно вставляя пользовательскую картинку? Возможно, вы создаёте процесс согласования и вам нужна юридически обязательная подпись *и* миниатюра фотографии подписанта на той же странице. Короче говоря, вы хотите **add digital signature pdf** контент, обрезать эту картинку и затем **add image to pdf** без усилий.  

Этот учебник проведёт вас через каждый шаг — от загрузки сертификата ECDSA PKCS#7 до обрезки JPEG и наложения его на подписанную страницу. К концу у вас будет один исполняемый файл C#, который подписывает страницу 1, обрезает фото до 400 × 400 px и размещает его в точном месте. Никаких внешних скриптов, никакой магии, только понятный код и объяснения.

## Prerequisites

- .NET 6.0 или новее (код также работает с .NET Framework 4.7+)
- **Aspose.Pdf for .NET** пакет NuGet (версия 23.9 или новее)
- Сертификат ECDSA P‑256 в формате PKCS#7 (`.pfx`) и его пароль
- JPEG‑изображение, которое вы хотите встроить (например, `photo.jpg`)

> **Pro tip:** Держите файл сертификата вне системы контроля версий и защищайте пароль с помощью менеджера секретов.

---

## Step 1: Set Up the Project and Imports

Сначала создайте консольное приложение (или интегрируйте это в любой существующий сервис). Добавьте ссылку на Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Затем подключите необходимые пространства имён:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

Эти `using`‑операторы дают вам доступ к классам `Document`, `Signature` и `Rectangle`, которые понадобятся позже.

## Step 2: Load the PDF and Prepare the Signature

Откроем существующий PDF (`source.pdf`) и создадим объект **digital signature pdf**, использующий отделённую подпись PKCS#7. Сертификат — ключ ECDSA P‑256, который широко принимается для соответствия требованиям.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Почему это важно:** Использование отделённой подписи PKCS#7 сохраняет оригинальное содержимое PDF, одновременно встраивая криптографический хеш. Это отраслевой стандарт для юридически обязательных PDF‑файлов.

## Step 3: Apply the Digital Signature to a Specific Page

Теперь разместим видимое поле подписи на **странице 1**. Прямоугольник определяет, где появится коробка подписи (координаты указаны в пунктах, где 1 дюйм = 72 пункта).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

Если вам не нужна видимая коробка, установите `isVisible` в `false`. `signatureRect` можно скорректировать под макет вашего документа.

## Step 4: Open the Image Stream and Define Crop Areas

Прочитаем JPEG‑файл в поток и укажем **исходный прямоугольник**, выбирающий левый верхний угол 400 × 400 пикселей. Это операция **crop image for pdf**.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Edge case:** Если ваше изображение меньше 400 × 400, обрезка автоматически ограничится реальными размерами изображения — исключение не будет выброшено.

## Step 5: Define Where the Cropped Image Should Appear

Далее задаём **целевой прямоугольник** на странице PDF. В этом примере мы размещаем изображение в точке (50, 50) размером 200 × 200 пунктов (≈2,78 дюйма квадрат).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

Экспериментируйте: меняйте координаты X/Y, чтобы переместить картинку, или изменяйте ширину/высоту для масштабирования.

## Step 6: Insert the Cropped Image onto the Signed Page

Наконец, добавляем изображение на **страницу 1** (ту же страницу, где уже есть подпись). Перегрузка `AddImage`, которую мы используем, принимает исходный и целевой прямоугольники, эффективно выполняя обрезку и размещение за один вызов.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

За кулисами Aspose.Pdf извлекает область 400 × 400 пикселей, масштабирует её до 200 × 200 пунктов и записывает в поток содержимого PDF.

## Step 7: Save the Signed and Image‑Enhanced PDF

После всех изменений сохраняем документ. Можно перезаписать оригинал или записать в новый файл.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

Когда откроете `output_signed.pdf` в Adobe Acrobat или любом PDF‑просмотрщике, вы увидите:

- Видимое поле подписи в указанных координатах.
- Обрезанную фотографию, размещённую в (50, 50) на странице 1.
- Проверенную цифровую подпись (при условии, что просмотрщик доверяет вашему сертификату).

## Frequently Asked Questions (FAQ)

| Вопрос | Ответ |
|----------|--------|
| **Можно ли подписать другую страницу?** | Измените аргумент `pageNumber` в `signature.Sign` на любой допустимый номер страницы (нумерация начинается с 1). |
| **Что делать, если нужны несколько подписей?** | Создайте новый экземпляр `Signature` для каждой страницы или места, повторно используя тот же `pkcsSignature`, если применяется один и тот же сертификат. |
| **Ограничена ли обрезка изображения только прямоугольниками?** | Да, `AddImage` в Aspose.Pdf работает только с прямоугольными областями. Для сложных форм нужно предварительно обработать изображение (например, с помощью System.Drawing) перед встраиванием. |
| **Как сделать подпись невидимой?** | Установите `isVisible` в `false` и опустите `signatureRect`. Подпись останется криптографически валидной. |
| **Какие форматы можно встраивать помимо JPEG?** | Поддерживаются PNG, BMP, GIF и TIFF. Просто измените путь к файлу и убедитесь, что поток читает правильные байты. |

## Full Working Example

Ниже приведена полностью самодостаточная программа. Скопируйте её в `Program.cs`, скорректируйте пути и запустите.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Ожидаемый результат:** При открытии `output_signed.pdf` вы увидите поле подписи (100 × 100 → 300 × 300 пунктов) и изображение размером 200 × 200 пунктов, полученное из левого верхнего угла `photo.jpg`. Подпись проходит проверку с использованием предоставленного сертификата ECDSA.

## Wrapping Up

Мы рассмотрели **how to sign PDF** файлы, как **add digital signature pdf** на конкретную страницу, как **crop image for pdf**, и наконец как **add image to pdf** с помощью Aspose.Pdf в C#. Весь процесс — от загрузки сертификата до сохранения финального документа — умещается в один легко читаемый исходный файл.

Если вы готовы к следующему вызову, подумайте о:

- Добавлении **multiple signatures** на разные страницы (используйте концепцию “digital signature pdf page”).
- Встраивании **QR‑кодов**, которые ссылаются на сервисы верификации.
- Автоматизации процесса в ASP.NET Core API для генерации PDF «на лету».

Помните, ключ к надёжной автоматизации PDF — чёткое разделение обязанностей: обработка подписи, работа с изображениями и финальная сборка документа. Играйте с координатами, меняйте формат изображения или экспериментируйте с отметкой времени — ваш рабочий процесс теперь полностью расширяем.

Есть вопросы, крайние случаи или интересный кейс, которым хотите поделиться? Оставляйте комментарий ниже, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}