---
category: general
date: 2026-06-21
description: Vytvořte textové pole PDF pomocí C# a naučte se, jak duplikovat pole
  formuláře PDF nebo přidat textové pole do PDF formuláře během několika řádků kódu.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: cs
og_description: Rychle vytvořte textové pole v PDF. Tento návod ukazuje, jak duplikovat
  pole formuláře PDF a přidat textové pole do PDF formuláře pomocí moderní knihovny
  PDF pro C#.
og_title: Vytvořte PDF textové pole – kompletní C# tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Vytvoření PDF textového pole – krok za krokem
url: /cs/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření textového pole PDF – Kompletní C# tutoriál

Už jste někdy potřebovali **create PDF textbox field**, ale nebyli jste si jisti, které API volání použít? Nejste v tom sami. Ať už budujete portál pro podepisování smluv nebo jednoduchý formulář pro sběr dat, přidání interaktivních textových polí do PDF je základní dovednost pro každého vývojáře automatizace formulářů.  

V tomto průvodci projdeme praktickým příkladem, který nejen **adds textbox to PDF form**, ale také ukazuje, jak **duplicate PDF form field**, aby se stejný vstup objevil na více stránkách. Na konci budete mít spustitelný program, který můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- .NET 6.0 nebo novější (kód funguje také s .NET Core)  
- Moderní C# PDF knihovna – níže uvedený úryvek používá **PDFTron SDK**, ale koncepty lze přenést na iText 7, PdfSharp nebo jiné knihovny.  
- Visual Studio 2022 (nebo jakékoli IDE, které preferujete)  

To je vše – žádné extra služby, žádné nejasné závislosti. Pokud už máte PDF, které chcete rozšířit, stačí nasměrovat kód na něj.

---

## Krok 1: Nastavení projektu a import SDK

Nejprve vytvořte konzolovou aplikaci:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Přidejte NuGet balíček PDFTron:

```bash
dotnet add package PDFTron.NET
```

Nyní otevřete `Program.cs` a naimportujte potřebné jmenné prostory:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** Pokud používáte jinou knihovnu, nahraďte `using` direktivy ekvivalenty (např. `iText.Kernel.Pdf` pro iText 7).

## Krok 2: Inicializace PDF dokumentu a formuláře

Začneme s novým PDF, který obsahuje dvě stránky – zdrojovou stránku pro původní textové pole a cílovou stránku pro duplikát.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

Objekt `Form` je místem, kde žijí všechna interaktivní pole. Pokud dokument ještě neměl formulář, `GetForm()` jej vytvoří.

## Krok 3: **Create PDF Textbox Field** na první stránce

Nyní přichází jádro našeho tutoriálu – vytvoření textového pole. Souřadnice obdélníku jsou vyjádřeny v bodech (1 palec = 72 bodů). Příklad umisťuje pole blízko horního středu první stránky.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Proč nastavujeme `Value` okamžitě? Předvyplnění pole dává uživatelům náznak očekávaného vstupu a také ukazuje, že pole je plně funkční.

## Krok 4: Přidání pole do formuláře – **Add Textbox to PDF Form**

Dále registrujeme pole ve formuláři pomocí logického názvu. Tento název budete později používat, když budete potřebovat programově číst nebo měnit data pole.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Volba jasného názvu (např. `"multiBox"`) usnadní pozdější kód, zejména když máte desítky polí.

## Krok 5: **Duplicate PDF Form Field** na další stránce

Běžnou požadavkem je zobrazit stejné pole na více stránkách – představte si pole „Customer Name“, které se objevuje na každé stránce faktury. PDFTron nám umožňuje klonovat widget anotaci, což je vizuální reprezentace pole.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Klonovaný widget sdílí stejná podkladová data jako původní textové pole. Když uživatel napíše do jedné instance, druhá se automaticky aktualizuje – to je magie **duplicate PDF form field**.

## Krok 6: Uložení dokumentu a úklid

Nakonec zapíšeme PDF na disk a ukončíme runtime PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Spuštěním programu vznikne dvoustránkové PDF (`output.pdf`). Otevřete jej v Adobe Acrobat Reader, klikněte na textové pole na stránce 1, něco napište a poté přejděte na stránku 2 – stejný text se objeví okamžitě. Jedná se o plně funkční příklad **create pdf textbox field** s duplikovaným polem.

---

## Kompletní funkční příklad (připravený ke kopírování)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Očekávaný výstup:** Soubor pojmenovaný `output.pdf` obsahující dvě stránky. Obě stránky zobrazují stejné editovatelné textové pole s popiskem „Sample“. Úprava jednoho okamžitě aktualizuje druhé.

---

## Časté otázky a okrajové případy

### Co když potřebuji pole na *více* než dvou stránkách?

Jednoduše opakujte kroky klonování a přidání pro každou další stránku. Podkladový datový objekt zůstává stejný, takže všechny widgety jsou synchronizovány.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Jak změním vzhled (font, okraj, pozadí)?

Každý `Widget` má metody `SetBorderColor`, `SetBorderWidth` a `SetBackgroundColor`. Můžete také přiřadit řetězec výchozího vzhledu (`DA`) pro nastavení fontu a velikosti.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Můžu pole nastavit jako jen pro čtení po vyplnění uživatelem?

Ano. Nastavte příznak `ReadOnly` na poli po shromáždění dat, nebo jej přepínejte podle pracovního postupu.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Co s PDF, které již obsahují formulář?

Pokud dokument již má AcroForm, `doc.GetForm()` jej jednoduše vrátí. Pak můžete přidávat nová pole, aniž byste narušili existující. Jen buďte opatrní a používejte jedinečné názvy polí.

---

## Tipy pro reálné projekty

- **Naming convention:** Přidejte předponu názvům polí podle stránky nebo sekce (např. `invoice_customer_name`), aby nedocházelo ke kolizím.  
- **Validation:** Použijte JavaScript akce (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`), pokud potřebujete klientskou validaci.  
- **Performance:** Při práci s velkými PDF zavolejte `doc.Lock()` před hromadnými operacemi, aby se snížila zátěž I/O.  
- **Accessibility:** Nastavte vlastnost `AlternateName`, aby čtečky obrazovky mohly pole popsat.

---

## Závěr

Právě jsme **created a PDF textbox field**, ukázali, jak **duplicate PDF form field** napříč stránkami, a předvedli nejjednodušší způsob, jak **add textbox to PDF form** pomocí C#. Kompletní spustitelný kód je výše a můžete jej rozšířit o stylování, validaci nebo další stránky podle potřeby.

Jste připraveni na další krok? Zkuste vložit rozbalovací seznam (`ChoiceField`) nebo widget pro podpis, nebo prozkoumejte, jak po zadání dat formulář zploštit pro archivaci. PDFTron SDK (nebo jakákoli srovnatelná knihovna) vám poskytuje stavební bloky – vaše představivost určuje konečný tvar.

Pokud narazíte na problém, zanechte komentář níže nebo si prohlédněte oficiální dokumentaci knihovny; je plná příkladů, které doplňují to, co jsme zde pokryli. Šťastné programování a ať jsou vaše formuláře vždy synchronizované!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit PDF s Aspose – Přidat formulářové pole a stránky](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Přidat formulářové pole do PDF dokumentu pomocí Javy](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Přidat formulářové pole do PDF dokumentu pomocí Javy](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}