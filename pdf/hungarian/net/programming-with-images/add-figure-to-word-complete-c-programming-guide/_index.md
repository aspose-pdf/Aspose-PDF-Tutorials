---
category: general
date: 2026-04-12
description: Adj hozzá ábrát a Wordhöz gyorsan C#-val. Tanuld meg, hogyan helyezd
  el az ábrát a Wordben, hogyan illeszd be az ábrát a docx-be, és hogyan adj hozzá
  egyedi XML-t a fejlett elrendezéshez.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: hu
og_description: Adj hozzá ábrát a Wordhöz gyorsan C#-val. Tanuld meg, hogyan helyezd
  el az ábrát a Wordben, hogyan szúrj be ábrát a docx-be, és hogyan adj hozzá egyedi
  XML-t a fejlett elrendezéshez.
og_title: Ábra hozzáadása a Wordhöz – Teljes C# programozási útmutató
tags:
- C#
- Word Automation
- Document Generation
title: Ábra hozzáadása a Wordhöz – Teljes C# programozási útmutató
url: /hu/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ábra hozzáadása Word-hez – Teljes C# programozási útmutató

Valaha is szükséged volt **ábra hozzáadására Word-hez**, de nem tudtad, hol kezdjed? Nem vagy egyedül. Sok irodai automatizálási projektben hiányzik egy jól elhelyezett kép vagy diagram, amely egy egyedi XML részben él. Ez az útmutató pontosan megmutatja, hogyan **helyezd el az ábrát Word-ben**, hogyan szúrd be az ábrát egy *.docx* fájlba, és még az alatta lévő egyedi XML-t is finomhangold, hogy a forma úgy viselkedjen, mint bármely natív Word-objektum.

Egy valós példán keresztül mutatjuk be a GemBox.Document könyvtár használatát (kisebb fájlokhoz ingyenes, nagyobb munkaterhekhez kereskedelmi). A végére egy önálló, futtatható programod lesz, amely egy ábrát helyez el X = 50, Y = 200 koordinátákon egy címkézett‑tartalom konténerben. Nincs homályos „lásd a dokumentációt” megoldás – csak tiszta kód, a működés magyarázata, és tippek, amelyeket közvetlenül beilleszthetsz a saját projektedbe.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Core 3.1‑gyel is lefordítható)
- **GemBox.Document** NuGet csomag (`Install-Package GemBox.Document`)
- Egy kiinduló Word fájl (`input.docx`), amely már tartalmaz egy egyedi XML címkét, ahová az ábrát szeretnéd helyezni
- Alapvető C# ismeretek (látni fogod, miért fontos minden sor)

> **Pro tipp:** Ha nincs előre címkézett dokumentumod, létrehozhatsz egyet a Wordben úgy, hogy beszúrod a *Tartalomvezérlő* → *XML leképezési ablaktábla* → egy egyedi XML részt. A könyvtár ezt a vezérlőt `TaggedContent`‑ként kezeli.

## 1. lépés – A forrásdokumentum betöltése

Az első dolog, amit teszünk, hogy megnyitjuk a meglévő *.docx* fájlt. A `Document` a belépési pont minden GemBox művelethez.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Miért?* A fájl betöltése hozzáférést biztosít a belső részeihez, beleértve az egyedi XML konténereket is. Enélkül nem tudnánk megtalálni azt a `TaggedContent` csomópontot, amely az ábrát fogja tartalmazni.

## 2. lépés – A címkézett tartalom (egyedi XML konténer) elérése

Az egyedi XML egy *tartalomvezérlő* belsejében tárolódik a Wordben. A GemBox ezt `TaggedContent`‑ként teszi elérhetővé.

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Ha a dokumentumnak több címkézett szekciója van, a `TaggedContent` az **elsőt** adja vissza. A `doc.TaggedContents` segítségével felsorolhatod és kiválaszthatod a kívánt címkét név alapján.

## 3. lépés – Az ábraelem létrehozása

A `FigureElement` egy képet, diagramot vagy bármilyen vizuális objektumot képvisel, amelyet a Word *alakzatként* kezel. Ezt a címkézett konténerben hozunk létre.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Miért hozunk itt ábrát?* Az egyedi XML csomóponthoz csatolva a Word tudja, hogy az ábra ehhez a logikai szekcióhoz tartozik, ami későbbi szerkesztés vagy tartalomvezérlő‑alapú munkafolyamatok esetén kritikus.

## 4. lépés – Az ábra pontos elhelyezése

A Word pontokban (1 pt ≈ 1/72 in) pozicionál. A `PointF` struktúra egyszerűvé teszi az X/Y koordináták beállítását.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Hogyan helyezzük el a shape-et Word-ben:** A `Position` tulajdonság egy `PointF`‑et fogad, ahol az első érték a vízszintes eltolás (bal), a második a függőleges eltolás (felső), a lap margójához képest. Ezeket a számokat finomhangolhatod a pontos elhelyezéshez.

## 5. lépés – Az ábra beszúrása a címkézett tartalom fába

Most csatoljuk az ábrát az egyedi XML fa gyökéreleméhez. Ez fizikailag hozzáadja a formát a Word dokumentumhoz.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

Ekkor az ábra már a dokumentumban van, de még nincs képforrása. Adjunk hozzá egy egyszerű PNG‑t a lemezről.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## 6. lépés – A módosított dokumentum mentése

Végül visszaírjuk a változtatásokat egy új *.docx* fájlba.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Amikor megnyitod a `output.docx`‑et a Wordben, a kép pontosan a (50, 200) koordinátán belül jelenik meg a célzott egyedi‑XML blokkban.

### Teljes működő példa

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Várt eredmény:** A `output.docx` megnyitásakor a PNG pontosan ott lesz, ahol megadtad, beágyazva az egyedi XML részbe. Ha megnézed a dokumentum XML‑ét (`.docx` → kicsomagolás → `word/document.xml`), látható lesz egy `<w:pict>` elem a megfelelő `<v:shape>` koordinátákkal.

## Gyakori kérdések és speciális esetek

### Mi a teendő, ha a dokumentumnak több címkézett szekciója van?

Használd a `doc.TaggedContents`‑t a felsoroláshoz és válaszd ki a címkét név alapján:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Hogyan adhatunk feliratot az ábrához?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Működik ez a Word 2010‑el és újabb verziókkal?

Igen. A GemBox.Document az Open XML szabványra épül, amely kompatibilis a Word 2007 + (beleértve a 2010, 2013, 2016, 2019 és a Microsoft 365 verziókat).

### Mi a teendő, ha el kell forgatni a formát?

```csharp
figure.Rotation = 45; // degrees
```

### Hogyan adhatunk hozzá vektorgrafikát raszteres kép helyett?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro tippek és buktatók

- **Fájlutak:** Használd a `Path.Combine`‑t a keménykódolt elválasztók elkerüléséhez, különösen nem‑Windows platformokon.
- **Licenckorlátok:** Az ingyenes GemBox licenc a dokumentumméretet 20 KB‑ra korlátozza. Nagyobb fájlokhoz vásárolj kereskedelmi kulcsot.
- **Teljesítmény:** Egyetlen `Document` példány újra‑használata kötegelt feldolgozásnál jelentősen csökkenti a memóriaigényt.
- **Alakzat túlcsordulás:** Ha az ábra méretei meghaladják a lap margóit, a Word levágja. Állítsd be a `figure.Width` és `figure.Height` értékeket ennek megfelelően.

## Összegzés

Most már tudod, **hogyan adjunk ábrát Word-hez**, pontosan **hogyan helyezzük el az ábrát Word-ben**, és hogyan manipuláljuk az alatta lévő egyedi XML‑t, hogy a forma úgy viselkedjen, mint bármely natív elem. A teljes, futtatható példakód minden lépést bemutat – a dokumentum betöltésétől, egy `FigureElement` létrehozásán, koordináták beállításán, kép csatolásán, egészen a frissített *.docx* mentéséig.

Most próbáld ki a **insert figure into docx**‑et több ábra hozzáadásával, ciklusok használatával, vagy diagramok dinamikus generálásával. Felfedezheted a **how to add custom xml** lehetőségeket gazdagabb tartalomvezérlők létrehozásához, vagy a **how to position shape word** technikákat táblázatokban és fejlécekben. A lehetőségek végtelenek, és a most lefedett alapokkal már profi módon automatizálhatod a Word dokumentumokat.

Boldog kódolást, és nyugodtan hagyj megjegyzést, ha elakadsz!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}