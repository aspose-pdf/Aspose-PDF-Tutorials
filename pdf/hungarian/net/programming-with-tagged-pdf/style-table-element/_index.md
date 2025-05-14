---
"description": "Tanuld meg, hogyan hozhatsz létre és formázhatsz táblázatelemeket az Aspose.PDF for .NET fájlban lépésről lépésre bemutatott utasításokkal, egyéni formázással és PDF/UA-megfelelőséggel."
"linktitle": "Stílustábla elem"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Stílustábla elem"
"url": "/hu/net/programming-with-tagged-pdf/style-table-element/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Stílustábla elem

## Bevezetés

Ebben a cikkben részletesebben is bemutatjuk, hogyan hozhatsz létre és formázhatsz táblázatelemeket az Aspose.PDF for .NET segítségével. Megtanulod, hogyan strukturálhatsz táblázatokat, hogyan alkalmazhatsz egyéni stílusokat, és hogyan ellenőrizheted a dokumentumod PDF/UA megfelelőségét. A bemutató végére könnyedén készíthetsz professzionális megjelenésű táblázatokat a PDF-fájljaidban!

## Előfeltételek

Mielőtt belevágnál az oktatóanyagba, győződj meg arról, hogy a következőkkel rendelkezel:

1. Visual Studio vagy hasonló IDE telepítve a gépedre.
2. .NET-keretrendszer vagy .NET Core SDK az alkalmazás futtatásához.
3. A projektedben letöltött és hivatkozott Aspose.PDF .NET könyvtár. A legújabb verziót innen szerezheted be: [itt](https://releases.aspose.com/pdf/net/).
4. Érvényes Aspose licenc vagy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) hogy a könyvtár teljes funkcionalitását kiaknázhassa.

## Csomagok importálása

Kezdésként importáld a szükséges névtereket a projektedbe:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ezek a névterek lefedik az alapvető PDF-műveleteket, a címkézett tartalmat, a táblázatokat és a szövegformázást.

Most bontsuk le egy táblázat létrehozásának és formázásának folyamatát az Aspose.PDF fájlban. Részletesen áttekintjük az egyes szakaszokat, hogy könnyebben követhesd a folyamatot.

## 1. lépés: Új PDF dokumentum létrehozása és címkézett tartalom beállítása

Ebben az első lépésben létrehozunk egy üres PDF dokumentumot, és beállítjuk a címkézett tartalmát.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Új PDF dokumentum létrehozása
Document document = new Document();

// Címkézett tartalom beállítása
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table style");
taggedContent.SetLanguage("en-US");
```

Egy új létrehozásával kezdjük `Document` objektum, amely a PDF-ünket képviseli. `TaggedContent` Az objektum a dokumentum szerkezetének kezelésére szolgál, biztosítva az akadálymentesítési szabványoknak való megfelelést. A megfelelő címkézés érdekében beállítjuk a dokumentum címét és nyelvét.

## 2. lépés: A gyökérelem meghatározása

Ezután létrehozzuk a gyökérstruktúra elemet, amely a PDF-ben található összes tartalom tárolójaként szolgál.

```csharp
// Szerezd meg a gyökérstruktúra elemet
StructureElement rootElement = taggedContent.RootElement;
```

A `RootElement` az összes strukturált elem, beleértve a táblázatunkat is, alaptárolójaként szolgál. Segít fenntartani a dokumentum szerkezeti hierarchiáját, ami fontos mind a rendszerezés, mind az akadálymentesítés szempontjából.

## 3. lépés: A táblázat elem létrehozása és formázása

Most, hogy a gyökérelem be van állítva, létrehozunk egy `TableElement` és alkalmazzon olyan stílusokat, mint a háttérszín, a szegélyek és az igazítás.

```csharp
// Táblázatszerkezeti elem létrehozása
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);

// Az asztal stílusa
tableElement.BackgroundColor = Color.Beige;
tableElement.Border = new BorderInfo(BorderSide.All, 0.80F, Color.Gray);
tableElement.Alignment = HorizontalAlignment.Center;
tableElement.Broken = TableBroken.Vertical;
tableElement.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```

Létrehozunk egy `TableElement`, amely meghatározza a táblázatunk szerkezetét. `BackgroundColor`, `Border`, és `Alignment` A tulajdonságok lehetővé teszik a táblázat megjelenésének testreszabását. `Broken` A tulajdonság biztosítja, hogy ha a táblázat oldalakon átívelően törik meg, akkor függőlegesen is törik meg.

## 4. lépés: Táblázatméretek és cellastílusok beállítása

Ebben a lépésben definiáljuk az oszlopok számát, a cellaközöket és a táblázat egyéb fontos tulajdonságait.

```csharp
tableElement.ColumnWidths = "80 80 80 80 80";
tableElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.DarkBlue);
tableElement.DefaultCellPadding = new MarginInfo(16.0, 2.0, 8.0, 2.0);
tableElement.DefaultCellTextState.ForegroundColor = Color.DarkCyan;
tableElement.DefaultCellTextState.FontSize = 8F;
```

Az oszlopszélességeket úgy adjuk meg, hogy a táblázat minden oszlopa egyenletesen legyen elosztva. `DefaultCellBorder`, `DefaultCellPadding`, és `DefaultCellTextState` határozza meg a cellák alapértelmezett stílusait, beleértve a szegélyeket, a kitöltést, a szöveg színét és a betűméretet.

## 5. lépés: Ismétlődő sorok és egyéni stílusok hozzáadása

Stílusokat is definiálhatunk ismétlődő sorokhoz és más specifikus táblázatelemekhez, például fejlécekhez és láblécekhez.

```csharp
tableElement.RepeatingRowsCount = 3;
TextState rowStyle = new TextState();
rowStyle.BackgroundColor = Color.LightCoral;
tableElement.RepeatingRowsStyle = rowStyle;
```

A `RepeatingRowsCount` biztosítja, hogy az első három sor ismétlődjön, ha a táblázat több oldalra terjed ki. Beállítjuk a `RepeatingRowsStyle` egyéni háttérszínt alkalmazni ezekre a sorokra.

## 6. lépés: Asztalfej, test és láb elemek hozzáadása

Most hozzuk létre a táblázat fejlécét, törzsét és láblécét, és töltsük fel őket tartalommal.

```csharp
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();

// Fejlécsor létrehozása
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 5; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
}

// Tábla törzsének feltöltése
for (int rowIndex = 0; rowIndex < 10; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    for (int colIndex = 0; colIndex < 5; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
    }
}
```

A táblázat három részre oszlik: fejre, törzsre és lábra. Először a fejlécsort hozzuk létre a következővel: `TableTHElement` és oszlopfejléceket adunk hozzá. Ezután a táblázat törzsét a következővel töltjük fel: `TableTDElement`, minden cellát egy címkével tölt meg, amely tartalmazza a pozícióját.

## 7. lépés: A dokumentum mentése

Végül a PDF dokumentumot a megadott könyvtárba mentjük.

```csharp
// Mentse el a címkézett PDF dokumentumot
document.Save(dataDir + "StyleTableElement.pdf");
```

Ez a lépés a PDF-fájl és a formázott táblázat mentésével véglegesíti a dokumentum létrehozási folyamatát.

## 8. lépés: PDF/UA megfelelőség ellenőrzése

A dokumentum mentése után elengedhetetlen annak biztosítása, hogy megfeleljen a PDF/UA (Univerzális Akadálymentesítés) szabványoknak.

```csharp
// PDF/UA megfelelőség ellenőrzése
document = new Document(dataDir + "StyleTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableElement.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Itt újratöltjük a dokumentumot, és ellenőrizzük a PDF/UA szabványok szerint. A megfelelőség biztosítja, hogy a PDF megfeleljen az akadálymentesítési követelményeknek, így széles felhasználói kör számára alkalmassá válik.

## Következtetés

Az Aspose.PDF for .NET segítségével a PDF dokumentumokban található táblázatok létrehozása és formázása egyszerű és intuitív. Az ebben az oktatóanyagban ismertetett lépéseket követve testreszabott stílusokkal hozhat létre táblázatokat, és biztosíthatja, hogy PDF-jei megfeleljenek az akadálymentesítési szabványoknak. Akár jelentéseket készít, akár strukturált dokumentumokat hoz létre, a táblázatok hatékony eszközök az adatok világos bemutatásához.

## GYIK

### Beilleszthetek képeket a táblázat celláiba?
Igen, beszúrhat képeket a táblázat celláiba a `Image` elem.

### Hogyan tudom dinamikusan beállítani az oszlopszélességet?
Beállíthatja a `ColumnAdjustment` ingatlan `AutoFitToWindow` az oszlopszélességek automatikus beállításához a tartalom alapján.

### Kötelező a PDF/UA megfelelőség minden dokumentum esetében?
Bár nem kötelező, ajánlott olyan dokumentumok esetében, amelyek magas szintű akadálymentesítést igényelnek.

### Alkalmazhatok különböző stílusokat adott sorokra?
Igen, testreszabhatja az egyes sorokat vagy cellákat a hozzájuk tartozó beállítások módosításával. `TextState` vagy `BackgroundColor`.

### Mi az előnye a címkézett tartalom használatának?
A címkézett tartalom javítja a dokumentumok hozzáférhetőségét, és segít biztosítani a szabványoknak, például a PDF/UA-nak való megfelelést.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}