---
title: PDF versleutelen om alleen formulierinvulling toe te staan met Aspose.Pdf for .NET
weight: 101
limit:
description: Leer hoe je een PDF versleutelt met AES‑256, wachtwoorden instelt en de permissies beperkt tot alleen formulierinvulling met Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, encrypt PDF, PDF form filling permissions, AES-256 PDF encryption, viewer password PDF, owner password PDF]
url: /net/security-permissions/encrypt-pdf-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Leer hoe je een PDF versleutelt met AES‑256, wachtwoorden instelt en
    de permissies beperkt tot alleen formulierinvulling met Aspose.Pdf for .NET.
  headline: PDF versleutelen om alleen formulierinvulling toe te staan met Aspose.Pdf
    for .NET
  type: TechArticle
- description: Leer hoe je een PDF versleutelt met AES‑256, wachtwoorden instelt en
    de permissies beperkt tot alleen formulierinvulling met Aspose.Pdf for .NET.
  name: PDF versleutelen om alleen formulierinvulling toe te staan met Aspose.Pdf
    for .NET
  steps:
  - name: Definieer de bron- en doelbestandspaden en de viewer- en owner-wachtwoorden.
    text: Definieer de bron- en doelbestandspaden en de viewer- en owner-wachtwoorden.
  - name: Controleer of de bron‑PDF bestaat en annuleer met een foutmelding als dat
      niet het geval is.
    text: Controleer of de bron‑PDF bestaat en annuleer met een foutmelding als dat
      niet het geval is.
  - name: Start een try‑block om eventuele fouten die tijdens de verwerking kunnen
      optreden af te handelen.
    text: Start een try‑block om eventuele fouten die tijdens de verwerking kunnen
      optreden af te handelen.
  - name: Open het bestaande PDF‑bestand door een Document‑object met de naam pdfDoc
      te maken.
    text: Open het bestaande PDF‑bestand door een Document‑object met de naam pdfDoc
      te maken.
  - name: Stel de permissies in om alleen formulierinvulling toe te staan, versleutel
      het document met viewer- en owner-wachtwoorden met AES‑256, en sla de beveiligde
      PDF op.
    text: Stel de permissies in om alleen formulierinvulling toe te staan, versleutel
      het document met viewer- en owner-wachtwoorden met AES‑256, en sla de beveiligde
      PDF op.
  - name: Schrijf een bevestigingsbericht naar de console en sluit het try‑block.
    text: Schrijf een bevestigingsbericht naar de console en sluit het try‑block.
  - name: Vang eventuele uitzonderingen op en geef het foutbericht weer in de console.
    text: Vang eventuele uitzonderingen op en geef het foutbericht weer in de console.
  type: HowTo
- questions:
  - answer: Wanneer het wordt geopend met het viewer‑ (gebruiker‑)wachtwoord, kan
      het document worden bekeken en kunnen formuliervelden worden ingevuld, maar
      alle andere handelingen zoals tekst bewerken, annotaties toevoegen of inhoud
      extraheren zijn geblokkeerd.
    question: Wat kan een gebruiker met de PDF doen nadat deze is versleuteld met
      `Permissions.FillForm`?
  - answer: Combineer permissies met de bitwise OR‑operator, bijv. `Permissions allowed
      = Permissions.FillForm | Permissions.Printing;` en geef de gecombineerde waarde
      door aan `pdfDoc.Encrypt`.
    question: Hoe kan ik extra rechten toestaan, zoals afdrukken, terwijl ik de rest
      nog steeds beperk?
  - answer: Ja. Het eerste argument is het gebruikers‑ (viewer) wachtwoord dat de
      beperkte rechten verleent, en het tweede argument is het eigenaar‑ (admin) wachtwoord
      dat volledige controle over het document geeft.
    question: Is de volgorde van de wachtwoorden in `pdfDoc.Encrypt(viewerPass, adminPass,
      …)` van belang?
  - answer: Aspose.Pdf zal een uitzondering gooien bij het proberen te openen van
      een al versleuteld bestand; je moet het eerst openen met het bestaande wachtwoord,
      de bescherming verwijderen of aanpassen, en vervolgens de nieuwe versleutelingsinstellingen
      toepassen.
    question: Wat gebeurt er als de bron‑PDF al met een wachtwoord is beveiligd?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-form-filling/og-image.png
og_title: PDF versleutelen en alleen formulierinvulling toestaan
og_description: Beveilig je PDF met AES‑256 en laat gebruikers formulieren invullen, maar niets anders.
og_image_alt: Schermafbeelding die Aspose.Pdf for .NET‑code toont die een PDF versleutelt en beperkt tot alleen formulierinvulling
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF versleutelen om alleen formulierinvulling toe te staan met Aspose.Pdf
In deze tutorial leer je hoe je een bestaande PDF opent met Aspose.Pdf for .NET, AES‑256‑versleuteling toepast, viewer- en owner-wachtwoorden instelt, en de permissies van het document beperkt zodat ontvangers alleen formuliervelden kunnen invullen. Deze aanpak is handig wanneer je de inhoud wilt beschermen, maar gebruikers toch interactieve formulieren wilt laten invullen. De code loopt stap voor stap door het proces en slaat de beveiligde PDF op, klaar voor distributie.

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

**Q: Wat kan een gebruiker met de PDF doen nadat deze is versleuteld met `Permissions.FillForm`?**  
A: Wanneer het wordt geopend met het viewer‑ (gebruiker‑)wachtwoord, kan het document worden bekeken en kunnen formuliervelden worden ingevuld, maar alle andere handelingen zoals tekst bewerken, annotaties toevoegen of inhoud extraheren zijn geblokkeerd.

**Q: Hoe kan ik extra rechten toestaan, zoals afdrukken, terwijl ik de rest nog steeds beperk?**  
A: Combineer permissies met de bitwise OR‑operator, bijv. `Permissions allowed = Permissions.FillForm | Permissions.Printing;` en geef de gecombineerde waarde door aan `pdfDoc.Encrypt`.

**Q: Is de volgorde van de wachtwoorden in `pdfDoc.Encrypt(viewerPass, adminPass, …)` van belang?**  
A: Ja. Het eerste argument is het gebruikers‑ (viewer) wachtwoord dat de beperkte rechten verleent, en het tweede argument is het eigenaar‑ (admin) wachtwoord dat volledige controle over het document geeft.

**Q: Wat gebeurt er als de bron‑PDF al met een wachtwoord is beveiligd?**  
A: Aspose.Pdf zal een uitzondering gooien bij het proberen te openen van een al versleuteld bestand; je moet het eerst openen met het bestaande wachtwoord, de bescherming verwijderen of aanpassen, en vervolgens de nieuwe versleutelingsinstellingen toepassen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}