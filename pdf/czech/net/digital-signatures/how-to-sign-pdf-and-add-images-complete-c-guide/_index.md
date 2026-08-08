---
category: general
date: 2026-03-29
description: Jak podepsat PDF digitálním podpisem a přidat oříznutý obrázek v C#.
  Naučte se přidávat digitální podpis do PDF, oříznout obrázek pro PDF a snadno přidat
  obrázek do PDF.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: cs
og_description: Jak podepsat PDF digitálním podpisem a vložit oříznutý obrázek pomocí
  Aspose.Pdf v C#. Postupujte podle tohoto návodu pro kompletní řešení.
og_title: Jak podepsat PDF a přidat obrázky – krok za krokem C# tutoriál
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Jak podepsat PDF a přidat obrázky – kompletní průvodce C#
url: /cs/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak podepsat PDF a přidat obrázky – Kompletní průvodce v C#  

Už jste se někdy zamysleli, **jak podepsat PDF** soubory programově a zároveň vložit vlastní obrázek? Možná budujete schvalovací workflow a potřebujete právně závazný podpis *a* miniaturu fotografie podepisujícího na stejné stránce. Zkrátka, chcete **add digital signature pdf** obsah, oříznout ten obrázek a pak **add image to pdf** bez námahy.  

Tento tutoriál vás provede každým krokem – od načtení certifikátu ECDSA PKCS#7 po oříznutí JPEG a jeho umístění na podepsanou stránku. Na konci budete mít jediný spustitelný soubor C#, který podepíše stránku 1, ořízne fotografii na 400 × 400 px a umístí ji na přesné místo. Žádné externí skripty, žádná magie, jen čistý kód a vysvětlení.

## Požadavky

- .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.7+)
- **Aspose.Pdf for .NET** NuGet balíček (verze 23.9 nebo novější)
- Certifikát ECDSA P‑256 v PKCS#7 (`.pfx`) formátu a jeho heslo
- JPEG obrázek, který chcete vložit (např. `photo.jpg`)

> **Pro tip:** Uchovávejte soubor certifikátu mimo správu verzí a chraňte heslo pomocí správce tajemství.

---

## Krok 1: Nastavení projektu a importů

Nejprve vytvořte konzolovou aplikaci (nebo ji integrujte do jakékoli existující služby). Přidejte odkaz na Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Poté zahrňte požadované jmenné prostory:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

Tyto `using` direktivy vám poskytují přístup ke třídám `Document`, `Signature` a `Rectangle`, které budeme později potřebovat.

## Krok 2: Načtení PDF a příprava podpisu

Otevřeme existující PDF (`source.pdf`) a vytvoříme objekt **digital signature pdf**, který používá oddělený PKCS#7 podpis. Certifikát je klíč ECDSA P‑256, který je široce akceptován pro shodu.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Proč je to důležité:** Použití odděleného PKCS#7 podpisu zachovává původní obsah PDF beze změny a vkládá kryptografický hash. Toto je průmyslový standard pro právně závazná PDF.

## Krok 3: Aplikace digitálního podpisu na konkrétní stránku

Nyní umístíme viditelné pole podpisu na **stránku 1**. Obdélník určuje, kde se pole podpisu zobrazí (souřadnice jsou v bodech, kde 1 palec = 72 bodů).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

Pokud nepotřebujete viditelné pole, nastavte `isVisible` na `false`. `signatureRect` lze upravit tak, aby odpovídal rozvržení vašeho dokumentu.

## Krok 4: Otevření proudu obrázku a definování oblastí ořezu

Přečteme JPEG soubor do proudu a specifikujeme **source rectangle**, který vybere levý horní roh 400 × 400 pixelů. Toto je operace **crop image for pdf**.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Edge case:** Pokud je váš obrázek menší než 400 × 400, ořez se automaticky omezí na skutečné rozměry obrázku – nevyvolá se výjimka.

## Krok 5: Definování místa, kde se oříznutý obrázek zobrazí

Dále nastavíme **destination rectangle** na stránce PDF. V tomto příkladu umístíme obrázek na (50, 50) s velikostí 200 × 200 bodů (≈2,78 palců čtverečních).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

Neváhejte experimentovat: změňte souřadnice X/Y pro posunutí obrázku, nebo upravte šířku/výšku pro škálování.

## Krok 6: Vložení oříznutého obrázku na podepsanou stránku

Nakonec přidáme obrázek na **stránku 1** (stejnou stránku, která nyní obsahuje podpis). Přetížení `AddImage`, které používáme, přijímá source a destination obdélníky a efektivně provádí ořez a umístění v jednom volání.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

Za scénou Aspose.Pdf extrahuje oblast 400 × 400 pixelů, přepočítá ji na 200 × 200 bodů a zapíše ji do PDF content streamu.

## Krok 7: Uložení podepsaného a obrázkem obohaceného PDF

Po všech úpravách dokument uložte. Můžete přepsat originál nebo zapsat do nového souboru.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

Když otevřete `output_signed.pdf` v Adobe Acrobat nebo jakémkoli PDF prohlížeči, uvidíte:

- Viditelné pole podpisu na souřadnicích, které jste zadali.
- Oříznutá fotografie umístěná na (50, 50) na stránce 1.
- Digitální podpis ověřen (pokud prohlížeč důvěřuje vašemu certifikátu).

## Často kladené otázky (FAQ)

| Otázka | Odpověď |
|----------|--------|
| **Mohu podepsat jinou stránku?** | Změňte argument `pageNumber` v `signature.Sign` na libovolný platný index stránky (číslování od 1). |
| **Co když potřebuji více podpisů?** | Vytvořte novou instanci `Signature` pro každou stránku nebo místo, přičemž můžete znovu použít stejný `pkcsSignature`, pokud se použije stejný certifikát. |
| **Je ořez obrázku omezen na obdélníky?** | Ano, `AddImage` v Aspose.Pdf funguje s obdélníkovými oblastmi. Pro složitější tvary musíte obrázek předem zpracovat (např. pomocí System.Drawing) před vložením. |
| **Jak udělat podpis neviditelný?** | Nastavte `isVisible` na `false` a vynechte `signatureRect`. Podpis bude i nadále kryptograficky platný. |
| **Jaké formáty mohu vložit kromě JPEG?** | PNG, BMP, GIF a TIFF jsou všechny podporovány. Stačí změnit cestu k souboru a zajistit, aby proud načetl správné bajty. |

## Úplný funkční příklad

Níže je kompletní, samostatný program. Zkopírujte jej do `Program.cs`, upravte cesty a spusťte.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Očekávaný výsledek:** Otevření `output_signed.pdf` zobrazí pole podpisu (100 × 100 → 300 × 300 bodů) a obrázek o velikosti 200 × 200 bodů odvozený z levého horního rohu `photo.jpg`. Podpis je ověřen vůči dodanému ECDSA certifikátu.

## Závěr

Probrali jsme **how to sign PDF** soubory, jak **add digital signature pdf** na konkrétní stránku, jak **crop image for pdf**, a nakonec jak **add image to pdf** pomocí Aspose.Pdf v C#. Celý proces – od načtení certifikátu po uložení finálního dokumentu – se vejde do jediného, snadno čitelného zdrojového souboru.

Pokud jste připraveni na další výzvu, zvažte:

- Přidání **multiple signatures** na různé stránky (použijte koncept „digital signature pdf page“).
- Vkládání **QR kódů**, které odkazují na ověřovací služby.
- Automatizace procesu v ASP.NET Core API pro generování PDF za běhu.

Pamatujte, že klíčem k robustní automatizaci PDF je jasné oddělení odpovědností: zpracování podpisu, zpracování obrázku a finální sestavení dokumentu. Hrajte si s koordináty, vyměňte formát obrázku nebo experimentujte s časovým razítkem – váš workflow je nyní plně rozšiřitelný.

Máte otázky, okrajové scénáře nebo zajímavý případ k sdílení? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}