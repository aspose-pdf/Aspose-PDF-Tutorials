---
category: general
date: 2026-06-08
description: Beskär bild i PDF med Aspose.PDF i C#. Lär dig hur du skapar PDF med
  bild, sparar PDF med bild och lägger till bild i PDF på bara några rader.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: sv
og_description: Beskär bild i PDF med Aspose.PDF i C#. Den här handledningen visar
  hur du skapar PDF med bild, sparar PDF med bild och lägger till bild i PDF snabbt.
og_title: Beskär bild i PDF med Aspose.PDF – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Beskär bild i PDF med Aspose.PDF – Komplett guide
url: /sv/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Beskär bild i PDF med Aspose.PDF – Komplett guide

Har du någonsin undrat hur du **crop image in PDF** utan att ta fram ett grafikprogram? Du är inte ensam. I många rapporter, fakturor eller e‑böcker behöver du bara en del av en bild—kanske logots hörn eller ett diagramfragment—och du vill ha den direkt i PDF:en.  

Den här guiden visar exakt det: vi kommer att **create PDF with image**, **add image to PDF**, och sedan **crop image in PDF** med hjälp av Aspose.PDF‑biblioteket för C#. I slutet kommer du också att veta hur du **save PDF with image** så att du kan skicka filen till vem som helst.

---

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)  
- En licensierad eller provversion av **Aspose.PDF for .NET** (installera via NuGet `Install-Package Aspose.PDF`)  
- En bildfil (JPEG/PNG) på disk – vi kallar den `image.jpg`  
- Valfri IDE du föredrar (Visual Studio, Rider, VS Code)

Det är allt. Inga extra tjänster, inga externa verktyg.

---

## Steg 1: Ställ in projektet och importerna

Först, skapa en konsolapp och importera de namnrymder vi kommer att använda. `using`‑satserna håller koden prydlig och gör de senare stegen lättare att läsa.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Proffstips:** Om du använder Visual Studio, högerklicka på projektet → *Manage NuGet Packages* → sök efter “Aspose.PDF” och installera. Biblioteket hanterar både bildplacering och beskärning internt, så du behöver inga tredjeparts‑bildbibliotek.

---

## Steg 2: Skapa PDF med bild

Nu skapar vi faktiskt **create pdf with image**. Kodsnutten nedan bygger ett nytt `Document`, lägger till en tom sida och förbereder en bildström.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

När du kör den här koden får du en PDF med hela bilden utsträckt till de dimensioner du angav. Det är en bra kontroll innan du börjar trimma.

---

## Steg 3: Hur man lägger till bild i PDF (och förbereder beskärning)

Om du redan vet exakt vilken region du vill ha, kan du hoppa över steget med full storlek och gå direkt till delen **how to add image to pdf**. Metoden `AddImage` accepterar tre parametrar:

1. **Image stream** – de råa bytena av din bild.  
2. **Placement rectangle** – var på sidan bilden placeras.  
3. **Crop rectangle** – den del av bilden du faktiskt vill rendera.

Nedan är den kompakta versionen som gör både placering **och** beskärning i ett anrop.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Varför detta fungerar:** Aspose.PDF mappar internt beskärningsrektangeln till bildens pixel-dimensioner och renderar sedan bara den delen inom `placement`‑området. Ingen extra bitmap‑behandling krävs, vilket betyder att du håller PDF‑storleken liten.

---

## Steg 4: Hur man beskär bild‑PDF – Avancerade alternativ

Ibland räcker inte kvartsbeskärningen. Kanske behöver du en anpassad rektangel eller vill bevara bildens bildförhållande. Här är ett mer flexibelt tillvägagångssätt:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Hantering av kantfall:**  
- **Null streams** – omslut alltid `FileStream` i ett `using`‑block, som visat, för att undvika läckor.  
- **Large images** – om källbilden är enorm, överväg att skala ner `placement`‑rektangeln; Aspose kommer automatiskt att nedskalera.  
- **Transparent PNGs** – biblioteket respekterar alfa‑kanaler, så ditt beskurna område behåller transparens.

---

## Steg 5: Spara PDF med bild (och verifiera)

Till sist **save pdf with image**. Metoden `Save` skriver dokumentet till disk. Du kan också strömma tillbaka det till en webbklient om du bygger ett API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

När du öppnar `output.pdf` bör du bara se den beskurna delen av `image.jpg` placerad exakt där du definierade den. Om bilden ser utdragen ut, justera `placement`‑rektangelns bredd/höjd så att den matchar bildförhållandet för beskärningsrektangeln.

---

## Vanliga frågor & fallgropar

| Fråga | Svar |
|----------|--------|
| **Kan jag beskära flera bilder på samma sida?** | Absolut. Anropa `page.AddImage` för varje bild med sina egna placerings- och beskärningsrektanglar. |
| **Vad händer om min bild är i ett annat format (t.ex. BMP)?** | Aspose.PDF stödjer JPEG, PNG, BMP, GIF och TIFF direkt. Byt bara filändelsen. |
| **Behöver jag en licens för produktionsbruk?** | En provversion fungerar för upp till 5 sidor. För verkliga distributioner, köp en licens för att ta bort vattenstämpeln. |
| **Hur roterar jag den beskurna bilden?** | Efter att ha lagt till bilden, hämta `Image`‑objektet och sätt dess `Rotate`‑egenskap (`Rotate = RotationAngle.Rotate90`). |
| **Finns det ett sätt att beskära med procent istället för absoluta punkter?** | Ja—beräkna rektangelns dimensioner baserat på `image.Width * 0.25` osv., och konvertera sedan till punkter som visas i Steg 4. |

---

## Fullt fungerande exempel (Kopiera‑klistra redo)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Kör programmet, öppna `output.pdf`, och du kommer bara att se det övre‑vänstra kvartalet av `image.jpg` renderat i det övre‑vänstra hörnet av sidan. Ändra `crop`‑rektangelns värden för att experimentera med olika delar.

---

## Slutsats

Vi har gått igenom hela processen för **crop image in pdf** med Aspose.PDF för C#. Från ett nytt dokument, vi **create pdf with image**, demonstrerar **how to add image to pdf**, tillämpar en anpassad **how to crop image pdf**‑rektangel och slutligen **save pdf with image**.  

Nu kan du bädda in exakt beskurna bilder i vilken PDF du än genererar—perfekt för fakturor, marknadsföringsbroschyrer eller automatiserade rapporter. Nästa steg är att överväga att lägga till textbeskrivningar (`TextFragment`) eller rita former runt den beskurna bilden för att framhäva den ytterligare.  

Har du fler scenarier du är nyfiken på? Lämna en kommentar, och lycka till med kodandet!

## Vad du bör lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man ställer in bildstorlek i en PDF med Aspose.PDF för .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Hur man lägger till en bildstämpel i en PDF med Aspose.PDF för .NET&#58; En omfattande guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Hur man extraherar bildinformation från PDF:er med Aspose.PDF för .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}