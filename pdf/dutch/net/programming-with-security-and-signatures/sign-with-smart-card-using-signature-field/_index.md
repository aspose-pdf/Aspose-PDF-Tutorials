---
"description": "Leer hoe u PDF's veilig kunt ondertekenen met een smartcard met Aspose.PDF voor .NET. Volg onze stapsgewijze handleiding voor eenvoudige implementatie."
"linktitle": "Ondertekenen met smartcard met behulp van handtekeningveld"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Ondertekenen met smartcard met behulp van handtekeningveld"
"url": "/nl/net/programming-with-security-and-signatures/sign-with-smart-card-using-signature-field/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ondertekenen met smartcard met behulp van handtekeningveld

## Invoering

In de digitale wereld van vandaag is het beveiligen van documenten belangrijker dan ooit. Of u nu een ontwikkelaar, bedrijfseigenaar of gewoon iemand bent die gevoelige informatie verwerkt, weten hoe u PDF's elektronisch kunt ondertekenen, bespaart u tijd en zorgt u ervoor dat uw documenten worden geverifieerd. In deze handleiding leiden we u door het proces van het ondertekenen van een PDF met een smartcard en een handtekeningveld met Aspose.PDF voor .NET. 

## Vereisten

Voordat we ingaan op de details van het ondertekeningsproces, willen we ervoor zorgen dat je alles hebt wat je nodig hebt om te beginnen. Hier is een checklist met vereisten:

1. Aspose.PDF voor .NET: Zorg ervoor dat de Aspose.PDF-bibliotheek in uw .NET-omgeving is geïnstalleerd. U kunt deze downloaden van de [site](https://releases.aspose.com/pdf/net/).

2. Visual Studio: Je hebt een IDE nodig om je .NET-code te schrijven en uit te voeren. Visual Studio Community Edition is een geweldige gratis optie.

3. Een smartcard: Deze is essentieel voor het ondertekenen van uw PDF. Zorg ervoor dat u een smartcardlezer en de benodigde certificaten op uw computer hebt geïnstalleerd.

4. Basiskennis van C#: Kennis van C#-programmering helpt u de codefragmenten te begrijpen die we gaan gebruiken.

5. Voorbeeld PDF-document: Zorg dat u een voorbeeld PDF-document bij de hand hebt om te testen. U kunt een lege PDF maken of een bestaand PDF-document gebruiken.

## Pakketten importeren

Voordat we beginnen met coderen, importeren we de benodigde pakketten. Je moet de volgende naamruimten in je C#-bestand opnemen:

```csharp
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Via deze naamruimten krijgt u toegang tot de klassen en methoden die nodig zijn voor het werken met PDF's en het verwerken van digitale handtekeningen.

## Stapsgewijze handleiding voor het ondertekenen van een PDF met een smartcard

Nu we onze vereisten op een rijtje hebben, kunnen we het ondertekeningsproces opsplitsen in beheersbare stappen. We nemen elke stap gedetailleerd door, zodat u begrijpt wat er onder de motorkap gebeurt.

### Stap 1: Stel uw documentenmap in

Wat u moet doen: Definieer het pad naar uw documentenmap.

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
```

Uitleg: Vervangen `"YOUR DOCUMENTS DIRECTORY"` met het daadwerkelijke pad waar uw PDF-bestanden zich bevinden. Hier lezen we de lege PDF en slaan we het ondertekende document op.

### Stap 2: Kopieer de lege PDF

Wat u moet doen: Maak een kopie van uw lege PDF om mee te werken.

```csharp
File.Copy(dataDir + "blank.pdf", dataDir + "externalSignature1.pdf", true);
```

Uitleg: Deze regel kopieert de `blank.pdf` bestand naar een nieuw bestand met de naam `externalSignature1.pdf`. De `true` parameter maakt overschrijven mogelijk als het bestand al bestaat.

### Stap 3: Open het PDF-document

Wat u moet doen: Open de gekopieerde PDF om te lezen en schrijven.

```csharp
using (FileStream fs = new FileStream(dataDir + "externalSignature1.pdf", FileMode.Open, FileAccess.ReadWrite))
{
    using (Document doc = new Document(fs))
    {
        // Verdere stappen zullen hier plaatsvinden
    }
}
```

Uitleg: Wij gebruiken een `FileStream` om ons PDF-bestand te openen. De `Document` klasse van Aspose.PDF stelt ons in staat de inhoud van een PDF te manipuleren.

### Stap 4: Een handtekeningveld maken

Wat u moet doen: Definieer een handtekeningveld in het PDF-bestand waar de handtekening moet worden geplaatst.

```csharp
SignatureField field1 = new SignatureField(doc.Pages[1], new Rectangle(100, 400, 10, 10));
```

Uitleg: Hier maken we een `SignatureField` op de tweede pagina (pagina-index begint bij 1) van de PDF. De `Rectangle` Definieert de positie en grootte van het handtekeningveld.

### Stap 5: Toegang tot de Smart Card-certificaatopslag

Wat u moet doen: Open de certificaatopslag om uw smartcardcertificaat te selecteren.

```csharp
X509Store store = new X509Store(StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly);
```

Uitleg: We hebben toegang tot de certificaatopslag van de huidige gebruiker. Hier worden uw smartcardcertificaten opgeslagen.

### Stap 6: Selecteer het certificaat

Wat u moet doen: De gebruiker vragen een certificaat uit de winkel te selecteren.

```csharp
X509Certificate2Collection sel = X509Certificate2UI.SelectFromCollection(store.Certificates, null, null, X509SelectionFlag.SingleSelection);
```

Uitleg: Deze regel opent een dialoogvenster waarin u een certificaat kunt selecteren. U kunt het certificaat kiezen dat aan uw smartcard is gekoppeld.

### Stap 7: Een externe handtekening maken

Wat te doen: Maak een exemplaar van `ExternalSignature` met behulp van het geselecteerde certificaat.

```csharp
Aspose.Pdf.Forms.ExternalSignature externalSignature = new Aspose.Pdf.Forms.ExternalSignature(sel[0])
{
    Authority = "Me",
    Reason = "Reason",
    ContactInfo = "Contact"
};
```

Uitleg: We initialiseren de `ExternalSignature` met het geselecteerde certificaat. U kunt ook de autoriteit, de reden voor ondertekening en de contactgegevens instellen.

### Stap 8: Voeg het handtekeningveld toe aan het document

Wat u moet doen: Voeg het handtekeningveld toe aan het document.

```csharp
field1.PartialName = "sig1";
doc.Form.Add(field1, 1);
```

Uitleg: We geven het handtekeningveld een naam en voegen het toe aan de eerste pagina van het document. Dit maakt de PDF klaar voor ondertekening.

### Stap 9: Onderteken het document

Wat u moet doen: Gebruik de externe handtekening om het PDF-bestand te ondertekenen.

```csharp
field1.Sign(externalSignature);
doc.Save();
```

Uitleg: Deze regel ondertekent het document met de externe handtekening en slaat de wijzigingen op in de PDF. Uw document is nu ondertekend!

### Stap 10: Controleer de handtekening

Wat u moet doen: Controleer of de handtekening geldig is.

```csharp
using (PdfFileSignature pdfSign = new PdfFileSignature(new Document(dataDir + "externalSignature1.pdf")))
{
    IList<string> sigNames = pdfSign.GetSignNames();
    for (int index = 0; index <= sigNames.Count - 1; index++)
    {
        if (!pdfSign.VerifySigned(sigNames[index]) || !pdfSign.VerifySignature(sigNames[index]))
        {
            throw new ApplicationException("Not verified");
        }
    }
}
```

Uitleg: We maken een instantie van `PdfFileSignature` om de handtekeningen in het document te verifiëren. Als de handtekening niet geldig is, wordt er een uitzondering gegenereerd.

## Conclusie

Gefeliciteerd! U hebt zojuist geleerd hoe u een PDF-document kunt ondertekenen met een smartcard en een handtekeningveld met Aspose.PDF voor .NET. Dit proces beveiligt niet alleen uw documenten, maar garandeert ook de authenticiteit ervan, waardoor het een essentiële vaardigheid is in het huidige digitale landschap. Of u nu contracten, facturen of andere belangrijke documenten ondertekent, weten hoe u digitale handtekeningen kunt implementeren, kan u tijd besparen en gemoedsrust geven.

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een krachtige bibliotheek waarmee ontwikkelaars PDF-documenten in .NET-toepassingen kunnen maken, bewerken en converteren.

### Heb ik een smartcard nodig om PDF's te ondertekenen?
Ja, voor het veilig ondertekenen van PDF's met een digitaal certificaat is een smartcard vereist.

### Kan ik Aspose.PDF gratis gebruiken?
Aspose.PDF biedt een gratis proefversie aan, die u kunt downloaden [hier](https://releases.aspose.com/).

### Hoe kan ik een ondertekend PDF-bestand verifiëren?
Je kunt de `PdfFileSignature` klasse in Aspose.PDF om de handtekeningen in uw PDF-document te verifiëren.

### Waar kan ik meer documentatie over Aspose.PDF vinden?
Je kunt de [Aspose.PDF-documentatie](https://reference.aspose.com/pdf/net/) voor meer details en voorbeelden.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}