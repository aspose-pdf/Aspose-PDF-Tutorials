---
category: general
date: 2026-09-27
description: Adjon hozzá Bates-számozást PDF-hez az Aspose.PDF használatával C#-ban.
  Ismerje meg, hogyan töltsön be egy PDF-dokumentumot, állítsa be a Bates-számozási
  beállításokat, és mentse el a frissített fájlt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: hu
lastmod: 2026-09-27
og_description: Bates-számozás hozzáadása PDF-hez az Aspose.PDF C#-ban. Ez az útmutató
  megmutatja, hogyan töltsünk be egy PDF-dokumentumot, konfiguráljuk a Bates-számozást,
  és mentsük el az eredményt.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Bates-számozás hozzáadása PDF-hez az Aspose.PDF segítségével – C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Bates-számozás hozzáadása PDF-hez az Aspose.PDF használatával C#-ban
url: /hu/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates számozás hozzáadása PDF-hez az Aspose.PDF használatával C#-ban

Ha PDF fájlhoz **bates számozást** kell hozzáadnia, ez az útmutató egy teljes, azonnal futtatható megoldást mutat be. Megmutatjuk, hogyan **töltsön be egy PDF dokumentumot**, állítsa be a Bates számozási beállításokat, és írja vissza a számozott fájlt a lemezre — mindezt az Aspose.PDF for .NET segítségével.

A Bates számok alkalmazása gyakori a jogi, a bűnüldözési és az archiválási munkafolyamatokban. A tutorial végére képes lesz minden oldalra beágyazni egy sorozatos azonosítót, testreszabni az előtagot, és tetszőleges számmal indítani a számlálást.

## Mit fog megtanulni

* Hogyan **töltsön be PDF dokumentum** tartalmat egy `Aspose.Pdf.Document` objektumba.  
* A pontos lépések **hogyan adjon hozzá bates számozást** a `BatesNumberingOptions` használatával.  
* Hogyan mentse el a módosított fájlt az eredeti elrendezés és minőség megőrzésével.  

Nem szükséges külső eszköz — csak az Aspose.PDF NuGet csomag és egy .NET fejlesztői környezet (Visual Studio, VS Code vagy Rider).  

---

## 1. lépés: Az Aspose.PDF for .NET telepítése

Nyissa meg a projekt mappáját egy terminálban, és futtassa:

```bash
dotnet add package Aspose.PDF
```

A csomag tartalmazza az `Aspose.Pdf` névteret, amely minden ebben a tutorialban használt osztályt biztosít. A telepítés után töltse újra a projektet, hogy az IDE felvegye az új hivatkozást.

## 2. lépés: PDF dokumentum betöltése

A forrásfájl betöltése az első művelet, mivel a Bates számozási motor egy meglévő `Document` példányon dolgozik.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Miért fontos:** A `Document` osztály elemzi a PDF struktúráját, hozzáférést biztosít az oldalakhoz, megjegyzésekhez és metaadatokhoz. A fájl betöltése nélkül nem alkalmazható semmilyen számozás.

## 3. lépés: Bates számozási beállítások konfigurálása

Hozzon létre egy `BatesNumberingOptions` objektumot, és állítsa be a kívánt előtagot, kezdőszámot, valamint az opcionális formázási paramétereket.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Miért fontos:** A `BatesNumberingOptions` megmondja az Aspose.PDF-nek, hogyan generálja az egyes oldalak címkéjét. A `Prefix` segít a kapcsolódó esetek csoportosításában, míg a `StartNumber` lehetővé teszi a sorozat folytatását egy korábbi köteg után.

## 4. lépés: PDF mentése Bates számok alkalmazásával

Adja át a beállítási objektumot a `Save` metódusnak. Az Aspose.PDF a számokat közvetlenül minden oldalra írja.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Miért fontos:** A `Save(string, BatesNumberingOptions)` túlterhelés egyesíti a renderelési lépést a számozási folyamattal, biztosítva, hogy a kimeneti fájl tartalmazza a látható azonosítókat.

## Teljes példa – minden egyben

Az alábbi egy önálló program, amelyet másolhat, beilleszthet és futtathat. Bemutatja, **hogyan adjon hozzá bates számozást** az elejétől a végéig.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Várt kimenet

A program futtatása `output.pdf`-t hoz létre, ahol minden oldal egy hasonló címkét jelenít meg:

```
CASE01-1
CASE01-2
CASE01-3
...
```

A számok alapértelmezés szerint a láblécben jelennek meg, de áthelyezhetők a `Margin` tulajdonság `BatesNumberingOptions`-ban történő módosításával.

## Szélsőséges esetek és gyakori variációk

| Situation | What to adjust |
|-----------|----------------|
| **Különböző előtag kötegenként** | Módosítsa a `Prefix` értékét a `Save` hívása előtt. Több dokumentumot is feldolgozhat különálló előtagokkal egy ciklusban. |
| **Számozás folytatása egy korábbi fájlból** | Állítsa a `StartNumber`-t az utolsó használt szám + 1 értékére. |
| **Számok elhelyezése a fejlécben** | Használja a `batesOptions.Margin = new Margin(20, 0, 0, 0);` (felső margó) beállítást, vagy testreszabhatja a `batesOptions.Position`-t. |
| **Egyedi betűtípus vagy szín** | Állítsa be a `Font`, `FontSize` és `Color` tulajdonságokat, ahogy a megjegyzett részben látható. |
| **Nagy PDF-ek (1000+ oldal)** | A művelet memóriahatékony; azonban érdemes lehet a `doc.OptimizeResources()` hívást engedélyezni a mentés előtt a fájlméret csökkentése érdekében. |

**Pro tipp:** Ha a munkafolyamat különböző számozási sémákat igényel dokumentumonként, helyezze a logikát egy segédmetódusba:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Következtetés

Most már tudja, **hogyan adjon hozzá bates számozást** bármely PDF-hez az Aspose.PDF C#-ban használva. A tutorial bemutatta a PDF dokumentum betöltését, a számozási beállítások konfigurálását és a végső fájl mentését — mindezt egyetlen, futtatható programban.  

Innen tovább felfedezheti a kapcsolódó témákat, mint a **vízjel hozzáadása**, **több PDF egyesítése**, vagy **szöveg kinyerése** az Aspose.PDF segítségével. Kísérletezzen különböző betűtípusokkal, színekkel és pozíciókkal, hogy megfeleljen a szervezet formázási szabványainak.

Készen áll a jogi dokumentumok munkafolyamatának automatizálására? Adja hozzá a kódot a build pipeline-hoz, futtassa a fájlkötegeken, és hagyja, hogy az Aspose.PDF végezze a nehéz munkát. Boldog kódolást!

## Mit érdemes még megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Create PDF Document C# – Add Bates Numbering](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}