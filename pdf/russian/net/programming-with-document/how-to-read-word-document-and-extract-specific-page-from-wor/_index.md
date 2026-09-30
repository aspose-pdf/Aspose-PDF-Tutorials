---
category: general
date: 2026-04-12
description: Как читать документ Word и извлекать определённую страницу из Word с
  помощью C#. Пошаговый код показывает загрузку .docx, получение второй страницы и
  чтение артефакта Бейтса.
draft: false
keywords:
- how to read word document
- extract specific page from word
- C# Word processing
- read .docx page
- document artifact extraction
language: ru
og_description: Как прочитать документ Word и извлечь определённую страницу из Word
  с полным примером на C#. Узнайте, как загрузить .docx, выбрать страницу 2 и получить
  номера Бейтса.
og_title: Как читать документ Word – извлечь конкретную страницу из Word в C#
tags:
- C#
- Word
- Document Automation
title: Как читать документ Word и извлекать определённую страницу из Word – руководство
  по C#
url: /ru/net/programming-with-document/how-to-read-word-document-and-extract-specific-page-from-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как читать документ Word и извлекать конкретную страницу из Word – Полный учебник C#  

Когда‑нибудь задумывались **как читать документ Word** программно и вытягивать только нужную часть? Возможно, вы создаёте систему управления делами, которой необходимо получить номер Бейтса со страницы 2 юридического брифа. В таком случае вам понадобится **извлекать конкретную страницу из Word** без загрузки всего файла в память каждый раз.  

В этом руководстве мы пройдём реальное решение: загрузим `.docx`, выберем вторую страницу, найдём первый артефакт «Bates» и выведем его текст. К концу у вас будет автономный, исполняемый фрагмент кода, который можно вставить в любой проект .NET. Никаких расплывчатых «см. документацию» обходных путей — только конкретный код и объяснения *почему* каждая строка важна.

> **Что вы узнаете**  
> * Как читать документ Word в C# с помощью популярного SDK.  
> * Как **извлекать конкретную страницу из Word** используя индексацию с нуля.  
> * Как искать артефакт (например, номер Бейтса) и корректно обрабатывать отсутствие данных.  
> * Советы по граничным случаям, производительности и дальнейшим расширениям.

## Требования  

Прежде чем погрузиться, убедитесь, что у вас есть:

| Требование | Почему это важно |
|-------------|----------------|
| .NET 6.0 или новее (или .NET Framework 4.7+) | SDK, который мы будем использовать, нацелен на .NET Standard 2.0+. |
| Visual Studio 2022 (или любая IDE по вашему выбору) | Для удобного отладки и IntelliSense. |
| **GroupDocs.Annotation for .NET** (или Aspose.Words, если предпочитаете) установлен через NuGet | Предоставляет классы `Document`, `Page` и `Artifact`, используемые в примере. |
| Пример файла Word (`input.docx`), размещённый в папке `YOUR_DIRECTORY` | В руководстве предполагается, что файл существует; вы можете заменить его своим путём. |

You can add the package with:

```bash
dotnet add package GroupDocs.Annotation --version 23.10
```

If you opt for Aspose.Words, the API differs slightly—but the core idea of loading a document, accessing page collections, and iterating artifacts stays the same.

![Диаграмма, иллюстрирующая как читать документ Word и извлекать одну страницу](/images/read-word-document.png){: .center alt="Диаграмма, показывающая как читать документ Word"}

## Пошаговая реализация  

Ниже мы разбиваем решение на логические части. Каждая часть имеет чёткий заголовок (полезно для индексации ИИ) и короткий фрагмент кода, который опирается на предыдущий.  

### 1. Как читать документ Word — загрузка файла  

Первое, что делает любой код обработки документов, — открывает файл. С GroupDocs.Annotation вы создаёте объект `Document`, передавая полный путь к `.docx`.  

```csharp
using GroupDocs.Annotation;
using GroupDocs.Annotation.Models;

// Load the source document (replace YOUR_DIRECTORY with your actual path)
string docPath = Path.Combine("YOUR_DIRECTORY", "input.docx");
Document doc = new Document(docPath);
```

**Почему это важно:**  
* Конструктор разбирает файл Word и создаёт в‑памяти представление страниц, аннотаций и артефактов.  
* Если файл отсутствует или повреждён, SDK бросает описательное `FileNotFoundException` или `AnnotationException`, которые можно перехватить позже.

### 2. Извлечь конкретную страницу из Word — доступ к нужной странице  

Документы Word не предоставляют нативный объект «страница», поскольку пагинация зависит от макета. Однако SDK рендерит документ в коллекцию объектов `Page` после загрузки. Страницы нумеруются с нуля, поэтому страница 2 имеет индекс 1.  

```csharp
// Retrieve the second page (zero‑based index)
int pageIndex = 1; // page 2 in human terms
Page secondPage = doc.Pages[pageIndex];
```

**Зачем это нужно:**  
* Прямой доступ к `doc.Pages[1]` позволяет избежать перебора всего документа, когда вам нужна только одна часть.  
* Если в документе меньше страниц, будет выброшено `IndexOutOfRangeException` — обработайте его, чтобы приложение было надёжным (см. раздел «Обработка ошибок» ниже).

### 3. Найти артефакт Bates — поиск на странице  

Артефакты — это объекты метаданных, привязанные к странице, похожие на скрытые заметки, такие как номера Бейтса, комментарии или пользовательские теги. Мы будем искать первый артефакт, у которого `Subtype` равно `"Bates"`.

```csharp
// Find the first artifact with subtype "Bates"
Artifact batesArtifact = secondPage.Artifacts
    .FirstOrDefault(a => a.Subtype.Equals("Bates", StringComparison.OrdinalIgnoreCase));
```

**Почему этот шаг важен:**  
* Использование `FirstOrDefault` возвращает безопасный null, если артефакт Bates отсутствует, позволяя решить, как реагировать (логировать, использовать значение по умолчанию и т.д.).  
* Защита `StringComparison.OrdinalIgnoreCase` предохраняет от различий в регистре в исходном документе.

### 4. Вывести текст артефакта — безопасный вывод в консоль  

Теперь, когда у нас есть (или нет) артефакт Bates, мы просто выводим его текст. Это отражает то, как реальное приложение может сохранять его в базе данных или отправлять в другой сервис.

```csharp
if (batesArtifact != null)
{
    Console.WriteLine($"Current Bates: {batesArtifact.Text}");
}
else
{
    Console.WriteLine("No Bates artifact found on page 2.");
}
```

**Что ожидать:**  
Запуск программы с документом, содержащим номер Bates на странице 2, выводит что‑то вроде:

```
Current Bates: 2023-00123
```

Если артефакт отсутствует, вы увидите сообщение‑запас, предотвращающее `NullReferenceException`.

### 5. Полный рабочий пример — собрать всё вместе  

Ниже представлен полный готовый к запуску консольный приложение. Скопируйте и вставьте его в новый проект C#, восстановите пакеты NuGet и нажмите **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using GroupDocs.Annotation;
using GroupDocs.Annotation.Models;

namespace WordPageExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the source document
                string docPath = Path.Combine("YOUR_DIRECTORY", "input.docx");
                Document doc = new Document(docPath);

                // 2️⃣ Extract specific page from word (page 2 = index 1)
                int pageIndex = 1;
                if (pageIndex >= doc.Pages.Count)
                {
                    Console.WriteLine($"Document only has {doc.Pages.Count} page(s). Cannot access page {pageIndex + 1}.");
                    return;
                }
                Page secondPage = doc.Pages[pageIndex];

                // 3️⃣ Locate the first Bates artifact on that page
                Artifact batesArtifact = secondPage.Artifacts
                    .FirstOrDefault(a => a.Subtype.Equals("Bates", StringComparison.OrdinalIgnoreCase));

                // 4️⃣ Output the result
                if (batesArtifact != null)
                {
                    Console.WriteLine($"Current Bates: {batesArtifact.Text}");
                }
                else
                {
                    Console.WriteLine("No Bates artifact found on page 2.");
                }
            }
            catch (Exception ex)
            {
                // Pro tip: Log the exception details for troubleshooting
                Console.Error.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

**Объяснение дополнительных частей:**  

* **Проверка границ** — Мы проверяем `pageIndex` относительно `doc.Pages.Count`, чтобы избежать сбоев в коротких документах.  
* **Блок try‑catch** — Перехватывает ошибки доступа к файлам, проблемы с правами или специфические исключения SDK, предоставляя чистое сообщение об ошибке вместо необработанного сбоя.  
* **Комментарии** — Встроенные комментарии (`// 1️⃣`) служат визуальными якорями; они полезны для новичков, просматривающих код.

### 6. Распространённые варианты и граничные случаи  

| Ситуация | Как адаптировать код |
|-----------|-----------------------|
| **Несколько номеров Bates на одной странице** | Используйте `Where(...).Select(a => a.Text)`, чтобы получить все совпадения, затем переберите их или объедините. |
| **Вам нужна страница 5 вместо страницы 2** | Измените `int pageIndex = 4;` (помните, нумерация с нуля). |
| **Документ использует другой подтип артефакта (например, “Comment”)** | Замените `"Bates"` на `"Comment"` в предикате `FirstOrDefault`. |
| **Производительность при работе с большими документами** | Загружайте только необходимую страницу, используя `Document.LoadPage(pageIndex)`, если SDK поддерживает ленивую загрузку. |
| **Запуск на .NET Core в Linux** | Убедитесь, что установлены нативные зависимости GroupDocs.Annotation (`libgdiplus` для рендеринга изображений). |

### 7. Советы и подводные камни  

* **Pro tip:** Если вы обрабатываете множество документов пакетно, переиспользуйте один экземпляр лицензии `Annotation`, чтобы избежать повторных проверок лицензии.  
* **Watch out for:** Word‑файлы, содержащие скрытые разделы (например, сноски

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}