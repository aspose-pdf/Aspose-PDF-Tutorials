---
title: Kryptera PDF för att endast tillåta formulärifyllning med Aspose.Pdf för .NET
weight: 101
limit:
description: Lär dig hur du krypterar en PDF med AES‑256, anger lösenord och begränsar behörigheterna till endast formulärifyllning med Aspose.Pdf för .NET.
keywords: [Aspose.Pdf for .NET, encrypt PDF, PDF form filling permissions, AES-256 PDF encryption, viewer password PDF, owner password PDF]
url: /net/security-permissions/encrypt-pdf-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Lär dig hur du krypterar en PDF med AES‑256, anger lösenord och begränsar
    behörigheterna till endast formulärifyllning med Aspose.Pdf för .NET.
  headline: Kryptera PDF för att endast tillåta formulärifyllning med Aspose.Pdf för
    .NET
  type: TechArticle
- description: Lär dig hur du krypterar en PDF med AES‑256, anger lösenord och begränsar
    behörigheterna till endast formulärifyllning med Aspose.Pdf för .NET.
  name: Kryptera PDF för att endast tillåta formulärifyllning med Aspose.Pdf för .NET
  steps:
  - name: Definiera sökvägarna för käll- och destinationsfilen samt visnings- och
      ägarlösenorden.
    text: Definiera sökvägarna för käll- och destinationsfilen samt visnings- och
      ägarlösenorden.
  - name: Kontrollera att käll-PDF:en finns och avbryt med ett felmeddelande om den
      inte gör det.
    text: Kontrollera att käll-PDF:en finns och avbryt med ett felmeddelande om den
      inte gör det.
  - name: Starta ett try‑block för att hantera eventuella fel som kan uppstå under
      bearbetningen.
    text: Starta ett try‑block för att hantera eventuella fel som kan uppstå under
      bearbetningen.
  - name: Öppna den befintliga PDF-filen genom att skapa ett Document‑objekt med namnet
      pdfDoc.
    text: Öppna den befintliga PDF-filen genom att skapa ett Document‑objekt med namnet
      pdfDoc.
  - name: Ställ in behörigheter så att endast formulärifyllning tillåts, kryptera
      dokumentet med visnings- och ägarlösenord med AES‑256 och spara den skyddade
      PDF‑filen.
    text: Ställ in behörigheter så att endast formulärifyllning tillåts, kryptera
      dokumentet med visnings- och ägarlösenord med AES‑256 och spara den skyddade
      PDF‑filen.
  - name: Skriv ett bekräftelsemeddelande till konsolen och avsluta try‑blocket.
    text: Skriv ett bekräftelsemeddelande till konsolen och avsluta try‑blocket.
  - name: Fånga eventuella undantag och skriv ut felmeddelandet till konsolen.
    text: Fånga eventuella undantag och skriv ut felmeddelandet till konsolen.
  type: HowTo
- questions:
  - answer: När den öppnas med visnings‑ (användar‑) lösenordet kan dokumentet visas
      och formulärfält fyllas i, men alla andra åtgärder såsom redigering av text,
      tillägg av kommentarer eller extrahering av innehåll blockeras.
    question: Vad kan en användare göra med PDF‑filen efter att den har krypterats
      med `Permissions.FillForm`?
  - answer: Kombinera behörigheter med bitvis OR‑operator, t.ex. `Permissions allowed
      = Permissions.FillForm | Permissions.Printing;` och skicka det kombinerade värdet
      till `pdfDoc.Encrypt`.
    question: Hur kan jag tillåta ytterligare rättigheter, som utskrift, samtidigt
      som jag fortfarande begränsar allt annat?
  - answer: Ja. Det första argumentet är användar‑ (visnings‑) lösenordet som ger
      de begränsade rättigheterna, och det andra argumentet är ägar‑ (admin‑) lösenordet
      som ger full kontroll över dokumentet.
    question: Spelar ordningen på lösenorden i `pdfDoc.Encrypt(viewerPass, adminPass,
      …)` någon roll?
  - answer: Aspose.Pdf kommer att kasta ett undantag när du försöker öppna en redan
      krypterad fil; du måste först öppna den med dess befintliga lösenord, ta bort
      eller ändra skyddet och sedan tillämpa de nya krypteringsinställningarna.
    question: Vad händer om käll‑PDF‑filen redan är lösenordsskyddad?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-form-filling/og-image.png
og_title: Kryptera PDF och tillåt endast formulärifyllning
og_description: Säkra din PDF med AES‑256 och låt användare fylla i formulär men inget annat.
og_image_alt: Skärmdump som visar Aspose.Pdf för .NET‑kod som krypterar en PDF och begränsar den till endast formulärifyllning
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kryptera PDF för att endast tillåta formulärifyllning med Aspose.Pdf för .NET
I den här handledningen kommer du att lära dig hur du öppnar en befintlig PDF med Aspose.Pdf för .NET, tillämpar AES‑256‑kryptering, anger visnings- och ägarlösenord och begränsar dokumentets behörigheter så att mottagarna endast kan fylla i formulärfält. Detta tillvägagångssätt är användbart när du behöver skydda innehållet samtidigt som du tillåter användare att fylla i interaktiva formulär. Koden går igenom varje steg och sparar den säkrade PDF‑filen klar för distribution.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-form-filling" >}}


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

**Q: Vad kan en användare göra med PDF‑filen efter att den har krypterats med `Permissions.FillForm`?**  
A: När den öppnas med visnings‑ (användar‑) lösenordet kan dokumentet visas och formulärfält fyllas i, men alla andra åtgärder såsom redigering av text, tillägg av kommentarer eller extrahering av innehåll blockeras.

**Q: Hur kan jag tillåta ytterligare rättigheter, som utskrift, samtidigt som jag fortfarande begränsar allt annat?**  
A: Kombinera behörigheter med bitvis OR‑operator, t.ex. `Permissions allowed = Permissions.FillForm | Permissions.Printing;` och skicka det kombinerade värdet till `pdfDoc.Encrypt`.

**Q: Spelar ordningen på lösenorden i `pdfDoc.Encrypt(viewerPass, adminPass, …)` någon roll?**  
A: Ja. Det första argumentet är användar‑ (visnings‑) lösenordet som ger de begränsade rättigheterna, och det andra argumentet är ägar‑ (admin‑) lösenordet som ger full kontroll över dokumentet.

**Q: Vad händer om käll‑PDF‑filen redan är lösenordsskyddad?**  
A: Aspose.Pdf kommer att kasta ett undantag när du försöker öppna en redan krypterad fil; du måste först öppna den med dess befintliga lösenord, ta bort eller ändra skyddet och sedan tillämpa de nya krypteringsinställningarna.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}