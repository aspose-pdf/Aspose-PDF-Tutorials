---
title: Kryptera PDF för endast formulärifyllning med AES‑256 med Aspose.Pdf för .NET
weight: 201
limit:
description: Lär dig hur du krypterar en PDF med AES‑256, begränsar den till endast formulärifyllning och anger visnings‑/ägarlösenord med Aspose.Pdf för .NET.
keywords: [Aspose.Pdf for .NET, PDF encryption .NET, restrict PDF permissions, form filling permission PDF, AES-256 PDF encryption, set PDF passwords .NET]
url: /net/security-permissions/encrypt-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Lär dig hur du krypterar en PDF med AES‑256, begränsar den till endast
    formulärifyllning och anger visnings‑/ägarlösenord med Aspose.Pdf för .NET.
  headline: Kryptera PDF för endast formulärifyllning med AES‑256 med Aspose.Pdf för
    .NET
  type: TechArticle
- description: Lär dig hur du krypterar en PDF med AES‑256, begränsar den till endast
    formulärifyllning och anger visnings‑/ägarlösenord med Aspose.Pdf för .NET.
  name: Kryptera PDF för endast formulärifyllning med AES‑256 med Aspose.Pdf för .NET
  steps:
  - name: Deklarera sökvägen till käll‑PDF‑filen, utskrivningssökvägen samt visnings‑
      och ägarlösenorden.
    text: Deklarera sökvägen till käll‑PDF‑filen, utskrivningssökvägen samt visnings‑
      och ägarlösenorden.
  - name: Kontrollera att källfilen finns; om den inte finns, skriv ett felmeddelande
      och avsluta.
    text: Kontrollera att källfilen finns; om den inte finns, skriv ett felmeddelande
      och avsluta.
  - name: Gå in i ett try‑block och öppna PDF‑dokumentet med en `using`‑sats, vilket
      skapar variabeln `pdfDoc`.
    text: Gå in i ett try‑block och öppna PDF‑dokumentet med en `using`‑sats, vilket
      skapar variabeln `pdfDoc`.
  - name: Skapa ett `Permissions`‑objekt som endast tillåter ifyllning av formulär.
    text: Skapa ett `Permissions`‑objekt som endast tillåter ifyllning av formulär.
  - name: Kryptera `pdfDoc` med visnings‑ och master‑lösenorden, tillämpa behörighetsuppsättningen
      och använd AES‑256.
    text: Kryptera `pdfDoc` med visnings‑ och master‑lösenorden, tillämpa behörighetsuppsättningen
      och använd AES‑256.
  - name: Spara den krypterade PDF‑filen till den angivna utdatafilen och stäng `using`‑blocket.
    text: Spara den krypterade PDF‑filen till den angivna utdatafilen och stäng `using`‑blocket.
  - name: Skriv ett bekräftelsemeddelande till konsolen och avsluta try‑blocket.
    text: Skriv ett bekräftelsemeddelande till konsolen och avsluta try‑blocket.
  - name: Fånga alla undantag, skriv ut dess meddelande till felströmmen och avsluta
      catch‑blocket.
    text: Fånga alla undantag, skriv ut dess meddelande till felströmmen och avsluta
      catch‑blocket.
  type: HowTo
- questions:
  - answer: '`Permissions.FillForm` tillåter användare att fylla i interaktiva formulärfält
      men inaktiverar alla andra åtgärder såsom utskrift, extrahering av innehåll
      eller ändring av dokumentstrukturen.'
    question: Vad tillåter och blockerar `Permissions.FillForm`‑flaggan egentligen
      i den krypterade PDF‑filen?
  - answer: Ja, ersätt `CryptoAlgorithm.AESx256` med `CryptoAlgorithm.AESx128` (eller
      ett annat stödd enum‑värde) i `pdfDoc.Encrypt`‑metoden för att ändra krypteringsstyrkan.
    question: Kan jag använda en annan krypteringsalgoritm, som AES‑128, med samma
      `Encrypt`‑anrop?
  - answer: Visningslösenordet (`readPass`) krävs för att öppna PDF‑filen och verkställa
      de angivna behörigheterna, medan ägarlösenordet (`fullPass`) ger full obegränsad
      åtkomst och kan användas för att ändra behörigheter eller ta bort kryptering.
    question: Vad är skillnaden mellan visningslösenordet (`viewerPwd`) och ägarlösenordet
      (`masterPwd`)?
  - answer: Att skicka `Permissions.None` (eller utelämna argumentet) resulterar i
      en PDF utan speciella begränsningar, vilket innebär att visningslösenordet fortfarande
      skyddar filen men användare kan utföra alla vanliga åtgärder som utskrift och
      kopiering.
    question: Om jag utelämnar argumentet `permissionSet` eller skickar `Permissions.None`,
      vilka behörigheter får PDF‑filen efter kryptering?
  type: FAQPage
images:
- /net/security-permissions/encrypt-form-filling/og-image.png
og_title: Kryptera en PDF för endast formulärifyllning med AES‑256
og_description: Säkra din PDF så att användare bara kan fylla i formulär, med AES‑256‑kryptering och lösenord i Aspose.Pdf för .NET.
og_image_alt: Skärmbild som visar stegen för att kryptera en PDF och begränsa den till formulärifyllning med Aspose.Pdf för .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kryptera PDF för endast formulärifyllning med AES‑256 med Aspose.Pdf för .NET
Den här handledningen visar hur man skyddar en befintlig PDF så att användare bara kan fylla i dess formulär. Den går igenom att öppna dokumentet med Aspose.Pdf för .NET, begränsa behörigheterna till formulärifyllning, tillämpa AES‑256‑kryptering, ange visnings‑ och ägarlösenord och slutligen spara den säkrade filen.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-form-filling" >}}


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

**Q: Vad tillåter och blockerar `Permissions.FillForm`‑flaggan egentligen i den krypterade PDF‑filen?**  
A: `Permissions.FillForm` tillåter användare att fylla i interaktiva formulärfält men inaktiverar alla andra åtgärder såsom utskrift, extrahering av innehåll eller ändring av dokumentstrukturen.

**Q: Kan jag använda en annan krypteringsalgoritm, som AES‑128, med samma `Encrypt`‑anrop?**  
A: Ja, ersätt `CryptoAlgorithm.AESx256` med `CryptoAlgorithm.AESx128` (eller ett annat stödd enum‑värde) i `pdfDoc.Encrypt`‑metoden för att ändra krypteringsstyrkan.

**Q: Vad är skillnaden mellan visningslösenordet (`viewerPwd`) och ägarlösenordet (`masterPwd`)?**  
A: Visningslösenordet (`readPass`) krävs för att öppna PDF‑filen och verkställa de angivna behörigheterna, medan ägarlösenordet (`fullPass`) ger full obegränsad åtkomst och kan användas för att ändra behörigheter eller ta bort kryptering.

**Q: Om jag utelämnar argumentet `permissionSet` eller skickar `Permissions.None`, vilka behörigheter får PDF‑filen efter kryptering?**  
A: Att skicka `Permissions.None` (eller utelämna argumentet) resulterar i en PDF utan speciella begränsningar, vilket innebär att visningslösenordet fortfarande skyddar filen men användare kan utföra alla vanliga åtgärder som utskrift och kopiering.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}