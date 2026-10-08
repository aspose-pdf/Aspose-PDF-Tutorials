---
category: general
date: 2026-06-18
description: Lägg till textruta i PDF-formulär snabbt. Lär dig hur du skapar en ifyllbar
  PDF-textruta och hur du lägger till ett kommentarsfält i PDF med Aspose.PDF för
  .NET.
draft: false
keywords:
- add text box to pdf form
- create fillable pdf textbox
- how to add comment field pdf
language: sv
og_description: Lägg till en textruta i PDF‑formulär med Aspose.PDF för .NET. Denna
  handledning visar hur du skapar en ifyllbar PDF‑textruta och hur du lägger till
  ett kommentarsfält i PDF på bara några rader.
og_title: Lägg till textruta i PDF‑formulär – Komplett C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Add text box to PDF form quickly. Learn how to create fillable PDF
    textbox and how to add comment field PDF using Aspose.PDF for .NET.
  headline: Add Text Box to PDF Form – Complete C# Guide
  type: TechArticle
- description: Add text box to PDF form quickly. Learn how to create fillable PDF
    textbox and how to add comment field PDF using Aspose.PDF for .NET.
  name: Add Text Box to PDF Form – Complete C# Guide
  steps:
  - name: – Load the PDF document
    text: We need a `Document` object that represents the existing file. Aspose.PDF
      makes this a one‑liner.
  - name: – Create a TextBox field on the target page
    text: We’ll place the textbox on page 1 (index 0) inside a rectangle that defines
      its size and position. The rectangle uses points (1 inch = 72 points).
  - name: – Assign a name to the field
    text: Every form field needs a unique identifier. This name is what you’ll reference
      later when extracting data.
  - name: – Enable multiple widget annotations (optional but handy)
    text: If you want the same textbox to appear on several pages, set `MultipleWidgetAnnotations`
      to `true`. For a single‑page comment field you can skip this, but it doesn’t
      hurt.
  - name: – Add the TextBox field to the document’s form collection
    text: Now the field becomes part of the PDF’s interactive form.
  - name: – Save the modified PDF
    text: Finally, write the changes back to disk.
  - name: Can I set a default value?
    text: Yes. Just assign `textBox.Value = "Enter your comment here";` before adding
      the field.
  - name: What if I need a multiline textbox?
    text: 'Set the `IsMultiline` property:'
  - name: How do I change the appearance (border, background)?
    text: '```csharp textBox.BorderColor = Color.Black; textBox.BorderWidth = 1; textBox.BackgroundColor
      = Color.LightYellow; ```'
  - name: Does this work with PDF/A or encrypted PDFs?
    text: 'Aspose.PDF can handle PDF/A‑1b, PDF/A‑2b, and encrypted files as long as
      you provide the password when loading:'
  type: HowTo
tags:
- pdf
- csharp
- pdf-form
- textbox
- aspnet
title: Lägg till en textruta i PDF‑formulär – komplett C#‑guide
url: /sv/net/programming-with-forms/add-text-box-to-pdf-form-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till textruta i PDF-formulär – Komplett C#-guide

Har du någonsin behövt **lägga till textruta i PDF-formulär** men varit osäker på vilka API‑anrop du ska använda? Du är inte ensam. Oavsett om du bygger en feedback‑samling, en portal för kontraktssignering eller ett enkelt kommentarfält, är en ifyllbar textruta den självklara lösningen. I den här guiden går vi igenom de exakta stegen för att **skapa ifyllbar PDF‑textruta** och svarar också på den vanliga frågan **hur man lägger till kommentarfält PDF** med Aspose.PDF för .NET.

Vi börjar med en ren PDF, placerar en textruta på sida 1, ger den ett vänligt namn, aktiverar flera widgetar och sparar slutligen resultatet. När du är klar har du en färdig PDF som vem som helst kan öppna i Adobe Reader, skriva en kommentar och trycka på Spara. Inga externa verktyg, ingen manuell redigering – bara ren C#‑kod.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.7+)  
- Visual Studio 2022 eller någon annan IDE du föredrar  
- Aspose.PDF för .NET NuGet‑paket (`Install-Package Aspose.PDF`)  
- En käll‑PDF (`input.pdf`) placerad i en mapp du kontrollerar  

Det är allt. Om du redan har dessa komponenter är du redo att köra.

## Lägg till textruta i PDF-formulär med C#

Nedan är kärnan i handledningen. Varje steg förklaras, följt av motsvarande C#‑kodsnutt. Känn dig fri att kopiera‑klistra in hela blocket i en konsolapp; den kompilerar och körs som den är.

### Steg 1 – Ladda PDF‑dokumentet

Vi behöver ett `Document`‑objekt som representerar den befintliga filen. Aspose.PDF gör detta till en enradare.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using System.Drawing;

// Load the source PDF
Document doc = new Document(@"C:\MyPdfs\input.pdf");
```

*Varför detta är viktigt:* Att ladda PDF‑en ger oss åtkomst till dess sidor, annotationer och formulärsamlingen där fält finns. Utan ett `Document`‑instans kan vi inte lägga till något.

### Steg 2 – Skapa ett TextBox‑fält på mål‑sidan

Vi placerar textrutan på sida 1 (index 0) inom en rektangel som definierar dess storlek och position. Rektangeln använder punkter (1 tum = 72 punkter).

```csharp
// Define the rectangle: left, bottom, right, top
Rectangle rect = new Rectangle(100, 600, 300, 630);

// Create the TextBox field on page 1
TextBoxField textBox = new TextBoxField(doc.Pages[1], rect);
```

*Varför detta är viktigt:* Rektangeln bestämmer var användaren ser fältet. Justera koordinaterna för att passa din layout. Klassen `TextBoxField` ärver automatiskt visuella egenskaper som ram och bakgrund.

### Steg 3 – Tilldela ett namn till fältet

Varje formulärfält behöver en unik identifierare. Detta namn är vad du kommer att referera till senare när du extraherar data.

```csharp
textBox.FieldName = "Comments";
```

*Varför detta är viktigt:* Att namnge fältet `"Comments"` låter dig hämta användarens inmatning med `doc.Form["Comments"]` efter att PDF‑en har fyllts i. Det visas också i PDF‑läsarens fältlista.

### Steg 4 – Aktivera flera widget‑annotationer (valfritt men praktiskt)

Om du vill att samma textruta ska visas på flera sidor, sätt `MultipleWidgetAnnotations` till `true`. För ett kommentarfält på en enda sida kan du hoppa över detta, men det skadar inte.

```csharp
textBox.MultipleWidgetAnnotations = true;
```

*Varför detta är viktigt:* Flera widgetar delar samma data, så en användare kan skriva en gång och se samma kommentar på varje sida som innehåller widgeten. Det är ett smart trick för flersidiga kontrakt.

### Steg 5 – Lägg till TextBox‑fältet i dokumentets formulärsamling

Nu blir fältet en del av PDF‑ens interaktiva formulär.

```csharp
doc.Form.Add(textBox);
```

*Varför detta är viktigt:* Att lägga till fältet registrerar det i PDF‑ens AcroForm‑ordbok. Utan detta steg skulle textrutan existera i minnet men aldrig visas i den sparade filen.

### Steg 6 – Spara den modifierade PDF‑en

Till sist skriver du ändringarna tillbaka till disken.

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

*Varför detta är viktigt:* Att spara bevarar det nya formulärfältet. Öppna `output.pdf` i Adobe Reader så ser du en tom textruta märkt “Comments” redo för inmatning.

## Fullständigt fungerande exempel

När vi sätter ihop allt, här är en fristående konsolapplikation som du kan köra omedelbart:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using System.Drawing; // for Rectangle

namespace PdfFormDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the existing PDF
            string inputPath = @"C:\MyPdfs\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Define the rectangle where the textbox will live
            Rectangle rect = new Rectangle(100, 600, 300, 630);

            // 3️⃣ Create the TextBox field on page 1 (index 1)
            TextBoxField textBox = new TextBoxField(doc.Pages[1], rect)
            {
                // 4️⃣ Give it a meaningful name
                FieldName = "Comments",

                // 5️⃣ Allow the same widget on multiple pages (optional)
                MultipleWidgetAnnotations = true
            };

            // 6️⃣ Add the field to the form collection
            doc.Form.Add(textBox);

            // 7️⃣ Save the updated PDF
            string outputPath = @"C:\MyPdfs\output.pdf";
            doc.Save(outputPath);

            Console.WriteLine("✅ Text box added successfully! Check " + outputPath);
        }
    }
}
```

**Förväntat resultat:** När du öppnar `output.pdf` ser du ett rektangulärt inmatningsområde på sida 1. Att klicka inuti låter dig skriva en kommentar. Fältet kvarstår efter sparning, vilket betyder att du framgångsrikt har svarat på **hur man lägger till kommentarfält PDF**.

## Vanliga frågor & specialfall

### Kan jag ange ett standardvärde?

Ja. Tilldela bara `textBox.Value = "Enter your comment here";` innan du lägger till fältet.

### Vad händer om jag behöver en flerradig textruta?

Sätt egenskapen `IsMultiline`:

```csharp
textBox.IsMultiline = true;
textBox.MaxLength = 500; // optional limit
```

### Hur ändrar jag utseendet (ram, bakgrund)?

```csharp
textBox.BorderColor = Color.Black;
textBox.BorderWidth = 1;
textBox.BackgroundColor = Color.LightYellow;
```

### Fungerar detta med PDF/A eller krypterade PDF‑filer?

Aspose.PDF kan hantera PDF/A‑1b, PDF/A‑2b och krypterade filer så länge du anger lösenordet vid inläsning:

```csharp
Document doc = new Document(inputPath, new LoadOptions { Password = "secret" });
```

### Vad händer om jag behöver textrutan på en annan sida?

Byt ut `doc.Pages[1]` mot önskat sidindex (`doc.Pages[2]` för sida 3, osv.). Kom ihåg att sidkollektioner är **1‑baserade** i Aspose.PDF.

## Pro‑tips

- **Pro tip:** Använd `doc.Form.RefreshAppearance();` efter att ha lagt till flera fält för att säkerställa att alla widgetar renderas korrekt i äldre PDF‑visare.
- **Se upp för:** Överlappande rektanglar. Om två fält delar samma område kan Acrobat dölja ett av dem.
- **Prestanda‑notering:** När du bearbetar tusentals PDF‑filer, återanvänd en enda `Document`‑instans för läsning och klona bara formulärfältet för att undvika upprepade allokeringar.

## Nästa steg

Nu när du vet hur man **lägger till textruta i PDF-formulär**, kanske du vill utforska relaterade ämnen:

- **Skapa ifyllbar PDF‑textruta** med valideringsregler (`textBox.Validate = new RegExValidator("[A-Za-z0-9]+");`)
- **Lägg till radioknappar eller kryssrutor** för att bygga ett komplett frågeformulär
- **Platta till formuläret** efter inlämning för att förhindra vidare redigering (`doc.Form.Flatten();`)
- **Extrahera inskrivna data** med `doc.Form["Comments"].Value` och lagra dem i en databas

Alla dessa bygger på samma grundkoncept som vi gick igenom, så du är väl förberedd att utöka ditt PDF‑automatiseringsverktyg.

---

*Lycka till med kodandet! Om du stöter på problem, lämna en kommentar nedan så felsöker vi tillsammans.*

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man lägger till TextBox‑fält i PDF‑filer med Aspose.PDF för .NET: En steg‑för‑steg‑guide](/pdf/english/net/forms-annotations/add-textbox-field-aspose-pdf-net/)
- [Hur man lägger till och extraherar PDF‑formulärfält med Aspose.PDF för .NET: En omfattande guide](/pdf/english/net/forms-annotations/manage-pdf-form-fields-aspose-dotnet/)
- [Hur man lägger till verktygstips i PDF‑text med Aspose.PDF för .NET (Formulär & Annotationer)](/pdf/english/net/forms-annotations/aspose-pdf-net-add-tooltips-pdfs/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}