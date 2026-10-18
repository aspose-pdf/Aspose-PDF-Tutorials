---
title: Porovnání PDF vedle sebe s vyloučením anotací pomocí Aspose.Pdf pro .NET
weight: 101
limit:
description: Postupný návod, jak porovnat PDF soubory a vyloučit oblasti anotací pomocí Aspose.Pdf pro .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Postupný návod, jak porovnat PDF soubory a vyloučit oblasti anotací
    pomocí Aspose.Pdf pro .NET.
  headline: Porovnání PDF vedle sebe s vyloučením anotací pomocí Aspose.Pdf pro .NET
  type: TechArticle
- description: Postupný návod, jak porovnat PDF soubory a vyloučit oblasti anotací
    pomocí Aspose.Pdf pro .NET.
  name: Porovnání PDF vedle sebe s vyloučením anotací pomocí Aspose.Pdf pro .NET
  steps:
  - name: Cestu k souborům definujte pro primární PDF, sekundární PDF a výstupní diff
      PDF.
    text: Cestu k souborům definujte pro primární PDF, sekundární PDF a výstupní diff
      PDF.
  - name: Zkontrolujte, že oba vstupní PDF soubory existují, a v případě, že některý
      chybí, ukončete s chybovou zprávou.
    text: Zkontrolujte, že oba vstupní PDF soubory existují, a v případě, že některý
      chybí, ukončete s chybovou zprávou.
  - name: Otevřete oba PDF soubory jako objekty Document (pdfA a pdfB) v rámci using
      bloku, aby byly automaticky uvolněny.
    text: Otevřete oba PDF soubory jako objekty Document (pdfA a pdfB) v rámci using
      bloku, aby byly automaticky uvolněny.
  - name: Shromážděte ohraničující obdélníky všech anotací v pdfA a uložte je do ignoredRectsA.
    text: Shromážděte ohraničující obdélníky všech anotací v pdfA a uložte je do ignoredRectsA.
  - name: Shromážděte ohraničující obdélníky všech anotací v pdfB a uložte je do ignoredRectsB.
    text: Shromážděte ohraničující obdélníky všech anotací v pdfB a uložte je do ignoredRectsB.
  - name: Vytvořte objekt SideBySideComparisonOptions a přiřaďte dříve sesbírané obdélníky
      anotací k ExcludeAreas1 a ExcludeAreas2, aby byly tyto oblasti během porovnání
      ignorovány.
    text: Vytvořte objekt SideBySideComparisonOptions a přiřaďte dříve sesbírané obdélníky
      anotací k ExcludeAreas1 a ExcludeAreas2, aby byly tyto oblasti během porovnání
      ignorovány.
  - name: Spusťte porovnání PDF vedle sebe pomocí dvou objektů Document a nakonfigurovaných
      možností a výsledek zapište do outputPdf.
    text: Spusťte porovnání PDF vedle sebe pomocí dvou objektů Document a nakonfigurovaných
      možností a výsledek zapište do outputPdf.
  - name: Uvolněte objekty Document a opusťte using blok.
    text: Uvolněte objekty Document a opusťte using blok.
  - name: Vytiskněte potvrzovací zprávu, která uvádí, že porovnání bylo dokončeno,
      a kde byl diff PDF uložen.
    text: Vytiskněte potvrzovací zprávu, která uvádí, že porovnání bylo dokončeno,
      a kde byl diff PDF uložen.
  type: HowTo
- questions:
  - answer: Ano. Kód jednoduše nepřidá žádné obdélníky do odpovídajícího seznamu `ignoredRects`,
      takže `ExcludeAreas1`/`ExcludeAreas2` dostanou prázdné pole a porovnávač zpracuje
      celou stránku.
    question: Co se stane, pokud stránka PDF nemá žádné anotace – bude porovnání stále
      fungovat?
  - answer: Nastavte `ExcludeAreas1` (nebo `ExcludeAreas2`) na sesbírané obdélníky
      a nechte druhou vlastnost jako prázdné pole; porovnávač bude ignorovat oblasti
      jen v určeném dokumentu.
    question: Mohu vyloučit anotace jen z jednoho dokumentu a zachovat anotace druhého
      v diffu?
  - answer: Překrývající se obdélníky jsou porovnávačem interně sloučeny, takže překrývající
      se hranice anotací jsou bezpečně vyloučeny bez dvojího počítání.
    question: Způsobují překrývající se obdélníky anotací nějaké problémy s `ExcludeAreas`?
  - answer: Ano, nastavte `compareOpts.ExcludeTables = true;` – tento příznak funguje
      spolu s `ExcludeAreas1`/`ExcludeAreas2` a také vylučuje oblasti tabulek.
    question: Existuje způsob, jak vyloučit tabulky kromě anotací pomocí stejného
      objektu možností?
  - answer: Kód kontroluje `if (a != null && a.Rect != null)` před přidáním do seznamu,
      takže nulové obdélníky jsou jednoduše přeskočeny a žádná výjimka není vyvolána.
    question: Co když je vlastnost `Rect` anotace null – vyvolá kód výjimku?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Porovnat PDF bez anotací
og_description: Spusťte porovnání PDF vedle sebe, které přeskočí všechny značky anotací.
og_image_alt: Návod ukazující porovnání PDF vedle sebe, které vylučuje oblasti anotací pomocí Aspose.Pdf pro .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Porovnání PDF vedle sebe s vyloučením anotací pomocí Aspose.Pdf pro .NET
Tento tutoriál ukazuje, jak porovnat dva PDF soubory pomocí Aspose.Pdf pro .NET při ignorování veškerého obsahu anotací. Extrahuje ohraničující rámečky všech anotací z každého dokumentu, předá tyto oblasti do SideBySideComparisonOptions a poté spustí porovnání vedle sebe. Výsledkem je diff PDF, který zvýrazňuje pouze změny mimo anotace.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: Co se stane, pokud stránka PDF nemá žádné anotace – bude porovnání stále fungovat?**  
A: Ano. Kód jednoduše nepřidá žádné obdélníky do odpovídajícího seznamu `ignoredRects`, takže `ExcludeAreas1`/`ExcludeAreas2` dostanou prázdné pole a porovnávač zpracuje celou stránku.

**Q: Mohu vyloučit anotace jen z jednoho dokumentu a zachovat anotace druhého v diffu?**  
A: Nastavte `ExcludeAreas1` (nebo `ExcludeAreas2`) na sesbírané obdélníky a nechte druhou vlastnost jako prázdné pole; porovnávač bude ignorovat oblasti jen v určeném dokumentu.

**Q: Způsobují překrývající se obdélníky anotací nějaké problémy s `ExcludeAreas`?**  
A: Překrývající se obdélníky jsou porovnávačem interně sloučeny, takže překrývající se hranice anotací jsou bezpečně vyloučeny bez dvojího počítání.

**Q: Existuje způsob, jak vyloučit tabulky kromě anotací pomocí stejného objektu možností?**  
A: Ano, nastavte `compareOpts.ExcludeTables = true;` – tento příznak funguje spolu s `ExcludeAreas1`/`ExcludeAreas2` a také vylučuje oblasti tabulek.

**Q: Co když je vlastnost `Rect` anotace null – vyvolá kód výjimku?**  
A: Kód kontroluje `if (a != null && a.Rect != null)` před přidáním do seznamu, takže nulové obdélníky jsou jednoduše přeskočeny a žádná výjimka není vyvolána.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}