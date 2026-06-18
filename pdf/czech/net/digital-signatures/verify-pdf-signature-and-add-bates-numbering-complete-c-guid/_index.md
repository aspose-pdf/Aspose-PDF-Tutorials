---
category: general
date: 2026-04-02
description: Rychle ověřte podpis PDF a naučte se, jak přidat číslování Bates pomocí
  Aspose.Pdf. Obsahuje krok‑za‑krokem kód a tipy.
draft: false
keywords:
- verify pdf signature
- add bates numbering
- how to verify signature
- how to add bates
- check pdf signature
language: cs
og_description: Rychle ověřte podpis PDF a naučte se, jak pomocí Aspose.Pdf přidat
  Batesovo číslování. Sledujte kompletní příklad a vyhněte se běžným úskalím.
og_title: Ověření PDF podpisu a přidání Batesova číslování – kompletní průvodce C#
tags:
- Aspose.Pdf
- C#
- Digital Signature
- Document Automation
title: Ověření PDF podpisu a přidání Batesova číslování – kompletní průvodce C#
url: /cs/net/digital-signatures/verify-pdf-signature-and-add-bates-numbering-complete-c-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ověření PDF podpisu a přidání Bates číslování – Kompletní průvodce v C#  

Už jste někdy potřebovali **ověřit PDF podpis** před odesláním smlouvy, ale nebyli jste si jisti, kterou API metodu použít? Nejste sami — mnoho vývojářů narazí na tento problém při práci s právně závaznými PDF. V tomto tutoriálu vám ukážeme, jak **ověřit PDF podpis** pomocí Aspose.Pdf a poté vám ukážeme, **jak přidat Bates číslování**, aby vaše soubory byly připravené na audit.  

Také se podíváme na **jak programově ověřit podpis**, pokryjeme **jak přidat Bates** v jednom průchodu a vysvětlíme **výsledky kontroly PDF podpisu**, abyste mohli výstup důvěřovat. Na konci budete mít spustitelnou C# konzolovou aplikaci, která provádí oba úkoly — žádná záhada, jen přehledný kód.

---

## Co budete potřebovat

- **.NET 6.0** nebo novější (příklad funguje také s .NET Framework 4.7+)  
- **Aspose.Pdf for .NET** NuGet balíček (verze 23.11 nebo novější)  
- Podepsaný PDF soubor (`signed.pdf`), který chcete ověřit  
- Prostý PDF (`input.pdf`), který bude obsahovat Bates čísla  

Pokud je máte, můžete začít. Žádné další SDK, žádné skryté konfigurační soubory.

## Krok 1: Nastavení projektu

Začněte vytvořením konzolového projektu:

```bash
dotnet new console -n PdfSignatureAndBatesDemo
cd PdfSignatureAndBatesDemo
dotnet add package Aspose.Pdf
```

Otevřete `Program.cs` a odstraňte výchozí kód. Všechno postavíme od začátku, abyste později mohli zkopírovat finální verzi.

## Krok 2: Ověření PDF podpisu

### Proč je ověření důležité

Digitální podpis může být **kompromitován**, pokud je podkladový certifikát odvolán nebo byl dokument po podpisu pozměněn. Aspose.Pdf poskytuje užitečnou metodu `IsSignatureCompromised`, která vrací boolean — jednoduché, ale dostatečně silné pro většinu auditních procesů.

### Ukázka kódu

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace PdfSignatureAndBatesDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ---------- Verify PDF Signature ----------
            string signedPdfPath = @"YOUR_DIRECTORY\signed.pdf";

            // Load the signed document inside a using block to ensure disposal
            using (Document signedDoc = new Document(signedPdfPath))
            using (PdfFileSignature pdfSignature = new PdfFileSignature(signedDoc))
            {
                // The name "Signature1" is the default for the first signature.
                // Change it if your PDF uses a custom field name.
                bool isCompromised = pdfSignature.IsSignatureCompromised("Signature1");

                Console.WriteLine($"Signature compromised: {isCompromised}");
                // Expected output: "Signature compromised: False" if everything is fine.
            }

            // The rest of the program (Bates numbering) continues below...
```

**Vysvětlení**

- `Document` načte PDF do paměti.  
- `PdfFileSignature` obaluje dokument a poskytuje metody související s podpisem.  
- `IsSignatureCompromised("Signature1")` kontroluje integritu podpisu pojmenovaného *Signature1*.  
- Boolean výsledek vám říká, zda je podpis stále důvěryhodný.

> **Tip:** Pokud si nejste jisti názvem pole podpisu, nejprve zavolejte `pdfSignature.GetSignatureNames()`; vrátí seznam všech identifikátorů podpisů.

## Krok 3: Připravte možnosti Bates číslování

### Co je Bates číslování?

Bates čísla jsou sekvenční identifikátory tištěné na každé stránce právního nebo forenzního dokumentu. Usnadňují odkazování na stránky během vyhledávání nebo auditních procesů. `BatesNumberingOptions` v Aspose.Pdf vám umožňuje přizpůsobit předponu, počáteční číslo, počet číslic, zarovnání a okraj — vše v jednom objektu.

### Pokračování kódu

```csharp
            // ---------- Configure Bates Numbering ----------
            string sourcePdfPath = @"YOUR_DIRECTORY\input.pdf";
            using (Document pdfWithBates = new Document(sourcePdfPath))
            {
                // Set up the numbering style
                BatesNumberingOptions batesOptions = new BatesNumberingOptions
                {
                    Prefix = "INV-",          // Anything before the numeric part
                    StartNumber = 1000,      // First number to use
                    NumberOfDigits = 5,      // Pads numbers with leading zeros (e.g., 01000)
                    Alignment = HorizontalAlignment.Right,
                    BottomMargin = 20        // Distance from the bottom edge (points)
                };

                // Apply the numbering to every page in the document
                pdfWithBates.AddBatesNumbering(batesOptions);

                // Save the newly numbered PDF
                string outputPdfPath = @"YOUR_DIRECTORY\BatesNumbered.pdf";
                pdfWithBates.Save(outputPdfPath);

                Console.WriteLine($"Bates numbering added. File saved to: {outputPdfPath}");
                // Expected output: "Bates numbering added. File saved to: ...\BatesNumbered.pdf"
            }
        }
    }
}
```

**Vysvětlení**

- `BatesNumberingOptions` centralizuje všechna nastavení formátování.  
- `AddBatesNumbering` automaticky prochází každou stránku — není potřeba ruční smyčka.  
- `Prefix` (`INV-`) a `StartNumber` (1000) vytvářejí štítky jako `INV-01000`, `INV-01001` atd.  
- Upravit `BottomMargin`, pokud potřebujete číslo výše nebo níže na stránce.

## Krok 4: Spusťte kompletní příklad

Uložte soubor a poté spusťte:

```bash
dotnet run
```

Měli byste vidět dva řádky v konzoli:

```
Signature compromised: False
Bates numbering added. File saved to: YOUR_DIRECTORY\BatesNumbered.pdf
```

Pokud první řádek vypíše `True`, podpis je kompromitován — to znamená, že dokument mohl být po podpisu změněn nebo certifikát již není platný. V takovém případě přerušte jakékoli následné zpracování.

## Krok 5: Běžné okrajové případy a jak je řešit

| Situace | Na co si dát pozor | Navrhované řešení |
|-----------|-------------------|---------------|
| **Více podpisů** | `IsSignatureCompromised` kontroluje pouze jedno pole najednou. | Procházejte `pdfSignature.GetSignatureNames()` a ověřte každý. |
| **Vlastní název pole podpisu** | Použití `"Signature1"` může vyvolat výjimku, pokud se název liší. | Nejprve načtěte seznam názvů, nebo předávejte přesný název, který vidíte v Acrobat. |
| **Velké PDF (100+ stran)** | Přidávání Bates čísel může být náročné na paměť. | Použijte `Document.Save` s `SaveOptions`, které umožňují streamování (`PdfSaveOptions { Compress = true }`). |
| **Ne-latinské znaky v předponě** | Některá písma ve výchozím nastavení nepodporují Unicode. | Nastavte `pdfWithBates.Font` na Unicode‑kompatibilní písmo, např. `Arial Unicode MS`. |
| **Potřeba umístit čísla vlevo** | Zarovnání je pevně nastaveno na `Right`. | Změňte `Alignment = HorizontalAlignment.Left` v `BatesNumberingOptions`. |

## Krok 6: Ověřte výsledek ručně (volitelné)

Otevřete `BatesNumbered.pdf` v libovolném PDF prohlížeči:

1. Projděte stránky — každá by měla zobrazovat štítek jako **INV‑01000** v pravém dolním rohu.  
2. Použijte **Panel podpisů** v Acrobat a dvojklikněte na podpis, abyste potvrdili, že stav odpovídá výstupu v konzoli.

Pokud vše souhlasí, úspěšně jste **zkontrolovali stav PDF podpisu** a aplikovali **přidání Bates číslování** najednou.

## Často kladené otázky

**Q: Mohu ověřit podpis bez načtení celého dokumentu?**  
**A:** Aspose.Pdf soubor streamuje pod kapotou, ale stále potřebujete instanci `Document`. Pro obrovské soubory zvažte použití `PdfFileSignature` přímo s file streamem, abyste snížili paměťovou náročnost.

**Q: Potřebuji licenci pro Aspose.Pdf?**  
**A:** Bezplatná zkušební verze funguje, ale přidává vodoznak. Pro produkci budete potřebovat řádnou licenci; jinak budou výstupní PDF obsahovat banner Aspose.

**Q: Co když potřebuji přidat Bates čísla jen na podmnožinu stránek?**  
**A:** Použijte `pdfWithBates.AddBatesNumbering(batesOptions, new[] { 1, 3, 5 })`, kde pole uvádí čísla stránek, které chcete číslovat.

## Závěr

Nyní víte, **jak ověřit PDF podpis** pomocí Aspose.Pdf, rozumíte významu boolean výsledku a můžete s jistotou **přidat Bates číslování** do libovolného PDF, které máte pod kontrolou. Kompletní, spustitelný příklad kombinuje oba úkoly a poskytuje vám jediný konzolový nástroj, který kontroluje pravost dokumentu a označuje jej auditně připravenými identifikátory.  

Dále můžete zkoumat **jak ověřit podpis** vůči důvěryhodnému kořenovému úložišti, nebo experimentovat s vlastním stylem **přidání Bates číslování**, například diagonálními razítky nebo předponami podle sekcí. Obě témata staví na základech, které jste právě zvládli, a učiní váš pipeline pro zpracování dokumentů ještě robustnější.  

Šťastné programování a pamatujte — kontrola podpisů a číslování stránek je hračka, jakmile máte správný kód! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}