---
"description": "Tanuld meg, hogyan hozhatsz létre kitöltött téglalapot PDF-ben az Aspose.PDF for .NET használatával ezzel a lépésről lépésre szóló útmutatóval. Tökéletes minden szintű fejlesztő számára."
"linktitle": "Kitöltött téglalap létrehozása"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Kitöltött téglalap létrehozása"
"url": "/hu/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kitöltött téglalap létrehozása

## Bevezetés

Szerettél volna már vizuálisan vonzó PDF-eket programozottan létrehozni? Ha igen, akkor jó helyen jársz! Ebben az oktatóanyagban elmerülünk az Aspose.PDF for .NET világában, amely egy hatékony könyvtár, amely lehetővé teszi a PDF-dokumentumok egyszerű kezelését. Ma egy kitöltött téglalap létrehozására fogunk összpontosítani egy PDF-fájlon belül. Akár tapasztalt fejlesztő vagy, akár csak most kezded, ez az útmutató barátságos és lebilincselő módon végigvezet minden lépésen. Szóval, ragadd meg a programozó sapkádat, és kezdjük is el!

## Előfeltételek

Mielőtt belevágnánk a kódba, van néhány dolog, aminek a helyén kell lennie:

1. Visual Studio: Győződj meg róla, hogy a Visual Studio telepítve van a gépeden. Ez egy fantasztikus IDE .NET fejlesztéshez.
2. Aspose.PDF .NET-hez: Le kell töltened és telepítened az Aspose.PDF könyvtárat. Megtalálod itt: [itt](https://releases.aspose.com/pdf/net/).
3. C# alapismeretek: Egy kis C# programozási ismeret segít jobban megérteni a kódrészleteket.

## Csomagok importálása

A kezdéshez importálnod kell a szükséges csomagokat a C# projektedbe. Így teheted meg:

### Új projekt létrehozása

Nyisd meg a Visual Studiot, és hozz létre egy új C# projektet. Az egyszerűség kedvéért választhatsz egy konzolalkalmazást.

### Aspose.PDF referencia hozzáadása

1. Kattintson jobb gombbal a projektjére a Megoldáskezelőben.
2. Válassza a „NuGet-csomagok kezelése” lehetőséget.
3. Keresd meg az „Aspose.PDF” fájlt, és telepítsd a legújabb verziót.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Most, hogy mindent beállítottunk, vágjunk bele a kódba!

## 1. lépés: Dokumentumkönyvtár beállítása

Először is meg kell adnia a PDF mentési útvonalát. Ez azért kulcsfontosságú, mert ez mondja meg a programnak, hogy hol hozza létre a fájlt.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Csere `"YOUR DOCUMENT DIRECTORY"` a gépeden található tényleges elérési úttal, ahová a PDF-et menteni szeretnéd.

## 2. lépés: Dokumentumpéldány létrehozása

Következőként létrehozunk egy példányt a következőből: `Document` osztály. Ez az osztály azt a PDF dokumentumot jelöli, amellyel dolgozni fog.

```csharp
// Dokumentumpéldány létrehozása
Document doc = new Document();
```

Ez a sor inicializál egy új PDF dokumentumot, amelyet aztán manipulálhatunk.

## 3. lépés: Oldal hozzáadása a dokumentumhoz

Most adjunk hozzá egy oldalt a dokumentumunkhoz. Minden PDF-nek kell legalább egy oldal, ugye?

```csharp
// Oldal hozzáadása PDF fájl oldalak gyűjteményéhez
Page page = doc.Pages.Add();
```

Ez a kód egy új oldalt ad hozzá a dokumentumhoz, amelyre alakzatokat rajzolhatunk.

## 4. lépés: Grafikonpéldány létrehozása

Alakzatok rajzolásához létre kell hoznunk egy `Graph` például. Gondolj egy gráfra úgy, mint egy vászonra, amelyre különféle alakzatokat rajzolhatsz.

```csharp
// Graph-példány létrehozása
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

Itt egy 100 szélességű és 400 magasságú gráfot hozunk létre.

## 5. lépés: Grafikon hozzáadása az oldalhoz

Most, hogy megvan a grafikonunk, adjuk hozzá a korábban létrehozott oldalhoz.

```csharp
// Grafikus objektum hozzáadása az oldalpéldány bekezdésgyűjteményéhez
page.Paragraphs.Add(graph);
```

Ez a vonal rögzíti a grafikont az oldalhoz, így az készen áll a rajzolásra.

## 6. lépés: Téglalap alakú példány létrehozása

Ezután létrehozunk egy téglalapot, amelyet színnel szeretnénk kitölteni.

```csharp
// Téglalap példány létrehozása
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

Ebben a kódban a téglalap pozícióját és méretét definiáljuk. A paraméterek az x és y koordinátákat, a szélességet és a magasságot jelölik.

## 7. lépés: Adja meg a kitöltési színt

Most válasszunk egy színt a téglalapunknak. Ebben a példában pirossal fogjuk kitölteni.

```csharp
// Adja meg a Graph objektum kitöltési színét
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

Ez a vonal a téglalap kitöltési színét pirosra állítja. Bármelyik színt választhatod!

## 8. lépés: Téglalap hozzáadása a grafikonhoz

Miután elkészült a téglalapunk, itt az ideje, hogy hozzáadjuk a grafikonhoz.

```csharp
// Téglalap objektum hozzáadása a Graph objektum alakzatgyűjteményéhez
graph.Shapes.Add(rect);
```

Ez a kód hozzáadja a téglalapot a grafikonhoz, így az a rajzunk részévé válik.

## 9. lépés: Mentse el a PDF dokumentumot

Végül el kell mentenünk a dokumentumunkat a megadott könyvtárba.

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// PDF fájl mentése
doc.Save(dataDir);
```

Ez a kód a következő néven menti el a PDF fájlt: `CreateFilledRectangle_out.pdf` a korábban megadott könyvtárban.

## 10. lépés: Megerősítő üzenet

Hogy tudassuk velünk, hogy minden simán ment, kinyomtathatunk egy visszaigazoló üzenetet.

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

Ez a sor egy üzenetet jelenít meg a konzolon, amely megerősíti, hogy a kitöltött téglalap sikeresen létrejött.

## Következtetés

És íme! Sikeresen létrehoztál egy kitöltött téglalapot egy PDF dokumentumban az Aspose.PDF for .NET segítségével. Ez a hatékony könyvtár a PDF-manipuláció lehetőségeinek tárházát nyitja meg, lehetővé téve lenyűgöző dokumentumok programozott létrehozását. Akár jelentéseket, számlákat vagy bármilyen más típusú PDF-et generálsz, az Aspose.PDF segít neked.

## GYIK

### Mi az Aspose.PDF .NET-hez?
Az Aspose.PDF for .NET egy olyan könyvtár, amely lehetővé teszi a fejlesztők számára, hogy programozottan hozzanak létre, szerkesszenek és konvertáljanak PDF dokumentumokat.

### Ingyenesen használhatom az Aspose.PDF fájlt?
Igen, az Aspose ingyenes próbaverziót kínál, amellyel felfedezheted a könyvtár funkcióit. Letöltheted. [itt](https://releases.aspose.com/).

### Van mód támogatást kérni az Aspose.PDF-hez?
Természetesen! Az Aspose fórumon keresztül kaphatsz támogatást. [itt](https://forum.aspose.com/c/pdf/10).

### Hogyan vásárolhatom meg az Aspose.PDF fájlt?
Az Aspose.PDF fájlt a vásárlási oldalon vásárolhatja meg. [itt](https://purchase.aspose.com/buy).

### Milyen típusú alakzatokat hozhatok létre az Aspose.PDF fájllal?
Az Aspose.PDF könyvtár segítségével különféle alakzatokat hozhat létre, beleértve a téglalapokat, köröket, vonalakat és egyebeket.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}