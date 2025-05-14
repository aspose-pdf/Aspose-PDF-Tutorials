---
"description": "Tanuld meg, hogyan hozhatsz létre csoportosított jelölőnégyzeteket (választógombokat) egy PDF dokumentumban az Aspose.PDF for .NET használatával ebből a lépésről lépésre szóló útmutatóból."
"linktitle": "Csoportosított jelölőnégyzetek PDF dokumentumban"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Csoportosított jelölőnégyzetek PDF dokumentumban"
"url": "/hu/net/programming-with-forms/grouped-check-boxes/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Csoportosított jelölőnégyzetek PDF dokumentumban

## Bevezetés

Interaktív PDF-ek létrehozása nem olyan nehéz, mint amilyennek hangzik, különösen akkor, ha olyan hatékony eszközök állnak rendelkezésedre, mint az Aspose.PDF for .NET. Az egyik interaktív elem, amelyet esetleg hozzá kell adnod a PDF-dokumentumaidhoz, a csoportosított jelölőnégyzetek, vagy pontosabban a választógombok, amelyek lehetővé teszik a felhasználók számára, hogy egy lehetőséget válasszanak ki egy készletből. Ez az oktatóanyag végigvezet a csoportosított jelölőnégyzetek (választógombok) PDF-dokumentumhoz való hozzáadásának folyamatán az Aspose.PDF for .NET használatával. Akár kezdő, akár tapasztalt fejlesztő vagy, ezt az útmutatót lebilincselőnek, részletesnek és könnyen követhetőnek találod.

## Előfeltételek

Mielőtt belemerülnénk a lépésről lépésre szóló útmutatóba, nézzük meg néhány lényeges előfeltételt:

1. Aspose.PDF .NET-hez: Győződjön meg róla, hogy telepítve van az Aspose.PDF könyvtár. Ha nem, akkor... [töltsd le itt](https://releases.aspose.com/pdf/net/).
2. IDE: Be kell állítania egy fejlesztői környezetet, például a Visual Studio-t.
3. .NET-keretrendszer: A projektnek a .NET-keretrendszer Aspose.PDF-fel kompatibilis verzióját kell céloznia.
4. C# alapismeretek: A C# és a PDF-manipuláció ismerete szükséges a zökkenőmentes haladáshoz.
5. Licenc: Az Aspose.PDF fájl teljes funkcionalitásához licenc szükséges. [szerezzen ideiglenes jogosítványt](https://purchase.aspose.com/temporary-license/) ha szükséges.

## Csomagok importálása

Kezdés előtt győződjön meg arról, hogy importálta a szükséges névtereket a projektbe:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

Ezek a csomagok hozzáférést biztosítanak a PDF dokumentumok kezeléséhez szükséges összes osztályhoz és metódushoz, beleértve a választógombok létrehozását és tulajdonságaik definiálását.

Ebben a részben a csoportosított jelölőnégyzetek (választógombok) létrehozásának folyamatát bontjuk le világos, könnyen követhető lépésekre.

## 1. lépés: Új PDF dokumentum létrehozása

Az első lépés egy példány létrehozása a `Document` objektum, amely a PDF-fájlt fogja képviselni. Ezután adjon hozzá egy üres oldalt a dokumentumhoz, ahová a csoportosított jelölőnégyzeteket fogja elhelyezni.

```csharp
// Dokumentum objektum példányosítása
Document pdfDocument = new Document();

// Oldal hozzáadása a PDF fájlhoz
Page page = pdfDocument.Pages.Add();
```

Ez megteremti az alapot bármilyen elem, például választógombok PDF-hez való hozzáadásához.

## 2. lépés: A rádiógomb mező inicializálása

Ezután létre kell hoznunk egy `RadioButtonField` objektum, amely a csoportosított jelölőnégyzeteket (választógombokat) fogja tartalmazni. Ez a mező hozzáadódik ahhoz az oldalhoz, ahol a jelölőnégyzetek megjelennek.

```csharp
// Hozza létre a RadioButtonField objektum példányát, és rendelje hozzá az első oldalhoz
RadioButtonField radio = new RadioButtonField(pdfDocument.Pages[1]);
```

Gondolj erre úgy, mint egy tárolóra, amely az egyes választógomb-opciókat csoportosítja.

## 3. lépés: Választógomb-beállítások hozzáadása

Most adjuk hozzá az egyes választógomb-beállításokat a mezőhöz. Ebben a példában két választógombot adunk hozzá, és a pozíciójukat a következővel adjuk meg: `Rectangle` objektum.

```csharp
// Adja hozzá az első választógomb opciót, és adja meg a pozícióját a Téglalap használatával
RadioButtonOptionField opt1 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(0, 0, 20, 20));
RadioButtonOptionField opt2 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(100, 0, 120, 20));

// Beállításnevek beállítása azonosításhoz
opt1.OptionName = "Option1";
opt2.OptionName = "Option2";
```

Itt a `Rectangle` Az objektum meghatározza az oldalon található egyes rádiógombok koordinátáit és méretét.

## 4. lépés: A rádiógombok stílusának testreszabása

A rádiógombok megjelenését testreszabhatja a hozzájuk tartozó beállításokkal. `Style` tulajdonság. Például négyzet alakú vagy kereszt alakú jelölőnégyzeteket szeretne.

```csharp
// A rádiógombok stílusának beállítása
opt1.Style = BoxStyle.Square;
opt2.Style = BoxStyle.Cross;
```

Ez lehetővé teszi a jelölőnégyzetek megjelenésének és érzetének szabályozását, így felhasználóbarátabbá és vizuálisan vonzóbbá teheti azokat.

## 5. lépés: Szegélytulajdonságok konfigurálása

A szegélyek létfontosságú szerepet játszanak abban, hogy a jelölőnégyzetek könnyen azonosíthatók legyenek. Itt minden egyes választógomb opció köré tömör szegélyt adunk, és meghatározzuk azok szélességét és színét.

```csharp
// Az első választógomb szegélyének konfigurálása
opt1.Border = new Border(opt1);
opt1.Border.Style = BorderStyle.Solid;
opt1.Border.Width = 1;
opt1.Characteristics.Border = Color.Black;

// A második választógomb szegélyének konfigurálása
opt2.Border = new Border(opt2);
opt2.Border.Style = BorderStyle.Solid;
opt2.Border.Width = 1;
opt2.Characteristics.Border = Color.Black;
```

Ez a lépés biztosítja, hogy minden választógombnak jól definiált szegélye legyen, javítva a dokumentum olvashatóságát.

## 6. lépés: Választógomb-beállítások hozzáadása az űrlaphoz

Most hozzáadjuk a választógombokat a dokumentum űrlapjához. Ez az utolsó lépés a jelölőnégyzetek egyetlen mező alá csoportosításában.

```csharp
// Választógomb mező hozzáadása a dokumentum űrlapobjektumához
pdfDocument.Form.Add(radio);
```

A form objektum tárolóként szolgál az összes interaktív elem számára, beleértve a csoportosított jelölőnégyzeteinket is.

## 7. lépés: Mentse el a PDF dokumentumot

Végül, miután minden beállított, elmentheti a PDF dokumentumot a kívánt helyre.

```csharp
// A kimeneti fájl elérési útjának meghatározása
string dataDir = "YOUR DOCUMENT DIRECTORY" + "GroupedCheckBoxes_out.pdf";

// PDF dokumentum mentése
pdfDocument.Save(dataDir);

// Sikeres létrehozás megerősítése
Console.WriteLine("Grouped checkboxes added successfully. File saved at " + dataDir);
```

És ennyi! Sikeresen létrehoztál egy csoportosított jelölőnégyzeteket tartalmazó PDF-et az Aspose.PDF for .NET használatával.

## Következtetés

Az interaktív elemek, például a csoportosított jelölőnégyzetek hozzáadása a PDF dokumentumokhoz elsőre bonyolultnak tűnhet, de az Aspose.PDF for .NET segítségével ez gyerekjáték lesz. Ezzel a lépésről lépésre haladó útmutatóval megtanultad, hogyan állíthatsz be egy alapvető PDF dokumentumot, hogyan adhatsz hozzá csoportosított választógombokat, hogyan szabhatod testre a megjelenésüket, és hogyan mentheted el a végeredményt. Akár űrlapokat, felméréseket vagy bármilyen más típusú interaktív PDF-et készítesz, ez az útmutató szilárd alapot nyújt a kezdéshez.

## GYIK

### Hozzáadhatok kettőnél több választógombot egy csoporthoz?
Teljesen! Egyszerűen hozzon létre további példányokat `RadioButtonOptionField` tárgyakat, és add hozzá őket a `RadioButtonField` ahogy az az oktatóanyagban látható.

### Hogyan kezelhetek több jelölőnégyzet-csoportot egy dokumentumban?
Több csoport létrehozásához külön példányokat kell létrehozni `RadioButtonField` tárgyak minden csoporthoz.

### Van-e korlátozás a hozzáadható jelölőnégyzetek számára?
Nem, az Aspose.PDF for .NET nem szab korlátozást a PDF-hez hozzáadható jelölőnégyzetek számára vonatkozóan.

### Módosíthatom a jelölőnégyzetek megjelenését a hozzáadása után?
Igen, a jelölőnégyzetek hozzáadása után módosíthatja a tulajdonságokat, például a szegély stílusát, szélességét és színét.

### Lehet képeket rádiógombként használni?
Igen, az Aspose.PDF lehetővé teszi egyéni képek választógombként való használatát a következő beállítással: `Appearance` az egyes rádiógomb-opciók tulajdonsága.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}