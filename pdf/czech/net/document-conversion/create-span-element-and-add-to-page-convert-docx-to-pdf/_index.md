---
category: general
date: 2026-03-27
description: Vytvořte element span v C# a naučte se, jak přidat span na stránku při
  převodu DOCX na PDF a uložení jako PDF. Krok za krokem průvodce pro vývojáře.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: cs
og_description: Vytvořte element span v C# a zjistěte, jak přidat span na stránku
  při převodu DOCX do PDF a následně jej uložit jako PDF. Kompletní příklad kódu je
  zahrnut.
og_title: Vytvořte span element a přidejte jej na stránku – Převést DOCX na PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Vytvořte span element a přidejte jej na stránku – Převod DOCX na PDF
url: /cs/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte element span a přidejte jej na stránku – Převod DOCX na PDF

Vytvoření **span element** v souboru DOCX je běžný úkol, když potřebujete přesnou kontrolu rozložení. V tomto tutoriálu vám ukážeme **jak přidat span** na stránku, **převést DOCX na PDF** a **uložit jako PDF**—vše během několika úhledných kroků.  

Pokud jste někdy zírali na dokument Word a pomysleli si: „Kéž bych mohl umístit malý textový rámeček na přesnou souřadnici,“ jste na správném místě. Provedeme vás celým pracovním postupem, od načtení zdrojového souboru až po získání vylepšeného PDF výstupu.

## Co dosáhnete

* Načtěte soubor `.docx` pomocí třídy `Document` z knihovny dokumentů.  
* **Create span element** pomocí API `TaggedContent`.  
* Umístěte tento span na přesné souřadnice X/Y na vybrané stránce.  
* **Add element to page** spolehlivě, i když stránka není první.  
* **Convert DOCX to PDF** a **save as PDF** jedním voláním `Save`.

Žádné externí nástroje, žádná tajemná nastavení—pouze čistý C# kód, který můžete zkopírovat‑vložit do svého projektu.

## Požadavky

* .NET 6+ (nebo jakýkoli recentní .NET runtime, který vaše knihovna podporuje).  
* SDK pro zpracování dokumentů, které poskytuje `Document`, `TaggedContent`, `Position` atd.  
* Základní pochopení syntaxe C#—pokud umíte napsat `Console.WriteLine`, jste v pořádku.

> **Pro tip:** Udržujte verzi SDK aktuální; poslední vydání (v3.2 k březnu 2026) obsahuje vylepšení výkonu pro operace na úrovni stránky.

---

![Diagram ukazující, jak vytvořit element span a umístit jej na stránku PDF](https://example.com/images/create-span-element.png "Diagram umístění elementu span")

## Vytvořte element span – Pozice a přidání na stránku

Níže je kompletní spustitelný kód, který dělá vše od načtení zdrojového DOCX až po zápis finálního PDF. Klidně jej vložte do konzolové aplikace, upravte cesty a spusťte.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Vysvětlení krok za krokem

#### Krok 1 – Načtení DOCX dokumentu  
Instanciujeme objekt `Document`, který ukazuje na `input.docx`. Tento objekt představuje celý soubor Word v paměti a poskytuje přístup ke stránkám, obsahu i metadatům.  

#### Krok 2 – Vytvoření elementu span  
Volání `TaggedContent.CreateSpanElement()` vrací lehký inline kontejner. Představte si ho jako malou, neviditelnou krabičku, která může obsahovat text, obrázky nebo jiné inline elementy. Přidání textu (`span.Text`) je volitelné, ale užitečné pro ladění.  

#### Krok 3 – Umístění span  
`new Position(50, 750)` nastaví levý horní roh span 50 pt od levého okraje a 750 pt od horního okraje stránky. Tyto hodnoty jsou absolutní, takže můžete span umístit kamkoli—ideální pro přesné rozvržení.  

#### Krok 4 – Přidání span na cílovou stránku  
`doc.Pages[1].Add(span)` vloží span na druhou stránku. API používá indexování od nuly, takže stránka 0 je první stránka. Pokud jej potřebujete na první stránku, jednoduše použijte `doc.Pages[0]`.  

#### Krok 5 – Převod DOCX na PDF a uložení jako PDF  
Volání `doc.Save("output.pdf")` dělá dvě věci: zapíše upravený dokument na disk **a** převede obsah do PDF díky příponě `.pdf`. Žádný další krok převodu není potřeba—toto je nejjednodušší způsob, jak **save as PDF**.

---

## Jak přidat span na jinou stránku (pokročilé)

Někdy neznáte index stránky předem. Můžete stránku najít podle jejího čísla (přátelského pro člověka) nebo vyhledáním konkrétního klíčového slova.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Why this matters:** V reportech, kde se počet stránek mění, může pevné kódování `Pages[1]` rozvržení rozbít. Tento úryvek ukazuje robustní vzor pro **how to add span** dynamicky.

---

## Časté úskalí a jak se jim vyhnout

| Problém | Co se stane | Řešení |
|-------|--------------|-----|
| **Span není viditelný** | Souřadnice jsou mimo stránku nebo má span nulovou šířku/výšku. | Zkontrolujte hodnoty `Position`; použijte pravítko ve vašem PDF prohlížeči. |
| **Špatný index stránky** | Přidáte na stránku 0, ale očekáváte ji na stránce 2. | Pamatujte, že API používá nulové indexování; přidejte 1 k lidskému číslu stránky. |
| **Ukládání přepíše zdroj** | `doc.Save("input.docx")` nahradí původní soubor. | Vždy ukládejte na novou cestu (`output.pdf`) při převodu. |
| **Chybí odkaz na SDK** | Chyba kompilace u třídy `Document`. | Nainstalujte NuGet balíček: `dotnet add package DocumentProcessing.SDK`. |

---

## Ověření výsledku

Po spuštění programu otevřete `output.pdf` v libovolném PDF prohlížeči. Měli byste vidět text „Hello, world!“ umístěný přesně na (50, 750) na druhé stránce. Pokud se text objeví jinde, upravte hodnoty `Position` a spusťte znovu.  

Pro automatizované testování můžete použít PDF parser (např. iTextSharp) a programově ověřit souřadnice textu.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Další kroky

* **Style the span** – prozkoumejte `span.Font`, `span.Color` a další vlastnosti stylování.  
* **Add images** – použijte `CreateImageElement()` místo span pro grafiku.  
* **Batch processing** – projděte složku s DOCX soubory ve smyčce

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}