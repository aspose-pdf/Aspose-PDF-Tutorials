---
"description": "Tanuld meg, hogyan szabhatod testre a PDF-ekben található vonalvezetési mintákat az Aspose.PDF for .NET segítségével lépésről lépésre szóló útmutatónkkal. Tökéletes a dokumentumok stílusának bővítéséhez."
"linktitle": "Vonószál hossza"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Vonószál hossza"
"url": "/hu/net/programming-with-graphs/dash-length/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vonószál hossza

## Bevezetés

Szeretnéd egy csipetnyi kreativitást adni PDF dokumentumaidnak a vonalak testreszabásával, különféle szaggatott mintákkal? Az Aspose.PDF for .NET segítségével könnyedén módosíthatod a vonalstílusokat a dokumentum igényeinek megfelelően. Ebben az oktatóanyagban azt vizsgáljuk meg, hogyan állíthatod be a vonalak szaggatott hosszát egy PDF dokumentumban az Aspose.PDF for .NET segítségével. Akár szaggatott vonalat, akár pontozott mintát szeretnél létrehozni, ez az útmutató biztosítja a kívánt eredmény eléréséhez szükséges eszközöket és lépéseket.

## Előfeltételek

Mielőtt belevágnál az oktatóanyagba, van néhány dolog, amire szükséged lesz:

1. Aspose.PDF .NET-hez: Győződjön meg róla, hogy telepítve van az Aspose.PDF .NET-hez fájl. Ha még nem telepítette, letöltheti innen: [Aspose.PDF .NET-hez](https://releases.aspose.com/pdf/net/).
2. C# alapismeretek: Ez az oktatóanyag feltételezi, hogy rendelkezel C# programozási alapismeretekkel. Ha még csak most ismerkedsz a C#-kal, érdemes lehet először felfrissíteni az alapokat.
3. Visual Studio: Bár bármilyen IDE-t használhatsz, ez az útmutató feltételezi, hogy a Visual Studio-t használod a C# kód írásához és futtatásához.
4. Aspose fiók: További forrásokért és támogatásért győződjön meg arról, hogy rendelkezik Aspose fiókkal. Regisztrálhat egy [ingyenes próba](https://releases.aspose.com/) vagy vásároljon licencet [itt](https://purchase.aspose.com/buy).

## Csomagok importálása

Az Aspose.PDF for .NET használatának megkezdéséhez importálnia kell a vonatkozó névtereket. Így teheti meg:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Ezek a névterek tartalmazzák a PDF dokumentumokkal, rajzokkal és vonalakkal való munkához szükséges osztályokat és metódusokat.

## 1. lépés: A projekt beállítása

Mielőtt elkezdenéd a kódolást, hozz létre egy új C# projektet a Visual Studioban. Add hozzá az Aspose.PDF for .NET könyvtárat a projektedhez a NuGet segítségével, vagy a DLL manuális hivatkozásával. 

## 2. lépés: A dokumentum inicializálása

Kezdésként hozz létre egy új PDF dokumentumot, és adj hozzá egy oldalt. Ez lesz a vászon, amelyre a vonalakat fogod rajzolni.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Dokumentumpéldány példányosítása
Document doc = new Document();

// Oldal hozzáadása a Dokumentum objektum oldalgyűjteményéhez
Page page = doc.Pages.Add();
```

Itt létrehozunk egy `Document` objektumot, és adj hozzá egy újat `Page` hozzá. Ez megalapozza a vonal meghúzását.

## 3. lépés: A rajzobjektum létrehozása

Ezután hozzon létre egy `Graph` egy objektum, amely a rajzolni kívánt területet jelöli. Adja meg a méreteit az igényeinek megfelelően.

```csharp
// Rajzobjektum létrehozása meghatározott méretekkel
Aspose.Pdf.Drawing.Graph canvas = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);

// Rajzobjektum hozzáadása az oldalpéldány bekezdésgyűjteményéhez
page.Paragraphs.Add(canvas);
```

A `Graph` Az objektum a rajzelemek tárolójaként szolgál. Itt a szélessége 100 egység, a magassága pedig 400 egység.

## 4. lépés: A vonal meghatározása

Most itt az ideje létrehozni a `Line` objektum. Adja meg a vonal kezdő- és végpontját, és szabja testre a stílusát.

```csharp
// Vonal objektum létrehozása
Aspose.Pdf.Drawing.Line line = new Aspose.Pdf.Drawing.Line(new float[] { 100, 100, 200, 100 });
```

Ez a vonal a (100, 100) koordinátáknál kezdődik és a (200, 100) koordinátáknál végződik. Ezeket a koordinátákat az igényeidnek megfelelően módosíthatod.

## 5. lépés: A vonalstílus testreszabása

Állítsd be a vonal színét és szaggatott mintázatát. Itt tudod kiemelni a vonaladat.

```csharp
// Vonal objektum színének beállítása
line.GraphInfo.Color = Aspose.Pdf.Color.Red;

// Vonalobjektumhoz tartozó szaggatott tömb megadása
line.GraphInfo.DashArray = new int[] { 0, 1, 0 };

// Állítsa be a kötőjel fázisát a vonalpéldányhoz
line.GraphInfo.DashPhase = 1;
```

- `line.GraphInfo.Color`: Beállítja a vonal színét. Ebben az esetben piros.
- `line.GraphInfo.DashArray`: Meghatározza a kötőjel mintázatát. Itt, `{ 0, 1, 0 }` szaggatott mintázatot jelöl.
- `line.GraphInfo.DashPhase`: Beállítja a szaggatott minta kezdőpontját.

## 6. lépés: Vonal hozzáadása a rajzhoz

Miután megformáztad a vonaladat, add hozzá a `Graph` objektum.

```csharp
// Vonal hozzáadása a rajzobjektum alakzatgyűjteményéhez
canvas.Shapes.Add(line);
```

Ez integrálja a vonalat a rajzvászonba.

## 7. lépés: A dokumentum mentése

Végül mentse el a dokumentumot a megadott elérési útra. Itt jön létre a PDF fájl.

```csharp
dataDir = dataDir + "DashLength_out.pdf";

// PDF dokumentum mentése
doc.Save(dataDir);
Console.WriteLine("\nLength dashed successfully in black and white.\nFile saved at " + dataDir);
```

Ez a kódsor menti a PDF dokumentumot, és egy megerősítő üzenetben jelzi, hogy hová lett mentve a fájl.

## Következtetés

PDF dokumentumokban található vonalstílusok testreszabása professzionális megjelenést kölcsönözhet jelentéseinek, prezentációinak és egyéb dokumentumainak. Ezzel az oktatóanyaggal megtanulta, hogyan állíthatja be a vonalak szaggatott vonalának hosszát az Aspose.PDF for .NET segítségével. Akár egyszerű szaggatott vonalakat, akár összetettebb mintákat hoz létre, az Aspose.PDF biztosítja a szükséges rugalmasságot, hogy dokumentumai kiemelkedjenek. Kísérletezzen különböző szaggatott mintákkal és színekkel, hogy megtalálja az igényeinek leginkább megfelelő stílust.

## GYIK

### Hogyan telepíthetem az Aspose.PDF for .NET fájlt?
Telepítheted a NuGet segítségével a Visual Studio-ban, vagy letöltheted innen: [Aspose weboldala](https://releases.aspose.com/pdf/net/).

### Ingyenesen használhatom az Aspose.PDF for .NET fájlt?
Igen, az Aspose kínál egy [ingyenes próba](https://releases.aspose.com/) így a licenc megvásárlása előtt kipróbálhatja a funkcióit.

### Milyen egyéb testreszabási lehetőségeket tudok alkalmazni egy PDF sorain?
Beállíthatja a vonal vastagságát, színét és a szaggatott mintákat. Lásd a [dokumentáció](https://reference.aspose.com/pdf/net/) további részletekért.

### Hogyan kaphatok támogatást, ha problémákba ütközöm?
A támogatást a következőn keresztül veheti igénybe: [Aspose Fórum](https://forum.aspose.com/c/pdf/10).

### Hol vásárolhatok licencet az Aspose.PDF for .NET fájlhoz?
Licenc vásárlása lehetséges [itt](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}