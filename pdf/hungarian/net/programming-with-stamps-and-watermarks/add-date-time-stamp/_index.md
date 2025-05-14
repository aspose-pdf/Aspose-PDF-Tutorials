---
"description": "Tanuld meg, hogyan adhatsz dátum- és időbélyeget PDF-fájljaidhoz az Aspose.PDF for .NET segítségével ezzel a lépésről lépésre szóló útmutatóval. Tökéletes a dokumentumok hitelességének fokozásához."
"linktitle": "Dátum-időbélyeg hozzáadása PDF fájlhoz"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Dátum-időbélyeg hozzáadása PDF fájlhoz"
"url": "/hu/net/programming-with-stamps-and-watermarks/add-date-time-stamp/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dátum-időbélyeg hozzáadása PDF fájlhoz

## Bevezetés

dokumentumok, különösen a PDF-ek kezelése terén a dátum- és időbélyeg hozzáadása gyökeresen megváltoztathatja a játékszabályokat. Akár jogi dokumentumokon, projektjelentéseken vagy számlákon dolgozik, az időbélyeg nemcsak hitelességet biztosít, hanem egyértelmű nyilvántartást is biztosít arról, hogy mikor készült vagy módosították a dokumentumot. Ebben az útmutatóban végigvezetjük Önt a dátum- és időbélyeg PDF-fájlhoz való hozzáadásának folyamatán az Aspose.PDF .NET-hez készült könyvtár használatával. 

Ez a cikk könnyen érthető és érthető, így még ha újonc vagy a programozásban vagy az Aspose.PDF könyvtárban, magabiztosan be tudod majd vezetni ezt a funkciót. Vágjunk bele!

## Előfeltételek

Mielőtt belekezdenénk, van néhány előfeltétel, aminek teljesülnie kell:

1. Visual Studio: Győződjön meg róla, hogy a Visual Studio telepítve van a gépén. Itt fogja megírni és végrehajtani a kódot.
2. Aspose.PDF .NET-hez: Le kell töltened és telepítened az Aspose.PDF könyvtárat. A legújabb verziót itt találod: [itt](https://releases.aspose.com/pdf/net/).
3. C# alapismeretek: A C# programozással való ismeret segít jobban megérteni a példákat, de ne aggódj, ha most kezded; mindent lépésről lépésre elmagyarázunk.
4. PDF-fájl: Készítsen elő egy minta PDF-fájlt. Példánkban egy nevű fájlt fogunk használni. `AddTextStamp.pdf`.

Miután megvannak ezek az előfeltételek, elkezdheti hozzáadni a dátum- és időbélyegeket a PDF-fájljaihoz!

## Csomagok importálása

Kezdéshez importálnod kell a szükséges névtereket a C# projektedbe. Így teheted meg:

### Új projekt létrehozása

1. Nyissa meg a Visual Studio-t: Indítsa el a Visual Studio alkalmazást.
2. Új projekt létrehozása: Válassza az „Új projekt létrehozása” lehetőséget a kezdőképernyőn.
3. Konzolalkalmazás kiválasztása: Válassza a „Konzolalkalmazás (.NET-keretrendszer)” lehetőséget a projektsablonok listájából.
4. Nevezd el a projekted: Adj nevet a projektednek, például `PDFDateTimeStamp`.

### Aspose.PDF referencia hozzáadása

1. Jobb klikk a Referenciákon: A Megoldáskezelőben kattints jobb klikkel a projekted „Referenciák” mappájára.
2. „Hivatkozás hozzáadása” kiválasztása: Válassza a „Hivatkozás hozzáadása” lehetőséget a helyi menüből.
3. Böngésszen az Aspose.PDF fájl megkeresése: Navigáljon arra a helyre, ahová letöltötte az Aspose.PDF fájlt, és jelölje ki. Kattintson az „OK” gombra a projekthez való hozzáadáshoz.

### Szükséges névterek importálása

A te tetején `Program.cs` fájlban a következő névtereket kell importálnia:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Annotations;
```

Most, hogy mindent előkészítettünk, bontsuk le világos és könnyen kezelhető lépésekre a dátum- és időbélyeg PDF-fájlhoz való hozzáadásának folyamatát.

## 1. lépés: Állítsa be a dokumentumkönyvtárat

Először is meg kell adnia azt a könyvtárat, ahol a PDF-fájl található. Ez azért fontos, mert a kód ebben a könyvtárban fogja keresni a PDF-et.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Cserélje le a tényleges elérési útra
```

Mindenképpen cserélje ki `YOUR DOCUMENT DIRECTORY` a PDF-fájl tényleges elérési útjával.

## 2. lépés: Nyissa meg a PDF dokumentumot

Ezután nyissa meg a PDF dokumentumot, amelyhez hozzá szeretné adni az időbélyeget. 

```csharp
// Dokumentum megnyitása
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

Ez a kódsor inicializálja a `Document` osztály és betölti a PDF fájlt a `pdfDocument` objektum.

## 3. lépés: Dátum-időbélyeg létrehozása

Most itt az ideje a dátum- és időbélyegző létrehozásának. Formázni fogod, hogy egy adott módon jelenjen meg. 

```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

Itt, `DateTime.Now` lekéri az aktuális dátumot és időt, és `ToString` formázza a kívánt formátumra.

## 4. lépés: Szövegbélyegző létrehozása

Miután a dátum és idő karakterlánca elkészült, létrehozhat egy szövegbélyegzőt, amelyet hozzáad a PDF-hez.

```csharp
// Szövegbélyeg létrehozása
TextStamp textStamp = new TextStamp(annotationText);
```

Ez a sor egy új példányt hoz létre a következőből: `TextStamp` formázott dátum- és időkarakterlánc használatával.

## 5. lépés: A bélyegző tulajdonságainak beállítása

Testreszabhatja a bélyegző megjelenését és pozícióját. A tulajdonságait a következőképpen állíthatja be:

```csharp
// A bélyegző tulajdonságainak beállítása
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

Ebben a lépésben beállítjuk a margókat, és a bélyegzőt a PDF-oldal jobb alsó sarkához igazítjuk.

## 6. lépés: Bélyegző hozzáadása a PDF-hez

Most itt az ideje, hogy hozzáadd a szövegbélyegzőt a PDF dokumentumodhoz. 

```csharp
// Bélyeg hozzáadása a bélyeggyűjteményhez
pdfDocument.Pages[1].AddStamp(textStamp);
```

Ez a sor a PDF első oldalára helyezi a bélyegzőt. Módosíthatja az oldalszámot, ha egy másik oldalra szeretné helyezni.

## 7. lépés: Szabad szöveges jegyzet létrehozása (opcionális)

Ha megjegyzést szeretne hozzáadni a bélyegzőhöz, létrehozhat egy `FreeTextAnnotation` alábbiak szerint:

```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance);
textAnnotation.Name = "Stamp";
textAnnotation.Accept(new AnnotationSelector(textAnnotation));
textAnnotation.Contents = textStamp.Value;
```

Ez az opcionális lépés egy szabad szöveges jegyzetet hoz létre, amely további kontextust vagy információkat nyújthat a bélyegzőről.

## 8. lépés: A megjegyzésszegély konfigurálása

Ha testre szeretnéd szabni a jegyzeted szegélyét, azt is megteheted:

```csharp
Border border = new Border(textAnnotation);
border.Width = 0;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(0, 0, 0, 0);
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

Ez a kódrészlet a szegély szélességét 0-ra állítja, így láthatatlanná válik, és hozzáadja a megjegyzést a PDF-hez.

## 9. lépés: Mentse el a PDF dokumentumot

Végül el kell mentenie a módosított PDF dokumentumot. 

```csharp
dataDir = dataDir + "AddDateTimeStamp_out.pdf"; // Adja meg a kimeneti fájl nevét
pdfDocument.Save(dataDir);
Console.WriteLine("\nDate time stamp added successfully.\nFile saved at " + dataDir);
```

Ez a sor a hozzáadott időbélyeggel ellátott PDF-et egy új fájlba menti. A kimenet megtekintéséhez ellenőrizheti a megadott könyvtárat.

## Következtetés

Gratulálunk! Sikeresen hozzáadott egy dátum- és időbélyegzőt egy PDF-fájlhoz az Aspose.PDF for .NET segítségével. Ez az egyszerű, mégis hatékony funkció javíthatja dokumentumai minőségét, professzionálisabbá teheti azokat, és egyértelműen feljegyezheti létrehozásuk vagy módosításuk időpontját. 

## GYIK

### Testreszabhatom a dátumformátumot az időbélyegben?
Igen, módosíthatja a `ToString` módszer a dátumformátum tetszés szerinti módosítására.

### Ingyenesen használható az Aspose.PDF?
Az Aspose.PDF ingyenes próbaverziót kínál, de a teljes funkciók eléréséhez licencet kell vásárolnia. Ideiglenes licencet is vásárolhat. [itt](https://purchase.aspose.com/temporary-license/).

### Hozzáadhatok több időbélyeget egy PDF-hez?
Természetesen! Többet is létrehozhatsz `TextStamp` példányokat, és hozzáadhatja azokat a PDF különböző oldalaihoz vagy pozícióihoz.

### Mi van, ha nincs Visual Studio-m?
Bármilyen C# IDE-t vagy szövegszerkesztőt használhatsz, de a projekt futtatásához és hibakereséséhez a Visual Studio ajánlott.

### Hol találok további példákat az Aspose.PDF használatára?
További példákat és oktatóanyagokat találhatsz a [Aspose.PDF dokumentáció](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}