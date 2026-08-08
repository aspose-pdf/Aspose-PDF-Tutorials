---
category: general
date: 2026-03-27
description: Lägg till Bates‑numrering i C# snabbt. Lär dig hur du lägger till anpassade
  sidnummer, lägger till sekventiella sidnummer och lägger till anpassade nummer i
  Word‑dokument.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: sv
og_description: Lägg till Bates‑numrering i C# med ett tydligt exempel. Denna guide
  visar hur du lägger till anpassade sidnummer, sekventiella sidnummer och mer.
og_title: Lägg till Bates‑nummerering i C# – Komplett handledning
tags:
- C#
- Document Processing
- Bates Numbering
title: Lägg till Bates-nummerering i C# – Steg‑för‑steg‑guide
url: /sv/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates-nummerering i C# – Steg‑för‑steg‑guide

Har du någonsin undrat hur man **lägger till bates-nummerering** i ett Word‑dokument utan att dra i håret? Du är inte ensam. I många juridiska eller efterlevnadsprojekt krävs en unik identifierare på varje sida, och att göra det för hand är en mardröm.  

I den här handledningen går vi igenom ett komplett, körbart exempel som **lägger till bates-nummerering**, visar dig **hur man lägger till bates** på några rader, och täcker även hur man **lägger till anpassade sidnummer** och **lägger till sekventiella sidnummer** när du behöver dem. I slutet har du en .docx‑fil stämplad med de nummer du väljer—inga tredjepartsverktyg behövs.

## Vad du kommer att lära dig

- Läs in en DOCX‑fil med Aspose.Words för .NET API (eller något kompatibelt bibliotek).  
- Konfigurera **lägga till anpassade nummer** såsom ett prefix, ett startvärde och en teckenstorlek.  
- Applicera numreringen på varje sida i ett anrop.  
- Spara resultatet och verifiera att numren visas som förväntat.  

Ingen tidigare erfarenhet av Bates‑nummerering krävs; bara en grundläggande C#‑miljö och en kopia av källdokumentet. Låt oss dyka ner.

## Förutsättningar

- .NET 6+ (koden fungerar på .NET Core och .NET Framework lika).  
- Aspose.Words för .NET installerat via NuGet (`Install-Package Aspose.Words`).  
- Ett Word‑dokument med namnet `input.docx` placerat i en mapp du kan referera till (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code, eller någon C#‑IDE du föredrar.

> **Pro tip:** Om du använder ett annat bibliotek (t.ex. Open XML SDK) förblir koncepten desamma—byt bara API‑anropen.

## Steg 1: Läs in källdokumentet

Först måste vi läsa in Word‑filen i minnet.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Varför detta är viktigt:* Att ladda filen skapar ett `Document`‑objekt som ger dig åtkomst till sidor, sektioner och det lågnivå‑nodträdet. Utan det kan du inte fästa någon numrering.

## Steg 2: Konfigurera Bates‑nummereringsalternativ

Nu definierar vi exakt hur numren ska se ut. Det är här du **lägger till anpassade sidnummer** eller **lägger till sekventiella sidnummer**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Varför detta är viktigt:* `Prefix` låter dig **lägga till anpassade nummer** som ett ärendenummer, medan `Start` bestämmer den initiala räknaren. Att ändra `FontSize` säkerställer att numren inte slukar sidmarginalerna.

## Steg 3: Applicera Bates‑nummerering på varje sida

När alternativen är klara instruerar vi biblioteket att stämpla varje sida.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Varför detta är viktigt:* Metoden `AddBatesNumbering` går igenom den interna sidkollektionen och injicerar en textruta i det nedre högra hörnet (standardplatsen). Det är kärnan i **hur man lägger till bates** utan att skriva en loop själv.

## Steg 4: Spara det uppdaterade dokumentet

Till sist skriver vi den modifierade filen tillbaka till disk.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Varför detta är viktigt:* Sparandet skapar en ny `output.docx` som du kan öppna i Word, LibreOffice eller någon visare för att bekräfta att numren visas.

## Förväntat resultat

Öppna `output.docx`. Varje sida bör visa något liknande:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Om du öppnar dokumentets utskriftsförhandsgranskning ser du numren i det nedre högra hörnet, med den teckenstorlek du angav.

## Kantfall & variationer

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Ingen prefix behövs** | `Prefix = string.Empty` | Tar bort “ABC‑”‑delen, så endast den numeriska sekvensen återstår. |
| **Starta på 1** | `Start = 1` | Användbart för enkla **lägga till sekventiella sidnummer** utan ett anpassat prefix. |
| **Stora dokument (>10 000 sidor)** | Increase `FontSize` or adjust `Location` (use overloads of `AddBatesNumbering`) | Förhindrar överlappning med sidfötter eller sidhuvuden. |
| **Skrivskyddad källfil** | Open with `LoadOptions` that allow write access, or copy the file first | Annars kommer `document.Save` att kasta ett undantag. |
| **Olika placering** | Use `batesOptions.Position = BatesNumberingPosition.TopLeft` (or other enum) | Vissa företag kräver nummer högst upp på sidan. |

> **Note:** Inte alla bibliotek exponerar en `BatesNumberingOptions`‑klass. Med Open XML SDK skulle du infoga en `TextBox` manuellt—samma princip, mer kod.

## Fullt fungerande exempel

Här är hela programmet på ett ställe. Kopiera‑klistra in det i en konsolapp och kör.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Kör programmet, öppna `output.docx`, och du kommer att se numreringen exakt där du förväntade dig. 🎉

## Vanliga frågor

**Q: Kan jag ändra färgen på numren?**  
A: Ja. Efter att ha anropat `AddBatesNumbering` kan du hämta de genererade `Shape`‑objekten och sätta deras `FillColor`‑egenskap.

**Q: Vad händer om jag behöver numren på vänster sida istället för höger?**  
A: Använd `batesOptions.Position = BatesNumberingPosition.BottomLeft` (eller `TopLeft`, `TopRight`). API‑et stödjer alla fyra hörn.

**Q: Fungerar detta med PDF‑utmatning?**  
A: Absolut. Efter att ha lagt till numreringen, anropa `document.Save("output.pdf")`. Numren renderas i PDF‑filen precis som i Word.

## Slutsats

Du vet nu **hur man lägger till bates-nummerering** i en Word‑fil med C#. Handledningen täckte inläsning av ett dokument, konfiguration av **lägga till anpassade nummer**, applicering av **lägga till sekventiella sidnummer**, och sparande av slutresultatet. Med hela kodexemplet kan du slänga in detta i vilket projekt som helst och börja stämpla dokument omedelbart.

Redo för nästa utmaning? Prova att kombinera detta med en batch‑processor som loopar igenom en mapp med filer, eller utforska **lägga till anpassade sidnummer** i sidhuvudet/sidfoten för ett mer polerat utseende. Oavsett har du en solid grund för alla juridiska‑teknik‑ eller efterlevnadsautomatiseringsuppgifter.

Har du frågor eller ett coolt användningsfall? Lämna en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}