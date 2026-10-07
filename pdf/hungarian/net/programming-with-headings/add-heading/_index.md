---
title: Fejléc, nyelv és cím hozzáadása PDF-hez az Aspose.PDF for .NET használatával
weight: 110
limit:
description: Hozzon létre egy PDF-et, állítsa be a nyelvét és címét, és adjon hozzá egy szint‑1 fejlécet az Aspose.PDF for .NET segítségével.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Hozzon létre egy PDF-et, állítsa be a nyelvét és címét, és adjon hozzá
    egy szint‑1 fejlécet az Aspose.PDF for .NET segítségével.
  headline: Fejléc, nyelv és cím hozzáadása PDF-hez az Aspose.PDF for .NET használatával
  type: TechArticle
- description: Hozzon létre egy PDF-et, állítsa be a nyelvét és címét, és adjon hozzá
    egy szint‑1 fejlécet az Aspose.PDF for .NET segítségével.
  name: Fejléc, nyelv és cím hozzáadása PDF-hez az Aspose.PDF for .NET használatával
  steps:
  - name: Határozza meg a kimeneti fájl nevét a létrehozott PDF-hez.
    text: Határozza meg a kimeneti fájl nevét a létrehozott PDF-hez.
  - name: Hozzon létre egy új üres PDF dokumentum példányt (`pdfDoc`) egy `using`
      blokkban.
    text: Hozzon létre egy új üres PDF dokumentum példányt (`pdfDoc`) egy `using`
      blokkban.
  - name: Szerezze meg az `ITaggedContent` interfészt a címkézett PDF struktúrákkal
      való munkához.
    text: Szerezze meg az `ITaggedContent` interfészt a címkézett PDF struktúrákkal
      való munkához.
  - name: Állítsa be a dokumentum alapértelmezett nyelvét angolra (US), és adjon meg
      egy cím metaadatot.
    text: Állítsa be a dokumentum alapértelmezett nyelvét angolra (US), és adjon meg
      egy cím metaadatot.
  - name: Szerezze meg a logikai struktúrafák gyökérelemét.
    text: Szerezze meg a logikai struktúrafák gyökérelemét.
  - name: Hozzon létre egy szint‑1 fejléc elemet, állítsa be a megjelenített szövegét,
      és adja meg a nyelvét.
    text: Hozzon létre egy szint‑1 fejléc elemet, állítsa be a megjelenített szövegét,
      és adja meg a nyelvét.
  - name: Fűzze hozzá a fejléc elemet a gyökérhez, így a fejléc megjelenik a PDF-ben.
    text: Fűzze hozzá a fejléc elemet a gyökérhez, így a fejléc megjelenik a PDF-ben.
  - name: Mentse a PDF-et a megadott fájlba, és zárja le a dokumentum hatókörét.
    text: Mentse a PDF-et a megadott fájlba, és zárja le a dokumentum hatókörét.
  - name: Írjon ki egy megerősítő üzenetet a konzolra.
    text: Írjon ki egy megerősítő üzenetet a konzolra.
  type: HowTo
- questions:
  - answer: '`SetLanguage` meghatározza az egész dokumentum logikai struktúrájának
      alapértelmezett nyelvét; minden olyan elem, amelynek nincs saját nyelve beállítva,
      örökli az \"en-US\" értéket.'
    question: Mi a hatása annak, ha a `tagContent.SetLanguage(\"en-US\")` metódust
      meghívja a PDF-en?
  - answer: A `header.Language` beállítása opcionális; a fejléc a dokumentum alapértelmezett
      nyelvét örökli, hacsak nem ad meg más értéket, ahogyan a példában látható.
    question: Szükséges-e beállítani a `header.Language` értékét, ha már meghívtam
      a `SetLanguage` metódust a dokumentumon?
  - answer: Használja a `tagContent.CreateHeaderElement(2)` metódust szint‑2 fejléc
      létrehozásához; a numerikus argumentum határozza meg a fejléc szintjét, amely
      a PDF struktúrafájában jelenik meg.
    question: Hogyan hozhatok létre szint‑2 fejlécet a szint‑1 helyett?
  - answer: '`SetTitle` a megadott karakterláncot a PDF dokumentum metaadat címmezőjébe
      írja, amely megtekinthető a PDF-olvasókban, és keresésre vagy indexelésre használható.'
    question: Mit csinál a `tagContent.SetTitle(\"PDF Example with Header\")`?
  - answer: A fejléc elem nem kerül hozzáadásra a logikai struktúrafához, ezért nem
      jelenik meg a PDF kimenetben, és a hozzáférhetőségi eszközök sem ismerik fel
      fejlécnek.
    question: Mi történik, ha kihagyom a `rootElement.AppendChild(header)` hívást?
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: Fejléc beszúrása és nyelv beállítása PDF-ben
og_description: Tanulja meg, hogyan hozhat létre PDF-et, állíthatja be a nyelvét és címét, majd adjon hozzá egy szint‑1 fejlécet néhány .NET sor kóddal.
og_image_alt: Útmutató, amely bemutatja, hogyan adjon hozzá fejlécet, állítson be nyelvet és címet egy PDF-ben az Aspose.PDF for .NET használatával
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Fejléc, nyelv és cím hozzáadása PDF-hez az Aspose.PDF for .NET használatával
Ez a bemutató végigvezeti Önt egy új PDF dokumentum létrehozásán az Aspose.PDF for .NET segítségével, alapértelmezett nyelv és dokumentumcím hozzárendelésén, valamint egy szint‑1 fejléc beszúrásán. Megmutatja, hogyan kell a Document, ITaggedContent, StructureElement és HeaderElement osztályokkal dolgozni, hogy megfelelően címkézett PDF-et állítsunk elő, amely alkalmas a hozzáférhetőségi eszközök számára.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


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

**Q: Mi a hatása annak, ha a `tagContent.SetLanguage(\"en-US\")` metódust meghívja a PDF-en?**  
A: `SetLanguage` meghatározza az egész dokumentum logikai struktúrájának alapértelmezett nyelvét; minden olyan elem, amelynek nincs saját nyelve beállítva, örökli az \"en-US\" értéket.

**Q: Szükséges-e beállítani a `header.Language` értékét, ha már meghívtam a `SetLanguage` metódust a dokumentumon?**  
A: A `header.Language` beállítása opcionális; a fejléc a dokumentum alapértelmezett nyelvét örökli, hacsak nem ad meg más értéket, ahogyan a példában látható.

**Q: Hogyan hozhatok létre szint‑2 fejlécet a szint‑1 helyett?**  
A: Használja a `tagContent.CreateHeaderElement(2)` metódust szint‑2 fejléc létrehozásához; a numerikus argumentum határozza meg a fejléc szintjét, amely a PDF struktúrafájában jelenik meg.

**Q: Mit csinál a `tagContent.SetTitle(\"PDF Example with Header\")`?**  
A: `SetTitle` a megadott karakterláncot a PDF dokumentum metaadat címmezőjébe írja, amely megtekinthető a PDF-olvasókban, és keresésre vagy indexelésre használható.

**Q: Mi történik, ha kihagyom a `rootElement.AppendChild(header)` hívást?**  
A: A fejléc elem nem kerül hozzáadásra a logikai struktúrafához, ezért nem jelenik meg a PDF kimenetben, és a hozzáférhetőségi eszközök sem ismerik fel fejlécnek.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}