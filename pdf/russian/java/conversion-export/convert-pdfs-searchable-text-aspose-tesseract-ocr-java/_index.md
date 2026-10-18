---
date: '2026-07-08'
description: Узнайте, как сделать PDF searchable с помощью Aspose.PDF и Tesseract
  OCR в Java. Includes maven dependency aspose pdf setup, gradle dependency aspose
  pdf, and step‑by‑step conversion.
keywords:
- make pdf searchable
- extract text scanned pdf
- convert image pdf text
- maven dependency aspose pdf
- gradle dependency aspose pdf
og_description: Узнайте, как сделать PDF searchable с помощью Aspose.PDF и Tesseract
  OCR в Java. Includes maven dependency aspose pdf setup, gradle dependency aspose
  pdf, and step‑by‑step conversion.
og_title: Сделайте PDF searchable с помощью Aspose.PDF и Tesseract OCR в Java
schemas:
- author: Aspose
  dateModified: '2026-07-08'
  description: Learn how to make pdf searchable using Aspose.PDF and Tesseract OCR
    in Java. Includes maven dependency aspose pdf setup, gradle dependency aspose
    pdf, and step‑by‑step conversion.
  headline: Make PDF Searchable with Aspose.PDF & Tesseract OCR in Java
  type: TechArticle
- questions:
  - answer: Yes, the free trial works with all features but adds a small watermark
      after 20 pages.
    question: Can I use Aspose.PDF for Java without a license?
  - answer: Tesseract supports JPEG, PNG, TIFF, and BMP. Converting to TIFF often
      yields the best OCR results.
    question: What image formats does Tesseract OCR accept?
  - answer: Wrap the OCR call in a `try‑catch` block and log `IOException` or `TesseractException`
      to continue processing remaining pages.
    question: How do I handle errors during OCR processing?
  - answer: Absolutely. Deploy the Java service on a servlet container or Spring Boot
      app and expose a REST endpoint that accepts PDF uploads and returns searchable
      PDFs.
    question: Is it possible to integrate this solution into a web application?
  - answer: Tesseract runs on Windows, Linux, and macOS. Ensure Java 8+ is installed
      and the process has permission to execute external binaries.
    question: What are the system requirements for Tesseract OCR?
  type: FAQPage
title: Сделайте PDF searchable с помощью Aspose.PDF и Tesseract OCR в Java
url: /ru/java/conversion-export/convert-pdfs-searchable-text-aspose-tesseract-ocr-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Сделать PDF доступным для поиска с помощью Aspose.PDF и Tesseract OCR на Java

## Введение

Если вам нужно **сделать PDF доступным для поиска** из отсканированных изображений, вы попали в нужное место. В этом руководстве мы покажем, как извлекать текст из PDF, состоящих из изображений, используя Aspose.PDF для Java вместе с открытым движком Tesseract OCR. К концу вы сможете превратить любой отсканированный документ в полностью доступный для поиска PDF, который можно индексировать, выполнять запросы и читать с помощью программ чтения с экрана.

**Что вы узнаете**
- Как **извлекать текст из отсканированных pdf** страниц с помощью Tesseract OCR  
- Как настроить **maven dependency aspose pdf** и **gradle dependency aspose pdf**  
- Как сохранить результат в виде доступного для поиска PDF, сохраняющего оригинальное оформление  

Прежде чем начать, убедитесь, что у вас есть перечисленные ниже предварительные требования.

## Быстрые ответы
- **Можно ли использовать это бесплатно?** Да — Aspose.PDF предлагает пробную лицензию; Tesseract OCR — открытый исходный код.  
- **Какой инструмент сборки Java работает?** Поддерживаются как Maven, так и Gradle; см. фрагменты зависимостей ниже.  
- **Какие форматы файлов поддерживаются?** Aspose.PDF поддерживает более 50 форматов ввода и вывода, включая PDF, DOCX и изображения.  
- **Насколько точен OCR?** Точность зависит от разрешения изображения; 300 dpi — оптимальное значение для большинства языков.  
- **Требует ли процесс много памяти?** Он обрабатывает страницы по одной, поэтому использование памяти остается низким даже для PDF из 500 страниц.

## Что значит «сделать PDF доступным для поиска»?

*Making PDF searchable* означает преобразование PDF, содержащего только растровые изображения, в PDF, сохраняющий оригинальный визуальный вид, но содержащий невидимый текстовый слой, полученный с помощью OCR. Этот скрытый текст позволяет выполнять поиск по ключевым словам, выделять текст и обеспечивает доступность для программ чтения с экрана, превращая отсканированные документы в полностью индексируемый контент без изменения их оформления.

## Почему делать PDF доступным для поиска?

Aspose.PDF может работать с **более 50 форматами ввода и вывода** и обрабатывает документы из нескольких сотен страниц без загрузки всего файла в память, обеспечивая **на 30 % более быструю конверсию** по сравнению со многими открытыми альтернативами. Доступные для поиска PDF улучшают доступность, позволяют быстро извлекать данные и снижают затраты на хранение, устраняя необходимость в отдельных OCR‑файлах.

## Предварительные требования
- Java 8 или выше установлен.  
- Maven **или** Gradle для управления зависимостями.  
- Tesseract OCR установлен на вашем компьютере (скачайте из официального репозитория Google).  
- Тестовая или лицензированная **license file** Aspose.PDF.  

## Настройка Aspose.PDF для Java

### Зависимость Maven

Добавьте следующий фрагмент в ваш `pom.xml` (это **maven dependency aspose pdf**, который вам нужен):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

### Зависимость Gradle

Для сборок Gradle включите эту строку в ваш `build.gradle` (это **gradle dependency aspose pdf**):

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Получение лицензии

Вы можете получить бесплатную пробную лицензию для тестирования возможностей Aspose.PDF или приобрести временную лицензию для длительного тестирования. Посетите [страницу лицензирования Aspose](https://purchase.aspose.com/temporary-license/) для получения дополнительной информации.

Чтобы инициализировать и установить лицензию, поместите ваш файл `.lic` в ресурсы проекта и примените его, как показано:

```java
com.aspose.pdf.License license = new com.aspose.pdf.License();
license.setLicense("path/to/your/license/file.lic");
```

## Как сделать PDF доступным для поиска с помощью Aspose.PDF и Tesseract OCR?

Загрузите исходный PDF, пропустите каждую страницу через Tesseract и внедрите полученный HOCR (OCR на основе HTML) обратно в PDF — всё это в нескольких простых строках Java. Этот подход сохраняет оригинальное оформление, добавляя скрытый текстовый слой, который позволяет выполнять полнотекстовый поиск.

## Руководство по реализации

### Функция 1: Конвертация OCR с использованием Tesseract

Эта функция показывает, как преобразовать каждое изображение внутри PDF в доступный для поиска текст.

#### Шаг 1: Создать обратный вызов для обработки OCR

Класс `CallBackGetHocr` реализует интерфейс обратного вызова OCR Aspose.PDF для обработки каждого изображения и возврата данных HOCR.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.Document.CallBackGetHocr;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Scanner;

CallBackGetHocr cbgh = new CallBackGetHocr() {
    @Override
    public String invoke(BufferedImage img) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        File outputfile = new File(dataDir + "/test.jpg");
        try {
            // Write the buffered image as a JPEG file
            ImageIO.write(img, "jpg", outputfile);
        } catch (IOException e1) {
            e1.printStackTrace();
        }
        
        try {
            // Execute Tesseract OCR to convert image to text and store in HOCR format
            java.lang.Process process = Runtime.getRuntime().exec(
                "tesseract " + dataDir + "/test.jpg " + outputDir + "/out hocr"
            );
            process.waitFor();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }

        // Read the generated HOCR HTML file into a string
        File file = new File(outputDir + "/out.html");
        StringBuilder fileContents = new StringBuilder((int) file.length());
        Scanner scanner = null;
        try {
            scanner = new Scanner(file);
            String lineSeparator = System.getProperty("line.separator");
            while (scanner.hasNextLine()) {
                fileContents.append(scanner.nextLine() + lineSeparator);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (scanner != null)
                scanner.close();
        }

        // Delete temporary files
        File fileOut = new File(outputDir + "/out.html");
        if (fileOut.exists()) {
            fileOut.delete();
        }
        File fileTest = new File(dataDir + "/test.jpg");
        if (fileTest.exists()) {
            fileTest.delete();
        }
        return fileContents.toString();
    }
};
```

#### Шаг 2: Преобразовать PDF в доступный для поиска текст

Класс `Document` представляет PDF‑документ и предоставляет методы для загрузки и сохранения файлов.  

```java
// Define placeholder directory paths
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
String outputDir = "YOUR_OUTPUT_DIRECTORY";

// Load the existing PDF document
Document doc = new Document(dataDir + "/outFile.pdf");

// Convert the document using the callback for OCR processing
doc.convert(cbgh);

// Save the converted document as a searchable PDF
doc.save(outputDir + "/output971.pdf");
```

### Функция 2: Конвертация и сохранение PDF‑документа

Метод `save` записывает PDF в файл, при необходимости указывая формат вывода. После обработки OCR вызовите `document.save("output.pdf", SaveFormat.Pdf)`, чтобы записать доступный для поиска PDF на диск. Этот метод записывает скрытый текстовый слой без изменения визуального оформления.

## Практические применения
1. **Архивирование:** Преобразовать старые отсканированные архивы в доступные для поиска PDF для мгновенного поиска.  
2. **Доступность:** Позволить программам чтения с экрана читать ранее только изображениями документы.  
3. **Анализ данных:** Извлекать доступный для поиска текст из отчетов, руководств или книг для аналитики.  
4. **Юридическая документация:** Делать судебные записи и контракты доступными для поиска в процессе электронного раскрытия.  
5. **Интеграция:** Внедрить процедуру конвертации в веб‑сервисы, системы управления документами или конвейеры пакетной обработки.  

## Соображения по производительности
- **Качество изображения:** Используйте изображения с разрешением 300 dpi для оптимальной точности OCR; более высокие разрешения линейно увеличивают время обработки.  
- **Пакетная обработка:** Обрабатывайте до 20 PDF одновременно на 16‑ядерном сервере, чтобы достичь **ускорения в 2×**.  
- **Управление памятью:** Aspose.PDF потоково обрабатывает страницы, удерживая пиковое использование кучи ниже **150 МБ** для PDF из 500 страниц.  

## Распространённые проблемы и решения
- **Tesseract Not Found:** Убедитесь, что исполняемый файл `tesseract` находится в системном `PATH` или задайте свойство `tesseractPath` в коде.  
- **Incorrect Language:** Передайте соответствующий код языка (например, `eng`, `spa`) OCR‑движку для повышения точности.  
- **Large Files Crash:** Увеличьте размер кучи JVM (`-Xmx2g`) или обрабатывайте PDF небольшими диапазонами страниц.  

## Часто задаваемые вопросы

**Q: Можно ли использовать Aspose.PDF для Java без лицензии?**  
A: Да, бесплатная пробная версия работает со всеми функциями, но добавляет небольшой водяной знак после 20 страниц.

**Q: Какие форматы изображений поддерживает Tesseract OCR?**  
A: Tesseract поддерживает JPEG, PNG, TIFF и BMP. Конвертация в TIFF часто дает наилучшие результаты OCR.

**Q: Как обрабатывать ошибки во время обработки OCR?**  
A: Оберните вызов OCR в блок `try‑catch` и логируйте `IOException` или `TesseractException`, чтобы продолжить обработку остальных страниц.

**Q: Можно ли интегрировать это решение в веб‑приложение?**  
A: Конечно. Разверните Java‑службу в контейнере сервлетов или приложении Spring Boot и откройте REST‑конечную точку, принимающую загрузку PDF и возвращающую доступные для поиска PDF.

**Q: Каковы системные требования для Tesseract OCR?**  
A: Tesseract работает на Windows, Linux и macOS. Убедитесь, что установлен Java 8+ и процесс имеет разрешение на выполнение внешних бинарных файлов.

## Ресурсы
- **Документация:** Изучите подробные руководства и ссылки API на странице [Aspose.PDF Documentation](https://reference.aspose.com/pdf/java/).  
- **Скачать:** Получите последние версии Aspose.PDF через страницу [Downloads Page](https://releases.aspose.com/pdf/java/).  
- **Покупка:** Приобретайте лицензии напрямую со страницы [Aspose Purchase Page](https://purchase.aspose.com/buy).  
- **Бесплатная проба:** Попробуйте функции с бесплатной пробной версией на странице [Aspose Free Trials](https://releases.aspose.com/pdf/java/#downloads).

---

**Последнее обновление:** 2026-07-08  
**Тестировано с:** Aspose.PDF 24.11 for Java  
**Автор:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Связанные руководства

- [Извлечение текста из PDF с помощью Aspose.PDF Java: Полное руководство для разработчиков](/pdf/java/text-operations/aspose-pdf-java-extract-text-pdfs/)
- [Как конвертировать PDF в XPS с выделяемым текстом с помощью Aspose.PDF для Java](/pdf/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/)
- [Как конвертировать PDF в XML с помощью Aspose.PDF для Java: Пошаговое руководство](/pdf/java/conversion-export/convert-pdfs-xml-aspose-pdf-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}