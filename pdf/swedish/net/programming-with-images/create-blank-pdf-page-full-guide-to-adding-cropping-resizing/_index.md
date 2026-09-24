---
category: general
date: 2026-03-27
description: Skapa en tom PDF-sida och lär dig hur du skapar PDF från bild, lägger
  till bild i PDF, beskär bild i PDF och ändrar storlek på bild i PDF med Aspose.Pdf
  i C#.
draft: false
keywords:
- create blank pdf page
- create pdf from image
- add image to pdf
- crop image in pdf
- resize image in pdf
language: sv
og_description: Skapa en tom PDF-sida och lägg omedelbart till, beskära och ändra
  storlek på bilder med Aspose.Pdf. Steg‑för‑steg C#‑handledning för utvecklare.
og_title: Skapa en tom PDF-sida – Lägg till, beskära och ändra storlek på bilder i
  C#
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Skapa tom PDF-sida – Fullständig guide för att lägga till, beskära och ändra
  storlek på bilder
url: /sv/net/programming-with-images/create-blank-pdf-page-full-guide-to-adding-cropping-resizing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa tom PDF‑sida – Komplett C#‑handledning

Har du någonsin behövt **skapa en tom PDF‑sida** och sedan lägga en bild på den, men inte vetat var du ska börja? Du är inte ensam. I många verkliga applikationer – tänk fakturor, produktkataloger eller snabba rapportgeneratorer – kommer du behöva ett fräscht PDF‑canvas, släppa in en bild, eventuellt beskära den och slutligen justera dess storlek.  

I den här guiden går vi igenom hela processen: **create PDF from image**, **add image to PDF**, **crop image in PDF** och **resize image in PDF** med Aspose.Pdf‑biblioteket. I slutet har du ett färdigt kodexempel som producerar en professionell PDF med en beskuren och skalad bild.

---

## Vad du behöver

- **.NET 6+** (eller .NET Framework 4.6+). API‑et fungerar likadant i alla versioner, men den senaste runtime‑en ger bättre prestanda.  
- **Aspose.Pdf for .NET** – du kan hämta det från NuGet (`Install-Package Aspose.Pdf`) eller ladda ner den kostnadsfria provversionen från den officiella webbplatsen.  
- En bildfil (JPEG, PNG osv.) placerad någonstans på disken; vi kallar den `input.jpg`.  
- En kodredigerare – Visual Studio, VS Code eller Rider – vad du än föredrar.

> Pro tip: Om du kör i en CI/CD‑pipeline, lägg till Aspose.Pdf‑NuGet‑paketet i din projektfil så att bygget aldrig glömmer beroendet.

---

## Steg 1: Skapa en tom PDF‑sida

Det första vi gör är att skapa ett helt nytt PDF‑dokument och lägga till en **tom PDF‑sida** i det. Tänk på dokumentet som en anteckningsbok och sidan som det första bladet du skriver på.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class Program
{
    static void Main()
    {
        // Step 1: Initialize a fresh PDF document (blank canvas)
        using var pdfDocument = new Document();

        // Step 2: Add a blank page – this is where the image will live
        Page pdfPage = pdfDocument.Pages.Add();

        // (More steps follow...)
```

Varför lägga till en sida först? Aspose‑API:t förväntar sig ett sidobjekt när du senare placerar grafik. Att hoppa över detta steg skulle kasta ett `NullReferenceException` eftersom det inte finns någon plats att rita på.

---

## Steg 2: Skapa PDF från bild (valfri snabbstart)

Om du bara vill ha en PDF som innehåller *endast* en bild – ingen extra text, inga extra sidor – erbjuder Aspose en genväg. Detta är inte ett krav för huvudflödet, men det är bra att känna till.

```csharp
// Quick way: convert an image directly to a one‑page PDF
// Comment out if you prefer the manual approach below
pdfDocument.Pages.Add(ImageStreamToPdfPage("YOUR_DIRECTORY/input.jpg"));
```

```csharp
static Page ImageStreamToPdfPage(string imagePath)
{
    var stream = File.OpenRead(imagePath);
    var page = new Page(pdfDocument);
    // The image fills the whole page by default
    page.AddImage(stream, new Rectangle(0, 0, pdfDocument.PageInfo.Width, pdfDocument.PageInfo.Height));
    return page;
}
```

Detta kodsnutt visar **create pdf from image**‑genvägen, men vi fortsätter med den manuella metoden så att vi kan **crop** och **resize** exakt.

---

## Steg 3: Läs in källbilden som en ström

Nu öppnar vi bildfilen som en stream. Att använda en stream håller minnesanvändningen låg, särskilt för stora bilder.

```csharp
        // Step 3: Open the source image file as a read‑only stream
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/input.jpg");
```

Om filen inte hittas kastas ett `FileNotFoundException` – så dubbelkolla sökvägen. I produktionskod kan du omsluta detta med ett try‑catch‑block och logga ett vänligt meddelande.

---

## Steg 4: Definiera käll‑ och destinationsrektanglar (beskärning & skalning)

Aspose låter dig ange två rektanglar:

1. **Source rectangle** – den del av originalbilden du vill behålla.  
2. **Destination rectangle** – området på PDF‑sidan där den delen ska ritas, vilket i praktiken styr den slutliga storleken.

```csharp
        // Step 4: Set up the area of the image to keep (crop) and its size on the PDF page (resize)
        // Source rectangle – top‑left corner (0,0), width 600px, height 800px
        var sourceRectangle = new Rectangle(0, 0, 600, 800);

        // Destination rectangle – where the cropped piece lands on the page
        // Here we shrink it to half the original dimensions (300x400)
        var destinationRectangle = new Rectangle(0, 0, 300, 400);
```

Varför inte bara använda hela bilden? Många verkliga scenarier kräver att du tar bort vita kanter eller fokuserar på en logotyp. Justera siffrorna så att de matchar dina egna bilddimensioner.

---

## Steg 5: Lägg till bilden i PDF, applicera beskärning & skalning

Med rektanglarna klara anropar vi `AddImage`. Detta enkla anrop gör det tunga arbetet: det extraherar den definierade delen av källbilden och målar den på sidan med den angivna storleken.

```csharp
        // Step 5: Place the cropped & resized image onto the blank page
        pdfPage.AddImage(imageStream, sourceRectangle, destinationRectangle);
```

Under huven skapar Aspose ett XObject, beskär det och skalar det i ett enda steg – så du behöver inga extra bildbehandlingsbibliotek.

---

## Steg 6: Spara den resulterande PDF‑filen

Till sist sparar vi dokumentet till disk. Filen `CroppedImage.pdf` kommer att innehålla den **blank PDF page** vi skapade, nu prydd med en snyggt beskuren och skalad bild.

```csharp
        // Step 6: Write the PDF to the output file
        pdfDocument.Save("YOUR_DIRECTORY/CroppedImage.pdf");
    }
}
```

När du öppnar `CroppedImage.pdf` i någon visare bör du se en enda sida där bilden sitter i det övre vänstra hörnet, exakt 300 × 400 points (≈4 × 5 tum vid 72 dpi).  

> **Förväntat resultat:** En PDF med en sida, bilden beskuren till rektangeln (0,0,600,800) från källan, och visad i halva storleken (300 × 400) på sidan.

---

## Vanliga frågor & kantfall

### Vad händer om min bild är mindre än källrektangeln?

Aspose kommer automatiskt att sträcka bilden för att fylla källrektangeln, vilket kan bli suddigt. För att undvika detta, beräkna källrektangeln baserat på bildens faktiska dimensioner:

```csharp
using var img = Image.FromStream(imageStream);
var actualWidth = img.Width;
var actualHeight = img.Height;
var sourceRect = new Rectangle(0, 0, actualWidth, actualHeight);
```

### Hur placerar jag bilden någon annanstans på sidan?

Ändra helt enkelt `destinationRectangle`‑värdena för X och Y. Till exempel, för att centrera bilden:

```csharp
float pageWidth = pdfPage.PageInfo.Width;
float pageHeight = pdfPage.PageInfo.Height;
float destX = (pageWidth - destinationRectangle.Width) / 2;
float destY = (pageHeight - destinationRectangle.Height) / 2;
var centeredRect = new Rectangle(destX, destY, destinationRectangle.Width, destinationRectangle.Height);
pdfPage.AddImage(imageStream, sourceRectangle, centeredRect);
```

### Vill du lägga till flera bilder?

Upprepa **Steg 5** med olika käll‑/destinationsrektanglar. Varje anrop lägger till ett nytt XObject på samma sida, eller så kan du skapa ytterligare sidor med `pdfDocument.Pages.Add()`.

### Behöver du högupplöst output?

Aspose arbetar i points (1 pt = 1/72 in). Om du kräver 300 dpi, multiplicera önskad storlek med 4,2 (300/72) innan du sätter destinationsrektangeln.

---

## Pro‑tips för produktionsklara PDF‑filer

- **Dispose korrekt:** `using`‑satserna i exemplet garanterar att filhandtag stängs, vilket förhindrar låsta filer på Windows.  
- **Kompression:** Anropa `pdfDocument.Compress();` innan du sparar för att minska filstorleken.  
- **Säkerhet:** Om du behöver skydda PDF‑en, sätt `pdfDocument.Encrypt` med ett användarlösenord.  
- **Prestanda:** Vid batch‑bearbetning, återanvänd en enda `Document`‑instans och lägg till sidor i en loop – detta minskar overhead.

---

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

```csharp
using System;
using System.Drawing;          // Needed for Image class (System.Drawing.Common NuGet)
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class CreatePdfWithCroppedImage
{
    static void Main()
    {
        // Initialize a new PDF document (blank canvas)
        using var pdfDocument = new Document();

        // Add a blank page – the surface for our image
        Page pdfPage = pdfDocument.Pages.Add();

        // Load the image file
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/input.jpg");

        // Optional: Adjust source rectangle to actual image size
        using var img = Image.FromStream(imageStream);
        var sourceRectangle = new Rectangle(0, 0, img.Width, img.Height);
        imageStream.Position = 0; // Reset stream after reading size

        // Destination rectangle – half the size, placed at (0,0)
        var destinationRectangle = new Rectangle(0, 0, img.Width / 2, img.Height / 2);

        // Place the cropped (full‑image here) and resized picture onto the page
        pdfPage.AddImage(imageStream, sourceRectangle, destinationRectangle);

        // Save the PDF
        pdfDocument.Save("YOUR_DIRECTORY/CroppedImage.pdf");

        Console.WriteLine("PDF created successfully!");
    }
}
```

> **Obs:** Ersätt `YOUR_DIRECTORY` med den faktiska mappvägen på din maskin. Koden ovan visar också hur du **create pdf from image** dynamiskt genom att läsa bildens verkliga dimensioner.

---

## Slutsats

Vi har nu gått igenom allt du behöver för att **create blank PDF page**, sedan **add image to PDF**, **crop image in PDF** och **resize image in PDF** med Aspose.Pdf för .NET. Kodsnutten är självständig, fungerar direkt och visar varför Aspose är ett starkt val för PDF‑manipulation – inga externa bildbibliotek, inga krångliga grafik‑kontexter.

Nästa steg kan vara att lägga till textanteckningar, generera tabeller eller slå ihop flera PDF‑filer. Alla dessa uppgifter följer samma mönster: börja med en **blank PDF page**, och bygg sedan upp innehållet lager för lager.

Har du någon twist du är nyfiken på? Lämna en kommentar så fortsätter vi diskussionen. Lycka till med kodandet!  

![Skapa tom PDF‑sida med beskuren bild med C#](https://example.com/placeholder-image.png "Skapa tom PDF‑sida med beskuren bild med C#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}