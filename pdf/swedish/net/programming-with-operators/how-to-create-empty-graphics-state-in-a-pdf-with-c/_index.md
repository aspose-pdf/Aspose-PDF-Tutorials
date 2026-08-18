---
category: general
date: 2026-08-17
description: Skapa ett tomt grafikstatus i en PDF med C# och Aspose.Pdf. Följ den
  här steg‑för‑steg‑guiden för att säkert redigera ExtGState‑resurser.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: sv
lastmod: 2026-08-17
og_description: Skapa ett tomt grafikläge i en PDF med C#. Denna handledning visar
  hur du redigerar ExtGState‑resurser med Aspose.Pdf för pålitliga PDF‑modifieringar.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Skapa tomt grafikläge i PDF med C# – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hur man skapar ett tomt grafikstatus i en PDF med C#
url: /sv/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar ett tomt grafikstillstånd i en PDF med C#

Om du behöver **skapa ett tomt grafikstillstånd** i en PDF visar den här guiden exakt hur du gör det med C# och Aspose.Pdf. Du får ett komplett, körbart exempel som lägger till en ny post i sidans ExtGState‑ordbok utan att påverka befintligt innehåll.

Att arbeta med PDF‑grafikstillstånd är ett vanligt krav när du vill kontrollera transparens, blandningslägen eller andra renderingsparametrar på objekt‑nivå. Koden nedan demonstrerar den rekommenderade metoden, förklarar varför varje steg är viktigt och tar upp typiska variationer du kan stöta på.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare (exemplet kompileras även med .NET Core).
* En Aspose.Pdf for .NET‑licens (eller en tillfällig evalueringsnyckel).
* En mapp som innehåller en `input.pdf`‑fil du vill modifiera.
* Grundläggande kunskap om C#‑syntax och PDF‑koncept som resurser‑ordböcker.

## Steg 1: Ställ in projektet och importera namnrymder

Skapa ett nytt konsolprogram eller integrera koden i ett befintligt projekt. Lägg till Aspose.Pdf‑NuGet‑paketet:

```bash
dotnet add package Aspose.Pdf
```

Importera sedan de nödvändiga namnrymderna:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Dessa importeringar ger dig åtkomst till `Document`, `DictionaryEditor` och PDF‑primitiva klasser som behövs för att **skapa ett tomt grafikstillstånd**.

## Steg 2: Definiera mappen som innehåller PDF‑filerna

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Byt ut sökvägen mot platsen för dina egna PDF‑filer. Att hålla katalogen i en variabel gör koden återanvändbar och enklare att testa.

## Steg 3: Läs in källdokumentet

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Att öppna dokumentet inom ett `using`‑statement säkerställer att filhandtaget frigörs automatiskt efter att du har sparat ändringarna.

## Steg 4: Åtkomst till den första sidan och dess Resources‑ordbok

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` hämtar den första sidan (PDF‑sidnummer börjar på 1).
* `DictionaryEditor` ger ett bekvämt sätt att läsa och modifiera PDF‑ordböcker.
* `ExtGState`‑posten innehåller alla grafik‑tillståndsobjekt för sidan. Om nyckeln saknas skapar Aspose.Pdf automatiskt en tom ordbok.

## Steg 5: Bygg en ny tom grafik‑tillståndsordbok

Grafik‑tillståndet du lägger till kan vara tomt eller förifyllt med parametrar som opacitet (`CA`, `ca`) eller blandningsläge (`BM`). I den här handledningen skapar vi ett **tomt grafikstillstånd** och sätter sedan några typiska värden för att illustrera hur ordboken fungerar.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` skapar en ren behållare som du kan fylla med vilka grafik‑tillståndsnycklar som helst.
* Att lägga till `CA`, `ca` och `BM` är valfritt; du kan utelämna dem om du verkligen behöver ett tomt tillstånd. Koden visar hur du lägger till poster när du senare vill styra rendering.

## Steg 6: Infoga det nya grafik‑tillståndet i ExtGState‑ordboken

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Att namnge posten `"GS0"` följer den vanliga konventionen att prefixa grafik‑tillståndsnamn med “GS”. Du kan välja vilket giltigt PDF‑namn som helst så länge det inte kolliderar med befintliga nycklar.

## Steg 7: Spara det modifierade PDF‑dokumentet

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

`Save`‑anropet skriver den uppdaterade filen till `output.pdf`. När du öppnar den här filen i en PDF‑visare bekräftas att det nya grafik‑tillståndet finns; du kan referera till det senare med `gs`‑operatorn i innehållsströmmar.

### Fullständig källkod

När allt sätts ihop ser det kompletta programmet ut så här:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

När programmet körs skrivs en bekräftelsesats ut och `output.pdf` skapas med det nyss tillagda grafik‑tillståndet.

## Varför denna metod fungerar bäst

* **Direkt ordboksredigering** – Med `DictionaryEditor` undviker du att behöva parsra hela innehållsströmmen. Du modifierar bara de resurser du bryr dig om.
* **Typade PDF‑primitiver** – `CosPdfNumber`, `CosPdfName` och `CosPdfDictionary` garanterar att den genererade PDF‑filen följer PDF 1.7‑specifikationen.
* **Säkerhet** – `using`‑blocket disponerar `Document`‑objektet, vilket förhindrar fil‑lås som kan korrupta efterföljande byggen.
* **Utbyggbarhet** – När det tomma grafik‑tillståndet finns kan du referera till det från vilken innehållsoperator (`gs`) som helst för att ändra opacitet, blandningsläge eller andra parametrar för valda ritkommandon.

## Vanliga variationer och kantfall

| Situation | Rekommenderad justering |
|-----------|------------------------|
| **Flera sidor** | Loopa över `pdfDocument.Pages` och upprepa ordboksinsättningen för varje sida du behöver modifiera. |
| **Ingen befintlig ExtGState‑post** | `resourcesEditor["ExtGState"]` skapar automatiskt en tom ordbok om den saknas. Ingen extra kod behövs. |
| **Annat grafik‑tillståndsnamn** | Byt ut `"GS0"` mot ett namn som matchar din namngivningskonvention, t.ex. `"MyTransparentState"`. |
| **Endast ett tomt tillstånd** | Utelämna `parameters`‑arrayen och `foreach`‑loopen; ordboken förblir tom. |
| **Arbeta med krypterade PDF‑filer** | Ange lösenordet när du konstruerar `new Document(path, password)` innan du redigerar resurser. |

## Verifiera resultatet

Du kan verifiera att grafik‑tillståndet har lagts till genom att inspektera PDF‑filen med en låg‑nivå‑visare som **PDF‑Tron** eller **iText Sharp**. Leta efter en post liknande:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Om posten visas har **skapa tomt grafikstillstånd**‑operationen lyckats.

## Slutsats

Du vet nu hur du **skapar ett tomt grafikstillstånd** i en PDF med C# och Aspose.Pdf. Handledningen gick igenom varje steg – från att läsa in dokumentet till att redigera `ExtGState`‑ordboken och spara resultatet – samtidigt som den förklarade motivet bakom varje åtgärd.  

Härifrån kan du:

* Använda det nya grafik‑tillståndet i innehållsströmmar (`gs /GS0`).
* Experimentera med ytterligare nycklar som `/SM` (stroke‑justering) eller `/OPM` (overprint‑läge).
* Tillämpa samma teknik på andra resurstyp‑er som `/XObject` eller `/ColorSpace`.

Lycka till med PDF‑hackandet, och utforska gärna andra **Aspose PDF graphics state**‑scenarier såsom dynamiska opacitetsändringar eller anpassade blandningslägen!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}