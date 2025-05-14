---
"description": "Lär dig hur du extraherar digitala signaturer och certifikatinformation från PDF-dokument med Aspose.PDF för .NET. En komplett steg-för-steg-guide för C#-utvecklare."
"linktitle": "Extrahera signaturinformation"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Extrahera signaturinformation"
"url": "/sv/net/programming-with-security-and-signatures/extract-signature-info/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera signaturinformation

## Introduktion

dagens digitala värld är det avgörande att säkerställa dokumentens säkerhet och integritet. En av de vanligaste metoderna för att säkra PDF-filer är att lägga till en digital signatur. Att hämta och verifiera signaturens uppgifter kan dock ibland vara en utmaning, särskilt när du har att göra med olika certifikat. I den här guiden guidar vi dig genom processen att extrahera signaturinformation från PDF-dokument med hjälp av Aspose.PDF för .NET, vilket gör uppgiften till en barnlek. Du lär dig hur du kommer åt signaturfält, extraherar certifikatinformation och sparar den till en fil.

## Förkunskapskrav

Innan vi börjar, låt oss se till att du har allt klart för att komma igång.

- Aspose.PDF för .NET-biblioteket: Om du inte redan har det kan du ladda ner det från [Aspose.PDF för .NET nedladdningssida](https://releases.aspose.com/pdf/net/). 
- .NET-utvecklingsmiljö: Du behöver en IDE som Visual Studio.
- Grundläggande C#-kunskaper: Bekantskap med C# är bra för att förstå kodavsnitten i den här handledningen.
- PDF-dokument med digital signatur: Se till att du har en PDF-fil som innehåller minst en digital signatur i testsyfte.

## Importera obligatoriska namnrymder

Innan du börjar med koden är det viktigt att importera de nödvändiga namnrymderna. Dessa namnrymder ger dig tillgång till Aspose.PDF-funktionen och kan arbeta med PDF-dokument.

```csharp
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
using System;
```

Nu när du har ställt in det viktigaste, låt oss gå vidare till själva processen att extrahera signaturinformation från en PDF.

## Steg 1: Konfigurera dokumentkatalogen

Innan du arbetar med ett PDF-dokument måste du ange platsen för filen du ska använda. Du kan ersätta `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen till katalogen där dina PDF-filer är lagrade.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string input = dataDir + "ExtractSignatureInfo.pdf";
```

Här anger vi katalogen som innehåller PDF-filen och själva filnamnet. Se till att filen finns i den katalogen!

## Steg 2: Ladda PDF-dokumentet

Nu när du har konfigurerat din katalog är nästa steg att ladda PDF-dokumentet med hjälp av `Document` klass från Aspose.PDF.

```csharp
using (Document pdfDocument = new Document(input))
{
    // Bearbeta PDF-filen här.
}
```

Den här kodraden initierar en `Document` objektet som representerar PDF-filen. `using` Uttrycket säkerställer att resurser rensas efter att dokumentet har bearbetats.

## Steg 3: Åtkomst till formulärfält

I det här steget kommer vi att loopa igenom alla formulärfält i PDF-dokumentet. Eftersom signaturer vanligtvis lagras som formulärfält, hjälper det här steget oss att identifiera signaturfälten.

```csharp
foreach (Field field in pdfDocument.Form)
{
    // Identifiera signaturfälten här.
}
```

Genom att iterera igenom `Form` egendomen tillhörande `Document` objekt kan vi undersöka varje formulärfält för att kontrollera om det är ett signaturfält.

## Steg 4: Identifiera signaturfält

När du har öppnat formulärfälten är nästa steg att identifiera vilka som är signaturfält. Vi kan göra detta genom att omvandla varje fält till en `SignatureField` objekt.

```csharp
SignatureField sf = field as SignatureField;
if (sf != null)
{
    // Extrahera signaturinformation.
}
```

Här använder vi `as` nyckelord för att försöka omvandla varje formulärfält till ett `SignatureField`Om rollbesättningen lyckas vet vi att fältet är en signatur.

## Steg 5: Extrahera certifikatet

Nu när du har identifierat signaturfältet är nästa uppgift att extrahera certifikatet från signaturen. Certifikat innehåller viktig information om undertecknaren och signaturens giltighet.

```csharp
Stream cerStream = sf.ExtractCertificate();
```

De `ExtractCertificate` metoden returnerar en `Stream` objekt som innehåller certifikatdata. Denna ström kan användas för att spara certifikatet för vidare analys eller lagring.

## Steg 6: Spara certifikatet till en fil

När du har extraherat certifikatet är det sista steget att spara det till en fil. I det här fallet sparar vi certifikatet som en `.cer` fil.

```csharp
if (cerStream != null)
{
    using (cerStream)
    {
        byte[] bytes = new byte[cerStream.Length];
        using (FileStream fs = new FileStream(dataDir + @"input.cer", FileMode.CreateNew))
        {
            cerStream.Read(bytes, 0, bytes.Length);
            fs.Write(bytes, 0, bytes.Length);
        }
    }
}
```

I det här kodblocket gör vi följande:

1. Kontrollera om certifikatströmmen inte är null.
2. Läs certifikatdatan in i en byte-array.
3. Skriv byte-arrayen till en `.cer` filen i dokumentkatalogen.

## Slutsats

Att extrahera digitala signaturer och deras relaterade certifikatinformation från PDF-dokument med hjälp av Aspose.PDF för .NET är ganska enkelt när det delas upp i enkla steg. Oavsett om du granskar dokument, verifierar signaturer eller bara lagrar certifikat för säker förvaring, ger den här handledningen dig kunskapen för att göra det effektivt. Kom ihåg att det är avgörande att säkra och verifiera dokument i dagens digitala värld, och att använda verktyg som Aspose.PDF för .NET gör det mycket enklare att hantera.

## Vanliga frågor

### Kan jag extrahera flera signaturer från en PDF med hjälp av Aspose.PDF för .NET?
Ja, koden loopar igenom alla formulärfält i dokumentet, vilket gör att du kan extrahera flera signaturer om de finns.

### Vad händer om ingen signatur hittas i PDF-filen?
Om inga signaturfält finns kommer koden helt enkelt att hoppa över dem utan att ge ett felmeddelande.

### Kan jag använda den här metoden för att verifiera giltigheten av en signatur?
Även om du kan extrahera certifikatet kräver verifiering av giltigheten av en signatur ytterligare steg, till exempel kontroll av certifikatets förtroendekedja.

### Är det möjligt att extrahera annan formulärfältsdata med Aspose.PDF för .NET?
Ja, Aspose.PDF låter dig komma åt och manipulera olika typer av formulärfält i en PDF, inte bara signaturfält.

### Hur kan jag se detaljerna i det extraherade certifikatet?
När certifikatet har sparats som en `.cer` filen kan du öppna den med valfri certifikatvisare eller importera den till ett systemcertifikatarkiv för vidare inspektion.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}