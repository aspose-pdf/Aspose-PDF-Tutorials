---
category: general
date: 2026-04-12
description: Aggiungi rapidamente una figura a Word con C#. Scopri come posizionare
  la figura in Word, inserire la figura nel file docx e aggiungere XML personalizzato
  per layout avanzati.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: it
og_description: Aggiungi rapidamente una figura a Word con C#. Scopri come posizionare
  la figura in Word, inserire la figura nel file docx e aggiungere XML personalizzato
  per un layout avanzato.
og_title: Aggiungi figura a Word – Guida completa alla programmazione C#
tags:
- C#
- Word Automation
- Document Generation
title: Aggiungi figura a Word – Guida completa alla programmazione C#
url: /it/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere una Figura a Word – Guida Completa alla Programmazione C#

Ti è mai capitato di dover **add figure to Word** ma non sapevi da dove cominciare? Non sei l'unico. In molti progetti di automazione office il pezzo mancante è un'immagine o un diagramma posizionato correttamente all'interno di una parte XML personalizzata. Questa guida ti mostra esattamente come **position figure in Word**, inserire la figura in un file *.docx* e persino modificare l'XML personalizzato sottostante affinché la forma si comporti come qualsiasi oggetto nativo di Word.

Passeremo in rassegna un esempio reale usando la libreria GemBox.Document (gratuita per file piccoli, commerciale per carichi più grandi). Alla fine avrai un programma autonomo, eseguibile, che inserisce una figura alle coordinate X = 50, Y = 200 all'interno di un contenitore di contenuto contrassegnato. Niente scorciatoie “vedi la documentazione” vaghe—solo codice chiaro, perché funziona e consigli che puoi copiare direttamente nel tuo progetto.

## Prerequisiti

- .NET 6.0 o successivo (il codice compila anche con .NET Core 3.1)
- Pacchetto NuGet **GemBox.Document** (`Install-Package GemBox.Document`)
- Un file Word di partenza (`input.docx`) che contiene già un tag XML personalizzato dove vuoi che appaia la figura
- Conoscenze di base di C# (vedrai perché ogni riga è importante)

> **Pro tip:** Se non hai un documento pre‑taggato, puoi crearne uno in Word inserendo un *Content Control* → *XML Mapping Pane* → mappare una parte XML personalizzata. La libreria tratterà quel controllo come `TaggedContent`.

## Step 1 – Load the Source Document

La prima cosa che facciamo è aprire il file *.docx* esistente. `Document` è il punto di ingresso per tutte le operazioni di GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Why?* Loading the file gives us access to its internal parts, including any custom XML containers. Without this, we couldn’t locate the `TaggedContent` node that will hold our figure.

## Step 2 – Access the Tagged Content (Custom XML Container)

Custom XML is stored inside a *content control* in Word. GemBox exposes it as `TaggedContent`. 

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

If the document has multiple tagged sections, `TaggedContent` returns the **first** one. You can also enumerate `doc.TaggedContents` to pick a specific tag by name.

## Step 3 – Create the Figure Element

A `FigureElement` represents a picture, chart, or any visual object that Word treats as a *shape*. We’ll create it inside the tagged container.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Why create a figure here?* By attaching it to the custom XML node, Word knows the figure belongs to that logical section, which is crucial for later editing or content‑control‑based workflows.

## Step 4 – Position the Figure Precisely

Word uses points (1 pt ≈ 1/72 in) for positioning. The `PointF` struct lets us set X/Y coordinates easily.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **How to position shape word:** The `Position` property accepts a `PointF` where the first value is the horizontal offset (left) and the second is the vertical offset (top) relative to the page margin. Adjust these numbers to fine‑tune placement.

## Step 5 – Insert the Figure into the Tagged Content Tree

Now we attach the figure to the root element of the custom XML tree. This physically adds the shape to the Word document.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

At this point the figure lives inside the document, but it doesn’t have an image source yet. Let’s add a simple PNG from disk.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Step 6 – Save the Modified Document

Finally, we write the changes back to a new *.docx* file.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

When you open `output.docx` in Word, you’ll see the picture positioned exactly at (50, 200) inside the custom‑XML block you targeted.

### Full Working Example

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Expected result:** Opening `output.docx` shows the PNG placed exactly where you specified, nested inside the custom XML part. If you inspect the document’s XML (`.docx` → unzip → `word/document.xml`), you’ll see a `<w:pict>` element with the correct `<v:shape>` coordinates.

## Common Questions & Edge Cases

### What if the document has multiple tagged sections?

Use `doc.TaggedContents` to enumerate and select by tag name:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### How to add a caption to the figure?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Does this work with Word 2010 and later?

Yes. GemBox.Document targets the Open XML standard, which is compatible with Word 2007 + (including 2010, 2013, 2016, 2019, and Microsoft 365).

### What if I need to rotate the shape?

```csharp
figure.Rotation = 45; // degrees
```

### How to add a vector graphic instead of a raster image?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro Tips & Pitfalls

- **File paths:** Use `Path.Combine` to avoid hard‑coded separators, especially on non‑Windows platforms.
- **License limits:** The free GemBox license caps the document size to 20 KB. For larger files, purchase a commercial key.
- **Performance:** Re‑using a single `Document` instance for batch processing reduces memory overhead dramatically.
- **Shape overflow:** If the figure’s dimensions exceed the page margins, Word will clip it. Adjust `figure.Width` and `figure.Height` accordingly.

## Conclusione

Ora sai **how to add figure to Word**, **position figure in Word** con precisione, e come manipolare l'XML personalizzato sottostante per far comportare la forma come qualsiasi elemento nativo. L'esempio completo e eseguibile dimostra ogni passaggio—dal caricamento del documento, alla creazione di un `FigureElement`, all'impostazione delle coordinate, all'aggiunta dell'immagine e infine al salvataggio del *.docx* aggiornato.

Successivamente, prova a sperimentare con **insert figure into docx** aggiungendo più figure, usando cicli, o generando grafici al volo. Potresti anche esplorare **how to add custom xml** per controlli di contenuto più ricchi o imparare **how to position shape word** in tabelle e intestazioni. Le possibilità sono infinite, e con le basi coperte qui sei pronto a automatizzare i documenti Word come un professionista.

Buona programmazione, e sentiti libero di lasciare un commento se incontri difficoltà!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}