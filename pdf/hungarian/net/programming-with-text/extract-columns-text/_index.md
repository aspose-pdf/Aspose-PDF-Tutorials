---
"description": "Tanuld meg, hogyan kinyerhetsz szövegoszlopokat PDF fájlokból az Aspose.PDF for .NET segítségével. Ez az útmutató kódpéldákkal és magyarázatokkal részletezi az egyes lépéseket."
"linktitle": "Oszlopok szövegének kinyerése PDF fájlból"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Oszlopok szövegének kinyerése PDF fájlból"
"url": "/hu/net/programming-with-text/extract-columns-text/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Oszlopok szövegének kinyerése PDF fájlból

## Bevezetés

PDF fájlokkal dolgozik, és egy adott oszlopformátumú szöveget kell kinyernie? Akár számlákat, jelentéseket vagy bármilyen strukturált dokumentumot dolgoz fel, a szöveg pontos kinyerése egy PDF-ből bonyolult feladat lehet. Itt lép a képbe az Aspose.PDF for .NET, hogy leegyszerűsítse a folyamatot. Ebben az oktatóanyagban végigvezetjük Önt azon, hogyan kinyerhet könnyedén szövegoszlopokat egy PDF fájlból. 

## Előfeltételek

Mielőtt belemerülnénk a kódba, nézzük meg a legfontosabb dolgokat, amikre szükséged lesz:

- Aspose.PDF .NET-hez: Győződjön meg róla, hogy telepítve van az Aspose.PDF .NET-hez legújabb verziója. Ha nem, akkor... [töltsd le itt](https://releases.aspose.com/pdf/net/).
- Fejlesztői környezet: A kóddal való munkához Visual Studio vagy más .NET fejlesztői környezet szükséges.
- PDF dokumentum: Legyen kéznél egy minta PDF dokumentum, lehetőleg egy szövegoszlopokkal rendelkező, mivel abból fogunk szöveget kinyerni.

Ha még nem telepítetted az Aspose.PDF for .NET fájlt, letölthetsz egyet [ingyenes próba](https://releases.aspose.com/) vagy [vásároljon egy licencet](https://purchase.aspose.com/buy) a teljes funkciókért. Igényelhet egyet is [ideiglenes engedély](https://purchase.aspose.com/temporary-license) ha szükséges.

## Névterek importálása

Az Aspose.PDF for .NET használatához a projektedben a következő névtereket kell importálnod:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## Lépésről lépésre útmutató: Szövegoszlopok kinyerése PDF-ből

Most pedig bontsuk le a kód egyes részeit, hogy jobban megértsük, hogyan működik. Kövessük a lépést, ahogy elmagyarázzuk a folyamat minden egyes szegmensét.

## 1. lépés: Töltse be a PDF dokumentumot

Első dolgod, hogy betöltöd a PDF fájlt a `Document` objektum. Így működik együtt az Aspose.PDF a dokumentummal.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "ExtractTextPage.pdf");
```

Ebben a lépésben egyszerűen csak azt a könyvtárat definiáljuk, ahol a PDF dokumentum tárolva van. Csere `"YOUR DOCUMENT DIRECTORY"` a helyi PDF-fájl elérési útjával. `Document` objektum betölti a PDF-et a memóriába, így az elérhetővé válik a további feldolgozáshoz.

## 2. lépés: Állítsa be a szövegtöredék-elnyelőt

Ezután egy `TextFragmentAbsorber` a PDF fájl összes szövegének elnyelésére vagy rögzítésére. Ez az elnyelő osztály szövegrészek kinyerésére szolgál a PDF adott területeiről, így ideális szövegoszlopok kinyerésére.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
pdfDocument.Pages.Accept(tfa);
TextFragmentCollection tfc = tfa.TextFragments;
```

Itt létrehozunk egy példányt a következőből: `TextFragmentAbsorber` és alkalmazza a PDF összes oldalára a következővel: `Accept()`. A `TextFragmentCollection` tárolja a kinyert szöveget, és ebből a gyűjteményből szükség szerint manipulálhatjuk vagy kinyerhetjük a szöveget.

## 3. lépés: Állítsa be a kivont szöveg betűméretét

Miután rögzítetted a szövegrészeket, érdemes lehet csökkenteni a betűméretüket, különösen akkor, ha az eredeti szöveg túl nagy. Ebben a példában 70%-kal csökkentjük a betűméretet.

```csharp
foreach (TextFragment tf in tfc)
{
    // Betűméret csökkentése 70%-kal
    tf.TextState.FontSize = tf.TextState.FontSize * 0.7f;
}
```

Ez a kód végigmegy mindegyiken `TextFragment` a gyűjteményben, és 70%-kal csökkenti a betűméretét. A betűméret módosítása megkönnyítheti a kinyert szöveg kezelését, különösen akkor, ha más célokra formázza.

## 4. lépés: Dokumentum mentése memóriafolyamba

A szöveg módosítása után elmentjük a PDF-et egy `MemoryStream`Ez lehetővé teszi számunkra, hogy a dokumentumot a memóriában tartsuk további feldolgozás céljából anélkül, hogy vissza kellene írnunk a lemezre.

```csharp
Stream st = new MemoryStream();
pdfDocument.Save(st);
pdfDocument = new Document(st);
```

Itt a PDF-et egy memóriafolyamba mentjük, majd újratöltjük a dokumentumot. Ez a módszer akkor hasznos, ha nagy fájlokkal dolgozik, és el szeretné kerülni a felesleges lemezműveleteket.

## 5. lépés: Az összes szöveg kinyerése a Text Absorber segítségével

Most, hogy elkészítettük a PDF-et, itt az ideje, hogy kivonjuk a szöveget. A következőt fogjuk használni: `TextAbsorber` hogy kiolvassa az összes szöveget a dokumentumból.

```csharp
TextAbsorber textAbsorber = new TextAbsorber();
pdfDocument.Pages.Accept(textAbsorber);
String extractedText = textAbsorber.Text;
```

Ebben a lépésben a `TextAbsorber` beolvasztja az összes szöveget a PDF-ből, és a kinyert szöveget a `extractedText` karakterlánc. Itt történik a varázslat – a szövegoszlopok mostantól egyszerű szöveg formátumban vannak!

## 6. lépés: Mentse el a kibontott szöveget egy fájlba

Végül a kivont szöveget elmentjük egy `.txt` fájl a könnyű hozzáférés és a további felhasználás érdekében.

```csharp
dataDir = dataDir + "ExtractColumnsText_out.txt";
System.IO.File.WriteAllText(dataDir, extractedText);
Console.WriteLine("\nColumns text extracted successfully from Pages of PDF Document.\nFile saved at " + dataDir);
```

Ez a kód a kibontott szöveget egy új fájlba írja. `.txt` fájlt, és elmenti azt a megadott könyvtárba. Egy üzenet jelenik meg a konzolon, amely megerősíti a folyamat sikerességét.

## Következtetés

Íme! Az Aspose.PDF for .NET segítségével PDF fájlokból szövegoszlopok kinyerése egyszerűbb, mint gondolnád. Mindössze néhány sornyi kóddal betölthetsz egy PDF fájlt, kinyerhetsz bizonyos szöveget, beállíthatod a formázást, és az eredményeket egy szövegfájlba mentheted.

Ez a technika hihetetlenül hasznos strukturált dokumentumok, például táblázatok, jelentések vagy oszlopokba rendezett tartalmak feldolgozásához. Akár automatizálni kell az adatkinyerést, akár tömeges dokumentumokat kell feldolgozni, az Aspose.PDF biztosítja az eszközöket a hatékony megvalósításhoz.

## GYIK

### Ki tudok nyerni szöveget egy PDF egyes oldalairól?  
Igen! Módosíthatja a `TextFragmentAbsorber` adott oldalak megcélzásához a `pdfDocument.Pages[pageIndex].Accept(tfa);` módszer.

### Lehetséges szöveget kinyerni csak egy oszlopból egy több oszlopos PDF-ben?  
Igen, de a szövegrészek koordinátáival kell dolgoznia a következő használatával: `TextFragment.Rectangle` a dokumentum meghatározott területeinek megcélzására.

### Hogyan javíthatom a szövegkiemelés pontosságát?  
A nagyobb pontosság érdekében győződjön meg arról, hogy a PDF szerkezete jól definiált, és kerülje a bonyolult elrendezésű dokumentumokat. A `TextFragmentAbsorber` szöveg kinyerése betűstílusok, méretek vagy régiók alapján.

### Az Aspose.PDF támogatja a szöveg kinyerését a szkennelt dokumentumokból?  
Igen, de OCR (optikai karakterfelismerő) technológiát kell használnod. Az Aspose ehhez is biztosít eszközöket.

### Hogyan kezeljek több ezer oldalas, nagyméretű PDF fájlokat?  
Nagy PDF-ek esetén a dokumentumot darabokban dolgozza fel, egyszerre csak néhány oldalról nyerve ki a szöveget, így elkerülhető a magas memóriahasználat.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}