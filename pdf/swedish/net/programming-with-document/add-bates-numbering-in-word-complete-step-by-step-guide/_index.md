---
category: general
date: 2026-06-21
description: Lägg till Bates‑nummerering i Word snabbt. Lär dig hur du lägger till
  Bates, tillämpar Bates‑nummerering för juridiska dokument och automatiserar numrering
  med C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: sv
og_description: Lägg till Bates-nummerering i Word med C#. Den här guiden visar hur
  du lägger till Bates, tillämpar Bates-nummerering för juridiska dokument och automatiserar
  processen.
og_title: Lägg till Bates-nummerering i Word – Fullständig programmeringsgenomgång
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Lägg till Bates-nummerering i Word – Komplett steg‑för‑steg‑guide
url: /sv/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates‑numrering i Word – Komplett steg‑för‑steg‑guide

Har du någonsin funderat på hur man lägger till Bates‑numrering i en Word‑fil utan att manuellt skriva in varje nummer? Du är inte ensam. Många advokater, juristassistenter och e‑discovery‑specialister behöver ett pålitligt sätt att **lägga till Bates‑numrering** på hundratals sidor, och att göra det för hand är en mardröm.

I den här handledningen går vi igenom en ren C#‑lösning som **tillämpar Bates‑numrering** på en `.docx`‑fil, förklarar varför varje rad är viktig och visar hur du kan justera koden för juridiska behov. När du är klar kan du generera ett perfekt numrerat dokument på några sekunder – utan extra tillägg.

## Vad du kommer att lära dig

- Den exakta koden som krävs för att **lägga till Bates‑numrering** i ett Word‑dokument.  
- Hur klassen `BatesNumberingOptions` fungerar och varför du kanske vill justera prefix eller startvärde.  
- Tips för att använda detta tillvägagångssätt på stora ärenden, inklusive minnesaspekter.  
- En snabb genomgång av förutsättningar så att du kan kopiera‑klistra lösningen och köra den idag.

**Förutsättningar**  
- .NET 6+ (eller .NET Framework 4.7.2+ om du föredrar den äldre runtime‑versionen).  
- En referens till Aspose.Words för .NET‑biblioteket (eller någon liknande API som exponerar `AddBatesNumbering`).  
- Grundläggande kunskap om C# och Visual Studio (eller din favorit‑IDE).

Om du är bekväm med detta, låt oss dyka ner.

## Steg 1: Skapa projektet och importera biblioteket

Skapa först en ny konsolapp (eller integrera i en befintlig tjänst). Lägg sedan till Aspose.Words NuGet‑paketet:

```bash
dotnet add package Aspose.Words
```

> **Pro‑tips:** Använd den kostnadsfria utvärderingslicensen för testning; den lägger till ett litet vattenstämpel men fungerar annars exakt som fullversionen.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Dessa `using`‑satser importerar klasserna `Document` och `BatesNumberingOptions` till ditt namnrum, vilket är nödvändigt för **tillämpa Bates‑numrering** senare.

## Steg 2: Läs in källdokumentet

Du behöver en Word‑fil att arbeta på. Koden nedan läser in `input.docx` från en mapp du anger. Ersätt `"YOUR_DIRECTORY"` med den faktiska sökvägen på din maskin.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Varför läsa in filen först? `Document`‑objektet parsar hela Word‑paketet till minnet, vilket gör att vi kan manipulera sidhuvuden, sidfötter och sidlayout innan vi sparar. Om filen är enorm (tänk 10 000 sidor) kan du överväga att använda `LoadOptions` med `LoadFormat.Docx` för att strömma sektioner istället för att ladda allt på en gång.

## Steg 3: Konfigurera Bates‑numreringsalternativ

Här sker magin. Du talar om för biblioteket vilket prefix som ska användas (`"ABC-"` i exemplet) och var räknandet ska börja (`1000`). Båda värdena är helt anpassningsbara.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Varför ett prefix?** Inom juridiken identifierar prefix ofta ärendet eller den producerande parten (`"ABC-"` kan stå för *Acme Bank Corp.*). Att börja på `1000` är vanligt eftersom många firmor reserverar de första 999 numren för interna utkast.

Om du arbetar med **Bates‑numrering för juridiska** dokument kan du också vilja sätta `batesOptions.Position` till `Header` eller `Footer` och justera justeringen enligt domstolsregler. Biblioteket stödjer dessa justeringar direkt.

## Steg 4: Tillämpa Bates‑numrering på hela dokumentet

Nu injicerar vi faktiskt numren. Metoden `AddBatesNumbering` går igenom varje sida, sätter in den formaterade strängen och uppdaterar dokumentets interna sidräkning.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Bakom kulisserna skapar Aspose.Words ett dolt fält på varje sida som renderas som `ABC-1000`, `ABC-1001` osv. Eftersom det är ett fält kan du senare redigera prefixet eller startnumret utan att generera om hela filen – praktiskt för **hur man lägger till Bates** efter att en discovery‑begäran förändras.

## Steg 5: Spara det modifierade dokumentet

Till sist skriver vi utdata till en ny fil. Att behålla originalet orört är en bästa praxis, särskilt när du hanterar bevis som måste förbli orörda.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Du har nu `output.docx` med sekventiella Bates‑nummer tillagda på varje sida. Öppna den i Word så ser du numren exakt där du specificerade (standard är sidfot). Filstorleken kan öka något på grund av de extra fälten, men det är försumbar jämfört med fördelarna.

### Förväntat resultat

| Sida | Bates‑nummer |
|------|--------------|
| 1    | ABC-1000     |
| 2    | ABC-1001     |
| …    | …            |
| N    | ABC‑(1000 + N‑1) |

Om du öppnar dokumentets “Fältkoder”-vy (`Alt+F9` i Word) ser du något i stil med `{ BATES \* MERGEFORMAT ABC-1000 }` på varje sida.

## Edge Cases & Vanliga frågor

### Vad händer om dokumentet redan innehåller sidnummer?

Metoden `AddBatesNumbering` **överskriver inte** befintliga sidnummerfält; den lägger bara till ett nytt fält. Om du vill ersätta de befintliga numren, ta bort dem först eller sätt `batesOptions.Position` till samma plats som de nuvarande sidnumren.

### Kan jag hoppa över sidor (t.ex. exkludera en framsida)?

Ja. Använd överlagringen som accepterar ett `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Detta är användbart när du behöver **Bates‑numrering för juridiska** inlagor som börjar efter en titelsida.

### Hur ändrar jag nummerformatet (romerska siffror, bokstäver)?

Klassen `BatesNumberingOptions` har en egenskap `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Sätt den innan du anropar `AddBatesNumbering`. Denna flexibilitet hjälper när en domstol kräver en specifik stil.

### Vad gäller prestanda på enorma filer?

Att ladda en 2 GB Word‑fil kan kräva mycket RAM. För att mildra detta, bearbeta dokumentet i delar med hjälp av verktyget `DocumentSplitter`, tillämpa Bates‑numrering på varje del och slå sedan ihop delarna igen. Detta mönster håller minnesanvändningen under kontroll samtidigt som du **tillämpar Bates‑numrering** effektivt.

## Fullt fungerande exempel

Sätter vi ihop allt får du ett färdigt konsolprogram:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Kör programmet, öppna `output.docx` och du ser en ren serie nummer redo för arkivering, discovery eller domstolsinlämning.

## Slutsats

Du vet nu exakt **hur man lägger till Bates** i ett Word‑dokument med C#. Stegen – ladda, konfigurera, tillämpa och spara – är enkla men tillräckligt flexibla för att tillgodose **Bates‑numrering för juridiska** arbetsflöden, anpassade prefix och även storskalig batch‑bearbetning.

Om du vill gå vidare, överväg att:

- Integrera koden i ett web‑API så att kollegor kan ladda upp filer och få numrerade PDF‑filer direkt.  
- Lägga till felhantering för saknade filer eller behörighetsproblem (en snabb `try/catch` runt `Document.Load`).  
- Utforska andra Aspose.Words‑funktioner som vattenstämplar eller rödning för en komplett e‑discovery‑verktygslåda.

Känn dig fri att experimentera med olika prefix, startnummer eller till och med kombinera flera numreringsscheman i samma dokument. Världen av **tillämpa Bates‑numrering** är förvånansvärt mångsidig när du har kärnlogiken på plats.

Har du frågor eller ett knepigt scenario? Lämna en kommentar nedan så felsöker vi tillsammans. Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}