---
"description": "Tanuld meg, hogyan alkalmazhatsz különböző számstílusokat (római számok, betűrend) a PDF-címsorokra az Aspose.PDF for .NET használatával ebből a lépésről lépésre szóló útmutatóból."
"linktitle": "Számstílus alkalmazása PDF fájlban"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Számstílus alkalmazása PDF fájlban"
"url": "/hu/net/programming-with-headings/apply-number-style/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Számstílus alkalmazása PDF fájlban

## Bevezetés

Előfordult már, hogy gyönyörűen számozott listákat kellett hozzáadnia PDF-dokumentumaihoz? Akár jogi dokumentumokat, jelentéseket vagy prezentációkat formáz, a megfelelő számozási stílusok elengedhetetlenek az információk rendszerezéséhez. Az Aspose.PDF for .NET segítségével különféle számozási stílusokat alkalmazhat PDF-fájljai címsoraira, így jól strukturált és professzionális dokumentumokat hozhat létre. 

## Előfeltételek

Mielőtt belevágnánk a kódolásba, nézzük át, mire lesz szükséged:

1. Aspose.PDF .NET-hez: Töltse le az Aspose.PDF legújabb verzióját innen: [itt](https://releases.aspose.com/pdf/net/).
2. Fejlesztői környezet: Győződjön meg róla, hogy rendelkezik Visual Studio vagy bármilyen más .NET-kompatibilis IDE-vel.
3. .NET-keretrendszer: Győződjön meg róla, hogy telepítve van a .NET-keretrendszer 4.0-s vagy újabb verziója.
4. Licenc: Használhat egy ideiglenes licencet a következőtől: [itt](https://purchase.aspose.com/temporary-license/) vagy fedezd fel a [ingyenes próba](https://releases.aspose.com/) opciók.

## Csomagok importálása

Első lépésként győződjön meg arról, hogy a következő névterek importálva vannak a projektjében:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

## 1. lépés: A dokumentum beállítása

Kezdjük egy új PDF dokumentum létrehozásával és az oldalbeállítások konfigurálásával. Beállítjuk az oldalméretet és a margókat a tartalom elrendezésének szabályozásához.

Magyarázat: Ebben a lépésben a PDF alapvető szerkezetét állítjuk be, amely magában foglalja az oldalméret, a magasság és a margók meghatározását az egységes formázás érdekében.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDoc = new Document();

// Oldalméretek és margók beállítása
pdfDoc.PageInfo.Width = 612.0;
pdfDoc.PageInfo.Height = 792.0;
pdfDoc.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfDoc.PageInfo.Margin.Left = 72;
pdfDoc.PageInfo.Margin.Right = 72;
pdfDoc.PageInfo.Margin.Top = 72;
pdfDoc.PageInfo.Margin.Bottom = 72;
```

Ezzel a dokumentum szabványos oldalméretű lesz, ami egy 8,5 x 11 hüvelykes oldalnak felel meg, és minden oldalon 72 pontos (vagy 1 hüvelykes) margóval.

## 2. lépés: Oldal hozzáadása a PDF-hez

Ezután hozzáadunk egy új oldalt a PDF dokumentumhoz, ahol később alkalmazni fogjuk a számozási stílusokat.

Magyarázat: Minden PDF-hez oldalak szükségesek! Ez a lépés egy üres oldalt ad a PDF-hez, és a margókat a dokumentumszintű beállításoknak megfelelően állítja be.

```csharp
// Új oldal hozzáadása a PDF dokumentumhoz
Aspose.Pdf.Page pdfPage = pdfDoc.Pages.Add();
pdfPage.PageInfo.Width = 612.0;
pdfPage.PageInfo.Height = 792.0;
pdfPage.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfPage.PageInfo.Margin.Left = 72;
pdfPage.PageInfo.Margin.Right = 72;
pdfPage.PageInfo.Margin.Top = 72;
pdfPage.PageInfo.Margin.Bottom = 72;
```

## 3. lépés: Lebegő doboz létrehozása

A FloatingBox lehetővé teszi tartalom (például szöveg vagy címsorok) elhelyezését egy olyan dobozban, amely az oldal folyásától függetlenül viselkedik. Ez akkor hasznos, ha teljes mértékben kontrollálni szeretnéd a tartalom elrendezését.

Magyarázat: Itt egy FloatingBox-ot állítunk be, amely tartalmazza azokat a címsorokat, amelyekre számstílusokat fogunk alkalmazni.

```csharp
// Hozz létre egy FloatingBox-ot strukturált tartalomhoz
Aspose.Pdf.FloatingBox floatBox = new Aspose.Pdf.FloatingBox();
floatBox.Margin = pdfPage.PageInfo.Margin;
pdfPage.Paragraphs.Add(floatBox);
```

## 4. lépés: Adja hozzá az első címsort római számokkal

Most jön az izgalmas rész! Adjuk hozzá az első címsort kisbetűs római számokkal.

Magyarázat: A NumberingStyle.NumeralsRomanLowercase stílust alkalmazzuk a címsorra, amely római számokkal (i, ii, iii stb.) jeleníti meg a számozást.

```csharp
// Hozd létre az első címsort római számokkal
Aspose.Pdf.Heading heading = new Aspose.Pdf.Heading(1);
heading.IsInList = true;
heading.StartNumber = 1;
heading.Text = "List 1";
heading.Style = NumberingStyle.NumeralsRomanLowercase;
heading.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading);
```

## 5. lépés: Adjon hozzá egy második római számot a címsorhoz

Bemutatásképpen adjunk hozzá egy második római számokat tartalmazó címsort, de ezúttal 13-tól kezdjük.

Magyarázat: A StartNumber tulajdonság lehetővé teszi a számozás egyéni számmal történő kezdését – ebben az esetben 13-tól kezdjük.

```csharp
// Hozz létre egy második címsort, amely a római 13-as számmal kezdődik
Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
heading2.IsInList = true;
heading2.StartNumber = 13;
heading2.Text = "List 2";
heading2.Style = NumberingStyle.NumeralsRomanLowercase;
heading2.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading2);
```

## 6. lépés: Címsor hozzáadása betűrendes számozással

A változatosság kedvéért adjunk hozzá egy harmadik címsort, de ezúttal kisbetűs betűrendes számozást fogunk használni (a, b, c stb.).

Magyarázat: Ha a NumberingStyle-t LettersLowercase-re módosítjuk, betűrendes számozást alkalmazhatunk a címsorainkra.

```csharp
// Hozzon létre egy címsort betűrendes számozással
Aspose.Pdf.Heading heading3 = new Aspose.Pdf.Heading(2);
heading3.IsInList = true;
heading3.StartNumber = 1;
heading3.Text = "the value, as of the effective date of the plan, of property to be distributed under the plan on account of each allowed";
heading3.Style = NumberingStyle.LettersLowercase;
heading3.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading3);
```

## 7. lépés: A PDF mentése

Végül, miután alkalmaztuk az összes címsor- és számstílust, mentsük el a PDF fájlt a kívánt könyvtárba.

Magyarázat: Ez a lépés menti a PDF fájlt, amely tartalmazza az összes formázott címsort az alkalmazott számozási stílusokkal.

```csharp
// PDF dokumentum mentése
dataDir = dataDir + "ApplyNumberStyle_out.pdf";
pdfDoc.Save(dataDir);
Console.WriteLine("\nNumber style applied successfully in headings.\nFile saved at " + dataDir);
```

## Következtetés

És íme! Sikeresen alkalmaztál számozási stílusokat – római számokat és betűrendet – egy PDF fájl címsoraira az Aspose.PDF for .NET segítségével. Az Aspose.PDF által biztosított rugalmasság az oldalelrendezés, a számozási stílusok és a tartalom elhelyezésének szabályozásában hatékony eszközkészletet biztosít jól szervezett, professzionális PDF dokumentumok létrehozásához.

## GYIK

### Alkalmazhatok különböző számstílusokat ugyanarra a PDF dokumentumra?  
Igen, az Aspose.PDF for .NET lehetővé teszi különböző számozási stílusok, például római számok, arab számok és betűrendes számozás keverését ugyanazon a dokumentumon belül.

### Hogyan tudom testreszabni a címsorok kezdőszámát?  
Bármely címsor kezdőszámát beállíthatja a használatával. `StartNumber` ingatlan.

### Van mód a számozási sorrend visszaállítására?  
Igen, a számozást visszaállíthatja a `StartNumber` tulajdonság minden címsorhoz.

### Alkalmazhatok félkövér vagy dőlt betűstílust a címsorokra a számozás mellett?  
Természetesen! A címsorstílusokat testreszabhatja olyan tulajdonságok módosításával, mint a betűtípus, a méret, a félkövér és a dőlt betűtípus a `TextState` objektum.

### Hogyan szerezhetek ideiglenes licencet az Aspose.PDF fájlhoz?  
Ideiglenes jogosítványt igényelhetsz [itt](https://purchase.aspose.com/temporary-license/) az Aspose.PDF korlátozás nélküli tesztelésére.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}