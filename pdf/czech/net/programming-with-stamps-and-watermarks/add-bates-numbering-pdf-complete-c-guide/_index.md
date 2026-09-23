---
category: general
date: 2026-03-22
description: Rychle přidejte Batesovo číslování do PDF pomocí Aspose.Pdf. Naučte se,
  jak přidat Bates, přidat sekvenční čísla stránek, přidat vlastní zápatí do PDF a
  přidat artefakt do PDF během několika minut.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: cs
og_description: Přidání Batesova číslování do PDF pomocí Aspose.Pdf. Tento návod ukazuje,
  jak přidat Bates, přidat sekvenční čísla stránek, přidat vlastní zápatí PDF a přidat
  artefakt do PDF.
og_title: Přidání Batesova číslování do PDF – krok za krokem C# tutoriál
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Přidání Batesova číslování PDF – Kompletní průvodce C#
url: /cs/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Bates číslování PDF – Kompletní průvodce v C#

Už jste někdy potřebovali **add bates numbering pdf** do dávky právních dokumentů, ale nebyli jste si jisti, kde začít? Nejste první – mnoho vývojářů narazilo na tento problém při tvorbě nástrojů pro správu případů. Dobrá zpráva? S Aspose.Pdf můžete **add bates**, **add sequential page numbers** a dokonce **add custom footer pdf** prvky pomocí několika řádků kódu.  

V tomto tutoriálu projdeme celý proces, od instalace knihovny po uložení finálního souboru, a přidáme tipy, jak **add artifact to pdf** soubory přidat, aniž byste narušili existující obsah. Na konci budete mít připravený úryvek kódu, který můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- .NET 6+ (kód funguje jak na .NET Core, tak na .NET Framework)  
- Platná licence Aspose.Pdf pro .NET (můžete začít s bezplatnou zkušební verzí)  
- Vstupní PDF (`input.pdf`) umístěné ve složce, na kterou můžete odkazovat  
- Visual Studio, Rider nebo jakýkoli C# editor, který preferujete  

To je vše – žádné další NuGet balíčky kromě Aspose.Pdf.

## Krok 1: Instalace Aspose.Pdf přes NuGet

Nejprve si nainstalujeme knihovnu na váš počítač. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.Pdf
```

Nebo pokud používáte Package Manager Console ve Visual Studiu:

```powershell
Install-Package Aspose.Pdf
```

*Tip:* Po instalaci zkontrolujte, že složka `Aspose.Pdf` se objeví pod `Dependencies → Packages` ve vašem Solution Exploreru.

## Krok 2: Načtení zdrojového PDF dokumentu

Nyní vytvoříme objekt `Document`, který představuje PDF, které chceme opatřit razítkem. Použití příkazu `using` zajistí automatické uvolnění souborového handle.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Proč použít `using var`? Zaručuje uvolnění i v případě výjimky, čímž zabraňuje problémům se zamčením souboru při pozdějším přepsání stejného souboru.

## Krok 3: Vytvoření a konfigurace Bates číslovacího artefaktu

Bates číslo je v podstatě textový artefakt, který existuje v logické struktuře PDF. Můžete jej považovat za **custom footer pdf**, protože se zobrazuje na každé stránce, aniž by byl součástí content streamu stránky.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Proč jsou tato nastavení důležitá

- **Prefix**: Užitečné pro rozlišení typů dokumentů (např. „INV‑“ pro faktury).  
- **Start**: Nastavuje první číslo; můžete jej načíst z databáze, pokud potřebujete kontinuitu napříč soubory.  
- **Format**: `"0000"` vynutí čtyřciferné zobrazení, což zajišťuje zarovnání při růstu čísel.  
- **X/Y**: Souřadnice se měří od levého dolního rohu, takže `Y = 20` umístí text těsně nad okraj stránky. Upravit `X`, pokud chcete číslo zarovnané vlevo nebo na střed.

Pokud potřebujete místo Bates čísel **add sequential page numbers**, jednoduše vynechte `Prefix` a upravte `Format` na `"###"` nebo jakýkoli jiný vzor, který preferujete.

## Krok 4: Aplikace artefaktu na všechny stránky

Aspose.Pdf vám umožní připojit artefakt k celému dokumentu jedním voláním. To je nejefektivnější způsob, jak **add artifact to pdf**, aniž byste museli ručně procházet každou stránku.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Za scénou Aspose přidá artefakt do slovníku stránky každé stránky, což znamená, že číslování se stane součástí logické struktury PDF – ideální pro pozdější extrakci nebo vyhledávání.

## Krok 5: Uložení aktualizovaného PDF

Nakonec zapíšete změny zpět na disk. Můžete přepsat originál nebo uložit do nového souboru; druhá možnost je během vývoje bezpečnější.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Když otevřete `output.pdf` v prohlížeči, uvidíte „INV‑1000“, „INV‑1001“, … v pravém dolním rohu každé stránky.

### Ověření výsledku

Otevřete PDF v Adobe Acrobat nebo jakémkoli prohlížeči a hledejte čísla. Pokud potřebujete potvrdit programově, můžete artefakt načíst zpět:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Tento úryvek vytiskne Bates štítek každé stránky – užitečné pro automatizované testy.

## Okrajové případy a časté otázky

### Co když moje PDF už má zápatí?

Přidání artefaktu nepřepíše existující zápatí, protože artefakty jsou v samostatné vrstvě. Pokud však překrývání vizuálu představuje problém, upravte souřadnici `Y` nebo zvětšete posun `X`, aby se Bates číslo posunulo.

### Můžu použít jiný font nebo barvu?

Určitě. `BatesNumberingArtifact` dědí z `Artifact`, takže můžete nastavit `Font`, `FontColor` a dokonce i `Opacity`. Příklad:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Jak resetovat čítač pro nový dokument?

Jednoduše změňte `Start` před voláním `AddArtifact`. Pokud generujete mnoho PDF v cyklu, udržujte běžící čítač ve vaší aplikační logice.

### Je tento přístup kompatibilní s šifrovanými PDF?

Aspose.Pdf může otevřít šifrované PDF, pokud zadáte heslo:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Po dešifrování fungují stejné kroky přidání artefaktu bezchybně.

## Kompletní funkční příklad

Níže je kompletní, připravený program. Vložte jej do konzolové aplikace, upravte cesty a stiskněte **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Očekávaný výstup:** Konzole vytiskne „Bates numbering added successfully!“ a `output.pdf` obsahuje sekvenční štítky jako `INV‑1000`, `INV‑1001` atd., umístěné v pravém dolním rohu každé stránky.

## Rychlé shrnutí

- **Primary goal:** **add bates numbering pdf** pomocí Aspose.Pdf.  
- Pokryli jsme **how to add bates**, **add sequential page numbers** a **add custom footer pdf** prvky pomocí jediného artefaktu.  
- Tutoriál ukázal, jak **add artifact to pdf**, řešit okrajové případy a ověřit výsledek.  

## Co dál?

- **Dynamic prefixes:** Načtěte hodnoty z databáze pro generování „CASE‑2023‑001“, „CASE‑2023‑002“, …  
- **Conditional placement:** Použijte detekci velikosti stránky (`page.MediaBox`) k centrování čísel na krajinových stránkách.  
- **Combine with watermarks:** Přidejte poloprůhledné logo vedle Bates čísla pro branding.  

Klidně experimentujte – možná objevíte chytřejší způsob, jak hromadně zpracovat tisíce souborů. Pokud narazíte na potíže, zanechte komentář nebo si prohlédněte oficiální dokumentaci Aspose (je překvapivě přehledná). Šťastné programování!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}