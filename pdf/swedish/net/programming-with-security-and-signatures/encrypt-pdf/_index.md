---
title: Kryptera PDF med användar‑ och ägarlösenord med Aspose.PDF för .NET
weight: 220
limit:
description: Lär dig att ladda en PDF, begränsa behörigheter, kryptera den med användar‑ och ägarlösenord med AES‑256 och spara det skyddade dokumentet med Aspose.PDF för .NET.
keywords: [pdf encryption, Aspose.PDF for .NET, aes-256 pdf protection, user password pdf, owner password pdf, restrict pdf permissions]
url: /net/programming-with-security-and-signatures/encrypt-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Lär dig att ladda en PDF, begränsa behörigheter, kryptera den med användar‑
    och ägarlösenord med AES‑256 och spara det skyddade dokumentet med Aspose.PDF
    för .NET.
  headline: Kryptera PDF med användar‑ och ägarlösenord med Aspose.PDF för .NET
  type: TechArticle
- description: Lär dig att ladda en PDF, begränsa behörigheter, kryptera den med användar‑
    och ägarlösenord med AES‑256 och spara det skyddade dokumentet med Aspose.PDF
    för .NET.
  name: Kryptera PDF med användar‑ och ägarlösenord med Aspose.PDF för .NET
  steps:
  - name: Deklarera sökvägarna för käll‑ och destinationsfilen samt användar‑ (klient)
      och ägar‑ (admin) lösenorden.
    text: Deklarera sökvägarna för käll‑ och destinationsfilen samt användar‑ (klient)
      och ägar‑ (admin) lösenorden.
  - name: Kontrollera att käll‑PDF‑filen finns och avbryt med ett felmeddelande om
      den inte gör det.
    text: Kontrollera att käll‑PDF‑filen finns och avbryt med ett felmeddelande om
      den inte gör det.
  - name: Öppna PDF‑filen, tillåt endast innehållsändring och extraktion, kryptera
      den med de två lösenorden med AES‑256, spara den skyddade filen och visa ett
      lyckat meddelande.
    text: Öppna PDF‑filen, tillåt endast innehållsändring och extraktion, kryptera
      den med de två lösenorden med AES‑256, spara den skyddade filen och visa ett
      lyckat meddelande.
  - name: Fånga eventuella fel som uppstår och skriv undantagsmeddelandet till felkonsolen.
    text: Fånga eventuella fel som uppstår och skriv undantagsmeddelandet till felkonsolen.
  type: HowTo
- questions:
  - answer: '`Permissions.ModifyContent` låter användaren redigera PDF:ens text och
      objekt, medan `Permissions.ExtractContent` möjliggör kopiering av text eller
      bilder. Tillsammans möjliggör de redigering och extraktion av innehåll men blockerar
      fortfarande utskrift eftersom `Permissions.Print` inte är inkluderat.'
    question: Vilka behörigheter ges när jag kombinerar `Permissions.ModifyContent`
      med `Permissions.ExtractContent`?
  - answer: Ja, ersätt `CryptoAlgorithm.AESx256` med ett annat enum‑värde som `CryptoAlgorithm.AESx128`
      i `Encrypt`‑anropet; resten av koden förblir densamma.
    question: Kan jag använda en annan krypteringsalgoritm, som AES‑128, istället
      för `CryptoAlgorithm.AESx256`?
  - answer: Användarlösenordet (`clientPwd`) krävs för att öppna PDF‑filen och verkställer
      de angivna behörigheterna, medan ägarlösenordet (`adminPwd`) ger full åtkomst
      och låter innehavaren ändra behörigheter eller ta bort kryptering.
    question: Vad är den praktiska skillnaden mellan användar‑ (klient) lösenordet
      och ägarlösenordet (admin)?
  - answer: PDF‑filen kommer fortfarande att vara krypterad, men skillnaden mellan
      användar‑ och ägarrättigheter försvinner; den som känner till det enda lösenordet
      får full åtkomst, vilket i praktiken gör behörighetsinställningarna meningslösa.
    question: Vad händer om jag använder samma sträng för både klient‑ och admin‑lösenorden?
  type: FAQPage
images:
- /net/programming-with-security-and-signatures/encrypt-pdf/og-image.png
og_title: Kryptera en PDF med användar‑ och ägarlösenord (AES‑256)
og_description: Säkra din PDF genom att lägga till både användar‑ och ägarlösenord med AES‑256‑kryptering på några minuter.
og_image_alt: Guide som visar hur man krypterar en PDF med användar‑ och ägarlösenord med AES‑256 i Aspose.PDF för .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kryptera PDF med användar‑ och ägarlösenord med Aspose.PDF för .NET
Den här handledningen guidar dig genom att ladda en befintlig PDF med Aspose.PDF, tillämpa behörighetsrestriktioner och säkra dokumentet genom att kryptera det med både ett användar‑ (klient) och ett ägar‑ (admin) lösenord med AES‑256‑algoritmen, innan den skyddade filen sparas.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-security-and-signatures/encrypt-pdf" >}}


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

**Q: Vilka behörigheter ges när jag kombinerar `Permissions.ModifyContent` med `Permissions.ExtractContent`?**  
A: `Permissions.ModifyContent` låter användaren redigera PDF:ens text och objekt, medan `Permissions.ExtractContent` möjliggör kopiering av text eller bilder. Tillsammans möjliggör de redigering och extraktion av innehåll men blockerar fortfarande utskrift eftersom `Permissions.Print` inte är inkluderat.

**Q: Kan jag använda en annan krypteringsalgoritm, som AES‑128, istället för `CryptoAlgorithm.AESx256`?**  
A: Ja, ersätt `CryptoAlgorithm.AESx256` med ett annat enum‑värde som `CryptoAlgorithm.AESx128` i `Encrypt`‑anropet; resten av koden förblir densamma.

**Q: Vad är den praktiska skillnaden mellan användar‑ (klient) lösenordet och ägarlösenordet (admin)?**  
A: Användarlösenordet (`clientPwd`) krävs för att öppna PDF‑filen och verkställer de angivna behörigheterna, medan ägarlösenordet (`adminPwd`) ger full åtkomst och låter innehavaren ändra behörigheter eller ta bort kryptering.

**Q: Vad händer om jag använder samma sträng för både klient‑ och admin‑lösenorden?**  
A: PDF‑filen kommer fortfarande att vara krypterad, men skillnaden mellan användar‑ och ägarrättigheter försvinner; den som känner till det enda lösenordet får full åtkomst, vilket i praktiken gör behörighetsinställningarna meningslösa.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}