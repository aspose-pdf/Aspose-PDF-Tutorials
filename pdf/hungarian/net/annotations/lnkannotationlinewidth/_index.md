---
"description": "Ismerje meg, hogyan állíthatja be a tintajelölések vonalvastagságát PDF-ben az Aspose.PDF for .NET használatával. Ez a részletes oktatóanyag végigvezeti Önt minden lépésen, biztosítva a kiváló minőségű kimenetet."
"linktitle": "lnk Annotáció vonalvastagsága"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "lnk Annotáció vonalvastagsága"
"url": "/hu/net/annotations/lnkannotationlinewidth/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# lnk Annotáció vonalvastagsága

## Bevezetés

PDF dokumentumokkal való munka során a megjegyzések hozzáadása hatékony módja lehet az információk kiemelésének vagy interaktív elemek hozzáadásának a fájlokhoz. Az egyik ilyen megjegyzés a tintahasználatos megjegyzés, amely lehetővé teszi szabadkézi vonalak rajzolását a PDF-en. De mi van akkor, ha testre kell szabnia ezeknek a vonalaknak a megjelenését, különösen a vonalvastagságot? Ebben az oktatóanyagban végigvezetjük a tintahasználatos megjegyzések vonalvastagságának beállításán az Aspose.PDF for .NET használatával.

## Előfeltételek

Mielőtt belemerülnénk a kódba, győződjünk meg róla, hogy mindent beállítottunk a bemutató zökkenőmentes követéséhez:

1. Aspose.PDF .NET-hez: Győződjön meg róla, hogy telepítve van az Aspose.PDF .NET-hez könyvtár. Letöltheti innen: [letöltési oldal](https://releases.aspose.com/pdf/net/) vagy telepítse a NuGet csomagkezelőn keresztül a Visual Studio-ban.
2. Fejlesztői környezet: Ez az oktatóanyag feltételezi, hogy egy .NET fejlesztői környezetben, például a Visual Studio-ban dolgozol.
3. C# alapismeretek: A C# alapvető ismerete segít a kódolási lépések követésében.
4. PDF dokumentum: Használjon egy meglévő PDF dokumentumot, vagy hozzon létre egy újat ehhez az oktatóanyaghoz.

## Szükséges névterek importálása

Mielőtt elkezdenéd a kódolást, győződj meg róla, hogy importáltad a szükséges névtereket a projektedbe:

```csharp
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;
using System.Collections;
using System.Collections.Generic;
```

Ezek a névterek biztosítják a PDF dokumentumok kezeléséhez, a jegyzetekkel való munkához és a grafikus elemek kezeléséhez szükséges osztályokat és metódusokat.

Most, hogy megvannak az előfeltételeink, bontsuk le a tintajelöléses vonalszélesség beállításának folyamatát világos, kezelhető lépésekre.

## 1. lépés: A PDF dokumentum inicializálása

Először létre kell hoznunk vagy meg kell nyitnunk egy PDF dokumentumot. Ebben az oktatóanyagban egy új PDF dokumentumot fogunk létrehozni a nulláról.

```csharp
// PDF dokumentum inicializálása
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Adja meg a dokumentum könyvtárát
Document doc = new Document();
doc.Pages.Add(); // Üres oldal hozzáadása a dokumentumhoz
```

Itt inicializálunk egy újat `Document` objektum, amely a PDF fájlunkat képviseli. Ezután hozzáadunk egy üres oldalt ehhez a dokumentumhoz, hogy azzal dolgozhassunk.

## 2. lépés: A tintajelölés létrehozása

Ezután létrehozzuk magát a tintajelölést. Ez magában foglalja a tintavonásokat alkotó pontok meghatározását.

```csharp
// Hozd létre a tintajelölést
IList<Point[]> inkList = new List<Point[]>();
LineInfo lineInfo = new LineInfo();
lineInfo.VerticeCoordinate = new float[] { 55, 55, 70, 70, 70, 90, 150, 60 };
lineInfo.Visibility = true;
lineInfo.LineColor = Color.Red;
lineInfo.LineWidth = 2;
```

Ebben a lépésben definiáljuk a `LineInfo` objektum, amely a tintavonások koordinátáit, láthatóságát, színét és kezdeti vonalvastagságát tartalmazza. `VerticeCoordinate` A tömb tartalmazza a körvonal egyes pontjainak X és Y koordinátáit.

## 3. lépés: Koordináták pontokká konvertálása

Most ezeket a koordinátákat pontokká kell konvertálnunk, amelyeket a tintarajzolás használhat.

```csharp
// Koordináták pontokká konvertálása
int length = lineInfo.VerticeCoordinate.Length / 2;
Aspose.Pdf.Point[] gesture = new Aspose.Pdf.Point[length];
for (int i = 0; i < length; i++)
{
    gesture[i] = new Aspose.Pdf.Point(lineInfo.VerticeCoordinate[2 * i], lineInfo.VerticeCoordinate[2 * i + 1]);
}

inkList.Add(gesture);
```

Ez a ciklus feldolgozza a koordináta-tömböt, és minden koordinátapárt egy `Point` objektum, amelyet aztán hozzáadunk a miénkhez `inkList`.

## 4. lépés: Tintajelölés hozzáadása a PDF oldalhoz

Miután a pontok készen állnak, létrehozhatjuk a tintajelölést, és hozzáadhatjuk a PDF oldalhoz.

```csharp
// Tintajegyzet hozzáadása a PDF oldalhoz
InkAnnotation a1 = new InkAnnotation(doc.Pages[1], new Aspose.Pdf.Rectangle(100, 100, 300, 300), inkList);
a1.Subject = "Test";
a1.Title = "Title";
a1.Color = Aspose.Pdf.Color.FromRgb(Color.Green);
```

Ebben a lépésben inicializálunk egy `InkAnnotation` objektumot, megadva az oldalt, egy határoló téglalapot és a pontok listáját. Beállítjuk a megjegyzés tárgyát, címét és színét is.

## 5. lépés: A jegyzet szegélyének testreszabása

A megjegyzés megjelenésének további testreszabásához módosítjuk a szegély tulajdonságait.

```csharp
// A jegyzet szegélyének testreszabása
Border border = new Border(a1);
border.Width = 3;
border.Effect = BorderEffect.Cloudy;
border.Dash = new Dash(1, 1);
border.Style = BorderStyle.Solid;
doc.Pages[1].Annotations.Add(a1);
```

Itt létrehozunk egy `Border` objektumot a jegyzetünkhöz, beállítva annak szélességét, hatását, vonásmintáját és stílusát. Ez a lépés biztosítja, hogy a jegyzet vizuálisan kiemelkedjen a PDF oldalon.

## 6. lépés: Mentse el a PDF dokumentumot

Végül, miután elvégeztük az összes szükséges módosítást, itt az ideje menteni a dokumentumot.

```csharp
// PDF dokumentum mentése
dataDir = dataDir + "lnkAnnotationLineWidth_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nInk annotation line width setup successfully.\nFile saved at " + dataDir);
```

Ez a kód a módosított PDF dokumentumot a megadott könyvtárba menti a tintajelöléssel együtt. `Console.WriteLine` utasítás megerősíti a kód sikeres végrehajtását.

## Következtetés

Gratulálunk! Sikeresen létrehoztál és testreszabtál egy tintahasználattal készült jegyzetet egy PDF dokumentumban az Aspose.PDF for .NET segítségével. Ez az oktatóanyag a teljes folyamatot lefedte, a dokumentum inicializálásától a végső fájl mentéséig. Ezzel a tudással tovább felfedezheted az Aspose.PDF for .NET hatalmas képességeit, és hasonló technikákat alkalmazhatsz más típusú jegyzetekre vagy PDF-manipulációkra.

## GYIK

### Használhatok különböző színeket a tintajelölés különböző részeihez?  
Igen, többet is létrehozhatsz `InkAnnotation` különböző színű objektumokat, és azokat a PDF ugyanazon vagy különböző oldalaira helyezheti.

### Hogyan tudom dinamikusan megváltoztatni a vonalvastagságot?  
Beállíthatja a `LineWidth` a tulajdona `LineInfo` objektumot a koordináták pontokká konvertálása előtt.

### Átlátszóvá tehető a tintajelölés?  
Igen, módosíthatja a `Opacity` a tulajdona `InkAnnotation` objektumot, hogy átlátszóvá tegye.

### Hozzáadhatok több szabadkézi jegyzetet ugyanahhoz az oldalhoz?  
Természetesen! A folyamat megismétlésével annyi szabadkézi jegyzetet adhatsz egyetlen oldalhoz, amennyit csak szeretnél.

### Hogyan távolíthatok el egy tintajelölést egy PDF-ből?  
Eltávolíthat egy megjegyzést a következővel: `doc.Pages[1].Annotations.Delete(a1)` módszer, ahol `a1` a te annotációs objektumod.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}