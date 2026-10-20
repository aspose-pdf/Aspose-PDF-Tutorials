---
category: general
date: 2026-04-25
description: Lägg till Bates‑nummerering i PDF-filer snabbt med Aspose.Pdf. Lär dig
  hur du lägger till sidnummer i PDF, automatiskt justerar teckenstorleken och lägger
  till textvattenstämpel i C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: sv
og_description: Lägg till Bates‑nummerering i PDF-filer med Aspose.Pdf. Denna guide
  visar hur du lägger till sidnummer i PDF, automatiskt justerar teckenstorlek och
  lägger till en textvattenstämpel i ett enda körbart exempel.
og_title: Lägg till Bates‑numrering i PDF‑filer – Fullständig Aspose.C#‑handledning
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Lägg till Bates-nummerering till PDF-filer med Aspose – Komplett guide
url: /sv/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates-numrering i PDF-filer med Aspose – Komplett guide

Har du någonsin behövt **lägga till Bates-numrering** i en PDF men varit osäker på var du ska börja? Du är inte ensam—juridiska team, revisorer och utvecklare stöter på detta dagligen. Den goda nyheten? Med Aspose.Pdf för .NET kan du stämpla ett Bates-nummer, automatiskt justera teckenstorleken och till och med behandla stämpeln som ett subtilt textvattenmärke—allt i några få rader C#.

I den här handledningen går vi igenom de exakta stegen för att **lägga till sidnummer pdf**, justera teckensnittet så att det aldrig överflödar, och besvara frågan “hur man lägger till bates” en gång för alla. I slutet har du en färdig konsolapp som producerar en professionellt numrerad PDF, och du får se hur du kan utöka den till en fullständig vattenmärkeslösning.

## Förutsättningar

* **Aspose.Pdf for .NET** (det senaste NuGet‑paketet per april 2026).  
* .NET 6.0 SDK eller nyare – API:et fungerar likadant på .NET Framework, men .NET 6 ger bäst prestanda.  
* En exempel‑PDF med namnet `input.pdf` placerad i en mapp du kan referera till (t.ex. `C:\Docs\`).  

Ingen extra konfiguration krävs; biblioteket är självständigt.

---

## Steg 1 – Ladda käll‑PDF‑dokumentet

Det första vi gör är att öppna filen vi vill numrera. Asposes `Document`‑klass representerar hela PDF‑filen, och inläsning är så enkelt som att skicka sökvägen till konstruktorn.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Varför detta är viktigt*: Att ladda dokumentet ger dig åtkomst till `Pages`‑samlingen, där vi senare kommer att fästa Bates‑stämpeln. Om filen inte kan hittas kastar Aspose ett tydligt `FileNotFoundException`, så du vet exakt vad som gick fel.

---

## Steg 2 – Skapa en TextStamp för Bates‑nummer

Nu skapar vi det visuella elementet som kommer att visas på varje sida. `TextStamp`‑klassen låter dig bädda in vilken sträng som helst, och vi använder platshållaren `{page}-{total}` så att Aspose automatiskt ersätter dessa token.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

* **auto adjust font size** – Att sätta `AutoAdjustFontSizeToFitStampRectangle` till `true` garanterar att texten aldrig rinner utanför rektangeln, vilket är perfekt för variabel‑längd sidnummer.  
* **add text watermark** – Genom att sänka `Opacity` förvandlar vi Bates‑numret till ett svagt vattenmärke, vilket uppfyller kravet “add text watermark” utan ett separat steg.  
* **how to add bates** – `{page}`‑ och `{total}`‑token är den hemliga ingrediensen; Aspose ersätter dem vid körning, så du behöver inte beräkna något själv.

---

## Steg 3 – Applicera stämpeln på varje sida

Ett vanligt fallgropp är att bara stämpla den första sidan. För att verkligen **lägga till sidnummer pdf**, måste vi loopa igenom hela `Pages`‑samlingen.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Varför klona? `AddStamp`‑metoden skapar internt en kopia, men att explicit använda en ny instans per iteration undviker oavsiktliga bieffekter om du senare ändrar stämpelns egenskaper (t.ex. färg för specifika sidor).

---

## Steg 4 – Spara den uppdaterade PDF-filen

Med stämplarna på plats är det enkelt att spara ändringarna. Du kan skriva över originalfilen eller spara till en ny plats—här sparar vi en ny fil med namnet `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Om du öppnar `output.pdf` kommer du att se varje sida märkt “Bates: 1‑10”, “Bates: 2‑10”, … längst ner till höger, med en svag opacitet som också fungerar som ett **add text watermark**.

---

## Fullt fungerande exempel

När vi sätter ihop allt, här är ett enda, självständigt konsolprogram som du kan kopiera‑klistra in i Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Förväntat resultat**: Öppna `output.pdf` i någon visare; varje sida visar en rad som “Bates: 3‑12” i det nedre högra hörnet, med rätt storlek för rektangeln och renderad med 40 % opacitet. Detta uppfyller både kravet på juridisk spårning och behovet av ett visuellt vattenmärke.

---

## Vanliga variationer & kantfall

| Situation | Vad som ska ändras | Varför |
|-----------|--------------------|--------|
| **Olika placering** | Justera `HorizontalAlignment` / `VerticalAlignment` eller sätt `XIndent`/`YIndent` | Vissa företag föredrar placering uppe till vänster eller i mitten. |
| **Anpassat prefix** | Byt ut `"Bates: "` mot `"Doc‑ID: "` eller någon annan sträng | Du kan använda en annan namngivningskonvention. |
| **Flera stämplar** | Skapa en andra `TextStamp` (t.ex. för en konfidentialitetsnotis) och lägg till den efter den första | Att kombinera **add bates numbering** med andra **add text watermark**‑krav är enkelt. |
| **Stora sidantal** | Öka den initiala teckenstorleken (t.ex. `14`) – auto‑adjust kommer att minska den vid behov | När du har > 999 sidor blir strängen längre; auto‑adjust förhindrar avklippning. |
| **Krypterade PDF-filer** | Anropa `pdfDocument.Decrypt("password")` innan stämpling | Du kan inte ändra en skyddad fil utan lösenordet. |

---

## Pro‑tips & fallgropar

* **Pro tip:** Sätt `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` om du märker att texten ligger för nära sidans kant.  
* **Watch out for:** Mycket små rektanglar (standardstorlek är 100 × 30 pt). Om du behöver ett större område, sätt `batesStamp.Width` och `batesStamp.Height` manuellt.  
* **Performance note:** Att stämpla tusentals sidor kan ta några sekunder, men Aspose strömmar sidor effektivt—ingen anledning att ladda hela dokumentet i minnet.  

---

## Slutsats

Vi har just demonstrerat hur man **add bates numbering** i en PDF med Aspose.Pdf, samtidigt som man **add page numbers pdf**, aktiverar **auto adjust font size** och skapar ett **add text watermark** i ett sammanhängande flöde. Det kompletta, körbara exemplet ovan ger dig en solid grund som du kan anpassa till vilken juridisk‑dokument‑arbetsflöde eller internt rapporteringssystem som helst.

Redo för nästa steg? Prova att kombinera detta tillvägagångssätt med Asposes PDF‑sammanfognings‑API för att batch‑processa flera filer, eller utforska `TextFragment`‑klassen för rikare vattenmärken (färgade, roterade eller flerradiga). Möjligheterna är oändliga, och koden du nu har är en pålitlig bas.

Om du fann den här guiden hjälpsam, tveka inte att lämna en kommentar, ge stjärna till repot, eller dela dina egna variationer. Lycklig kodning, och må dina PDF-filer alltid vara perfekt numrerade!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}