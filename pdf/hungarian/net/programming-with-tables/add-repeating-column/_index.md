---
"description": "Tanuld meg, hogyan adhatsz hozzá ismétlődő oszlopokat PDF dokumentumokhoz az Aspose.PDF for .NET segítségével. Lépésről lépésre útmutató példákkal és kóddal. Tökéletes fejlesztők számára."
"linktitle": "Ismétlődő oszlop hozzáadása PDF dokumentumban"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Ismétlődő oszlop hozzáadása PDF dokumentumban"
"url": "/hu/net/programming-with-tables/add-repeating-column/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ismétlődő oszlop hozzáadása PDF dokumentumban

## Bevezetés

Ha PDF dokumentumokkal dolgozol, és ismétlődő oszlopokat kell hozzáadnod, jó helyen jársz! Az Aspose.PDF for .NET segítségével könnyedén kezelheted a táblázatokat és a tartalmat egy PDF dokumentumban. Akár dinamikus jelentéseket, számlákat vagy bármilyen más strukturált dokumentumot készítesz, az ismétlődő oszlopok forradalmi változást hozhatnak az adatok rendszerezésében. Nézzük meg lépésről lépésre, hogyan adhatsz hozzá ismétlődő oszlopokat egy PDF dokumentumhoz.

## Előfeltételek

Mielőtt belevágnánk a kódba, győződjünk meg róla, hogy mindent beállítottunk:

- Aspose.PDF .NET-hez: Telepítenie kell az Aspose.PDF .NET-hez könyvtárat a projektjébe.
- [Aspose.PDF letöltése .NET-hez](https://releases.aspose.com/pdf/net/)
- [Ingyenes próbaverzió](https://releases.aspose.com/)
- Fejlesztői környezet: Győződjön meg róla, hogy telepítve van egy .NET-kompatibilis IDE, például a Visual Studio.
- C# alapismeretek: Bár mindent részletesen bemutatunk, a C# alapvető ismerete segít abban, hogy zökkenőmentesen kövesd a feladatot.
  
Ha még nincs meg az Aspose.PDF .NET-hez készült fájlod, letöltheted [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) hogy elkezdhesd felfedezni a funkcióit.

## Csomagok importálása

Kezdéshez importálnia kell a szükséges névtereket az Aspose.PDF for .NET fájlból. Így teheti meg:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Ezek a csomagok biztosítják a PDF dokumentumokkal való munkához és a táblázatok kezeléséhez szükséges alapvető osztályokat és metódusokat.

Most bontsuk le a folyamatot több lépésre, hogy ismétlődő oszlopokat adjunk hozzá egy PDF dokumentumhoz. Kövesd a példát!

## 1. lépés: Állítsa be a Dokumentumok könyvtár elérési útját

Mielőtt bármilyen fájlt létrehoznánk vagy módosítanánk, meg kell adnunk azt az elérési utat, ahová a létrehozott PDF mentésre kerül. A C# projektedben állítsd be a fájlok tárolási útvonalát:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "AddRepeatingColumn_out.pdf";
```

Ez az elérési út arra a könyvtárra mutat, ahová a kimeneti PDF mentésre kerül. Csere `"YOUR DOCUMENT DIRECTORY"` a gépeden lévő tényleges elérési úttal.

## 2. lépés: Új PDF dokumentum létrehozása

Kezdésként hozz létre egy új példányt `Document` objektum. Ez fog tárolóként szolgálni a PDF összes oldalának és tartalmának.

```csharp
Document doc = new Document();
Aspose.Pdf.Page page = doc.Pages.Add();
```

Itt létrehoztunk egy új PDF dokumentumot, és hozzáadtunk egy üres oldalt. `doc.Pages.Add()` A metódus új oldalt szúr be a dokumentumba.

## 3. lépés: A külső tábla példányosítása

Ezután létrehozunk egy külső táblázatot. Ez a táblázat az oldal teljes szélességét kitölti, és tárolóként szolgál más táblázatok számára, beleértve azt is, amelyik az ismétlődő oszlopokat fogja tartalmazni.

```csharp
Aspose.Pdf.Table outerTable = new Aspose.Pdf.Table();
outerTable.ColumnWidths = "100%";
outerTable.HorizontalAlignment = HorizontalAlignment.Left;
```

Beállítottuk a `ColumnWidths` tulajdonságot „100%-ra” állítja, ami azt jelenti, hogy a táblázat a teljes oldalszélességre kiterjed.

## 4. lépés: A belső táblázat létrehozása

Most hozzuk létre a belső táblázatot, amely ismétlődő oszlopokat fog tartalmazni. A legfontosabb tulajdonságok a következők: `Broken`, amely lehetővé teszi a táblázat folytatását ugyanazon az oldalon keresztül, és `ColumnAdjustment`, amely automatikusan a tartalomhoz igazítja az oszlopszélességet.

```csharp
Aspose.Pdf.Table mytable = new Aspose.Pdf.Table();
mytable.Broken = TableBroken.VerticalInSamePage;
mytable.ColumnAdjustment = ColumnAdjustment.AutoFitToContent;
```

Ez a belső tábla a külső táblába lesz beágyazva.

## 5. lépés: Táblázatok hozzáadása az oldalhoz

Most, hogy mind a külső, mind a belső táblázatok készen állnak, adjuk hozzá őket az oldalhoz. Ez a lépés biztosítja, hogy a táblázatok bekerüljenek a dokumentum struktúrájába.

```csharp
page.Paragraphs.Add(outerTable);
var bodyRow = outerTable.Rows.Add();
var bodyCell = bodyRow.Cells.Add();
bodyCell.Paragraphs.Add(mytable);
mytable.RepeatingColumnsCount = 5;
```

Itt hozzáadtuk a `outerTable` az oldalra, majd a külső táblázatba beágyaztuk a `mytable`Ezenkívül beállítottuk `RepeatingColumnsCount` 5-ig, megadva, hogy hány oszlop ismétlődjön az adatok hozzáadásakor.

## 6. lépés: Fejlécsor hozzáadása

Most itt az ideje, hogy hozzáadjuk a fejléceket a táblázathoz. A fejlécsor kontextust ad az adatoknak, és segít az oszlopok strukturálásában. 

```csharp
Aspose.Pdf.Row row = mytable.Rows.Add();
row.Cells.Add("header 1");
row.Cells.Add("header 2");
row.Cells.Add("header 3");
row.Cells.Add("header 4");
row.Cells.Add("header 5");
row.Cells.Add("header 6");
row.Cells.Add("header 7");
row.Cells.Add("header 11");
row.Cells.Add("header 12");
row.Cells.Add("header 13");
row.Cells.Add("header 14");
row.Cells.Add("header 15");
row.Cells.Add("header 16");
row.Cells.Add("header 17");
```

Ez a kódrészlet hozzáadja az első sort (amelyet fejlécként fogunk használni), és olyan szöveget tartalmazó cellákkal tölti fel, mint például a „fejléc 1”, „fejléc 2” stb.

## 7. lépés: Adatsorok hozzáadása

Végül hozzáadhatunk néhány adatot a táblázathoz. Ez a ciklus dinamikusan létrehozza a sorokat és kitölti a cellákat tartalommal:

```csharp
for (int RowCounter = 0; RowCounter <= 5; RowCounter++)
{
    Aspose.Pdf.Row row1 = mytable.Rows.Add();
    row1.Cells.Add("col " + RowCounter.ToString() + ", 1");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 2");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 3");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 4");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 5");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 6");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 7");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 11");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 12");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 13");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 14");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 15");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 16");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 17");
}
```

A ciklus hatszor ismétlődik, sorokat ad hozzá, és minden cellát a megfelelő oszlopadatokkal tölt fel (pl. „1. oszlop, 1”, „2. oszlop, 2” stb.).

## 8. lépés: A dokumentum mentése

Miután az összes sort és oszlopot hozzáadtuk, az utolsó lépés a dokumentum mentése a megadott fájlútvonalra.

```csharp
doc.Save(outFile);
```

A dokumentum most ismétlődő oszlopokkal lett mentve!

## Következtetés

Íme, itt van! Ezekkel az egyszerű lépésekkel ismétlődő oszlopokkal rendelkező PDF dokumentumot hozhatsz létre az Aspose.PDF for .NET segítségével. A beágyazott táblázatok rugalmasságát kihasználva összetett elrendezéseket érhetsz el, amelyek professzionális és rendezett megjelenést kölcsönöznek PDF-eidnek. Próbáld ki ezt a következő projektedhez, és fedezd fel az Aspose.PDF teljes potenciálját a PDF-generálási igényeid kielégítésére.

## GYIK

### Mi az Aspose.PDF .NET-hez?
Az Aspose.PDF for .NET egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára, hogy programozottan hozzanak létre, szerkeszthessenek és kezelhessenek PDF dokumentumokat.

### Dinamikusan beállíthatom az ismétlődő oszlopok számát?
Igen, az ismétlődő oszlopok számát módosíthatja a `RepeatingColumnsCount` ingatlan.

### Hogyan igényelhetek licencet az Aspose.PDF for .NET fájlhoz?
Fájlból vagy adatfolyamból is alkalmazhat licencet a következő utasítások végrehajtásával. [dokumentáció](https://reference.aspose.com/pdf/net/).

### Lehet képeket hozzáadni a táblázat celláihoz?
Igen, az Aspose.PDF for .NET támogatja különféle típusú tartalmak, beleértve a képeket is, táblázatcellákhoz való hozzáadását.

### Testreszabhatom a táblázat elrendezését tovább?
Abszolút! Az Aspose.PDF kiterjedt funkciókat kínál a táblázatstílusok testreszabásához, beleértve a szegélyeket, a kitöltést, az igazítást és egyebeket.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}