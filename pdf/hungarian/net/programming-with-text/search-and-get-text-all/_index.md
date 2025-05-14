---
"description": "Ismerje meg, hogyan kereshet és nyerhet ki szöveget egy PDF dokumentum összes oldaláról az Aspose.PDF for .NET használatával."
"linktitle": "Keresés és szöveges fogadás"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Keresés és szöveges fogadás"
"url": "/hu/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Keresés és szöveges fogadás

## Bevezetés

Előfordult már, hogy egy adott szöveget kellett kinyernie egy PDF-ből, de bonyolultnak találta? A PDF-ek néha zárolt tárolóknak tűnhetnek, ami megnehezíti a szükséges információk megszerzését. De van egy jó hír: az Aspose.PDF for .NET segítségével könnyedén kereshet és kinyerhet szöveget bármely PDF-ből. Ez a hatékony könyvtár mindent biztosít, amire szüksége van a PDF-ekkel való munkához a .NET-alkalmazásokban, így a szövegkinyerés gyerekjáték. Ebben az oktatóanyagban végigvezetjük a szöveg keresésének és kinyerésének folyamatán egy PDF-fájlból az Aspose.PDF for .NET segítségével. Akár szövegelemző eszközt épít, akár csak automatizálnia kell az adatok kinyerését PDF-jelentésekből, jó helyen jár!

## Előfeltételek

Mielőtt belevágnánk a kódba, győződjünk meg róla, hogy mindent beállítottunk:

1. Aspose.PDF .NET-hez: Le kell töltened és telepítened az Aspose.PDF .NET-hez fájlt. Letöltheted a letöltési oldalról. [itt](https://releases.aspose.com/pdf/net/).
2. .NET környezet: Győződjön meg arról, hogy a .NET keretrendszer vagy a .NET Core telepítve van a fejlesztőgépén.
3. Alapvető C## ismeretek: Ajánlott némi C#-ismeret és .NET projektekkel való munka.
4. PDF dokumentum: Egy minta PDF fájl, amelyből szöveget fogunk kinyerni. Ebben a példában a következőt fogjuk használni: `SearchAndGetTextFromAll.pdf`.

## Csomagok importálása

Mielőtt bármilyen kódot írnál, importálnod kell a szükséges névtereket a projektedbe az Aspose.PDF használatához.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Ezek a névterek hozzáférést biztosítanak a PDF dokumentumobjektum-modelljéhez, és lehetővé teszik számunkra a fájlon belüli szöveg manipulálását.

Bontsuk le a folyamatot egyszerű lépésekre, hogy könnyedén követhesd.

## 1. lépés: Állítsa be a dokumentumkönyvtárat

Először is meg kell adnia annak a könyvtárnak az elérési útját, ahol a PDF található. Ez segít az alkalmazásnak megtalálni azt a fájlt, amelyből a szöveget ki szeretné nyerni.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- A `dataDir` változónak arra a könyvtárra kell mutatnia, ahol a `SearchAndGetTextFromAll.pdf` fájl tárolva van.
- Csere `"YOUR DOCUMENT DIRECTORY"` a gépeden lévő tényleges elérési úttal.

## 2. lépés: Nyissa meg a PDF dokumentumot

Ezután az Aspose.PDF segítségével nyitjuk meg a PDF dokumentumot. `Document` objektum.

```csharp
// Dokumentum megnyitása
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- Létrehozunk egy új példányt a `Document` osztályt a PDF teljes fájlútvonalának átadásával.
- Ez betölti a PDF-et a memóriába, így az készen áll a feldolgozásra.

## 3. lépés: Hozz létre egy szövegelnyelőt

A `TextFragmentAbsorber` Az objektum egy adott szöveg PDF-ben való keresésére szolgál. Ebben az esetben a „szöveg” szót fogjuk keresni.

```csharp
// Hozz létre TextAbsorber objektumot a megadott keresési kifejezés összes előfordulásának megkereséséhez
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- A `TextFragmentAbsorber` karakterlánccal inicializálódik `"text"`Ez azt jelenti, hogy a „szöveg” szó minden előfordulását keresi a PDF dokumentumban.

## 4. lépés: Fogadd el az összes oldal abszorberét

Most arra utasítjuk a PDF dokumentumot, hogy fogadja el az abszorbert, és keresse meg a szöveget az összes oldalán.

```csharp
// Fogadd el az összes oldal abszorberét
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- A `Accept` metódus a dokumentum oldalaira kerül alkalmazásra. Ez az összes oldalon át fogja keresni a megadott szöveget.

## 5. lépés: Szövegrészletek kinyerése

Miután az abszorber beolvasta a dokumentumot, visszakereshetjük a kinyert szövegrészeket.

```csharp
// A kivont szövegrészek beszerzése
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- A `TextFragments` a tulajdona `TextFragmentAbsorber` visszaadja a keresési kifejezésnek megfelelő összes szövegrészlet gyűjteményét.

## 6. lépés: Szövegrészletek ismétlése

Most, hogy megvan a szövegrészek gyűjteménye, végigmegyünk rajtuk, és kinyerjük a részleteket.

```csharp
// Ugorj végig a töredékeken
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- A `foreach` ciklus végigmegy mindegyiken `TextFragment` a gyűjteményben.
- Minden egyes töredék különböző tulajdonságait kinyomtatjuk, például a tényleges szöveget, annak pozícióját az oldalon, a betűtípus részleteit és a betűméretet.
- A `XIndent` és `YIndent` A tulajdonságok megadják a szövegrészlet pontos koordinátáit a PDF-en belül.

## Következtetés

És íme! Néhány sornyi kóddal sikeresen kerestünk és kinyertünk szöveget egy PDF-ből az Aspose.PDF for .NET segítségével. Az Aspose.PDF rugalmassága lehetővé teszi a PDF-ek számos módon történő manipulálását, így kiváló választás azoknak a fejlesztőknek, akiknek robusztus PDF-megoldásokra van szükségük .NET környezetben. Ezt a példát könnyedén kiterjesztheted más szavak keresésére, további részletek kinyerésére, vagy akár a PDF tartalmának manipulálására az igényeid szerint. Remélhetőleg ez az útmutató világos és egyszerű megközelítést adott a PDF-ekkel való munkához. Próbáld ki a saját PDF-jeiddel!

## GYIK

### Több szóra is kereshetek egyszerre?  
Igen, módosíthatja a `TextFragmentAbsorber` több kifejezés kereséséhez a keresési karakterlánc megfelelő módosításával.

### Mi van, ha a szöveg több soron átível?  
Az Aspose.PDF akkor is felismeri és kinyeri a szöveget, ha az több soron átível. Ezeket a töredékeket egyenként is kezelheti.

### Hogyan menthetem el a kivágott szöveget egy fájlba?  
kinyert szöveget szabványos C# fájl I/O műveletekkel írhatja fájlba, például `StreamWriter`.

### Az Aspose.PDF támogatja a szöveg kinyerését a beolvasott PDF-ekből?  
Az Aspose.PDF nem támogatja az OCR-t. Szkennelt PDF-ek esetén OCR eszközre van szükség a szöveg felismeréséhez.

### Hogyan kezelhetem a titkosított PDF fájlokat?  
Ha a PDF fájl jelszóval védett, az Aspose.PDF segítségével feloldhatja a zárolást a jelszó megadásával a dokumentum betöltésekor.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}