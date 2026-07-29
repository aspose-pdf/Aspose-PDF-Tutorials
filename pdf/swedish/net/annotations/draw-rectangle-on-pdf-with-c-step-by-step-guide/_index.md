---
category: general
date: 2026-06-21
description: Rita en rektangel på PDF med C#. Lär dig hur du laddar PDF-dokument,
  skapar en svart rektangelannotation och sparar den modifierade PDF-filen effektivt.
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: sv
og_description: Rita en rektangel på PDF i C# genom att ladda ett PDF‑dokument, skapa
  en svart rektangelannotation och spara den modifierade PDF‑filen. Fullständig kod
  inkluderad.
og_title: Rita rektangel på PDF med C# – Komplett programmeringshandledning
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: Rita rektangel på PDF med C# – Steg‑för‑steg‑guide
url: /sv/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rita rektangel i PDF med C# – Komplett programmeringstutorial

Har du någonsin behövt **draw rectangle on PDF**‑filer från en .NET‑app men varit osäker på var du ska börja? Du är inte ensam. Oavsett om det handlar om att markera ett avsnitt, maskera känslig data eller helt enkelt lägga till en visuell ledtråd, kan kunskapen om hur man *draw rectangle on PDF* programatiskt spara dig timmar av manuellt redigerande.

I den här guiden går vi igenom ett praktiskt exempel som **loads a PDF document**, **creates a black rectangle**, och sedan **saves the modified PDF**. I slutet har du ett återanvändbart kodsnutt som du kan klistra in i vilket C#‑projekt som helst—ingen mystik, bara tydlig kod och förklaringar.

## Vad den här tutorialen täcker

- Hur man **load pdf document** med Aspose.PDF för .NET‑biblioteket  
- Definiera en rektangels koordinater och säkerställa att den förblir inom sidans gränser  
- Använda **add black rectangle**‑metoden för att annotera sidan  
- **Save modified pdf** till en ny filplats  
- Hantera edge‑case (flera sidor, rektanglar utanför gränser, anpassade färger)  

Inga externa verktyg, inga vaga referenser—bara ett komplett, körbart exempel som du kan kopiera‑och‑klistra.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

1. .NET 6.0 SDK (eller någon nyare .NET‑version) installerad  
2. En referens till **Aspose.PDF for .NET** (tillgänglig via NuGet: `Install-Package Aspose.PDF`)  
3. En befintlig PDF‑fil (`input.pdf`) placerad i en mapp du kan läsa/skriva i  

Det är allt. Om du är bekväm med grundläggande C#‑syntax, är du redo att köra.

---

## Steg 1: Ladda PDF‑dokument

Det första vi behöver är ett **load pdf document**‑anrop. Aspose.PDF:s `Document`‑klass tar filvägen och läser in hela filen i minnet.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*Varför detta är viktigt*: Att ladda PDF‑en ger dig åtkomst till dess sidor, metadata och ritningsyta. Utan detta steg kan du inte placera några former.

---

## Steg 2: Välj mål sidan

PDF‑sidor är 1‑baserade i Aspose, så den första sidan har index 1. Hämta den sida du vill annotera—vanligtvis den första för en snabb demonstration.

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

Om du behöver arbeta på en annan sida, ändra bara indexet. Kom ihåg att validera att indexet finns för att undvika `ArgumentOutOfRangeException`.

---

## Steg 3: Definiera rektangelns geometri

En rektangel definieras av sina nedre‑vänstra (X,Y) och övre‑högra (X,Y) koordinater. `Rectangle`‑strukturen lagrar dessa som `LLX`, `LLY`, `URX`, `URY`.

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

Justera gärna dessa siffror—`100,100` placerar det nedre‑vänstra hörnet 100 punkter från vänster- och bottenkant, medan `300,300` sätter det övre‑högra hörnet 300 punkter från kanterna.

---

## Steg 4: Verifiera att rektangeln får plats inom sidan

Att försöka rita utanför sidans gränser kommer antingen att ignoreras eller orsaka ett undantag, beroende på biblioteksversionen. En snabb kontroll håller din kod robust.

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*Proffstips*: Om du planerar att stödja PDF‑filer med varierande storlekar, kan du beräkna rektangeln baserat på en procentandel av sidans bredd/höjd istället för absoluta punkter.

---

## Steg 5: Lägg till svart rektangel‑annotation

Nu blir det roligt—**add black rectangle** till sidan. Aspose tillhandahåller `AddRectangle` som tar geometrin och en `Color`. Vi kommer att använda `Color.Black` för att **create black rectangle**.

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

Den enda raden gör det tunga arbetet: den skapar ett annoteringsobjekt, sätter dess kantfärg till svart och infogar det i sidans annoteringssamling.

Om du någon gång behöver en annan fyllning eller kantstil, utforska overload‑versionen som accepterar ett `Annotation`‑objekt där du kan justera linjebredd, streckmönster eller till och med opacitet.

---

## Steg 6: Spara modifierad PDF

Till sist, spara dina ändringar med **save modified pdf**. Du kan skriva över originalet eller skriva till en ny fil—här skapar vi en output‑fil.

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

Det är hela arbetsflödet. Kör programmet och öppna `output.pdf`; du bör se en solid svart rektangel där du definierade den.

---

## Fullt fungerande exempel

Nedan är en fristående konsolapplikation som samlar alla stegen. Kopiera den till ett nytt `.csproj` och tryck på **Run**.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**Förväntad output** i konsolen:

```
Successfully drew rectangle on PDF and saved the file.
```

Öppna `output.pdf` så ser du en svart rektangel placerad på de koordinater du angav.

---

## Hantera vanliga variationer

| Situation | Vad du ska ändra | Varför |
|-----------|------------------|--------|
| **Multiple pages** | Loopa igenom `pdfDocument.Pages` och tillämpa samma logik på varje `Page`‑objekt. | Gör det möjligt att batch‑annotera hela dokumentet. |
| **Different colors** | Byt `Color.Black` mot `Color.Red` eller någon `System.Drawing.Color`. | Användbart för att markera snarare än att maskera. |
| **Transparent fill** | Använd `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }`. | Ger ett halvtransparent lager istället för ett solid block. |
| **Dynamic rectangle size** | Beräkna `URX` och `URY` baserat på `PageInfo.Width * 0.5` osv. | Gör att rektangeln anpassar sig till olika sidstorlekar. |
| **Error handling** | Omslut hela blocket med `try…catch` och logga `Aspose.Pdf.IOException`. | Förhindrar krascher när källfilen saknas eller är låst. |

---

## Proffstips & fallgropar

- **Dispose the Document**: Även om Aspose.PDF implementerar `IDisposable` är `using`‑mönstret inte strikt nödvändigt för kortlivade konsolappar. I långlivade tjänster, omslut `Document` med ett `using`‑block för att snabbt frigöra inhemska resurser.  
- **Coordinate System**: PDF‑koordinater börjar i det nedre‑vänstra hörnet. Om du är van vid ett övre‑vänster ursprung (som i WinForms) måste du invertera Y‑axeln: `pageHeight - y`.  
- **Performance**: Att lägga till annotationer i mycket stora PDF‑filer kan vara minnesintensivt. Överväg att bearbeta sidor i delar eller använda `PdfFileEditor` för mer lättviktiga redigeringar.  
- **Legal**: Säkerställ att du har rätt att modifiera käll‑PDF‑en—vissa dokument är skyddade mot redigering.

---

## Slutsats

Vi har just demonstrerat hur man **draw rectangle on PDF** med C#—från **load pdf document**, definiera geometri, **add black rectangle**, och slutligen **save modified pdf**. Exemplet är komplett, körbart och anpassningsbart till verkliga scenarier som batch‑bearbetning eller anpassad stil.

Nästa steg kan vara att utforska att lägga till andra annoteringstyper (text, markeringar) eller att slå ihop flera PDF‑filer efter annotering. Både **load pdf document** och **save modified pdf**‑stegen förblir desamma, så du kan utöka detta mönster med förtroende.

Har du ett eget knep du provat? Dela det i kommentarerna, och lycka till med kodandet!

---

## Vad bör du lära dig härnäst?

Följande tutorials täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa fyllt rektangelobjekt i PDF med Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Skapa fyllt rektangelobjekt i PDF med Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Skapa fyllt rektangelobjekt i PDF med Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}