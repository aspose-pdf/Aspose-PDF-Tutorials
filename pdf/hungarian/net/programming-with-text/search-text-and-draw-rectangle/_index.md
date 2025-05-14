---
"description": "Tanuld meg, hogyan kereshetsz szöveget PDF-ekben, és hogyan jelölheted ki téglalapokkal az Aspose.PDF for .NET segítségével! Egyszerű, lépésről lépésre bemutató a PDF-szerkesztési készségek fejlesztéséhez."
"linktitle": "Szöveg keresése és téglalap rajzolása"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Szöveg keresése és téglalap rajzolása"
"url": "/hu/net/programming-with-text/search-text-and-draw-rectangle/"
"weight": 460
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg keresése és téglalap rajzolása

## Bevezetés

Szeretnéd fejleszteni PDF-szerkesztési készségeidet? Szeretnéd megtanulni, hogyan kereshetsz adott szöveget PDF fájlokban, és hogyan jelölheted ki azt egy téglalappal? Megtaláltad a tökéletes útmutatót! Ma bemutatom, hogyan használhatod az Aspose.PDF for .NET-et szöveg keresésére egy PDF dokumentumban, és hogyan rajzolhatsz téglalapokat köré. Ez a cikk egy lépésről lépésre szóló útmutatót tartalmaz, amelyet az érthetőség és a hasznosság szem előtt tartásával terveztek, biztosítva, hogy követni tudd és alkalmazni ezeket a technikákat a projektjeidben. 

## Előfeltételek

Mielőtt belevágnánk az oktatóanyagba, készítsük elő, amire szükségünk van a zökkenőmentes munkafolyamat biztosításához:

1. A .NET alapjai: Ahhoz, hogy hatékonyan követni tudd ezt az oktatóanyagot, ismerned kell a C# programozást és a .NET keretrendszert.
   
2. Visual Studio telepítve: Szükséged lesz egy integrált fejlesztői környezetre (IDE) a kódod írásához és teszteléséhez. A Visual Studio Community egy nagyszerű lehetőség, és ingyenes.
   
3. Aspose.PDF .NET-hez: A projektedben telepíteni kell az Aspose.PDF könyvtárat. Letöltheted [itt](https://releases.aspose.com/pdf/net/) vagy fontoljon meg egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) kibővített funkciókhoz.
   
4. Minta PDF dokumentum: Ehhez az oktatóanyaghoz szüksége lesz egy minta PDF fájlra, amelynek neve `SearchAndGetTextFromAll.pdf` a projektkönyvtárában tárolva. 

## Csomagok importálása

A kezdéshez először importálnia kell a szükséges csomagokat a .NET projektjébe. Kövesse az alábbi lépéseket:

### Nyissa meg a Visual Studio-t

Indítsa el a Visual Studio programot, és hozzon létre egy új konzolalkalmazást, vagy használjon egy meglévőt, amelybe a PDF-funkciókat szeretné megvalósítani.

### Aspose.PDF hozzáadása a projekthez

1. Kattintson jobb gombbal a projektjére a Megoldáskezelőben.
2. Válassza a „NuGet-csomagok kezelése” lehetőséget.
3. Keresés `Aspose.PDF` és telepítsd a legújabb verziót.

Ezzel megteremted az alapot az összes lenyűgöző PDF-manipulációhoz, amit most végrehajtasz.

## Névterek importálása

programfájl tetején importáld a releváns névtereket az Aspose könyvtárból:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Facades;
```

Ez megkönnyíti az Aspose.PDF könyvtáron belüli osztályok és metódusok elérését a feladatokhoz.


Most, hogy minden elő van készítve, bontsuk le kezelhető lépésekre a PDF-ben való szövegkeresés és a köré rajzolt téglalap folyamatát.

## 1. lépés: Állítsa be a dokumentum elérési útját

Először is, állítsd be a PDF fájl elérési útját. Ügyelj arra, hogy kicseréld `YOUR DOCUMENT DIRECTORY` a tényleges útvonallal, ahol a `SearchAndGetTextFromAll.pdf` tárolva van.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## 2. lépés: Nyissa meg a PDF dokumentumot

Ezután hozzon létre egy példányt a `Document` osztály a PDF betöltéséhez:

```csharp
Document document = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

Ez a kódsor megnyitja a megadott PDF fájlt, lehetővé téve a további módosításokat.

## 3. lépés: Hozz létre egy szövegelnyelőt

Most szükséged lesz egy módszerre, amellyel szöveget kereshetsz a dokumentumban. Ehhez a következőt használjuk: `TextFragmentAbsorber`:

```csharp
TextFragmentAbsorber textAbsorber = new TextFragmentAbsorber(@"[\S]+");
```

A reguláris kifejezés `@"[\S]+"` úgy van kialakítva, hogy a PDF-ben található bármely nem szóköz karakterlánchoz illeszkedjen. 

## 4. lépés: Szöveges keresési beállítások konfigurálása

Ezután be kell állítania a szöveges keresési beállításokat:

```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textAbsorber.TextSearchOptions = textSearchOptions;
```

Itt a `true` paraméter azt jelenti, hogy a keresés megkülönbözteti a kis- és nagybetűket. Beállíthatja erre: `false` ha kis- és nagybetűket megkülönböztető keresést szeretne.

## 5. lépés: Fogadja el a szövegelnyelőt a dokumentumban

A tiéddel `TextFragmentAbsorber` és a keresési lehetőségek készen állnak, itt az ideje, hogy szöveget kinyerjünk a dokumentumból:

```csharp
document.Pages.Accept(textAbsorber);
```

Ez a módszer a PDF minden egyes oldalát megvizsgálja, hogy a megadott mintának megfelelő szövegrészeket találjon.

## 6. lépés: PDFContentEditor létrehozása

Alakzatok rajzolásához a dokumentumban szüksége lesz a következőkre: `PdfContentEditor`:

```csharp
var editor = new PdfContentEditor(document);
```

Ez a szerkesztő lehetővé teszi a PDF-tartalom egyszerű kezelését és szerkesztését.

## 7. lépés: Keresse végig a talált szövegrészeket

Most végig kell menned a megtalált szövegrészeken, hogy téglalapokat rajzolhass köréjük:

```csharp
foreach (TextFragment textFragment in textAbsorber.TextFragments)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        DrawBox(editor, textFragment.Page.Number, textSegment, System.Drawing.Color.Red);
    }
}
```

Ez a ciklus végigmegy minden szövegrészen és azok szegmensein, meghívva egy `DrawBox` Téglalap rajzolásának módszere.

## 8. lépés: A DrawBox metódus definiálása

Meg kell határoznod a `DrawBox` metódus, amely a téglalap rajzolási logikáját fogja kezelni. Íme egy egyszerű megvalósítás:

```csharp
private static void DrawBox(PdfContentEditor editor, int pageNumber, TextSegment textSegment, System.Drawing.Color color)
{
    // Számítsa ki a téglalap méreteit a szövegszegmens alapján
    float x = textSegment.Rectangle.LLX;
    float y = textSegment.Rectangle.LLY;
    float width = textSegment.Rectangle.Width;
    float height = textSegment.Rectangle.Height;

    // Rajzolj egy téglalapot a kiszámított értékek felhasználásával
    editor.DrawRectangle(pageNumber, x, y, width, height, color, 1);
}
```

Ez a metódus a téglalap pozícióját és méretét a szegmenst határoló téglalap alapján határozza meg, és a szerkesztőt használja a megrajzolásához.

## 9. lépés: Mentse el a módosított dokumentumot

Miután megrajzolta a téglalapokat a talált szöveg köré, mentheti a módosított dokumentumot:

```csharp
dataDir = dataDir + "SearchTextAndDrawRectangle_out.pdf";
document.Save(dataDir);
```

Győződjön meg róla, hogy az új fájlt egyedi névvel menti, hogy elkerülje az eredeti dokumentum felülírását.

## 10. lépés: Megerősítő üzenet

Végül írjon ki egy megerősítő üzenetet a konzolra, amely jelzi a művelet sikerességét:

```csharp
Console.WriteLine("\nRectangle drawn successfully on searched text.\nFile saved at " + dataDir);
```

És íme! Sikeresen létrehoztál egy szkriptet, amely szöveget keres egy PDF-ben, és téglalapokkal jelöli ki azt.

## Következtetés

Gratulálunk! Most egy hatékony készségre tettél szert, amely nagymértékben fejlesztheti PDF-szerkesztési képességeidet az Aspose.PDF for .NET használatával. Néhány egyszerű lépéssel megkeresheted a dokumentumodban található szöveget, és vizuálisan kiemelheted, így PDF-dokumentumaid interaktívabbak és kezelhetőbbek lesznek. Ne habozz kísérletezni a különböző reguláris kifejezésmintákkal és színbeállításokkal, hogy igazán a sajátoddá tedd ezt az eszközt!

## GYIK

### Mi az Aspose.PDF .NET-hez?
Az Aspose.PDF for .NET egy átfogó módszert kínál PDF dokumentumok programozott létrehozására, kezelésére és konvertálására.

### Ingyenesen használhatom az Aspose.PDF fájlt?
Igen, az Aspose ingyenes próbaverziót kínál, amellyel tesztelheti a könyvtár funkcióit. Nézze meg. [itt](https://releases.aspose.com/).

### Milyen programozási nyelvet kell használnom az Aspose.PDF for .NET fájllal?
Az Aspose.PDF for .NET fájlt C# és más .NET nyelvekkel való használatra tervezték.

### Hogyan kaphatok segítséget az Aspose.PDF fájllal kapcsolatban?
Bármilyen problémával vagy kérdéssel kapcsolatban felkeresheted az Aspose támogatási fórumát. [itt](https://forum.aspose.com/c/pdf/10).

### Honnan tudom letölteni az Aspose.PDF fájlt .NET-hez?
A könyvtárat letöltheted az Aspose weboldaláról, [itt](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}