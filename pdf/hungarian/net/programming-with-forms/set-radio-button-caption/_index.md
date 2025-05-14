---
"description": "Ismerje meg, hogyan állíthat be választógomb-feliratokat PDF-fájlokban az Aspose.PDF for .NET használatával. Ez a lépésről lépésre szóló útmutató végigvezeti Önt a PDF-űrlapok betöltésén, módosításán és mentésén."
"linktitle": "Rádiógomb feliratának beállítása"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Rádiógomb feliratának beállítása"
"url": "/hu/net/programming-with-forms/set-radio-button-caption/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rádiógomb feliratának beállítása

## Bevezetés

Ha az Aspose.PDF for .NET segítségével merülsz el a PDF-manipuláció világában, igazi élményben lesz részed! Ma egy praktikus funkcióra összpontosítunk: a választógombok feliratainak beállítására a PDF űrlapokon. A választógombok elengedhetetlenek a felhasználói űrlapokon, ahol egy sor lehetőség közül kell választani. Képzeld el őket feleletválasztós kérdésekként, ahol csak egy válasz megengedett. Ez az oktatóanyag végigvezet a választógombok feliratainak frissítésének folyamatán egy PDF űrlapon, hogy dokumentumaid interaktívak és felhasználóbarátak is legyenek. 

## Előfeltételek

Mielőtt belemerülnél a kódba, van néhány dolog, amiről meg kell győződnöd:

1. Aspose.PDF .NET-hez: Győződjön meg róla, hogy telepítve van az Aspose.PDF könyvtár. Ez a könyvtár segít a PDF fájlok programozott kezelésében.
2. Fejlesztői környezet: Rendelkeznie kell egy beállított .NET fejlesztői környezettel, például a Visual Studio-val.
3. Minta PDF űrlap: Ehhez az oktatóanyaghoz szükséged lesz egy minta PDF űrlapra választógombokkal. Használhatsz bármilyen meglévő PDF űrlapot, vagy létrehozhatsz egy újat választógombokkal.
4. C# alapismeretek: Ez az útmutató feltételezi, hogy rendelkezel a C# és a .NET programozási alapismeretekkel.

Ha még nem telepítette az Aspose.PDF for .NET fájlt, vagy ideiglenes licencre van szüksége, akkor megteheti [töltsd le itt](https://releases.aspose.com/pdf/net/) vagy [szerezz ideiglenes jogosítványt](https://purchase.aspose.com/temporary-license/).

## Csomagok importálása

A kezdéshez importálnod kell a szükséges csomagokat a C# projektedbe. Így illesztheted be az Aspose.PDF könyvtárat:

```csharp
using System;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
using Aspose.Pdf.Text;
```

Győződjön meg róla, hogy ezeket a csomagokat hozzáadta a projekthez a NuGet vagy az Ön által preferált módszer segítségével.

## 1. lépés: Töltse be a PDF űrlapot

Először is be kell töltenie a választógombokat tartalmazó PDF űrlapot. `Aspose.Pdf.Facades.Form` osztályt használjuk erre a célra. Így csináld:

```csharp
// Adja meg a dokumentumkönyvtár elérési útját
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Töltse be a forrás PDF űrlapot
Aspose.Pdf.Facades.Form form1 = new Aspose.Pdf.Facades.Form(dataDir + "RadioButtonField.pdf");
Document PDF_Template_PDF_HTML = new Document(dataDir + "RadioButtonField.pdf");
```

Ebben a kódrészletben:
- `dataDir` megadja a PDF fájl elérési útját.
- `Form` Az osztály a PDF űrlapmezők használatával működik.
- `Document` Az osztály hozzáférést biztosít a PDF dokumentum oldalaihoz.

## 2. lépés: Ismételje át a választógomb mezőit

Ezután végig kell haladnia az űrlap mezőin a választógomb mezőinek azonosításához és kezeléséhez:

```csharp
foreach (var item in form1.FieldNames)
{
    Console.WriteLine(item.ToString());
    Dictionary<string, string> radioOptions = form1.GetButtonOptionValues(item);
```

Ebben a ciklusban:
- `FieldNames` listát ad a PDF-ben található összes mező nevéről.
- `GetButtonOptionValues(item)` lekéri az egyes választógombokhoz elérhető opciókat.

## 3. lépés: A rádiógomb beállításainak módosítása

Miután azonosította a választógomb mezőit, módosíthatja azok beállításait. Ehhez a mezőt a következőre kell konvertálni: `RadioButtonField` és frissítse a beállításait:

```csharp
    if (item.Contains("radio1"))
    {
        Aspose.Pdf.Forms.RadioButtonField field0 = PDF_Template_PDF_HTML.Form[item] as Aspose.Pdf.Forms.RadioButtonField;
        Aspose.Pdf.Forms.RadioButtonOptionField fieldoption = new Aspose.Pdf.Forms.RadioButtonOptionField();
        fieldoption.OptionName = "Yes";
        fieldoption.PartialName = "Yesname";
```

Itt:
- Ellenőrizzük, hogy a mező neve tartalmazza-e a „radio1” karakterláncot, hogy azonosítsuk a módosítani kívánt választógomb mezőt.
- `RadioButtonField` az űrlapmezőkből konvertálódik a kívánt módosítások végrehajtásához.

## 4. lépés: Állítsa be a választógomb feliratát

A választógomb feliratának beállításához vagy frissítéséhez létre kell hoznia egy `TextFragment` és használja `TextBuilder` a kívánt helyre helyezéséhez:

```csharp
        var updatedFragment = new Aspose.Pdf.Text.TextFragment("test123");
        updatedFragment.TextState.Font = FontRepository.FindFont("Arial");
        updatedFragment.TextState.FontSize = 10;
        updatedFragment.TextState.LineSpacing = 6.32f;

        // TextParagraph objektum létrehozása
        TextParagraph par = new TextParagraph();
        // Bekezdés pozíciójának beállítása
        par.Position = new Position(field0.Rect.LLX, field0.Rect.LLY + updatedFragment.TextState.FontSize);
        // Sortörési mód megadása
        par.FormattingOptions.WrapMode = TextFormattingOptions.WordWrapMode.ByWords;
        // Új szövegtöredék hozzáadása a bekezdéshez
        par.AppendLine(updatedFragment);
        // TextParagraph hozzáadása a TextBuilder segítségével
        TextBuilder textBuilder = new TextBuilder(PDF_Template_PDF_HTML.Pages[1]);
        textBuilder.AppendParagraph(par);
```

Ebben a részben:
- `TextFragment` a szöveg és annak megjelenésének meghatározására szolgál.
- `TextParagraph` segít a szöveg pozicionálásában és formázásában.
- `TextBuilder` hozzáadja a szöveget a PDF megadott oldalához.

## 5. lépés: Mentse el a frissített PDF-et

Végül mentse el a frissített PDF-et egy új fájlba:

```csharp
        field0.DeleteOption("item1");
    }
}
PDF_Template_PDF_HTML.Save(dataDir + "RadioButtonField_out.pdf");
```

Ez biztosítja, hogy:
- A módosítások érvénybe lépnek a PDF fájlban.
- Az eredeti választógomb opció a megadottak szerint eltávolításra kerül.

## Következtetés

PDF űrlapokon található választógomb-feliratok módosítása az Aspose.PDF for .NET segítségével jelentősen javíthatja dokumentumai interaktivitását és használhatóságát. Az ebben az oktatóanyagban ismertetett lépésekkel könnyedén betölthet egy PDF-et, frissítheti a választógomb-beállításokat, és mentheti a módosításokat. Ez a megközelítés hasznos az űrlapkezeléshez, és biztosítja, hogy PDF-jei pontosan megfeleljenek a felhasználók igényeinek. Merüljön el az Aspose.PDF-ben, és fedezze fel a képességeit további PDF-manipulációkhoz!

## GYIK

### Frissíthetek egyszerre több választógomb mezőt?
Igen, végigmehetsz az összes választógomb mezőn, és szükség szerint alkalmazhatod a módosításokat.

### Szükségem van licencre az Aspose.PDF használatához?
Ingyenes próbaverzióval kezdheted, de a hosszabb használathoz licenc szükséges. [Szerezz jogosítványt itt](https://purchase.aspose.com/buy).

### Hogyan tesztelhetem a módosításokat a PDF mentése előtt?
A PDF-et megtekintheti a fejlesztői környezetében, vagy PDF-megjelenítővel ellenőrizheti a módosításokat.

### Az Aspose.PDF kompatibilis a .NET összes verziójával?
Az Aspose.PDF a .NET számos verzióját támogatja. Ellenőrizze a kompatibilitást az Ön által használt .NET verzióval.

### Hasonlóképpen tudok más űrlapmezőket is kezelni?
Igen, hasonló technikák alkalmazhatók más típusú űrlapmezőkre is PDF dokumentumokban.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}