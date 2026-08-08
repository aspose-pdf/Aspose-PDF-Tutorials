---
category: general
date: 2026-05-27
description: Как удалить встроенные шрифты из PDF с помощью Aspose.Pdf в C#. Узнайте
  быстрый приём манипуляции PDF на C#, позволяющий удалить шрифты и уменьшить размер
  файла.
draft: false
keywords:
- how to remove embedded fonts pdf
- Aspose.Pdf
- C# PDF manipulation
- remove embedded fonts
- PDF resource dictionary
language: ru
og_description: Как удалить встроенные шрифты из PDF с помощью Aspose.Pdf в C#. Следуйте
  этому краткому руководству, чтобы очистить PDF и уменьшить их размер.
og_title: Как удалить встроенные шрифты из PDF – Полный учебник по C#
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: How to remove embedded fonts PDF using Aspose.Pdf in C#. Learn a quick
    C# PDF manipulation technique to strip fonts and shrink file size.
  headline: How to Remove Embedded Fonts PDF – Step‑by‑Step C# Guide
  type: TechArticle
- description: How to remove embedded fonts PDF using Aspose.Pdf in C#. Learn a quick
    C# PDF manipulation technique to strip fonts and shrink file size.
  name: How to Remove Embedded Fonts PDF – Step‑by‑Step C# Guide
  steps:
  - name: Does removing fonts break text rendering?
    text: Usually not. PDF viewers will substitute missing glyphs with a default font
      (often Helvetica or Arial). If the original PDF used custom glyphs (e.g., a
      brand‑specific typeface), those characters may appear as boxes. In such cases,
      you might prefer to subset the fonts instead of removing them entirel
  - name: What about encrypted PDFs?
    text: 'Aspose.Pdf can open password‑protected PDFs, but you must supply the password
      when constructing the `Document` object:'
  - name: Can I automate this for a whole folder?
    text: Absolutely. Wrap the core logic in a method and iterate over `Directory.GetFiles`.
      Remember to handle exceptions—corrupt PDFs will throw `PdfException`, which
      you can log and skip.
  type: HowTo
tags:
- PDF
- C#
- Aspose
title: Как удалить встроенные шрифты из PDF – пошаговое руководство на C#
url: /ru/net/document-manipulation/how-to-remove-embedded-fonts-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как удалить встроенные шрифты PDF – Полный учебник C#

Когда‑нибудь задавались вопросом **how to remove embedded fonts PDF** файлов, которые бесконечно растут в размере? Вы не одиноки. Во многих проектах — будь то генераторы автоматических отчётов или конвейеры пакетной обработки — скрытые потоки шрифтов могут добавить мегабайты без надобности. Хорошая новость? С помощью нескольких строк C# и Aspose.Pdf вы можете чисто удалить эти шрифты, и результатом будет более лёгкий, более переносимый документ.

В этом учебнике мы пройдём практический пример от начала до конца, который не только покажет *how to remove embedded fonts PDF*, но и объяснит, почему работа с **PDF resource dictionary** работает, какие подводные камни могут возникнуть и как проверить результат. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любое C# консольное приложение, веб‑службу или фоновую задачу.

## Требования

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

- **.NET 6.0** или новее (код также работает на .NET Framework 4.7+).  
- Действительная лицензия **Aspose.Pdf for .NET** или бесплатная оценочная копия.  
- PDF‑файл (`input.pdf`), содержащий встроенные шрифты — большинство PDF, созданных из Word или дизайнерских инструментов, подходят.

Если у вас нет библиотеки, получите её из NuGet:

```bash
dotnet add package Aspose.Pdf
```

Теперь, когда подготовка завершена, приступим к делу.

## Шаг 1: Загрузка PDF‑документа

Первое, что нужно сделать — открыть исходный PDF. Класс `Document` из Aspose.Pdf абстрагирует низкоуровневую работу с файлом, предоставляя чистую объектную модель для работы.

```csharp
using Aspose.Pdf;

// Step 1: Load the PDF document from disk
using (var doc = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // The document is now in memory and ready for manipulation.
```

> **Почему это важно:**  
> Загрузка файла внутри блока `using` гарантирует автоматическое освобождение всех неуправляемых ресурсов (дескрипторы файлов, буферы потоков). Пропуск этого блока может оставить файл заблокированным, особенно в Windows, где по умолчанию используется эксклюзивный доступ.

## Шаг 2: Доступ к PDF‑Resource Dictionary первой страницы

Каждая страница PDF имеет словарь **Resources**, в котором перечислены шрифты, изображения, цветовые пространства и прочее. Удаление записи `Font` из этого словаря сообщает рендереру PDF, что страница больше не ссылается на встроенные объекты шрифтов.

```csharp
    // Step 2: Grab the resource dictionary for the first page (pages are 1‑based)
    var editor = new Aspose.Pdf.DataEditor.DictionaryEditor(doc.Pages[1].Resources);

    // At this point, `editor` gives us direct access to the underlying PDF dictionary.
```

> **Совет:** Если ваш PDF содержит несколько страниц и вы хотите очистить их все, выполните цикл по `doc.Pages` и примените ту же логику. Для одностраничного документа приведённый выше код достаточен.

## Шаг 3: Удаление записи «Font»

Теперь переходим к основной части операции **how to remove embedded fonts PDF**. Вызвав `Remove("Font")`, мы удаляем весь подсловарь шрифтов, эффективно убирая все ссылки на встроенные шрифты с этой страницы.

```csharp
    // Step 3: Delete the Font entry – this removes all embedded fonts on this page
    editor.Remove("Font");
```

> **Что происходит под капотом?**  
> Спецификация PDF хранит каждый шрифт как косвенный объект. Запись `Font` в Resources страницы указывает на коллекцию этих объектов. Когда вы стираете эту запись, PDF‑чтение больше не может найти шрифты, поэтому оно переключается на системные шрифты или заменители, что резко уменьшает размер файла.  
> 
> **Особый случай:** Некоторые PDF используют шрифты косвенно через Form XObjects или аннотации. Если после этого шага вы всё ещё видите потоки шрифтов, возможно, потребуется также очистить ресурсы этих XObject‑ов. Тот же подход `DictionaryEditor` работает — просто нацелитесь на словарь Resources соответствующего XObject.

## Шаг 4: Сохранение изменённого PDF

Наконец, запишите очищенный PDF обратно на диск. Вы можете перезаписать оригинальный файл или, как показано здесь, создать новый (`noFonts.pdf`), чтобы оставить исходный нетронутым.

```csharp
    // Step 4: Persist the changes to a new file
    doc.Save("YOUR_DIRECTORY/noFonts.pdf");
} // The using block disposes the Document instance here
```

> **Совет по проверке:** Откройте `noFonts.pdf` в просмотрщике PDF и проверьте размер файла. Вы должны увидеть заметное сокращение — часто 30‑70 % в зависимости от количества встроенных шрифтов. Кроме того, большинство просмотрщиков позволяют просмотреть свойства документа и убедиться, что в разделе «Fonts» нет перечисленных шрифтов.

## Полный рабочий пример

Собрав всё вместе, получаем полностью готовую к запуску программу. Вставьте её в новое консольное приложение (`dotnet new console`) и нажмите **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.DataEditor;

namespace RemoveEmbeddedFonts
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputPath = "YOUR_DIRECTORY/input.pdf";
            string outputPath = "YOUR_DIRECTORY/noFonts.pdf";

            // Load the PDF document
            using (var doc = new Document(inputPath))
            {
                // Loop through every page to ensure all fonts are removed
                foreach (Page page in doc.Pages)
                {
                    var editor = new DictionaryEditor(page.Resources);
                    // If a Font dictionary exists, remove it
                    if (editor.ContainsKey("Font"))
                    {
                        editor.Remove("Font");
                    }
                }

                // Save the cleaned document
                doc.Save(outputPath);
                Console.WriteLine($"Embedded fonts removed. Output saved to: {outputPath}");
            }
        }
    }
}
```

**Ожидаемый вывод в консоли:**

```
Embedded fonts removed. Output saved to: YOUR_DIRECTORY/noFonts.pdf
```

Откройте полученный PDF, и вы заметите:

- Размер файла уменьшился.  
- Визуальное отображение осталось прежним (если только оригинал не полагался на пользовательские глифы).  
- Панель «Fonts» в просмотрщике PDF показывает только стандартные системные шрифты.

## Часто задаваемые вопросы и подводные камни

### Удаление шрифтов ломает отображение текста?

Обычно нет. Просмотрщики PDF заменят отсутствующие глифы шрифтом по умолчанию (часто Helvetica или Arial). Если оригинальный PDF использовал пользовательские глифы (например, фирменный шрифт), эти символы могут отобразиться как квадратики. В таких случаях предпочтительнее выполнить субсетинг шрифтов, а не полное их удаление — более продвинутая тема, выходящая за рамки данного руководства.

### Что делать с зашифрованными PDF?

Aspose.Pdf может открывать защищённые паролем PDF, но вам нужно передать пароль при создании объекта `Document`:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var doc = new Document("protected.pdf", loadOptions);
```

После расшифровки те же шаги редактирования словаря применимы.

### Можно ли автоматизировать процесс для всей папки?

Безусловно. Вынесите основную логику в метод и переберите файлы с помощью `Directory.GetFiles`. Не забудьте обработать исключения — повреждённые PDF бросают `PdfException`, который можно залогировать и пропустить.

```csharp
foreach (var file in Directory.GetFiles(sourceFolder, "*.pdf"))
{
    try { RemoveFonts(file, Path.Combine(destFolder, Path.GetFileName(file))); }
    catch (PdfException ex) { Console.WriteLine($"Failed on {file}: {ex.Message}"); }
}
```

## Соображения по производительности

- **Использование памяти:** Загрузка PDF в память дешёва для файлов до 50 МБ. Для огромных архивов рассмотрите обработку страниц по одной, как показано в цикле выше.  
- **Скорость:** Удаление одной записи словаря — O(1). Узким местом обычно является ввод‑вывод на диск, а не вызов `DictionaryEditor`.

## Итоги

Мы только что рассмотрели **how to remove embedded fonts PDF** файлы с помощью Aspose.Pdf и нескольких лаконичных команд C#. Ключевые шаги:

1. Загрузить документ.  
2. Доступ к **PDF resource dictionary** каждой страницы.  
3. Удалить запись `Font`.  
4. Сохранить очищенный PDF.

Обладая этими знаниями, вы сможете уменьшать PDF‑файлы «на лету», ускорять загрузку и соответствовать ограничениям по размеру вложений в электронных письмах или облачном хранилище. Далее вы можете изучить техники **C# PDF manipulation**, такие как сжатие изображений, удаление метаданных или даже создание PDF с нуля, используя тот же API Aspose.Pdf.

Есть другой сценарий использования? Возможно, вам нужно оставить некоторые шрифты, удалив остальные, или вы интересуетесь вариантами лицензирования **Aspose.Pdf**. Обратитесь к официальной документации Aspose или задавайте вопросы в комментариях — happy coding!

## Связанные учебники

- [Unembed Fonts in PDFs Using Aspose.PDF for .NET&#58; Reduce File Size and Improve Performance](/pdf/english/net/performance-optimization/optimize-pdfs-unembed-fonts-aspose-pdf-net/)
- [How to Embed and Subset Fonts in PDFs Using Aspose.PDF for .NET - A Comprehensive Guide](/pdf/english/net/text-operations/embed-subset-fonts-aspose-pdf-net/)
- [How to Remove All Attachments from a PDF Using Aspose.PDF .NET&#58; A Comprehensive Guide](/pdf/english/net/attachments-embedded-files/remove-attachments-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}