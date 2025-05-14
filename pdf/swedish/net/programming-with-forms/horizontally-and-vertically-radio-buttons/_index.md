---
"description": "Lär dig hur du skapar horisontellt och vertikalt justerade radioknappar i PDF med Aspose.PDF för .NET med den här steg-för-steg-handledningen."
"linktitle": "Horisontellt och vertikalt radioknappar"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Horisontellt och vertikalt radioknappar"
"url": "/sv/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Horisontellt och vertikalt radioknappar

## Introduktion

Att skapa interaktiva PDF-formulär kan avsevärt förbättra användarupplevelsen, särskilt när det gäller att samla in information. Ett av de vanligaste formulärelementen är radioknappen, som låter användare välja ett alternativ från en uppsättning. I den här handledningen kommer vi att utforska hur man skapar horisontellt och vertikalt justerade radioknappar med Aspose.PDF för .NET. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer den här guiden att guida dig genom processen steg för steg, så att du har en tydlig förståelse för varje del.

## Förkunskapskrav

Innan du dyker ner i koden finns det några förutsättningar du bör ha på plats:

1. Aspose.PDF för .NET: Se till att du har Aspose.PDF-biblioteket installerat. Du kan ladda ner det från [plats](https://releases.aspose.com/pdf/net/).
2. Visual Studio: En utvecklingsmiljö där du kan skriva och testa din kod.
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.

## Importera paket

För att komma igång behöver du importera de nödvändiga paketen i ditt C#-projekt. Så här gör du:

### Skapa ett nytt projekt

Öppna Visual Studio och skapa ett nytt C#-projekt. Du kan välja en konsolapplikation för enkelhetens skull.

### Lägg till Aspose.PDF-referens

1. Högerklicka på ditt projekt i lösningsutforskaren.
2. Välj "Hantera NuGet-paket".
3. Sök efter "Aspose.PDF" och installera den senaste versionen.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

Nu när du har allt konfigurerat, låt oss bryta ner koden för att skapa horisontellt och vertikalt justerade radioknappar.

## Steg 1: Konfigurera dokumentkatalogen

I det här steget definierar vi sökvägen till katalogen där dina PDF-dokument ska lagras.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersätta `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen dit du vill spara din PDF-fil. Detta är avgörande eftersom det talar om för programmet var det ska leta efter indatafiler och var det ska spara utdata.

## Steg 2: Ladda det befintliga PDF-dokumentet

Nästa steg är att ladda PDF-dokumentet som vi ska arbeta med. Detta görs med hjälp av `FormEditor` klass.

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

Här skapar vi en instans av `FormEditor` och binda den till en befintlig PDF-fil med namnet `input.pdf`Se till att den här filen finns i den angivna katalogen.

## Steg 3: Konfigurera egenskaper för radioknappar

Nu ska vi ange några egenskaper för våra radioknappar. Detta inkluderar avståndet mellan knapparna, deras orientering och deras storlek.

```csharp
formEditor.RadioGap = 4; // Avstånd mellan alternativknappar
formEditor.RadioHoriz = true; // Ställ in på sant för horisontell justering
formEditor.RadioButtonItemSize = 20; // Storleken på radioknappen
formEditor.Facade.BorderWidth = 1; // Kantbredd
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // Kantfärg
```

Dessa egenskaper hjälper till att definiera hur radioknapparna ska visas i PDF-filen. `RadioGap` egenskapen styr avståndet mellan knapparna, medan `RadioHoriz` bestämmer deras layout.

## Steg 4: Lägg till horisontella radioknappar

Nu ska vi lägga till de horisontella radioknapparna i PDF-filen.

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

I den här koden definierar vi objekten för radioknapparna och lägger till dem i PDF-filen. `AddField` Metoden tar flera parametrar, inklusive fälttyp, fältnamn och koordinater för placering.

## Steg 5: Lägg till vertikala radioknappar

Nästa steg är att lägga till de vertikala radioknapparna. För att göra detta måste vi ändra orienteringen tillbaka till vertikal.

```csharp
formEditor.RadioHoriz = false; // Ställ in på falskt för vertikal justering
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

Precis som tidigare definierar vi objekten och lägger till dem i PDF-filen, men den här gången kommer de att justeras vertikalt.

## Steg 6: Spara PDF-dokumentet

Slutligen måste vi spara det modifierade PDF-dokumentet.

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

Den här koden sparar PDF-filen med de nyligen tillagda alternativknapparna. Se till att kontrollera den angivna katalogen för utdatafilen.

## Slutsats

Att skapa radioknappar i en PDF med Aspose.PDF för .NET är en enkel process. Genom att följa stegen som beskrivs i den här handledningen kan du enkelt lägga till både horisontellt och vertikalt justerade radioknappar i dina PDF-formulär. Detta förbättrar inte bara interaktiviteten i dina dokument utan förbättrar också den övergripande användarupplevelsen. Så prova!

## Vanliga frågor

### Vad är Aspose.PDF för .NET?
Aspose.PDF för .NET är ett kraftfullt bibliotek som låter utvecklare skapa, manipulera och konvertera PDF-dokument programmatiskt.

### Kan jag använda Aspose.PDF gratis?
Ja, Aspose erbjuder en gratis testversion som du kan använda för att utvärdera biblioteket. Du kan ladda ner den. [här](https://releases.aspose.com/).

### Hur får jag support för Aspose.PDF?
Du kan få stöd genom att besöka [Aspose-forumet](https://forum.aspose.com/c/pdf/10).

### Är det möjligt att skapa andra formulärelement med Aspose.PDF?
Absolut! Aspose.PDF stöder olika formulärelement, inklusive textfält, kryssrutor och rullgardinsmenyer.

### Var kan jag köpa Aspose.PDF för .NET?
Du kan köpa Aspose.PDF för .NET från [köpsida](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}