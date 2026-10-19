---
title: Jämför PDF‑filer medan du ignorerar specifika områden med Aspose.Pdf för .NET
weight: 201
limit:
description: Lär dig att jämföra PDF‑filer sida‑vid‑sida och ignorera valda regioner med Aspose.Pdf för .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Lär dig att jämföra PDF‑filer sida‑vid‑sida och ignorera valda regioner
    med Aspose.Pdf för .NET.
  headline: Jämför PDF‑filer medan du ignorerar specifika områden med Aspose.Pdf för
    .NET
  type: TechArticle
- description: Lär dig att jämföra PDF‑filer sida‑vid‑sida och ignorera valda regioner
    med Aspose.Pdf för .NET.
  name: Jämför PDF‑filer medan du ignorerar specifika områden med Aspose.Pdf för .NET
  steps:
  - name: Definiera filsökvägarna för de två käll‑PDF‑filerna och den utgående diff‑PDF‑filen.
    text: Definiera filsökvägarna för de två käll‑PDF‑filerna och den utgående diff‑PDF‑filen.
  - name: Kontrollera att båda käll‑PDF‑filerna finns och avbryt med ett felmeddelande
      om någon av dem saknas.
    text: Kontrollera att båda käll‑PDF‑filerna finns och avbryt med ett felmeddelande
      om någon av dem saknas.
  - name: Skapa en array som innehåller det rektangulära området som ska ignoreras
      i den första PDF‑filen.
    text: Skapa en array som innehåller det rektangulära området som ska ignoreras
      i den första PDF‑filen.
  - name: Skapa en array som innehåller det rektangulära området som ska ignoreras
      i den andra PDF‑filen.
    text: Skapa en array som innehåller det rektangulära området som ska ignoreras
      i den andra PDF‑filen.
  - name: Konfigurera sida‑vid‑sida‑jämförelsen genom att tilldela ignorera‑område‑arrayerna
      till de lämpliga egenskaperna.
    text: Konfigurera sida‑vid‑sida‑jämförelsen genom att tilldela ignorera‑område‑arrayerna
      till de lämpliga egenskaperna.
  - name: Läs in båda PDF‑filerna och kör sida‑vid‑sida‑jämförelsen, vilket skapar
      diff‑filen på den angivna sökvägen.
    text: Läs in båda PDF‑filerna och kör sida‑vid‑sida‑jämförelsen, vilket skapar
      diff‑filen på den angivna sökvägen.
  - name: Skriv ut ett bekräftelsemeddelande som visar att jämförelsen har slutförts
      och var diff‑PDF‑filen sparades.
    text: Skriv ut ett bekräftelsemeddelande som visar att jämförelsen har slutförts
      och var diff‑PDF‑filen sparades.
  type: HowTo
- questions:
  - answer: Koordinaterna är i punkter (1/72 tum) med origo i sidans nedre vänstra
      hörn, så de två första siffrorna är nedre vänstra X/Y och de två sista är övre
      högra X/Y.
    question: Vilket koordinatsystem använder `Rectangle`‑värdena när du definierar
      ignorerade zoner?
  - answer: Ja – ange flera `Aspose.Pdf.Rectangle`‑objekt i `ExcludeAreas1` (eller
      `ExcludeAreas2`)‑arrayen; varje rektangel kommer att exkluderas oberoende under
      jämförelsen.
    question: Kan jag ignorera mer än ett rektangulärt område i samma dokument?
  - answer: Nej. `ExcludeAreas1` gäller för den första PDF‑filen och `ExcludeAreas2`
      för den andra, så du kan ange olika koordinater för varje dokument.
    question: Måste de ignorerade rektanglarna vara identiska i båda PDF‑filerna?
  - answer: Aspose.Pdf ignorerar tyst rektanglar som ligger helt utanför sidan; de
      har ingen inverkan på jämförelsens resultat.
    question: Vad händer om en rektangel definieras utanför sidans gränser?
  - answer: '`ExcludeAreas`‑arrayerna gäller per sida, så du måste lägga till samma
      `Rectangle` i varje sidas samling (t.ex. loopa igenom `pdf.Pages` och tilldela
      arrayen) innan du anropar `SideBySidePdfComparer.Compare`.'
    question: Hur kan jag exkludera samma region på varje sida i en PDF?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Ignorera regioner vid jämförelse av PDF‑filer
og_description: Se hur du hoppar över valda områden i en sida‑vid‑sida‑PDF‑jämförelse och får en ren diff‑PDF.
og_image_alt: Guide som visar sida‑vid‑sida‑PDF‑jämförelse med exkluderade rektangulära regioner med Aspose.Pdf för .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Jämför PDF‑filer medan du ignorerar specifika områden med Aspose.Pdf för .NET
Denna handledning visar hur du jämför två PDF‑dokument sida‑vid‑sida med Aspose.Pdf för .NET samtidigt som du utesluter angivna rektangulära områden från analysen. Genom att definiera uteslutna områden i varje fil markerar den genererade diff‑PDF‑filen endast de förändringar som är viktiga, vilket gör det enklare att fokusera på relevanta skillnader.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Vilket koordinatsystem använder `Rectangle`‑värdena när du definierar ignorerade zoner?**  
A: Koordinaterna är i punkter (1/72 tum) med origo i sidans nedre vänstra hörn, så de två första siffrorna är nedre vänstra X/Y och de två sista är övre högra X/Y.

**Q: Kan jag ignorera mer än ett rektangulärt område i samma dokument?**  
A: Ja – ange flera `Aspose.Pdf.Rectangle`‑objekt i `ExcludeAreas1` (eller `ExcludeAreas2`)‑arrayen; varje rektangel kommer att exkluderas oberoende under jämförelsen.

**Q: Måste de ignorerade rektanglarna vara identiska i båda PDF‑filerna?**  
A: Nej. `ExcludeAreas1` gäller för den första PDF‑filen och `ExcludeAreas2` för den andra, så du kan ange olika koordinater för varje dokument.

**Q: Vad händer om en rektangel definieras utanför sidans gränser?**  
A: Aspose.Pdf ignorerar tyst rektanglar som ligger helt utanför sidan; de har ingen inverkan på jämförelsens resultat.

**Q: Hur kan jag exkludera samma region på varje sida i en PDF?**  
A: `ExcludeAreas`‑arrayerna gäller per sida, så du måste lägga till samma `Rectangle` i varje sidas samling (t.ex. loopa igenom `pdf.Pages` och tilldela arrayen) innan du anropar `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}