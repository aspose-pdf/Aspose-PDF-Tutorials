---
"description": "Lépésről lépésre útmutató PDF-fájlok oldaltájolásának megváltoztatásához az Aspose.PDF for .NET segítségével. Könnyen követhető és megvalósítható a projektjeiben."
"linktitle": "Orientációváltás"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Orientációváltás"
"url": "/hu/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Orientációváltás

## Bevezetés

Előfordult már, hogy nehezen boldogulsz egy olyan PDF fájllal, ahol az oldal tájolása egyszerűen... rossz? Talán egy rosszul szkennelt vagy létrehozott dokumentummal van dolgod, és az oldalakat el kell forgatni, hogy értelmesek legyenek. Szerencsénkre az Aspose.PDF for .NET egy egyszerű és hatékony módszert kínál a PDF fájlok szinte bármilyen elképzelhető módon történő manipulálására – beleértve az oldalak tájolásának megváltoztatását is. Akár állóról fekvőre, akár fordítva szeretnél váltani, ez az útmutató lépésről lépésre végigvezet a folyamaton.

Tehát, ha készen állsz arra, hogy belevágj és könnyedén forgathasd ezeket a PDF oldalakat, kezdjük is!

## Előfeltételek

Mielőtt belemennénk a PDF oldaltájolásának módosításának részleteibe, nézzük át röviden, mire lesz szükséged:

- Aspose.PDF .NET-hez: Győződjön meg róla, hogy telepítette az Aspose.PDF .NET-hez készült könyvtárat. Ha nem tette meg, akkor megteheti [töltsd le itt](https://releases.aspose.com/pdf/net/).
- .NET fejlesztői környezet: A .NET-tel való munkához használhatja a Visual Studio-t, a JetBrains Rider-t vagy bármilyen más preferált IDE-t.
- C# alapismeretek: Bár ez az útmutató közérthető, a C# alapvető ismeretei még könnyebbé teszik a követését.
- PDF-fájl: Az alábbi példa feltételezi, hogy van egy többoldalas PDF-fájlja. Ha nincs kéznél ilyen, hozzon létre vagy töltsön le egy minta PDF-fájlt a munkához.

Továbbá, ha most kezded, kipróbálhatod az Aspose.PDF fájlt egy [ingyenes ideiglenes jogosítvány](https://purchase.aspose.com/temporary-license/) mielőtt úgy döntene, hogy [vedd meg a teljes verziót](https://purchase.aspose.com/buy).

## Névterek importálása

Mielőtt módosíthatnád az oldalak tájolását a PDF-ben, importálnod kell a szükséges névtereket a C#-projektedbe. Győződj meg róla, hogy a következőkkel rendelkezel:

```csharp
using System.IO;
using Aspose.Pdf;
```

Miután ezt importáltuk, ugorjunk rá a bemutató fő részére.

## 1. lépés: Töltse be a PDF dokumentumot

Az első dolog, amit tennünk kell, az a módosítani kívánt PDF fájl betöltése. Használhatod a `Document` osztályt az Aspose.PDF névtérből a PDF megnyitásához.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Ez a sor betölti a PDF-et a megadott könyvtárból. Ügyeljen arra, hogy kicserélje a következőt: `"YOUR DOCUMENT DIRECTORY"` a fájl tényleges elérési útjával. `"input.pdf"` az a PDF, amelynek a tájolását módosítani szeretné.

## 2. lépés: Végigmérés minden oldalon

Most, hogy betöltettük a dokumentumot, menjünk végig a PDF minden egyes oldalán. Használni fogunk egy `foreach` egy ciklust, hogy végigmenjen az összes oldalon, lehetővé téve számunkra, hogy a tájolásváltozást mindegyikre alkalmazzuk.

```csharp
foreach (Page page in doc.Pages)
{
    // Minden oldal manipulálása
}
```

Ez a ciklus végigmegy a dokumentum összes oldalán.

## 3. lépés: Szerezd meg az oldal médiadobozát

Egy PDF minden oldalán található egy `MediaBox` amely meghatározza az oldal határait. Ehhez hozzá kell férnünk az aktuális tájolás meghatározásához és módosításához.

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

A `MediaBox` megadja az oldal méreteit, például a szélességét, magasságát és elhelyezkedését.

## 4. lépés: Cserélje fel a szélességet és a magasságot

Az oldal tájolásának állóról fekvőre vagy fekvőről állóra való módosításához egyszerűen fel kell cserélnünk a szélesség és a magasság értékeit. Ez a lépés az oldal méreteit módosítja.

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

Ez a kód felcseréli a magasságot és a szélességet, és áthelyezi a bal alsó sarkot (`LLY`), hogy a tartalom forgatás után szépen illeszkedjen.

## 5. lépés: A MediaBox és a CropBox frissítése

Most, hogy megvan az új magasság és szélesség, alkalmazzuk a módosításokat az oldalra `MediaBox` és `CropBox`. A `CropBox` elengedhetetlen, ha az eredeti dokumentumnak csak egy példánya volt, biztosítva, hogy a teljes oldal helyesen jelenjen meg.

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

Ez a lépés az újonnan kiszámított méretek alapján méretezi át az oldalt.

## 6. lépés: Az oldal elforgatása

Végül beállítjuk az oldal elforgatási szögét. Az Aspose.PDF ezt rendkívül egyszerűvé teszi. Az oldalt 90 fokkal elforgathatjuk, így álló helyzetből fekvőbe vagy fordítva válthatunk.

```csharp
page.Rotate = Rotation.on90;
```

Ez a kód 90 fokkal elforgatja az oldalt, a kívánt irányba fordítva azt.

## 7. lépés: Mentse el a kimeneti PDF-et

Miután az összes oldalra alkalmaztuk a tájolási módosításokat, a módosított dokumentumot egy új fájlba mentjük. 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

Ügyeljen arra, hogy új fájlnevet adjon meg (ebben az esetben `ChangeOrientation_out.pdf`) a kimenet mentéséhez. Így nem írja felül az eredeti fájlt.

### Következtetés

És íme! Egy PDF fájl oldaltájolásának módosítása az Aspose.PDF for .NET segítségével olyan egyszerű, mint a dokumentum betöltése, az oldalak közötti ismétlés, a MediaBox beállítása és a frissített fájl mentése. Akár egy rosszul szkennelt dokumentummal van dolgod, akár az oldalakat kell elforgatnod a formázási igényeidnek megfelelően, ez a lépésről lépésre szóló útmutató mindent segít.

## GYIK

### Elforgathatom a PDF összes oldala helyett csak bizonyos oldalakat?  
Igen, módosíthatod a ciklust úgy, hogy az összes oldal végigfutása helyett az adott oldalakat az indexük alapján célozza meg.

### Mi a `MediaBox`?  
A `MediaBox` Meghatározza az oldal méretét és alakját egy PDF fájlban. Ide kerül az oldal tartalma.

### Az Aspose.PDF for .NET működik más fájlformátumokkal is?  
Igen, az Aspose.PDF számos fájlformátumot képes kezelni, például HTML-t, XML-t, XPS-t és egyebeket.

### Létezik az Aspose.PDF ingyenes verziója .NET-hez?  
Igen, elkezdheted egy [ingyenes próba](https://releases.aspose.com/) vagy kérjen egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/).

### Visszavonhatom a módosításokat a mentés után?  
A dokumentum mentése után a módosítások véglegesek. Ügyeljen arra, hogy az eredeti fájl másolatán dolgozzon, vagy biztonsági másolatot készítsen róla.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}