---
title: Přidejte označený externí odkaz s tooltipem do PDF pomocí Aspose.Pdf pro .NET
weight: 440
limit:
description: Naučte se, jak pomocí Aspose.Pdf pro .NET přidat do PDF označený externí hypertextový odkaz se zobrazovaným textem a tooltipem.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Naučte se, jak pomocí Aspose.Pdf pro .NET přidat do PDF označený externí
    hypertextový odkaz se zobrazovaným textem a tooltipem.
  headline: Přidejte označený externí odkaz s tooltipem do PDF pomocí Aspose.Pdf pro
    .NET
  type: TechArticle
- description: Naučte se, jak pomocí Aspose.Pdf pro .NET přidat do PDF označený externí
    hypertextový odkaz se zobrazovaným textem a tooltipem.
  name: Přidejte označený externí odkaz s tooltipem do PDF pomocí Aspose.Pdf pro .NET
  steps:
  - name: Definujte cesty pro zdrojové PDF a soubor výsledku.
    text: Definujte cesty pro zdrojové PDF a soubor výsledku.
  - name: Ověřte, že zdrojové PDF existuje, a pokud jej nelze najít, přerušte operaci.
    text: Ověřte, že zdrojové PDF existuje, a pokud jej nelze najít, přerušte operaci.
  - name: Otevřete PDF dokument v bloku using, aby byl zajištěn řádný uvolnění prostředků.
    text: Otevřete PDF dokument v bloku using, aby byl zajištěn řádný uvolnění prostředků.
  - name: Získejte správce označeného obsahu (tagged‑content manager) pro otevřený
      dokument.
    text: Získejte správce označeného obsahu (tagged‑content manager) pro otevřený
      dokument.
  - name: Nastavte jazyk dokumentu na angličtinu (US) a dejte PDF titulek odvozený
      od názvu souboru.
    text: Nastavte jazyk dokumentu na angličtinu (US) a dejte PDF titulek odvozený
      od názvu souboru.
  - name: Získejte kořenový prvek stromu logické struktury, do kterého budou přidány
      nové prvky.
    text: Získejte kořenový prvek stromu logické struktury, do kterého budou přidány
      nové prvky.
  - name: Vytvořte prvek odkazu, nastavte jeho zobrazovaný text, cílovou URL a titulek
      tooltipu a poté jej vložte do struktury dokumentu.
    text: Vytvořte prvek odkazu, nastavte jeho zobrazovaný text, cílovou URL a titulek
      tooltipu a poté jej vložte do struktury dokumentu.
  - name: Uložte aktualizované PDF do určeného výstupního souboru.
    text: Uložte aktualizované PDF do určeného výstupního souboru.
  - name: Vypište potvrzovací zprávu, která uvádí, kam byl upravený PDF soubor uložen.
    text: Vypište potvrzovací zprávu, která uvádí, kam byl upravený PDF soubor uložen.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` vrací existující označený obsah, pokud je dokument
      již označený; nevytváří duplicitní strom.'
    question: Co když je zdrojové PDF již označené – vytvoří volání `pdfDoc.TaggedContent`
      nový strom značek, nebo použije existující?
  - answer: Ano – najděte požadovaný `StructureElement` (např. `Div` nebo `Paragraph`
      na stránce) pomocí stromu logické struktury a zavolejte `AppendChild(externalLink)`
      na tomto prvku.
    question: Mohu umístit hypertextový odkaz na konkrétní stránku místo připojení
      k kořenovému prvku?
  - answer: Tooltip se zobrazí pouze pokud je `externalLink.Title` nastaven před voláním
      `pdfDoc.Save`; nastavení po uložení nemá žádný vliv na již zapsané PDF.
    question: Je vlastnost `Title` třídy `LinkElement` vyžadována pro zobrazení tooltipu
      a lze ji nastavit po volání `Save`?
  - answer: Přiřaďte `FileSpecification` (např. `new FileSpecification("file:///C:/Docs/manual.pdf")`)
      k `externalLink.Hyperlink` místo použití `WebHyperlink`.
    question: Jak vytvořit odkaz na lokální soubor místo webové URL?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Vložte označený externí odkaz s tooltipem do PDF
og_description: Vložte přístupný hypertextový odkaz s viditelným textem a tooltipem do svého PDF pomocí Aspose.Pdf pro .NET.
og_image_alt: Návod ukazující, jak přidat do PDF označený externí hypertextový odkaz s tooltipem pomocí Aspose.Pdf pro .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidejte označený externí odkaz s tooltipem do PDF pomocí Aspose.Pdf pro .NET
Tento tutoriál ukazuje, jak otevřít existující PDF pomocí Aspose.Pdf pro .NET, vytvořit označený externí hypertextový odkaz, který obsahuje viditelný zobrazovaný text a titulek tooltipu, vložit odkaz do logické struktury dokumentu a uložit aktualizovaný soubor. Dodržením kroků vytvoříte přístupné PDF, kde je odkaz součástí hierarchie značek a poskytuje čtenářům další kontext.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: Co když je zdrojové PDF již označené – vytvoří volání `pdfDoc.TaggedContent` nový strom značek, nebo použije existující?**  
A: `pdfDoc.TaggedContent` vrací existující označený obsah, pokud je dokument již označený; nevytváří duplicitní strom.

**Q: Mohu umístit hypertextový odkaz na konkrétní stránku místo připojení k kořenovému prvku?**  
A: Ano – najděte požadovaný `StructureElement` (např. `Div` nebo `Paragraph` na stránce) pomocí stromu logické struktury a zavolejte `AppendChild(externalLink)` na tomto prvku.

**Q: Je vlastnost `Title` třídy `LinkElement` vyžadována pro zobrazení tooltipu a lze ji nastavit po volání `Save`?**  
A: Tooltip se zobrazí pouze pokud je `externalLink.Title` nastaven před voláním `pdfDoc.Save`; nastavení po uložení nemá žádný vliv na již zapsané PDF.

**Q: Jak vytvořit odkaz na lokální soubor místo webové URL?**  
A: Přiřaďte `FileSpecification` (např. `new FileSpecification("file:///C:/Docs/manual.pdf")`) k `externalLink.Hyperlink` místo použití `WebHyperlink`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}