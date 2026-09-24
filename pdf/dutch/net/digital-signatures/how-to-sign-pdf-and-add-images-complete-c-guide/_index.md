---
category: general
date: 2026-03-29
description: Hoe PDF te ondertekenen met een digitale handtekening en een bijgesneden
  afbeelding toe te voegen in C#. Leer hoe je een digitale handtekening aan een PDF
  toevoegt, een afbeelding bijsnijdt voor een PDF, en eenvoudig een afbeelding aan
  een PDF toevoegt.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: nl
og_description: Hoe een PDF te ondertekenen met een digitale handtekening en een bijgesneden
  afbeelding in te sluiten met Aspose.Pdf in C#. Volg deze gids voor een volledige
  oplossing.
og_title: Hoe PDF te ondertekenen en afbeeldingen toe te voegen – Stapsgewijze C#‑handleiding
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hoe PDF te ondertekenen en afbeeldingen toe te voegen – Complete C#‑gids
url: /nl/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PDF ondertekenen en afbeeldingen toevoegen – Complete C# gids

Heb je je ooit afgevraagd **hoe je PDF**‑bestanden programmatically kunt ondertekenen terwijl je ook een aangepaste afbeelding invoegt? Misschien bouw je een goedkeuringsworkflow en heb je een juridisch bindende handtekening *en* een miniatuur van de foto van de ondertekenaar op dezelfde pagina nodig. Kortom, je wilt **add digital signature pdf**‑inhoud toevoegen, die afbeelding bijsnijden, en vervolgens **add image to pdf** zonder moeite.  

Deze tutorial leidt je stap voor stap – van het laden van een ECDSA PKCS#7‑certificaat tot het bijsnijden van een JPEG en het stempelen ervan op de ondertekende pagina. Aan het einde heb je één enkel, uitvoerbaar C#‑bestand dat pagina 1 ondertekent, een foto bijsnijdt tot 400 × 400 px, en deze op een precieze locatie plaatst. Geen externe scripts, geen toverspreuken, alleen heldere code en uitleg.

## Prerequisites

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+)
- **Aspose.Pdf for .NET** NuGet‑package (versie 23.9 of nieuwer)
- Een ECDSA P‑256‑certificaat in PKCS#7 (`.pfx`)‑formaat en het bijbehorende wachtwoord
- Een JPEG‑afbeelding die je wilt insluiten (bijv. `photo.jpg`)

> **Pro tip:** Houd je certificaatbestand buiten versiebeheer en bescherm het wachtwoord met een secret manager.

---

## Step 1: Set Up the Project and Imports

First, create a console app (or integrate this into any existing service). Add the Aspose.Pdf reference:

```bash
dotnet add package Aspose.Pdf
```

Then include the required namespaces:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

These `using` statements give you access to the `Document`, `Signature`, and `Rectangle` classes we’ll need later.

## Step 2: Load the PDF and Prepare the Signature

We’ll open an existing PDF (`source.pdf`) and create a **digital signature pdf** object that uses a PKCS#7 detached signature. The certificate is an ECDSA P‑256 key, which is widely accepted for compliance.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Why this matters:** Using a detached PKCS#7 signature keeps the original PDF content intact while embedding a cryptographic hash. This is the industry‑standard approach for legally‑binding PDFs.

## Step 3: Apply the Digital Signature to a Specific Page

Now we’ll place the visible signature field on **page 1**. The rectangle defines where the signature box appears (coordinates are in points, where 1 inch = 72 points).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

If you don’t need a visible box, set `isVisible` to `false`. The `signatureRect` can be adjusted to match your document layout.

## Step 4: Open the Image Stream and Define Crop Areas

We’ll read the JPEG file into a stream and specify a **source rectangle** that selects the top‑left 400 × 400 pixels. This is the **crop image for pdf** operation.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Edge case:** If your image is smaller than 400 × 400, the crop will automatically clamp to the image’s actual dimensions—no exception is thrown.

## Step 5: Define Where the Cropped Image Should Appear

Next, set the **destination rectangle** on the PDF page. In this example we place the image at (50, 50) with a size of 200 × 200 points (≈2.78 inches square).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

Feel free to experiment: change the X/Y coordinates to move the picture, or adjust width/height for scaling.

## Step 6: Insert the Cropped Image onto the Signed Page

Finally, we add the image to **page 1** (the same page that now carries the signature). The `AddImage` overload we use accepts the source and destination rectangles, effectively performing the crop and placement in one call.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

Behind the scenes, Aspose.Pdf extracts the 400 × 400 pixel region, rescales it to 200 × 200 points, and writes it into the PDF content stream.

## Step 7: Save the Signed and Image‑Enhanced PDF

After all modifications, persist the document. You can overwrite the original or write to a new file.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

When you open `output_signed.pdf` in Adobe Acrobat or any PDF viewer, you’ll see:

- A visible signature field at the coordinates you specified.
- The cropped photo placed at (50, 50) on page 1.
- The digital signature validated (provided the viewer trusts your certificate).

---

## Frequently Asked Questions (FAQ)

| Vraag | Antwoord |
|-------|----------|
| **Kan ik een andere pagina ondertekenen?** | Verander het `pageNumber`‑argument in `signature.Sign` naar elk geldig paginanummer (1‑gebaseerd). |
| **Wat als ik meerdere handtekeningen nodig heb?** | Maak voor elke pagina of locatie een nieuwe `Signature`‑instantie, en hergebruik dezelfde `pkcsSignature` als hetzelfde certificaat geldt. |
| **Is het bijsnijden van de afbeelding beperkt tot rechthoeken?** | Ja, `AddImage` van Aspose.Pdf werkt met rechthoekige regio’s. Voor complexe vormen moet je de afbeelding vooraf bewerken (bijv. met System.Drawing) voordat je deze insluit. |
| **Hoe maak ik de handtekening onzichtbaar?** | Zet `isVisible` op `false` en laat `signatureRect` weg. De handtekening blijft cryptografisch geldig. |
| **Welke formaten kan ik naast JPEG insluiten?** | PNG, BMP, GIF en TIFF worden allemaal ondersteund. Pas gewoon het bestandspad aan en zorg dat de stream de juiste bytes leest. |

---

## Full Working Example

Below is the complete, self‑contained program. Copy‑paste it into `Program.cs`, adjust the paths, and run.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Expected result:** Opening `output_signed.pdf` shows a signature field (100 × 100 → 300 × 300 points) and a 200 × 200‑point picture derived from the top‑left corner of `photo.jpg`. The signature validates against the supplied ECDSA certificate.

---

## Wrapping Up

We’ve covered **how to sign PDF** files, how to **add digital signature pdf** to a specific page, how to **crop image for pdf**, and finally how to **add image to pdf** using Aspose.Pdf in C#. The whole flow—from loading the certificate to saving the final document—fits into a single, easy‑to‑read source file.

If you’re ready for the next challenge, consider:

- Adding **multiple signatures** on different pages (use the “digital signature pdf page” concept).
- Embedding **QR codes** that link to verification services.
- Automating the process in an ASP.NET Core API for on‑the‑fly PDF generation.

Remember, the key to robust PDF automation is clear separation of concerns: signature handling, image processing, and final document assembly. Play with the coordinates, swap out the image format, or experiment with timestamping—your workflow is now fully extensible.

Got questions, edge‑case scenarios, or a cool use‑case to share? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}