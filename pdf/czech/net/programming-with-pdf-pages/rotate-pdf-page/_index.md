---
title: Otočte jednu stránku PDF o 180 stupňů pomocí Aspose.PDF pro .NET
weight: 260
limit:
description: Naučte se, jak otočit třetí stránku PDF o 180° pomocí Aspose.PDF pro .NET.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Naučte se, jak otočit třetí stránku PDF o 180° pomocí Aspose.PDF pro
    .NET.
  headline: Otočte jednu stránku PDF o 180 stupňů pomocí Aspose.PDF pro .NET
  type: TechArticle
- description: Naučte se, jak otočit třetí stránku PDF o 180° pomocí Aspose.PDF pro
    .NET.
  name: Otočte jednu stránku PDF o 180 stupňů pomocí Aspose.PDF pro .NET
  steps:
  - name: Soubor obsahuje pouze vysvětlující komentáře a žádný spustitelný kód, slouží
      jako zástupný soubor pro původní příklad.
    text: Soubor obsahuje pouze vysvětlující komentáře a žádný spustitelný kód, slouží
      jako zástupný soubor pro původní příklad.
  type: HowTo
- questions:
  - answer: Použijte kolekci stránek SDK s nulovým indexováním, např. `pdfDocument.Pages[2]`,
      protože index 2 odpovídá třetí stránce.
    question: Jak mohu cílit na třetí stránku PDF pro otočení?
  - answer: Vlastnost rotation akceptuje pouze čtyři standardní hodnoty 0, 90, 180
      a 270 stupňů; jakákoli jiná hodnota je zaokrouhlena na nejbližší povolený úhel.
    question: Mohu otočit stránku o úhel jiný než 180 stupňů?
  - answer: Otočení se aplikuje pouze na `PdfDocument` v paměti; musíte zavolat `pdfDocument.Save(\"output.pdf\")`
      (nebo podobnou metodu ukládání), aby se změny zapsaly do nového souboru, přičemž
      zdroj zůstane nezměněn.
    question: Změní se při otáčení stránky původní soubor automaticky?
  - answer: SDK automaticky přepočítá pozice anotací a formulářových polí, aby zůstaly
      správně zarovnané s novou orientací.
    question: Co se stane s anotacemi nebo formulářovými poli po otočení stránky?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: Otočte stránku PDF o 180° pomocí Aspose.PDF
og_description: Rychle převraťte třetí stránku svého PDF vzhůru nohama pomocí několika řádků kódu Aspose.PDF pro .NET.
og_image_alt: Průvodce ukazující kód, který otáčí třetí stránku PDF o 180 stupňů pomocí Aspose.PDF pro .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Otočte jednu stránku PDF o 180 stupňů pomocí Aspose.PDF pro .NET
V tomto tutoriálu se naučíte, jak otočit třetí stránku PDF dokumentu o 180 stupňů pomocí Aspose.PDF pro .NET. Příklad ukazuje, jak načíst PDF, vybrat stránku 3, aplikovat otočení a uložit aktualizovaný soubor. Tento přístup vám umožní převrátit konkrétní stránku, aniž byste měnili orientaci ostatních stránek.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: Jak mohu cílit na třetí stránku PDF pro otočení?**  
A: Použijte kolekci stránek SDK s nulovým indexováním, např. `pdfDocument.Pages[2]`, protože index 2 odpovídá třetí stránce.

**Q: Mohu otočit stránku o úhel jiný než 180 stupňů?**  
A: Vlastnost rotation akceptuje pouze čtyři standardní hodnoty 0, 90, 180 a 270 stupňů; jakákoli jiná hodnota je zaokrouhlena na nejbližší povolený úhel.

**Q: Změní se při otáčení stránky původní soubor automaticky?**  
A: Otočení se aplikuje pouze na `PdfDocument` v paměti; musíte zavolat `pdfDocument.Save(\"output.pdf\")` (nebo podobnou metodu ukládání), aby se změny zapsaly do nového souboru, přičemž zdroj zůstane nezměněn.

**Q: Co se stane s anotacemi nebo formulářovými poli po otočení stránky?**  
A: SDK automaticky přepočítá pozice anotací a formulářových polí, aby zůstaly správně zarovnané s novou orientací.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}