---
category: general
date: 2026-08-17
description: Создайте пустое графическое состояние в PDF с помощью C# и Aspose.Pdf.
  Следуйте этому пошаговому руководству, чтобы безопасно редактировать ресурсы ExtGState.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: ru
lastmod: 2026-08-17
og_description: Создайте пустое графическое состояние в PDF с помощью C#. Этот учебник
  показывает, как редактировать ресурсы ExtGState с помощью Aspose.Pdf для надёжных
  модификаций PDF.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Создание пустого графического состояния в PDF с помощью C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Как создать пустое графическое состояние в PDF с помощью C#
url: /ru/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать пустое графическое состояние в PDF с помощью C#

Если вам нужно **создать пустое графическое состояние** в PDF, это руководство покажет, как сделать это с помощью C# и Aspose.Pdf. Вы увидите полностью готовый, исполняемый пример, который добавляет новую запись в словарь ExtGState страницы, не затрагивая существующее содержимое.

Работа с графическими состояниями PDF часто требуется, когда нужно управлять прозрачностью, режимами наложения или другими параметрами рендеринга для отдельных объектов. Приведённый ниже код демонстрирует рекомендуемый подход, объясняет, почему каждый шаг важен, и охватывает типичные варианты, с которыми вы можете столкнуться.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 или новее (пример также компилируется с .NET Core).
* Лицензия Aspose.Pdf for .NET (или временный оценочный ключ).
* Папка, содержащая файл `input.pdf`, который вы хотите изменить.
* Базовые знания синтаксиса C# и концепций PDF, таких как словари ресурсов.

## Шаг 1: Настройка проекта и импорт пространств имён

Создайте новое консольное приложение или интегрируйте код в существующий проект. Добавьте пакет Aspose.Pdf через NuGet:

```bash
dotnet add package Aspose.Pdf
```

Затем импортируйте необходимые пространства имён:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Эти импорты дают доступ к классам `Document`, `DictionaryEditor` и PDF‑примитивам, необходимым для **создания пустого графического состояния**.

## Шаг 2: Определите папку, в которой находятся PDF‑файлы

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Замените путь на расположение ваших собственных PDF‑файлов. Хранение директории в переменной делает код переиспользуемым и упрощает тестирование.

## Шаг 3: Загрузите исходный PDF‑документ

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Открытие документа внутри блока `using` гарантирует, что файловый дескриптор будет освобождён автоматически после сохранения изменений.

## Шаг 4: Получите первую страницу и её словарь Resources

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` возвращает первую страницу (нумерация страниц PDF начинается с 1).
* `DictionaryEditor` предоставляет удобный способ чтения и изменения словарей PDF.
* Запись `ExtGState` содержит все объекты графических состояний для страницы. Если ключ отсутствует, Aspose.Pdf автоматически создаёт пустой словарь.

## Шаг 5: Создайте новый пустой словарь графического состояния

Графическое состояние, которое вы добавляете, может быть пустым или предварительно заполненным параметрами, такими как непрозрачность (`CA`, `ca`) или режим наложения (`BM`). В этом руководстве мы создаём **пустое графическое состояние**, а затем задаём несколько типичных значений для демонстрации работы словаря.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` создаёт чистый контейнер, который вы можете заполнить любыми ключами графического состояния.
* Добавление `CA`, `ca` и `BM` необязательно; их можно опустить, если действительно нужен пустой статус. Код показывает, как добавить записи, когда позже понадобится управлять рендерингом.

## Шаг 6: Вставьте новое графическое состояние в словарь ExtGState

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Имя записи `"GS0"` следует общепринятой конвенции префикса графических состояний «GS». Вы можете выбрать любое допустимое имя PDF, которое не конфликтует с существующими ключами.

## Шаг 7: Сохраните изменённый PDF‑документ

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

Вызов `Save` записывает обновлённый файл в `output.pdf`. Открытие этого файла в просмотрщике PDF подтверждает наличие нового графического состояния; позже его можно будет ссылаться оператором `gs` в потоках содержимого.

### Полный листинг исходного кода

Объединив всё вместе, получаем полную программу:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

Запуск программы выводит строку подтверждения и создаёт `output.pdf` с добавленным графическим состоянием.

## Почему этот подход работает лучше всего

* **Прямое редактирование словарей** – Использование `DictionaryEditor` избавляет от необходимости парсить весь поток содержимого. Вы изменяете только те ресурсы, которые вам нужны.
* **Типизированные PDF‑примитивы** – `CosPdfNumber`, `CosPdfName` и `CosPdfDictionary` гарантируют, что сгенерированный PDF соответствует спецификации PDF 1.7.
* **Безопасность** – Блок `using` освобождает объект `Document`, предотвращая блокировки файлов, которые могут повредить последующие сборки.
* **Расширяемость** – Как только пустое графическое состояние существует, вы можете ссылаться на него из любого оператора содержимого (`gs`), меняя непрозрачность, режим наложения или другие параметры для выбранных команд рисования.

## Общие варианты и граничные случаи

| Ситуация | Рекомендуемое изменение |
|-----------|-------------------|
| **Несколько страниц** | Выполните цикл по `pdfDocument.Pages` и повторите вставку словаря для каждой страницы, которую нужно изменить. |
| **Отсутствует запись ExtGState** | `resourcesEditor["ExtGState"]` автоматически создаёт пустой словарь, если он не существует. Дополнительный код не требуется. |
| **Другое имя графического состояния** | Замените `"GS0"` на имя, соответствующее вашей конвенции, например, `"MyTransparentState"`. |
| **Добавление только пустого состояния** | Опустите массив `parameters` и цикл `foreach`; словарь останется пустым. |
| **Работа с зашифрованными PDF** | Перед редактированием ресурсов передайте пароль при создании `new Document(path, password)`. |

## Проверка результата

Вы можете убедиться, что графическое состояние добавлено, проверив PDF в низкоуровневом просмотрщике, таком как **PDF‑Tron** или **iText Sharp**. Ищите запись, похожую на:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Если запись присутствует, операция **создания пустого графического состояния** выполнена успешно.

## Заключение

Теперь вы знаете, как **создать пустое графическое состояние** в PDF с помощью C# и Aspose.Pdf. Руководство охватило каждый шаг — от загрузки документа до редактирования словаря `ExtGState` и сохранения результата, объясняя логику каждого действия.  

Дальше вы можете:

* Использовать новое графическое состояние в потоках содержимого (`gs /GS0`).
* Поэкспериментировать с дополнительными ключами, такими как `/SM` (коррекция штриха) или `/OPM` (режим наложения).
* Применить тот же приём к другим типам ресурсов, например `/XObject` или `/ColorSpace`.

Удачной работы с PDF, и не стесняйтесь исследовать другие **сценарии графических состояний Aspose PDF**, такие как динамические изменения непрозрачности или пользовательские режимы наложения!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как создать пунктирные линии в PDF с помощью Aspose.PDF для .NET&#58; Пошаговое руководство](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Как удалить графику из PDF с помощью Aspose.PDF .NET&#58; Полное руководство](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Создание и заполнение прямоугольников в PDF с помощью Aspose.PDF для .NET&#58; Пошаговое руководство](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}