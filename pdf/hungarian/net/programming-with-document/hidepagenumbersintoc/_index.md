---
"description": "Tanuld meg, hogyan rejtheted el az oldalszámokat a tartalomjegyzékben az Aspose.PDF for .NET segítségével. Kövesd ezt a részletes útmutatót kódpéldákkal professzionális PDF-ek létrehozásához."
"linktitle": "Oldalszámok elrejtése a tartalomjegyzékben"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Oldalszámok elrejtése a tartalomjegyzékben"
"url": "/hu/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Oldalszámok elrejtése a tartalomjegyzékben

## Bevezetés

Amikor PDF-ekkel dolgozol, előfordulhat, hogy szeretnél tartalomjegyzéket (TOC) létrehozni, de az oldalszámok elrejtésével megőrizni az esztétikai megjelenést. Lehet, hogy a dokumentum jobban néz ki nélkülük, vagy talán esztétikai okokból. Bármi is legyen az okod, ha az Aspose.PDF for .NET fájllal dolgozol, ez az oktatóanyag pontosan megmutatja, hogyan rejtheted el az oldalszámokat a tartalomjegyzékben.

## Előfeltételek

Mielőtt belekezdenénk, van néhány dolog, amire szükséged lesz. Íme egy gyors ellenőrzőlista:

- Visual Studio telepítve: A kódoláshoz a Visual Studio egy működő verziójára lesz szükséged.
- Aspose.PDF .NET könyvtárhoz: Győződjön meg róla, hogy telepítette az Aspose.PDF .NET könyvtárat.
  - Letöltési link: [Aspose.PDF .NET-hez](https://releases.aspose.com/pdf/net/)
- Ideiglenes licenc: Ha teszteli a funkciókat, hasznos, ha ideiglenes licenccel rendelkezik.
  - Ideiglenes jogosítvány: [Szerezd meg itt](https://purchase.aspose.com/temporary-license/)

## Csomagok importálása

Mielőtt belevágnál a kódba, mindenképpen importáld a következő névtereket a C# projektedbe. Ezek biztosítják a szükséges osztályokat és metódusokat a PDF dokumentumokkal való munkához és a tartalomjegyzék (TOC) létrehozásához.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Most, hogy a környezeted elkészült és a csomagok importálása megtörtént, bontsuk le a folyamat egyes lépéseit. A kód minden részét áttekintjük az érthetőség kedvéért, hogy könnyen követhesd a folyamatot.

## 1. lépés: PDF dokumentum inicializálása

Az első dolog, amit tennünk kell, egy új PDF dokumentum létrehozása és egy oldal hozzáadása a tartalomjegyzékhez (TOC).


```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir: Ez a könyvtár, ahová a kimeneti fájl mentésre kerül.
- Document(): Inicializál egy új PDF dokumentumot.
- Pages.Add(): Egy új üres oldalt ad hozzá a dokumentumhoz, amely később a tartalomjegyzéket fogja tartalmazni.

## 2. lépés: Tartalomjegyzék-információk és cím beállítása

Ezután meghatározzuk a tartalomjegyzék adatait, beleértve a tartalomjegyzék tetején megjelenő cím beállítását is.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo: Ez az objektum a tartalomjegyzékkel kapcsolatos összes információt tartalmazza.
- TextFragment: A tartalomjegyzék címének szövegét jelöli, itt „Tartalomjegyzékként” van beállítva.
- Betűstílus: A tartalomjegyzék címét úgy formázzuk meg, hogy a méretét 20-ra állítjuk, és félkövér betűtípust használunk.
- tocPage.TocInfo: A tartalomjegyzék adatait hozzárendeljük ahhoz az oldalhoz, amelyik megjeleníti a tartalomjegyzéket.

## 3. lépés: Oldalszámok elrejtése a tartalomjegyzékben

Most pedig jöjjön a mókás rész! Itt konfiguráljuk a tartalomjegyzéket az oldalszámok elrejtéséhez.

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers: Ez a varázslatos kapcsoló, amely elrejti az oldalszámokat. Állítsa erre: `false`és az oldalszámok nem jelennek meg a tartalomjegyzékben.
- FormatArrayLength: Ezt 4-re állítottuk be, ami azt jelzi, hogy a tartalomjegyzék címsorainak négy szintjéhez szeretnénk formázást definiálni.

## 4. lépés: A tartalomjegyzék formázásának testreszabása

A tartalomjegyzék stílusosabbá tételéhez most definiáljuk a különböző szintű címsorok formázását.

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray: Ez a tömb a tartalomjegyzék-bejegyzések formázását szabályozza. Minden index egy másik címsorszintet jelöl.
- Margó és szövegstílus: Minden címsorszinthez margókat állítunk be, és betűstílusokat alkalmazunk, például félkövér, dőlt és aláhúzott.

## 5. lépés: Címsorok hozzáadása a dokumentumhoz

Végül adjuk hozzá a tartalomjegyzék részét képező tényleges címsorokat.

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- Címsor és szövegszegmens: Ezek jelölik a tartalomjegyzékben megjelenő címsorokat. Minden szintnek saját címsora van.
- IsAutoSequence: Automatikusan számozza a címsorokat.
- IsInList: Biztosítja, hogy minden címsor megjelenjen a tartalomjegyzékben.

## 6. lépés: A dokumentum mentése

Miután mindent beállítottál, mentsd el a PDF dokumentumot a megadott kimeneti fájlba.

```csharp
doc.Save(outFile);
```

És kész is! Sikeresen létrehoztál egy tartalomjegyzékkel ellátott PDF-et, és az oldalszámok rejtve vannak!

## Következtetés

Tartalomjegyzék létrehozása PDF-ben és oldalszámok elrejtése bonyolultnak tűnhet, de az Aspose.PDF for .NET segítségével ez gyerekjáték. Ezzel a lépésről lépésre haladó útmutatóval megtanultad, hogyan szabhatod testre a tartalomjegyzék formátumát, hogyan rejtheted el az oldalszámokat, és hogyan alkalmazhatsz különböző stílusokat a címsorokra. Mostantól professzionális, az igényeidre szabott PDF-eket hozhatsz létre.

## GYIK

### Megjeleníthetem az oldalszámokat bizonyos címsorokhoz a tartalomjegyzékben?
Nem, az Aspose.PDF elrejti vagy megjeleníti az oldalszámokat a teljes tartalomjegyzékben. Nem rejtheted el őket szelektíven bizonyos bejegyzéseknél.

### Lehetséges további szinteket hozzáadni a tartalomjegyzékhez?
Igen, növelheted a `FormatArrayLength` a tartalomjegyzék címsorainak több szintjének meghatározásához.

### Hogyan tudom megváltoztatni a tartalomjegyzék összes bejegyzésének betűtípusát?
A betűtípust a következő módosításával módosíthatja: `TextState.Font` tulajdonság minden szinthez a `FormatArray`.

### Beszúrhatok hiperhivatkozásokat a tartalomjegyzékbe?
Igen, minden tartalomjegyzék-bejegyzést a dokumentum egy adott szakaszához csatolhat a `Heading.TocPage` ingatlan.

### Szükségem van licencre az Aspose.PDF fájlhoz?
Igen, érvényes engedély szükséges a termelési célú felhasználáshoz. Ideiglenes engedélyt is igényelhet. [itt](https://purchase.aspose.com/temporary-license/) a funkciók teszteléséhez.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}