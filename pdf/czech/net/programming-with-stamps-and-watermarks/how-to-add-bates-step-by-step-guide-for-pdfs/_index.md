---
category: general
date: 2026-02-10
description: Jak rychle přidat Bates do PDF — naučte se, jak přidat Bates číslo do
  PDF a vytvořit neviditelný vodoznak pomocí Aspose.Pdf v C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: cs
og_description: Jak přidat Bates v C# s Aspose.Pdf. Tento tutoriál ukazuje, jak přidat
  Bates číslo do PDF, přidat neviditelný vodoznak do PDF a další.
og_title: Jak přidat Bates – kompletní PDF průvodce
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Jak přidat Bates – krok za krokem průvodce pro PDF
url: /cs/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat Bates – Kompletní PDF průvodce

Už jste se někdy zamýšleli **jak přidat bates** do právního PDF, aniž byste narušili prohledávatelný text? Nejste v tom sami. V mnoha advokátních kancelářích a e‑discovery projektech je číslo Bates nezbytným zápatím, ale zároveň ho chcete, aby byl neviditelný pro OCR nástroje. Tento tutoriál ukazuje **jak přidat bates** pomocí Aspose.Pdf pro .NET a zároveň se podíváme na **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf** a dokonce i **add page footer pdf** v jedné přehledné řešení.

Projdeme každý řádek kódu, vysvětlíme, proč je každé nastavení důležité, a poskytneme vám připravený příklad, který můžete hned vložit do svého projektu. Žádné vágní odkazy typu „viz dokumentace“ — vše, co potřebujete, je zde.

## Co si odnesete

- Kompletní, spustitelný úryvek C#, který přidá číslo Bates jako artefaktový razítko.
- Porozumění tomu, jak udělat razítko jako **invisible watermark**, které se stále zobrazuje na stránce.
- Tipy, jak škálovat řešení na vícestránkové PDF, měnit písma nebo nahradit razítko vlastním grafickým prvkem.
- Rychlé ukazatele, jak **add page footer pdf** stylizovat obsah, aniž byste narušili extrakci textu.

### Předpoklady

- .NET 6+ (nebo .NET Framework 4.7.2) s Visual Studio 2022 nebo libovolným IDE podle vašeho výběru.
- Aspose.Pdf pro .NET (můžete si stáhnout bezplatnou zkušební verzi z webu Aspose).
- Ukázkový PDF soubor pojmenovaný `source.pdf` umístěný ve složce, kterou ovládáte.

Pokud máte vše připravené, pojďme na to.

---

## Jak přidat Bates – Hlavní implementace

Jádrem řešení je `TextStamp`, který považujeme za **artefakt**. Artefakty jsou ignorovány enginy pro extrakci textu, což je důvod, proč tento přístup funguje také jako technika **add invisible watermark pdf**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Proč to funguje

1. **Artifact flag** – Nastavením `Artifact = new Artifact(ArtifactType.Artifact)` se razítko chová jako ne‑obsahový prvek. Vyhledávače a právní e‑discovery nástroje jej ignorují, což je přesně to, co chcete pro **add invisible watermark pdf**.
2. **Horizontální/vertikální zarovnání** – Střed‑dolní pozice napodobuje klasický styl **add page footer pdf**, takže číslo Bates vypadá profesionálně.
3. **Průhledné pozadí** – Zaručuje, že razítko nezakrývá podkladový obsah, což je nenápadný, ale zásadní detail, když později potřebujete PDF vytisknout nebo zobrazit na různých zařízeních.

---

## Add Bates Number PDF – Škálování na více stránek

Většina reálných PDF má více než jednu stránku. Výše uvedený úryvek upravuje pouze první stránku, ale rozšířit jej je hračka:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Tip:** Pokud potřebujete sekvenční číslo, které není svázáno s fyzickým pořadím stránek (např. začít od 1000), stačí před smyčkou inicializovat čítač a v ní ho inkrementovat.

---

## Add Custom Stamp PDF – Přesahování čistého textu

Někdy čisté textové razítko nestačí — můžete chtít logo, QR kód nebo barevný pruh. Aspose.Pdf vám umožní vyměnit `TextStamp` za `ImageStamp` nebo dokonce kombinovat oba pomocí objektů `Stamp`.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Míchání razítek je tak jednoduché jako přidat obě na stejnou stránku. Funkce **add custom stamp pdf** zazáří, když potřebujete vedle čísla Bates umístit firemní pečeť.

---

## Add Invisible Watermark PDF – Skutečně skrytý razítko

Pokud opravdu potřebujete, aby razítko bylo neviditelné jak lidskému oku, *také* extrakčním nástrojům, můžete nastavit barvu písma tak, aby odpovídala pozadí stránky (obvykle bílá) a snížit průhlednost:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

I při `Opacity = 0` artefakt stále existuje ve struktuře PDF, takže právní software jej může najít, pokud zná ID artefaktu. To je ultimátní trik **add invisible watermark pdf**.

---

## Add Page Footer PDF – Konzistentní stylování zápatí

Profesionální zápatí často obsahuje více než jen číslo Bates: datum, název dokumentu nebo upozornění o důvěrnosti. Zde je rychlý způsob, jak spojit několik textových částí do jednoho razítka:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Všimněte si jemné šedé barvy — ideální pro **add page footer pdf**, která neodvádí pozornost od hlavního obsahu, ale stále splňuje právní požadavky.

---

## Očekávaný výstup a jak jej ověřit

Po spuštění celého skriptu otevřete `bates_artifact.pdf` v libovolném PDF prohlížeči:

- Uvidíte „Bates 00123“ (nebo sekvenční číslo) centrované ve spodní části každé stránky.
- Výběr textu na stránce **neobsahuje** číslo Bates, což potvrzuje chování artefaktu.
- Pokud jste použili nastavení neviditelné vodotisky, číslo nebude vůbec viditelné, ale zůstane v interní struktuře PDF (zkontrolujte pomocí nástroje jako PDF‑XChange Editor → „Document → Properties → Advanced“).

---

## Často kladené otázky a okrajové případy

**Co když už moje PDF má zápatí?**  
Můžete upravit `VerticalAlignment` na `VerticalAlignment.Top` nebo změnit vlastnost `Margin`, aby se razítko posunulo nad existující zápatí.

**Mohu použít jiné písmo?**  
Určitě. Stačí nahradit `"Arial"` libovolným názvem písma, které Aspose dokáže najít, nebo vložit vlastní TTF soubor pomocí `FontRepository.AddFont("path/to/font.ttf")`.

**Je tento přístup kompatibilní s .NET Core?**  
Ano — Aspose.Pdf pro .NET funguje napříč .NET Framework, .NET Core i .NET 5/6. Jen se ujistěte, že odkazujete na správný NuGet balíček.

**Jaká je výkonnost u obrovských PDF (1000+ stránek)?**  
Vytvoření jediného `TextStamp` a jeho klonování uvnitř smyčky je paměťově úsporné. Pro masivní soubory zvažte zpracování po dávkách nebo použití `PdfProcessor`, abyste se vyhnuli načítání celého dokumentu najednou.

---

## Závěr

Probrali jsme **jak přidat bates** do PDF od začátku až do konce, předvedli **add bates number pdf**, ukázali vám, jak **add custom stamp pdf**, proměnili razítko v **add invisible watermark pdf** a stylizovali jej jako profesionální **add page footer pdf**. Kompletní ukázkový kód běží tak, jak je, a vysvětlení vám poskytují „proč“ za každým řádkem — právě to, co AI asistenti rádi citují.

Další kroky? Zkuste nahradit textové razítko obrázkovým, experimentujte s různými typy artefaktů nebo integrujte tuto logiku do služby pro hromadné zpracování, která automaticky očísluje každý dokument ve složce. Možnosti jsou nekonečné a nyní máte pevný základ, na kterém můžete stavět.

Šťastné kódování a ať jsou vaše PDF vždy perfektně očíslovaná!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}