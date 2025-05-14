---
"description": "Tanuld meg, hogyan formázhatod a táblázat sorait PDF-ben az Aspose.PDF for .NET segítségével egy lépésről lépésre bemutató útmutató segítségével, amely segít a dokumentumok formázásának egyszerű javításában."
"linktitle": "Stílustábla sor"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Stílustábla sor"
"url": "/hu/net/programming-with-tagged-pdf/style-table-row/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Stílustábla sor

## Bevezetés

Ha jól strukturált és szépen formázott PDF dokumentumok létrehozásáról van szó, az Aspose.PDF for .NET a tökéletes megoldás. Akár jelentéseket, számlákat automatizál, akár dinamikus táblázatokat hoz létre, a táblázatok különböző stílusokkal való formázása kulcsfontosságú a kifinomult dokumentumhoz. Ebben az oktatóanyagban mélyrehatóan elmerülünk egy táblázatsor formázásában az Aspose.PDF for .NET használatával. És ne aggódjon, lépésről lépésre végigvezetem Önt, akárcsak egy jó beszélgetést egy kávé mellett!

## Előfeltételek

Mielőtt belevágnánk a lényegbe, győződjünk meg róla, hogy minden kacsa egy sorban van. Szükséged lesz:

1. Aspose.PDF .NET könyvtárhoz  
   Ha még nincs meg, akkor innen szerezheted be [itt](https://releases.aspose.com/pdf/net/). Kaphatsz egy [ingyenes próba](https://releases.aspose.com/) hogy elkezdhessük.
2. Fejlesztői környezet  
   Állítsd be a Visual Studio-t vagy bármilyen általad választott C# IDE-t. Szükséged lesz a .NET telepítésére is, de gondolom, azzal már ismered.
3. C# és .NET alapismeretek  
   C# alapos ismerete gyerekjátékká teszi ezt az oktatóanyagot. De ne aggódj, minden lépést részletesen elmagyarázok!

## Csomagok importálása

Mielőtt elkezdhetnénk dolgozni az Aspose.PDF fájllal, importálnunk kell a szükséges névtereket. A C# projektedben győződj meg róla, hogy a következőket is belefoglaltad:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ezek elengedhetetlenek a táblázat létrehozásához és formázásához, és természetesen a címkézett tartalommal való munkához a megfelelőség érdekében.

Most bontsuk le lépésről lépésre a feladatot, hogy profi módon formázhasd a táblázat sorait!

## 1. lépés: Új PDF dokumentum létrehozása

Először is: hozzunk létre egy vadonatúj PDF dokumentumot. Ez a dokumentum fogja tartalmazni az összes formázott táblázatsort.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Dokumentum létrehozása
Document document = new Document();
```

Itt egyszerűen csak egy újat inicializálunk `Document` objektum, amely a PDF fájlunkat fogja reprezentálni. Ügyeljen arra, hogy beállítsa a könyvtár elérési útját, ahová a kimeneti fájlokat menteni fogja.

## 2. lépés: Címkézett tartalommal való munka

PDF akadálymentesítéséhez címkézett tartalommal fogunk dolgozni. Ez segít strukturált elemek, például táblázatok létrehozásában, biztosítva, hogy azok megfeleljenek az akadálymentesítési szabványoknak, például a PDF/UA-nak.

```csharp
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table row style");
taggedContent.SetLanguage("en-US");
```

Itt a PDF címkézett tartalmának címét és nyelvét állítjuk be. Olyan ez, mintha nevet adnál a PDF-nek, és megmondanád neki, hogy milyen nyelven beszéljen!

## 3. lépés: A tábla szerkezetének meghatározása

Következő lépésként definiáljuk a létrehozni kívánt táblázat szerkezetét. Minden táblázatnak szüksége van fejlécre, törzsre és láblécre – hasonlóan egy jól szervezett blogbejegyzéshez!

```csharp
// Gyökérszerkezeti elem lekérése
StructureElement rootElement = taggedContent.RootElement;

// Táblázatszerkezeti elem létrehozása
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

Amit itt csinálunk, az egy táblázat létrehozása fejléccel (`THead`), test (`TBody`), és lábléc (`TFoot`). Ezek az elemek fogják tartalmazni a sorainkat.

## 4. lépés: Táblázat fejléc sorának hozzáadása

A fejléc nélküli táblázatok olyanok, mint a cím nélküli könyvek. Először hozzuk létre a fejlécsort, hogy kontextust biztosítsunk az adatoknak.

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText(String.Format("Head {0}", colIndex));
}
```

Itt végigmegyünk a cikluson, és hozzáadunk három fejléccellát (`TableTHElement`), mindegyikhez egy leíró szöveget adva. Egyszerű, ugye?

## 5. lépés: Stílusos törzssorok hozzáadása

Most jön a mókás rész – a sorok stílusának beállítása! Hozzunk létre hét sort egyéni stílusokkal. Beállítjuk a háttérszíneket, a szegélyeket, a kitöltést és a szöveg igazítását.

```csharp
for (int rowIndex = 0; rowIndex < 7; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = String.Format("Row {0}", rowIndex);
    trElement.BackgroundColor = Color.LightGoldenrodYellow;
    trElement.Border = new BorderInfo(BorderSide.All, 0.75F, Color.DarkGray);
    trElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.Blue);
    trElement.MinRowHeight = 100.0;
    trElement.FixedRowHeight = 120.0;
    trElement.IsInNewPage = (rowIndex % 3 == 1);
    trElement.IsRowBroken = true;

    for (int colIndex = 0; colIndex < 3; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText(String.Format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}
```

- Háttérszín: Világos aranyvesszősárgát használtunk a professzionális, mégis meleg hatás érdekében.
- Szegélyek: Minden sor sötétszürke külső szegélyt és kék cellaszegélyeket kap az éles megjelenés érdekében.
- Magasság és kitöltés: A sorok magassága be van állítva, és a kitöltés hozzáadva van a letisztult megjelenés érdekében.
- Oldaltörések: A táblázat olvashatóságának javítása érdekében minden második sor új oldalon kezdődik.

## 6. lépés: Láblécsor hozzáadása

A fejléchez hasonlóan a lábléc is rögzíti a táblázatot. Hozzunk létre egyet.

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText(String.Format("Foot {0}", colIndex));
}
```

Egyszerűen végigmegyünk három lábléccellán, és hozzáadunk egy kis szöveget. A lábléc alternatív szövege a „Lábsor”, hogy akadálymentes legyen.

## 7. lépés: Mentse el a PDF dokumentumot

Most, hogy az asztal készen áll, itt az ideje megmenteni a remekművet!

```csharp
document.Save(dataDir + "StyleTableRow.pdf");
```

Így a PDF-fájl mentésre kerül az összes gyönyörű táblázatsorral, amelyeket az imént formáztunk meg.

## 8. lépés: PDF/UA megfelelőség ellenőrzése

Annak érdekében, hogy PDF-fájlunk megfeleljen az akadálymentesítési szabványoknak, ellenőrizzük a PDF/UA megfelelőségét.

```csharp
document = new Document(dataDir + "StyleTableRow.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableRow.xml", PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

Ez biztosítja, hogy a PDF-ed megfeleljen a PDF/UA szabványnak, így mindenki számára hozzáférhetővé válik. Az akadálymentesítés a lényeg!

## Következtetés

És íme! Néhány sornyi kóddal létrehoztál egy teljesen formázott táblázatot egy PDF-ben az Aspose.PDF for .NET segítségével. A fejlécektől a láblécekig minden sort formáztunk, akadálymentesítési elemeket adtunk hozzá, sőt, még a dokumentum megfelelőségét is ellenőriztük. Akár vállalati jelentéseken, prezentációkon dolgozol, vagy csak szórakozol PDF-ekkel, ez az útmutató mindent segít. Most pedig vágj bele, és kezdd el profi módon formázni a táblázataidat!

## GYIK

### A táblázat betűstílusát is meg lehet változtatni?  
Igen! A betűtípust a következővel módosíthatja: `TextState` objektum minden cellához, ami teljes testreszabást tesz lehetővé.

### Hogyan adhatok hozzá több oszlopot a táblázatomhoz?  
Csak igazítsd be a `colCount` változót, és adjon hozzá további cellákat a ciklusokban a fejlécekhez, a törzshöz és a láblécekhez.

### Mi történik, ha nem állítom be a sor magasságát?  
Ha nem állítja be a sormagasságot, a táblázat automatikusan igazodik a tartalomhoz.

### Használhatom ezt dinamikus sorszámhoz?  
Természetesen! Adatbázisból vagy bármilyen más forrásból lekérhet adatokat, és dinamikusan módosíthatja a sorok és oszlopok számát.

### Ingyenesen használható az Aspose.PDF for .NET?  
Az Aspose.PDF for .NET egy licencelt termék, de kipróbálható egy [ingyenes próba](https://releases.aspose.com/) vagy szerezz egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}