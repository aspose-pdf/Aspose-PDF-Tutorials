---
"description": "Tanuld meg, hogyan húzhatsz ki szavakat egy PDF-ben az Aspose.PDF for .NET segítségével ezzel az átfogó, lépésről lépésre haladó útmutatóval. Fejleszd dokumentumszerkesztési készségeidet."
"linktitle": "Szavak áthúzása"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Szavak áthúzása"
"url": "/hu/net/annotations/strikeoutwords/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Szavak áthúzása

## Bevezetés

Előfordult már veled, hogy egy adott szövegrészt áthúzással kellett kiemelned egy PDF-ben? Akár dokumentumokat nézel át, akár szöveget jelölsz meg, vagy egyszerűen csak bizonyos részeket kell kiemelned, a szavak áthúzása értékes eszköz lehet. Ebben az oktatóanyagban megvizsgáljuk, hogyan teheted ezt meg az Aspose.PDF for .NET használatával. Ez az átfogó útmutató végigvezet az egyes lépéseken, biztosítva, hogy minden szükséges információval rendelkezz ahhoz, hogy ezt a funkciót hatékonyan megvalósítsd a .NET alkalmazásaidban. 

## Előfeltételek

Mielőtt belevágnánk a kódba, van néhány előfeltétel, aminek meg kell felelned ahhoz, hogy követhesd ezt az oktatóanyagot:

1. Aspose.PDF .NET könyvtárhoz: Győződjön meg róla, hogy telepítve van az Aspose.PDF .NET könyvtár. [töltsd le itt](https://releases.aspose.com/pdf/net/).

2. .NET-keretrendszer: Győződjön meg arról, hogy a .NET-keretrendszer telepítve van a gépén. Ez az oktatóanyag .NET-alkalmazásokhoz készült.

3. Fejlesztői környezet: A kód írásához és futtatásához szükséged lesz egy IDE-re, például a Visual Studio-ra.

4. PDF dokumentum: Készítsen elő egy minta PDF fájlt, amellyel dolgozni szeretne. Ebben a dokumentumban fogjuk áthúzni a szöveget.

5. C# alapismeretek: A C# programozással való ismeret szükséges a bemutató lépéseinek megértéséhez és megvalósításához.

## Csomagok importálása

Mielőtt elkezdhetnénk a kódolást, importálnunk kell a szükséges névtereket a .NET projektünkbe. Ez hozzáférést biztosít számunkra azokhoz az osztályokhoz és metódusokhoz, amelyek a PDF fájlok Aspose.PDF segítségével történő kezeléséhez szükségesek.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Ezek a névterek elengedhetetlenek a PDF dokumentumokkal való munkához, a szöveg kezeléséhez és az olyan megjegyzések hozzáadásához, mint az áthúzások.

Ebben a részben egyszerű, könnyen kezelhető lépésekre bontjuk a szavak PDF-dokumentumban történő áthúzásának folyamatát. Minden lépést részletes magyarázat kísér, hogy biztosan megértsd, hogyan működik minden.

## 1. lépés: Töltse be a PDF dokumentumot

Az első lépés a szerkeszteni kívánt PDF dokumentum betöltése. Ebben a dokumentumban fogsz kihúzni bizonyos szavakat vagy kifejezéseket.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Nyissa meg a PDF dokumentumot
Document document = new Document(dataDir + "input.pdf");
```

- `dataDir`: Ez a változó a dokumentumkönyvtár elérési útját tartalmazza. Csere `"YOUR DOCUMENT DIRECTORY"` a PDF-fájl tényleges elérési útjával.
- `Document`A `Document` Az osztály egy PDF dokumentumot reprezentál. A fájl elérési útját átadva a konstruktorának, megnyitjuk a PDF fájlt feldolgozásra.

## 2. lépés: Hozz létre egy TextFragment Absorber-t adott szöveg kereséséhez

Következőként létrehozunk egy példányt a következőből: `TextFragmentAbsorber` egy adott szövegrészlet kereséséhez a PDF dokumentumban. Ez lehetővé teszi számunkra, hogy megtaláljuk a kihúzni kívánt szöveget.

```csharp
// TextFragment Absorber példány létrehozása egy adott szövegrészlet kereséséhez
Aspose.Pdf.Text.TextFragmentAbsorber textFragmentAbsorber = new Aspose.Pdf.Text.TextFragmentAbsorber("Estoque");
```

- `TextFragmentAbsorber`Ez az osztály a PDF dokumentumban található adott szövegrészek megkeresésére és feldolgozására szolgál. Ebben a példában az „Estoque” szót keressük. Cserélje le az „Estoque” szót a dokumentumban keresni kívánt szóra vagy kifejezésre.

## 3. lépés: Ismételje át a PDF dokumentum oldalait

Most, hogy megvan a miénk `TextFragmentAbsorber`, a PDF dokumentum minden egyes oldalán végig kell mennünk a megadott szöveg megtalálásához.

```csharp
// Ismételd végig a PDF dokumentum oldalait
for (int i = 1; i <= document.Pages.Count; i++)
{
    // A PDF dokumentum aktuális oldalának lekérése
    Page page = document.Pages[i];
    page.Accept(textFragmentAbsorber);
}
```

- `for (int i = 1; i <= document.Pages.Count; i++)`: Ez a ciklus végigmegy a PDF dokumentum minden oldalán.
- `document.Pages[i]`: Lekéri az aktuálisan feldolgozott oldalt.
- `page.Accept(textFragmentAbsorber)`: Ez a módszer a következőt alkalmazza: `TextFragmentAbsorber` az aktuális oldalra ugrik, a megadott szöveget keresve.

## 4. lépés: A szövegrészek gyűjtése és feldolgozása

Miután végigmentünk az oldalakon, összegyűjtjük a talált szövegrészeket, és előkészítjük őket a további feldolgozásra.

```csharp
// Elnyelt szövegrészek gyűjteményének létrehozása
Aspose.Pdf.Text.TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`Ez a gyűjtemény a dokumentumban található összes szövegrészletet tárolja. A következő lépésben ezt a gyűjteményt fogjuk használni a szöveg áthúzásához.

## 5. lépés: Ismételd át a szövegrészeket, és húzd ki őket

Ebben a lépésben végigmegyünk a gyűjteményünkben található összes szövegrészleten, és áthúzott megjegyzést alkalmazunk rájuk.

```csharp
// Szövegtöredékek gyűjteményének ismétlése
for (int j = 1; j <= textFragmentCollection.Count; j++)
{
	Aspose.Pdf.Text.TextFragment textFragment = textFragmentCollection[j];

    // A TextFragment objektum téglalap alakú méreteinek lekérése
    Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(
        (float)textFragment.Position.XIndent,
        (float)textFragment.Position.YIndent,
        (float)textFragment.Position.XIndent + (float)textFragment.Rectangle.Width,
        (float)textFragment.Position.YIndent + (float)textFragment.Rectangle.Height);

    // Áthúzott jegyzet példányának példányosítása
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.Page, rect);

    // Az áthúzott megjegyzés tulajdonságainak beállítása
    strikeOut.Opacity = .80f;
    strikeOut.Border = new Border(strikeOut);
    strikeOut.Color = Aspose.Pdf.Color.Red;

    // Adja hozzá a megjegyzést a szövegrészlet oldalának megjegyzésgyűjteményéhez
    textFragment.Page.Annotations.Add(strikeOut);
}
```

- `TextFragment textFragment = textFragmentCollection[j]`: Ez a sor visszaadja az aktuális szövegrészletet.
- `Aspose.Pdf.Rectangle`Kiszámítjuk a szövegrészlet téglalap alakú méreteit, hogy meghatározzuk, hová kell alkalmazni az áthúzást.
- `StrikeOutAnnotation`Ez az osztály az áthúzott annotációt jelöli. A kiszámított téglalappal és az aktuális oldallal példányosítjuk.
- `strikeOut.Opacity`: Ez a tulajdonság az áthúzott rész átlátszóságát állítja be, így az 80%-ban látható.
- `strikeOut.Color`kihúzott rész színét pirosra állítottuk. Ezt bármilyen kívánt színre módosíthatod.
- `textFragment.Page.Annotations.Add(strikeOut)`: Ez hozzáadja az áthúzott megjegyzést az oldalhoz.

## 6. lépés: Mentse el a módosított PDF dokumentumot

Az utolsó lépés a módosított PDF dokumentum mentése az áthúzásokkal.

```csharp
// Mentse el a frissített PDF dokumentumot
dataDir = dataDir + "StrikeOutWords_out.pdf";
document.Save(dataDir);
```

- `dataDir + "StrikeOutWords_out.pdf"`: Ez új fájlnevet hoz létre a módosított dokumentum számára. Az eredeti fájl változatlan marad.
- `document.Save(dataDir)`: A PDF dokumentumot az áthúzott részekkel együtt menti a megadott helyre.

## Következtetés

Gratulálunk! Sikeresen áthúzott bizonyos szavakat egy PDF dokumentumban az Aspose.PDF for .NET segítségével. Ezt a lépésenkénti útmutatót követve mostantól testreszabhatja a PDF dokumentumokat a szöveg kiemelésével vagy áthúzásával, így dinamikusabbá és az igényeihez igazodóbbá teheti őket. Akár jogi dokumentumokat jegyzetel, akár jelentéseket készít, vagy csak szöveget jelöl meg ellenőrzésre, ez az oktatóanyag felvértezte Önt a hatékony munkavégzéshez.

## GYIK

### Meg tudom változtatni az áthúzott rész színét?

Igen, a színt módosíthatod a `strikeOut.Color` tulajdonság. Például beállíthatja úgy, hogy `Aspose.Pdf.Color.Blue` egy kék strikeoutért.

### Lehetséges egyszerre több szót is kihúzni?

Abszolút! A `TextFragmentAbsorber` segítségével bármely szót vagy kifejezést kereshet a dokumentumban. Az áthúzást több példányra is alkalmazhatja a következőn keresztüli iterációval: `TextFragmentCollection`.

### Mi van, ha csak bizonyos oldalakon szeretnék szöveget áthúzni?

Módosíthatja az oldalakon végighaladó ciklust úgy, hogy csak a módosítani kívánt oldalakat tartalmazza. Például: `for (int i = 1; i <= 3; i++)` csak az első három oldalra alkalmazná az áthúzást.

### Hogyan tudom beállítani az áthúzott vonal vastagságát?

Az áthúzott vonal vastagságát a következő módosításával állíthatja be: `Border` a tulajdona `StrikeOutAnnotation`Ez lehetővé teszi az áthúzott rész megjelenésének testreszabását.

### Van mód a dokumentum mentése után az áthúzás visszavonására?

dokumentum mentése után az áthúzás végleges. Ha meg kell őriznie az eredeti szöveget az áthúzás nélkül, érdemes lehet biztonsági másolatot készíteni az eredeti dokumentumról, mielőtt bármilyen módosítást alkalmazna.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}