---
title: Kryptera PDF utan utskriftsbehörighet med Aspose.PDF för .NET
weight: 101
limit:
description: Lär dig hur du krypterar en PDF med AES‑256 och inaktiverar utskrift med Aspose.PDF för .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Lär dig hur du krypterar en PDF med AES‑256 och inaktiverar utskrift
    med Aspose.PDF för .NET.
  headline: Kryptera PDF utan utskriftsbehörighet med Aspose.PDF för .NET
  type: TechArticle
- description: Lär dig hur du krypterar en PDF med AES‑256 och inaktiverar utskrift
    med Aspose.PDF för .NET.
  name: Kryptera PDF utan utskriftsbehörighet med Aspose.PDF för .NET
  steps:
  - name: Definiera sökvägen till käll‑PDF‑filen, namn på den skyddade utdatafilen
      samt visar‑ och ägarlösenorden.
    text: Definiera sökvägen till käll‑PDF‑filen, namn på den skyddade utdatafilen
      samt visar‑ och ägarlösenorden.
  - name: Kontrollera att källfilen finns och avbryt med ett felmeddelande om den
      saknas.
    text: Kontrollera att källfilen finns och avbryt med ett felmeddelande om den
      saknas.
  - name: Öppna den ursprungliga PDF‑filen, ange inga behörigheter, kryptera den med
      AES‑256 med de angivna lösenorden och spara den skyddade filen.
    text: Öppna den ursprungliga PDF‑filen, ange inga behörigheter, kryptera den med
      AES‑256 med de angivna lösenorden och spara den skyddade filen.
  - name: Öppna den krypterade PDF‑filen igen med visarlösenordet och skriv dess IsEncrypted‑flagga
      till konsolen för att bekräfta skyddet.
    text: Öppna den krypterade PDF‑filen igen med visarlösenordet och skriv dess IsEncrypted‑flagga
      till konsolen för att bekräfta skyddet.
  - name: Skriv ut ett slutligt meddelande som indikerar att krypteringen är klar
      och visar utdatafilens namn.
    text: Skriv ut ett slutligt meddelande som indikerar att krypteringen är klar
      och visar utdatafilens namn.
  type: HowTo
- questions:
  - answer: '`Permissions` är en flagg‑enum; att tilldela `0` betyder att inga behörighetsbitar
      är satta, så Aspose.Pdf beviljar inte PrintDocument‑rättigheten och visaren
      kan inte skriva ut PDF‑filen.'
    question: Varför inaktiverar inställningen `Permissions rights = 0;` utskrift?
  - answer: Ja, ersätt `CryptoAlgorithm.AESx256` med `CryptoAlgorithm.AESx128` (eller
      ett annat stödjt enum‑värde) i anropet `pdfDoc.Encrypt`; resten av koden förblir
      oförändrad.
    question: Kan jag använda en annan krypteringsalgoritm, som AES‑128, med samma
      kod?
  - answer: Aspose.Pdf accepterar identiska lösenord, men ägarlösenordet ger då inga
      extra privilegier; PDF‑filen kommer fortfarande att vara krypterad, och de behörigheter
      du angav (inga) kommer att gälla.
    question: Vad händer om visarlösenordet och huvud‑ (ägarlösenordet) är identiska?
  - answer: Öppna den skyddade filen med visarlösenordet (`new Document(securedFile,
      viewerPwd)`) och försök skriva ut från en PDF‑visare; eftersom ingen `PrintDocument`‑behörighet
      har satts, kommer visaren att avvisa utskriftskommandot.
    question: Hur kan jag bekräfta att utskrift verkligen är blockerat efter kryptering?
  - answer: Koden kontrollerar `File.Exists(sourceFile)` och skriver ett fel till
      `Console.Error` innan den returnerar, vilket förhindrar att en `FileNotFoundException`
      kastas av `Document`‑konstruktorn.
    question: Vilket fel kastas om `original.pdf` inte finns, och hur ska jag hantera
      det?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: Kryptera PDF och blockera utskrift
og_description: Säkra din PDF med AES‑256‑kryptering och se till att den inte kan skrivas ut—steg‑för‑steg‑guide.
og_image_alt: Skärmdump som visar Aspose.PDF för .NET‑kod som krypterar en PDF och inaktiverar utskrift.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kryptera PDF utan utskriftsbehörighet med Aspose.PDF för .NET
Denna handledning visar hur man öppnar en befintlig PDF med Aspose.PDF för .NET, tillämpar AES‑256‑kryptering utan att bevilja några behörigheter—vilket i praktiken inaktiverar utskrift—sparar det säkrade dokumentet och bekräftar skyddet genom att öppna det med visarlösenordet. Följ den steg‑för‑steg‑koden för att säkerställa att din PDF inte kan skrivas ut efter kryptering.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


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

**Q: Varför inaktiverar inställningen `Permissions rights = 0;` utskrift?**  
A: `Permissions` är en flagg‑enum; att tilldela `0` betyder att inga behörighetsbitar är satta, så Aspose.Pdf beviljar inte PrintDocument‑rättigheten och visaren kan inte skriva ut PDF‑filen.

**Q: Kan jag använda en annan krypteringsalgoritm, som AES‑128, med samma kod?**  
A: Ja, ersätt `CryptoAlgorithm.AESx256` med `CryptoAlgorithm.AESx128` (eller ett annat stödjt enum‑värde) i anropet `pdfDoc.Encrypt`; resten av koden förblir oförändrad.

**Q: Vad händer om visarlösenordet och huvud‑ (ägarlösenordet) är identiska?**  
A: Aspose.Pdf accepterar identiska lösenord, men ägarlösenordet ger då inga extra privilegier; PDF‑filen kommer fortfarande att vara krypterad, och de behörigheter du angav (inga) kommer att gälla.

**Q: Hur kan jag bekräfta att utskrift verkligen är blockerat efter kryptering?**  
A: Öppna den skyddade filen med visarlösenordet (`new Document(securedFile, viewerPwd)`) och försök skriva ut från en PDF‑visare; eftersom ingen `PrintDocument`‑behörighet har satts, kommer visaren att avvisa utskriftskommandot.

**Q: Vilket fel kastas om `original.pdf` inte finns, och hur ska jag hantera det?**  
A: Koden kontrollerar `File.Exists(sourceFile)` och skriver ett fel till `Console.Error` innan den returnerar, vilket förhindrar att en `FileNotFoundException` kastas av `Document`‑konstruktorn.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}