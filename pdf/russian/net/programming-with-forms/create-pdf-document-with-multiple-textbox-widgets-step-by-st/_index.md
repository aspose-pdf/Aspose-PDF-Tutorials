---
category: general
date: 2026-02-12
description: Создайте PDF‑документ и добавьте пустую страницу PDF при построении поля
  формы — быстро научитесь добавлять виджеты текстовых полей PDF в C#.
draft: false
keywords:
- create pdf document
- add blank page pdf
- create pdf form field
- how to create pdf form
- how to add textbox pdf
language: ru
og_description: Создайте PDF‑документ с пустой страницей и несколькими виджетами текстовых
  полей. Следуйте этому руководству, чтобы узнать, как добавить текстовые поля PDF
  с помощью Aspose.Pdf.
og_title: Создать PDF‑документ – добавить виджеты TextBox в C#
tags:
- pdf
- csharp
- aspose
- form-fields
title: Создание PDF‑документа с несколькими виджетами TextBox – пошаговое руководство
url: /ru/net/programming-with-forms/create-pdf-document-with-multiple-textbox-widgets-step-by-st/
---

" is part of the tutorial, but it's a phrase to translate? The instruction: translate all text content naturally to Russian, but keep technical terms in English. "create pdf document" is a phrase but includes "pdf". Probably translate to Russian but keep "pdf". So "создать PDF‑документ". The bold phrase should be translated: **создать PDF‑документ**. Similarly **how to add textbox pdf** keep as phrase but translate: **как добавить textbox pdf**? But "textbox pdf" is technical term; maybe keep as is. We'll translate the surrounding text.

Let's produce translation.

Proceed.

We'll keep code block placeholders unchanged.

Also need to translate bullet points, list items.

Let's craft final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF‑документа с несколькими виджетами TextBox – Полный учебник

Когда‑нибудь вам нужно было **создать PDF‑документ**, содержащий форму с более чем одним виджетом TextBox? Вы не одиноки — разработчики часто спрашивают: *«как добавить textbox pdf‑поля, которые отображаются в двух местах?»* Хорошая новость в том, что Aspose.Pdf делает это проще простого. В этом руководстве мы пройдемся по созданию PDF, добавлению пустой страницы PDF, построению поля формы и, наконец, покажем **как добавить textbox pdf** виджеты программно.

Мы охватим всё, что вам нужно знать: от инициализации документа до сохранения конечного файла. К концу вы получите готовый к использованию PDF, демонстрирующий **как создать pdf form** элементы с несколькими виджетами, и поймёте небольшие нюансы, которые делают форму надёжной во всех PDF‑просмотрщиках.

## Что вам понадобится

- **Aspose.Pdf for .NET** (любая актуальная версия; используемый API работает с 23.x и новее).  
- Среда разработки .NET (Visual Studio, Rider или даже VS Code с расширением C#).  
- Базовое знакомство с синтаксисом C# — глубокие знания PDF не требуются.

Если все пункты отмечены, приступаем.

## Шаг 1: Создание PDF‑документа – инициализация и добавление пустой страницы

Первое, что мы делаем, — **создать pdf document** объект и предоставить ему чистый холст. Добавление пустой страницы PDF так же просто, как вызов `Pages.Add()`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

public class MultiWidgetExample
{
    public static void Main()
    {
        // Step 1: Create a new PDF document (the canvas)
        using (var pdfDocument = new Document())
        {
            // Step 2: Add a blank page pdf to the document
            var pdfPage = pdfDocument.Pages.Add();

            // The rest of the steps follow...
```

*Почему это важно:* Класс `Document` представляет весь файл. Без страницы некуда помещать поля формы, поэтому пустая страница PDF является фундаментом любой формы, которую вы будете строить.

## Шаг 2: Создание PDF‑формы – определение TextBox, способного содержать несколько виджетов

Теперь мы создаём фактическое **create pdf form field**. Aspose называет его `TextBoxField`. Установка `MultipleWidgets = true` сообщает движку, что это поле может появляться более одного раза.

```csharp
            // Step 3: Create a TextBox field that supports multiple widgets
            var multiWidgetTextBox = new TextBoxField(
                pdfPage,
                new Rectangle(50, 700, 250, 730)); // position on the first page
            multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
            multiWidgetTextBox.Value = "First widget";
```

*Совет профессионала:* Координаты прямоугольника задаются в пунктах (1 pt = 1/72 in). Подгоните их под ваш макет; в примере поле размещено рядом с верхним левым углом.

## Шаг 3: Добавление первого виджета в форму

После определения поля мы привязываем его к коллекции форм документа. Это шаг **how to add textbox pdf** для основного виджета.

```csharp
            // Step 4: Add the TextBox field to the form (first widget)
            pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);
```

Третий аргумент (`1`) — индекс виджета, начинающийся с 1, потому что уже есть виджет на странице, созданной на предыдущем шаге.

## Шаг 4: Программное добавление второго виджета – реальная сила нескольких виджетов

Если вы когда‑нибудь задумывались **how to create pdf form** элементы, которые повторяются, здесь происходит магия. Мы создаём `WidgetAnnotation` и добавляем его в коллекцию `Widgets` поля.

```csharp
            // Step 5: Create and attach a second widget programmatically
            var secondWidget = new WidgetAnnotation(
                new Rectangle(300, 700, 500, 730)); // position on the same page
            multiWidgetTextBox.Widgets.Add(secondWidget);
```

*Зачем нужен второй виджет?* Пользователям может потребоваться вводить одно и то же значение в двух местах — представьте поле «Имя клиента», которое появляется в верхней части формы и ещё раз в блоке подписи. Используя одно и то же имя поля (`MultiTB`), любое изменение в одном месте автоматически обновляет другое.

## Шаг 5: Сохранение PDF – проверка появления обоих виджетов

Наконец, мы записываем документ на диск. Файл будет содержать два синхронных виджета TextBox.

```csharp
            // Step 6: Save the PDF with both widgets
            pdfDocument.Save("multiWidget.pdf");
        }
    }
}
```

Когда вы откроете `multiWidget.pdf` в Adobe Acrobat, Foxit или даже в браузерном PDF‑просмотрщике, вы увидите два текстовых поля рядом. Ввод в одно мгновенно обновляет другое — доказательство того, что мы успешно **how to add textbox pdf** с несколькими виджетами.

### Ожидаемый результат

- Одностраничный PDF с именем `multiWidget.pdf`.  
- Два виджета TextBox с подписью «First widget».  
- Оба поля используют одно и то же имя, поэтому их содержимое зеркалируется.

![Create PDF document with multiple textbox widgets](https://example.com/images/multi-widget.png "Create PDF document example")

*Текст альтернативы изображения:* create pdf document showing two textbox widgets

## Часто задаваемые вопросы и особые случаи

### Можно ли разместить виджеты на разных страницах?

Конечно. Просто создайте новый объект `Page` для второго виджета и используйте его координаты. Поле останется связанным, потому что имя (`"MultiTB"`) остаётся тем же.

```csharp
var secondPage = pdfDocument.Pages.Add();
var thirdWidget = new WidgetAnnotation(new Rectangle(50, 700, 250, 730));
multiWidgetTextBox.Widgets.Add(thirdWidget);
```

### Что если нужен разный значение по умолчанию для каждого виджета?

Свойство `Value` применяется ко всему полю, а не к отдельным виджетам. Если нужны разные значения по умолчанию, придётся создавать отдельные поля вместо использования `MultipleWidgets`.

### Работает ли это с соответствием PDF/A или PDF/UA?

Да, но после добавления полей формы может потребоваться установить дополнительные свойства документа (например, `pdfDocument.ConvertToPdfA()`). Связь виджетов остаётся неизменной.

## Полный рабочий пример (готов к копированию)

Ниже представлен полностью готовый к запуску код. Просто вставьте его в консольный проект, добавьте ссылку на пакет Aspose.Pdf через NuGet и нажмите **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

namespace AsposePdfMultiWidget
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Add a blank page pdf
                var pdfPage = pdfDocument.Pages.Add();

                // Create a TextBox field that can contain multiple widgets
                var multiWidgetTextBox = new TextBoxField(
                    pdfPage,
                    new Rectangle(50, 700, 250, 730));
                multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
                multiWidgetTextBox.Value = "First widget";

                // Add the TextBox field to the form (first widget)
                pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);

                // Create and attach a second widget programmatically
                var secondWidget = new WidgetAnnotation(
                    new Rectangle(300, 700, 500, 730));
                multiWidgetTextBox.Widgets.Add(secondWidget);

                // Save the PDF with both widgets
                pdfDocument.Save("multiWidget.pdf");
            }
        }
    }
}
```

Запустите программу и откройте `multiWidget.pdf`. Вы увидите два синхронных текстовых поля — именно то, что вы искали, задавая вопрос **how to create pdf form** с несколькими записями.

## Итоги и дальнейшие шаги

Мы только что прошли процесс **create pdf document**, добавления **blank page pdf**, определения **create pdf form field** и, наконец, ответили на вопрос **how to add textbox pdf** виджетов, которые делятся данными. Основная идея в том, что одно имя поля может быть отрисовано несколько раз, предоставляя гибкие макеты форм без дополнительного кода.

Хотите идти дальше? Попробуйте следующие идеи:

- **Стилизовать textbox** — измените цвет границы, фон или шрифт с помощью свойств `TextBoxField`.  
- **Добавить валидацию** — используйте JavaScript‑действия (`TextBoxField.Actions.OnValidate`) для проверки форматов.  
- **Комбинировать с другими полями** — добавьте флажки, переключатели или цифровые подписи, чтобы построить полнофункциональную форму.  
- **Экспортировать данные формы** — вызовите `pdfDocument.Form.ExportFields()` для получения пользовательского ввода в виде JSON или XML.

Все эти возможности опираются на тот же фундамент, который мы рассмотрели, так что вы готовы создавать сложные PDF‑формы для счетов, контрактов, опросов или любых других бизнес‑задач.

---

*Счастливого кодинга! Если возникнут трудности, оставьте комментарий ниже или изучите документацию Aspose.Pdf для более глубокого погружения. Помните, лучший способ освоить генерацию PDF — экспериментировать, поэтому меняйте координаты, добавляйте новые виджеты и наблюдайте, как ваша форма оживает.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}