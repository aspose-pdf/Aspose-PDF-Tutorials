---
title: PDF versleutelen zonder afdrukrechten met Aspose.PDF for .NET
weight: 101
limit:
description: Leer hoe u een PDF versleutelt met AES‑256 en afdrukken uitschakelt met Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Leer hoe u een PDF versleutelt met AES‑256 en afdrukken uitschakelt
    met Aspose.PDF for .NET.
  headline: PDF versleutelen zonder afdrukrechten met Aspose.PDF for .NET
  type: TechArticle
- description: Leer hoe u een PDF versleutelt met AES‑256 en afdrukken uitschakelt
    met Aspose.PDF for .NET.
  name: PDF versleutelen zonder afdrukrechten met Aspose.PDF for .NET
  steps:
  - name: Definieer het pad naar de bron‑PDF, de naam van het beveiligde uitvoerbestand,
      en de weergave‑ en eigenaar‑wachtwoorden.
    text: Definieer het pad naar de bron‑PDF, de naam van het beveiligde uitvoerbestand,
      en de weergave‑ en eigenaar‑wachtwoorden.
  - name: Controleer of het bronbestand bestaat en annuleer met een foutmelding als
      het ontbreekt.
    text: Controleer of het bronbestand bestaat en annuleer met een foutmelding als
      het ontbreekt.
  - name: Open de originele PDF, stel geen rechten in, versleutel deze met AES‑256
      met de opgegeven wachtwoorden, en sla het beveiligde bestand op.
    text: Open de originele PDF, stel geen rechten in, versleutel deze met AES‑256
      met de opgegeven wachtwoorden, en sla het beveiligde bestand op.
  - name: Open de versleutelde PDF opnieuw met het weergave‑wachtwoord en schrijf
      de IsEncrypted‑vlag naar de console om de bescherming te bevestigen.
    text: Open de versleutelde PDF opnieuw met het weergave‑wachtwoord en schrijf
      de IsEncrypted‑vlag naar de console om de bescherming te bevestigen.
  - name: Print een laatste bericht dat aangeeft dat de versleuteling voltooid is
      en de naam van het uitvoerbestand.
    text: Print een laatste bericht dat aangeeft dat de versleuteling voltooid is
      en de naam van het uitvoerbestand.
  type: HowTo
- questions:
  - answer: '`Permissions` is een flag‑enum; het toewijzen van `0` betekent dat er
      geen permissie‑bits zijn ingesteld, waardoor Aspose.Pdf het PrintDocument‑recht
      niet verleent en de viewer de PDF niet kan afdrukken.'
    question: Waarom schakelt het instellen van `Permissions rights = 0;` afdrukken
      uit?
  - answer: Ja, vervang `CryptoAlgorithm.AESx256` door `CryptoAlgorithm.AESx128` (of
      een andere ondersteunde enum‑waarde) in de `pdfDoc.Encrypt`‑aanroep; de rest
      van de code blijft ongewijzigd.
    question: Kan ik een ander versleutelingsalgoritme gebruiken, zoals AES‑128, met
      dezelfde code?
  - answer: Aspose.Pdf accepteert identieke wachtwoorden, maar het eigenaar‑wachtwoord
      biedt dan geen extra privileges meer; de PDF blijft wel versleuteld en de door
      u opgegeven rechten (geen) worden toegepast.
    question: Wat gebeurt er als het weergave‑wachtwoord en het master‑ (eigenaar‑)wachtwoord
      hetzelfde zijn?
  - answer: Open het beveiligde bestand met het weergave‑wachtwoord (`new Document(securedFile,
      viewerPwd)`) en probeer te printen vanuit een PDF‑viewer; omdat er geen `PrintDocument`‑recht
      is ingesteld, zal de viewer de afdrukopdracht weigeren.
    question: Hoe kan ik bevestigen dat afdrukken echt geblokkeerd is na versleuteling?
  - answer: De code controleert `File.Exists(sourceFile)` en schrijft een fout naar
      `Console.Error` voordat hij terugkeert, waardoor een `FileNotFoundException`
      die door de `Document`‑constructor zou worden gegooid, wordt voorkomen.
    question: Welke fout wordt gegooid als `original.pdf` niet bestaat, en hoe moet
      ik die afhandelen?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: PDF versleutelen en afdrukken blokkeren
og_description: Beveilig uw PDF met AES‑256‑versleuteling en zorg ervoor dat deze niet kan worden afgedrukt — stap‑voor‑stap gids.
og_image_alt: Schermafbeelding die Aspose.PDF for .NET code toont die een PDF versleutelt en afdrukken uitschakelt.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF versleutelen zonder afdrukrechten met Aspose.PDF
Deze tutorial laat zien hoe u een bestaande PDF opent met Aspose.PDF for .NET, AES‑256‑versleuteling toepast zonder rechten toe te kennen — waardoor afdrukken effectief wordt uitgeschakeld — het beveiligde document opslaat, en de bescherming bevestigt door het te openen met het weergave‑wachtwoord. Volg de stap‑voor‑stap code om er zeker van te zijn dat uw PDF na versleuteling niet kan worden afgedrukt.

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

**Q: Waarom schakelt het instellen van `Permissions rights = 0;` afdrukken uit?**  
A: `Permissions` is een flag‑enum; het toewijzen van `0` betekent dat er geen permissie‑bits zijn ingesteld, waardoor Aspose.Pdf het PrintDocument‑recht niet verleent en de viewer de PDF niet kan afdrukken.

**Q: Kan ik een ander versleutelingsalgoritme gebruiken, zoals AES‑128, met dezelfde code?**  
A: Ja, vervang `CryptoAlgorithm.AESx256` door `CryptoAlgorithm.AESx128` (of een andere ondersteunde enum‑waarde) in de `pdfDoc.Encrypt`‑aanroep; de rest van de code blijft ongewijzigd.

**Q: Wat gebeurt er als het weergave‑wachtwoord en het master‑ (eigenaar‑)wachtwoord hetzelfde zijn?**  
A: Aspose.Pdf accepteert identieke wachtwoorden, maar het eigenaar‑wachtwoord biedt dan geen extra privileges meer; de PDF blijft wel versleuteld en de door u opgegeven rechten (geen) worden toegepast.

**Q: Hoe kan ik bevestigen dat afdrukken echt geblokkeerd is na versleuteling?**  
A: Open het beveiligde bestand met het weergave‑wachtwoord (`new Document(securedFile, viewerPwd)`) en probeer te printen vanuit een PDF‑viewer; omdat er geen `PrintDocument`‑recht is ingesteld, zal de viewer de afdrukopdracht weigeren.

**Q: Welke fout wordt gegooid als `original.pdf` niet bestaat, en hoe moet ik die afhandelen?**  
A: De code controleert `File.Exists(sourceFile)` en schrijft een fout naar `Console.Error` voordat hij terugkeert, waardoor een `FileNotFoundException` die door de `Document`‑constructor zou worden gegooid, wordt voorkomen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}