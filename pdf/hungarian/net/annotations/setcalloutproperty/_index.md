---
"description": "Ebben a részletes, lépésről lépésre bemutató útmutatóban megtudhatja, hogyan állíthatja be a callout tulajdonságot egy PDF fájlban az Aspose.PDF for .NET használatával."
"linktitle": "Felhívás tulajdonságának beállítása PDF fájlban"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Felhívás tulajdonságának beállítása PDF fájlban"
"url": "/hu/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Felhívás tulajdonságának beállítása PDF fájlban

## Bevezetés

professzionális és vizuálisan vonzó PDF dokumentumok létrehozása gyakran megköveteli a figyelemfelkeltő megjegyzések hozzáadását, amelyek felhívják a figyelmet egy adott tartalomra. Az egyik ilyen megjegyzés a felirat, amely olyan, mint a képregényekben látható szövegbuborékok. Segítenek tisztázni vagy kiemelni a szöveget a PDF-ben. Az Aspose.PDF for .NET hihetetlenül egyszerűvé teszi az ilyen megjegyzések hozzáadását a dokumentumokhoz, és ebben az oktatóanyagban végigvezetjük azon, hogyan állíthatja be a felirat tulajdonságot egy PDF fájlban ennek a hatékony könyvtárnak a segítségével. Akár tapasztalt fejlesztő, akár most kezd, az útmutató végére világosan megérti majd, hogyan kell feliratokkal dolgozni a PDF fájlokban.

## Előfeltételek

Mielőtt belemerülnénk a kódba, nézzük meg a kezdéshez szükséges alapvető tudnivalókat.

1. Aspose.PDF .NET-hez: Győződjön meg róla, hogy telepítve van az Aspose.PDF .NET-hez könyvtár. Letöltheti innen: [itt](https://releases.aspose.com/pdf/net/).
2. IDE: Fejlesztői környezet, például a Visual Studio.
3. .NET-keretrendszer: Győződjön meg arról, hogy a .NET telepítve van a gépén.
4. Ideiglenes licenc: Ha korlátozások nélkül szeretné kipróbálni az Aspose.PDF összes funkcióját, szerezzen be egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/).

## Csomagok importálása

Mielőtt elkezdenéd a kód írását, importálnod kell a szükséges csomagokat, amelyek lehetővé teszik a PDF-fájlokkal és annotációkkal való munkát.

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Ezek az importálások minden szükséges osztályt és metódust biztosítanak a PDF dokumentumok kezeléséhez és olyan jegyzetek létrehozásához, mint a kiemelés.

## 1. lépés: A PDF dokumentum inicializálása

Az első lépés az utunkon egy új PDF dokumentum inicializálása, ahová felvesszük a kiemelt jegyzeteket. Gondoljon erre úgy, mint egy üres vászon létrehozására, ahová elkezdheti az elemek hozzáadását.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Új PDF dokumentum inicializálása
Document doc = new Document();
```
Itt egy újat hozunk létre, `Document` objektum, amely PDF fájlként fog szolgálni. `dataDir` változó értéke az a könyvtár, ahová a PDF fájlt menteni szeretnénk, miután elkészültünk.

## 2. lépés: Új oldal hozzáadása a dokumentumhoz

Egy PDF dokumentum több oldalból állhat, és ebben a lépésben egy új oldalt adunk hozzá a dokumentumhoz. Ez az oldal lesz a hely, ahová a kiemelt jegyzeteket helyezzük el.

```csharp
// Új oldal hozzáadása a dokumentumhoz
Page page = doc.Pages.Add();
```
A `Pages.Add()` metódust használunk egy új oldal hozzáadására a `doc` objektum. Az új oldal a következő helyen tárolódik: `page` változó, amelyet később fogunk használni az annotáció hozzáadásakor.

## 3. lépés: Az alapértelmezett megjelenés meghatározása

A jegyzetek, akárcsak a feliratok, testreszabható vizuális megjelenéssel rendelkeznek. Ebben a lépésben meghatározzuk, hogyan nézzen ki a feliraton belüli szöveg.

```csharp
// A jegyzet alapértelmezett megjelenésének meghatározása
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
Létrehozunk egy `DefaultAppearance` egy objektum, amely meghatározza a szöveg színét és betűméretét. Itt a szöveg piros lesz, a betűméret pedig 10-es. Ez a megjelenés lesz érvényes a feliratra.

## 4. lépés: Hozza létre a szabad szöveges jegyzetet

Most itt az ideje létrehozni magát a jegyzetet. A szabad szöveges jegyzet lehetővé teszi számunkra, hogy egy adott szöveggel és stílussal ellátott feliratot adjunk hozzá.

```csharp
// Hozzon létre egy FreeTextAnnotation-t egy kiemeléssel
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
Létrehozunk egy `FreeTextAnnotation` egy adott koordinátákkal rendelkező objektum, amely meghatározza a pozícióját az oldalon. `Intent` erre van beállítva `FreeTextCallout`, jelezve, hogy ez egy kiemelt megjegyzés. `EndingStyle` erre van beállítva `OpenArrow`, ami azt jelenti, hogy a kiemelő sor egy nyitott nyíllal végződik.

## 5. lépés: A kiemelő vonal pontjainak meghatározása

Egy kiemelt megjegyzésben egy vonal található, amely a vizsgált területre mutat. Itt definiáljuk a vonalat alkotó pontokat.

```csharp
// Határozza meg a kiemelő vonal pontjait
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
A `Callout` az ingatlan egy tömb `Point` objektumok, amelyek mindegyike egy koordinátát jelöl az oldalon. Ezek a pontok határozzák meg a feliratvonal útvonalát, így a klasszikus szövegbuborék-megjelenést kölcsönözve neki.

## 6. lépés: Jegyzet hozzáadása az oldalhoz

Miután létrehoztuk és konfiguráltuk az annotációnkat, a következő lépés az, hogy hozzáadjuk azt az oldalhoz.

```csharp
// Adja hozzá a jegyzetet az oldalhoz
page.Annotations.Add(fta);
```
A `Annotations.Add()` A metódust használjuk a korábban létrehozott oldalon található jegyzet elhelyezésére. Ez a lépés gyakorlatilag „megrajzolja” a feliratot a PDF oldalon.

## 7. lépés: A Rich Text tartalom beállítása

A kiemelt szövegrészek tartalmazhatnak formázott szöveget, így formázott tartalom is elhelyezhető a buborékban. Adjunk hozzá néhány mintaszöveget.

```csharp
// Rich Text beállítása a jegyzethez
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">Ez egy minta</span></p></body>";
```
A `RichText` A tulajdonság HTML tartalommal van beállítva. Ez lehetővé teszi a részletes formázást a feliraton belül, például a betűméret, a szín és a stílus megadását.

## 8. lépés: Mentse el a PDF dokumentumot

Végül, miután mindent beállítottunk, mentenünk kell a dokumentumot. Ez a lépés véglegesíti a PDF létrehozását a kiemelt megjegyzésekkel.

```csharp
// Mentse el a dokumentumot
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
A `Save()` A metódus a megadott könyvtárba menti a dokumentumot „SetCalloutProperty.pdf” fájlnévvel. Ez a lépés lezárja a PDF létrehozási folyamatát.

## Következtetés

És íme! Most hoztál létre egy PDF dokumentumot egy kiemelt jegyzettel az Aspose.PDF for .NET segítségével. Ez a jegyzet hihetetlenül hasznos lehet a dokumentum egyes részeinek kiemelésére vagy magyarázatára. Az Aspose.PDF egy hatékony API-t kínál, amely egyszerűvé és rugalmassá teszi a PDF-manipulációt. Akár jegyzeteket adsz hozzá, akár dokumentumokat konvertálsz, akár összetett PDF-feladatokat kezelsz, az Aspose.PDF segít neked.

## GYIK

### Testreszabhatom tovább a felirat megjelenését?

Természetesen! Testreszabhatod a különböző aspektusokat, például a vonal színét, vastagságát, valamint a szöveg betűtípusát és stílusát.

### Lehetséges több feliratot elhelyezni egyetlen oldalon?

Igen, annyi feliratot adhat hozzá, amennyire szüksége van, a lépések megismétlésével minden egyes megjegyzéshez.

### Hogyan tudom megváltoztatni a felirat pozícióját?

Egyszerűen módosítsa a koordinátákat a `Rectangle` és `Callout` tulajdonságok a megjegyzés áthelyezéséhez.

### Hozzáadhatok más típusú megjegyzéseket az Aspose.PDF használatával?

Igen, az Aspose.PDF különféle annotációtípusokat támogat, beleértve a kiemeléseket, bélyegzőket és fájlmellékleteket.

### A rich text tartalom HTML-re korlátozódik?

A `RichText` tulajdonság a HTML egy részhalmazát támogatja, lehetővé téve formázott szöveg és alapvető formázás hozzáadását.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}