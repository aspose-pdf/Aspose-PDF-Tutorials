---
category: general
date: 2026-06-24
description: Lägg till Bates‑nummerering i PDF‑filer med C# och Aspose.PDF. Lär dig
  anpassade sidnummer, sekventiella sidnummer och numrering i sidhuvud och sidfot
  på några minuter.
draft: false
keywords:
- add bates numbering
- custom page numbers
- sequential page numbers
- bates numbering pdf
- header footer numbering
language: sv
og_description: Lägg till Bates‑nummerering i PDF‑filer med C# och Aspose.PDF. Bemästra
  anpassade sidnummer samt sidhuvud‑ och sidfot‑nummerering på några enkla steg.
og_title: Lägg till Bates-nummerering i PDF-filer med C# – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  headline: Add Bates Numbering to PDFs with C# – Complete Guide
  type: TechArticle
- description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  name: Add Bates Numbering to PDFs with C# – Complete Guide
  steps:
  - name: Load the Source PDF Document
    text: First we need a `Document` object that represents the file we want to modify.
  - name: Configure Bates Numbering Options (custom page numbers)
    text: Now we set up a `BatesNumberingOptions` object. This is where you define
      **custom page numbers**, the font, colors, and margins.
  - name: Apply the Bates Numbering to the Entire Document
    text: With the options prepared, the actual insertion is a single method call.
  - name: Save the PDF with Bates Numbers Applied
    text: Finally, write the modified document back to disk.
  - name: Limiting the Page Range
    text: 'Sometimes you only want to number a subset, such as pages 3‑10 of a 25‑page
      contract. Adjust `StartingPage` and `EndingPage` accordingly:'
  - name: Changing the Placement to Footer
    text: 'If your workflow requires **header footer numbering** at the bottom left,
      tweak the `Margin`:'
  - name: Using a Different Format
    text: 'Legal teams sometimes use “2024‑A‑001”. Just change the format string:'
  - name: Handling Transparent Backgrounds
    text: The `BackgroundColor = Color.Transparent` ensures the number doesn’t obscure
      existing content. If you need a light gray box behind the text for readability,
      replace it with `Color.LightGray`.
  type: HowTo
- questions:
  - answer: Yes—load the document with the password first (`pdfDocument = new Document("file.pdf",
      new LoadOptions { Password = "pwd" })`) then apply the same steps.
    question: Will this work with password‑protected PDFs?
  - answer: You can run `AddBatesNumbering` twice with two separate `BatesNumberingOptions`,
      each targeting either odd (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count;
      PageSequence = PageSequence.Odd`) or even pages.
    question: Can I add different numbers to odd and even pages?
  - answer: A trial works for evaluation, but the trial adds a watermark. For production
      use you’ll need a valid license to get a clean **bates numbering pdf**.
    question: Do I need a license for Aspose.PDF?
  type: FAQPage
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Lägg till Bates-numrering i PDF-filer med C# – Komplett guide
url: /sv/net/programming-with-pdf-pages/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates‑nummerering i PDF‑filer med C# – Komplett guide

Lägg till Bates‑nummerering i dina PDF‑filer med C# med bara några rader kod. Om du någonsin har behövt anpassade sidnummer för juridiska handlingar eller vill ha sekventiella sidnummer i ett kontraktspaket, så täcker den här handledningen allt du behöver.

Under de kommande minuterna går vi igenom allt du behöver veta: hur du laddar en PDF, konfigurerar nummereringsstilen, applicerar numren och slutligen sparar den uppdaterade filen. När du är klar kan du generera en **bates‑nummerering pdf** som ser professionell ut, oavsett om du bearbetar en enskild fil eller en hel mapp med dokument.

## Vad du behöver

Innan vi dyker ner, se till att du har följande förutsättningar:

- **.NET 6.0 eller senare** – koden riktar sig mot .NET 6, men tidigare versioner av .NET Framework fungerar också.
- **Aspose.PDF for .NET** – ett kommersiellt bibliotek (gratis provversion finns) som tillhandahåller klasserna `Document` och `BatesNumberingOptions` som används i den här guiden.
- En **C#‑IDE** (Visual Studio, Rider eller VS Code) – vilken editor som helst som kan kompilera .NET‑projekt räcker.
- En inmatnings‑PDF med namnet `input.pdf` placerad i en mapp som du kan referera till från din kod.

Har du allt? Bra – låt oss komma igång.

## Lägg till Bates‑nummerering – Översikt

Kärnidén bakom **add bates numbering** är att behandla PDF‑filen som en canvas och sedan måla en sträng (t.ex. “DOC‑001”) på varje sidas header eller footer. Aspose.PDF sköter det tunga arbetet: du beskriver bara formatet, sidintervallet och den visuella stilen, så skriver biblioteket in numren åt dig.

Nedan är det fullständiga, körbara exemplet som du kan kopiera‑klistra in i en konsolapp. Varje rad förklaras, så du förstår både *vad* du ska skriva och *varför* varje del är viktig.

### Steg 1: Läs in källdokumentet

Först behöver vi ett `Document`‑objekt som representerar filen vi vill ändra.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

// Load the source PDF (replace the path with your actual folder)
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Varför detta är viktigt:** Klassen `Document` är startpunkten för alla PDF‑operationer. Den laddar filen i minnet och ger dig åtkomst till samlingen `Pages`, som vi senare kommer att iterera över när vi lägger till nummer.

### Steg 2: Konfigurera Bates‑nummereringsalternativ (anpassade sidnummer)

Nu skapar vi ett `BatesNumberingOptions`‑objekt. Här definierar du **custom page numbers**, teckensnitt, färger och marginaler.

```csharp
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    NumberingFormat = "DOC-{0:D3}",          // e.g., DOC-001, DOC-002 …
    StartNumber = 1,
    StartingPage = 1,
    EndingPage = pdfDocument.Pages.Count,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
    ForegroundColor = Color.Black,
    BackgroundColor = Color.Transparent,
    Margin = new Margin(0, 20, 20, 0)        // top, right, bottom, left (points)
};
```

- **NumberingFormat** – platshållaren `{0:D3}` talar om för Aspose att fylla ut siffrorna med tre tecken.
- **StartNumber** – var sekvensen börjar; ändra detta om du lägger till nummer i ett befintligt paket.
- **StartingPage / EndingPage** – definierar sidintervallet; du kan begränsa det till 2‑5 för ett delmängd, så du får **sequential page numbers** bara där du behöver dem.
- **Font & Colors** – visuell stil för **header footer numbering**; Helvetica fungerar bra för juridiska dokument eftersom det är rent och läsbart.
- **Margin** – placerar texten 20 pt från toppen och högra kanten; justera dessa värden för att flytta numret till botten eller vänster om så önskas.

> **Proffstips:** Om du vill ha numren i footern istället för headern, byt ut `Margin`‑värdena till exempelvis `new Margin(0, 0, 20, 20)` (bottom, left).

### Steg 3: Applicera Bates‑nummereringen på hela dokumentet

Med alternativen klara är själva insättningen ett enda metodanrop.

```csharp
// Apply the numbering to every page in the defined range
pdfDocument.AddBatesNumbering(batesOptions);
```

I bakgrunden itererar Aspose över de valda sidorna, formaterar varje nummer enligt `NumberingFormat` och ritar strängen på sidans canvas. Detta är hjärtat i **add bates numbering** – ingen manuell loopning behövs.

### Steg 4: Spara PDF‑filen med Bates‑nummer

Till sist skriver vi tillbaka det modifierade dokumentet till disk.

```csharp
// Save the output file (choose a different name to avoid overwriting the source)
pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");
```

När du öppnar `BatesNumbered.pdf` ser du “DOC‑001”, “DOC‑002”, … tryckt i det övre högra hörnet på varje sida. Det är en fullt funktionell **bates numbering pdf** redo för arkivering eller e‑discovery.

## Förväntat resultat

| Sida | Header (exempel) |
|------|------------------|
| 1    | DOC‑001 |
| 2    | DOC‑002 |
| …    | … |
| N    | DOC‑00N |

Numren visas exakt där `Margin` placerade dem, med Helvetica Bold 12‑pt. Om du öppnar filen i Adobe Acrobat märker du att numren är en del av sidinnehållet – inte en separat annotation – så de överlever utskrift och flattening.

## Edge Cases & Variationer

### Begränsa sidintervallet

Ibland vill du bara numrera en delmängd, t.ex. sidorna 3‑10 i ett 25‑sidigt kontrakt. Justera `StartingPage` och `EndingPage` därefter:

```csharp
batesOptions.StartingPage = 3;
batesOptions.EndingPage = 10;
batesOptions.StartNumber = 1; // reset numbering for the subset
```

### Ändra placeringen till footer

Om ditt arbetsflöde kräver **header footer numbering** längst ner till vänster, justera `Margin`:

```csharp
batesOptions.Margin = new Margin(20, 0, 0, 20); // top, right, bottom, left
```

### Använd ett annat format

Juridiska team använder ibland “2024‑A‑001”. Byt bara formatsträngen:

```csharp
batesOptions.NumberingFormat = "2024-A-{0:D3}";
```

### Hantera transparent bakgrund

`BackgroundColor = Color.Transparent` säkerställer att numret inte döljer befintligt innehåll. Om du vill ha en ljusgrå ruta bakom texten för bättre läsbarhet, ersätt den med `Color.LightGray`.

## Vanliga frågor (Svarade)

- **Fungerar detta med lösenordsskyddade PDF‑filer?**  
  Ja – ladda först dokumentet med lösenordet (`pdfDocument = new Document("file.pdf", new LoadOptions { Password = "pwd" })`) och kör sedan samma steg.

- **Kan jag lägga till olika nummer på udda och jämna sidor?**  
  Du kan köra `AddBatesNumbering` två gånger med två separata `BatesNumberingOptions`, där den ena riktar sig mot udda (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count; PageSequence = PageSequence.Odd`) och den andra mot jämna sidor.

- **Behöver jag en licens för Aspose.PDF?**  
  En provversion fungerar för utvärdering, men den lägger till ett vattenmärke. För produktionsbruk behöver du en giltig licens för att få en ren **bates numbering pdf**.

## Fullt fungerande exempel (Kopiera‑klistra redo)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Set up numbering options (custom page numbers, sequential page numbers)
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            NumberingFormat = "DOC-{0:D3}",
            StartNumber = 1,
            StartingPage = 1,
            EndingPage = pdfDocument.Pages.Count,
            Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
            ForegroundColor = Color.Black,
            BackgroundColor = Color.Transparent,
            Margin = new Margin(0, 20, 20, 0) // top, right, bottom, left
        };

        // 3️⃣ Apply the numbering (header footer numbering)
        pdfDocument.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the result
        pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Kör programmet, öppna utdatafilen och du ser numren exakt där koden instruerade Aspose att placera dem. Inga extra loopar, ingen manuell ritning – bara **add bates numbering** i fyra koncisa steg.

## Slutsats

Du har nu ett robust, produktionsklart sätt att **add bates numbering** till vilken PDF som helst med C# och Aspose.PDF. Från att läsa in dokumentet till att konfigurera **custom page numbers**, applicera **sequential page numbers** och spara en ren **bates numbering pdf**, så ryms hela arbetsflödet i ett enda metodanrop.

Vad blir nästa steg? Prova att kombinera den här tekniken med andra Aspose‑funktioner – som att stämpla en logotyp, slå ihop flera PDF‑filer eller extrahera sidor baserat på de nummer du just lagt till. Att utforska **header footer numbering** tillsammans med vattenmärken kan ge ännu mer kraftfulla resultat.

## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Add Images & Page Numbers to PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}