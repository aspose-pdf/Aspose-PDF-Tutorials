---
"description": "Ebben a lépésről lépésre bemutató útmutatóban könnyedén hozzáadhatsz oldalszámokat a PDF fejlécéhez és láblécéhez egy lebegő doboz segítségével az Aspose.PDF for .NET segítségével."
"linktitle": "Oldalszámozás fejlécben és láblécben lebegő doboz használatával"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Oldalszámozás fejlécben és láblécben lebegő doboz használatával"
"url": "/hu/net/programming-with-stamps-and-watermarks/page-number-in-header-footer-using-floating-box/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Oldalszámozás fejlécben és láblécben lebegő doboz használatával

## Bevezetés

A PDF dokumentumok programozott kezelésének terén az Aspose.PDF for .NET kivételes eszközként tűnik ki. Leegyszerűsíti a PDF fájlok létrehozásának, szerkesztésének és manipulálásának módját a .NET alkalmazásokban. Akár számlákat, jelentéseket vagy bármilyen más dokumentumtípust generál, az oldalszámok elegáns hozzáadása javíthatja a PDF-ek professzionalizmusát és szervezettségét. Ebben az oktatóanyagban elmerülünk abban, hogyan adhatunk hozzá oldalszámokat a PDF fejlécéhez és láblécéhez egy lebegő doboz segítségével. Készen állsz a kezdésre? Rajta!

## Előfeltételek

Mielőtt belevágnánk ebbe az izgalmas utazásba a PDF-manipuláció birodalmába, van néhány dolog, amire szükséged van:

### .NET környezet beállítása
Győződjön meg róla, hogy rendelkezik .NET fejlesztői környezettel. Használhatja a Visual Studio-t, amely népszerű választás a fejlesztők körében a .NET alkalmazásokhoz.

### Aspose.PDF könyvtár
Telepítsd az Aspose.PDF könyvtárat. Könnyen letöltheted a weboldalról:

- [Aspose.PDF letöltése .NET-hez](https://releases.aspose.com/pdf/net/)

### C# programozási alapismeretek
A C# alapvető ismerete segít megérteni az ebben az oktatóanyagban bemutatott fogalmakat és kódrészleteket.

### Hozzáférés a dokumentációhoz
Mindig előnyös, ha van [Aspose.PDF dokumentáció](https://reference.aspose.com/pdf/net/) hasznos referenciaként és a további funkciók mélyebb megismeréséhez.

## Csomagok importálása

A kezdéshez importálnod kell a szükséges csomagokat a projektedbe. Ez biztosítja, hogy az Aspose.PDF assembly hozzáférhető legyen a kódodban. Így teheted meg:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Most pedig bontsuk le kezelhető lépésekre az oldalszámozás folyamatát egy lebegő doboz segítségével. Kövesd a lépést.

## 1. lépés: Dokumentumkörnyezet beállítása

Kezdjük azzal, hogy megadjuk azt a könyvtárat, ahová a PDF dokumentumot tárolni szeretnénk. Ez azért kulcsfontosságú, mert ez határozza meg, hogy hová kerül mentésre a kimeneti fájl.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Csere `YOUR DOCUMENT DIRECTORY` a választott elérési úttal, ahová a kimeneti PDF fájlt menteni szeretné.

## 2. lépés: A dokumentum példányosítása

A következő lépés egy új PDF dokumentum létrehozása. Ez magában foglalja a következő használatát: `Document` osztály az Aspose.PDF könyvtárból.

```csharp
// Dokumentumpéldány példányosítása
Aspose.Pdf.Document pdf = new Aspose.Pdf.Document();
```
Itt létrehozunk egy új példányt a `Document` osztály, amely a manipulációnk vászonjaként szolgál.

## 3. lépés: Új oldal hozzáadása

Most adjunk hozzá egy oldalt a PDF dokumentumunkhoz. Minden PDF-nek kell legalább egy oldal, ugye?

```csharp
// Oldal hozzáadása a PDF dokumentumhoz
Aspose.Pdf.Page page = pdf.Pages.Add();
```
Ez a kódrészlet egy új oldalt ad hozzá a dokumentumunkhoz, így az készen áll a tartalom fogadására, beleértve az oldalszámokkal ellátott lebegő dobozunkat is.

## 4. lépés: Lebegő doboz létrehozása

Ezután itt az ideje létrehozni a lebegő dobozt, amely az oldalszámot fogja tartalmazni. `FloatingBox` Az osztály lehetővé teszi számunkra, hogy a tartalmat szabadon elhelyezzük az oldalon.

```csharp
// Inicializálja a FloatingBox osztály egy új példányát.
Aspose.Pdf.FloatingBox box1 = new Aspose.Pdf.FloatingBox(140, 80);
```
Itt a paraméterek `(140, 80)` Adja meg a lebegő doboz szélességét és magasságát. Ezeket az értékeket az elrendezési preferenciák alapján módosíthatja.

## 5. lépés: Az úszó doboz elhelyezése

A pozicionálás kulcsfontosságú! Meg kell határoznod, hogy az oldalszám hol jelenjen meg az oldalon. A következővel fogsz dolgozni: `Left` és `Top` tulajdonságok a pozíció meghatározásához.

```csharp
// A bekezdés bal oldali pozícióját jelző lebegőpontos érték
box1.Left = 2;
// Lebegőpontos érték, amely a bekezdés legfelső pozícióját jelzi
box1.Top = 10;
```
Ezek az értékek határozzák meg a lebegő doboz elhelyezését az oldalon. Kísérletezz velük nyugodtan, hogy lásd, mi mutat a legjobban a dokumentumodban.

## 6. lépés: Szöveg hozzáadása az Oldalszám makróval

Most hozzáadunk egy karakterláncot, amely dinamikusan megjeleníti az oldalszámot. Itt történik a varázslat!

```csharp
// Makrók hozzáadása a FloatingBox bekezdésgyűjteményéhez
box1.Paragraphs.Add(new Aspose.Pdf.Text.TextFragment("Page: ($p/ $P )"));
```
Ebben az esetben `($p/ $P)` egy makró, amely megjeleníti az aktuális oldalszámot (`$p`) és az oldalak teljes száma (`$P`). Ennek eredményeként a szöveget úgy formázza, hogy valami ilyesmi legyen olvasható, mint „Oldal: 1/5”.

## 7. lépés: Add hozzá a lebegő dobozt az oldalhoz

Ideje hozzáadni a lebegő dobozt az oldalszám szövegével együtt az újonnan létrehozott oldalunkhoz.

```csharp
// Adj hozzá egy floatingBox-ot az oldalhoz
page.Paragraphs.Add(box1);
```
Ez a sor lényegében beágyazza a lebegő dobozt az oldalba, így az a dokumentum elrendezésének részévé válik. 

## 8. lépés: Mentse el a dokumentumot

Végül ne felejtsd el menteni a munkádat! Az utolsó lépés a PDF dokumentum megfelelő fájlnévvel történő mentése.

```csharp
// Mentse el a dokumentumot
pdf.Save(dataDir + "PageNumberinHeaderFooterUsingFloatingBox_out.pdf");
```
Győződjön meg róla, hogy a megadott elérési út tartalmazza a kívánt fájlnevet. Most elkészült a lenyűgöző, oldalszámokkal ellátott PDF! 

## Következtetés

És tessék, emberek! Az Aspose.PDF for .NET segítségével oldalszámokat adhatsz a PDF fejlécéhez és láblécéhez, ilyen egyszerű. Mindössze néhány sornyi kóddal elindulhatsz a dokumentumfeldolgozás mesteri elsajátítása felé az alkalmazásaidban. Ne habozz kísérletezni a különböző elrendezésekkel és formázásokkal – elvégre a kreativitás határtalan! Készen állsz egy professzionális dokumentum létrehozására? Kapd fel a programozó sapkádat, és kezdj el kísérletezni.

## GYIK

### Testreszabhatom az oldalszám szövegének megjelenését?  
Igen, testreszabhatja a szöveg tulajdonságait, például a betűméretet, a színt és a stílust a `TextFragment` tulajdonságok.

### Ingyenesen használható az Aspose.PDF?  
Bár az Aspose.PDF ingyenes próbaverziót kínál, éles használatra fizetős termék. [vedd meg itt](https://purchase.aspose.com/buy).

### Hol találok részletesebb dokumentációt?  
Átfogó dokumentációt találhat a [Aspose.PDF dokumentációs webhely](https://reference.aspose.com/pdf/net/).

### Hogyan alkalmazhatok fejléceket és lábléceket több oldalra?  
Végiglépkedhet a dokumentum összes oldalán, és hasonlóképpen alkalmazhatja a Lebegő dobozt mindegyikre.

### Mi van, ha további funkciókhoz van szükségem támogatásra?  
További kérdéseivel vagy támogatásával kapcsolatban látogassa meg a következőt: [Aspose Fórum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}