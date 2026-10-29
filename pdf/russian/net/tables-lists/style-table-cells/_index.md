---
title: Настройте фон, границы и отступы ячеек таблицы в PDF с помощью Aspose.Pdf for .NET
weight: 101
limit:
description: Узнайте, как создать PDF с таблицей из двух столбцов и применить пользовательские цвета фона, границы и отступы к каждой ячейке, используя Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Узнайте, как создать PDF с таблицей из двух столбцов и применить пользовательские
    цвета фона, границы и отступы к каждой ячейке, используя Aspose.Pdf for .NET.
  headline: Настройте фон, границы и отступы ячеек таблицы в PDF с помощью Aspose.Pdf
    for .NET
  type: TechArticle
- description: Узнайте, как создать PDF с таблицей из двух столбцов и применить пользовательские
    цвета фона, границы и отступы к каждой ячейке, используя Aspose.Pdf for .NET.
  name: Настройте фон, границы и отступы ячеек таблицы в PDF с помощью Aspose.Pdf
    for .NET
  steps:
  - name: Создайте новый пустой PDF‑документ внутри блока using.
    text: Создайте новый пустой PDF‑документ внутри блока using.
  - name: Добавьте пустую страницу в PDF‑документ.
    text: Добавьте пустую страницу в PDF‑документ.
  - name: Создайте объект Table с двумя колонками по 200 пунктов, тонкой чёрной внешней
      границей и отступом ячейки по умолчанию 5 пунктов.
    text: Создайте объект Table с двумя колонками по 200 пунктов, тонкой чёрной внешней
      границей и отступом ячейки по умолчанию 5 пунктов.
  - name: Добавьте первую строку в таблицу.
    text: Добавьте первую строку в таблицу.
  - name: Создайте первую ячейку, вставьте текст "First cell", задайте светло‑желтый
      фон, красную границу толщиной 2 пункта и отступ 4 пункта.
    text: Создайте первую ячейку, вставьте текст "First cell", задайте светло‑желтый
      фон, красную границу толщиной 2 пункта и отступ 4 пункта.
  - name: Создайте вторую ячейку, добавьте текст "Second cell", задайте светло‑зеленый
      фон, синюю границу толщиной 2 пункта и отступ 4 пункта.
    text: Создайте вторую ячейку, добавьте текст "Second cell", задайте светло‑зеленый
      фон, синюю границу толщиной 2 пункта и отступ 4 пункта.
  - name: Добавьте вторую строку в таблицу.
    text: Добавьте вторую строку в таблицу.
  - name: Создайте третью ячейку, вставьте "Third cell", задайте светло‑голубой фон,
      темно‑серую границу толщиной 2 пункта и отступ 4 пункта.
    text: Создайте третью ячейку, вставьте "Third cell", задайте светло‑голубой фон,
      темно‑серую границу толщиной 2 пункта и отступ 4 пункта.
  - name: Создайте четвертую ячейку, добавьте "Fourth cell", задайте светло‑розовый
      фон, пурпурную границу толщиной 2 пункта и отступ 4 пункта.
    text: Создайте четвертую ячейку, добавьте "Fourth cell", задайте светло‑розовый
      фон, пурпурную границу толщиной 2 пункта и отступ 4 пункта.
  - name: Добавьте полностью оформленную таблицу на страницу, чтобы она стала видна
      в PDF.
    text: Добавьте полностью оформленную таблицу на страницу, чтобы она стала видна
      в PDF.
  - name: Сохраните PDF‑документ в файл и закройте блок using.
    text: Сохраните PDF‑документ в файл и закройте блок using.
  - name: Выведите подтверждающее сообщение в консоль.
    text: Выведите подтверждающее сообщение в консоль.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` задаёт базовый отступ для каждой ячейки, но если
      вы назначаете `Margin` (например, `cellA1.Margin = new MarginInfo(...)`), значения
      отступа переопределяют отступ по умолчанию для этой конкретной ячейки.'
    question: Влияет ли `DefaultCellPadding`, установленный для `Table`, на ячейки,
      у которых также определён `Margin`?
  - answer: Без `Table.Border` внешний прямоугольник вокруг всей таблицы не будет
      отображаться; видимыми останутся только отдельные границы ячеек, которые вы
      задаёте (например, `cellA2.Border`).
    question: Как будет выглядеть PDF, если я удалю свойство `Border` у объекта `Table`?
  - answer: Да, создайте `BorderInfo` с конкретным `BorderSide` (например, `new BorderInfo(BorderSide.Left,
      3, Aspose.Pdf.Color.Black)`) и присвойте его свойству `Border` ячейки.
    question: Могу ли я задать ячейке разную толщину границы по каждому краю?
  - answer: Создайте новый `Row` с помощью `Row newRow = dataTable.Rows.Add();`, а
      затем добавьте ячейки в `newRow.Cells` так же, как в предыдущих строках.
    question: Как добавить третью строку в таблицу после показанного кода?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: Оформление ячеек таблицы PDF – фон, граница, отступы
og_description: Быстро форматируйте ячейки таблицы в PDF с помощью пользовательских цветов, границ и интервалов, используя Aspose.Pdf for .NET.
og_image_alt: Руководство, показывающее, как оформить цвет фона, границу и отступы ячеек таблицы в PDF с помощью Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Настройте фон, границы и отступы ячеек таблицы в PDF с помощью Aspose.Pdf
В этом учебнике вы увидите, как создать PDF‑документ, добавить таблицу из двух столбцов и точно управлять внешним видом каждой ячейки. Устанавливая цвета фона, определяя границы и регулируя отступы, вы можете выделить данные таблицы и придать им аккуратный вид. В примере используются классы Aspose.Pdf Document и Table для демонстрации каждой опции оформления.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


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

**Q: Влияет ли `DefaultCellPadding`, установленный для `Table`, на ячейки, у которых также определён `Margin`?**  
A: `DefaultCellPadding` задаёт базовый отступ для каждой ячейки, но если вы назначаете `Margin` (например, `cellA1.Margin = new MarginInfo(...)`), значения отступа переопределяют отступ по умолчанию для этой конкретной ячейки.

**Q: Как будет выглядеть PDF, если я удалю свойство `Border` у объекта `Table`?**  
A: Без `Table.Border` внешний прямоугольник вокруг всей таблицы не будет отображаться; видимыми останутся только отдельные границы ячеек, которые вы задаёте (например, `cellA2.Border`).

**Q: Могу ли я задать ячейке разную толщину границы по каждому краю?**  
A: Да, создайте `BorderInfo` с конкретным `BorderSide` (например, `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) и присвойте его свойству `Border` ячейки.

**Q: Как добавить третью строку в таблицу после показанного кода?**  
A: Создайте новый `Row` с помощью `Row newRow = dataTable.Rows.Add();`, а затем добавьте ячейки в `newRow.Cells` так же, как в предыдущих строках.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}