---
"description": "Lär dig hur du digitalt signerar en PDF med en tidsstämpel med Aspose.PDF för .NET. Den här steg-för-steg-guiden täcker förutsättningar, certifikatkonfiguration, tidsstämpling och mer."
"linktitle": "Digital signering med tidsstämpel i PDF-fil"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Digital signering med tidsstämpel i PDF-fil"
"url": "/sv/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Digital signering med tidsstämpel i PDF-fil

## Introduktion

Har du någonsin behövt signera en PDF digitalt och inkludera en tidsstämpel för extra säkerhet? Oavsett om du arbetar med juridiska dokument, kontrakt eller något som kräver säker autentisering, ger en digital signatur med en tidsstämpel ett extra lager av trovärdighet. I den här handledningen går vi igenom hur du kan använda Aspose.PDF för .NET för att lägga till en digital signatur tillsammans med en tidsstämpel i dina PDF-dokument. Oroa dig inte, vi tar det steg för steg!

## Förkunskapskrav

Innan vi går in i koden finns det några saker du behöver ställa in för att kunna följa med. Här är en snabb checklista över förutsättningarna för att komma igång:

- Aspose.PDF för .NET-bibliotek: Du behöver Aspose.PDF för .NET-biblioteket installerat i ditt projekt. Du kan [ladda ner den senaste versionen här](https://releases.aspose.com/pdf/net/) eller lägg till den i ditt projekt via NuGet.
- Ett PDF-dokument: Du behöver en exempel-PDF-fil att arbeta med. Se till att du har en fil i projektets katalog som du vill signera.
- Digitalt certifikat (PFX-fil): Se till att du har ett digitalt certifikat (ett `.pfx` fil) för att signera dokumentet digitalt.
- Tidsstämplings-URL: Detta är en tidsstämplingstjänst online som används för att bifoga en tidsstämpel till den digitala signaturen. 
- Grundläggande C#-kunskaper: Du behöver inte vara expert, men att känna till grunderna i C# hjälper dig att förstå och anpassa koden.

När du har kryssat i alla dessa rutor är du redo att börja koda!

## Importera paket

För att komma igång måste du importera följande namnrymder till ditt C#-projekt. Detta säkerställer att du har tillgång till relevanta Aspose.PDF-klasser och funktioner.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## Steg 1: Ladda PDF-dokumentet

Det första vi behöver göra är att ladda PDF-dokumentet som vi vill signera. Så här gör du:

```csharp
// Definiera sökvägen till din dokumentkatalog
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// Ladda PDF-dokumentet
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

Det här steget är ganska enkelt. Vi definierar helt enkelt sökvägen till dokumentet vi vill signera. `Document` klassen från Aspose.PDF hanterar laddningen av filen.

## Steg 2: Konfigurera den digitala signaturen

Härnäst skapar vi den digitala signaturen med hjälp av PKCS7-klassen och laddar PFX-filen. Denna PFX-fil innehåller ditt certifikat och din privata nyckel, vilka är nödvändiga för att signera dokumentet.

```csharp
// Sökväg till din .pfx-fil
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// Initiera signaturobjektet
PdfFileSignature signature = new PdfFileSignature(document);

// Ladda PFX-filen med ett lösenord
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

Vid det här laget ber du Aspose att använda ditt digitala certifikat för att signera dokumentet. `PKCS7` object hanterar allt kryptografiskt arbete åt dig, så du behöver inte oroa dig för de allra minsta detaljerna.

## Steg 3: Lägg till tidsstämpelinställningarna

En av nyckelkomponenterna i en robust digital signatur är tidsstämpeln. Detta säkerställer att dokumentets signatur kan verifieras även efter att certifikatet har löpt ut. Låt oss ställa in tidsstämpeln med hjälp av en tidsstämpelinstans online.

```csharp
// Definiera tidsstämpelinställningar
TimestampSettings timestampSettings = new TimestampSettings("https://"din_tidsstämpel_url", "användare:lösenord");

// Lägg till tidsstämpelinställningar till PKCS7-objektet
pkcs.TimestampSettings = timestampSettings;
```

Här anger du URL:en för tidsstämplingstjänsten, som automatiskt anger tid och datum för din signatur. Detta kan göras med eller utan autentisering.

## Steg 4: Definiera signaturens placering och utseende

Nu ska vi definiera var signaturen ska visas i PDF-filen och dess dimensioner. Du kan anpassa signaturrutans position på sidan, såväl som storleken.

```csharp
// Definiera signaturens utseende och placering (sida 1, med angiven rektangel)
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

Här definierar vi en rektangel som placerar signaturen vid koordinaterna (100, 100) på PDF-filens första sida, med en bredd på 200 och en höjd på 100. Du kan ändra dessa värden så att de passar din design.

## Steg 5: Signera PDF-dokumentet

När allt är klart är det dags att faktiskt tillämpa den digitala signaturen på PDF-filen. Det här steget kombinerar certifikatet, tidsstämpeln och positioneringen i ett enkelt kommando.

```csharp
// Signera dokumentet på första sidan
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

Här är vad som händer:
- 1: Detta indikerar att signaturen ska appliceras på första sidan.
- "Orsak till underskrift": Här kan du ange varför du signerar dokumentet.
- "Kontakt": Ange kontaktuppgifter till undertecknaren.
- "Plats": Ange signerarens plats.
- sant: Detta booleska värde anger om signaturen är synlig i dokumentet.
- rekt: Rektangeln vi definierade tidigare anger signaturens storlek och position.
- pkcs: PKCS7-objektet innehåller inställningarna för digitalt certifikat och tidsstämpel.

## Steg 6: Spara den signerade PDF-filen

När dokumentet är signerat är allt som återstår att göra att spara det. Du kan välja ett nytt filnamn för att behålla både originalversionen och den signerade versionen.

```csharp
// Spara det signerade PDF-dokumentet
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

Din nyligen signerade och tidsstämplade PDF har nu sparats i den angivna katalogen!

## Slutsats

Och där har du det! Du har framgångsrikt signerat en PDF digitalt med en tidsstämpel med Aspose.PDF för .NET. Denna process säkerställer dina dokuments äkthet och integritet, vilket ger både dig och mottagaren sinnesro. Digitala signaturer blir allt viktigare i dagens digitala värld, så att behärska denna process är definitivt en färdighet värd att ha.

## Vanliga frågor

### Kan jag använda ett annat filformat för certifikatet?  
Ja, men handledningen fokuserar på att använda en PFX-fil, vilket är det vanligaste formatet för digitala certifikat.

### Behöver jag en internetanslutning för att tillämpa tidsstämpeln?  
Ja, eftersom tidsstämpeln hämtas från en online-tidsstämplingsinstans behöver du internetåtkomst.

### Kan jag signera flera sidor i en PDF?  
Absolut! Du kan ändra `signature.Sign()` metod för att rikta in sig på flera sidor eller loopa igenom alla sidor.

### Vad händer om lösenordet till PFX-filen är felaktigt?  
Du får ett undantag om lösenordet är fel, så se till att det är korrekt angett.

### Kan jag göra signaturen osynlig?  
Ja, du kan passera `false` till `Sign` metodens visibility-parameter för att göra signaturen osynlig.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}