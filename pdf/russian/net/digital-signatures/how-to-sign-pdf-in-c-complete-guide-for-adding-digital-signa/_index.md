---
category: general
date: 2026-04-12
description: Как подписать PDF с помощью Aspose.Pdf в C#. Узнайте, как добавить цифровую
  подпись в PDF, подписать PDF сертификатом и добавить подпись к PDF за несколько
  шагов.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- sign pdf with certificate
- append signature to pdf
- load pdf document c#
language: ru
og_description: Как подписать PDF с помощью Aspose.Pdf в C#. Этот учебник показывает,
  как добавить цифровую подпись в PDF, подписать PDF сертификатом и легко добавить
  подпись к PDF.
og_title: Как подписать PDF в C# — пошаговое руководство по цифровой подписи
tags:
- Aspose.Pdf
- C#
- Digital Signature
title: Как подписать PDF в C# – Полное руководство по добавлению цифровых подписей
url: /ru/net/digital-signatures/how-to-sign-pdf-in-c-complete-guide-for-adding-digital-signa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как подписать PDF в C# – Полное руководство по добавлению цифровых подписей

Когда‑нибудь задавались вопросом **как подписать PDF** файлы программно без открытия ридера? Возможно, вы создаёте систему выставления счетов и хотите, чтобы каждый PDF имел надёжную печать. Хорошая новость: это можно сделать полностью на C# с помощью Aspose.Pdf, и понадобится всего несколько строк кода. В этом руководстве мы пройдёмся по загрузке PDF‑документа, созданию отделённой подписи PKCS#7 и добавлению этой подписи на первую страницу. К концу вы точно будете знать, как добавить цифровую подпись в PDF‑файлы, подписать PDF сертификатом и даже работать с пользовательским хеш‑подписыванием.

Мы охватим всё, что вам нужно: необходимые пакеты NuGet, минимальный заглушка `MySigner` для пользовательского хеширования и полностью готовый пример. Никаких неопределённых «см. документацию» обходных путей — только автономное решение, которое можно вставить в любой .NET‑проект. Если вы уверенно владеете C# и у вас есть сертификат `.pfx`, вы полностью готовы.

## Предварительные требования – Что понадобится перед началом

- **.NET 6.0 или новее** – код компилируется как в .NET Core, так и в .NET Framework.  
- **Aspose.Pdf for .NET** пакет NuGet (`Aspose.Pdf` и `Aspose.Pdf.Facades`).  
  ```bash
  dotnet add package Aspose.Pdf
  dotnet add package Aspose.Pdf.Facades
  ```
- **Сертификат PKCS#12 (.pfx)**, содержащий закрытый ключ.  
  (Если у вас его нет, можно создать самоподписанный сертификат с помощью `MakeCert` или `OpenSSL` для тестов.)
- Базовое знакомство с **C# async/await** необязательно; пример работает синхронно для ясности.

> **Pro tip:** Храните файл сертификата вне корня веб‑приложения и защищайте пароль с помощью Azure Key Vault или переменных окружения.

Теперь давайте перейдём к реальным шагам.

## Шаг 1 – Загрузка PDF‑документа, который нужно подписать

Первое, что нужно сделать, — прочитать PDF‑файл в объект `Aspose.Pdf.Document`. Представьте это как открытие файла в памяти, готового к манипуляциям.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF you intend to sign
        string pdfPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");
        Document pdfDocument = new Document(pdfPath);
        // Rest of the workflow follows...
```

**Почему это важно:** Загрузка PDF является основой для операций **load pdf document c#**. Без корректного экземпляра `Document` вы не сможете получить доступ к страницам, добавить аннотации или внедрить подпись.

## Шаг 2 – Создание объекта PdfFileSignature

`PdfFileSignature` — это шлюз к функциям цифровой подписи. Он оборачивает документ и предоставляет метод `Sign`, который мы используем позже.

```csharp
        // 2️⃣ Initialize the signature helper
        PdfFileSignature pdfSignature = new PdfFileSignature(pdfDocument);
```

**Пояснение:** Класс `PdfFileSignature` обрабатывает низкоуровневые изменения PDF, такие как добавление нового объектного потока, содержащего подпись. Это рекомендованный способ **append signature to pdf** без повреждения исходного содержимого.

## Шаг 3 – Подготовка отделённой подписи PKCS#7

Отделённая подпись PKCS#7 хранит хеш документа отдельно от значения подписи. Это самый распространённый формат для цифровых подписей PDF и работает с большинством удостоверяющих центров.

```csharp
        // 3️⃣ Set up the PKCS#7 detached signature
        string certPath = Path.Combine("YOUR_DIRECTORY", "certificate.pfx");
        string certPassword = "yourPassword";

        PKCS7Detached pkcsSignature = new PKCS7Detached(certPath, certPassword)
        {
            // CustomSignHash lets you plug in your own cryptographic provider.
            // Here we call a static method on MySigner that you can replace.
            CustomSignHash = (hash, algorithm) => MySigner.Sign(hash)
        };
```

**Зачем нужен пользовательский делегат?** Во многих корпоративных средах закрытый ключ находится в HSM или Azure Key Vault. Предоставив `CustomSignHash`, вы можете передать фактическое подписывание любой внешней службе, пока Aspose занимается «трубопроводом» PDF. Если такая гибкость не нужна, просто опустите делегат, и Aspose использует закрытый ключ из `.pfx`.

### Минимальная заглушка `MySigner`

Ниже быстрый пример, использующий встроенную в .NET реализацию RSA. Замените её своей логикой при интеграции с аппаратным токеном.

```csharp
    public static class MySigner
    {
        public static byte[] Sign(byte[] hash)
        {
            // Load the private key from the same .pfx (for demo only)
            var cert = new System.Security.Cryptography.X509Certificates.X509Certificate2(
                Path.Combine("YOUR_DIRECTORY", "certificate.pfx"),
                "yourPassword",
                System.Security.Cryptography.X509Certificates.X509KeyStorageFlags.Exportable);

            using var rsa = cert.GetRSAPrivateKey();
            // Use SHA256 as an example; match the algorithm Aspose expects.
            return rsa.SignHash(hash, System.Security.Cryptography.HashAlgorithmName.SHA256,
                                 System.Security.Cryptography.RSASignaturePadding.Pkcs1);
        }
    }
```

> **Note:** В продакшене никогда не загружайте закрытый ключ напрямую из файла. Используйте защищённое хранилище.

## Шаг 4 – Определение места появления подписи

Подписи PDF могут быть невидимыми (отделёнными) или видимыми. Здесь мы создаём прямоугольник, который указывает рендереру, где отрисовать поле подписи. Настройте координаты под макет вашего документа.

```csharp
        // 4️⃣ Visible signature rectangle (lower‑left X, lower‑left Y, upper‑right X, upper‑right Y)
        Rectangle signatureRect = new Rectangle(100, 100, 200, 150);
```

Числа измеряются в пунктах (1/72 дюйма). Если вам нужна **add digital signature pdf**, появляющаяся внизу страницы, скорректируйте значения Y соответственно.

## Шаг 5 – Применение подписи к нужной странице

Наконец, мы просим Aspose внедрить подпись на страницу 1 и, при желании, *добавить* подпись к существующему PDF, а не перезаписать его.

```csharp
        // 5️⃣ Sign the first page and append the signature
        pdfSignature.Sign(pageNumber: 1, append: true, signatureRect, pkcsSignature);

        // Save the signed PDF
        string outputPath = Path.Combine("YOUR_DIRECTORY", "signed_output.pdf");
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ PDF signed successfully! Saved to {outputPath}");
    }
}
```

**Что происходит «под капотом»:**  
- `pageNumber: 1` – первая страница (страницы PDF нумеруются с 1).  
- `append: true` – сохраняет оригинальное содержимое и добавляет новую ревизию, что критично для аудита.  
- `signatureRect` – определяет визуальный виджет. Если задать прямоугольник нулевого размера, подпись станет невидимой, но всё равно удовлетворит требования **sign pdf with certificate**.

### Ожидаемый результат

Откройте `signed_output.pdf` в Adobe Acrobat Reader:

- Вы увидите видимое поле подписи в указанных координатах.  
- Панель подписи покажет детали сертификата (издатель, срок действия и т.д.).  
- История ревизий документа отобразит новое инкрементальное обновление, подтверждая успешное выполнение операции **append signature to pdf**.

## Общие варианты и особые случаи

### 1️⃣ Подписание нескольких страниц

Если нужно подписать каждую страницу (например, многостраничный контракт), пройдитесь по количеству страниц в цикле:

```csharp
for (int i = 1; i <= pdfDocument.Pages.Count; i++)
{
    pdfSignature.Sign(i, true, signatureRect, pkcsSignature);
}
```

### 2️⃣ Использование другого алгоритма хеширования

Aspose поддерживает SHA‑256, SHA‑384 и SHA‑512. Измените алгоритм, скорректировав делегат `CustomSignHash`:

```csharp
CustomSignHash = (hash, algorithm) => MySigner.Sign(hash, algorithm);
```

Затем адаптируйте `MySigner.Sign`, чтобы учитывать параметр `algorithm`.

### 3️⃣ Невидимая (отделённая) подпись

Если визуальный индикатор не нужен, передайте прямоугольник нулевого размера:

```csharp
Rectangle invisibleRect = new Rectangle(0, 0, 0, 0);
pdfSignature.Sign(1, true, invisibleRect, pkcsSignature);
```

PDF всё равно будет содержать криптографическую печать, удовлетворяя проверкам соответствия, требующим **sign pdf with certificate**.

### 4️⃣ Эффективная работа с большими PDF

Для PDF‑файлов более 100 МБ рассмотрите потоковую обработку документа вместо полной загрузки в память:

```csharp
using (FileStream fs = new FileStream(pdfPath, FileMode.Open, FileAccess.Read))
{
    Document largeDoc = new Document(fs);
    // Proceed with the same signing steps.
}
```

### 5️⃣ Программная проверка подписи

Aspose также предоставляет API для верификации:

```csharp
PdfFileSignatureVerifier verifier = new PdfFileSignatureVerifier(largeDoc);
bool isValid = verifier.VerifySignature(1);
Console.WriteLine(isValid ? "Signature is valid." : "Signature verification failed.");
```

## Полный рабочий пример (готовый к копированию)

Ниже представлен весь код программы в одном месте. Замените `YOUR_DIRECTORY`, `certificate.pfx` и пароль на свои реальные значения.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System;
using System.IO;

public static class MySigner
{
    public static byte[] Sign(byte[] hash)
    {
        var cert = new System.Security.Cryptography.X509Certificates.X509Certificate2(
            Path.Combine("YOUR_DIRECTORY", "certificate.pfx"),
            "yourPassword",
            System.Security.Cryptography.X509Certificates.X509KeyStorageFlags.Exportable);

        using var rsa = cert.GetRSAPrivateKey();
        return rsa.SignHash(hash, System.Security.Cryptography.HashAlgorithmName.SHA256,
                            System.Security.Cryptography.RSASignaturePadding.Pkcs1);
    }
}

class Program
{
    static void Main()
    {
        // Load PDF
        string pdfPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");
        Document pdfDocument = new Document(pdfPath);

        // Signature helper
        PdfFileSignature pdfSignature = new PdfFileSignature(pdfDocument);

        // PKCS#7 detached signature with custom signer
        string certPath = Path.Combine("YOUR_DIRECTORY", "certificate.pfx");
        string certPassword = "yourPassword";

        PKCS7Detached pkcsSignature = new PKCS7Detached(certPath, certPassword)
        {
            CustomSignHash = (hash, algorithm) => MySigner.Sign(hash)
        };

        // Visible rectangle (adjust as needed)
        Rectangle signatureRect = new Rectangle(100, 100, 200, 150);

        // Apply signature to first page, append mode
        pdfSignature.Sign(pageNumber: 1, append: true, signatureRect, pkcsSignature);

        // Save signed PDF
        string outputPath = Path.Combine("YOUR_DIRECTORY", "signed_output.pdf");
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ PDF signed successfully! Saved to {outputPath}");
    }
}
```

Запустите программу (`dotnet run`) — и у вас будет подписанный PDF, готовый к распространению.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}