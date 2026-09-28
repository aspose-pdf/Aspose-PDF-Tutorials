---
category: general
date: 2026-03-24
description: Skapa PDF-dokument och lär dig hur du ställer in absolut position för
  märkt text. Denna handledning visar hur du lägger till ett span‑element, hur du
  lägger till märkt innehåll och placerar text på sidan.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: sv
og_description: Skapa PDF-dokument och se omedelbart hur du anger absolut position,
  lägger till ett span-element och placerar text på sidan med taggat PDF-innehåll.
og_title: Skapa PDF-dokument – Absolut positionering av taggad text
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Skapa PDF-dokument – Ange absolut position för taggad text
url: /sv/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF-dokument – Ställ in absolut position för taggad text

Har du någonsin behövt **skapa pdf-dokument** som innehåller tillgänglig, taggad text placerad exakt där du vill ha den? Kanske bygger du ett formulär‑likt PDF där etiketten måste sitta på en exakt koordinat, eller så genererar du ett certifikat och namnet måste ligga perfekt i linje med en bakgrundsbild.  

I den här guiden går vi igenom ett komplett, körbart exempel som visar **hur man lägger till taggad** innehåll, **sätter absolut position**, och **lägger till span‑element** så att du kan **positionera text på sidan** utan att gissa. Inga externa referenser – bara koden du kan kopiera‑klistra in, plus förklaringar av “varför” bakom varje rad.

## Förutsättningar

- .NET 6+ (eller .NET Framework 4.6+) med en C#‑kompilator  
- Aspose.Pdf for .NET (senaste versionen vid skrivtillfället, 23.12) installerad via NuGet  
- Grundläggande kunskap om C#‑syntax  

Om du har detta, låt oss komma igång.

---

## Skapa PDF-dokument – Ställa in den absoluta positionen

Det första vi gör är att instansiera ett tomt `Document`. Detta objekt representerar hela PDF‑filen och ger oss åtkomst till det taggade innehållsträdet.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Varför detta är viktigt:**  
`Document` är roten i PDF‑strukturen. Genom att skapa den först säkerställer vi att det finns en canvas för både visuella element (sidor, grafik) och logisk struktur (taggar). `using`‑satsen garanterar att filen tas om hand korrekt, vilket förhindrar filhandtagsläckor på Windows.

---

## Aktivera taggat innehåll (Hur man lägger till taggat)

Innan vi kan infoga några taggade element måste dokumentet markeras som *taggat*. Aspose.Pdf skapar automatiskt ett `TaggedContent`‑objekt, men du måste ändå slå på flaggan.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Vad händer under huven?**  
Att sätta `TaggedContent` till `true` talar om för PDF‑läsare att filen innehåller ett logiskt strukturträd. Detta är avgörande för skärmläsare och för att `SetPosition`‑metoden ska fungera korrekt på ett span‑element.

---

## Hämta rot‑elementet i det taggade innehållsträdet

Rot‑elementet är ingångspunkten för alla strukturella taggar (som `<Document>`, `<Section>`, `<Span>`). Tänk på det som den osynliga “body” i PDF‑filen.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Varför vi behöver roten:**  
Alla efterföljande taggar måste fästas någonstans i trädet; annars visas de inte i tillgänglighetshierarkin.

---

## Lägg till ett Span‑element – Byggstenen för inline‑text

Ett *span* är PDF‑motsvarigheten till ett HTML‑`<span>`—perfekt för korta textstycken som du vill placera exakt.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Designnotering:**  
Om du behöver rikare formatering (fet, kursiv, hyperlänkar) kan du omsluta spannen i ett `<Paragraph>` eller använda `TextFragment`‑objekt senare. För absolut positionering är ett enkelt span det lättaste.

---

## Ställ in absolut position – X=100, Y=200

Nu kommer den roliga delen: att placera spannen på en exakt plats på sidan. Koordinatsystemet startar i det nedre vänstra hörnet (0,0) och använder punkter (1 pt ≈ 1/72 tum).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Varför absolut positionering?**  
När du behöver pixel‑perfekt layout—tänk certifikat, fakturor eller formulär—räcker inte relativ flöde (som vänster‑till‑höger‑text). `SetPosition` kringgår den normala textflödet och fäster elementet där du anger.

---

## Lägg till text i spannen

När spannen är placerad injicerar vi nu själva strängen.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Tips:**  
Om du behöver Unicode‑tecken eller skript som skrivs från höger till vänster, skicka bara strängen; Aspose.Pdf hanterar kodningen automatiskt.

---

## Bifoga spannen till rot‑elementet

Till sist fäster vi spannen i dokumentets logiska träd så att den blir en del av den färdiga PDF‑filen.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Vad händer om du glömmer detta steg?**  
Spannen skulle finnas i minnet men aldrig serialiseras till filen, så du skulle inte se någon text och tillgänglighetsträdet skulle vara ofullständigt.

---

## Komplett, körbart exempel

Nedan är hela programmet som du kan klistra in i en konsolapp. Det skapar en en‑sidig PDF, lägger till ett taggat span vid (100, 200), och sparar filen som `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Förväntat resultat:**  
Öppna `TaggedPositioned.pdf` i någon visare (Adobe Acrobat, Foxit, osv.). Du kommer att se frasen **“Positioned tagged text”** exakt 100 pt från vänster kant och 200 pt från botten av sidan. Om du inspekterar *Tags*-panelen kommer ett `<Span>`‑element listas under dokumentets rot, vilket bekräftar att innehållet är korrekt taggat.

---

## Vanliga frågor & specialfall

### Vad händer om jag behöver placera text på en specifik sida annat än den första?

Lägg till den sida du vill (`var page = pdfDocument.Pages[3];`) innan du anropar `SetPosition`. Spannen kommer automatiskt att fästa sig till den aktiva sidkontexten.

### Kan jag ange positionen i tum eller centimeter?

`SetPosition` accepterar punkter. Konvertera med formlerna:  
- **Tum → punkter:** `points = inches * 72`  
- **Centimeter → punkter:** `points = cm * 28.3465`

### Hur ändrar jag teckensnittet eller färgen på spannen?

Efter att ha skapat spannen kan du hämta dess `TextState` och modifiera den:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Vad händer om dokumentet redan har befintliga taggar?

Du kan fortfarande skapa ett nytt span och bifoga det till vilket befintligt element som helst (`rootElement`, ett specifikt `<Section>`, osv.). Se bara till att du behåller en logisk hierarki—skärmläsare förväntar sig ett välstrukturerat träd.

### Fungerar detta med PDF/A eller PDF/UA‑efterlevnad?

Ja. Taggade PDF‑filer är ett grundkrav för PDF/UA. Om du behöver PDF/A, sätt `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` efter att innehållet byggts.

---

## Proffstips och fallgropar

- **Proffstips:** Lägg alltid till en sida innan du positionerar innehåll. Utan en sida misslyckas `SetPosition` tyst eftersom det inte finns någon renderingsyta.
- **Var uppmärksam på enheter:** Att blanda pixlar från en UI‑design med PDF‑punkter kommer att placera din text fel. Dubbelkolla konverteringen.
- **Prestandahint:** Om du genererar tusentals PDF‑filer, återanvänd en enda `Document`‑instans och anropa `pdfDocument.Pages.Clear()` mellan körningar för att undvika onödig minnesallokering.
- **Tillgänglighetspåminnelse:** Taggning är inte bara ett trevligt tillägg; många regelverk (Section 508, EN 301 549) kräver det. Att använda `CreateSpanElement` säkerställer att texten kan upptäckas av hjälpmedel.

---

## Slutsats

Vi har just **skapat pdf-dokument** från grunden, **ställt in absolut position**, **lagt till span‑element**, och demonstrerat **hur man lägger till taggat** innehåll så att du kan **positionera text på sidan** med pixel‑perfekt precision. Det kompletta exemplet är redo att köras, och förklaringen täckte både *hur* och *varför*—precis vad utvecklare (och AI‑assistenter) söker när de behöver en pålitlig lösning.

Nästa steg kan vara att utforska:

- Att lägga till bilder bakom den positionerade texten för vattenmärkta certifikat.  
- Att använda `CreateParagraphElement` för flerradiga block som fortfarande behöver absolut placering.  
- Att exportera till PDF/UA för att uppfylla strikta tillgänglighetsgranskningar.  

Känn dig fri att justera koordinater, teckensnitt eller färger—experimentering är det snabbaste sättet att bemästra taggad PDF‑generering. Om du stöter på problem, lämna en kommentar nedan; happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}