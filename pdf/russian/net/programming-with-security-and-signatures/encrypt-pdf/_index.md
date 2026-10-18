---
title: Шифрование PDF с паролями пользователя и владельца с помощью Aspose.PDF for .NET
weight: 220
limit:
description: Научитесь загружать PDF, ограничивать разрешения, шифровать его паролями пользователя и владельца с использованием AES‑256 и сохранять защищённый документ с помощью Aspose.PDF for .NET.
keywords: [pdf encryption, Aspose.PDF for .NET, aes-256 pdf protection, user password pdf, owner password pdf, restrict pdf permissions]
url: /net/programming-with-security-and-signatures/encrypt-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Научитесь загружать PDF, ограничивать разрешения, шифровать его паролями
    пользователя и владельца с использованием AES‑256 и сохранять защищённый документ
    с помощью Aspose.PDF for .NET.
  headline: Шифрование PDF с паролями пользователя и владельца с помощью Aspose.PDF
    for .NET
  type: TechArticle
- description: Научитесь загружать PDF, ограничивать разрешения, шифровать его паролями
    пользователя и владельца с использованием AES‑256 и сохранять защищённый документ
    с помощью Aspose.PDF for .NET.
  name: Шифрование PDF с паролями пользователя и владельца с помощью Aspose.PDF for
    .NET
  steps:
  - name: Объявите пути к исходному и целевому файлам, а также пароли пользователя
      (клиент) и владельца (администратор).
    text: Объявите пути к исходному и целевому файлам, а также пароли пользователя
      (клиент) и владельца (администратор).
  - name: Проверьте, существует ли исходный PDF, и при его отсутствии прервите выполнение
      с сообщением об ошибке.
    text: Проверьте, существует ли исходный PDF, и при его отсутствии прервите выполнение
      с сообщением об ошибке.
  - name: Откройте PDF, разрешите только изменение содержимого и его извлечение, зашифруйте
      его двумя паролями с использованием AES‑256, сохраните защищённый файл и отобразите
      сообщение об успешном выполнении.
    text: Откройте PDF, разрешите только изменение содержимого и его извлечение, зашифруйте
      его двумя паролями с использованием AES‑256, сохраните защищённый файл и отобразите
      сообщение об успешном выполнении.
  - name: Перехватите любые возникающие ошибки и выведите сообщение исключения в консоль
      ошибок.
    text: Перехватите любые возникающие ошибки и выведите сообщение исключения в консоль
      ошибок.
  type: HowTo
- questions:
  - answer: '`Permissions.ModifyContent` позволяет пользователю редактировать текст
      и объекты PDF, а `Permissions.ExtractContent` позволяет копировать текст или
      изображения. Вместе они дают возможность редактировать и извлекать содержимое,
      но по‑прежнему блокируют печать, поскольку `Permissions.Print` не включён.'
    question: Какие разрешения предоставляются, когда я комбинирую `Permissions.ModifyContent`
      с `Permissions.ExtractContent`?
  - answer: Да, замените `CryptoAlgorithm.AESx256` на другое значение перечисления,
      например `CryptoAlgorithm.AESx128`, в вызове `Encrypt`; остальная часть кода
      остаётся без изменений.
    question: Могу ли я использовать другой алгоритм шифрования, например AES‑128,
      вместо `CryptoAlgorithm.AESx256`?
  - answer: Пароль пользователя (`clientPwd`) необходим для открытия PDF и применяет
      указанные разрешения, тогда как пароль владельца (`adminPwd`) предоставляет
      полный доступ, позволяя его обладателю изменять разрешения или удалять шифрование.
    question: В чём практическая разница между паролем пользователя (клиент) и паролем
      владельца (администратор)?
  - answer: PDF всё равно будет зашифрован, но различие между привилегиями пользователя
      и владельца исчезнет; любой, кто знает единственный пароль, получит полный доступ,
      фактически делая настройки разрешений бессмысленными.
    question: Что произойдёт, если я установлю одинаковую строку и для пароля клиента,
      и для пароля администратора?
  type: FAQPage
images:
- /net/programming-with-security-and-signatures/encrypt-pdf/og-image.png
og_title: Шифрование PDF с паролями пользователя и владельца (AES‑256)
og_description: Защитите ваш PDF, добавив оба пароля — пользователя и владельца — с шифрованием AES‑256 за считанные минуты.
og_image_alt: Руководство, показывающее, как зашифровать PDF паролями пользователя и владельца с использованием AES‑256 в Aspose.PDF for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Шифрование PDF с паролями пользователя и владельца с помощью Aspose.PDF
Этот учебный материал пошагово показывает, как загрузить существующий PDF с помощью Aspose.PDF, применить ограничения разрешений и защитить документ, зашифровав его как паролем пользователя (клиент), так и паролем владельца (администратор) с использованием алгоритма AES‑256, а затем сохранить защищённый файл.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-security-and-signatures/encrypt-pdf" >}}


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

**Q: Какие разрешения предоставляются, когда я комбинирую `Permissions.ModifyContent` с `Permissions.ExtractContent`?**  
A: `Permissions.ModifyContent` позволяет пользователю редактировать текст и объекты PDF, а `Permissions.ExtractContent` позволяет копировать текст или изображения. Вместе они дают возможность редактировать и извлекать содержимое, но по‑прежнему блокируют печать, поскольку `Permissions.Print` не включён.

**Q: Могу ли я использовать другой алгоритм шифрования, например AES‑128, вместо `CryptoAlgorithm.AESx256`?**  
A: Да, замените `CryptoAlgorithm.AESx256` на другое значение перечисления, например `CryptoAlgorithm.AESx128`, в вызове `Encrypt`; остальная часть кода остаётся без изменений.

**Q: В чём практическая разница между паролем пользователя (клиент) и паролем владельца (администратор)?**  
A: Пароль пользователя (`clientPwd`) необходим для открытия PDF и применяет указанные разрешения, тогда как пароль владельца (`adminPwd`) предоставляет полный доступ, позволяя его обладателю изменять разрешения или удалять шифрование.

**Q: Что произойдёт, если я установлю одинаковую строку и для пароля клиента, и для пароля администратора?**  
A: PDF всё равно будет зашифрован, но различие между привилегиями пользователя и владельца исчезнет; любой, кто знает единственный пароль, получит полный доступ, фактически делая настройки разрешений бессмысленными.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}