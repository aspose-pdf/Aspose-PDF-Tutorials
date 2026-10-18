---
title: Side‑by‑Side PDF összehasonlítás annotációk kizárásával az Aspose.Pdf for .NET segítségével
weight: 101
limit:
description: Lépésről‑lépésre útmutató a PDF-ek összehasonlításához és az annotációs területek kizárásához az Aspose.Pdf for .NET használatával.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Lépésről‑lépésre útmutató a PDF-ek összehasonlításához és az annotációs
    területek kizárásához az Aspose.Pdf for .NET használatával.
  headline: Side‑by‑Side PDF összehasonlítás annotációk kizárásával az Aspose.Pdf
    for .NET segítségével
  type: TechArticle
- description: Lépésről‑lépésre útmutató a PDF-ek összehasonlításához és az annotációs
    területek kizárásához az Aspose.Pdf for .NET használatával.
  name: Side‑by‑Side PDF összehasonlítás annotációk kizárásával az Aspose.Pdf for
    .NET segítségével
  steps:
  - name: Határozza meg a fájlútvonalakat az elsődleges PDF, a másodlagos PDF és a
      kimeneti diff PDF számára.
    text: Határozza meg a fájlútvonalakat az elsődleges PDF, a másodlagos PDF és a
      kimeneti diff PDF számára.
  - name: Ellenőrizze, hogy mindkét bemeneti PDF fájl létezik-e, és ha valamelyik
      hiányzik, abortáljon egy hibaüzenettel.
    text: Ellenőrizze, hogy mindkét bemeneti PDF fájl létezik-e, és ha valamelyik
      hiányzik, abortáljon egy hibaüzenettel.
  - name: Nyissa meg a két PDF fájlt Document objektumként (pdfA és pdfB) egy using
      blokkban, hogy azok automatikusan felszabaduljanak.
    text: Nyissa meg a két PDF fájlt Document objektumként (pdfA és pdfB) egy using
      blokkban, hogy azok automatikusan felszabaduljanak.
  - name: Gyűjtse össze minden annotáció körülhatároló téglalapját a pdfA-ban, és
      tárolja őket az ignoredRectsA-ban.
    text: Gyűjtse össze minden annotáció körülhatároló téglalapját a pdfA-ban, és
      tárolja őket az ignoredRectsA-ban.
  - name: Gyűjtse össze minden annotáció körülhatároló téglalapját a pdfB-ban, és
      tárolja őket az ignoredRectsB-ban.
    text: Gyűjtse össze minden annotáció körülhatároló téglalapját a pdfB-ban, és
      tárolja őket az ignoredRectsB-ban.
  - name: Hozzon létre egy SideBySideComparisonOptions objektumot, és rendelje hozzá
      a korábban összegyűjtött annotációs téglalapokat az ExcludeAreas1 és ExcludeAreas2
      tulajdonságokhoz, hogy ezek a területek figyelmen kívül legyenek hagyva az összehasonlítás
      során.
    text: Hozzon létre egy SideBySideComparisonOptions objektumot, és rendelje hozzá
      a korábban összegyűjtött annotációs téglalapokat az ExcludeAreas1 és ExcludeAreas2
      tulajdonságokhoz, hogy ezek a területek figyelmen kívül legyenek hagyva az összehasonlítás
      során.
  - name: Futtassa az oldal‑oldali PDF összehasonlítást a két Document objektummal
      és a beállított opciókkal, az eredményt az outputPdf-be írva.
    text: Futtassa az oldal‑oldali PDF összehasonlítást a két Document objektummal
      és a beállított opciókkal, az eredményt az outputPdf-be írva.
  - name: Szabadítsa fel a Document objektumokat, és lépjen ki a using blokkból.
    text: Szabadítsa fel a Document objektumokat, és lépjen ki a using blokkból.
  - name: Írjon ki egy megerősítő üzenetet, amely jelzi, hogy az összehasonlítás befejeződött,
      és megmutatja, hol lett elmentve a diff PDF.
    text: Írjon ki egy megerősítő üzenetet, amely jelzi, hogy az összehasonlítás befejeződött,
      és megmutatja, hol lett elmentve a diff PDF.
  type: HowTo
- questions:
  - answer: Igen. A kód egyszerűen nem ad hozzá téglalapokat a megfelelő `ignoredRects`
      listához, így az `ExcludeAreas1`/`ExcludeAreas2` egy üres tömböt kap, és az
      összehasonlító a teljes oldalt dolgozza fel.
    question: Mi történik, ha egy PDF oldalnak nincsenek annotációi – működni fog-e
      az összehasonlítás?
  - answer: Állítsa be az `ExcludeAreas1` (vagy `ExcludeAreas2`) értékét a gyűjtött
      téglalapokra, és hagyja a másik tulajdonságot üres tömbként; az összehasonlító
      csak a megadott dokumentumban lévő területeket hagyja figyelmen kívül.
    question: Kizárhatok csak egy dokumentumból annotációkat, miközben a másik dokumentum
      annotációi megmaradnak a diffben?
  - answer: Az átfedő téglalapokat a comparer belsőleg egyesíti, így az átfedő annotációs
      határok biztonságosan kizárásra kerülnek dupla számolás nélkül.
    question: Az átfedő annotációs téglalapok okoznak-e problémát az `ExcludeAreas`
      esetén?
  - answer: Igen, állítsa be a `compareOpts.ExcludeTables = true;` – ez a jelző az
      `ExcludeAreas1`/`ExcludeAreas2` mellett működik, és a táblázati területeket
      is figyelmen kívül hagyja.
    question: Van-e mód arra, hogy a táblázatokat is kizárjuk az annotációk mellett
      ugyanazzal az options objektummal?
  - answer: A kód ellenőrzi, hogy `if (a != null && a.Rect != null)` mielőtt hozzáadná
      a listához, így a null téglalapok egyszerűen kihagyásra kerülnek, és nem dobódik
      kivétel.
    question: Mi van, ha egy annotáció `Rect` tulajdonsága null – a kód kivételt dob?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: PDF-ek összehasonlítása annotációk nélkül
og_description: Futtasson egy oldal‑oldali PDF diff-et, amely kihagyja az összes annotációs jelet.
og_image_alt: Útmutató egy oldal‑oldali PDF összehasonlításhoz, amely kizárja az annotációs területeket az Aspose.Pdf for .NET használatával
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Side‑by‑Side PDF összehasonlítás annotációk kizárásával az Aspose.Pdf for .NET segítségével
Ez az útmutató bemutatja, hogyan lehet két PDF fájlt összehasonlítani az Aspose.Pdf for .NET használatával, miközben figyelmen kívül hagyjuk az annotációk tartalmát. Kinyeri az összes annotáció körülhatároló dobozát minden dokumentumból, ezeket a területeket a SideBySideComparisonOptions-ba adja, majd egy oldal‑oldali összehasonlítást hajt végre. Az eredmény egy diff PDF, amely csak a nem‑annotációs változásokat emeli ki.

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

**Q: Mi történik, ha egy PDF oldalnak nincsenek annotációi – működni fog-e az összehasonlítás?**  
A: Igen. A kód egyszerűen nem ad hozzá téglalapokat a megfelelő `ignoredRects` listához, így az `ExcludeAreas1`/`ExcludeAreas2` egy üres tömböt kap, és az összehasonlító a teljes oldalt dolgozza fel.

**Q: Kizárhatok csak egy dokumentumból annotációkat, miközben a másik dokumentum annotációi megmaradnak a diffben?**  
A: Állítsa be az `ExcludeAreas1` (vagy `ExcludeAreas2`) értékét a gyűjtött téglalapokra, és hagyja a másik tulajdonságot üres tömbként; az összehasonlító csak a megadott dokumentumban lévő területeket hagyja figyelmen kívül.

**Q: Az átfedő annotációs téglalapok okoznak-e problémát az `ExcludeAreas` esetén?**  
A: Az átfedő téglalapokat a comparer belsőleg egyesíti, így az átfedő annotációs határok biztonságosan kizárásra kerülnek dupla számolás nélkül.

**Q: Van-e mód arra, hogy a táblázatokat is kizárjuk az annotációk mellett ugyanazzal az options objektummal?**  
A: Igen, állítsa be a `compareOpts.ExcludeTables = true;` – ez a jelző az `ExcludeAreas1`/`ExcludeAreas2` mellett működik, és a táblázati területeket is figyelmen kívül hagyja.

**Q: Mi van, ha egy annotáció `Rect` tulajdonsága null – a kód kivételt dob?**  
A: A kód ellenőrzi, hogy `if (a != null && a.Rect != null)` mielőtt hozzáadná a listához, így a null téglalapok egyszerűen kihagyásra kerülnek, és nem dobódik kivétel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}