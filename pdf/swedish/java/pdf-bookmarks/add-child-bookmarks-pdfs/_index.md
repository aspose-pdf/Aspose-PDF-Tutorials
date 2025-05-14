---
"description": "Lär dig hur du förbättrar PDF-dokument med underordnade bokmärken med Aspose.PDF för Java. Steg-för-steg-guide med kodexempel för förbättrad navigering och organisation."
"linktitle": "Lägg till underordnade bokmärken till PDF-filer"
"second_title": "Aspose.PDF Java PDF-bearbetnings-API"
"title": "Lägg till underordnade bokmärken till PDF-filer"
"url": "/sv/java/pdf-bookmarks/add-child-bookmarks-pdfs/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till underordnade bokmärken till PDF-filer


## Introduktion till att lägga till underordnade bokmärken till PDF-filer

den här artikeln ska vi utforska hur man lägger till underordnade bokmärken till PDF-dokument med hjälp av Aspose.PDF för Java. Underordnade bokmärken är ett bekvämt sätt att organisera och navigera genom innehållet i ett PDF-dokument, vilket gör det enklare för användare att hitta specifika avsnitt eller ämnen i dokumentet.

## Förkunskapskrav

Innan vi går in i implementeringen, se till att du har följande förutsättningar på plats:

- Java-utvecklingsmiljön installerad på ditt system.
- Aspose.PDF för Java-biblioteket. Du kan ladda ner det från [här](https://releases.aspose.com/pdf/java/).

## Konfigurera miljön

1. Ladda ner Aspose.PDF för Java-biblioteket från den medföljande länken.
2. Lägg till biblioteket i ditt Java-projekt.

Nu ska vi börja med att skapa ett nytt PDF-dokument och lägga till underordnade bokmärken i det steg för steg.

## Skapa ett nytt PDF-dokument

För att börja behöver vi initiera ett PDF-dokument och lägga till sidor i det. Här är kodavsnittet för att komma igång:

```java
// Initiera ett PDF-dokument
Document pdfDocument = new Document();

// Lägg till sidor i PDF-filen
pdfDocument.getPages().add();
pdfDocument.getPages().add();
```

det här exemplet har vi skapat ett nytt PDF-dokument och lagt till två sidor i det.

## Lägga till överordnade bokmärken

Överordnade bokmärken fungerar som huvudavsnitt eller kategorier i ditt PDF-dokument. Nu skapar vi några överordnade bokmärken:

```java
// Skapa överordnade bokmärken
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);
```

Vi har lagt till två överordnade bokmärken, "Överordnat bokmärke 1" och "Överordnat bokmärke 2".

## Lägga till underordnade bokmärken

Nu är det dags att lägga till underordnade bokmärken till de överordnade bokmärken vi skapade tidigare. Underordnade bokmärken representerar specifika ämnen eller underavsnitt inom varje överordnat bokmärke. Så här gör du:

```java
// Lägg till underordnade bokmärken till överordnat bokmärke 1
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// Lägg till underordnade bokmärken till överordnat bokmärke 2
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);
```

Vi har lagt till underordnade bokmärken till både "Föräldrabokmärke 1" och "Föräldrabokmärke 2".

## Anpassa bokmärkets utseende

Du kan anpassa utseendet på bokmärken genom att ändra deras text och stil. Dessutom kan du lägga till ikoner i bokmärken för bättre visuell representation. Här är ett exempel på hur du gör det:

```java
// Anpassa bokmärkets utseende
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());
```

I det här exemplet har vi gjort det överordnade bokmärket kursivt, ändrat textfärgen på det underordnade bokmärket till grönt och lagt till en kursiv ikon i det underordnade bokmärket.

## Hantering av händelser

Bokmärken kan också ha associerade åtgärder. Du kan till exempel lägga till åtgärder som utlöses när en användare klickar på ett bokmärke. Så här hanterar du klickhändelser på bokmärken:

```java
// Lägg till en åtgärd i ett bokmärke
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);
```

I den här koden har vi lagt till en "Gå till"-åtgärd till ett underordnat bokmärke som tar användaren till den andra sidan i PDF-filen när man klickar på den.

## Spara PDF-filen

När du har lagt till alla nödvändiga bokmärken och anpassat deras utseende och åtgärder kan du spara det modifierade PDF-dokumentet:

```java
// Spara PDF-dokumentet
pdfDocument.save("output.pdf");
```

Ditt PDF-dokument med underordnade bokmärken är nu klart.

## Komplett källkod

Här är den kompletta källkoden för att lägga till underordnade bokmärken till ett PDF-dokument med Aspose.PDF för Java:

```java
// Initiera ett PDF-dokument
Document pdfDocument = new Document();

// Lägg till sidor i PDF-filen
pdfDocument.getPages().add();
pdfDocument.getPages().add();

// Skapa överordnade bokmärken
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);

// Lägg till underordnade bokmärken till överordnat bokmärke 1
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// Lägg till underordnade bokmärken till överordnat bokmärke 2
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);

// Anpassa bokmärkets utseende
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());

// Lägg till en åtgärd i ett bokmärke
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);

// Spara PDF-dokumentet
pdfDocument.save("output.pdf");
```

## Slutsats

Att lägga till underordnade bokmärken till PDF-filer med Aspose.PDF för Java är en kraftfull funktion som förbättrar navigeringen och organiseringen av dina dokument. Genom att följa stegen som beskrivs i den här artikeln kan du skapa välstrukturerade PDF-filer med överordnade och underordnade bokmärken, anpassa deras utseende och till och med lägga till åtgärder för att förbättra användarupplevelsen.

## Vanliga frågor

### Hur kan jag ladda ner Aspose.PDF för Java?

Du kan ladda ner Aspose.PDF för Java från webbplatsen [här](https://releases.aspose.com/pdf/java/).

### Stöds underordnade bokmärken i alla PDF-läsare?

Ja, underordnade bokmärken stöds i de flesta moderna PDF-visare och ger en förbättrad användarupplevelse för att navigera i PDF-dokument.

### Kan jag anpassa utseendet på bokmärken ytterligare?

Ja, du kan anpassa utseendet på bokmärken genom att justera textstilar, färger och ikoner så att de passar dokumentets design.

### Vilka andra åtgärder kan jag lägga till i bokmärken?

Förutom "Gå till"-åtgärder kan du lägga till åtgärder som "URI"-åtgärder för att öppna webblänkar eller "JavaScript"-åtgärder för att köra anpassade skript när man klickar på ett bokmärke.

### Är Aspose.PDF för Java lämplig för kommersiella projekt?

Ja, Aspose.PDF för Java är lämpligt för både personliga och kommersiella projekt, och det erbjuder ett brett utbud av funktioner för PDF-manipulation och generering.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}