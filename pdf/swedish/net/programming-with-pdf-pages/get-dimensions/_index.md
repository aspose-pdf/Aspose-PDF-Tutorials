---
"description": "I den här handledningen förklarar vi hur man hämtar PDF-siddimensioner och utför manipulationer med Aspose.PDF för .NET. Detaljerade steg finns för att vägleda dig genom processen."
"linktitle": "Hämta PDF-siddimensioner"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Hämta PDF-siddimensioner"
"url": "/sv/net/programming-with-pdf-pages/get-dimensions/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hämta PDF-siddimensioner

## Introduktion

Har du någonsin behövt manipulera siddimensionerna i ett PDF-dokument? Kanske har du velat ändra storlek på en sida eller rotera den för att passa dina behov? I så fall har du kommit rätt! I den här handledningen guidar vi dig genom hur du hämtar och modifierar PDF-siddimensioner med hjälp av Aspose.PDF för .NET. Oavsett om du är nybörjare eller en erfaren utvecklare kommer du att tycka att den här guiden är enkel och lätt att följa.

Aspose.PDF för .NET är ett kraftfullt bibliotek som låter dig skapa, manipulera och omvandla PDF-filer utan ansträngning. Det är som att ha en schweizisk armékniv för PDF-filer – du kan finjustera varje liten detalj för att passa dina exakta behov. Så låt oss dyka rakt in och lära oss hur man hämtar och uppdaterar PDF-siddimensioner med hjälp av detta fantastiska verktyg!

## Förkunskapskrav

Innan du börjar behöver du ha några saker på plats för att följa den här handledningen smidigt:

1. Aspose.PDF för .NET: Du kan [ladda ner den senaste versionen här](https://releases.aspose.com/pdf/net/)Om du inte har någon licens, oroa dig inte! Du kan begära en [gratis provperiod](https://releases.aspose.com/), eller välj en [tillfällig licens](https://purchase.aspose.com/temporary-license/).
2. Visual Studio: Utvecklingsmiljön du kommer att använda för att skriva och exekvera koden.
3. Grundläggande kunskaper i C#: Vi kommer att hålla det enkelt, men lite förtrogenhet med C# kommer att göra processen smidigare.
4. PDF-fil att arbeta med: Hämta valfri exempel-PDF-fil eller skapa en ny att testa.

## Importera paket

För att arbeta med Aspose.PDF för .NET behöver du importera några viktiga namnrymder. Detta förbereder förutsättningarna för att interagera med PDF-dokument. Så här gör du:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Dessa importer säkerställer att du har tillgång till de kärnklasser som behövs för att manipulera PDF-filer, särskilt för att hantera sidor och hämta deras dimensioner.

Nu när vi har allt på plats, låt oss dela upp processen i enkla steg.

## Steg 1: Definiera filsökvägen och ladda dokumentet

Det första steget är att ange sökvägen till ditt PDF-dokument och ladda det med Aspose.PDF. Detta gör att du kan interagera med sidorna i PDF-filen.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Öppna dokumentet
Document pdfDocument = new Document(dataDir + "UpdateDimensions.pdf");
```

I det här steget öppnar du i princip PDF-filen du vill arbeta med. Om du någonsin har öppnat en bok på en viss sida är det ganska likt – men istället öppnar du ett PDF-dokument för att komma åt dess sidor.

## Steg 2: Lägg till en tom sida om inga sidor finns

Vad händer om ditt dokument inte har några sidor? Oroa dig inte! Vi kan lägga till en tom sida i dokumentet och arbeta med den. Så här kontrollerar du om en sida finns och lägger till en ny om det behövs:

```csharp
// Lägger till en tom sida i ett pdf-dokument
Page page = pdfDocument.Pages.Count > 0 ? pdfDocument.Pages[1] : pdfDocument.Pages.Add();
```

Den här kodraden kontrollerar om det redan finns en sida i dokumentet. Om ja, väljer den första sidan (`Pages[1]`Annars skapas en tom sida och den läggs till i PDF-filen.

Tänk på det som att öppna en tom anteckningsbok och skriva på första sidan om ingenting finns där – enkelt, eller hur?

## Steg 3: Hämta information om sidans höjd och bredd

Nu när vi har en sida att arbeta med, låt oss hämta sidans dimensioner. Vi använder `GetPageRect()` metod för att få höjd och bredd.

```csharp
// Hämta information om sidans höjd och bredd
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

Här, `GetPageRect(true)` returnerar en rektangel som inkluderar sidans höjd och bredd. Det är som att mäta ett papper med en linjal. Utdata visas i konsolen och ger dig de aktuella sidmåtten.

## Steg 4: Rotera sidan 90 grader

Vill du rotera sidan? Inga problem! Med en enkel egenskap kan du rotera sidan 90 grader.

```csharp
// Rotera sidan i 90 graders vinkel
page.Rotate = Rotation.on90;
```

Det här steget roterar sidan medsols 90 grader. Tänk dig att du vänder ett utskrivet ark på skrivbordet – nu är det i liggande läge!

## Steg 5: Kontrollera siddimensionerna igen efter rotation

Efter att du har roterat sidan är det en bra idé att kontrollera måtten igen. Varför? Rotation kan påverka hur du tolkar höjden och bredden.

```csharp
// Hämta information om sidans höjd och bredd
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

Nu kommer sidans dimensioner att uppdateras baserat på den nya orienteringen. Det är som att rotera ett foto på din telefon – plötsligt blir bredden höjden och vice versa.


## Slutsats

Grattis! Du har nu lärt dig hur man hämtar och ändrar måtten på en PDF-sida med Aspose.PDF för .NET. Nu borde du kunna ladda en PDF, kontrollera dess sidmått och till och med rotera sidan om det behövs.

Att manipulera PDF-filer behöver inte vara komplicerat. Med Aspose.PDF är det så enkelt som att följa några steg och använda intuitiva metoder. Så nästa gång du behöver hantera PDF-siddimensioner vet du exakt vad du ska göra!

## Vanliga frågor

### Kan jag rotera sidan med andra vinklar än 90 grader?
Ja, Aspose.PDF låter dig rotera sidor med 0, 90, 180 eller 270 grader med hjälp av `Rotation` egendom.

### Vad händer om min PDF inte har några sidor?
Om din PDF inte har några sidor kan du lägga till en tom sida med hjälp av `Pages.Add()` metod, som visas i den här handledningen.

### Kan jag manipulera flera sidor samtidigt?
Ja, du kan loopa igenom flera sidor och tillämpa transformationer, som att ändra storlek eller rotera, på dem alla.

### Påverkar sidmåtten innehållet i PDF-filen?
Sidmått ändrar bara storleken på arbetsytan, inte innehållet. Däremot kan storleksändring påverka hur innehållet visas på sidan.

### Var kan jag hitta mer information om Aspose.PDF för .NET?
Du kan besöka [dokumentation här](https://reference.aspose.com/pdf/net/) för mer detaljerad information och avancerade användningsfall.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}