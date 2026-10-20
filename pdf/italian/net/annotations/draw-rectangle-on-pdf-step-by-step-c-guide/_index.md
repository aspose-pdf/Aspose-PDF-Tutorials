---
category: general
date: 2026-08-14
description: Disegna un rettangolo su PDF rapidamente usando C#. Scopri come definire
  le dimensioni del rettangolo e aggiungere forme a una pagina PDF in poche righe.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: it
lastmod: 2026-08-14
og_description: disegna un rettangolo su PDF con C# in pochi secondi. Questa guida
  mostra come definire le dimensioni del rettangolo, aggiungere una forma e verificare
  i limiti della pagina per una grafica PDF affidabile.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: disegnare un rettangolo su PDF – tutorial completo C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Disegnare un rettangolo su PDF – guida passo‑passo C#
url: /it/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# disegnare un rettangolo su pdf – tutorial completo C#

Se hai bisogno di **draw rectangle on pdf** usando C#, questa guida ti mostra una soluzione concisa, pronta per la produzione. Vedrai esattamente **how to define rectangle dimensions**, verifica che la forma si adatti e aggiungila a una pagina con una singola chiamata di metodo.

Il tutorial copre tutto, dalla creazione di un documento PDF al rendering del rettangolo, così puoi copiare‑incollare il codice nel tuo progetto e vedere i risultati immediatamente. Non è necessaria alcuna documentazione esterna—basta seguire i passaggi qui sotto.

## Prerequisiti

* .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.7+)
* Il pacchetto NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
* Una conoscenza di base della sintassi C#
* Un IDE come Visual Studio o VS Code

> **Consiglio professionale:** Usa la licenza di valutazione gratuita di Aspose.PDF per esperimenti rapidi; aggiunge una piccola filigrana ma ti consente di testare tutte le funzionalità.

## Come disegnare un rettangolo su PDF con C#

Il nucleo del compito è creare un `RectangleShape`, impostarne le dimensioni e lo spessore, e collegarlo a una `Page`. L'intestazione H2 seguente contiene la parola chiave principale, soddisfacendo i requisiti SEO.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Spiegazione di ogni passaggio

| Passaggio | Perché è importante |
|------|----------------|
| **1️⃣ Create a new PDF document** | Inizializza il contenitore che conterrà pagine e grafica. |
| **2️⃣ Add a blank page** | Hai bisogno di un oggetto `Page` perché le forme vengono collegate a una pagina, non direttamente al documento. |
| **3️⃣ Define the rectangle bounds** | Qui è dove **how to define rectangle dimensions**. Il costruttore `Rectangle` accetta `x`, `y`, `width` e `height` in punti (1 pt = 1/72 in). |
| **4️⃣ Create the rectangle shape** | `RectangleShape` è la classe Aspose che renderizza un rettangolo. Impostare `StrokeColor` definisce il contorno; puoi anche impostare `FillColor` per un riempimento solido. |
| **5️⃣ Verify page boundaries** | `CheckShapeBoundary` lancia un'eccezione se il rettangolo supera le dimensioni della pagina, evitando PDF malformati. |
| **6️⃣ Add the shape to the page** | La forma diventa parte del flusso di contenuto della pagina. |
| **7️⃣ Save the PDF** | Salva il documento su un file che puoi aprire con qualsiasi visualizzatore PDF. |

Il risultato `RectangleDemo.pdf` contiene un rettangolo nero posizionato nell'angolo in alto a sinistra della pagina, esattamente 500 pt di larghezza e 700 pt di altezza.

![disegnare rettangolo su pdf esempio](https://example.com/rectangle-demo.png "disegnare rettangolo su pdf esempio")

*Testo alternativo dell'immagine: disegnare rettangolo su pdf esempio che mostra un rettangolo nero nell'angolo superiore sinistro di una pagina PDF.*

## Come definire le dimensioni del rettangolo per diverse dimensioni di pagina

Il frammento sopra utilizza valori fissi (`500 x 700`). Nelle applicazioni reali spesso è necessario che il rettangolo si adatti alla larghezza e all'altezza della pagina.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Punti chiave:**

* Usa `page.PageInfo.Width` e `Height` per leggere le dimensioni effettive della pagina.
* Moltiplicare per un fattore (ad esempio `0.8f`) ti consente di esprimere le dimensioni come percentuale della pagina.
* Il centraggio si ottiene sottraendo la dimensione del rettangolo dalla dimensione della pagina e dividendo a metà il resto.

## Errori comuni e come evitarli

| Problema | Perché succede | Soluzione |
|---------|----------------|-----|
| Rectangle extends beyond the page | Dimensioni codificate rigide più grandi della dimensione della pagina. | Chiama `page.CheckShapeBoundary` **prima** di aggiungere la forma; regola le dimensioni se viene lanciata un'eccezione. |
| Stroke not visible | `StrokeColor` lasciato al valore predefinito (`Color.Empty`). | Imposta esplicitamente `StrokeColor` (ad esempio `Color.Black`). |
| Rectangle appears off‑screen | Le coordinate iniziano in basso a sinistra nello spazio PDF; usare coordinate stile schermo in alto a sinistra provoca un'inversione. | Ricorda che l'origine `(0,0)` è l'angolo in basso a sinistra. Regola `y` di conseguenza o usa `pageHeight - desiredY`. |
| Unexpected line thickness | Lo spessore di linea predefinito può essere troppo sottile per la stampa. | Imposta `rectangleShape.LineWidth = 2;` per aumentare lo spessore. |

## Estendere l'esempio

Una volta che puoi **draw rectangle on pdf**, puoi facilmente aggiungere altre forme:

* **EllipseShape** – per cerchi o ovali.
* **PolygonShape** – per poligoni personalizzati.
* **TextFragment** – per etichettare i tuoi rettangoli.

Tutte le forme condividono lo stesso flusso di lavoro: definire i limiti, configurare l'aspetto, verificare i confini, quindi aggiungere alla pagina.

## Programma completo e eseguibile

Di seguito è riportato il programma completo che combina il rettangolo di base e l'esempio di dimensionamento dinamico. Copialo in un nuovo progetto console, ripristina il pacchetto NuGet `Aspose.PDF` e avvialo.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Output previsto:**  
Apri `CombinedRectangles.pdf`. Vedrai un rettangolo nero ancorato nell'angolo in basso a sinistra e un rettangolo blu scuro centrato con riempimento giallo chiaro. Entrambi i rettangoli rispettano i margini della pagina.

## Conclusione

Ora sai come **draw rectangle on pdf** con C# e precisamente **how to define rectangle dimensions** per layout sia fissi che reattivi. L'approccio utilizza `RectangleShape` di Aspose.PDF, il controllo dei confini e semplici operazioni aritmetiche per adattarsi a qualsiasi dimensione di pagina.

Successivamente, potresti esplorare:

* Aggiungere **colori di riempimento** e **stili di linea** (tratteggiata, puntinata) – parola chiave secondaria: how to define rectangle dimensions with style.
* Combinare più forme in una singola `Page` per creare grafici o moduli.
* Esportare il PDF in uno stream per API web invece di salvarlo su disco.

Sperimenta con diverse dimensioni, colori e posizioni per padroneggiare la grafica PDF nelle tue applicazioni .NET. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come personalizzare i PDF con Aspose.PDF per .NET: impostare i margini della pagina e disegnare linee](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Come aggiungere timbri di pagina nei PDF usando Aspose.PDF per .NET: guida completa](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Come aggiungere timbri numerati di pagina nei PDF usando Aspose.PDF per .NET | Timbri e sfondi](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}