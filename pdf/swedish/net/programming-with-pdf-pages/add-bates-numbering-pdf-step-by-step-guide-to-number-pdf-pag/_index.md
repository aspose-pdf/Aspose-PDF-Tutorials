---
category: general
date: 2026-03-03
description: Lägg till Bates‑numrering i PDF snabbt och lär dig hur du numrerar PDF‑sidor
  eller lägger till sekventiella PDF‑nummer med Aspose.Pdf i C#.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: sv
og_description: Lägg till Bates‑numrering i PDF med C# för att numrera PDF‑sidor och
  lägga till sekventiella PDF‑nummer. Fullständig kod, förklaringar och bästa praxis.
og_title: Lägg till Bates-nummerering i PDF – Komplett C#‑handledning
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: Lägg till Bates-nummerering i PDF – Steg‑för‑steg guide för att numrera PDF‑sidor
url: /sv/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates-numrering PDF – Komplett C#-handledning

Har du någonsin behövt **add bates numbering pdf** filer men varit osäker på var du ska börja? Du är inte ensam—juridiska team, revisorer och arkivarier kämpar alla med samma problem. Den goda nyheten? Med några rader C# och Aspose.Pdf‑biblioteket kan du automatiskt **number pdf pages**, och du får även flexibiliteten att **add sequential pdf numbers** med anpassade prefix, suffix och placering.

I den här guiden går vi igenom ett verkligt exempel, förklarar varför varje inställning är viktig och visar hur du finjusterar koden för specialfall som olika sidstorlekar eller anpassat antal siffror. När du är klar har du ett färdigt kodexempel som lägger till Bates‑nummer på vilken PDF du än matar in, och du förstår “varför” bakom varje alternativ.

## Förutsättningar

Innan vi dyker ner, se till att du har:

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)
- En giltig Aspose.Pdf för .NET‑licens (eller en gratis utvärderingsnyckel)
- Visual Studio 2022 (eller någon annan C#‑redigerare du föredrar)
- En käll‑PDF som heter `source.pdf` i en mapp du kan referera till

Det är allt—inga extra NuGet‑paket utöver Aspose.Pdf.

## Steg 1 – Öppna källdokumentet PDF

Det första du behöver göra är att ladda PDF‑filen du vill stämpla. Att använda ett `using`‑block garanterar att filhandtaget släpps korrekt, vilket förhindrar lås‑problem senare.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Why this matters:** Att öppna dokumentet inom ett `using`‑statement säkerställer deterministisk disponering. Om du hoppar över det kan filen förbli låst, och efterföljande försök att spara eller radera PDF‑filen misslyckas—något jag har sett orsaka huvudvärk i produktionspipeline.

## Steg 2 – Konfigurera Bates‑numreringsalternativ

Nu berättar vi för Aspose hur vi vill att Bates‑numren ska se ut. Varje egenskap motsvarar direkt ett visuellt element på sidan.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### Snabba tips för alternativen

| Egenskap | Vad den gör | När du ska ändra den |
|----------|--------------|----------------------|
| **Prefix / Suffix** | Lägger till statisk text före/efter den numeriska delen. | Använd ett ärende‑ID, projektkod eller “CONF‑” för konfidentiella dokument. |
| **Start** | Det första numret i serien. | Om du fortsätter ett numreringsschema från en tidigare batch, ange detta därefter. |
| **NumberOfDigits** | Styr noll‑utfyllnad. | För juridiska inlagor behöver du ofta exakt 6 siffror; sätt till `6`. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | Välj baserat på ditt dokumentlayout; BottomRight är vanligast för Bates‑nummer. |

> **Pro tip:** Om du behöver **number pdf pages** i flera kolumner kan du anropa `pdfDocument.AddBatesNumbering` två gånger med olika `Placement`‑värden och olika `Prefix`‑strängar.

## Steg 3 – Tillämpa Bates‑numreringen på dokumentet

Med alternativen klara är den faktiska stämplingen ett enda metodanrop. Aspose hanterar paginering, rotation och marginalberäkningar internt.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Why a single call works:** Under huven itererar Aspose över `pdfDocument.Pages`, skapar ett `TextFragment` för varje sida och placerar det baserat på den `Placement` du valt. Denna abstraktion sparar dig från att skriva en manuell loop och hantera koordinat‑omvandlingar.

## Steg 4 – Spara den uppdaterade PDF‑filen

Till sist skriver du den modifierade filen till disk. Du kan skriva över originalet eller skapa en ny fil; exemplet nedan skapar en färsk kopia.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

Om du behöver **add sequential pdf numbers** till en ström (t.ex. när du skickar filen via ett API), ersätt filsökvägen med en `MemoryStream`:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## Fullt fungerande exempel

Sätter vi ihop allt får du det kompletta, färdiga programmet:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### Förväntat resultat

- En ny fil `bates_numbered.pdf` visas i `C:\MyDocs`.
- Varje sida visar något i stil med `2025-05000-A`, `2025-05001-A`, … i det nedre högra hörnet.
- Numren är noll‑utfyllda till fem siffror, i enlighet med inställningen `NumberOfDigits`.

## Hantera vanliga variationer

### 1. Olika sidstorlekar

Om din PDF blandar stående och liggande sidor kan du märka att numret klipps av på den bredare sidan. För att åtgärda detta, aktivera egenskapen `AutoFit`:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. Anpassat teckensnitt eller färg

Bates‑nummer är som standard svarta, 12‑pt Times New Roman. Ändra utseendet genom att nå `TextState`:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. Hoppa över sidor

Anta att du vill **number pdf pages** men hoppa över titelsidan. Använd ett sidintervall:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. Lägg till flera numreringsscheman

Juridiska team kräver ibland både ett Bates‑nummer och ett konfidentiellt vattenstämpel. Kör två separata `AddBatesNumbering`‑anrop med olika `Placement`‑värden:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## Vanliga frågor

**Q: Fungerar detta med PDF‑filer som redan har befintlig text?**  
A: Ja. Aspose lägger till Bates‑numret som ett separat lager, så befintligt innehåll förblir orört. Om du behöver att numren ska visas *bakom* befintlig text (sällsynt) måste du manipulera sidans innehållsströmmar manuellt.

**Q: Vad händer om PDF‑filen är lösenordsskyddad?**  
A: Ladda den först med lösenordet: `new Document(path, new LoadOptions { Password = "secret" })`. Efter stämpling kan du återapplicera kryptering via `pdfDocument.Encrypt(...)`.

**Q: Kan jag använda detta i en .NET Core‑konsolapp?**  
A: Absolut. Samma kod fungerar i .NET Core, .NET 5+ och .NET Framework. Referera bara till rätt Aspose.Pdf NuGet‑paket.

## Slutsats

Vi har precis gått igenom hur du **add bates numbering pdf** filer, hur du **number pdf pages**, och hur du **add sequential pdf numbers** med full kontroll över formatering, placering och specialfallshantering. Det korta kodexemplet ovan gör det tunga arbetet, medan de extra alternativen låter dig anpassa lösningen till vilket juridiskt, arkiv‑ eller efterlevnadsflöde som helst.

Redo för nästa steg? Prova att kombinera detta tillvägagångssätt med:

- **Batch‑behandling** – loopa igenom en mapp med PDF‑filer och applicera samma numreringsschema.
- **Dynamiska prefix** – hämta ärende‑ID:n från en databas och injicera dem per dokument.
- **PDF/A‑efterlevnad** – efter numrering, anropa `pdfDocument.Convert(..., PdfFormat.PdfA2b)` för att säkerställa långsiktig bevarande.

Känn dig fri att experimentera, dela dina resultat eller ställa frågor i kommentarerna. Lycka till med kodandet, och må dina PDF‑filer alltid vara perfekt indexerade! 

![Skärmbild av en PDF‑sida med Bates‑nummer i det nedre högra hörnet](https://example.com/images/bates-numbered.png "exempel på add bates numbering pdf")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}