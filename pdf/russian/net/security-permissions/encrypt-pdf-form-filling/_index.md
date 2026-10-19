---
title: Зашифровать PDF, разрешив только заполнение форм, с помощью Aspose.Pdf for .NET
weight: 101
limit:
description: Узнайте, как зашифровать PDF с помощью AES‑256, задать пароли и ограничить разрешения только заполнением форм, используя Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, encrypt PDF, PDF form filling permissions, AES-256 PDF encryption, viewer password PDF, owner password PDF]
url: /net/security-permissions/encrypt-pdf-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Узнайте, как зашифровать PDF с помощью AES‑256, задать пароли и ограничить
    разрешения только заполнением форм, используя Aspose.Pdf for .NET.
  headline: Зашифровать PDF, разрешив только заполнение форм, с помощью Aspose.Pdf
    for .NET
  type: TechArticle
- description: Узнайте, как зашифровать PDF с помощью AES‑256, задать пароли и ограничить
    разрешения только заполнением форм, используя Aspose.Pdf for .NET.
  name: Зашифровать PDF, разрешив только заполнение форм, с помощью Aspose.Pdf for
    .NET
  steps:
  - name: Определите пути к исходному и целевому файлам, а также пароли просмотра
      и владельца.
    text: Определите пути к исходному и целевому файлам, а также пароли просмотра
      и владельца.
  - name: Проверьте, существует ли исходный PDF, и при его отсутствии завершите работу
      с сообщением об ошибке.
    text: Проверьте, существует ли исходный PDF, и при его отсутствии завершите работу
      с сообщением об ошибке.
  - name: Начните блок try, чтобы обработать любые ошибки, которые могут возникнуть
      во время обработки.
    text: Начните блок try, чтобы обработать любые ошибки, которые могут возникнуть
      во время обработки.
  - name: Откройте существующий PDF-файл, создав объект Document с именем pdfDoc.
    text: Откройте существующий PDF-файл, создав объект Document с именем pdfDoc.
  - name: Установите разрешения, позволяющие только заполнение форм, зашифруйте документ
      паролями просмотра и владельца с использованием AES‑256 и сохраните защищённый
      PDF.
    text: Установите разрешения, позволяющие только заполнение форм, зашифруйте документ
      паролями просмотра и владельца с использованием AES‑256 и сохраните защищённый
      PDF.
  - name: Выведите сообщение подтверждения в консоль и закройте блок try.
    text: Выведите сообщение подтверждения в консоль и закройте блок try.
  - name: Перехватите любые исключения и выведите сообщение об ошибке в консоль.
    text: Перехватите любые исключения и выведите сообщение об ошибке в консоль.
  type: HowTo
- questions:
  - answer: При открытии паролем просмотра (пользователя) документ можно просматривать
      и заполнять поля форм, но все остальные действия, такие как редактирование текста,
      добавление аннотаций или извлечение содержимого, заблокированы.
    question: Что пользователь может делать с PDF после его шифрования с помощью `Permissions.FillForm`?
  - answer: Объедините разрешения с помощью побитового оператора OR, например, `Permissions
      allowed = Permissions.FillForm | Permissions.Printing;` и передайте полученное
      значение в `pdfDoc.Encrypt`.
    question: Как я могу разрешить дополнительные права, например печать, при этом
      оставив все остальные ограничения?
  - answer: Да. Первый аргумент — пароль пользователя (просмотра), который предоставляет
      ограниченные права, а второй аргумент — пароль владельца (администратора), который
      обеспечивает полный контроль над документом.
    question: Имеет ли значение порядок паролей в `pdfDoc.Encrypt(viewerPass, adminPass,
      …)`?
  - answer: Aspose.Pdf выбросит исключение при попытке открыть уже зашифрованный файл;
      сначала необходимо открыть его с использованием существующего пароля, удалить
      или изменить защиту, а затем применить новые настройки шифрования.
    question: Что происходит, если исходный PDF уже защищён паролем?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-form-filling/og-image.png
og_title: Зашифровать PDF и разрешить только заполнение форм
og_description: Защитите ваш PDF с помощью AES‑256 и позвольте пользователям заполнять формы, но ничего более.
og_image_alt: Скриншот, показывающий код Aspose.Pdf for .NET, который шифрует PDF и ограничивает его только заполнением форм
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Зашифровать PDF, разрешив только заполнение форм, с помощью Aspose.Pdf
В этом учебном материале вы узнаете, как открыть существующий PDF с помощью Aspose.Pdf for .NET, применить шифрование AES‑256, задать пароли просмотра и владельца и ограничить разрешения документа так, чтобы получатели могли только заполнять поля форм. Такой подход полезен, когда необходимо защитить содержимое, но при этом позволить пользователям заполнять интерактивные формы. Код пошагово демонстрирует каждый этап и сохраняет защищённый PDF, готовый к распространению.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-form-filling" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Что пользователь может делать с PDF после его шифрования с помощью `Permissions.FillForm`?**  
A: При открытии паролем просмотра (пользователя) документ можно просматривать и заполнять поля форм, но все остальные действия, такие как редактирование текста, добавление аннотаций или извлечение содержимого, заблокированы.

**Q: Как я могу разрешить дополнительные права, например печать, при этом оставив все остальные ограничения?**  
A: Объедините разрешения с помощью побитового оператора OR, например, `Permissions allowed = Permissions.FillForm | Permissions.Printing;` и передайте полученное значение в `pdfDoc.Encrypt`.

**Q: Имеет ли значение порядок паролей в `pdfDoc.Encrypt(viewerPass, adminPass, …)`?**  
A: Да. Первый аргумент — пароль пользователя (просмотра), который предоставляет ограниченные права, а второй аргумент — пароль владельца (администратора), который обеспечивает полный контроль над документом.

**Q: Что происходит, если исходный PDF уже защищён паролем?**  
A: Aspose.Pdf выбросит исключение при попытке открыть уже зашифрованный файл; сначала необходимо открыть его с использованием существующего пароля, удалить или изменить защиту, а затем применить новые настройки шифрования.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}