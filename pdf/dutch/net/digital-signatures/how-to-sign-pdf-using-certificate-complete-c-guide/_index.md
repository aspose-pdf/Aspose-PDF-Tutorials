---
category: general
date: 2026-06-05
description: Leer hoe je een PDF ondertekent met een certificaat en een digitale handtekening
  toevoegt aan een PDF met een aangepaste PKCS#7‑ondertekenaar in C#. Stapsgewijze
  code en tips.
draft: false
keywords:
- how to sign pdf using certificate
- add digital signature to pdf
language: nl
og_description: Hoe PDF te ondertekenen met een certificaat, uitgelegd in de eerste
  zin. Volg deze gids om een digitale handtekening aan PDF toe te voegen met een aangepaste
  PKCS#7-ondertekenaar.
og_title: Hoe PDF ondertekenen met certificaat – volledige C#-tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Learn how to sign PDF using certificate and add digital signature to
    PDF with a custom PKCS#7 signer in C#. Step‑by‑step code and tips.
  headline: How to Sign PDF Using Certificate – Complete C# Guide
  type: TechArticle
- description: Learn how to sign PDF using certificate and add digital signature to
    PDF with a custom PKCS#7 signer in C#. Step‑by‑step code and tips.
  name: How to Sign PDF Using Certificate – Complete C# Guide
  steps:
  - name: What if I need to sign multiple pages?
    text: Just loop over the desired page numbers and call `signature.Sign` for each,
      reusing the same `pkcs7Signer`. Some libraries require a fresh `Signature` instance
      per page; check the docs.
  - name: Can I use a SHA‑256 hash instead of the default?
    text: 'Absolutely. Set the hash algorithm in your `CustomSignHash` delegate, e.g.:'
  - name: How do I validate the signature programmatically?
    text: 'Most PDF libraries expose a `Validate` method:'
  type: HowTo
tags:
- pdf
- digital signature
- csharp
title: Hoe PDF te ondertekenen met een certificaat – Complete C#‑gids
url: /nl/net/digital-signatures/how-to-sign-pdf-using-certificate-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PDF te ondertekenen met certificaat – Complete C#‑gids

Heb je je ooit afgevraagd **hoe je pdf ondertekent met certificaat** zonder te worstelen met obscure command‑line tools? Je bent niet de enige. Veel ontwikkelaars moeten een betrouwbare digitale handtekening in een PDF opnemen — denk aan contracten, facturen of compliance‑rapporten — en ze willen een nette, programmeerbare manier om dat te doen.  

In deze tutorial lopen we een praktisch voorbeeld door dat niet alleen laat zien **hoe je pdf ondertekent met certificaat**, maar ook demonstreert hoe je **digitale handtekening aan pdf toevoegt** met een aangepaste PKCS#7 detached signer in C#. Aan het einde heb je een kant‑klaar code‑fragment, uitleg per regel, en een reeks tips om veelvoorkomende valkuilen te vermijden.

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

- .NET 6.0 of later geïnstalleerd (de code werkt ook met .NET Core).
- Een geldig X.509‑certificaat in PFX‑formaat (`certificate.pfx`) plus het wachtwoord.
- De `Signature`‑ en `PKCS7Detached`‑klassen uit de PDF‑ondertekeningsbibliotheek die je gebruikt (het voorbeeld gaat uit van een bibliotheek die de getoonde API volgt).
- Een IDE naar keuze — Visual Studio, Rider of VS Code volstaat.

Er zijn geen extra NuGet‑pakketten nodig buiten de ondertekeningsbibliotheek zelf.

## Overzicht van het proces

Op een hoog niveau ziet de workflow er zo uit:

1. Laad het certificaatbestand en wachtwoord.  
2. Maak een **PKCS#7 detached signer** en koppel een aangepaste hash‑ondertekenings‑delegate.  
3. Open de PDF die je wilt beveiligen.  
4. Definieer waar de handtekeningweergave op een pagina moet komen.  
5. Pas de handtekening toe met de signer uit stap 2.  
6. Sla de nieuw ondertekende PDF op.

Klinkt simpel, toch? Laten we elke stap afzonderlijk bekijken.

---

## Hoe PDF te ondertekenen met certificaat – Stap 1: Het certificaat laden

Eerst moeten we de signer vertellen waar ons certificaat zich bevindt en hoe het te ontgrendelen.

```csharp
// Step 1: Specify the certificate file and its password
string certificatePath = "YOUR_DIRECTORY/certificate.pfx";
string certificatePassword = "yourPassword";
```

**Waarom dit belangrijk is:** Het certificaat bevat de publieke sleutel die in de PDF verschijnt en de private sleutel die wordt gebruikt om de cryptografische hash te maken. Als het wachtwoord onjuist is, zal de ondertekeningsoperatie een authenticatiefout geven — controleer het dus dubbel.

> **Pro tip:** Bewaar het wachtwoord in een veilige kluis (Azure Key Vault, AWS Secrets Manager) in plaats van het hard‑coded in de code te zetten. Het fragment gebruikt een letterlijke alleen ter illustratie.

---

## Stap 2: Een PKCS#7 Detached Signer maken met een aangepaste hash‑delegate

Nu instantieren we het signer‑object. De bibliotheek laat je je eigen hash‑ondertekeningsroutine injecteren via `CustomSignHash`. Handig wanneer je hardware‑security‑modules (HSM) of externe services nodig hebt.

```csharp
// Step 2: Create a PKCS#7 detached signer with a custom hash‑signing delegate
var pkcs7Signer = new PKCS7Detached(certificatePath, certificatePassword)
{
    // Use your own implementation to sign the hash
    CustomSignHash = (hash, alg) => MySigner.Sign(hash)
};
```

**Uitleg:**  
- `PKCS7Detached` bouwt een PKCS#7‑container die de handtekening apart van het document houdt (detached).  
- `CustomSignHash` ontvangt de vooraf berekende hash (`hash`) en de algoritme‑identifier (`alg`). Je `MySigner.Sign`‑methode kan een HSM aanroepen, een webservice, of simpelweg `RSA.SignData` gebruiken als je in‑process blijft.

> **Edge case:** Als je geen aangepaste delegate opgeeft, kan de bibliotheek terugvallen op een standaard software‑signer, wat minder veilig kan zijn voor productie.

---

## Stap 3: Het PDF‑document laden dat ondertekend moet worden

Met de signer klaar, laden we de doel‑PDF in het geheugen.

```csharp
// Step 3: Load the PDF document to be signed
var signature = new Signature("YOUR_DIRECTORY/input.pdf");
```

De `Signature`‑klasse is het toegangspunt voor alle ondertekeningsoperaties. Hij laadt de PDF, parseert bestaande objecten en bereidt een mutabele structuur voor.

> **Wat als het bestand met een wachtwoord is beveiligd?** Sommige bibliotheken laten je het PDF‑wachtwoord als extra argument doorgeven. Bekijk de API‑documentatie en pas het aan indien nodig.

---

## Stap 4: De handtekeningweergave definiëren (pagina & rechthoek)

Een digitale handtekening is niet alleen een cryptografische blob; hij heeft vaak een visuele representatie op een pagina. We moeten aangeven *waar* die moet verschijnen.

```csharp
// Step 4: Define the page number and the rectangle where the signature will appear
int pageNumber = 1;
var rect = new Rectangle(100, 100, 200, 200); // left, bottom, right, top
```

- `pageNumber` is 1‑gebaseerd, dus `1` verwijst naar de eerste pagina.  
- `Rectangle` gebruikt de PDF‑coördinatenruimte (origine links‑onder). Pas de waarden aan naar jouw lay‑out.

> **Tip:** Als je niet zeker bent van de coördinaten, open de PDF in een viewer die linialen toont (Adobe Acrobat Pro doet dit netjes).

---

## Stap 5: De digitale handtekening toepassen op de geselecteerde pagina

Nu gebeurt de magie — koppel de signer aan de PDF en embed de handtekening.

```csharp
// Step 5: Apply the digital signature to the selected page using the PKCS#7 signer
signature.Sign(pageNumber, true, rect, pkcs7Signer);
```

Parameters uitgelegd:

| Parameter   | Betekenis |
|-------------|-----------|
| `pageNumber`| Doelpagina (1‑gebaseerd). |
| `true`      | Geeft aan dat het een **detached** handtekening is (de hash wordt apart opgeslagen). |
| `rect`      | Visuele rechthoek voor de handtekeningweergave. |
| `pkcs7Signer`| Onze aangepaste PKCS#7‑signer uit Stap 2. |

Als de oproep slaagt, bevat de PDF nu een handtekeningveld dat valideert tegen het opgegeven certificaat.

---

## Stap 6: Het ondertekende PDF‑document opslaan

Tot slot schrijven we de aangepaste PDF terug naar de schijf.

```csharp
// Step 6: Save the signed PDF document
signature.Save("YOUR_DIRECTORY/output.pdf");
```

Je kunt nu `output.pdf` openen in elke PDF‑lezer (Adobe Acrobat, Foxit, enz.) en een groen vinkje of een “Signed and all signatures are valid”‑bericht zien — mits de certificaatketen vertrouwd is op de hostmachine.

> **Verificatietip:** In Acrobat, ga naar *Bestand → Eigenschappen → Beveiliging* om de handtekeningdetails te bekijken.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is een zelfstandig programma dat je in een console‑app kunt plakken.

```csharp
using System;
using YourPdfSigningLibrary; // replace with actual namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Certificate details
        string certificatePath = "YOUR_DIRECTORY/certificate.pfx";
        string certificatePassword = "yourPassword";

        // 2️⃣ PKCS#7 signer with a custom hash delegate
        var pkcs7Signer = new PKCS7Detached(certificatePath, certificatePassword)
        {
            CustomSignHash = (hash, alg) => MySigner.Sign(hash) // implement MySigner
        };

        // 3️⃣ Load PDF
        var signature = new Signature("YOUR_DIRECTORY/input.pdf");

        // 4️⃣ Appearance settings
        int pageNumber = 1;
        var rect = new Rectangle(100, 100, 200, 200);

        // 5️⃣ Sign the PDF
        signature.Sign(pageNumber, true, rect, pkcs7Signer);

        // 6️⃣ Save output
        signature.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("✅ PDF signed successfully! Check output.pdf.");
    }
}
```

**Verwachte output:** Wanneer je het programma uitvoert, print de console de succes‑regel. Het openen van `output.pdf` toont een zichtbaar handtekeningveld en, wanneer je de handtekeningeigenschappen bekijkt, verschijnt het certificaat van de ondertekenaar (`certificate.pfx`) als auteur.

---

## Veelgestelde vragen & valkuilen

### Wat als ik meerdere pagina's moet ondertekenen?
Loop simpelweg over de gewenste paginanummers en roep `signature.Sign` voor elke pagina aan, waarbij je dezelfde `pkcs7Signer` hergebruikt. Sommige bibliotheken vereisen een verse `Signature`‑instantie per pagina; controleer de docs.

### Kan ik een SHA‑256‑hash gebruiken in plaats van de standaard?
Zeker. Stel het hash‑algoritme in je `CustomSignHash`‑delegate in, bijvoorbeeld:

```csharp
CustomSignHash = (hash, alg) => MySigner.Sign(hash, HashAlgorithmName.SHA256);
```

Zorg ervoor dat het sleutelgebruik van het certificaat het gekozen algoritme toestaat.

### Hoe valideer ik de handtekening programmatisch?
De meeste PDF‑bibliotheken bieden een `Validate`‑methode:

```csharp
bool isValid = signature.ValidateSignature(pageNumber);
Console.WriteLine(isValid ? "Signature is valid." : "Signature failed validation.");
```

Als je de intrekkingsstatus moet controleren, integreer OCSP‑ of CRL‑checks — dit valt buiten de scope van deze gids, maar is zeker de moeite waard voor productie‑compliance.

---

## Conclusie

We hebben zojuist **hoe je pdf ondertekent met certificaat** van begin tot eind behandeld, en onderweg geleerd hoe je **digitale handtekening aan pdf toevoegt** met een aangepaste PKCS#7 detached signer in C#. De stappen zijn eenvoudig: laad je certificaat, configureer een signer, open de PDF, definieer de visuele rechthoek, pas de handtekening toe, en sla het bestand op.  

Nu kun je vertrouwde handtekeningen in elke PDF die je genereert embedden — of het nu facturen, juridische contracten of interne rapporten zijn. Wil je verder gaan? Probeer tijdstempel‑authorities (TSA) toe te voegen, een aangepaste handtekeningafbeelding te embedden, of PDF’s in bulk te ondertekenen met parallelle verwerking. De mogelijkheden zijn eindeloos, en je hebt de basis die je nodig hebt.

Vragen of een lastig scenario? Laat een reactie achter, en happy coding! 

![how to sign pdf using certificate](/images/how-to-sign-pdf-using-certificate.png "how to sign pdf using certificate")


## Wat kun je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑features onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe PDF’s digitaal ondertekenen met Aspose.PDF voor .NET: Een uitgebreide gids](/pdf/english/net/security-permissions/digitally-sign-pdf-aspose-pdf-net/)
- [Hoe PDF’s digitaal ondertekenen met tijdstempels met Aspose.PDF .NET | Beveiliging‑ & permissiegids](/pdf/english/net/security-permissions/digitally-sign-pdfs-aspose-pdf-net/)
- [PDF digitaal ondertekenen met aangepaste weergave met Aspose.PDF voor .NET: Een stapsgewijze handleiding](/pdf/english/net/digital-signatures/digitally-sign-pdf-custom-appearance-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}