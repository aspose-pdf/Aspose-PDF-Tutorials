---
title: Зашифровать PDF только для заполнения форм с помощью AES‑256, используя Aspose.Pdf for .NET
weight: 201
limit:
description: Узнайте, как зашифровать PDF с помощью AES‑256, ограничить его только заполнением форм и установить пароли для просмотра/владельца, используя Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, PDF encryption .NET, restrict PDF permissions, form filling permission PDF, AES-256 PDF encryption, set PDF passwords .NET]
url: /net/security-permissions/encrypt-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Узнайте, как зашифровать PDF с помощью AES‑256, ограничить его только
    заполнением форм и установить пароли для просмотра/владельца, используя Aspose.Pdf
    for .NET.
  headline: Зашифровать PDF только для заполнения форм с помощью AES‑256, используя
    Aspose.Pdf for .NET
  type: TechArticle
- description: Узнайте, как зашифровать PDF с помощью AES‑256, ограничить его только
    заполнением форм и установить пароли для просмотра/владельца, используя Aspose.Pdf
    for .NET.
  name: Зашифровать PDF только для заполнения форм с помощью AES‑256, используя Aspose.Pdf
    for .NET
  steps:
  - name: Объявите путь к исходному PDF, путь к выходному файлу и пароли для просмотра
      и владельца.
    text: Объявите путь к исходному PDF, путь к выходному файлу и пароли для просмотра
      и владельца.
  - name: Проверьте, существует ли исходный файл; если нет, выведите сообщение об
      ошибке и завершите работу.
    text: Проверьте, существует ли исходный файл; если нет, выведите сообщение об
      ошибке и завершите работу.
  - name: Войдите в блок try и откройте PDF‑документ с помощью инструкции `using`,
      создав переменную `pdfDoc`.
    text: Войдите в блок try и откройте PDF‑документ с помощью инструкции `using`,
      создав переменную `pdfDoc`.
  - name: Создайте объект `Permissions`, который позволяет только заполнение форм.
    text: Создайте объект `Permissions`, который позволяет только заполнение форм.
  - name: Зашифруйте `pdfDoc` с помощью паролей просмотра и владельца, применив набор
      разрешений и используя AES‑256.
    text: Зашифруйте `pdfDoc` с помощью паролей просмотра и владельца, применив набор
      разрешений и используя AES‑256.
  - name: Сохраните зашифрованный PDF в указанный выходной файл и закройте блок `using`.
    text: Сохраните зашифрованный PDF в указанный выходной файл и закройте блок `using`.
  - name: Выведите сообщение подтверждения в консоль и закройте блок try.
    text: Выведите сообщение подтверждения в консоль и закройте блок try.
  - name: Перехватите любое исключение, выведите его сообщение в поток ошибок и закройте
      блок catch.
    text: Перехватите любое исключение, выведите его сообщение в поток ошибок и закройте
      блок catch.
  type: HowTo
- questions:
  - answer: '`Permissions.FillForm` позволяет пользователям заполнять интерактивные
      поля формы, но отключает все остальные действия, такие как печать, извлечение
      содержимого или изменение структуры документа.'
    question: Что именно разрешает и блокирует флаг `Permissions.FillForm` в зашифрованном
      PDF?
  - answer: Да, замените `CryptoAlgorithm.AESx256` на `CryptoAlgorithm.AESx128` (или
      другое поддерживаемое значение перечисления) в методе `pdfDoc.Encrypt`, чтобы
      изменить уровень шифрования.
    question: Могу ли я использовать другой алгоритм шифрования, например AES‑128,
      с тем же вызовом `Encrypt`?
  - answer: Пароль для просмотра (`readPass`) необходим для открытия PDF и применения
      указанных разрешений, тогда как пароль владельца (`fullPass`) предоставляет
      полный неограниченный доступ и может использоваться для изменения разрешений
      или снятия шифрования.
    question: В чём разница между паролем для просмотра (`viewerPwd`) и паролем владельца
      (`masterPwd`)?
  - answer: 'Передача `Permissions.None` (или отсутствие аргумента) приводит к PDF
      без специальных ограничений: пароль для просмотра по‑прежнему защищает файл,
      но пользователи могут выполнять все стандартные действия, такие как печать и
      копирование.'
    question: Если я опущу аргумент `permissionSet` или передам `Permissions.None`,
      какие разрешения будет иметь PDF после шифрования?
  type: FAQPage
images:
- /net/security-permissions/encrypt-form-filling/og-image.png
og_title: Зашифровать PDF только для заполнения форм с AES‑256
og_description: Защитите ваш PDF, чтобы пользователи могли только заполнять формы, используя шифрование AES‑256 и пароли в Aspose.Pdf for .NET.
og_image_alt: Скриншот, показывающий шаги по шифрованию PDF и ограничению его только заполнением форм с использованием Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Зашифровать PDF только для заполнения форм с помощью AES‑256, используя Aspose.Pdf
Этот учебник показывает, как защитить существующий PDF, чтобы пользователи могли только заполнять его формы. В нём пошагово описывается открытие документа с помощью Aspose.Pdf for .NET, ограничение разрешений до заполнения форм, применение шифрования AES‑256, установка паролей для просмотра и владельца и, наконец, сохранение защищённого файла.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-form-filling" >}}


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

**Q: Что именно разрешает и блокирует флаг `Permissions.FillForm` в зашифрованном PDF?**  
A: `Permissions.FillForm` позволяет пользователям заполнять интерактивные поля формы, но отключает все остальные действия, такие как печать, извлечение содержимого или изменение структуры документа.

**Q: Могу ли я использовать другой алгоритм шифрования, например AES‑128, с тем же вызовом `Encrypt`?**  
A: Да, замените `CryptoAlgorithm.AESx256` на `CryptoAlgorithm.AESx128` (или другое поддерживаемое значение перечисления) в методе `pdfDoc.Encrypt`, чтобы изменить уровень шифрования.

**Q: В чём разница между паролем для просмотра (`viewerPwd`) и паролем владельца (`masterPwd`)?**  
A: Пароль для просмотра (`readPass`) необходим для открытия PDF и применения указанных разрешений, тогда как пароль владельца (`fullPass`) предоставляет полный неограниченный доступ и может использоваться для изменения разрешений или снятия шифрования.

**Q: Если я опущу аргумент `permissionSet` или передам `Permissions.None`, какие разрешения будет иметь PDF после шифрования?**  
A: Передача `Permissions.None` (или отсутствие аргумента) приводит к PDF без специальных ограничений: пароль для просмотра по‑прежнему защищает файл, но пользователи могут выполнять все стандартные действия, такие как печать и копирование.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}