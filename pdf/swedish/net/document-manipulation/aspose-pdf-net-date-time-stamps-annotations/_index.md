---
"date": "2025-04-11"
"description": "Lär dig hur du effektivt lägger till datum- och tidsstämplar eller anteckningar i dina PDF-dokument med Aspose.PDF för .NET. Förbättra dokumenthanteringen med dessa enkla steg."
"title": "Lägg till datum- och tidsstämplar till PDF-filer med Aspose.PDF för .NET"
"url": "/sv/net/document-manipulation/aspose-pdf-net-date-time-stamps-annotations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Lägg till datum- och tidsstämplar till PDF-filer med Aspose.PDF för .NET

## Introduktion

I dagens digitala tidsålder är effektiv dokumenthantering avgörande för företag och privatpersoner. Att lägga till datum- och tidsstämplar eller anteckningar i dina PDF-filer kan förbättra dataintegriteten och organisationen. Den här handledningen visar hur man integrerar dessa funktioner med Aspose.PDF för .NET.

**Viktiga slutsatser:**
- Lägg till aktuellt datum och tid som textstämplar på en angiven PDF-sida.
- Skapa fritextanteckningar på önskade platser i dokumentet.
- Följ bästa praxis för optimal prestanda med Aspose.PDF för .NET.

## Förkunskapskrav
Innan du börjar, se till att du har:

### Nödvändiga bibliotek och versioner
- **Aspose.PDF för .NET**Ett robust bibliotek för PDF-hantering utan Adobe Acrobat. Använd version 21.x eller senare.

### Krav för miljöinstallation
- Utvecklingsmiljö med .NET Framework 4.5+ eller .NET Core 2.0+
- Visual Studio eller annan IDE som stöder C#-programmering

### Kunskapsförkunskaper
- Grundläggande förståelse för C# och .NET projektstrukturer
- Vana vid hantering av filer i en katalogstruktur

## Konfigurera Aspose.PDF för .NET
Installera Aspose.PDF med någon av följande metoder:

**Använda .NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**Använda pakethanteraren:**
```powershell
Install-Package Aspose.PDF
```

**Via NuGet Package Manager-gränssnittet:**
- Öppna NuGet-pakethanteraren i din IDE.
- Sök efter "Aspose.PDF" och installera den senaste versionen.

### Steg för att förvärva licens
För att fullt ut utnyttja Aspose.PDF:
1. **Gratis provperiod:** Ladda ner en tillfällig licens för att utforska alla funktioner.
2. **Tillfällig licens:** Begär en utökad utvärderingslicens om det behövs.
3. **Köpa:** Köp en licens för långvarig användning från Asposes webbplats.

Initiera din licens i kod:
```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to License File");
```

## Implementeringsguide
Låt oss lägga till datum- och tidsstämplar i PDF-filer.

### Funktion 1: Lägg till datum- och tidsstämpel till PDF
Den här funktionen lägger till aktuellt datum och tid som en textstämpel på den första sidan i ett angivet PDF-dokument.

#### Steg-för-steg-implementering

##### 1. Öppna befintligt PDF-dokument
Ladda ditt måldokument:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/AddTextStamp.pdf");
```

##### 2. Hämta aktuellt datum och tid som sträng
Formatera aktuellt datum och tid:
```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

##### 3. Skapa textstämpel med aktuellt datum och tid
Skapa en `TextStamp` exempel med den formaterade strängen:
```csharp
TextStamp textStamp = new TextStamp(annotationText);
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

##### 4. Lägg till textstämpel på första sidan
Lägg till stämpeln på första sidan av ditt dokument:
```csharp
document.Pages[1].AddStamp(textStamp);
```

##### 5. Skapa och lägg till fritextannotering (valfritt)
För mer komplexa anteckningar, skapa en `FreeTextAnnotation`:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(document.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance)
{
    Name = "Stamp",
    Contents = textStamp.Value
};
textAnnotation.Border = new Border(textAnnotation) { Width = 0 };
document.Pages[1].Annotations.Add(textAnnotation);
```

##### 6. Spara det ändrade dokumentet
Spara dina ändringar:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/AddDateTimeStamp_out.pdf";
document.Save(outputDir);
```

### Funktion 2: Lägg till fritextannotering i PDF
Lägg till fritextanteckningar på valfri plats i ett PDF-dokument.

#### Steg-för-steg-implementering

##### 1. Öppna ett befintligt PDF-dokument
Ladda ditt måldokument:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/Sample.pdf");
```

##### 2. Definiera rektangelområdet för annotering
Ange var anteckningen ska placeras på sidan:
```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(100, 400, 200, 450);
```

##### 3. Skapa en fritextannotering med angivet utseende och plats
Initiera din anteckning med önskade text- och utseendeinställningar:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 12, System.Drawing.Color.Blue);
FreeTextAnnotation freeTextAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], rect, default_appearance)
{
    Contents = "This is a sample annotation",
    Title = "Sample Annotation"
};
```

##### 4. Ställ in kantstil och lägg till annoteringen
Se till att kantstilen matchar dina behov (osynlig i det här fallet):
```csharp
freeTextAnnotation.Border = new Border(freeTextAnnotation) { Width = 0 };
pdfDocument.Pages[1].Annotations.Add(freeTextAnnotation);
```

##### 5. Spara det ändrade dokumentet
Spara ditt dokument med den nyligen tillagda anteckningen:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/FreeTextAnnotation_out.pdf";
document.Save(outputDir);
```

## Praktiska tillämpningar
Att lägga till datumstämplar och anteckningar i PDF-filer är användbart inom olika branscher:
- **Juridiska dokument**Säkerställer efterlevnad genom att tidsstämpla ändringar.
- **Akademiska artiklar**Underlättar gemensam redigering med anteckningar.
- **Finansiella register**Upprätthåller noggranna revisionsloggar med tidsstämplade rapporter.
- **Teknisk dokumentation**: Markerar uppdateringar eller viktiga anteckningar i manualer.

## Prestandaöverväganden
För optimal prestanda när du använder Aspose.PDF för .NET:
- **Batchbearbetning**Bearbeta flera PDF-filer i omgångar för att minska omkostnader.
- **Minneshantering**Användning `Dispose` metoder för att frigöra minnesresurser efter bearbetning av varje dokument.
- **Optimerade teckensnitt och bilder**Begränsa teckensnitt och bildupplösningar för att minska filstorleken.

## Slutsats
Genom att integrera Aspose.PDF för .NET kan du lägga till datumstämpling och anteckningsfunktioner i PDF-dokument, vilket förbättrar funktionaliteten. Dessa verktyg förbättrar dataintegriteten och effektiviserar dokumenthanteringen.

Experimentera med olika konfigurationer och utforska ytterligare funktioner som Aspose.PDF erbjuder för att möta dina specifika behov.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}