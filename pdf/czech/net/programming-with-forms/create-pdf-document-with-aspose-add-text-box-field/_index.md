---
category: general
date: 2026-03-24
description: Vytvořte PDF dokument pomocí Aspose.PDF v C#. Naučte se, jak rychle přidat
  textové pole PDF formuláře a přidat pole formuláře PDF.
draft: false
keywords:
- create pdf document
- add text box pdf
- add form field pdf
- how to create pdf
- how to add textbox
language: cs
og_description: Vytvořte PDF dokument pomocí Aspose.PDF v C#. Tento průvodce ukazuje,
  jak během několika minut přidat textové pole PDF formuláře a přidat pole formuláře
  PDF.
og_title: Vytvořte PDF dokument pomocí Aspose – Přidejte textové pole
tags:
- Aspose.PDF
- C#
- PDF Forms
title: Vytvořte PDF dokument pomocí Aspose – Přidejte textové pole
url: /cs/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF dokumentu pomocí Aspose – Přidání textového pole

Už jste někdy potřebovali **vytvořit PDF dokument** programově a přemýšleli, kde začít? Nejste v tom sami – mnoho vývojářů narazí na tuto překážku, když jejich aplikace musí sbírat vstup od uživatele bez nasazení těžké UI knihovny. Dobrá zpráva? S Aspose.PDF pro .NET můžete vytvořit PDF, umístit textové pole na libovolnou stránku a dokonce připojit stejné pole k více stránkám – vše během několika řádků.

V tomto tutoriálu projdeme celý proces: od inicializace PDF, přes **add text box PDF** formulářová pole, až po **add form field PDF** registraci, a nakonec jak ověřit, že vše funguje. Na konci budete vědět **how to create PDF** soubory, které jsou interaktivní, a také uvidíte **how to add textbox** ovládací prvky, které se chovají přesně jako nativní pole v Acrobat.

---

## Co budete potřebovat

- **ASP.NET Core** nebo jakýkoli projekt .NET 6+ (kód funguje také na .NET Framework 4.6+).  
- **Aspose.PDF for .NET** NuGet balíček (verze 23.9 nebo novější).  
- Mírné zkušenosti s C# – nic složitého, jen základy.  

Pokud máte tyto položky zaškrtnuté, můžete začít. Žádné extra nástroje, žádné externí služby, jen čistý C# kód, který můžete vložit do konzolové aplikace a spustit.

---

## Vytvoření PDF dokumentu a přidání textového pole formuláře

Prvním krokem, jak už to napovídá, je **create PDF document**. Představte si třídu `Document` jako prázdné plátno; jakmile ji máte, můžete začít kreslit stránky, tvary a interaktivní prvky.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (the blank canvas)
using var document = new Document();

// Step 2: Add a new page where the text box will live
var page1 = document.Pages.Add();
```

> **Why this matters:** Vytvoření instance `Document` bez jakýchkoli stránek vyvolá výjimku v okamžiku, kdy se pokusíte umístit widget. Přidání stránky nejprve zaručuje platný index stránky (`Pages[1]`) pro další kroky.

---

## Přidání textového pole PDF formuláře na stránku 1

Nyní, když máme stránku, pojďme **add text box PDF** formulářové pole. Třída `TextBoxField` představuje jediné logické pole; můžete si ji představit jako „název“ vstupu, který se může objevit na mnoha místech.

```csharp
// Step 3: Define the rectangle where the textbox will appear (x, y, width, height)
var textBoxRect = new Rectangle(100, 500, 300, 520);

// Step 4: Create the text box field on page 1
var textBoxField = new TextBoxField(document.Pages[1], textBoxRect)
{
    // This logical name is used later when you retrieve the value
    PartialName = "MultiWidget"
};
```

> **Pro tip:** Obdélník používá jednotky point (1/72 palce). Přizpůsobte souřadnice tak, aby odpovídaly vašemu rozvržení; počátek (0,0) je v levém dolním rohu stránky.

---

## Vytvoření druhého widgetu na další stránce

Jedno logické pole může mít více vizuálních widgetů – ideální pro více‑stránkové formuláře. Zde je **how to add textbox** na druhé stránce, s opětovným použitím stejného názvu pole.

```csharp
// Step 5: Add a second page for the extra widget
var page2 = document.Pages.Add();

// Step 6: Create a widget for the same field on page 2
var secondWidget = textBoxField.CreateWidget(new Rectangle(100, 400, 300, 420));
```

> **Why we do this:** Uživatelé často potřebují vyplnit stejné informace v různých sekcích (např. „Jméno“ nahoře a znovu v souhrnu). Sdílením logického názvu Aspose zajistí, že oba widgety zůstanou synchronizované.

---

## Registrace formulářového pole v PDF

Vytvoření objektu pole není dostačující; musíte jej přidat do kolekce formulářů dokumentu. Toto je krok, kde **add form field PDF** do interní struktury.

```csharp
// Step 7: Register the field (with both widgets) in the document's form collection
document.Form.Add(textBoxField, "MultiWidget");

// Optional: Save the PDF to disk
document.Save("MultiWidgetExample.pdf");
```

> **What happens under the hood:** `Form.Add` zapíše definici pole do slovníku AcroForm, což umožní PDF být interaktivní při otevření v Acrobat Readeru nebo jakémkoli prohlížeči PDF, který podporuje formuláře.

---

## Spuštění a ověření výsledku

Zkompilujte a spusťte konzolovou aplikaci. Otevřete `MultiWidgetExample.pdf` v Adobe Acrobat (nebo v jakémkoli prohlížeči podporujícím formuláře) a uvidíte dvě identické textové pole na stránkách 1 a 2. Napište něco do jednoho pole – druhé se okamžitě aktualizuje. To je síla sdíleného logického pole.

```text
Expected outcome:
- PDF with two pages.
- Each page shows a white rectangle (the text box).
- Editing one box updates the other automatically.
```

Pokud nevidíte pole, zkontrolujte, že obdélníky jsou uvnitř hranic stránky a že jste dokument uložili po přidání pole.

---

## Časté otázky a okrajové případy

### Co když potřebuji odlišný vzhled na každé stránce?

Můžete si přizpůsobit každý widget po vytvoření:

```csharp
secondWidget.Rect = new Rectangle(150, 350, 350, 370); // reposition
secondWidget.Border = new Border(BorderStyle.Solid, 1, Color.Black);
secondWidget.BackgroundColor = Color.LightYellow;
```

### Mohu nastavit výchozí hodnotu?

Jistě – stačí přiřadit `Value` před uložením:

```csharp
textBoxField.Value = "Enter your name here";
```

Všechna widgety zobrazí tuto výplň, dokud ji uživatel nepřepíše.

### Jak nastavit pole jako povinné?

```csharp
textBoxField.Required = true;
```

Acrobat varuje uživatele, pokud se pokusí odeslat formulář bez vyplnění pole.

### Funguje to s kompatibilitou PDF/A?

Aspose.PDF podporuje PDF/A‑1b,‑2b,‑3b. Po dokončení tvorby formuláře můžete převést:

```csharp
document.Convert(new PdfConversionOptions { Compliance = PdfCompliance.PdfA2b });
```

---

## Úplný funkční příklad

Níže je kompletní program připravený ke zkopírování a vložení. Uložte jej jako `Program.cs` v .NET konzolovém projektu, přidejte NuGet balíček Aspose.PDF a spusťte.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var document = new Document();

        // 2️⃣ Add two pages (page 1 will host the first widget, page 2 the second)
        var page1 = document.Pages.Add();
        var page2 = document.Pages.Add();

        // 3️⃣ Define the rectangle for the first widget
        var rect1 = new Rectangle(100, 500, 300, 520);

        // 4️⃣ Create the text box field (logical name = "MultiWidget")
        var textBoxField = new TextBoxField(document.Pages[1], rect1)
        {
            PartialName = "MultiWidget",
            Value = "Sample text",        // optional default value
            Required = true               // makes the field mandatory
        };

        // 5️⃣ Add a second widget on page

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}