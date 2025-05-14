---
"description": "Lär dig hur du ställer in linjebredden för bläckanteckningar i en PDF med Aspose.PDF för .NET. Den här detaljerade handledningen guidar dig genom varje steg och säkerställer högkvalitativa resultat."
"linktitle": "lnk Annotationslinjebredd"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "lnk Annotationslinjebredd"
"url": "/sv/net/annotations/lnkannotationlinewidth/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# lnk Annotationslinjebredd

## Introduktion

När du arbetar med PDF-dokument kan det vara ett kraftfullt sätt att markera information eller lägga till interaktiva element i dina filer genom att lägga till anteckningar. En sådan anteckning är bläckanteckningar, som låter dig rita fritt formade linjer i din PDF. Men tänk om du behöver anpassa utseendet på dessa linjer, särskilt linjebredden? I den här handledningen guidar vi dig genom processen att ställa in linjebredden för bläckanteckningar med Aspose.PDF för .NET.

## Förkunskapskrav

Innan vi går in i koden, låt oss se till att du har allt konfigurerat för att följa den här handledningen smidigt:

1. Aspose.PDF för .NET: Se till att du har biblioteket Aspose.PDF för .NET installerat. Du kan ladda ner det från [nedladdningssida](https://releases.aspose.com/pdf/net/) eller installera den via NuGet Package Manager i Visual Studio.
2. Utvecklingsmiljö: Den här handledningen förutsätter att du arbetar i en .NET-utvecklingsmiljö som Visual Studio.
3. Grundläggande kunskaper i C#: En grundläggande förståelse för C# hjälper dig att följa kodningsstegen.
4. PDF-dokument: Använd antingen ett befintligt PDF-dokument eller skapa ett nytt för den här handledningen.

## Importera nödvändiga namnrymder

Innan du börjar koda, se till att importera nödvändiga namnrymder i ditt projekt:

```csharp
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;
using System.Collections;
using System.Collections.Generic;
```

Dessa namnrymder tillhandahåller de klasser och metoder som behövs för att manipulera PDF-dokument, arbeta med anteckningar och hantera grafiska element.

Nu när vi har våra förutsättningar på plats, låt oss dela upp processen för att ställa in linjebredden för bläckanteckningar i tydliga, hanterbara steg.

## Steg 1: Initiera PDF-dokumentet

Först måste vi skapa eller öppna ett PDF-dokument. I den här handledningen skapar vi ett nytt PDF-dokument från grunden.

```csharp
// Initiera PDF-dokumentet
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Ange din dokumentkatalog
Document doc = new Document();
doc.Pages.Add(); // Lägg till en tom sida i dokumentet
```

Här initierar vi ett nytt `Document` objektet, vilket representerar vår PDF-fil. Vi lägger sedan till en tom sida i dokumentet att arbeta med.

## Steg 2: Skapa bläckannoteringen

Härnäst skapar vi själva bläckanteckningen. Detta innebär att definiera punkterna som utgör bläckstrecken.

```csharp
// Skapa bläckannoteringen
IList<Point[]> inkList = new List<Point[]>();
LineInfo lineInfo = new LineInfo();
lineInfo.VerticeCoordinate = new float[] { 55, 55, 70, 70, 70, 90, 150, 60 };
lineInfo.Visibility = true;
lineInfo.LineColor = Color.Red;
lineInfo.LineWidth = 2;
```

I det här steget definierar vi `LineInfo` objekt, som innehåller koordinaterna för pennstrecken, deras synlighet, färg och initial linjebredd. `VerticeCoordinate` Arrayen innehåller X- och Y-koordinaterna för varje punkt i linjen.

## Steg 3: Konvertera koordinater till punkter

Nu behöver vi konvertera dessa koordinater till punkter som kan användas av bläckannoteringen.

```csharp
// Konvertera koordinater till punkter
int length = lineInfo.VerticeCoordinate.Length / 2;
Aspose.Pdf.Point[] gesture = new Aspose.Pdf.Point[length];
for (int i = 0; i < length; i++)
{
    gesture[i] = new Aspose.Pdf.Point(lineInfo.VerticeCoordinate[2 * i], lineInfo.VerticeCoordinate[2 * i + 1]);
}

inkList.Add(gesture);
```

Denna loop bearbetar koordinatuppsättningen och omvandlar varje koordinatpar till en `Point` objekt, som sedan läggs till i vårt `inkList`.

## Steg 4: Lägg till bläckannoteringen på PDF-sidan

Med punkterna redo kan vi nu skapa bläckanteckningen och lägga till den på PDF-sidan.

```csharp
// Lägg till bläckanteckningen på PDF-sidan
InkAnnotation a1 = new InkAnnotation(doc.Pages[1], new Aspose.Pdf.Rectangle(100, 100, 300, 300), inkList);
a1.Subject = "Test";
a1.Title = "Title";
a1.Color = Aspose.Pdf.Color.FromRgb(Color.Green);
```

det här steget initierar vi en `InkAnnotation` objekt, som anger sidan, en avgränsande rektangel och vår lista med punkter. Vi anger även anteckningens ämne, titel och färg.

## Steg 5: Anpassa annoteringens kantlinje

För att ytterligare anpassa utseendet på vår annotering ändrar vi dess kantegenskaper.

```csharp
// Anpassa annoteringens kantlinje
Border border = new Border(a1);
border.Width = 3;
border.Effect = BorderEffect.Cloudy;
border.Dash = new Dash(1, 1);
border.Style = BorderStyle.Solid;
doc.Pages[1].Annotations.Add(a1);
```

Här skapar vi en `Border` objekt för vår annotering, och ange dess bredd, effekt, streckmönster och stil. Detta steg säkerställer att annoteringen syns tydligt på PDF-sidan.

## Steg 6: Spara PDF-dokumentet

Slutligen, efter att ha gjort alla nödvändiga ändringar, är det dags att spara dokumentet.

```csharp
// Spara PDF-dokumentet
dataDir = dataDir + "lnkAnnotationLineWidth_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nInk annotation line width setup successfully.\nFile saved at " + dataDir);
```

Den här koden sparar det modifierade PDF-dokumentet med bläckanteckningen i den angivna katalogen. `Console.WriteLine` kommandot bekräftar att koden har körts korrekt.

## Slutsats

Grattis! Du har skapat och anpassat en bläckanteckning i ett PDF-dokument med Aspose.PDF för .NET. Den här handledningen täckte hela processen, från att initiera dokumentet till att spara den slutliga filen. Med denna kunskap kan du utforska de stora möjligheterna hos Aspose.PDF för .NET ytterligare och tillämpa liknande tekniker på andra typer av anteckningar eller PDF-manipulationer.

## Vanliga frågor

### Kan jag använda olika färger för olika delar av bläckanteckningen?  
Ja, du kan skapa flera `InkAnnotation` objekt med olika färger och lägg till dem på samma eller olika sidor i din PDF.

### Hur ändrar jag linjebredden dynamiskt?  
Du kan justera `LineWidth` egendomen tillhörande `LineInfo` objektet innan koordinaterna konverteras till punkter.

### Är det möjligt att göra bläckannoteringen transparent?  
Ja, du kan ändra `Opacity` egendomen tillhörande `InkAnnotation` objekt för att göra det transparent.

### Kan jag lägga till flera bläckanteckningar på samma sida?  
Absolut! Du kan lägga till så många bläckanteckningar du vill på en enda sida genom att upprepa processen.

### Hur tar jag bort en bläckanteckning från en PDF?  
Du kan ta bort en anteckning med hjälp av `doc.Pages[1].Annotations.Delete(a1)` metod, där `a1` är ditt annoteringsobjekt.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}