---
"description": "Leer hoe u PDF-bestanden ondertekent met een smartcard met Aspose.PDF voor .NET. Volg deze stapsgewijze handleiding voor veilige digitale handtekeningen."
"linktitle": "Ondertekenen met smartcard met behulp van PDF-bestandshandtekening"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Ondertekenen met smartcard met behulp van PDF-bestandshandtekening"
"url": "/nl/net/programming-with-security-and-signatures/sign-with-smart-card-using-pdf-file-signature/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ondertekenen met smartcard met behulp van PDF-bestandshandtekening

## Invoering

In het digitale tijdperk is het beveiligen van documenten belangrijker dan ooit. Of het nu gaat om een contract, een overeenkomst of gevoelige informatie, het is van het grootste belang dat het document authentiek is en er niet mee is geknoeid. Digitale handtekeningen zijn in de maak! Vandaag gaan we dieper in op hoe je een PDF-bestand kunt ondertekenen met een smartcard met Aspose.PDF voor .NET. Deze krachtige bibliotheek stelt ontwikkelaars in staat om PDF-documenten efficiënt te bewerken en te creëren, inclusief het toevoegen van veilige digitale handtekeningen. Dus pak je smartcard en laten we aan de slag gaan!

## Vereisten

Voordat we ingaan op de details van het ondertekenen van een PDF-bestand, willen we eerst controleren of je alles hebt wat je nodig hebt. Hier is een checklist om je te helpen bij de voorbereiding:

1. Aspose.PDF voor .NET: Zorg ervoor dat de Aspose.PDF-bibliotheek geïnstalleerd is. U kunt deze downloaden van de [site](https://releases.aspose.com/pdf/net/).
2. Visual Studio: een ontwikkelomgeving waarin u uw .NET-code kunt schrijven en uitvoeren.
3. Smartcard: U hebt een smartcard nodig met een geldig digitaal certificaat.
4. Basiskennis van C#: Kennis van C#-programmering is nuttig omdat we codefragmenten in deze taal gaan schrijven.
5. PDF-document: een voorbeeld-PDF-bestand (zoals `blank.pdf`) om ons ondertekeningsproces te testen.

Nu u aan deze vereisten hebt voldaan, bent u klaar om met code aan de slag te gaan!

## Pakketten importeren

Laten we eerst de benodigde pakketten importeren. Je moet referenties toevoegen aan de Aspose.PDF-bibliotheek in je project. Zo doe je dat:

1. Visual Studio openen.
2. Maak een nieuw project of open een bestaand project.
3. Klik met de rechtermuisknop op uw project in de Solution Explorer en selecteer `Manage NuGet Packages`.
4. Zoeken naar `Aspose.PDF` en installeer de nieuwste versie.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nu we de benodigde pakketten hebben geïmporteerd, kunnen we de code stap voor stap doornemen.

## Stap 1: Stel uw document in

De eerste stap in ons proces is het aanmaken van het PDF-document dat we willen ondertekenen. Zo doet u dat:

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
Document doc = new Document(dataDir + "blank.pdf");
```
In dit fragment definiëren we het pad naar onze documentenmap en maken we een exemplaar van de `Document` klasse met behulp van een voorbeeld PDF-bestand met de naam `blank.pdf`Zorg ervoor dat u deze vervangt `"YOUR DOCUMENTS DIRECTORY"` met het werkelijke pad waar uw PDF zich bevindt.

## Stap 2: Initialiseer PdfFileSignature

Vervolgens initialiseren we de `PdfFileSignature` klasse, die verantwoordelijk is voor de afhandeling van het ondertekeningsproces.

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature())
{
    pdfSign.BindPdf(doc);
```
Hier maken we een instantie van `PdfFileSignature` en bind het aan ons PDF-document. Dit maakt het document klaar voor ondertekening.

## Stap 3: Toegang tot het smartcardcertificaat

Nu komt het cruciale deel: toegang krijgen tot het digitale certificaat dat op uw smartcard is opgeslagen. Zo doen we dat:

### Open de certificaatopslag

```csharp
System.Security.Cryptography.X509Certificates.X509Store store = new System.Security.Cryptography.X509Certificates.X509Store(System.Security.Cryptography.X509Certificates.StoreLocation.CurrentUser);
store.Open(System.Security.Cryptography.X509Certificates.OpenFlags.ReadOnly);
```
We openen de certificaatopslag in het profiel van de huidige gebruiker. Dit geeft ons toegang tot de certificaten die op uw computer zijn geïnstalleerd, inclusief die op uw smartcard.

### Selecteer het certificaat

```csharp
System.Security.Cryptography.X509Certificates.X509Certificate2Collection sel =
    System.Security.Cryptography.X509Certificates.X509Certificate2UI.SelectFromCollection(
        store.Certificates, null, null, System.Security.Cryptography.X509Certificates.X509SelectionFlag.SingleSelection);
```
Deze code vraagt de gebruiker een certificaat uit de verzameling te selecteren. De gebruikersinterface toont alle beschikbare certificaten, zodat u het certificaat kunt kiezen dat aan uw smartcard is gekoppeld.

## Stap 4: De externe handtekening maken

Nadat u uw certificaat hebt geselecteerd, is de volgende stap het maken van een externe handtekening met behulp van het geselecteerde certificaat.

```csharp
Aspose.Pdf.Forms.ExternalSignature externalSignature = new Aspose.Pdf.Forms.ExternalSignature(sel[0]);
```
Hier maken we een instantie van `ExternalSignature` met behulp van het geselecteerde certificaat. Dit object wordt gebruikt om het PDF-document te ondertekenen.

## Stap 5: Handtekeninguiterlijk instellen

Laten we nu het uiterlijk van onze handtekening instellen. Hier kunt u aanpassen hoe uw handtekening er in het document uitziet.

```csharp
pdfSign.SignatureAppearance = dataDir + "demo.png";
```
In dit fragment specificeren we het uiterlijk van de handtekening door het pad naar een afbeeldingsbestand (zoals een logo of een afbeelding van een handtekening) op te geven. Zorg ervoor dat u `"demo.png"` met de afbeelding die u daadwerkelijk wilt gebruiken.

## Stap 6: Onderteken de PDF

Zodra alles is ingesteld, is het tijd om het PDF-document te ondertekenen!

```csharp
pdfSign.Sign(1, "Reason", "Contact", "Location", true, new System.Drawing.Rectangle(100, 100, 200, 200), externalSignature);
pdfSign.Save(dataDir + "externalSignature2.pdf");
```
In deze stap noemen we de `Sign` methode op onze `pdfSign` object. Dit is wat elke parameter betekent:
- `1`: Het paginanummer waarop de handtekening zal verschijnen.
- `"Reason"`: De reden voor het ondertekenen van het document.
- `"Contact"`: Contactgegevens van de ondertekenaar.
- `"Location"`: De locatie van de ondertekenaar.
- `true`: Geeft aan of er een zichtbare handtekening moet worden gemaakt.
- `new System.Drawing.Rectangle(100, 100, 200, 200)`: De positie en grootte van de handtekening op het PDF-bestand.
- `externalSignature`: Het handtekeningobject dat we eerder hebben gemaakt.

Ten slotte slaan we het ondertekende document op als `externalSignature2.pdf`.

## Stap 7: Controleer de handtekening

Nadat u het document hebt ondertekend, is het essentieel om te controleren of de handtekening geldig is. Zo doet u dat:

### Initialiseer verificatieproces

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature(new Document(dataDir + "externalSignature2.pdf")))
{
    IList<string> sigNames = pdfSign.GetSignNames();
```
We creëren een nieuw exemplaar van `PdfFileSignature` voor het ondertekende document. Vervolgens halen we de namen op van alle handtekeningen die in het document aanwezig zijn.

### Controleer de geldigheid van de handtekening

```csharp
for (int index = 0; index <= sigNames.Count - 1; index++)
{
    if (!pdfSign.VerifySigned(sigNames[index]) || !pdfSign.VerifySignature(sigNames[index]))
    {
        throw new ApplicationException("Not verified");
    }
}
```
We doorlopen elke handtekeningnaam en controleren de geldigheid ervan. Als een handtekening de verificatie niet doorstaat, wordt er een uitzondering gegenereerd die aangeeft dat de handtekening ongeldig is.

## Conclusie

En voilà! U hebt met succes een PDF-document ondertekend met een smartcard met Aspose.PDF voor .NET. Dit proces beveiligt uw document niet alleen, maar voegt ook een authenticiteitslaag toe die cruciaal is in de digitale wereld van vandaag. Of u nu te maken hebt met contracten, juridische documenten of andere gevoelige informatie, weten hoe u digitale handtekeningen implementeert, is een waardevolle vaardigheid. 

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een krachtige bibliotheek waarmee ontwikkelaars PDF-documenten kunnen maken, bewerken en converteren in .NET-toepassingen.

### Heb ik een smartcard nodig om PDF's te ondertekenen?
Hoewel een smartcard niet verplicht is, wordt deze voor veilige digitale handtekeningen wel sterk aanbevolen, omdat deze een extra beveiligingslaag biedt.

### Kan ik elk PDF-bestand gebruiken om te ondertekenen?
Ja, je kunt elk PDF-bestand gebruiken, maar zorg ervoor dat het niet met een wachtwoord is beveiligd. Als dat wel zo is, moet je het eerst ontgrendelen.

### Wat als ik geen digitaal certificaat heb?
kunt een digitaal certificaat verkrijgen van een vertrouwde certificeringsinstantie (CA) of een zelfondertekend certificaat gebruiken voor testdoeleinden.

### Is er een proefversie van Aspose.PDF beschikbaar?
Ja, u kunt een gratis proefversie downloaden van de [Aspose-website](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}