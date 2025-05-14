---
"description": "Lär dig hur du skapar grupperade kryssrutor (radioknappar) i ett PDF-dokument med Aspose.PDF för .NET med den här steg-för-steg-handledningen."
"linktitle": "Grupperade kryssrutor i PDF-dokument"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Grupperade kryssrutor i PDF-dokument"
"url": "/sv/net/programming-with-forms/grouped-check-boxes/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Grupperade kryssrutor i PDF-dokument

## Introduktion

Att skapa interaktiva PDF-filer är inte så svårt som det kanske låter, särskilt när du har kraftfulla verktyg som Aspose.PDF för .NET till ditt förfogande. Ett av de interaktiva elementen du kan behöva lägga till i dina PDF-dokument är grupperade kryssrutor, eller mer specifikt, radioknappar som låter användare välja ett alternativ från en uppsättning. Den här handledningen guidar dig genom processen att lägga till grupperade kryssrutor (radioknappar) i ett PDF-dokument med Aspose.PDF för .NET. Oavsett om du är nybörjare eller en erfaren utvecklare kommer du att tycka att den här guiden är engagerande, detaljerad och lätt att följa.

## Förkunskapskrav

Innan vi går in på steg-för-steg-guiden, låt oss gå igenom några viktiga förutsättningar:

1. Aspose.PDF för .NET: Se till att du har Aspose.PDF-biblioteket installerat. Om inte kan du [ladda ner den här](https://releases.aspose.com/pdf/net/).
2. IDE: Du bör ha en utvecklingsmiljö konfigurerad, till exempel Visual Studio.
3. .NET Framework: Projektet bör rikta in sig på en version av .NET Framework som är kompatibel med Aspose.PDF.
4. Grundläggande C#-kunskaper: För att kunna följa processen smidigt krävs det att du har goda kunskaper i C# och PDF-hantering.
5. Licens: Aspose.PDF kräver en licens för full funktionalitet. Du kan [få en tillfällig licens](https://purchase.aspose.com/temporary-license/) om det behövs.

## Importera paket

Innan du börjar, se till att du har importerat nödvändiga namnrymder till ditt projekt:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

Dessa paket ger dig tillgång till alla klasser och metoder som krävs för att manipulera PDF-dokument, inklusive att skapa radioknappar och definiera deras egenskaper.

I det här avsnittet kommer vi att dela upp processen för att skapa grupperade kryssrutor (radioknappar) i tydliga och lättförståeliga steg.

## Steg 1: Skapa ett nytt PDF-dokument

Det första steget är att skapa en instans av `Document` objektet, vilket kommer att representera din PDF-fil. Lägg sedan till en tom sida i ditt dokument där du kommer att placera dina grupperade kryssrutor.

```csharp
// Instansiera dokumentobjekt
Document pdfDocument = new Document();

// Lägg till en sida i PDF-filen
Page page = pdfDocument.Pages.Add();
```

Detta lägger grunden för att lägga till element, till exempel radioknappar, i PDF-filen.

## Steg 2: Initiera radioknappsfältet

Nästa steg är att skapa en `RadioButtonField` objekt, som kommer att innehålla de grupperade kryssrutorna (radioknappar). Detta fält läggs till på den specifika sidan där kryssrutorna kommer att visas.

```csharp
// Instansiera RadioButtonField-objektet och tilldela det till den första sidan
RadioButtonField radio = new RadioButtonField(pdfDocument.Pages[1]);
```

Tänk på detta som behållaren som grupperar de enskilda alternativen för radioknappar.

## Steg 3: Lägg till alternativ för radioknappar

Nu lägger vi till de individuella alternativen för radioknappar i fältet. I det här exemplet lägger vi till två radioknappar och anger deras positioner med hjälp av `Rectangle` objekt.

```csharp
// Lägg till det första alternativet för radioknapp och ange dess position med hjälp av rektangeln
RadioButtonOptionField opt1 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(0, 0, 20, 20));
RadioButtonOptionField opt2 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(100, 0, 120, 20));

// Ange alternativnamn för identifiering
opt1.OptionName = "Option1";
opt2.OptionName = "Option2";
```

Här, den `Rectangle` objektet definierar koordinaterna och storleken för varje radioknapp på sidan.

## Steg 4: Anpassa stilen på radioknapparna

Du kan anpassa utseendet på radioknapparna genom att ställa in deras `Style` egenskap. Du kanske till exempel vill ha fyrkantiga kryssrutor eller korsformade.

```csharp
// Ställ in stilen på radioknapparna
opt1.Style = BoxStyle.Square;
opt2.Style = BoxStyle.Cross;
```

Detta gör att du kan kontrollera utseendet och känslan av kryssrutorna, vilket gör dem mer användarvänliga och visuellt tilltalande.

## Steg 5: Konfigurera kantegenskaper

Kantlinjer spelar en viktig roll för att göra kryssrutorna lätt identifierbara. Här lägger vi till heldragna kanter runt varje alternativknapp och definierar deras bredd och färg.

```csharp
// Konfigurera kanten för den första alternativknappen
opt1.Border = new Border(opt1);
opt1.Border.Style = BorderStyle.Solid;
opt1.Border.Width = 1;
opt1.Characteristics.Border = Color.Black;

// Konfigurera kanten för den andra alternativknappen
opt2.Border = new Border(opt2);
opt2.Border.Style = BorderStyle.Solid;
opt2.Border.Width = 1;
opt2.Characteristics.Border = Color.Black;
```

Det här steget säkerställer att varje alternativknapp har en väldefinierad kantlinje, vilket förbättrar dokumentets läsbarhet.

## Steg 6: Lägg till alternativ för radioknappar i formuläret

Nu lägger vi till radioknapparna i dokumentets formulär. Detta är det sista steget i att gruppera kryssrutorna under ett enda fält.

```csharp
// Lägg till radioknappsfält till dokumentets formulärobjekt
pdfDocument.Form.Add(radio);
```

Formulärobjektet fungerar som en behållare för alla interaktiva element, inklusive våra grupperade kryssrutor.

## Steg 7: Spara PDF-dokumentet

Slutligen, när allt är konfigurerat, kan du spara PDF-dokumentet på önskad plats.

```csharp
// Definiera sökvägen till utdatafilen
string dataDir = "YOUR DOCUMENT DIRECTORY" + "GroupedCheckBoxes_out.pdf";

// Spara PDF-dokumentet
pdfDocument.Save(dataDir);

// Bekräfta att skapandet lyckades
Console.WriteLine("Grouped checkboxes added successfully. File saved at " + dataDir);
```

Och det var allt! Du har skapat en PDF med grupperade kryssrutor med hjälp av Aspose.PDF för .NET.

## Slutsats

Att lägga till interaktiva element som grupperade kryssrutor i PDF-dokument kan verka knepigt till en början, men med Aspose.PDF för .NET blir det en barnlek. Genom att följa den här steg-för-steg-guiden har du lärt dig hur du konfigurerar ett enkelt PDF-dokument, lägger till grupperade radioknappar, anpassar deras utseende och sparar slutresultatet. Oavsett om du skapar formulär, undersökningar eller någon annan typ av interaktiv PDF, ger den här guiden dig en solid grund att börja med.

## Vanliga frågor

### Kan jag lägga till fler än två radioknappar i en grupp?
Absolut! Instansiera bara ytterligare `RadioButtonOptionField` objekt och lägg till dem i `RadioButtonField` som visas i handledningen.

### Hur hanterar jag flera grupper av kryssrutor i ett dokument?
För att skapa flera grupper, instansiera separata `RadioButtonField` objekt för varje grupp.

### Finns det en gräns för antalet kryssrutor jag kan lägga till?
Nej, Aspose.PDF för .NET har inga begränsningar för antalet kryssrutor du kan lägga till i en PDF.

### Kan jag ändra utseendet på kryssrutor efter att de har lagts till?
Ja, du kan ändra egenskaper som kantlinjestil, bredd och färg efter att kryssrutorna har lagts till.

### Är det möjligt att använda bilder som radioknappar?
Ja, Aspose.PDF låter dig använda anpassade bilder som radioknappar genom att ställa in `Appearance` egenskapen för varje alternativ för radioknapp.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}