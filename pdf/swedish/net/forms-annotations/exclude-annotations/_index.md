---
title: Sida‑vid‑sida PDF‑jämförelse utan annoteringar med Aspose.Pdf for .NET
weight: 101
limit:
description: Steg‑för‑steg‑guide för att jämföra PDF‑filer och utesluta annoteringsområden med Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Steg‑för‑steg‑guide för att jämföra PDF‑filer och utesluta annoteringsområden
    med Aspose.Pdf for .NET.
  headline: Sida‑vid‑sida PDF‑jämförelse utan annoteringar med Aspose.Pdf for .NET
  type: TechArticle
- description: Steg‑för‑steg‑guide för att jämföra PDF‑filer och utesluta annoteringsområden
    med Aspose.Pdf for .NET.
  name: Sida‑vid‑sida PDF‑jämförelse utan annoteringar med Aspose.Pdf for .NET
  steps:
  - name: Definiera filsökvägarna för den primära PDF-filen, den sekundära PDF-filen
      och den resulterande diff‑PDF-filen.
    text: Definiera filsökvägarna för den primära PDF-filen, den sekundära PDF-filen
      och den resulterande diff‑PDF-filen.
  - name: Kontrollera att båda inmatnings‑PDF‑filerna finns och avbryt med ett felmeddelande
      om någon av dem saknas.
    text: Kontrollera att båda inmatnings‑PDF‑filerna finns och avbryt med ett felmeddelande
      om någon av dem saknas.
  - name: Öppna de två PDF-filerna som Document‑objekt (pdfA och pdfB) inom ett using‑block
      så att de tas bort automatiskt.
    text: Öppna de två PDF-filerna som Document‑objekt (pdfA och pdfB) inom ett using‑block
      så att de tas bort automatiskt.
  - name: Samla in avgränsningsrektanglarna för varje annotering i pdfA och lagra
      dem i ignoredRectsA.
    text: Samla in avgränsningsrektanglarna för varje annotering i pdfA och lagra
      dem i ignoredRectsA.
  - name: Samla in avgränsningsrektanglarna för varje annotering i pdfB och lagra
      dem i ignoredRectsB.
    text: Samla in avgränsningsrektanglarna för varje annotering i pdfB och lagra
      dem i ignoredRectsB.
  - name: Skapa ett SideBySideComparisonOptions‑objekt och tilldela de tidigare insamlade
      annoteringsrektanglarna till ExcludeAreas1 och ExcludeAreas2 så att dessa områden
      ignoreras under jämförelsen.
    text: Skapa ett SideBySideComparisonOptions‑objekt och tilldela de tidigare insamlade
      annoteringsrektanglarna till ExcludeAreas1 och ExcludeAreas2 så att dessa områden
      ignoreras under jämförelsen.
  - name: Kör sida‑vid‑sida PDF‑jämförelsen med de två Document‑objekten och de konfigurerade
      alternativen, och skriv resultatet till outputPdf.
    text: Kör sida‑vid‑sida PDF‑jämförelsen med de två Document‑objekten och de konfigurerade
      alternativen, och skriv resultatet till outputPdf.
  - name: Frigör Document‑objekten och lämna using‑blocket.
    text: Frigör Document‑objekten och lämna using‑blocket.
  - name: Skriv ut ett bekräftelsemeddelande som visar att jämförelsen är klar och
      var diff‑PDF‑filen sparades.
    text: Skriv ut ett bekräftelsemeddelande som visar att jämförelsen är klar och
      var diff‑PDF‑filen sparades.
  type: HowTo
- questions:
  - answer: Ja. Koden lägger helt enkelt inte till några rektanglar i den motsvarande
      `ignoredRects`‑listan, så `ExcludeAreas1`/`ExcludeAreas2` får en tom array och
      jämförelsen bearbetar hela sidan.
    question: Vad händer om en PDF-sida saknar annoteringar – fungerar jämförelsen
      fortfarande?
  - answer: Ställ in `ExcludeAreas1` (eller `ExcludeAreas2`) på de insamlade rektanglarna
      och låt den andra egenskapen vara en tom array; jämförelsen kommer då att ignorera
      regioner endast i det angivna dokumentet.
    question: Kan jag utesluta endast annoteringar från ett dokument samtidigt som
      jag behåller det andra dokumentets annoteringar i diff‑filen?
  - answer: Överlappande rektanglar slås ihop internt av jämförelsen, så överlappande
      annoteringsgränser utesluts säkert utan dubbelräkning.
    question: Orsakar överlappande annoteringsrektanglar några problem med `ExcludeAreas`?
  - answer: Ja, sätt `compareOpts.ExcludeTables = true;` – den här flaggan fungerar
      tillsammans med `ExcludeAreas1`/`ExcludeAreas2` för att även ignorera tabellregioner.
    question: Finns det ett sätt att utesluta tabeller utöver annoteringar med samma
      options‑objekt?
  - answer: Koden kontrollerar `if (a != null && a.Rect != null)` innan den läggs
      till i listan, så null‑rektanglar helt enkelt hoppas över och inget undantag
      kastas.
    question: Vad händer om en annoterings `Rect`‑egenskap är null – kastar koden
      ett undantag?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Jämför PDF‑filer utan annoteringar
og_description: Kör en sida‑vid‑sida PDF‑diff som hoppar över alla annoteringsmärken.
og_image_alt: Guide som visar en sida‑vid‑sida PDF‑jämförelse som utesluter annoteringsregioner med Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sida‑vid‑sida PDF‑jämförelse utan annoteringar med Aspose.Pdf
Den här handledningen visar hur man jämför två PDF-filer med Aspose.Pdf for .NET samtidigt som man ignorerar all annoteringsinnehåll. Den extraherar avgränsningsrutorna för alla annoteringar från varje dokument, matar in dessa regioner i SideBySideComparisonOptions och kör sedan en sida‑vid‑sida‑jämförelse. Resultatet är en diff‑PDF som endast markerar förändringar som inte är annoteringar.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Vad händer om en PDF-sida saknar annoteringar – fungerar jämförelsen fortfarande?**  
A: Ja. Koden lägger helt enkelt inte till några rektanglar i den motsvarande `ignoredRects`‑listan, så `ExcludeAreas1`/`ExcludeAreas2` får en tom array och jämförelsen bearbetar hela sidan.

**Q: Kan jag utesluta endast annoteringar från ett dokument samtidigt som jag behåller det andra dokumentets annoteringar i diff‑filen?**  
A: Ställ in `ExcludeAreas1` (eller `ExcludeAreas2`) på de insamlade rektanglarna och låt den andra egenskapen vara en tom array; jämförelsen kommer då att ignorera regioner endast i det angivna dokumentet.

**Q: Orsakar överlappande annoteringsrektanglar några problem med `ExcludeAreas`?**  
A: Överlappande rektanglar slås ihop internt av jämförelsen, så överlappande annoteringsgränser utesluts säkert utan dubbelräkning.

**Q: Finns det ett sätt att utesluta tabeller utöver annoteringar med samma options‑objekt?**  
A: Ja, sätt `compareOpts.ExcludeTables = true;` – den här flaggan fungerar tillsammans med `ExcludeAreas1`/`ExcludeAreas2` för att även ignorera tabellregioner.

**Q: Vad händer om en annoterings `Rect`‑egenskap är null – kastar koden ett undantag?**  
A: Koden kontrollerar `if (a != null && a.Rect != null)` innan den läggs till i listan, så null‑rektanglar helt enkelt hoppas över och inget undantag kastas.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}