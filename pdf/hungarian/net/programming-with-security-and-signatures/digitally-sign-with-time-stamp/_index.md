---
"description": "Ismerje meg, hogyan írhat digitálisan alá egy PDF-et időbélyeggel az Aspose.PDF for .NET használatával. Ez a lépésről lépésre szóló útmutató ismerteti az előfeltételeket, a tanúsítványok beállítását, az időbélyegzést és egyebeket."
"linktitle": "Digitális aláírás időbélyeggel PDF fájlban"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Digitális aláírás időbélyeggel PDF fájlban"
"url": "/hu/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Digitális aláírás időbélyeggel PDF fájlban

## Bevezetés

Előfordult már, hogy digitálisan alá kellett írnia egy PDF-et, és időbélyeget kellett hozzáadnia a fokozott biztonság érdekében? Akár jogi dokumentumokon, szerződéseken vagy bármi máson dolgozik, ami biztonságos hitelesítést igényel, az időbélyeggel ellátott digitális aláírás extra hitelességi réteget ad hozzá. Ebben az oktatóanyagban bemutatjuk, hogyan használhatja az Aspose.PDF for .NET programot digitális aláírás és időbélyeg hozzáadására PDF-dokumentumaihoz. Ne aggódjon, lépésről lépésre bemutatjuk!

## Előfeltételek

Mielőtt belemerülnénk a kódba, van néhány dolog, amit be kell állítanod a folytatáshoz. Íme egy gyors ellenőrzőlista az előfeltételekről a kezdéshez:

- Aspose.PDF .NET könyvtárhoz: A projektedben telepíteni kell az Aspose.PDF .NET könyvtárat. [töltsd le a legújabb verziót itt](https://releases.aspose.com/pdf/net/) vagy add hozzá a projektedhez a NuGet segítségével.
- PDF dokumentum: Szükséged lesz egy minta PDF fájlra a munkához. Győződj meg róla, hogy van egy fájl a projekt könyvtárában, amelyet alá szeretnél írni.
- Digitális tanúsítvány (PFX fájl): Győződjön meg arról, hogy rendelkezik digitális tanúsítvánnyal (PFX fájl). `.pfx` fájl) a dokumentum digitális aláírásához.
- Időbélyegző URL: Ez egy online időbélyegző szolgáltatás, amelyet arra használnak, hogy időbélyeget csatoljanak a digitális aláíráshoz. 
- C# alapismeretek: Nem kell szakértőnek lenned, de a C# alapjainak ismerete segít megérteni és testre szabni a kódot.

Miután ezeket az összes négyzetet kipipáltad, elkezdheted a kódolást!

## Csomagok importálása

A kezdéshez importálnod kell a következő névtereket a C# projektedbe. Ez biztosítja, hogy hozzáférj a releváns Aspose.PDF osztályokhoz és függvényekhez.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## 1. lépés: Töltse be a PDF dokumentumot

Az első dolog, amit tennünk kell, az az, hogy betöltjük a PDF dokumentumot, amelyet alá szeretnénk írni. Így teheted ezt meg:

```csharp
// Adja meg a dokumentumkönyvtár elérési útját
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// PDF dokumentum betöltése
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

Ez a lépés meglehetősen egyszerű. Egyszerűen csak meg kell adnunk az aláírni kívánt dokumentum elérési útját. `Document` Az Aspose.PDF osztálya kezeli a fájl betöltését.

## 2. lépés: A digitális aláírás beállítása

Ezután létrehozzuk a digitális aláírást a PKCS7 osztály használatával, és betöltjük a PFX fájlt. Ez a PFX fájl tartalmazza a tanúsítványodat és a privát kulcsodat, amelyek szükségesek a dokumentum aláírásához.

```csharp
// A .pfx fájl elérési útja
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// Az aláírásobjektum inicializálása
PdfFileSignature signature = new PdfFileSignature(document);

// Jelszóval töltse be a PFX fájlt
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

Ezen a ponton arra utasítod az Aspose-t, hogy a digitális tanúsítványodat használja a dokumentum aláírásához. `PKCS7` Az objektum elvégzi helyetted az összes titkosítási munkát, így nem kell aggódnod a részletek miatt.

## 3. lépés: Időbélyegző-beállítások hozzáadása

A robusztus digitális aláírás egyik kulcsfontosságú eleme az időbélyeg. Ez biztosítja, hogy a dokumentum aláírása a tanúsítvány lejárta után is ellenőrizhető legyen. Állítsuk be az időbélyeget egy online időbélyegző szolgáltató segítségével.

```csharp
// Időbélyeg-beállítások meghatározása
TimestampSettings timestampSettings = new TimestampSettings("https://your_timestamp_url", "felhasználó:jelszó");

// Időbélyeg-beállítások hozzáadása a PKCS7 objektumhoz
pkcs.TimestampSettings = timestampSettings;
```

Itt megadhatja az időbélyegző szolgáltatás URL-címét, amely automatikusan időpontot és dátumot rendel az aláírásához. Ez hitelesítéssel vagy anélkül is elvégezhető.

## 4. lépés: Az aláírás helyének és megjelenésének meghatározása

Most meghatározzuk, hogy hol jelenjen meg az aláírás a PDF-ben, és milyen méretű legyen. Testreszabhatja az aláírásmező pozícióját az oldalon, valamint a méretét is.

```csharp
// Az aláírás megjelenésének és helyének meghatározása (1. oldal, megadott téglalappal)
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

Itt egy téglalapot definiálunk, amely az aláírást a PDF első oldalán a (100, 100) koordinátákon helyezi el, 200 szélességgel és 100 magassággal. Ezeket az értékeket a tervnek megfelelően módosíthatja.

## 5. lépés: A PDF dokumentum aláírása

Miután minden beállított, itt az ideje, hogy a digitális aláírást alkalmazzuk a PDF-re. Ez a lépés egyetlen egyszerű parancsban egyesíti a tanúsítványt, az időbélyeget és a pozicionálást.

```csharp
// Írja alá a dokumentumot az első oldalon
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

Íme, mi történik:
- 1: Ez azt jelzi, hogy az aláírást az első oldalra kell helyezni.
- „Aláírás oka”: Itt adhatja meg, hogy miért írja alá a dokumentumot.
- „Kapcsolat”: Adja meg az aláíró elérhetőségi adatait.
- „Helyszín”: Adja meg az aláíró helyét.
- igaz: Ez a logikai érték azt jelzi, hogy az aláírás látható-e a dokumentumban.
- rect: A korábban definiált téglalap határozza meg az aláírás méretét és pozícióját.
- pkcs: A PKCS7 objektum tartalmazza a digitális tanúsítvány és az időbélyeg beállításait.

## 6. lépés: Mentse el az aláírt PDF-et

Miután a dokumentumot aláírta, már csak mentenie kell. Új fájlnevet választhat, hogy mind az eredeti, mind az aláírt verziót megőrizze.

```csharp
// Mentse el az aláírt PDF dokumentumot
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

Az újonnan aláírt és időbélyeggel ellátott PDF-fájl most a megadott könyvtárba lett mentve!

## Következtetés

És íme! Sikeresen digitálisan aláírtál egy időbélyeggel ellátott PDF-et az Aspose.PDF for .NET segítségével. Ez a folyamat biztosítja a dokumentumok hitelességét és integritását, így mind neked, mind a címzettnek megnyugvást ad. A digitális aláírások egyre fontosabbá válnak a mai digitális világban, így a folyamat elsajátítása mindenképpen érdemes készség.

## GYIK

### Használhatok más fájlformátumot a tanúsítványhoz?  
Igen, de az oktatóanyag a PFX fájl használatára összpontosít, amely a digitális tanúsítványok leggyakoribb formátuma.

### Szükségem van internetkapcsolatra az időbélyeg alkalmazásához?  
Igen, mivel az időbélyeget egy online időbélyegző hatóságtól kérik le, internet-hozzáférésre lesz szüksége.

### Aláírhatok több oldalt egy PDF-ben?  
Természetesen! Módosíthatod a `signature.Sign()` metódus több oldal megcélzására vagy az összes oldal végigkeresésére.

### Mi történik, ha a PFX fájl jelszava helytelen?  
Kivételt kapsz, ha a jelszó helytelen, ezért ellenőrizd, hogy helyesen adtad-e meg.

### Láthatatlanná tehetem az aláírást?  
Igen, átmehetsz `false` a `Sign` a metódus láthatósági paramétere az aláírás láthatatlanná tételéhez.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}