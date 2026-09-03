---
category: general
date: 2026-02-14
description: Lägg enkelt till Bates‑numrering i PDF på dina dokument. Lär dig hur
  du lägger till sidnummer i foten och sekventiella nummer i PDF med Aspose.Pdf på
  några minuter.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: sv
og_description: Lägg till Bates‑numrering i PDF snabbt. Den här guiden visar hur du
  lägger till sidnummer i sidfoten och sekventiella nummer i PDF med Aspose.Pdf, med
  fullständig kod och tips.
og_title: Lägg till Bates-nummerering i PDF – Steg‑för‑steg C#-handledning
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Lägg till Bates-nummerering i PDF – Komplett C#-guide
url: /sv/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

"RTL formatting if needed" but not needed.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates Numbering PDF – Komplett C#-guide

Har du någonsin behövt **add Bates numbering PDF** filer men varit osäker på var du ska börja? Du är inte ensam. Juridiska team, revisorer och alla som hanterar stora dokumentuppsättningar frågar ständigt: “Hur lägger jag till Bates-nummer utan att förstöra layouten?” Den goda nyheten är att med Aspose.Pdf för .NET kan du injicera dessa nummer som en enkel sidfot – ingen manuell redigering krävs.

I den här handledningen går vi igenom en praktisk, end‑to‑end‑lösning som inte bara **adds footer page numbers** utan också låter dig **add sequential numbers PDF** filer med ett anpassat prefix, teckenstorlek och justering. I slutet har du ett färdigt C#‑program, en tydlig förståelse för varför varje inställning är viktig, och några proffstips för att undvika de vanligaste fallgroparna.

## Vad du kommer att lära dig

- Hur man laddar en befintlig PDF och förbereder den för Bates-numrering.  
- Vilka **BatesNumberingOptions**‑egenskaper som styr utseende och placering.  
- Hur man applicerar numrering på varje sida i ett anrop.  
- Sätt att anpassa prefix, startnummer och marginaler för olika juridiska format.  
- Edge‑case‑hantering – vad man gör med krypterade PDF‑filer eller dokument som redan innehåller sidfötter.

**Förutsättningar**: .NET 6+ (eller .NET Framework 4.7+), en recent version of Aspose.Pdf (exemplet använder 23.10), och en inmatnings‑PDF som du har rätt att ändra. Inga andra tredjepartsbibliotek behövs.

---

## Steg 1 – Ladda PDF‑filen du vill numrera

Det första vi gör är att skapa en `Document`‑instans som pekar på källfilen. Genom att använda `using var`‑mönstret säkerställs att filhandtaget frigörs automatiskt.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Varför detta är viktigt:** Aspose.Pdf läser in hela PDF‑strukturen i minnet, vilket gör att vi kan manipulera sidor, annotationer och metadata utan att röra den ursprungliga filen på disken. Om PDF‑filen är lösenordsskyddad kan du skicka lösenordet till konstruktorn – se noteringen “Encrypted PDFs” i slutet.

---

## Steg 2 – Definiera dina Bates‑numreringsalternativ

Bates‑nummer är i princip sidfötter med ett konfigurerbart prefix och en sekventiell räknare. Klassen `BatesNumberingOptions` låter dig finjustera varje visuellt aspekt.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Snabbtips

- **Prefix**: Använd en kort, unik identifierare (t.ex. ärendenummer) för att hålla sidfoten läsbar.  
- **StartNumber**: Juridiska firmor börjar ofta på `1` eller ett eget offset; välj det som matchar ditt arkiveringssystem.  
- **Margins**: Den nedre marginalen på `20` punkter håller texten fri från fotnoter eller signaturer som redan kan ligga nära sidans kant.

---

## Steg 3 – Applicera numreringen på alla sidor

Med alternativen konfigurerade är själva injektionen en enradare. Aspose.Pdf hanterar paginering, uppdaterar befintliga innehållsströmmar och respekterar sidrotation automatiskt.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **Vad händer under huven?** Biblioteket itererar över varje `Page`‑objekt, skapar ett `TextFragment` som inkluderar prefixet och den aktuella räknaren, och ritar sedan det med sidans koordinatsystem. Eftersom vi har satt `HorizontalAlignment.Right` och `VerticalAlignment.Bottom` fästs texten i det nedre högra hörnet oavsett sidstorlek.

---

## Steg 4 – Spara den modifierade PDF‑filen

Slutligen skriver du resultatet till en ny fil. Att skriva över originalet är möjligt, men att behålla en kopia underlättar versionskontroll.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Om du behöver bevara den ursprungliga metadata (författare, skapelsedatum) kopierar Aspose.Pdf den som standard. Du kan också ange ett `SaveOptions`‑objekt för PDF/A‑kompatibilitet eller komprimering.

---

## Fullt fungerande exempel

Nedan är det kompletta, färdiga programmet. Klistra in det i ett konsolapp‑projekt, justera filsökvägarna och tryck **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Förväntat resultat:** Varje sida i `output.pdf` visar nu en sidfot som `ABC-1000`, `ABC-1001`, … förankrad i det nedre högra hörnet. Öppna filen i någon PDF‑läsare för att verifiera.

---

## Hantera vanliga variationer

### Lägg bara till sidfotssidnummer

Om du bara behöver enkla sidnummer utan prefix, sätt `Prefix = ""` och justera eventuellt marginalen för att undvika kollision med befintliga sidfötter.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Använd en annan justering

Juridiska dokument kräver ibland att numret är centrerat längst ner. Byt justering:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Hantera krypterade PDF‑filer

När käll‑PDF‑filen är lösenordsskyddad, ange lösenordet så här:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

Resten av arbetsflödet förblir identiskt.

### Hoppa över befintliga sidfötter

Om ett dokument redan innehåller en sidfot som du inte vill skriva över, kan du lägga till en anpassad sträng före som gör det nya numret distinkt, eller så kan du iterera sidor manuellt och lägga till ett `TextFragment` endast där sidfoten saknas. Bibliotekets `Page`‑klass exponerar `Annotations`‑ och `Contents`‑samlingar för fin‑granulerad kontroll.

---

## Proffstips & fallgropar

- **Avoid clipping**: Mycket små nedre marginaler kan leda till att texten klipps av på skrivare. Testa med en fysisk utskrift om du ska distribuera papperskopior.  
- **Performance**: Att lägga till Bates‑nummer till en 500‑sidig PDF tar under en sekund på en modern laptop, men stora batcher drar nytta av parallell bearbetning – kom bara ihåg att `Document` inte är trådsäker, så varje tråd behöver sin egen instans.  
- **Version compatibility**: Koden fungerar med Aspose.Pdf 23.10 och nyare. Om du använder en äldre version är egenskapsnamnen desamma men `MarginInfo`‑konstruktorn kan kräva `float`‑argument.  
- **Legal compliance**: Vissa jurisdiktioner kräver att Bates‑numret placeras på en specifik plats (t.ex. nedre vänstra). Justera `HorizontalAlignment` därefter.

---

## Slutsats

Vi har just demonstrerat hur man **add Bates numbering PDF** filer med Aspose.Pdf för .NET, och täckt allt från att ladda dokumentet till att spara den slutgiltiga versionen med en ren sidfot. Genom att justera ett fåtal egenskaper kan du också **add footer page numbers**, **add sequential numbers PDF**, eller anpassa utseendet för att uppfylla vilken juridisk standard som helst.

Redo för nästa steg? Prova att kombinera tekniken med OCR‑textutdrag för att bädda in sökbara nyckelord tillsammans med dina Bates‑nummer, eller automatisera processen för hela mappar med `Directory.GetFiles`. Möjligheterna är oändliga, och den grund du nu har kommer göra dessa utökningar smidiga.

Lycka till med kodningen, och må dina PDF‑filer alltid vara perfekt numrerade!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}