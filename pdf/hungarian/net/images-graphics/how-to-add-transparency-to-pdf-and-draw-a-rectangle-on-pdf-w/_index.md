---
category: general
date: 2026-09-12
description: Ismerje meg, hogyan adhat átlátszóságot a PDF-hez, hogyan rajzolhat téglalapot
  a PDF-re, és hogyan mentheti el a PDF-et átlátszósággal az Aspose.PDF C#-ban – lépésről
  lépésre útmutató.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: hu
lastmod: 2026-09-12
og_description: Adj átlátszóságot a PDF-nek, rajzolj egy téglalapot a PDF-re, és mentsd
  el a PDF-et átlátszósággal az Aspose.PDF C# használatával. Kövesd ezt a teljes útmutatót.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Átlátszóság hozzáadása a PDF-hez és téglalap rajzolása a PDF-re – teljes
  C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Hogyan adhatunk átlátszóságot a PDF-hez, és rajzolhatunk egy téglalapot a PDF-re
  az Aspose.PDF segítségével
url: /hu/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan adjon átlátszóságot a PDF-hez és rajzoljon téglalapot a PDF-re az Aspose.PDF segítségével

Ha **átlátszóságot szeretne adni a PDF** fájloknak, ez az útmutató pontosan megmutatja, hogyan teheti ezt meg C#‑ban. Emellett megtanulja, hogyan **rajzoljon téglalapot a PDF-re**, és végül **mentse el a PDF‑et átlátszósággal**, hogy az eredmény újra felhasználható legyen jelentésekben, számlákban vagy bármilyen dokumentum‑automatizálási munkafolyamatban.

Ebben a tutorialban:

* Betölt egy meglévő PDF‑dokumentumot.
* Létrehoz egy egyedi grafikai állapotot, amely meghatározza a vonal és a kitöltés átlátszóságát.
* Alkalmazza ezt a grafikai állapotot a vászonra és téglalapot rajzol.
* Elmenti a módosított fájlt, miközben megőrzi az átlátszósági beállításokat.

Nem szükséges külső eszköz a Aspose.PDF for .NET könyvtáron kívül, és minden kódsor magyarázatot kap, hogy megértse, *miért* fontos az egyes lépések.

## Előfeltételek

* .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑vel is működik).
* Licencelt vagy értékelő változatú **Aspose.PDF for .NET**. Telepítse NuGet‑en keresztül:

```bash
dotnet add package Aspose.Pdf
```

* Egy bemeneti PDF (`input.pdf`) egy olyan mappában, amelyre a projekt hivatkozhat.

## 1. lépés: PDF‑dokumentum betöltése

Az első művelet a forrásfájl megnyitása. A `using` utasítás garantálja, hogy a dokumentum megfelelően felszabadul, ezáltal elkerülve a fájl‑zárolási problémákat a mentéskor.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Miért fontos*: A dokumentum betöltése hozzáférést biztosít az oldalak gyűjteményéhez, az erőforrás‑szótárakhoz és a rajzoláshoz szükséges vászonobjektumokhoz.

## 2. lépés: Az első oldal erőforrás‑szótárának elérése

Minden PDF‑oldal rendelkezik egy **erőforrás‑szótárral**, amely olyan objektumokat tárol, mint betűtípusok, képek és grafikai állapotok. Új átlátszósági beállítás bevezetéséhez szerkesztenünk kell az `ExtGState` bejegyzést.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Miért fontos*: A `DictionaryEditor` lehetővé teszi alacsony szintű PDF‑objektumok olvasását és módosítását anélkül, hogy megsértené a dokumentum szerkezetét.

## 3. lépés: Egyedi grafikai állapot létrehozása átlátszósági értékekkel

A grafikai állapot (`ExtGState`) szabályozza, hogyan jelennek meg a rajzolási műveletek. Két átlátszósági paramétert definiálunk:

* **CA** – vonal átlátszóság (alakzatok körvonala).
* **ca** – kitöltés átlátszóság (alakzatok belseje).

A keverési módot (`BM`) is beállítjuk „Normal” értékre, ami a leggyakoribb kompozíciós művelet.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Miért fontos*: A `GS0` hozzáadásával az `ExtGState` szótárhoz újrahasználható hivatkozást hozunk létre, amelyet a vászon aktiválhat a rajzolás előtt. A `0.5` kitöltési átlátszóság félig átlátszó téglalapot eredményez, ezáltal elérve a **átlátszóság hozzáadása a PDF‑hez** célt.

## 4. lépés: Grafikai állapot alkalmazása és téglalap rajzolása

Most azt mondjuk az oldal vásznának, hogy használja a most létrehozott grafikai állapotot, majd téglalapot rajzolunk. A koordináták a PDF koordináta‑rendszerét követik (origó a bal alsó sarokban).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Miért fontos*: A `SetGraphicsState("GS0")` a rajzolási kontextust a korábban definiált átlátszósági beállításokra váltja. A `Rectangle` metódus definiálja az alakzatot, a `Stroke` pedig a megadott átlátszósággal rajzolja meg a körvonalat. Ha kitöltött téglalapot is szeretne, cserélje a `Stroke()`‑t `FillAndStroke()`‑ra.

## 5. lépés: Módosított PDF mentése átlátszóság megőrzésével

Végül írjuk vissza a dokumentumot a lemezre. A kimeneti fájl tartalmazza az új grafikai állapotot, a rajzolt téglalapot és az átlátszósági információkat.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Miért fontos*: A dokumentum mentése véglegesíti az összes változtatást. A kapott fájl bármely PDF‑olvasóval megnyitható, és a téglalap 50 % kitöltési átlátszósággal jelenik meg.

### Várt eredmény

Amikor megnyitja a `output_with_extgstate.pdf` fájlt, egy olyan téglalapot kell látnia, amelynek szegélye teljesen átlátszatlan, a belseje pedig félig átlátszó, így az alatta lévő oldal tartalma látható marad.

## Szélhelyzetek és gyakorlati tippek

| Helyzet | Ajánlott módosítás |
|-----------|------------------------|
| **Több oldal** | Iteráljon a `pdfDocument.Pages`‑en, és ismételje meg a 2‑4. lépéseket minden céloldalra. |
| **Eltérő átlátszósági értékek** | Módosítsa a `CosPdfNumber` értékeket a `CA` (vonal) és `ca` (kitöltés) esetén bármely 0‑tól (teljesen átlátszó) 1‑ig (teljesen átlátszatlan) tartományban. |
| **Egyedi keverési módok** | Cserélje a „Normal” értéket „Multiply”, „Screen” vagy bármely, a nézője által támogatott PDF‑standard keverési módra. |
| **Kitöltött téglalap** | Hívja a `canvas.FillAndStroke()`‑t a `canvas.Stroke()` helyett, hogy a kitöltés és a körvonal is megjelenjen. |
| **Ugyanazon grafikai állapot újbóli használata** | A `canvas.SetGraphicsState("GS0")`‑t meghívhatja bármennyi alakzat rajzolása előtt ugyanazon az oldalon. |

**Pro tipp:** Mindig ellenőrizze az erőforrás‑szótárat új `ExtGState` hozzáadása után. Ha a szótár nem létezik, hozza létre előbb:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Teljes, futtatható példa

Az alábbi önálló programot beillesztheti egy konzolalkalmazásba, és azonnal futtathatja (cserélje le a `YOUR_DIRECTORY`‑t egy valós útvonalra).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

A program futtatása `output_with_extgstate.pdf`‑t hoz létre, amely bemutatja a **átlátszóság hozzáadása a PDF‑hez**, a **téglalap rajzolása a PDF‑re**, és a **PDF mentése átlátszósággal** mind egy folyamatban.

## Összegzés

Most már tudja, hogyan **adjunk átlátszóságot a PDF‑hez**, **rajzoljunk téglalapot a PDF‑re**, és **mentsük el a PDF‑et átlátszósággal** az Aspose.PDF for .NET segítségével. A folyamat lényege egy egyedi `ExtGState` létrehozása, annak alkalmazása a vászonra, és a változások mentése. Ezekkel az építőelemekkel kiterjesztheti a technikát más alakzatokra, több oldalra vagy dinamikus átlátszósági értékekre.

**Következő lépések**

* Fedezze fel a többi rajzolási primitívet, például a `canvas.Ellipse`, `canvas.Path` vagy `canvas.TextFragment` használatát, miközben ugyanazt a grafikai állapotot újrahasználja.
* Kombinálja az átlátszóságot képrétegekkel, hogy vízjeleket hozzon létre (`canvas.Image` + egyedi `ExtGState`).
* Tekintse át az Aspose.PDF dokumentációját a **grafikai állapot paraméterek** kapcsán, hogy haladó kompozíciós hatásokat érjen el.

Jó kódolást, és élvezze az átlátszóság által nyújtott vizuális rugalmasságot PDF‑folyamataiban!

## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}