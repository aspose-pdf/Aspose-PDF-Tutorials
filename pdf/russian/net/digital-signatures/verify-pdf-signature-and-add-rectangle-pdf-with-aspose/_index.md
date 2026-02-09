---
category: general
date: 2026-02-09
description: Проверьте подпись PDF с помощью Aspose.PDF в C#. Узнайте, как добавить
  прямоугольник в PDF, сохранить обновлённый PDF и использовать функции подписи Aspose
  PDF.
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: ru
og_description: быстро проверяйте подпись PDF в C#. Это руководство показывает, как
  добавить графику в PDF, сохранить обновлённый PDF и использовать API подписи Aspose
  PDF.
og_title: Проверка подписи PDF и добавление прямоугольника в PDF – Полное руководство
  Aspose
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: Проверка подписи PDF и добавление прямоугольника в PDF с помощью Aspose
url: /ru/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# проверка подписи PDF и добавление прямоугольника в PDF с помощью Aspose

Когда‑нибудь вам нужно было **verify pdf signature** в проекте C#, но вы не знали, с чего начать? Вы не одиноки — цифровые подписи являются обязательными для соответствия, однако многие разработчики сталкиваются с трудностями, когда им также нужно изменить документ после этого.  

В этом руководстве мы пройдем полный, исполняемый пример, который **verifies pdf signature**, добавляет **rectangle** на первую страницу, проверяет, что фигура находится внутри границ страницы, и в конце **save updated pdf** — всё с использованием современного API Aspose.PDF. К концу у вас будет единая, автономная программа, которую можно добавить в любое решение .NET.

## Что вы узнаете

- Загрузить подписанный PDF с помощью Aspose.PDF.
- Использовать классы **aspose pdf signature** для проверки каждой подписи и обнаружения компромиссов.
- **Add rectangle pdf** графику безопасно, гарантируя, что она помещается на страницу.
- **Save updated pdf**, сохраняя существующие подписи.
- Советы, обработка граничных случаев и распространённые подводные камни.

Внешняя документация не требуется — всё, что вам нужно, находится здесь.

## Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).
- Пакет NuGet Aspose.PDF для .NET (≥ 23.10). Установите с помощью:

```bash
dotnet add package Aspose.Pdf
```

- Подписанный PDF‑файл с именем `signed.pdf`, размещённый в папке, которой вы управляете (замените `YOUR_DIRECTORY` в коде).
- Базовое знакомство с C# и Visual Studio или VS Code.

> **Pro tip:** Если у вас нет под рукой подписанного PDF, Aspose предоставляет бесплатный демонстрационный файл на своём сайте, который вы можете скачать для тестирования.

---

## проверка подписи PDF – пошагово

Первое, что нам нужно сделать, — открыть документ и пройтись по каждой цифровой подписи. Aspose.PDF предоставляет два удобных метода: `VerifySignature` сообщает, прошла ли криптографическая проверка, а более новый `IsSignatureCompromised` отмечает любые изменения, которые могли произойти после подписания.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**Почему это важно:**  
- `VerifySignature` сам по себе лишь подтверждает, что сертификат подписанта всё ещё доверенный.  
- `IsSignatureCompromised` фиксирует тонкие изменения — например, добавление скрытого объекта — поэтому вы знаете, изменилось ли визуальное содержание PDF после подписи.

**Ожидаемый вывод** (пример с двумя подписями):

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

Если какая‑либо подпись сообщает `compromised=True`, следует прервать дальнейшую обработку или предупредить пользователя, поскольку целостность документа не может быть гарантирована.

---

## добавить прямоугольник в PDF на страницу

Теперь, когда мы убедились, что подписи целы (или, по крайней мере, знаем о любых компромисах), добавим простую графику‑прямоугольник. Это полезно для нанесения отметок «Reviewed», выделения разделов или просто привлечения внимания к области.

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**Что означают числа:**  
- Система координат PDF начинается в левом нижнем углу.  
- В примере прямоугольник имеет ширину 100 пунктов и высоту 100 пунктов, размещён примерно в центре типичной страницы A4.

> **Note:** Aspose также поддерживает `AddEllipse`, `AddPolygon` и т.д., если вам нужны более сложные формы.

---

## проверка границ графики – убедиться, что прямоугольник помещается

Прежде чем фиксировать изменения, разумно проверить, что наша графика остаётся внутри печатной области страницы. Новый метод `CheckGraphicsBounds` делает именно это.

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

Если `shapeFits` возвращает `false`, вам понадобится скорректировать координаты прямоугольника — возможно, уменьшить его или сместить ниже на странице. Это предотвращает случайное обрезание, которое может выглядеть непрофессионально, особенно при последующей печати PDF.

---

## сохранить обновлённый PDF – сохранить подписи и новую графику

Наконец, мы записываем изменённый документ обратно на диск. Метод `Save` сохраняет существующие подписи; он не аннулирует их, если только содержимое действительно не изменилось (что мы уже проверили с помощью `IsSignatureCompromised`).

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**Почему использовать новый файл?**  
Сохранение поверх оригинала может стереть исходные подписи, делая невозможным сравнение состояний «до» и «после». Записывая в `output.pdf`, вы сохраняете исходный файл для целей аудита.

---

## Полный, исполняемый пример

Ниже представлен полный код программы, который можно скопировать и вставить в консольное приложение. Все шаги объединены, комментарии объясняют каждый блок, и в конце вы увидите ожидаемый вывод в консоль.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**Ожидаемый вывод в консоль** (при одной действительной, некомпрометированной подписи):

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

Если подпись компрометирована, вы увидите `compromised=True` и сможете решить, продолжать ли работу.

---

## Часто задаваемые вопросы и обработка граничных случаев

| Вопрос | Ответ |
|----------|--------|
| **Что если в PDF нет подписей?** | `GetSignNames()` возвращает пустую коллекцию; цикл просто пропускает её, и вы всё равно можете добавить графику. |
| **Могу ли я добавить несколько прямоугольников?** | Да — просто вызывайте `AddRectangle` последовательно с разными объектами `Rectangle`. |
| **Что насчёт PDF, защищённых паролем?** | Загрузите их с помощью `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` перед проверкой. |
| **Приведёт ли добавление графики к аннулированию действительной подписи?** | Только если подпись охватывает страницу, где вы вставляете графику. Используйте `IsSignatureCompromised` для обнаружения этого; иначе подпись остаётся действительной. |
| **Нужно ли закрывать ресурсы?** | Объекты Aspose.PDF управляются автоматически; освобождение ресурсов необязательно, но вы можете обернуть код в блок `using` для дополнительной безопасности. |

---

## Профессиональные советы для продакшн

- **Batch processing:** Оберните всю процедуру в метод, принимающий пути ввода/вывода; затем передайте список файлов в `Parallel.ForEach` для ускорения.
- **Logging:** Замените `Console.WriteLine` на полноценный логгер (например, Serilog), чтобы фиксировать результаты проверки в аудиторских журналах.
- **Signature policy:** Сочетайте `VerifySignature` с проверкой отзыва сертификата (OCSP/CRL) для более строгого соответствия.
- **Graphics styling:** Используйте `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });`, чтобы выделить прямоугольник.
- **Version lock:** Зафиксируйте версию NuGet пакета Aspose.PDF, чтобы избежать несовместимых изменений при обновлении библиотеки.

---

## Заключение

Теперь у вас есть надёжный, сквозной пример, который **verify pdf signature**, **add rectangle pdf**, и **save updated pdf** с использованием последних API Aspose.PDF. Код проверяет наличие компрометированных подписей, гарантирует, что графика остаётся внутри границ страницы, и сохраняет оригинальные цифровые подписи — именно то, что требуется в реальном рабочем процессе соответствия.

Далее вы можете исследовать:

- Добавление **add graphics pdf**, например, водяных знаков или QR‑кодов.
- Использование API **aspose pdf signature** для программного создания новых подписей.
- Автоматизацию процесса в веб‑службе ASP.NET Core для проверки документов «на лету».

Попробуйте, измените координаты прямоугольника и посмотрите, как библиотека реагирует на разные структуры PDF. Приятного кодинга, и пусть ваши PDF остаются как подписанными, так и стильными! 

![verify pdf signature example](image.png "verify pdf signature example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}