---
"description": "Lär dig hur du använder funktionen GetDocumentWindow i Aspose.PDF för .NET för att hämta information om ett PDF-dokuments fönsteregenskaper."
"linktitle": "Hämta dokument-fönstret"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Hämta dokument-fönstret"
"url": "/sv/net/programming-with-document/getdocumentwindow/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hämta dokument-fönstret

# Introduktion

Arbetar du med PDF-filer och vill ha mer kontroll över hur de visas när de öppnas? Oavsett om det handlar om att dölja menyraden eller ändra storlek på fönstret så att det passar den första sidan, ger Aspose.PDF för .NET dig alla verktyg du behöver för att anpassa hur en PDF beter sig när den öppnas i ett visningsprogram. I den här handledningen kommer vi att gå igenom hur man hämtar och manipulerar dokumentfönsterinställningar i Aspose.PDF för .NET.


# Förkunskapskrav

Innan du börjar med handledningen, se till att du har följande förutsättningar på plats:

- Aspose.PDF för .NET installerat i din utvecklingsmiljö.
  - [Ladda ner Aspose.PDF för .NET](https://releases.aspose.com/pdf/net/)
- En giltig licens för Aspose.PDF, eller så kan du skaffa en [gratis provperiod](https://releases.aspose.com/) eller [tillfällig licens](https://purchase.aspose.com/temporary-license/).
- Grundläggande förståelse för .NET och C#.
- Visual Studio eller annan lämplig IDE.

# Importera paket

Innan du börjar skriva någon kod måste du importera de nödvändiga paketen. Öppna ditt projekt och lägg till följande namnrymd högst upp i din C#-fil:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Detta ger dig tillgång till alla klasser och metoder som behövs för att manipulera PDF-dokument med Aspose.PDF för .NET.

Nu ska vi gå igenom processen för att hämta olika dokumentfönsterinställningar. I det här exemplet använder vi en exempel-PDF-fil med namnet `GetDocumentWindow.pdf`.

## Steg 1: Ange sökvägen till dokumentkatalogen

Först och främst måste vi definiera sökvägen till vår PDF-fil. Det är avgörande att du har rätt sökväg för att undvika fel under körningen.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Här, ersätt `"YOUR DOCUMENT DIRECTORY"` med den faktiska katalogen där din PDF-fil finns. Detta är din arbetskatalog varifrån du kommer att ladda PDF-dokumentet.

## Steg 2: Öppna PDF-dokumentet

Nu när filsökvägen är inställd är nästa steg att öppna PDF-dokumentet med Aspose.PDF. Detta laddar dokumentet till minnet, vilket gör att du kan hämta dess egenskaper.

```csharp
Document pdfDocument = new Document(dataDir + "GetDocumentWindow.pdf");
```

Med denna enkla kodrad har du framgångsrikt laddat din PDF-fil till `pdfDocument` objektet, vilket nu ger dig åtkomst till alla dess egenskaper.

## Steg 3: Hämta fönstercentreringsstatus

Nu ska vi kontrollera om dokumentfönstret ska vara centrerat när det öppnas. Standardvärdet för detta är `false`.

```csharp
Console.WriteLine("CenterWindow : {0}", pdfDocument.CenterWindow);
```

Om utdata är `true`, öppnas dokumentets fönster i mitten av skärmen. Annars öppnas det på sin standardposition.

## Steg 4: Kontrollera textriktningen

En annan viktig aspekt av en PDF-fils utseende är textriktningen, som avgör om texten läses från vänster till höger (V2H) eller från höger till vänster (R2V). Du kan hämta denna information med hjälp av följande kod:

```csharp
Console.WriteLine("Direction : {0}", pdfDocument.Direction);
```

Utgången kommer att vara `L2R` för text från vänster till höger och `R2L` för text från höger till vänster. Den här inställningen är särskilt användbar för dokument på språk som arabiska eller hebreiska.

## Steg 5: Visa dokumenttitel i fönstret

Nästa egenskap låter dig styra om dokumenttiteln eller filnamnet ska visas i fönstrets titelfält. Som standard är detta inställt på `false`, vilket betyder att filnamnet kommer att visas.

```csharp
Console.WriteLine("DisplayDocTitle : {0}", pdfDocument.DisplayDocTitle);
```

Om du vill att dokumentets titel ska visas istället för filnamnet måste den här inställningen vara aktiverad.

## Steg 6: Ändra storlek på fönstret så att det passar den första sidan

Ibland kanske du vill att dokumentfönstret automatiskt ska ändra storlek för att passa den första sidan i PDF-filen när det öppnas. Så här kontrollerar du om den funktionen är aktiverad:

```csharp
Console.WriteLine("FitWindow : {0}", pdfDocument.FitWindow);
```

Som standard är detta inställt på `false`, vilket innebär att fönsterstorleken kommer att förbli oförändrad oavsett den första sidans storlek.

## Steg 7: Dölj menyraden

För en mer fokuserad läsupplevelse kanske du vill dölja menyraden i läsprogrammet. Du kan hämta den här inställningen med följande rad:

```csharp
Console.WriteLine("HideMenuBar : {0}", pdfDocument.HideMenubar);
```

Detta kommer att återkomma `true` om menyraden är dold, och `false` annat.

## Steg 8: Dölj verktygsfältet

På samma sätt kan du också vilja dölja verktygsfältet i PDF-läsaren för ett renare användargränssnitt. Den här inställningen kan hämtas på följande sätt:

```csharp
Console.WriteLine("HideToolBar : {0}", pdfDocument.HideToolBar);
```

Om den här inställningen är aktiverad kommer verktygsfältet att döljas när PDF-filen öppnas.

## Steg 9: Dölj rullningslisterna och användargränssnittselementen

Om du bara vill visa sidans innehåll utan ytterligare gränssnittselement som rullningslister, styr den här inställningen beteendet:

```csharp
Console.WriteLine("HideWindowUI : {0}", pdfDocument.HideWindowUI);
```

När den är inställd på `true`, kommer PDF-läsaren att dölja rullningslister och andra element i användargränssnittet, så att endast dokumentinnehållet finns kvar.

## Steg 10: Ställ in sidläge som inte är helskärm

Du kan styra hur dokumentet visas när du avslutar helskärmsläge med hjälp av `NonFullScreenPageMode` egenskap. Den här inställningen är användbar för att definiera hur användaren ska interagera med dokumentet i icke-helskärmsläge.

```csharp
Console.WriteLine("NonFullScreenPageMode : {0}", pdfDocument.NonFullScreenPageMode);
```

Utdata kan ställas in på olika lägen som miniatyrer, konturer eller bilagepanelen.

## Steg 11: Definiera sidlayout

Den här inställningen låter dig styra hur dokumentsidorna är utformade. Du kan till exempel välja en enkelsidig vy eller en kontinuerlig kolumnvy:

```csharp
Console.WriteLine("PageLayout : {0}", pdfDocument.PageLayout);
```

Detta ger användarna flexibilitet i hur de läser eller visar dokumentinnehållet.

## Steg 12: Ange sidläge

Slutligen, den `PageMode` Egenskapen definierar hur dokumentet ska visas när det öppnas. Alternativen inkluderar att visa miniatyrbilder, gå in i helskärmsläge eller visa panelen för bilagor.

```csharp
Console.WriteLine("PageMode : {0}", pdfDocument.PageMode);
```

Beroende på dina behov kan du ställa in detta till vilket läge som helst som passar din PDF-fils syfte.

## Slutsats

Som du kan se erbjuder Aspose.PDF för .NET omfattande verktyg för att manipulera hur dina PDF-dokument visas i olika PDF-visningsprogram. Oavsett om du vill dölja verktygsfältet, centrera fönstret eller kontrollera textriktningen, erbjuder Aspose.PDF flexibiliteten att förbättra användarens visningsupplevelse.

# Vanliga frågor

### Kan jag anpassa den initiala zoomnivån för PDF-filen?
Ja, Aspose.PDF låter dig ställa in zoomnivån när dokumentet öppnas.

### Hur kan jag låsa fönsterstorleken på en PDF?
Du kan ställa in `FitWindow` egenskap för att förhindra att fönstret ändrar storlek.

### Stöder Aspose.PDF olika läslägen?
Ja, det stöder olika lägen som helskärm, miniatyrbilder och bilagor.

### Är det möjligt att dölja rullningslister i PDF-läsaren?
Absolut, du kan dölja rullningslister genom att ställa in `HideWindowUI` egendom till `true`.

### Kan jag centrera dokumentfönstret när det öppnas?
Ja, du kan styra detta genom att ställa in `CenterWindow` egendom.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}