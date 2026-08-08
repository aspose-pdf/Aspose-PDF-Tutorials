---
category: general
date: 2026-04-06
description: Skapa PDF från JPG snabbt och lär dig hur du beskär en bild i PDF, lägger
  till en ny PDF-sida och konverterar JPG till PDF med beskärning med C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: sv
og_description: Skapa PDF från JPG och beskära bild i PDF med C#. Lär dig hur du lägger
  till en ny PDF-sida och konverterar JPG till PDF med beskärning.
og_title: Skapa PDF från JPG i C# – Steg‑för‑steg guide
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Skapa PDF från JPG i C# – Fullständig guide med beskärning och nya sidor
url: /sv/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF från JPG i C# – Fullständig guide med beskärning och nya sidor

Har du någonsin behövt **create PDF from JPG** men varit osäker på hur du behåller bara den del du faktiskt vill ha? Du är inte ensam. I många appar—tänk fakturor, kvitton eller fotoböcker—måste utvecklare omvandla en bild till en PDF samtidigt som de kastar bort de oönskade kanterna.  

I den här handledningen går vi igenom en komplett, färdigkörbar lösning som **creates PDF from JPG**, visar dig hur du **crop image in PDF**, och demonstrerar **how to add new pdf page** när du behöver mer än en bild. I slutet kommer du också att veta hur du **convert JPG to PDF with crop** och **insert image into PDF C#** med Aspose.Pdf‑biblioteket.

## Vad du kommer att lära dig

- Ställ in Aspose.Pdf i ett .NET‑projekt (ingen tung konfiguration krävs).  
- Läs in en JPEG, definiera området du vill behålla, och beskära den samtidigt som du infogar den i en PDF‑sida.  
- Lägg till ytterligare sidor i samma dokument, så att du kan bygga flersidiga PDF‑filer från många bilder.  
- Spara den slutgiltiga filen och verifiera resultatet.  

**Förutsättningar:** .NET 6+ (eller .NET Framework 4.6+), Visual Studio 2022 eller någon annan editor du föredrar, och ett NuGet‑referens till `Aspose.Pdf`. Inga andra externa tjänster behövs.

![Create PDF from JPG example](image.jpg){: .align-center alt="Exempel på att skapa PDF från JPG som visar en beskuren bild placerad på en PDF‑sida"}

---

## Steg 1: Installera Aspose.Pdf och förbered ditt projekt

Först och främst—lägg till Aspose.Pdf‑paketet. Öppna en terminal i din lösningsmapp och kör:

```bash
dotnet add package Aspose.Pdf
```

Den enda raden hämtar allt du behöver: klasserna `Document`, `Rectangle` och `Page` som vi kommer att använda senare. Enligt min erfarenhet är NuGet‑vägen det renaste sättet att hålla sig uppdaterad utan att pilla med DLL‑filer.

> **Proffstips:** Om du riktar dig mot .NET Framework, använd paketet `Aspose.Pdf.NET` istället; API‑ytan är identisk.

---

## Steg 2: Läs in JPEG‑filen och definiera sidstorleken

Vi behöver en canvas som matchar de dimensioner vi vill ha för den slutgiltiga PDF‑sidan. Koden nedan skapar ett nytt `Document` och öppnar källbilden som en ström.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Varför en rektangel? I Aspose.Pdf representerar en `Rectangle` både sidans dimensioner och området av bilden du vill visa. Genom att separera *sidan* från *beskärningsområdet* får du finjusterad kontroll över vad som hamnar i PDF‑filen.

---

## Steg 3: Välj beskärningsområdet (övre‑vänstra kvarten)

Anta att du bara behöver den övre‑vänstra kvarten av fotot. Vi beräknar det området relativt till sidans storlek:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

`Rectangle`‑konstruktorn tar **nedre‑vänster X/Y** och **övre‑höger X/Y**‑värden. Genom att lägga till halva höjden till `LLY` flyttar vi beskärningens botten uppåt, vilket effektivt kastar bort den nedre halvan av bilden. Justera dessa beräkningar om du behöver en annan del.

> **Varför beskära innan du lägger till?**  
> Beskärning på PDF‑sidan undviker att skapa en temporär bitmap på disk, vilket sparar både I/O och minne. Aspose hanterar matematiken åt dig, och resultatet blir en ren, vektorgynnsam PDF.

---

## Steg 4: Lägg till en ny sida och infoga den beskurna bilden

Nu placerar vi faktiskt bilden på en PDF‑sida. Det är här nyckelordet **how to add new pdf page** kommer till sin rätt.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` tar tre argument:

1. **Stream** – käll‑JPEG‑filen.  
2. **Page rectangle** – definierar sidans storlek (vår `pageBounds`).  
3. **Crop rectangle** – talar om för Aspose vilken del av bilden som ska renderas.

Om du behöver fler sidor, upprepa helt enkelt `Add` + `AddImage`‑mönstret med ett nytt `imageStream` varje gång. Detta uppfyller kravet **how to add new pdf page** samtidigt som koden hålls prydlig.

---

## Steg 5: Spara PDF‑filen och verifiera resultatet

Det sista steget är en enradare, men underskatta det inte—att spara till rätt sökväg säkerställer att filen kan öppnas av vilken PDF‑visare som helst.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

När du öppnar `cropped_image.pdf` bör du se en enda sida som bara innehåller den övre‑vänstra kvarten av den ursprungliga JPEG‑filen, perfekt centrerad inom 600 × 800‑sidan.

---

## Fullständigt fungerande exempel (alla steg kombinerade)

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i en konsolapp. Det kompilerar som det är, förutsatt att du har installerat Aspose.Pdf och placerat en JPEG på den angivna platsen.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Förväntad utdata

- **Fil:** `cropped_image.pdf` (≈ 30 KB).  
- **Innehåll:** En sida, 600 × 800 punkter, som visar den övre‑vänstra kvarten av `photo.jpg`.  
- **Beteende:** Ingen förvrängning; bilden behåller sin ursprungliga upplösning inom de beskurna gränserna.

---

## Vanliga frågor & specialfall

### Vad händer om jag vill behålla hela bilden, inte bara en kvartsdel?

Ställ helt enkelt in `cropArea` lika med `pageBounds`:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### Kan jag använda en annan sidstorlek (t.ex. A4)?

Absolut. Ersätt `pageBounds`‑värdena med dimensionerna för en A4‑sida i punkter (595 × 842):

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

Beskärningsrektangeln kan förbli densamma eller omberäknas för att matcha det nya bildförhållandet.

### Hur lägger jag till flera bilder, var och en på sin egen sida?

Loopa över en samling av filsökvägar:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### Vad händer med transparens eller PNG‑bilder?

Aspose.Pdf behandlar PNG på samma sätt som JPEG. Om källan har en alfakanal kommer PDF‑filen att bevara den, förutsatt att PDF‑versionen stödjer transparens (standard är okej).

### Fungerar detta på .NET Core på Linux?

Ja. Aspose.Pdf är plattformsoberoende; se bara till att `imageStream` pekar på en giltig filsökväg på mål‑OS:et. Inga Windows‑specifika API:er används.

---

## Tips & bästa praxis

- **Memory Management:** Wrappa alltid strömmar i `using`‑satser (som visat) för att undvika fil‑lås.  
- **Performance:** Om du bearbetar dussintals bilder, överväg att återanvända en enda `Document`‑instans och anropa `pdfDocument.Pages.Add()` för varje bild.  
- **Error Handling:** Omge hela rutinen med ett `try/catch`‑block och logga `PdfException` för felsökning.  
- **Quality Control:** Aspose.Pdf låter dig sätta bildens upplösning via `ImageFragment`. För hög‑dpi‑skanningar, sätt `ImageFragment.Resolution = 300;`.  
- **Security:** Om PDF‑filen ska delas externt kan du lägga till kryptering med `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

---

## Slutsats

Vi har precis gått igenom hur man **create PDF from JPG** i C#, **crop image in PDF**, och **add new PDF page** för att bygga flersidiga dokument. Samma mönster låter dig **convert JPG to PDF with crop** och **insert image into PDF C#** för alla scenarier—från enkla kvitton till komplexa fotoböcker.  

Prova det: byt ut beskärningslogiken, experimentera med A4‑sidor, eller kedja flera bilder tillsammans. Aspose.Pdf‑biblioteket gör dessa uppgifter smärtfritt, och koden ovan är en solid, citeringsvärd referens som du kan klistra in i vilket projekt som helst.

---

### Vad blir nästa steg?

- **Add text annotations** till PDF‑filen (t.ex. bildtexter under varje bild).  
- **Create a table of contents** automatiskt för flersidiga PDF‑filer.  
- **Merge multiple PDFs** med `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

Var och en av dessa ämnen bygger på de grunder du just behärskat, så du är väl förberedd att utforska dem

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}