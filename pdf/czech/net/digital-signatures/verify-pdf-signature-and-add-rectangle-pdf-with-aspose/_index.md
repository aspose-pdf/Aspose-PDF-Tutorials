---
category: general
date: 2026-02-09
description: Ověřte podpis PDF pomocí Aspose.PDF v C#. Naučte se, jak přidat obdélník
  do PDF, uložit aktualizovaný PDF a použít funkce podpisu Aspose PDF.
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: cs
og_description: Rychle ověřte podpis PDF v C#. Tento průvodce ukazuje, jak přidat
  grafiku do PDF, uložit aktualizovaný PDF a použít API pro podpis PDF od Aspose.
og_title: Ověřte podpis PDF a přidejte obdélník do PDF – kompletní průvodce Aspose
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: Ověřit podpis PDF a přidat obdélník do PDF s Aspose
url: /cs/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

Ensure code block placeholders remain.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ověření podpisu PDF a přidání obdélníku PDF pomocí Aspose

Už jste někdy potřebovali **ověřit podpis PDF** v C# projektu, ale nebyli jste si jisti, kde začít? Nejste v tom sami — digitální podpisy jsou nezbytné pro soulad, přesto se mnoho vývojářů potýká s úpravou dokumentu poté.  

V tomto tutoriálu vás provedeme kompletním, spustitelným příkladem, který **ověřuje podpis PDF**, přidá **obdélník** na první stránku, zkontroluje, že tvar zůstává uvnitř okrajů stránky, a nakonec **uloží aktualizovaný PDF** — vše pomocí moderního Aspose.PDF API. Na konci budete mít jediný, samostatný program, který můžete vložit do libovolného .NET řešení.

## Co se naučíte

- Načíst podepsaný PDF pomocí Aspose.PDF.
- Použít třídy **aspose pdf signature** k ověření každého podpisu a detekci kompromitací.
- **Přidat obdélník PDF** grafiku bezpečně, zajistit, že se vejde na stránku.
- **Uložit aktualizovaný PDF** při zachování existujících podpisů.
- Tipy, řešení okrajových případů a běžné úskalí.

Nejsou potřeba žádné externí dokumenty — vše, co potřebujete, je zde.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje na .NET Framework 4.7+).
- Aspose.PDF for .NET NuGet balíček (≥ 23.10). Nainstalujte pomocí:

```bash
dotnet add package Aspose.Pdf
```

- Podepsaný PDF soubor pojmenovaný `signed.pdf` umístěný ve složce, kterou ovládáte (nahraďte `YOUR_DIRECTORY` v kódu).
- Základní znalost C# a Visual Studio nebo VS Code.

> **Pro tip:** Pokud nemáte po ruce podepsaný PDF, Aspose poskytuje zdarma demo soubor na svých stránkách, který si můžete stáhnout pro testování.

---

## ověření podpisu PDF – krok za krokem

Prvním krokem je otevřít dokument a projít každým digitálním podpisem. Aspose.PDF poskytuje dvě užitečné metody: `VerifySignature` vám řekne, zda kryptografická kontrola projde, zatímco novější `IsSignatureCompromised` označí jakoukoli manipulaci, která mohla nastat po podpisu.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**Proč je to důležité:**  
- `VerifySignature` samotné pouze potvrzuje, že certifikát podepisujícího je stále důvěryhodný.  
- `IsSignatureCompromised` zachytí jemné změny — například přidání skrytého objektu — takže víte, zda byl vizuální obsah PDF po podpisu změněn.

**Očekávaný výstup** (example with two signatures):

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

Pokud některý podpis hlásí `compromised=True`, měli byste přerušit další zpracování nebo upozornit uživatele, protože integrita dokumentu nemůže být zaručena.

## přidání obdélníku PDF na stránku

Nyní, když jsme potvrdili, že podpisy jsou neporušené (nebo alespoň víme o případném kompromisu), přidáme jednoduchou grafiku obdélníku. To je užitečné pro označování „Reviewed“, zvýrazňování sekcí nebo jen upoutání pozornosti na oblast.

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**Co čísla znamenají:**  
- Systém souřadnic PDF začíná v levém dolním rohu.  
- V příkladu obdélník má šířku 100 bodů a výšku 100 bodů, umístěný přibližně uprostřed typické stránky A4.

> **Poznámka:** Aspose také podporuje `AddEllipse`, `AddPolygon` atd., pokud potřebujete složitější tvary.

## kontrola ohraničení grafiky – zajistit, aby obdélník pasoval

Před uložením změn je rozumné ověřit, že naše grafika zůstává uvnitř tiskové oblasti stránky. Nová metoda `CheckGraphicsBounds` dělá právě to.

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

Pokud `shapeFits` vrátí `false`, budete muset upravit souřadnice obdélníku — možná jej zmenšit nebo posunout níže na stránce. To zabraňuje náhodnému oříznutí, které může vypadat neprofesionálně, zejména při pozdějším tisku PDF.

## uložení aktualizovaného PDF – zachování podpisů a nové grafiky

Nakonec zapíšeme upravený dokument zpět na disk. Metoda `Save` respektuje existující podpisy; neinvaliduje je, pokud se obsah skutečně nezměnil (což jsme již ověřili pomocí `IsSignatureCompromised`).

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**Proč použít nový soubor?**  
Uložení přes původní soubor by mohlo smazat původní podpisy, což znemožní porovnání stavů před a po. Zapsáním do `output.pdf` si zachováte zdroj pro auditní účely.

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do konzolové aplikace. Všechny kroky jsou sloučeny, komentáře vysvětlují každý blok a na konci uvidíte očekávaný výstup do konzole.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**Očekávaný výstup v konzoli** (assuming one valid, uncompromised signature):

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

Pokud je podpis kompromitován, uvidíte `compromised=True` a můžete se rozhodnout, zda pokračovat.

## Časté otázky a řešení okrajových případů

| Question | Answer |
|----------|--------|
| **Co když PDF nemá žádné podpisy?** | `GetSignNames()` vrací prázdnou kolekci; smyčka jednoduše přeskočí a můžete i nadále přidávat grafiku. |
| **Mohu přidat více obdélníků?** | Ano — stačí opakovaně volat `AddRectangle` s různými objekty `Rectangle`. |
| **Co s PDF chráněnými heslem?** | Načtěte je pomocí `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` před ověřením. |
| **Způsobí přidání grafiky neplatnost platného podpisu?** | Pouze pokud podpis pokrývá stránku, na kterou grafiku vkládáte. Použijte `IsSignatureCompromised` k detekci; jinak podpis zůstane neporušený. |
| **Je potřeba uzavřít zdroje?** | Obj​ekty Aspose.PDF jsou spravované; uvolnění je volitelné, ale můžete kód zabalit do bloku `using` pro vyšší bezpečnost. |

## Pro tipy pro produkční nasazení

- **Dávkové zpracování:** Zabalte celý postup do metody, která přijímá vstupní/výstupní cesty; poté předávejte seznam souborů do `Parallel.ForEach` pro zvýšení rychlosti.
- **Logování:** Nahraďte `Console.WriteLine` vhodným loggerem (např. Serilog), aby se výsledky ověření zaznamenaly do auditních záznamů.
- **Politika podpisů:** Kombinujte `VerifySignature` s kontrolou revokace certifikátu (OCSP/CRL) pro přísnější soulad.
- **Styling grafiky:** Použijte `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });`, aby obdélník vynikl.
- **Uzamčení verze:** Připevněte verzi Aspose.PDF NuGet, aby nedošlo k rozbití při aktualizacích knihovny.

## Závěr

Nyní máte solidní, end‑to‑end příklad, který **ověřuje podpis PDF**, **přidává obdélník PDF** a **ukládá aktualizovaný PDF** pomocí nejnovějších Aspose.PDF API. Kód kontroluje kompromitované podpisy, zajišťuje, že grafika zůstává v mezích stránky, a zachovává původní digitální podpisy — přesně to, co vyžaduje reálný workflow pro soulad.

Další kroky, které můžete prozkoumat:

- Přidání **grafiky PDF** jako vodoznaků nebo QR kódů.
- Použití **aspose pdf signature** API k programatickému vytváření nových podpisů.
- Automatizace procesu v ASP.NET Core webové službě pro okamžité ověřování dokumentů.

Vyzkoušejte to, upravte souřadnice obdélníku a podívejte se, jak knihovna reaguje na různé struktury PDF. Šťastné programování a ať vaše PDF zůstávají jak podepsané, tak stylové! 

![verify pdf signature example](image.png "verify pdf signature example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}