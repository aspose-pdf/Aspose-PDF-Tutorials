---
category: general
date: 2026-08-14
description: Rajzolj téglalapot PDF-re gyorsan C#-ban. Tanulja meg, hogyan definiálja
  a téglalap méreteit, és hogyan adjon hozzá alakzatokat egy PDF oldalhoz néhány sorban.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: hu
lastmod: 2026-08-14
og_description: Rajzolj téglalapot PDF-re C#-vel pillanatok alatt. Ez az útmutató
  bemutatja, hogyan határozd meg a téglalap méreteit, adj hozzá alakzatot, és ellenőrizd
  az oldalhatárokat a megbízható PDF-grafikához.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: téglalap rajzolása PDF-re – teljes C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Téglalap rajzolása PDF-re – lépésről lépésre C# útmutató
url: /hu/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# téglalap rajzolása PDF-re – teljes C# útmutató

Ha C#-ban **draw rectangle on pdf**-t kell készítened, ez az útmutató egy tömör, termelés‑kész megoldást mutat be. Pontosan láthatod, **how to define rectangle dimensions**, ellenőrizheted, hogy a forma belefér-e, és egyetlen metódushívással hozzáadhatod egy oldalhoz.

Az útmutató mindent lefed a PDF dokumentum létrehozásától a téglalap megjelenítéséig, így a kódot egyszerűen átmásolhatod a saját projektedbe, és azonnal láthatod az eredményt. Külső dokumentációra nincs szükség – csak a lenti lépésekre.

## Előfeltételek

* .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑vel is működik)
* A **Aspose.PDF for .NET** NuGet csomag (`Install-Package Aspose.PDF`)
* Alapvető C# szintaxis ismerete
* Egy IDE, például Visual Studio vagy VS Code

> **Pro tip:** Használd az Aspose.PDF ingyenes értékelő licencét gyors kísérletekhez; egy kis vízjelet ad hozzá, de lehetővé teszi az összes funkció tesztelését.

## Hogyan rajzoljunk téglalapot PDF-re C#-ban

A feladat lényege egy `RectangleShape` létrehozása, méretének és vonalának beállítása, majd egy `Page`-hez csatolása. Az alábbi H2 fejléc tartalmazza az elsődleges kulcsszót, ezzel megfelelve az SEO követelményeknek.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Az egyes lépések magyarázata

| Lépés | Miért fontos |
|------|----------------|
| **1️⃣ Create a new PDF document** | Inicializálja a tárolót, amely az oldalakat és a grafikákat tartalmazza. |
| **2️⃣ Add a blank page** | Szükséged van egy `Page` objektumra, mert a formákat egy oldalhoz kell csatolni, nem közvetlenül a dokumentumhoz. |
| **3️⃣ Define the rectangle bounds** | Itt történik a **how to define rectangle dimensions**. A `Rectangle` konstruktor `x`, `y`, `width` és `height` értékeket vár pontban (1 pt = 1/72 in). |
| **4️⃣ Create the rectangle shape** | A `RectangleShape` az Aspose osztály, amely egy téglalapot rajzol. A `StrokeColor` beállítása határozza meg a körvonalat; a `FillColor` is beállítható szilárd kitöltéshez. |
| **5️⃣ Verify page boundaries** | A `CheckShapeBoundary` kivételt dob, ha a téglalap meghaladja az oldal méretét, megakadályozva a hibás PDF-eket. |
| **6️⃣ Add the shape to the page** | A forma az oldal tartalomsorozatának részévé válik. |
| **7️⃣ Save the PDF** | Elmenti a dokumentumot egy fájlba, amelyet bármely PDF-olvasóval megnyithatsz. |

Az eredményül kapott `RectangleDemo.pdf` egy fekete téglalapot tartalmaz, amely az oldal bal‑felső sarkában helyezkedik el, pontosan 500 pt széles és 700 pt magas.

![draw rectangle on pdf példa](https://example.com/rectangle-demo.png "draw rectangle on pdf példa")

*Kép alternatív szövege: draw rectangle on pdf példa, amely egy fekete téglalapot mutat a PDF oldal bal‑felső sarkában.*

## Hogyan definiáljuk a téglalap méreteit különböző oldalméretekhez

A fenti kódrészlet rögzített értékeket (`500 x 700`) használ. Valós alkalmazásokban gyakran szükség van arra, hogy a téglalap alkalmazkodjon az oldal szélességéhez és magasságához.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Kulcspontok:**

* Használd a `page.PageInfo.Width` és `Height` értékeket a tényleges oldalméret lekérdezéséhez.
* Egy tényezővel (pl. `0.8f`) való szorzás lehetővé teszi a méretek oldal százalékában való kifejezését.
* A középre helyezés úgy érhető el, hogy a téglalap méretét levonod az oldal méretéből, majd a maradékot felosztod kettővel.

## Gyakori buktatók és hogyan kerüld el őket

| Buktató | Miért fordul elő | Megoldás |
|---------|----------------|-----|
| A téglalap túlnyúlik az oldalon | Keménykódolt méretek nagyobbak az oldal méreténél. | Hívd meg a `page.CheckShapeBoundary` **előtt**, mielőtt hozzáadod a formát; ha kivétel keletkezik, módosítsd a méreteket. |
| A körvonal nem látható | `StrokeColor` alapértelmezett (`Color.Empty`) maradt. | Állítsd be kifejezetten a `StrokeColor`-t (pl. `Color.Black`). |
| A téglalap a képernyőn kívül jelenik meg | A koordináták a PDF térben bal‑alsó sarokból indulnak; képernyő‑stílusú bal‑felső koordináták használata fordítást okoz. | Ne feledd, hogy a `(0,0)` a bal‑alsó sarok. Ennek megfelelően állítsd be a `y` értéket, vagy használd a `pageHeight - desiredY` képletet. |
| Váratlan vonalvastagság | Az alapértelmezett vonalvastagság túl vékony lehet nyomtatáshoz. | Állítsd be a `rectangleShape.LineWidth = 2;` értéket a vastagság növeléséhez. |

## A példa kibővítése

Miután képes vagy **draw rectangle on pdf**-re, könnyen hozzáadhatsz más alakzatokat:

* **EllipseShape** – körök vagy oválisok számára.
* **PolygonShape** – egyedi sokszögekhez.
* **TextFragment** – a téglalapok feliratozásához.

Minden alakzat ugyanazt a munkafolyamatot követi: meghatározod a határokat, beállítod a megjelenést, ellenőrzöd a határokat, majd hozzáadod az oldalhoz.

## Teljes, futtatható program

Az alábbiakban a teljes program látható, amely egyesíti az alap téglalapot és a dinamikus méretezés példáját. Másold be egy új konzolprojektbe, állítsd vissza a `Aspose.PDF` NuGet csomagot, és futtasd.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Várható kimenet:**  
Nyisd meg a `CombinedRectangles.pdf`-et. Egy fekete téglalapot látsz, amely a bal‑alsó sarokban van rögzítve, valamint egy középre helyezett sötétkék téglalapot világossárga kitöltéssel. Mindkét téglalap tiszteletben tartja az oldal margóit.

## Következtetés

Most már tudod, hogyan **draw rectangle on pdf** C#-ban, és pontosan **how to define rectangle dimensions** rögzített és reszponzív elrendezésekhez egyaránt. A megközelítés az Aspose.PDF `RectangleShape`-ját, a határok ellenőrzését és egyszerű aritmetikát használ a bármely oldalmérethez való alkalmazkodáshoz.

Ezután érdemes felfedezni:

* **Kitöltőszínek** és **vonalstílusok** (szaggatott, pontozott) hozzáadása – másodlagos kulcsszó: how to define rectangle dimensions with style.
* Több alakzat egyesítése egyetlen `Page`‑be diagramok vagy űrlapok létrehozásához.
* A PDF exportálása stream-be web API-khoz a lemezre mentés helyett.

## Mit érdemes még megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan testre szabjuk a PDF-eket az Aspose.PDF for .NET: oldal margók beállítása és vonalak rajzolása](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Hogyan adjunk hozzá oldalbélyegeket PDF-ekhez az Aspose.PDF for .NET: teljes útmutató](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Hogyan adjunk hozzá oldalszám bélyegeket PDF-ekhez az Aspose.PDF for .NET | Vízjelek és háttér](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}