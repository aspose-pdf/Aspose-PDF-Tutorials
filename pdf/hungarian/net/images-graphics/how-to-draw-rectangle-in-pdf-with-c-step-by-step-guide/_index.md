---
category: general
date: 2026-03-27
description: Tanulja meg, hogyan rajzoljon téglalapot PDF-be az Aspose.Pdf for C#
  segítségével. Adjon hozzá téglalapot a PDF-hez, adjon hozzá alakzatot a PDF-hez,
  és rajzoljon alakzatot a PDF-re világos kódrészletekkel.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: hu
og_description: Tanulja meg, hogyan rajzoljon téglalapot PDF-ben az Aspose.Pdf segítségével.
  Ez az útmutató lépésről lépésre bemutatja, hogyan adjon hozzá téglalapot a PDF-hez,
  hogyan adjon hozzá alakzatot a PDF-hez, és hogyan rajzoljon alakzatot a PDF-re.
og_title: Hogyan rajzoljunk téglalapot PDF-ben C#-val – Teljes útmutató
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hogyan rajzoljunk téglalapot PDF-ben C#‑val – Lépésről lépésre útmutató
url: /hu/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan rajzoljunk téglalapot PDF-ben C#‑val – Lépésről‑lépésre útmutató

Gondolkodtál már **hogyan lehet téglalapot rajzolni** egy PDF‑ben anélkül, hogy alacsony szintű PDF szintaxissal kellene bajlódni? Nem vagy egyedül. Sok fejlesztő akad el, amikor egy határoló keretet, kiemelési területet vagy egyszerű díszítő elemet szeretne megjeleníteni egy generált dokumentumban. A jó hír? Az Aspose.Pdf for .NET‑tel ez a folyamat gyerekjáték.

Ebben a bemutatóban végigvezetünk mindenen, ami szükséges a **téglalap PDF‑hez adásához**, a **alak PDF‑hez adásához**, és végül a **téglalap PDF‑ben való rajzolásához** tiszta, idiomatikus C#‑val. A végére egy futtatható programot kapsz, amely egy PDF‑fájlt hoz létre egy éles téglalappal – külső eszközök nélkül.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Core‑dal és .NET Framework‑kel is működik)
- Aspose.Pdf for .NET NuGet csomag (`Install-Package Aspose.Pdf`)
- Alap C# fejlesztői környezet (Visual Studio, VS Code, Rider, stb.)

Más könyvtárra nincs szükség; minden mást az Aspose.Pdf maga kezel.

## 1. lépés: Projekt létrehozása és névterek importálása

Először hozz létre egy új konzolos alkalmazást, és importáld az Aspose.Pdf névteret.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Miért fontos:** Az `Aspose.Pdf.Drawing` importálása hozzáférést biztosít a `Rectangle` alak osztályhoz, amelyet a **alak PDF‑re rajzolásához** fogunk használni. A belépési pont rendezett tartása megkönnyíti a későbbi lépéseket.

## 2. lépés: Új PDF dokumentum és oldal létrehozása

Egy PDF‑nek oldalakra van szüksége, ezért kezdjük egy dokumentum objektummal, majd adjunk hozzá egyetlen oldalt.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Magyarázat:** A `Document` osztály a teljes fájlt képviseli, míg a `Pages.Add()` egy friss `Page` objektumot ad vissza, ahová később **téglalapot adunk a PDF‑hez**. Az alapértelmezett A4 méret a legtöbb esetben megfelelő, de ha egyedi vászonra van szükséged, megadhatod a szélességet/magasságot is.

## 3. lépés: A téglalap alak definiálása

Most következik a **hogyan kell téglalapot rajzolni** magja – a pozíció és a méretek meghatározása.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Miért állítjuk be ezeket a tulajdonságokat:**  
- A `BorderColor` és a `BorderWidth` szabályozza a körvonalat, így a téglalap látható lesz.  
- A `FillColor` finom háttérszínt ad, ami hasznos, ha egy területet szeretnél kiemelni.  
- A `(x, y, width, height)` konstruktor lehetővé teszi, hogy **téglalapot rajzolj PDF‑ben** pontosan ott, ahol szükséges.

## 4. lépés: A téglalap hozzáadása az oldalhoz

Miután az alak készen áll, **alakot adunk a PDF‑hez**, az oldal `Annotations` gyűjteményéhez csatolva. Az Aspose.Pdf automatikusan ellenőrzi a határokat, így nem kell aggódnod a túlcsordulás miatt.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Mi történik a háttérben:** Az `Annotations` gyűjtemény a téglalapot vektoros grafikaként kezeli. Amikor a PDF megjelenik, a könyvtár a koordinátákat a PDF tartalomsorba fordítja.

## 5. lépés: Dokumentum mentése

Végül írjuk a PDF‑et a lemezre, hogy bármely megjelenítővel megnyithasd.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Eredmény:** A `RectangleDemo.pdf` megnyitásakor egy világosszürke téglalap látható fekete körvonallal, amely 100 pt-re van a bal szélről és 500 pt-re az oldal aljától. Ez a teljes megoldás a **hogyan kell téglalapot rajzolni** PDF‑ben C#‑val.

## Teljes működő példa

Az összes részt összevonva itt a kész, futtatható program:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Várt kimenet:** Egy `RectangleDemo.pdf` nevű fájl, amely egyetlen oldalt tartalmaz középen elhelyezett, világosszürke téglalappal, fekete körvonallal. Megnyitható Adobe Readerrel, Chrome‑nal vagy bármely PDF‑olvasóval.

## Gyakori variációk és széljegyek

### 1. Több téglalap rajzolása

Ha **téglalapot adsz a PDF‑hez** többször, egyszerűen hozz létre további `Rectangle` objektumokat, és add hozzá mindegyiket a `page.Annotations`‑hoz. Egy koordinátakollekció felett iterálva ez könnyedén megoldható.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Különböző mértékegységek használata

Az Aspose.Pdf pontokban dolgozik (1 pt = 1/72 inch). Ha millimétert részesítesz előnyben, előbb konvertáld őket:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Téglalap hozzáadása űrlapmezőként

Amikor interaktív téglalapra (például kattintható terület) van szükség, használj `LinkAnnotation`‑t a sima `Rectangle` helyett. A kód hasonló, csak egy URL‑t vagy JavaScript‑műveletet ad hozzá.

### 4. Kompatibilitási kérdések

Az Aspose.Pdf 23.9-es verziója (2026 elején kiadva) teljes mértékben támogatja a fent bemutatott API‑kat. Régebbi verziók esetén előfordulhat, hogy `page.AddAnnotation(rectangleShape)`‑t kell használni a `page.Annotations.Add` helyett. Mindig ellenőrizd a kiadási megjegyzéseket, ha fordítási hibákkal találkozol.

## Pro tippek és buktatók

- **Pro tipp:** Állítsd `FillColor = Color.Transparent`‑ra, ha csak a körvonalra van szükséged. Ez kissé csökkenti a fájlméretet.
- **Vigyázz:** Ne használj olyan koordinátákat, amelyek meghaladják az oldal méretét. Az Aspose.Pdf csendben levágja az alakot, ami hibakereséskor zavaró lehet.
- **Teljesítményjegyzet:** Több ezer téglalap hozzáadása megoldható, de ha nagy jelentéseket generálsz, fontold meg a formák egyetlen `Graphics` objektumba való csoportosítását a terhelés csökkentése érdekében.

## Vizuális referencia

Alább egy gyors képernyőfotó a generált PDF‑ről (a téglalap világosszürkével ki van emelve). Az alt szöveg tartalmazza a fő kulcsszót a SEO‑hoz.

![hogyan kell téglalapot rajzolni PDF-ben példa](https://example.com/images/rectangle-demo.png "hogyan kell téglalapot rajzolni PDF-ben példa")

## Összegzés

Áttekintettük, **hogyan kell téglalapot rajzolni** PDF‑ben az Aspose.Pdf for C# segítségével. Egy `Document` létrehozásával, egy `Page` hozzáadásával, egy `Rectangle` alak definiálásával és végül **alak PDF‑hez adásával** vektoros grafikákat generálhatsz néhány sor kóddal. Akár **téglalapot adsz a pdf‑hez** kiemeléshez, elrendezés‑debugoláshoz vagy UI‑átfedésekhez, ez a megközelítés könnyen skálázható.

A következő lépésben felfedezheted a **alak PDF‑re rajzolását** téglalapokon túl – gondolj körökre, vonalláncokra vagy akár egyedi SVG‑útvonalakra. Vagy merülj el a szöveg renderelésben, képek beillesztésében és PDF‑űrlapok kezelésében, hogy teljes körű jelentéseket építs. Az Aspose.Pdf gazdag API‑t kínál, és a most bemutatott alapokkal készen állsz a kísérletezésre.

Boldog kódolást, és legyenek a PDF‑eid mindig úgy, ahogy elképzelted!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}