---
"description": "Ismerje meg, hogyan kereshet és nyerhet ki szöveget egy adott oldalról PDF fájlban az Aspose.PDF for .NET használatával."
"linktitle": "Szöveges oldal keresése és lekérése PDF fájlban"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Szöveges oldal keresése és lekérése PDF fájlban"
"url": "/hu/net/programming-with-text/search-and-get-text-page/"
"weight": 430
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Szöveges oldal keresése és lekérése PDF fájlban

## Bevezetés

Előfordult már veled, hogy egy PDF dokumentumban egy adott szövegrészt kellett megkeresned, és kinyerned későbbi felhasználás céljából? Talán egy olyan alkalmazást építesz, amely dokumentumokat dolgoz fel, és precíz adatkinyerést igényel, vagy talán csak hatékonyan kell elemezned a PDF-eket. Bármi is legyen az eseted, jó helyen jársz! Ebben az oktatóanyagban elmerülünk abban, hogyan kereshetsz és kinyerhetsz szöveget egy PDF fájl egy oldalán az Aspose.PDF for .NET segítségével. Akár kezdő, akár tapasztalt fejlesztő vagy, ez az útmutató végigvezet az egyes lépéseken társalgási és lebilincselő módon. Készen állsz? Kezdjük is!

## Előfeltételek

Mielőtt belevágnánk a kódolásba, győződjünk meg róla, hogy minden szükséges dolog megvan:

1. Aspose.PDF .NET könyvtárhoz: Letöltheti innen [itt](https://releases.aspose.com/pdf/net/) vagy szerezzen be egy ingyenes próbaverziót ugyanazon a linken keresztül. A vásárláshoz látogasson el a következő oldalra: [Aspose áruház](https://purchase.aspose.com/buy).
2. .NET-keretrendszer: Szükséged lesz egy működő .NET fejlesztői környezetre, például a Visual Studio-ra.
3. PDF-fájl: Szükséged lesz egy minta PDF-fájlra, amelyben kereshetünk és kinyerhetünk a szövegből. Ebben az oktatóanyagban tegyük fel, hogy a fájl neve `SearchAndGetTextPage.pdf`.

## Csomagok importálása

Először is importálnunk kell a szükséges névtereket az Aspose.PDF for .NET használatához. Győződj meg róla, hogy ezek szerepelnek a kódod elején.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System
```

Most, hogy áttekintettük az előfeltételeket, bontsuk le a kódot lépésről lépésre. Minden lépést világosan felvázoltunk, hogy könnyen követhető legyen.

## 1. lépés: Állítsa be a Dokumentumok könyvtár elérési útját

Mielőtt elkezdenéd a PDF-fájl használatát, meg kell adnod a PDF-dokumentum tárolási útvonalát. Ez biztosítja, hogy a program hozzáférhessen a fájlhoz.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- dataDir: Ez annak a mappának az elérési útja, ahol a PDF-fájlok tárolva vannak. Cserélje ki `"YOUR DOCUMENT DIRECTORY"` a PDF tényleges elérési útjával.

## 2. lépés: Töltse be a PDF dokumentumot

A következő lépés a PDF dokumentum betöltése a memóriába, hogy dolgozhasson vele. Így teheti meg:

```csharp
Document pdfDocument = new Document(dataDir + "SearchAndGetTextPage.pdf");
```

- Dokumentum: Ez az Aspose.PDF osztály, amely betölti a PDF fájlt.
- pdfDocument: Az a változó, ahol a PDF fájl a betöltés után tárolódik.

## 3. lépés: Hozz létre egy szövegelnyelő objektumot

A `TextFragmentAbsorber` osztály lehetővé teszi adott szöveg keresését a PDF-ben. Hozzunk létre egy példányt ebből az osztályból, hogy megkeressük egy adott keresési kifejezés összes előfordulását.

```csharp
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Figure");
```

- TextFragmentAbsorber: Ez az osztály felelős a szöveg megkereséséért és kinyeréséért a PDF-ből.
- „Ábra”: Cserélje le ezt bármilyen szöveggel, amelyet a PDF-ben keresni szeretne.

## 4. lépés: A szövegelnyelő alkalmazása a teljes PDF-re

Miután a szövegelnyelő be van állítva, meg kell adni a programnak, hogy keressen végig a PDF összes oldalán.

```csharp
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- Accept(): Ez a metódus a szövegelnyelőt alkalmazza a PDF-re, és minden oldalon beolvassa a megadott szöveget.

## 5. lépés: A kinyert szöveg visszakeresése és iterációja

Most, hogy beolvastuk a PDF-et, itt az ideje, hogy lekérjük és megjelenítsük az eredményeket. Végigmegyünk a kinyert szövegrészeken.

```csharp
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- TextFragmentCollection: Ez a gyűjtemény tartalmazza a szövegelnyelő által talált szövegtöredékek összes példányát.

## 6. lépés: Végigmegyünk az egyes töredékeken, és kinyerjük az adatokat

Most végigmegyünk a `textFragmentCollection` és kinyerheti az egyes szövegszegmensek különböző tulajdonságait, például a pozícióját, a betűtípus részleteit és a színét.

```csharp
foreach (TextFragment textFragment in textFragmentCollection)
{
	foreach (TextSegment textSegment in textFragment.Segments)
	{
		Console.WriteLine("Text : {0} ", textSegment.Text);
		Console.WriteLine("Position : {0} ", textSegment.Position);
		Console.WriteLine("XIndent : {0} ", textSegment.Position.XIndent);
		Console.WriteLine("YIndent : {0} ", textSegment.Position.YIndent);
		Console.WriteLine("Font - Name : {0}", textSegment.TextState.Font.FontName);
		Console.WriteLine("Font - IsAccessible : {0} ", textSegment.TextState.Font.IsAccessible);
		Console.WriteLine("Font - IsEmbedded : {0} ", textSegment.TextState.Font.IsEmbedded);
		Console.WriteLine("Font - IsSubset : {0} ", textSegment.TextState.Font.IsSubset);
		Console.WriteLine("Font Size : {0} ", textSegment.TextState.FontSize);
		Console.WriteLine("Foreground Color : {0} ", textSegment.TextState.ForegroundColor);
	}
}
```

- TextFragment: Minden töredék a talált szöveg egyes részeit tartalmazza.
- TextSegment: Minden töredék több szegmensből állhat, amelyek a szöveg különböző részeit képviselik.
- TextState: Ez részletes információkat nyújt a szöveg betűtípusáról, méretéről és színéről.

Ebben a ciklusban kinyomtatjuk a részleteket, például a tényleges szöveget, annak pozícióját (X és Y koordináták), a betűtípust, azt, hogy a betűtípus be van-e ágyazva a PDF-be, és a szöveg előtérszínét.

## Következtetés

És íme! Sikeresen kerestél és kinyertél szöveget egy PDF fájlból az Aspose.PDF for .NET segítségével. Hihetetlen, mennyi rugalmassággal rendelkezel ezzel a könyvtárral. Akár egy adott szöveget kell keresned egy nagy dokumentumban, akár kinyerned, akár a tulajdonságait kell elemezned, az Aspose.PDF gyerekjátékká teszi ezt. Ráadásul a bemutatott kóddal mindennel fel vagy készülve arra, hogy az igényeidhez igazítsd. 

## GYIK

### Több kifejezésre is kereshetek egyszerre?  
Igen, módosíthatod a kódot úgy, hogy több kifejezésre is keress, több létrehozásával `TextFragmentAbsorber` tárgyak.

### Hogyan tudok szöveget kinyerni egy adott oldalról?  
Egy adott oldalt megcélozhat a következő alkalmazásával: `TextFragmentAbsorber` egyetlen oldalra a teljes dokumentum helyett. Például: `pdfDocument.Pages[1].Accept(textFragmentAbsorber);`.

### Ingyenes az Aspose.PDF .NET-hez?  
Az Aspose.PDF egy kereskedelmi forgalomban kapható termék, de használható egy [ingyenes próba](https://releases.aspose.com/).

### Ki tudok nyerni képeket a PDF-ből az Aspose.PDF segítségével?  
Igen, az Aspose.PDF lehetővé teszi a szöveg mellett képek kinyerését is. Ellenőrizze a [dokumentáció](https://reference.aspose.com/pdf/net/) további részletekért.

### Mi van, ha további segítségre vagy támogatásra van szükségem?  
Mindig kérhetsz segítséget a [Aspose Támogatási Fórum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}