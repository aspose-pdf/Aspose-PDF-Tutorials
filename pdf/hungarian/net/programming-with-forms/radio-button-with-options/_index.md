---
"description": "Az interaktív PDF-ekben rejlő lehetőségeket az Aspose.PDF for .NET segítségével választógombok hozzáadásával szabadíthatja fel. Hozzon létre lebilincselő űrlapokat könnyedén, és javítsa a felhasználói élményt."
"linktitle": "Választható választógomb"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Választható választógomb"
"url": "/hu/net/programming-with-forms/radio-button-with-options/"
"weight": 230
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Választható választógomb

## Bevezetés

Az interaktív PDF dokumentumok létrehozása jelentősen növelheti a felhasználói elköteleződést és egyszerűsítheti az adatgyűjtést. A beilleszthető különféle elemek közül a választógombok kiemelkednek, mint felhasználóbarát módszer a feleletválasztós lehetőségek megjelenítésére. Az Aspose.PDF for .NET segítségével könnyedén hozzáadhat választógombokat a PDF űrlapokhoz, megkönnyítve a felhasználók számára a beállítások kiválasztását. Akár felméréseken, visszajelzési űrlapokon vagy alkalmazásokon dolgozik, ez az útmutató segít kihasználni az Aspose.PDF erejét a választógombok hatékony megvalósításához.

## Előfeltételek

Mielőtt belekezdenénk, van néhány dolog, amit be kell állítanod a zökkenőmentes folyamat érdekében, miközben létrehozzuk a választógombokkal ellátott PDF-ünket:

1. Aspose.PDF .NET-hez: Győződjön meg róla, hogy az Aspose.PDF könyvtár telepítve van a projektjében. Ha még nem telepítette, könnyen letöltheti innen: [kiadási oldal](https://releases.aspose.com/pdf/net/).
2. .NET keretrendszer: A .NET keretrendszer alapvető ismerete segít eligazodni a felmerülő problémákban.
3. Fejlesztői környezet: Szükséged lesz egy megfelelő .NET IDE-re (például Visual Studio), ahol megírhatod és tesztelheted a kódodat.
4. C# ismeretek: Bár nem kell profinak lenned, a C# programozásban való jártasság mindenképpen megkönnyíti és élvezetesebbé teszi ezt a folyamatot.
5. A PDF-fájlok szerkezetének alapvető ismerete: A PDF-fájlok szerkezetének ismerete segíthet a hibaelhárításban vagy az űrlapok további testreszabásában.

Ha mindezzel megvagy, szabadjára engedheted kreativitásodat a PDF-ek világában!

## Csomagok importálása

Ahhoz, hogy elkezdhesd használni a rádiógombokat az Aspose.PDF fájlban, először importálnod kell a szükséges csomagokat a C# projektedbe. Így csináld:

### Nyisd meg a kódszerkesztődet

Nyisd meg a fejlesztői környezetedet (például a Visual Studio-t), és hozz létre egy új C# projektet, ha még nem tetted meg. 

### Adja hozzá az Aspose.PDF referenciát

Kattintson jobb gombbal a projektjére a Megoldáskezelőben, válassza a Hozzáadás > Referencia lehetőséget, és az Összeállítások részben keresse meg az Aspose.PDF fájlt. Ha helyesen telepítette a könyvtárat, akkor meg kell jelennie a listában. Csak pipálja ki, és kattintson az OK gombra.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Most a projekted készen áll arra, hogy kihasználd az Aspose erejét!

Miután minden beállítottunk, hozzunk létre egy PDF dokumentumot, tele választógombokkal lépésről lépésre!

## 1. lépés: A dokumentum beállítása

Először is hozzunk létre egy új PDF dokumentumot, és adjunk hozzá egy oldalt. Ez lesz a vászon, ahová a választógomb beállításait fogjuk festeni.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document();
Page page = doc.Pages.Add();
```

Ebben a részletben egy újat hozunk létre `Document` objektum és egy `Page` a tartalmunkért. Ügyeljen arra, hogy kicserélje `YOUR DOCUMENT DIRECTORY` azzal az elérési úttal, ahová menteni szeretné a PDF-et.

## 2. lépés: Elrendezési táblázat létrehozása

Ezután szükségünk van egy elrendezésre a rádiógombjainkhoz. Egy táblázat használata megkönnyíti a szép elhelyezésüket.

```csharp
Aspose.Pdf.Table table = new Aspose.Pdf.Table();
table.ColumnWidths = "120 120 120"; // Az oszlopszélességek meghatározása
page.Paragraphs.Add(table);
```

Itt hoztunk létre egy `Table` objektumot, és megadtuk a három oszlop szélességét. Ez egy rendezett elrendezést hoz létre a lehetőségeink számára.

## 3. lépés: Sorok hozzáadása a táblázathoz

Most hozzáadunk egy sort a táblázatunkhoz és a cellákat, amelyek a választógombokat fogják tartalmazni.

```csharp
Row r1 = table.Rows.Add();
Cell c1 = r1.Cells.Add();
Cell c2 = r1.Cells.Add();
Cell c3 = r1.Cells.Add();
```

Létrehozunk egy új sort és három cellát a sorban. Minden cellában egy választógomb opció lesz.

## 4. lépés: Választógomb mező hozzáadása

Itt kezdődik a móka – adjuk hozzá a választógomb mezőt a PDF-ünkhöz!

```csharp
RadioButtonField rf = new RadioButtonField(page);
rf.PartialName = "radio";
doc.Form.Add(rf, 1);
```

Példányt hozunk létre egy `RadioButtonField`, adja meg a nevét, majd adja hozzá a dokumentuműrlaphoz. Ez a mező lehetővé teszi a felhasználók számára a kiválasztást.

## 5. lépés: A rádiógombok beállításainak konfigurálása

Ideje létrehozni a választógombok beállításait! Három lehetőséget adunk hozzá, amelyek közül a felhasználók választhatnak.

```csharp
RadioButtonOptionField opt1 = new RadioButtonOptionField();
RadioButtonOptionField opt2 = new RadioButtonOptionField();
RadioButtonOptionField opt3 = new RadioButtonOptionField();
opt1.OptionName = "Item1";
opt2.OptionName = "Item2";
opt3.OptionName = "Item3";
```

Itt hármat hozunk létre `RadioButtonOptionField` példányokat minden választási lehetőségünkhöz, és neveket rendelünk hozzájuk. Ha kreatívan bánunk ezekkel a nevekkel, jobban eligazíthatjuk a felhasználókat a választásban.

## 6. lépés: Opciók méreteinek beállítása

Következő lépésként állítsuk be a választógombok méretét, hogy vizuálisan vonzóak legyenek.

```csharp
opt1.Width = 15;
opt1.Height = 15;
opt2.Width = 15;
opt2.Height = 15;
opt3.Width = 15;
opt3.Height = 15;
```

Ezzel a kóddal definiáljuk az egyes választógombok méreteit. Ezeket az értékeket módosíthatod, ha nagyobb vagy kisebb opciókat szeretnél.

## 7. lépés: Opciók hozzáadása a választógomb mezőhöz

Most, hogy a beállítások létrejöttek, hozzá kell adnunk őket a választógomb mezőhöz.

```csharp
rf.Add(opt1);
rf.Add(opt2);
rf.Add(opt3);
```

Ez a kód nemcsak hozzáadja a lehetőségeket, hanem összekapcsolja azokat a választógomb mezőnkkel is, lehetővé téve a felhasználók számára, hogy kiválasszák az egyik lehetőséget.

## 8. lépés: A beállítások stílusának meghatározása

Hogy a lehetőségeink kiemelkedjenek, formázzuk meg őket. Hozzáadhatunk szegélyeket és beállíthatunk színeket.

```csharp
opt1.Border = new Border(opt1);
opt1.Border.Width = 1;
opt1.Border.Style = BorderStyle.Solid;
opt1.Characteristics.Border = System.Drawing.Color.Black;
opt1.DefaultAppearance.TextColor = System.Drawing.Color.Red;
opt1.Caption = new TextFragment("Item1");
```

Ismételje meg ezt a formázást a következőhöz: `opt2` és `opt3`, ennek megfelelően módosítva a feliratokat. Ez biztosítja, hogy minden lehetőség professzionális és lebilincselő legyen.

## 9. lépés: Opciók hozzáadása cellákhoz

Ezután el kell helyeznünk ezeket a rádiógombokat a táblázatunk megfelelő celláiba.

```csharp
c1.Paragraphs.Add(opt1);
c2.Paragraphs.Add(opt2);
c3.Paragraphs.Add(opt3);
```

Ez a sor hozzáadja a korábban létrehozott cellákhoz a formázott beállításokat, szépen rendszerezve azokat a táblázatban.

## 10. lépés: Mentse el a PDF dokumentumot

Végre itt az ideje menteni a munkádat! Ez a lépés mindent PDF fájlba ment el, amit eddig csináltunk.

```csharp
dataDir = dataDir + "RadioButtonWithOptions_out.pdf";
// PDF fájl mentése
doc.Save(dataDir);
Console.WriteLine("\nRadio button field with three options added successfully.\nFile saved at " + dataDir);
```

Ezzel a kóddal a dokumentum a megadott könyvtárba kerül mentésre. Most megnyithatja ezt a PDF fájlt, hogy működés közben lássa a választógombokat. Gratulálunk első interaktív PDF-je megvalósításához!

## Következtetés

Az interaktív elemek, például a választógombok létrehozásának elsajátítása az Aspose.PDF for .NET segítségével teljesen új lehetőségeket nyit meg PDF-dokumentumai számára. Az útmutató követésével mostantól képes lesz arra, hogy könnyedén beépítsen választógombokat projektjeibe, javítva a felhasználói élményt és az adatgyűjtési folyamatokat. Akár egy egyszerű felmérésről, akár egy összetett űrlapról van szó, a személyre szabott interaktív PDF-ek létrehozásának lehetősége egy kézben van.

## GYIK

### Mi az Aspose.PDF .NET-hez?
Az Aspose.PDF for .NET egy olyan könyvtár, amely lehetővé teszi a fejlesztők számára PDF dokumentumok programozott létrehozását és kezelését.

### Hogyan telepíthetem az Aspose.PDF for .NET fájlt?
A könyvtárat letöltheted innen: [Aspose kiadási oldal](https://releases.aspose.com/pdf/net/) és add hozzá a projektedhez.

### Létrehozhatok választógombokat PDF fájlokban más programozási nyelvekkel?
Igen, az Aspose.PDF Java és más nyelveken is elérhető hasonló funkciókkal.

### Van ingyenes próbaverzió az Aspose.PDF-hez?
Igen, az Aspose.PDF funkcióit letöltheti a következőből: [ingyenes próbaverzió](https://releases.aspose.com/).

### Hol kaphatok támogatást az Aspose.PDF-hez?
Támogatásért látogassa meg a következőt: [Aspose támogatói fórum](https://forum.aspose.com/c/pdf/10) szakértők és a közösség tagjainak segítségét kérni.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}