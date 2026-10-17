---
title: Porovnejte PDF soubory při ignorování konkrétních oblastí pomocí Aspose.Pdf pro .NET
weight: 201
limit:
description: Naučte se porovnávat PDF soubory vedle sebe a ignorovat vybrané oblasti pomocí Aspose.Pdf pro .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Naučte se porovnávat PDF soubory vedle sebe a ignorovat vybrané oblasti
    pomocí Aspose.Pdf pro .NET.
  headline: Porovnejte PDF soubory při ignorování konkrétních oblastí pomocí Aspose.Pdf
    pro .NET
  type: TechArticle
- description: Naučte se porovnávat PDF soubory vedle sebe a ignorovat vybrané oblasti
    pomocí Aspose.Pdf pro .NET.
  name: Porovnejte PDF soubory při ignorování konkrétních oblastí pomocí Aspose.Pdf
    pro .NET
  steps:
  - name: Definujte cesty k souborům pro oba zdrojové PDF a výstupní diff PDF.
    text: Definujte cesty k souborům pro oba zdrojové PDF a výstupní diff PDF.
  - name: Zkontrolujte, že oba zdrojové PDF soubory existují, a v případě, že některý
      chybí, ukončete s chybovou zprávou.
    text: Zkontrolujte, že oba zdrojové PDF soubory existují, a v případě, že některý
      chybí, ukončete s chybovou zprávou.
  - name: Vytvořte pole obsahující obdélníkovou oblast, která má být v prvním PDF
      ignorována.
    text: Vytvořte pole obsahující obdélníkovou oblast, která má být v prvním PDF
      ignorována.
  - name: Vytvořte pole obsahující obdélníkovou oblast, která má být ve druhém PDF
      ignorována.
    text: Vytvořte pole obsahující obdélníkovou oblast, která má být ve druhém PDF
      ignorována.
  - name: Nastavte porovnání vedle sebe a přiřaďte pole s ignorovanými oblastmi k
      příslušným vlastnostem.
    text: Nastavte porovnání vedle sebe a přiřaďte pole s ignorovanými oblastmi k
      příslušným vlastnostem.
  - name: Načtěte oba PDF soubory a spusťte porovnání vedle sebe, čímž vytvoříte diff
      soubor na zadané cestě.
    text: Načtěte oba PDF soubory a spusťte porovnání vedle sebe, čímž vytvoříte diff
      soubor na zadané cestě.
  - name: Vytiskněte potvrzovací zprávu, která uvádí, že porovnání bylo dokončeno
      a kde byl diff PDF uložen.
    text: Vytiskněte potvrzovací zprávu, která uvádí, že porovnání bylo dokončeno
      a kde byl diff PDF uložen.
  type: HowTo
- questions:
  - answer: Souřadnice jsou v bodech (1/72 palce) s počátkem v levém dolním rohu stránky,
      takže první dvě čísla představují X/Y levého dolního rohu a poslední dvě X/Y
      pravého horního rohu.
    question: Jaký souřadnicový systém používají hodnoty `Rectangle` při definování
      ignorovaných zón?
  - answer: Ano – poskytněte více objektů `Aspose.Pdf.Rectangle` v poli `ExcludeAreas1`
      (nebo `ExcludeAreas2`); každý obdélník bude během porovnání vyloučen samostatně.
    question: Mohu v jednom dokumentu ignorovat více než jednu obdélníkovou oblast?
  - answer: Ne. `ExcludeAreas1` se vztahuje na první PDF a `ExcludeAreas2` na druhé,
      takže můžete pro každý dokument zadat jiné souřadnice.
    question: Musí být ignorované obdélníky v obou PDF identické?
  - answer: Aspose.Pdf tiše ignoruje obdélníky, které jsou zcela mimo stránku; nemají
      žádný vliv na výsledek porovnání.
    question: Co se stane, pokud je obdélník definován mimo hranice stránky?
  - answer: Pole `ExcludeAreas` se vztahují na každou stránku, takže je potřeba přidat
      stejný `Rectangle` do kolekce každé stránky (např. projít `pdf.Pages` a přiřadit
      pole) před voláním `SideBySidePdfComparer.Compare`.
    question: Jak mohu vyloučit stejnou oblast na každé stránce PDF?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Ignorovat oblasti při porovnávání PDF
og_description: Podívejte se, jak přeskočit vybrané oblasti při porovnání PDF vedle sebe a získat čistý diff PDF.
og_image_alt: Průvodce ukazující porovnání PDF vedle sebe s vyloučenými obdélníkovými oblastmi pomocí Aspose.Pdf pro .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Porovnejte PDF soubory při ignorování konkrétních oblastí pomocí Aspose.Pdf pro .NET
Tento tutoriál ukazuje, jak porovnat dva PDF dokumenty vedle sebe pomocí Aspose.Pdf pro .NET při vyloučení určených obdélníkových oblastí z analýzy. Definováním vylučovacích oblastí v každém souboru se vytvořený diff PDF zvýrazní pouze změny, které jsou podstatné, což usnadňuje soustředit se na relevantní rozdíly.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Jaký souřadnicový systém používají hodnoty `Rectangle` při definování ignorovaných zón?**  
A: Souřadnice jsou v bodech (1/72 palce) s počátkem v levém dolním rohu stránky, takže první dvě čísla představují X/Y levého dolního rohu a poslední dvě X/Y pravého horního rohu.

**Q: Mohu v jednom dokumentu ignorovat více než jednu obdélníkovou oblast?**  
A: Ano – poskytněte více objektů `Aspose.Pdf.Rectangle` v poli `ExcludeAreas1` (nebo `ExcludeAreas2`); každý obdélník bude během porovnání vyloučen samostatně.

**Q: Musí být ignorované obdélníky v obou PDF identické?**  
A: Ne. `ExcludeAreas1` se vztahuje na první PDF a `ExcludeAreas2` na druhé, takže můžete pro každý dokument zadat jiné souřadnice.

**Q: Co se stane, pokud je obdélník definován mimo hranice stránky?**  
A: Aspose.Pdf tiše ignoruje obdélníky, které jsou zcela mimo stránku; nemají žádný vliv na výsledek porovnání.

**Q: Jak mohu vyloučit stejnou oblast na každé stránce PDF?**  
A: Pole `ExcludeAreas` se vztahují na každou stránku, takže je potřeba přidat stejný `Rectangle` do kolekce každé stránky (např. projít `pdf.Pages` a přiřadit pole) před voláním `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}