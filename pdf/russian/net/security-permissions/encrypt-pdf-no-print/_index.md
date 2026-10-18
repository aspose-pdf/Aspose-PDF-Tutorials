---
title: Шифрование PDF без разрешения на печать с использованием Aspose.PDF for .NET
weight: 101
limit:
description: Узнайте, как зашифровать PDF с помощью AES‑256 и отключить печать, используя Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Узнайте, как зашифровать PDF с помощью AES‑256 и отключить печать,
    используя Aspose.PDF for .NET.
  headline: Шифрование PDF без разрешения на печать с использованием Aspose.PDF for
    .NET
  type: TechArticle
- description: Узнайте, как зашифровать PDF с помощью AES‑256 и отключить печать,
    используя Aspose.PDF for .NET.
  name: Шифрование PDF без разрешения на печать с использованием Aspose.PDF for .NET
  steps:
  - name: Определите путь к исходному PDF, имя выходного защищённого файла и пароли
      для просмотра и владельца.
    text: Определите путь к исходному PDF, имя выходного защищённого файла и пароли
      для просмотра и владельца.
  - name: Проверьте, существует ли исходный файл, и при его отсутствии завершите работу
      с сообщением об ошибке.
    text: Проверьте, существует ли исходный файл, и при его отсутствии завершите работу
      с сообщением об ошибке.
  - name: Откройте оригинальный PDF, задайте отсутствие разрешений, зашифруйте его
      с помощью AES‑256, используя указанные пароли, и сохраните защищённый файл.
    text: Откройте оригинальный PDF, задайте отсутствие разрешений, зашифруйте его
      с помощью AES‑256, используя указанные пароли, и сохраните защищённый файл.
  - name: Снова откройте зашифрованный PDF с паролем просмотра и выведите значение
      свойства IsEncrypted в консоль, чтобы подтвердить защиту.
    text: Снова откройте зашифрованный PDF с паролем просмотра и выведите значение
      свойства IsEncrypted в консоль, чтобы подтвердить защиту.
  - name: Выведите окончательное сообщение, указывающее, что шифрование завершено,
      и имя выходного файла.
    text: Выведите окончательное сообщение, указывающее, что шифрование завершено,
      и имя выходного файла.
  type: HowTo
- questions:
  - answer: '`Permissions` — это перечисление-флаг; присваивание `0` означает, что
      ни один бит разрешения не установлен, поэтому Aspose.Pdf не предоставляет право
      PrintDocument, и просмотрщик не может распечатать PDF.'
    question: Почему установка `Permissions rights = 0;` отключает печать?
  - answer: Да, замените `CryptoAlgorithm.AESx256` на `CryptoAlgorithm.AESx128` (или
      другое поддерживаемое значение перечисления) в вызове `pdfDoc.Encrypt`; остальная
      часть кода остаётся без изменений.
    question: Могу ли я использовать другой алгоритм шифрования, например AES‑128,
      с тем же кодом?
  - answer: Aspose.Pdf примет одинаковые пароли, но пароль владельца больше не будет
      предоставлять дополнительных привилегий; PDF всё равно будет зашифрован, и применятся
      указанные вами разрешения (отсутствие).
    question: Что произойдёт, если пароль просмотра и мастер‑пароль (пароль владельца)
      будут одинаковыми?
  - answer: Откройте защищённый файл с паролем просмотра (`new Document(securedFile,
      viewerPwd)`) и попытайтесь распечатать его в PDF‑просмотрщике; поскольку разрешение
      `PrintDocument` не было установлено, просмотрщик отклонит команду печати.
    question: Как я могу убедиться, что печать действительно заблокирована после шифрования?
  - answer: Код проверяет `File.Exists(sourceFile)` и записывает ошибку в `Console.Error`
      перед возвратом, предотвращая выброс `FileNotFoundException` конструктором `Document`.
    question: Какую ошибку генерирует система, если `original.pdf` не существует,
      и как её следует обработать?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: Шифрование PDF и блокировка печати
og_description: Защитите ваш PDF с помощью шифрования AES‑256 и убедитесь, что его нельзя распечатать — пошаговое руководство.
og_image_alt: Снимок экрана, показывающий код Aspose.PDF for .NET, который шифрует PDF и отключает печать.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Шифрование PDF без разрешения на печать с использованием Aspose.PDF
В этом учебнике показано, как открыть существующий PDF с помощью Aspose.PDF for .NET, применить шифрование AES‑256, не предоставляя никаких разрешений — фактически отключая печать — сохранить защищённый документ и подтвердить защиту, открыв его с паролем просмотра. Следуйте пошаговому коду, чтобы убедиться, что ваш PDF нельзя распечатать после шифрования.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


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

**Q: Почему установка `Permissions rights = 0;` отключает печать?**  
A: `Permissions` — это перечисление-флаг; присваивание `0` означает, что ни один бит разрешения не установлен, поэтому Aspose.Pdf не предоставляет право PrintDocument, и просмотрщик не может распечатать PDF.

**Q: Могу ли я использовать другой алгоритм шифрования, например AES‑128, с тем же кодом?**  
A: Да, замените `CryptoAlgorithm.AESx256` на `CryptoAlgorithm.AESx128` (или другое поддерживаемое значение перечисления) в вызове `pdfDoc.Encrypt`; остальная часть кода остаётся без изменений.

**Q: Что произойдёт, если пароль просмотра и мастер‑пароль (пароль владельца) будут одинаковыми?**  
A: Aspose.Pdf примет одинаковые пароли, но пароль владельца больше не будет предоставлять дополнительных привилегий; PDF всё равно будет зашифрован, и применятся указанные вами разрешения (отсутствие).

**Q: Как я могу убедиться, что печать действительно заблокирована после шифрования?**  
A: Откройте защищённый файл с паролем просмотра (`new Document(securedFile, viewerPwd)`) и попытайтесь распечатать его в PDF‑просмотрщике; поскольку разрешение `PrintDocument` не было установлено, просмотрщик отклонит команду печати.

**Q: Какую ошибку генерирует система, если `original.pdf` не существует, и как её следует обработать?**  
A: Код проверяет `File.Exists(sourceFile)` и записывает ошибку в `Console.Error` перед возвратом, предотвращая выброс `FileNotFoundException` конструктором `Document`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}