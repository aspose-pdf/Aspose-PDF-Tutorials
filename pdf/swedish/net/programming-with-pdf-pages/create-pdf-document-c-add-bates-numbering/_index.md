---
category: general
date: 2026-03-03
description: Skapa PDF-dokument i C# med Bates-nummerering – lär dig hur du lägger
  till Bates, lägger till sekventiella sidnummer och genererar Bates på bara några
  steg.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: sv
og_description: Skapa PDF-dokument i C# med Bates-nummerering. Den här guiden visar
  hur du lägger till Bates, lägger till sekventiella sidnummer och snabbt genererar
  Bates.
og_title: Skapa PDF-dokument C# – Lägg till Bates-nummerering
tags:
- C#
- PDF
- Bates numbering
title: Skapa PDF-dokument i C# – Lägg till Bates‑nummerering
url: /sv/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF‑dokument C# – Lägg till Bates‑nummerering

Har du någonsin behövt **create PDF document C#** och sedan märka varje sida med en unik identifierare för juridiska eller arkiveringsändamål? Du är inte ensam – advokatbyråer, domstolar och stora företag frågar ständigt: ”Hur lägger jag automatiskt till Bates‑nummer i mina PDF‑filer?” Den goda nyheten är att med några få rader kod kan du generera en PDF, sprida Bates‑nummer över varje sida och spara resultatet utan att någonsin öppna en redigerare.

I den här handledningen går vi igenom ett praktiskt, end‑to‑end‑exempel som visar **hur man lägger till Bates**, hur man **lägger till sekventiella sidnummer**, och även hur man **genererar Bates** med egna prefix. När du är klar har du ett återanvändbart kodsnutt som du kan klistra in i vilket .NET‑projekt som helst.

## Vad du behöver

- **.NET 6+** (koden fungerar även på .NET Framework 4.6+)
- **Aspose.Pdf for .NET** – ett kommersiellt bibliotek som erbjuder ett rent API för PDF‑manipulation. En gratis utvärderingsversion räcker för testning.
- Grundläggande kunskaper i C# (du är förmodligen redan bekväm med `using`‑satser och objekt).

Inga ytterligare NuGet‑paket krävs förutom `Aspose.Pdf`. Om du ännu inte har installerat det, kör:

```bash
dotnet add package Aspose.Pdf
```

> **Proffstips:** Håll din Aspose‑version uppdaterad; den senaste 23.x‑utgåvan innehåller prestandaförbättringar för stora dokument.

## Steg 1: Öppna (eller skapa) käll‑PDF‑dokumentet

Först behöver vi en PDF att arbeta med. I många verkliga scenarier har du redan en indatafil – exempelvis ett skannat kontrakt. För detta exempel öppnar vi en befintlig fil som heter `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Varför det är viktigt:** Att öppna dokumentet i ett `using`‑block garanterar att filhandtaget frigörs omedelbart, vilket undviker låsproblem när du senare försöker skriva över samma fil.

## Steg 2: Definiera dina Bates‑nummereringsalternativ

Bates‑nummer består av ett **prefix** (ofta en ärendenummer) och ett **startnummer**. Du kan också styra antalet siffror, placeringen på sidan och teckensnittsstilen. Här använder vi nyckelordet **add bates numbering pdf** genom att konfigurera ett `BatesNumberingOptions`‑objekt.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **Hur man lägger till bates:** Genom att justera `Prefix` och `Start` bestämmer du exakt vilken sträng som visas på varje sida. Egenskapen `NumberOfDigits` säkerställer enhetlig bredd, vilket är praktiskt för juridiska inlagor.

## Steg 3: Applicera Bates‑nummerering på varje sida

Nu kommer kärnoperationen – att lägga till numren. Metoden `AddBatesNumbering` går igenom varje sida, ritar texten och respekterar de alternativ vi definierat.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Under huven renderar Aspose texten som ett *content*‑element, vilket betyder att numren blir en del av PDF‑filen och inte kan döljas i en visare. Detta är exakt vad du behöver när du vill **add sequential page numbers** som är oföränderliga.

### Kantfall & variationer

- **Flera prefix:** Om du behöver olika prefix per avsnitt, skapa separata `BatesNumberingOptions` och anropa `AddBatesNumbering` på ett sidintervall (`pdfDocument.Pages[1..5]`).
- **Noll‑utfyllnad:** Utelämna `NumberOfDigits` för ett variabelt antal siffror, eller sätt ett högre värde för ledande nollor.
- **Anpassad placering:** Använd `Margin` för att förskjuta numret från kanten, eller byt `HorizontalAlignment` till `Center` för en fotnot‑stil.

## Steg 4: Spara den modifierade PDF‑filen

Till sist skriver vi det uppdaterade dokumentet till disk. Du kan skriva över originalet eller skapa en helt ny fil.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

När den här raden har körts innehåller `output.pdf` det ursprungliga innehållet plus en synlig Bates‑tagg på varje sida – precis som du förväntar dig när du **how to generate bates** för ett ärende.

## Fullt, körbart exempel

Sätter vi ihop allt får du följande kompletta kodsnutt som du kan kopiera och klistra in i en konsolapp:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Förväntat resultat

Öppna `output.pdf` i någon visare (Adobe Reader, Edge osv.). Du kommer att se varje sida stämplad med något i stil med **CASE-001000**, **CASE-001001**, … upp till sista sidan. Numren sitter lagom längst ner till höger, enligt de alternativ vi angav.

## Vanliga frågor & felsökning

- **”Vad händer om min PDF är lösenordsskyddad?”**  
  Läs in den med lösenordet: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **”Kan jag lägga till Bates‑nummer till en nyss skapad PDF?”**  
  Absolut. Skapa dokumentet först (`var doc = new Document();`) och följ sedan steg 2‑4 innan du sparar.

- **”Är teckensnittet alltid inbäddat?”**  
  Aspose bäddar automatiskt in teckensnittet om det inte redan finns i PDF‑filen. Om du behöver ett specifikt teckensnittsfamilj, sätt `options.Font` därefter.

- **”Hur är prestandan på filer med 10 000 sidor?”**  
  Biblioteket strömmar sidor, så minnesanvändningen förblir måttlig. Du kan dock öka `PdfSaveOptions.CompressionMode` för snabbare I/O.

## Proffstips för produktionsanvändning

1. **Batch‑behandling:** Lägg in logiken i en loop som itererar över en mapp med PDF‑filer. Använd `Directory.GetFiles("*.pdf")` och bearbeta varje fil individuellt.
2. **Loggning:** Skriv ut första och sista Bates‑numret till en loggfil – underlättar för revisorer att verifiera att numreringen är kontinuerlig.
3. **Felkoll:** Omge hela blocket med ett `try/catch` och visa ett tydligt meddelande om käll‑PDF‑filen saknas eller är korrupt.
4. **Flexibel noll‑utfyllnad:** Om du behöver ett dynamiskt antal siffror baserat på totalt antal sidor, beräkna `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Slutsats

Vi har just visat hur man **create PDF document C#** och sömlöst **add Bates numbering** – från inläsning till slutlig sparning. Det korta exemplet demonstrerar **how to add bates**, **add sequential page numbers**, och **how to generate bates** med egna prefix och noll‑utfyllnad. Med några justeringar kan du anpassa detta mönster för batchjobb, olika layouter eller till och med integrera det i ett webb‑API som returnerar en nynumrerad PDF på begäran.

Redo för nästa steg? Prova att kombinera detta med Asposes **watermark**‑funktion, eller generera ett sammanfattnings‑index som listar varje Bates‑nummer tillsammans med en kort beskrivning av sidans innehåll. Möjligheterna är oändliga, och koden du nu har är en solid grund för alla dokument‑automatiseringsarbetsflöden.

Lycka till med kodandet, och må dina PDF‑filer alltid vara perfekt numrerade! 

![Screenshot of a PDF viewer showing create pdf document c# with Bates numbers applied](image-placeholder.png "create pdf document c# with Bates numbers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}