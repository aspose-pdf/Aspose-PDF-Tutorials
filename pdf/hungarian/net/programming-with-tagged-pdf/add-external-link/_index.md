---
title: Címkézett külső link hozzáadása tooltip‑pel a PDF-hez az Aspose.Pdf for .NET használatával
weight: 440
limit:
description: Tanulja meg, hogyan adhat hozzá egy címkézett külső hiperhivatkozást megjelenítési szöveggel és tooltip‑pel egy PDF-hez az Aspose.Pdf for .NET használatával.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Tanulja meg, hogyan adhat hozzá egy címkézett külső hiperhivatkozást
    megjelenítési szöveggel és tooltip‑pel egy PDF-hez az Aspose.Pdf for .NET használatával.
  headline: Címkézett külső link hozzáadása tooltip‑pel a PDF-hez az Aspose.Pdf for
    .NET használatával
  type: TechArticle
- description: Tanulja meg, hogyan adhat hozzá egy címkézett külső hiperhivatkozást
    megjelenítési szöveggel és tooltip‑pel egy PDF-hez az Aspose.Pdf for .NET használatával.
  name: Címkézett külső link hozzáadása tooltip‑pel a PDF-hez az Aspose.Pdf for .NET
    használatával
  steps:
  - name: Határozza meg a forrás PDF és a kimeneti fájl útvonalait.
    text: Határozza meg a forrás PDF és a kimeneti fájl útvonalait.
  - name: Ellenőrizze, hogy a forrás PDF létezik-e, és szakítsa meg a folyamatot,
      ha nem található.
    text: Ellenőrizze, hogy a forrás PDF létezik-e, és szakítsa meg a folyamatot,
      ha nem található.
  - name: Nyissa meg a PDF dokumentumot egy using blokkban, hogy biztosítsa a megfelelő
      erőforrás-felszabadítást.
    text: Nyissa meg a PDF dokumentumot egy using blokkban, hogy biztosítsa a megfelelő
      erőforrás-felszabadítást.
  - name: Szerezze meg a címkézett tartalomkezelőt a megnyitott dokumentumhoz.
    text: Szerezze meg a címkézett tartalomkezelőt a megnyitott dokumentumhoz.
  - name: Állítsa be a dokumentum nyelvét English (US) értékre, és adjon a PDF-nek
      egy, a fájlnévből származó címet.
    text: Állítsa be a dokumentum nyelvét English (US) értékre, és adjon a PDF-nek
      egy, a fájlnévből származó címet.
  - name: Hozza vissza a logikai struktúrafa gyökérelemét, amelyhez az új elemeket
      hozzá fogják adni.
    text: Hozza vissza a logikai struktúrafa gyökérelemét, amelyhez az új elemeket
      hozzá fogják adni.
  - name: Hozzon létre egy linkelemet, állítsa be a megjelenített szöveget, a cél
      URL-t és a tooltip címet, majd illessze be a dokumentum struktúrájába.
    text: Hozzon létre egy linkelemet, állítsa be a megjelenített szöveget, a cél
      URL-t és a tooltip címet, majd illessze be a dokumentum struktúrájába.
  - name: Mentse el a frissített PDF-et a megadott kimeneti fájlba.
    text: Mentse el a frissített PDF-et a megadott kimeneti fájlba.
  - name: Írjon ki egy megerősítő üzenetet, amely jelzi, hová lett mentve a módosított
      PDF.
    text: Írjon ki egy megerősítő üzenetet, amely jelzi, hová lett mentve a módosított
      PDF.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` visszaadja a meglévő címkézett tartalmat, ha a
      dokumentum már címkézett; nem hoz létre duplikált fát.'
    question: Mi van, ha a forrás PDF már címkézett – a `pdfDoc.TaggedContent` hívása
      új címkefa létrehozását eredményezi, vagy a meglévőt használja újra?
  - answer: Igen – keresse meg a kívánt `StructureElement`‑et (például egy `Div` vagy
      `Paragraph` elemet egy oldalon) a logikai struktúrafán keresztül, és hívja meg
      a `AppendChild(externalLink)` metódust azon az elemen.
    question: Elhelyezhetem a hiperhivatkozást egy adott oldalon, ahelyett, hogy a
      gyökérelemhez fűznék?
  - answer: A tooltip csak akkor jelenik meg, ha `externalLink.Title` a `pdfDoc.Save`
      előtt van beállítva; a mentés után történő beállítás nem befolyásolja a már
      írt PDF-et.
    question: Kötelező-e a `LinkElement` `Title` tulajdonsága a tooltip megjelenítéséhez,
      és beállítható-e a `Save` hívása után?
  - answer: Rendeljen egy `FileSpecification`‑t (például `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`)
      az `externalLink.Hyperlink`‑hez a `WebHyperlink` helyett.
    question: Hogyan hozhatok létre egy linket egy helyi fájlra a webes URL helyett?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Címkézett külső link beszúrása tooltip‑pel egy PDF-be
og_description: Ágyazzon be egy hozzáférhető hiperhivatkozást látható szöveggel és tooltip‑pel a PDF-jébe az Aspose.Pdf for .NET segítségével.
og_image_alt: Útmutató, amely bemutatja, hogyan adhat hozzá egy címkézett külső hiperhivatkozást tooltip‑pel egy PDF-hez az Aspose.Pdf for .NET használatával.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Címkézett külső link hozzáadása tooltip‑pel a PDF-hez az Aspose.Pdf for .NET használatával
Ez az útmutató bemutatja, hogyan nyithat meg egy meglévő PDF-et az Aspose.Pdf for .NET segítségével, hogyan hozhat létre egy címkézett külső hiperhivatkozást, amely látható megjelenítési szöveget és tooltip címet tartalmaz, hogyan illesztheti be a linket a dokumentum logikai struktúrájába, és hogyan mentheti el a frissített fájlt. A lépések követésével egy hozzáférhető PDF-et hoz létre, ahol a link a címkefája része, és további kontextust biztosít az olvasóknak.

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

**Q: Mi van, ha a forrás PDF már címkézett – a `pdfDoc.TaggedContent` hívása új címkefa létrehozását eredményezi, vagy a meglévőt használja újra?**  
A: `pdfDoc.TaggedContent` visszaadja a meglévő címkézett tartalmat, ha a dokumentum már címkézett; nem hoz létre duplikált fát.

**Q: Elhelyezhetem a hiperhivatkozást egy adott oldalon, ahelyett, hogy a gyökérelemhez fűznék?**  
A: Igen – keresse meg a kívánt `StructureElement`‑et (például egy `Div` vagy `Paragraph` elemet egy oldalon) a logikai struktúrafán keresztül, és hívja meg a `AppendChild(externalLink)` metódust azon az elemen.

**Q: Kötelező-e a `LinkElement` `Title` tulajdonsága a tooltip megjelenítéséhez, és beállítható-e a `Save` hívása után?**  
A: A tooltip csak akkor jelenik meg, ha `externalLink.Title` a `pdfDoc.Save` előtt van beállítva; a mentés után történő beállítás nem befolyásolja a már írt PDF-et.

**Q: Hogyan hozhatok létre egy linket egy helyi fájlra a webes URL helyett?**  
A: Rendeljen egy `FileSpecification`‑t (például `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`) az `externalLink.Hyperlink`‑hez a `WebHyperlink` helyett.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}