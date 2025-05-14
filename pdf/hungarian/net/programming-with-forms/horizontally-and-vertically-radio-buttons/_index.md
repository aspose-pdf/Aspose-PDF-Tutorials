---
"description": "Tanuld meg, hogyan hozhatsz létre vízszintesen és függőlegesen igazított választógombokat PDF formátumban az Aspose.PDF for .NET használatával ezzel a lépésről lépésre szóló útmutatóval."
"linktitle": "Vízszintesen és függőlegesen választógombok"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Vízszintesen és függőlegesen választógombok"
"url": "/hu/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vízszintesen és függőlegesen választógombok

## Bevezetés

Az interaktív PDF űrlapok létrehozása jelentősen javíthatja a felhasználói élményt, különösen az információgyűjtés terén. Az egyik leggyakoribb űrlapelem a választógomb, amely lehetővé teszi a felhasználók számára, hogy egy lehetőség közül válasszanak egyet egy készletből. Ebben az oktatóanyagban azt vizsgáljuk meg, hogyan hozhatunk létre vízszintesen és függőlegesen igazított választógombokat az Aspose.PDF for .NET használatával. Akár tapasztalt fejlesztő vagy, akár most kezded, ez az útmutató lépésről lépésre végigvezet a folyamaton, biztosítva, hogy minden egyes részt világosan megérts.

## Előfeltételek

Mielőtt belemerülnénk a kódba, van néhány előfeltétel, aminek teljesülnie kell:

1. Aspose.PDF .NET-hez: Győződjön meg róla, hogy telepítve van az Aspose.PDF könyvtár. Letöltheti innen: [telek](https://releases.aspose.com/pdf/net/).
2. Visual Studio: Egy fejlesztői környezet, ahol kódot írhatsz és tesztelhetsz.
3. C# alapismeretek: A C# programozással való ismeret segít jobban megérteni a kódrészleteket.

## Csomagok importálása

A kezdéshez importálnod kell a szükséges csomagokat a C# projektedbe. Így teheted meg:

### Új projekt létrehozása

Nyisd meg a Visual Studiot, és hozz létre egy új C# projektet. Az egyszerűség kedvéért választhatsz egy konzolalkalmazást.

### Aspose.PDF referencia hozzáadása

1. Kattintson jobb gombbal a projektjére a Megoldáskezelőben.
2. Válassza a „NuGet-csomagok kezelése” lehetőséget.
3. Keresd meg az „Aspose.PDF” fájlt, és telepítsd a legújabb verziót.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

Most, hogy mindent beállítottál, bontsuk le a kódot, hogy vízszintesen és függőlegesen igazított választógombokat hozzunk létre.

## 1. lépés: A dokumentumkönyvtár beállítása

Ebben a lépésben meghatározzuk annak a könyvtárnak az elérési útját, ahová a PDF dokumentumokat tárolni fogjuk.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Csere `"YOUR DOCUMENT DIRECTORY"` PDF-fájl mentési útvonalával. Ez azért kulcsfontosságú, mert megmondja a programnak, hogy hol keresse a bemeneti fájlokat, és hová mentse a kimenetet.

## 2. lépés: Töltse be a meglévő PDF dokumentumot

Ezután be kell töltenünk a PDF dokumentumot, amellyel dolgozni fogunk. Ezt a következővel tehetjük meg: `FormEditor` osztály.

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

Itt létrehozunk egy példányt a következőből: `FormEditor` és kösd össze egy meglévő, úgynevezett PDF fájllal `input.pdf`Győződjön meg róla, hogy a fájl létezik a megadott könyvtárban.

## 3. lépés: A választógomb tulajdonságainak konfigurálása

Most állítsunk be néhány tulajdonságot a választógombjainkhoz. Ez magában foglalja a gombok közötti távolságot, azok tájolását és méretét.

```csharp
formEditor.RadioGap = 4; // Rádiógomb opciók közötti távolság
formEditor.RadioHoriz = true; // Vízszintes igazításhoz igazra állítva
formEditor.RadioButtonItemSize = 20; // A rádiógomb mérete
formEditor.Facade.BorderWidth = 1; // Szegély szélessége
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // Szegély színe
```

Ezek a tulajdonságok segítenek meghatározni, hogyan jelenjenek meg a választógombok a PDF-ben. `RadioGap` tulajdonság a gombok közötti távolságot szabályozza, míg a `RadioHoriz` meghatározza azok elrendezését.

## 4. lépés: Vízszintes választógombok hozzáadása

Most adjuk hozzá a vízszintes választógombokat a PDF-hez.

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

Ebben a kódban definiáljuk a rádiógombok elemeit, és hozzáadjuk azokat a PDF-hez. `AddField` A metódus számos paramétert fogad el, beleértve a mező típusát, a mező nevét és az elhelyezés koordinátáit.

## 5. lépés: Függőleges választógombok hozzáadása

Ezután hozzáadjuk a függőleges választógombokat. Ehhez vissza kell állítanunk a tájolást függőlegesre.

```csharp
formEditor.RadioHoriz = false; // Függőleges igazításhoz állítsa hamisra
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

A korábbiakhoz hasonlóan definiáljuk az elemeket és hozzáadjuk őket a PDF-hez, de ezúttal függőlegesen lesznek igazítva.

## 6. lépés: Mentse el a PDF dokumentumot

Végül el kell mentenünk a módosított PDF dokumentumot.

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

Ez a kód az újonnan hozzáadott választógombokkal menti el a PDF-et. Ügyeljen arra, hogy ellenőrizze a kimeneti fájl megadott könyvtárát.

## Következtetés

Rádiógombok létrehozása PDF-ben az Aspose.PDF for .NET használatával egy egyszerű folyamat. Az ebben az oktatóanyagban ismertetett lépéseket követve könnyedén hozzáadhat vízszintesen és függőlegesen is igazított rádiógombokat a PDF űrlapokhoz. Ez nemcsak a dokumentumok interaktivitását fokozza, hanem az általános felhasználói élményt is javítja. Tehát próbálja ki!

## GYIK

### Mi az Aspose.PDF .NET-hez?
Az Aspose.PDF for .NET egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára, hogy programozottan hozzanak létre, szerkesszenek és konvertáljanak PDF dokumentumokat.

### Ingyenesen használhatom az Aspose.PDF fájlt?
Igen, az Aspose ingyenes próbaverziót kínál, amellyel kiértékelheted a könyvtárat. Letöltheted. [itt](https://releases.aspose.com/).

### Hogyan kaphatok támogatást az Aspose.PDF fájlhoz?
Támogatást kaphatsz, ha ellátogatsz a következő oldalra: [Aspose fórum](https://forum.aspose.com/c/pdf/10).

### Lehetséges más űrlapelemeket létrehozni az Aspose.PDF segítségével?
Abszolút! Az Aspose.PDF különféle űrlapelemeket támogat, beleértve a szövegmezőket, jelölőnégyzeteket és legördülő menüket.

### Hol tudom megvásárolni az Aspose.PDF for .NET fájlt?
Az Aspose.PDF for .NET fájlt megvásárolhatod a következő címen: [vásárlási oldal](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}