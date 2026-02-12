---
category: general
date: 2026-02-12
description: Lägg till Bates-nummer i PDF-filer snabbt. Lär dig hur du lägger till
  textfält i PDF, lägger till formulärfält i PDF och lägger till sidnummer i PDF med
  Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: sv
og_description: Lägg till Bates-nummer i PDF-dokument i C#. Den här guiden visar hur
  du lägger till textfält i PDF, lägger till formulärfält i PDF och lägger till sidnummer
  i PDF med Aspose.PDF.
og_title: Lägg till Bates-nummer i PDF-filer – Komplett C#-handledning
tags:
- PDF
- C#
- Aspose.PDF
title: Lägg till Bates-nummer i PDF-filer – Steg‑för‑steg C#‑guide
url: /sv/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

-bates-numbers.png "add bates numbers example")

Leave unchanged.

Then closing shortcodes.

Now produce final content with all translations.

Be careful to preserve markdown formatting exactly.

Let's construct final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates-nummer i PDF-filer – Komplett C#-guide

Har du någonsin behövt **add bates numbers** till en hög med juridiska PDF-filer men inte varit säker på var du ska börja? Du är inte ensam. På många advokatbyråer och e‑discovery‑projekt är det en daglig syssla att stämpla varje sida med en unik identifierare, och att göra det manuellt är en mardröm.  

Den goda nyheten? Med några rader C# och Aspose.PDF kan du automatisera hela processen. I den här handledningen går vi igenom **how to add bates**-nummer, strör ett textfält på varje sida och sparar en ren, sökbar PDF—utan att svettas.

> **Vad du får:** ett fullt körbart kodexempel, förklaringar till varför varje rad är viktig, tips för kantfall och en snabb checklista för att verifiera ditt resultat.  

Vi kommer också att beröra relaterade uppgifter som **add text field pdf**, **add form field pdf** och **add page numbers pdf**, så att du har en verktygslåda redo för alla dokument‑automatiseringsutmaningar.

---

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)  
- Visual Studio 2022 (eller någon annan IDE du föredrar)  
- En giltig Aspose.PDF for .NET‑licens (gratis provversion fungerar för test)  
- En käll‑PDF med namnet `source.pdf` placerad i en mapp du kan referera till  

Om någon av dessa är okänd, pausa och installera den saknade delen innan du fortsätter. Stegen nedan förutsätter att du redan har lagt till Aspose.PDF NuGet‑paketet:

```bash
dotnet add package Aspose.Pdf
```

---

## Så lägger du till bates-nummer i en PDF med Aspose.PDF

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Det laddar en PDF, skapar ett **text box field** på varje sida, skriver ett formaterat Bates‑nummer och sparar slutligen den modifierade filen.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Varför detta fungerar

- **`Document`** är ingångspunkten; den representerar hela PDF‑filen.  
- **`Rectangle`** definierar var fältet placeras på sidan. Nummerna är i punkter (1 pt ≈ 1/72 in). Justera koordinaterna om du vill ha numret i ett annat hörn.  
- **`TextBoxField`** är ett *form field* som kan hålla vilken sträng som helst. Genom att tilldela `Value` lägger vi effektivt till **add page numbers pdf** med ett eget prefix.  
- **`pdfDocument.Form.Add`** registrerar fältet i PDF‑ens AcroForm, vilket gör det synligt i visare som Adobe Acrobat.  

Om du någonsin behöver ändra utseendet (font, färg, storlek) kan du justera `TextBoxField`‑egenskaperna—se Aspose‑dokumentationen för `DefaultAppearance` och `Border`.

---

## Lägga till ett textfält på varje PDF-sida (steg “add text field pdf”)

Ibland vill du bara ha en synlig etikett, inte ett interaktivt formulärfält. I så fall kan du ersätta `TextBoxField` med ett `TextFragment` och lägga till det direkt i sidans `Paragraphs`‑samling. Här är ett snabbt alternativ:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

**add text field pdf**‑metoden är användbar när det slutgiltiga dokumentet ska vara skrivskyddat, medan **add form field pdf**‑metoden behåller numren redigerbara senare.

---

## Spara PDF-filen med Bates-nummer (ögonblicket “add page numbers pdf”)

När loopen är klar skriver ett anrop till `pdfDocument.Save` allt till disk. Om du behöver bevara originalfilen, ändra bara utskrifts‑sökvägen eller använd `pdfDocument.Save`‑overload‑metoder för att streama resultatet direkt till ett svar i ett web‑API.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Det är den smidiga delen—inga temporära filer, inga extra bibliotek, bara Aspose som hanterar den tunga lyften.

---

## Förväntat resultat & snabb verifiering

Öppna `bates.pdf` i någon PDF‑visare. Du bör se en liten ruta i det nedre vänstra hörnet på varje sida med texten:

```
BATES-00001
BATES-00002
…
```

Om du granskar dokumentegenskaperna märker du ett AcroForm som innehåller fält med namn `Bates_1`, `Bates_2` osv. Det bekräftar att **add form field pdf**‑steget lyckades.

---

## Vanliga fallgropar & proffstips

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| Numren visas off‑center | Rektangelkoordinaterna är relativa till sidans nedre‑vänstra hörn. | Vänd Y‑värdet (`pageHeight - marginTop`) eller använd `page.PageInfo.Height` för att beräkna en placering med top‑marginal. |
| Fälten är osynliga i Adobe Reader | Standardramen är satt till “No”. | Sätt `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Stora PDF-filer orsakar minnespress | `using` frigör dokumentet först efter att loopen är klar. | Processa sidor i delar eller använd `pdfDocument.Save` med `SaveOptions` som möjliggör streaming. |
| Licensen har inte tillämpats | Aspose skriver ut ett vattenmärke på första sidan. | Registrera din licens tidigt: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Utöka lösningen

- **Custom prefixes:** Ersätt `"BATES-"` med vilken sträng som helst (`"DOC-"`, `"CASE-"`, …).  
- **Zero‑padding length:** Ändra `{pageNumber:D5}` till `{pageNumber:D3}` för tre siffror.  
- **Dynamic placement:** Använd `pdfDocument.Pages[pageNumber].PageInfo.Width` för att placera fältet på högra sidan.  
- **Conditional numbering:** Hoppa över tomma sidor genom att kontrollera `pdfDocument.Pages[pageNumber].IsBlank`.

Alla dessa variationer behåller kärnmönstret **add bates numbers**, **add text field pdf** och **add form field pdf** intakt.

---

## Fullt fungerande exempel (allt-i-ett)

Nedan är det slutgiltiga, färdiga programmet som inkorporerar tipsen ovan. Kopiera det till en ny konsolapp och tryck F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Kör det, öppna resultatet, och du kommer att se en professionell identifierare på varje sida—precis vad en specialist inom litigation support förväntar sig.

---

## Slutsats

Vi har just demonstrerat **how to add bates numbers** till vilken PDF som helst med C# och Aspose.PDF. Genom att skapa ett **text box field** på varje sida lägger vi samtidigt till **add text field pdf**, **add form field pdf** och **add page numbers pdf** i ett enda pass. Metoden är snabb, skalbar och lätt att justera för egna prefix, olika layouter eller villkorlig logik.

Redo för nästa utmaning? Prova att bädda in en QR‑kod som länkar till originalfallet, eller generera en separat indexsida som listar alla Bates‑nummer med motsvarande sidtitlar. Samma API låter dig slå ihop PDF‑filer, extrahera sidor och till och med rensa känslig data—så himlen är gränsen.

Om du stöter på problem, lämna en kommentar nedan eller kolla in Asposes officiella dokumentation för djupare insikter. Lycka till med kodningen, och må dina PDF‑er alltid vara perfekt numrerade!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}