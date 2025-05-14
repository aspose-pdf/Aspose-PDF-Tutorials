---
"description": "Ismerje meg, hogyan exportálhat Excel-munkalapadatokat PDF-táblázatba az Aspose.PDF for .NET használatával. Lépésről lépésre bemutató kódpéldákkal, előfeltételekkel és hasznos tippekkel."
"linktitle": "Excel munkalap adatainak exportálása táblázatba"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Excel munkalap adatainak exportálása táblázatba"
"url": "/hu/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkalap adatainak exportálása táblázatba

## Bevezetés

Előfordult már, hogy Excel-munkalapból kellett adatokat exportálnia egy PDF-fájlba, táblázatos formátumban? Képzelje el, hogy egy csomó adata van az Excelben, de professzionális megjelenésű PDF-ként kell megosztania. Bonyolultan hangozhat, igaz? De az Aspose.PDF for .NET segítségével ezt a feladatot gyerekjátékká teheti. Ebben az oktatóanyagban végigvezetjük Önt az Excel-munkalap adatainak PDF-dokumentumon belüli táblázatba exportálásának folyamatán az Aspose.PDF for .NET használatával. Lépésről lépésre végigvezetjük Önt, mindent lebontva, így még ha újonc is ebben, a végére profinak fogja érezni magát.

## Előfeltételek

Mielőtt belevágnánk a kódolásba, állítsunk be néhány dolgot:

1. Aspose.PDF .NET könyvtárhoz – Győződjön meg róla, hogy a legújabb verzió telepítve van. [töltsd le itt](https://releases.aspose.com/pdf/net/).
2. Aspose.Cells for .NET Library – Erre szükséged lesz az Excel műveletek kezeléséhez. Töltsd le innen: [itt](https://releases.aspose.com/cells/net/).
3. .NET fejlesztői környezet – Egy olyan eszköz, mint a Visual Studio, tökéletesen működik kódoláshoz.
4. Excel fájl – Készítsen elő egy Excel fájlt az exportálni kívánt adatokkal.

Ha nincsenek meg az Aspose.PDF és Aspose.Cells könyvtárak, akkor kezdheti egy [ingyenes próba](https://releases.aspose.com/).

## Csomagok importálása

Először is győződj meg róla, hogy telepítetted mind az Aspose.PDF, mind az Aspose.Cells könyvtárakat a projektedbe. Telepítheted őket a Visual Studio NuGet csomagkezelőjével.

Így importálhatod a szükséges csomagokat a C# kódodba:

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

Most, hogy az előfeltételek megvannak, nézzük meg az adatok Excel-táblázatból PDF-dokumentumban lévő táblázatba exportálásának folyamatát.

## 1. lépés: Töltse be az Excel-munkafüzetet

Kezdéshez be kell töltened az Excel munkafüzetedet a programba. Ebben a lépésben az Aspose.Cells segítségével fogjuk megnyitni az Excel fájlt.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Töltse be az Excel munkafüzetet
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

Magyarázat: Itt megadjuk az Excel-fájlunk könyvtárútvonalát, és betöltjük a munkafüzetet a következővel: `Aspose.Cells.Workbook`. Ügyeljen arra, hogy beállítsa `"YOUR DOCUMENT DIRECTORY"` hogy a fájl helyére mutasson.

## 2. lépés: Az első munkalap elérése

A munkafüzet betöltése után el kell érnünk az első munkalapot, ahol az adatainkat tároljuk.

```csharp
// Az Excel fájl első munkalapjának elérése
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

Magyarázat: Ez a lépés egyszerű – a munkafüzetből kivesszük az első munkalapot, amely az exportálandó adatokat tartalmazza.

## 3. lépés: Adatok exportálása DataTable-be

Most exportáljuk az adatokat az Excel-táblázatból egy DataTable objektumba, amely közvetítőként fog működni az adatok PDF-be átvitelében.

```csharp
// 7 sor és 2 oszlop tartalmának exportálása az első cellától kezdve a DataTable táblába
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

Magyarázat: A `ExportDataTable` A metódus a munkalap első cellájától kezdve kinyeri az adatokat, és az összes sort és oszlopot átfogja. Ezeket az adatokat ezután egy `DataTable` további felhasználásra.

## 4. lépés: Új PDF dokumentum létrehozása

Ezután létre kell hoznunk egy új PDF dokumentumot az Aspose.PDF használatával.

```csharp
// Dokumentumpéldány létrehozása
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// Oldal létrehozása a dokumentumpéldányban
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

Magyarázat: Itt inicializálunk egy újat `Aspose.Pdf.Document` és adjunk hozzá egy oldalt. Ez az oldal fogja később tartalmazni azt a táblázatot, amelyet az Excel-adatokból hozunk létre.

## 5. lépés: Táblázatobjektum létrehozása PDF-ben

Térjünk át egy táblázat létrehozására a PDF dokumentumban.

```csharp
// Táblázat objektum létrehozása
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// Adja hozzá a Table objektumot az oldal bekezdésgyűjteményéhez
page.Paragraphs.Add(table);
```

Magyarázat: Létrehozunk egy `Aspose.Pdf.Table` objektumot, és hozzáadjuk az oldal bekezdésgyűjteményéhez, ami biztosítja, hogy a táblázat megjelenjen az oldalon.

## 6. lépés: Oszlopszélességek és szegélyek beállítása

A PDF-ben található táblázatoknak definiált oszlopszélességeket kell tartalmazniuk. Szegélyeket is hozzáadunk, hogy a táblázat olvashatóbb legyen.

```csharp
// A táblázat oszlopszélességének beállítása
table.ColumnWidths = "40 100 100";

// Alapértelmezett cellaszegély beállítása
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

Magyarázat: Beállítottuk a három oszlop szélességét, és minden cellának alapértelmezett szegélyt adtunk, amelynek vastagsága `0.1F`.

## 7. lépés: Adatok importálása a DataTable-ből PDF-táblázatba

Most itt az ideje, hogy importáljuk az adatokat a DataTable-ból a PDF táblázatunkba.

```csharp
// Adatok importálása a Table objektumba a DataTable-ból
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

Magyarázat: A `ImportDataTable` a metódus az összes adatot átviszi a `DataTable` a PDF táblázatba. Ez feltölti a táblázatot az Excel-táblázat adataival.

## 8. lépés: A fejlécsor stílusának megadása

Stílusosítsuk meg a táblázat fejléc sorát a háttérszín, a betűtípus és az igazítás megváltoztatásával.

```csharp
// Szerezd meg az első sort a táblázatból
Aspose.Pdf.Row headerRow = table.Rows[0];

// Fejlécsor stílusának beállítása
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

Magyarázat: Végigmegyünk az első sor (fejléc) összes celláján, és a háttérszínüket kékre, a szövegszínüket sárgára állítjuk, majd a szöveget középre igazítjuk.

## 9. lépés: A fennmaradó sorok formázása

A fejléc és a többi sor megkülönböztetéséhez adjunk hozzá eltérő stílust a fennmaradó sorokhoz.

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

Magyarázat: A fejléc kivételével minden sorhoz szürke hátteret és fehér szövegszínt állítottunk be.

## 10. lépés: Mentse el a PDF dokumentumot

Végül mentse el a táblázatot tartalmazó PDF dokumentumot.

```csharp
// Mentsd el a Pdf-et
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

Magyarázat: Elmentettük a PDF-et a megadott könyvtárba. Voilà! Az Excel-adataid most egy szépen formázott PDF-táblázatban vannak.

## Következtetés

És íme! Néhány lépésben exportáltál adatokat egy Excel-munkalapból egy PDF-ben található táblázatba az Aspose.PDF for .NET segítségével. A folyamat lebontásával és stílusának módosításával testreszabhatod a kimenetet, és biztosíthatod, hogy az adataid tiszták és professzionálisak legyenek. Így legközelebb, amikor valaki egy Excel-fájlt ad át neked, és PDF-jelentést kér, pontosan tudod, mit kell tenned.

## GYIK

### Lehet jobban testre szabni a táblázatot?
Természetesen! Módosíthatod a színeket, betűtípusokat, igazítást, sőt akár szegélyeket is hozzáadhatsz bizonyos cellákhoz.

### Ingyenes az Aspose.PDF .NET-hez?
Ingyenes próbaverziót kínál, de hosszabb használathoz licencre lesz szükséged. [vedd meg itt](https://purchase.aspose.com/buy).

### Exportálhatok csak bizonyos sorokat és oszlopokat?
Igen, módosíthatja a paramétereket a `ExportDataTable` metódus adott tartományok exportálására.

### Ez működik nagy Excel fájlokkal?
Igen, az Aspose.Cells úgy lett kialakítva, hogy hatékonyan kezelje a nagyméretű Excel fájlokat.

### Hogyan adhatok hozzá több oldalt a PDF-hez?
Használhatod `pdfDocument.Pages.Add()` annyi oldal hozzáadásához, amennyire szüksége van.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}