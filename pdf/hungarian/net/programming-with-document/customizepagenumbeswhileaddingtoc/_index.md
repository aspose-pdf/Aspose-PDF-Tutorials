---
"description": "Ebben az átfogó oktatóanyagban megtudhatja, hogyan szabhatja testre az oldalszámozást tartalomjegyzék hozzáadásakor PDF-dokumentumaihoz az Aspose.PDF for .NET használatával."
"linktitle": "Oldalszámok testreszabása tartalomjegyzék hozzáadásakor"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Oldalszámok testreszabása tartalomjegyzék hozzáadásakor"
"url": "/hu/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Oldalszámok testreszabása tartalomjegyzék hozzáadásakor

## Bevezetés

dokumentumkezelés világában a PDF-ek uralják a főszerepet. Ezek a dokumentumok különböző platformokon keresztüli megosztásának és megőrzésének elsődleges formátumai. De mi történik, ha PDF-dokumentumait olyan funkciókkal szeretné kiegészíteni, mint a tartalomjegyzék (TOC)? Itt jön képbe az Aspose.PDF for .NET! Ez a hatékony könyvtár lehetővé teszi a fejlesztők számára, hogy könnyedén kezeljék a PDF-fájlokat, lehetővé téve számukra a tartalom erőfeszítés nélküli hozzáadását, módosítását és testreszabását. Ebben az oktatóanyagban belemerülünk abba, hogyan szabhatja testre az oldalszámokat, miközben tartalomjegyzéket ad hozzá PDF-dokumentumaihoz az Aspose.PDF for .NET segítségével. Tehát, ragadja meg a programozó sapkáját, és kezdjük is!

## Előfeltételek

Mielőtt belevágnánk a kódba, van néhány dolog, aminek a helyén kell lennie:

1. Visual Studio: Győződjön meg róla, hogy a Visual Studio telepítve van a gépén. Ez lesz a fejlesztői környezetünk.
2. Aspose.PDF .NET-hez: Le kell töltened és telepítened az Aspose.PDF könyvtárat. Megtalálod itt: [itt](https://releases.aspose.com/pdf/net/).
3. C# alapismeretek: A C# programozással való ismeret segít jobban megérteni a kódrészleteket.
4. Minta PDF fájl: Készítsen elő egy minta PDF fájlt, amellyel dolgozhatunk. Létrehozhat egy egyszerűt, vagy letölthet egy meglévő PDF fájlt.

## Csomagok importálása

Kezdésként importálnunk kell a szükséges csomagokat. Nyisd meg a Visual Studio projektedet, és adj hozzá egy hivatkozást az Aspose.PDF könyvtárhoz. Ezt a NuGet csomagkezelővel teheted meg:

1. Kattintson jobb gombbal a projektjére a Megoldáskezelőben.
2. Válassza a „NuGet-csomagok kezelése” lehetőséget.
3. Keresd meg az „Aspose.PDF” fájlt, és telepítsd.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Miután telepítetted a könyvtárat, elkezdhetsz kódolni!

## 1. lépés: Dokumentumkönyvtár beállítása

Először is be kell állítanunk a dokumentumkönyvtárunkat. Ide fogjuk tárolni a bemeneti és kimeneti PDF fájljainkat. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

Ebben a kódrészletben cserélje ki a következőt: `YOUR DOCUMENT DIRECTORY` a PDF-fájlok tényleges elérési útjával. Ez segít nekünk betölteni a meglévő PDF-et és menteni a módosított verziót.

## 2. lépés: Töltse be a meglévő PDF fájlt

Most, hogy beállítottuk a dokumentumkönyvtárunkat, töltsük be a meglévő PDF fájlt. 

```csharp
Document doc = new Document(inFile);
```

Itt létrehozunk egy újat `Document` objektum a bemeneti fájl elérési útjának átadásával. Ez lehetővé teszi számunkra, hogy programozottan manipuláljuk a PDF tartalmát.

## 3. lépés: Új oldal beszúrása a tartalomjegyzékhez

Ezután létre kell hoznunk egy új oldalt a PDF-ben, ahol a tartalomjegyzék lesz.

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

Ez a sor új oldalt szúr be a dokumentum elejére. A tartalomjegyzék ezen az oldalon fog megjelenni.

## 4. lépés: Tartalomjegyzék-információk létrehozása

Most hozzunk létre egy objektumot a tartalomjegyzék információinak ábrázolására.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

Ebben a lépésben létrehozunk egy `TocInfo` objektumot, és a címét „Tartalomjegyzék”-re állítjuk. A betűméretet és -stílust is testre szabjuk. `PageNumbersPrefix` „P” értékre van állítva, amely a tartalomjegyzékben az oldalszámok elé kerül.

## 5. lépés: Címsorok hozzáadása a tartalomjegyzékhez

Most jön a mókás rész! Végigmegyünk a dokumentum oldalain, és címsorokat adunk a tartalomjegyzékhez.

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

Ebben a ciklusban létrehozunk egy újat `Heading` objektum minden oldalhoz. Beállítjuk az egyes címsorok céloldalát, és megadjuk a megjelenítendő szöveget, ami az „X. oldal”, ahol X az oldalszám. Végül hozzáadjuk a címsort a tartalomjegyzék oldalhoz.

## 6. lépés: Mentse el a frissített dokumentumot

Miután hozzáadtuk az összes szükséges címsort, itt az ideje menteni a frissített dokumentumot.

```csharp
doc.Save(outFile);
```

Ez a sor menti a módosított PDF-et a tartalomjegyzékkel együtt. Most megnyithatja a kimeneti fájlt, és megtekintheti a testreszabott tartalomjegyzéket!

## Következtetés

És íme! Sikeresen testre szabtad az oldalszámozást, miközben tartalomjegyzéket adtál a PDF dokumentumodhoz az Aspose.PDF for .NET segítségével. Ez a hatékony könyvtár megkönnyíti a PDF fájlok kezelését, és mindössze néhány sornyi kóddal jelentősen javíthatod a dokumentumok minőségét. Akár jelentéseket, e-könyveket vagy bármilyen más típusú PDF-et készítesz, a tartalomjegyzék nagyban javíthatja az olvasók navigációját. Szóval, mire vársz? Merülj el az Aspose.PDF-ben, és kezdj el lenyűgöző PDF-eket készíteni még ma!

## GYIK

### Mi az Aspose.PDF .NET-hez?
Az Aspose.PDF for .NET egy olyan könyvtár, amely lehetővé teszi a fejlesztők számára, hogy programozottan hozzanak létre, szerkesszenek és konvertáljanak PDF dokumentumokat.

### Ingyenesen használhatom az Aspose.PDF fájlt?
Igen, az Aspose ingyenes próbaverziót kínál, amellyel felfedezheted a könyvtár funkcióit. Letöltheted. [itt](https://releases.aspose.com/).

### Hogyan kaphatok támogatást az Aspose.PDF fájlhoz?
Segítséget kaphatsz az Aspose fórumon [itt](https://forum.aspose.com/c/pdf/10).

### Van ideiglenes jogosítvány?
Igen, kérhet ideiglenes licencet az Aspose.PDF fájlhoz. [itt](https://purchase.aspose.com/temporary-license/).

### Hol tudom megvásárolni az Aspose.PDF .NET-hez készült fájlt?
Megvásárolhatja az Aspose.PDF fájlt .NET-hez [itt](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}