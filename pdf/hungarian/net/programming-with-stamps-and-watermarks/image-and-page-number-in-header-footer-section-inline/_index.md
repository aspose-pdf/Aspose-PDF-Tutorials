---
"description": "Tanuld meg, hogyan adhatsz hozzá képet és oldalszámot egy PDF fejléc részéhez az Aspose.PDF for .NET használatával ebből a lépésről lépésre szóló útmutatóból."
"linktitle": "Kép és oldalszám a fejléc és lábléc szakaszban beágyazva"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Kép és oldalszám a fejléc és lábléc szakaszban beágyazva"
"url": "/hu/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section-inline/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kép és oldalszám a fejléc és lábléc szakaszban beágyazva

## Bevezetés

Az Aspose.PDF for .NET egy hatékony eszköz, amely széleskörű lehetőségeket kínál PDF fájlok manipulálására és létrehozására. Akár képeket kell hozzáadnia, fejléceket és lábléceket kell testreszabnia, akár szöveget kell kezelnie, az Aspose.PDF segít. Ebben az oktatóanyagban megvizsgáljuk, hogyan adhat hozzá képet és oldalszámot egy PDF dokumentum fejlécéhez vagy láblécéhez. Vágjunk bele rögtön, és bontsuk le a folyamatot lépésről lépésre.

## Előfeltételek

Mielőtt belevágnánk a kódba, győződjünk meg róla, hogy minden a helyén van a követéshez:

- Aspose.PDF .NET-hez: Töltse le a legújabb verziót innen: [Aspose PDF letöltési oldal](https://releases.aspose.com/pdf/net/).
- Fejlesztői környezet: Szükséged lesz egy C# IDE-re, például a Visual Studio-ra.
- Jogosítvány: Ha még nincs jogosítványod, szerezhetsz egyet [ideiglenes jogosítvány itt](https://purchase.aspose.com/temporary-license/) vagy vásároljon egy komplettet a [Aspose áruház](https://purchase.aspose.com/buy).

Most, hogy megvannak az előfeltételek, kezdjük is el.

## Csomagok importálása

Mielőtt elkezdenéd a kódolást, győződj meg róla, hogy importáltad a szükséges névtereket:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ezek a csomagok lehetővé teszik PDF fájlokkal való munkát és szövegszerkesztést.

## 1. lépés: A dokumentumkönyvtár beállítása

Az első dolog, amit tennünk kell, az az elérési út meghatározása, ahová a PDF fájlunkat menteni fogjuk. Ez az elérési út testreszabható a projekt mappájához vagy a gép bármely más helyéhez.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ez a változó tartalmazza a dokumentum tárolási helyét. `"YOUR DOCUMENT DIRECTORY"` a tényleges úttal.

## 2. lépés: A PDF dokumentum példányosítása

Ebben a lépésben létrehozunk egy új példányt a `Aspose.Pdf.Document` objektum. Ez az objektum a PDF-fájl gerincét fogja képezni.

```csharp
// Dokumentum objektum példányosítása az üres konstruktor meghívásával
Aspose.Pdf.Document pdf1 = new Aspose.Pdf.Document();
```

Itt egy üres PDF fájlt hozunk létre, amelyet később tartalommal tölthetünk fel.

## 3. lépés: Oldal hozzáadása a PDF-hez

A PDF-nek legalább egy oldalra van szüksége, ahová fejléceket, lábléceket és tartalmat adhatsz hozzá. Adjunk hozzá egy üres oldalt a dokumentumunkhoz.

```csharp
// Hozz létre egy oldalt a PDF objektumban
Aspose.Pdf.Page page = pdf1.Pages.Add();
```

Hívással `pdf1.Pages.Add()`, egy új oldal kerül a dokumentumba, amely készen áll a fejléc és a lábléc testreszabására.

## 4. lépés: Fejléc létrehozása és beállítása

Most itt az ideje, hogy létrehozzuk a dokumentum fejlécét. Ide fogjuk hozzáadni a szöveget, a képet és az oldalszámot.

```csharp
// A dokumentum fejléc szakaszának létrehozása
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
// PDF fájl fejlécének beállítása
page.Header = header;
```

Létrehozunk egy `HeaderFooter` objektumot, és rendelje hozzá a `Header` az oldal tulajdonsága, biztosítva, hogy bármi, amit a fejléchez adunk, az az oldal tetején jelenjen meg.

## 5. lépés: Szöveg hozzáadása a fejléchez

A szöveg hozzáadása olyan egyszerű, mint egy `TextFragment` és a tulajdonságainak megadása. Adjunk hozzá színes szöveget a fejlécünkhöz.

```csharp
// Szövegobjektum létrehozása
Aspose.Pdf.Text.TextFragment txt1 = new Aspose.Pdf.Text.TextFragment("Aspose.Pdf is a Robust component by");
// Adja meg a színt
txt1.TextState.ForegroundColor = Color.Blue;
txt1.IsInLineParagraph = true;
```

Ebben a lépésben létrehozunk egy `TextFragment` „Aspose.Pdf egy Robust komponens a következő tartalommal:” és állítsd be a színét kékre. `IsInLineParagraph` tulajdonság biztosítja, hogy a szöveg beágyazott legyen, ami azt jelenti, hogy ugyanabban a sorban jelenik meg, mint a többi elem (például a kép és a további szöveg).

## 6. lépés: Szúrjon be egy beágyazott képet a fejlécbe

A fejléc vizuális vonzóbbá tételéhez hozzáadhat egy képet a szövegbe ágyazva. Ez lehet a cége logója vagy bármilyen más grafika.

```csharp
// Hozz létre egy képobjektumot a szakaszban
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
// Állítsa be a képfájl elérési útját
image1.File = dataDir + "aspose-logo.jpg";
// Kép szélességének beállítása Információk
image1.FixWidth = 50;
image1.FixHeight = 20;
// Jelezze, hogy a seg1 InlineParagraph eleme egy kép.
image1.IsInLineParagraph = true;
```

Itt egy képet adunk a fejléchez egy `Image` objektumot, beállítja az útvonalát, valamint a szélességét és magasságát. `IsInLineParagraph` biztosítja, hogy a kép illeszkedjen a szöveghez.

## 7. lépés: További beágyazott szöveg hozzáadása a fejléc kiegészítéséhez

Adjunk hozzá még egy kis szöveget a beágyazott fejléc kiegészítéséhez.

```csharp
Aspose.Pdf.Text.TextFragment txt2 = new Aspose.Pdf.Text.TextFragment(" Pty Ltd.");
txt2.IsInLineParagraph = true;
txt2.TextState.ForegroundColor = Color.Maroon;
header.Paragraphs.Add(txt1);
header.Paragraphs.Add(image1);
header.Paragraphs.Add(txt2);
```

Ebben a részben létrehozunk egy másikat `TextFragment` „Pty Ltd.” tartalommal, és a színét bordó színűre állítjuk. Mind a szövegrészek, mind a kép hozzáadódnak a fejléchez.

## 8. lépés: Mentse el a PDF-et

Miután beállítottad a fejlécet, itt az ideje menteni a PDF-et.

```csharp
// Mentsd el a Pdf-et
pdf1.Save(dataDir + "ImageAndPageNumberInHeaderFooter_UsingInlineParagraph_out.pdf");
```

A `Save` A metódus a megadott helyre írja a végleges PDF fájlt.

## Következtetés

Gratulálunk! Sikeresen hozzáadott egy képet és szöveget egy PDF dokumentum fejlécéhez az Aspose.PDF for .NET segítségével. Ez az oktatóanyag végigvezette a legfontosabb lépéseken, beleértve a dokumentum létrehozását, oldalak hozzáadását, fejlécek beszúrását és a szöveg és képekhez hasonló beágyazott tartalom elhelyezését. Az Aspose.PDF hihetetlen rugalmasságot biztosít a PDF-fájlok kezelésében, legyen szó akár fejlécek, láblécek vagy összetett tartalom kezeléséről. 

## GYIK

### Hozzáadhatok egy oldalszámot a fejléchez is?
Igen! Könnyen hozzáadhatsz oldalszámot a használatával `TextFragment` osztályt, és szükség szerint formázd meg. Csak illeszd be a fejléc szakaszba beágyazott tartalomként.

### Hogyan tudok háttérképet beállítani a fejlécben?
Használhatod a `BackgroundImage` a tulajdona `HeaderFooter` osztály háttérkép beállításához. Ez azonban nem beágyazott tartalom, és a teljes fejlécterületet lefedi.

### Lehetséges a JPEG-en kívül más képformátumokat is használni?
Abszolút! Az Aspose.PDF különféle képformátumokat támogat, például PNG-t, BMP-t és GIF-et.

### Testreszabhatom a fejlécben lévő szöveg betűtípusát?
Igen, használhatod a `TextState` objektum a szöveg betűtípusának, méretének és stílusának megváltoztatásához.

### Szükségem van licencre az Aspose.PDF for .NET használatához?
Igen, az Aspose.PDF licencet igényel a termelési használathoz, de elkezdheted egy [ingyenes próba itt](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}