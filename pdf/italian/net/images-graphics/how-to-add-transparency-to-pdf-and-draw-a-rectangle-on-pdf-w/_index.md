---
category: general
date: 2026-09-12
description: Scopri come aggiungere trasparenza a un PDF, disegnare un rettangolo
  su un PDF e salvare il PDF con trasparenza usando Aspose.PDF in C# – guida passo
  passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: it
lastmod: 2026-09-12
og_description: Aggiungi trasparenza al PDF, disegna un rettangolo sul PDF e salva
  il PDF con trasparenza usando Aspose.PDF in C#. Segui questo tutorial completo.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Aggiungi trasparenza al PDF e disegna un rettangolo sul PDF – guida completa
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Come aggiungere trasparenza a un PDF e disegnare un rettangolo su PDF con Aspose.PDF
url: /it/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere trasparenza a PDF e disegnare un rettangolo su PDF con Aspose.PDF

Se hai bisogno di **aggiungere trasparenza a PDF** file, questa guida ti mostra esattamente come farlo in C#. Imparerai anche come **disegnare un rettangolo su PDF** e infine **salvare PDF con trasparenza**, così il risultato potrà essere riutilizzato in report, fatture o qualsiasi flusso di lavoro di automazione dei documenti.

In questo tutorial tu:

* Caricare un documento PDF esistente.
* Creare uno stato grafico personalizzato che definisce l'opacità del contorno e del riempimento.
* Applicare quello stato grafico al canvas e disegnare un rettangolo.
* Salvare il file modificato mantenendo le impostazioni di trasparenza.

Non sono necessari strumenti esterni oltre alla libreria Aspose.PDF per .NET, e ogni riga di codice è spiegata in modo da comprendere *perché* ogni passaggio è importante.

## Prerequisiti

* .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.7+).
* Una copia con licenza o di valutazione di **Aspose.PDF for .NET**. Installala tramite NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Un PDF di input (`input.pdf`) posizionato in una cartella che puoi referenziare dal tuo progetto.

## Passo 1: Caricare il documento PDF

La prima operazione è aprire il file di origine. L'uso dell'istruzione `using` garantisce che il documento venga eliminato correttamente, evitando problemi di blocco del file in seguito quando si tenta di salvare.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Perché è importante*: Caricare il documento ti dà accesso alla collezione di pagine, ai dizionari delle risorse e agli oggetti canvas necessari per il disegno.

## Passo 2: Accedere al dizionario delle risorse della prima pagina

Ogni pagina PDF ha un **resource dictionary** che memorizza oggetti come font, immagini e stati grafici. Per introdurre una nuova impostazione di trasparenza dobbiamo modificare la voce `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Perché è importante*: Il `DictionaryEditor` ci permette di leggere e modificare oggetti PDF a basso livello senza rompere la struttura del documento.

## Passo 3: Creare uno stato grafico personalizzato con valori di trasparenza

Uno stato grafico (`ExtGState`) controlla come vengono renderizzate le operazioni di disegno. Definiamo due parametri di opacità:

* **CA** – opacità del contorno (il bordo delle forme).
* **ca** – opacità del riempimento (l'interno delle forme).

Impostiamo inoltre il blend mode (`BM`) su “Normal”, che è l'operazione di composizione più comune.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Perché è importante*: Aggiungendo `GS0` al dizionario `ExtGState` creiamo un riferimento riutilizzabile che il canvas può attivare prima del disegno. L'opacità di riempimento di `0.5` rende il rettangolo semi‑trasparente, raggiungendo l'obiettivo di **add transparency to PDF**.

## Passo 4: Applicare lo stato grafico e disegnare un rettangolo

Ora indichiamo al canvas della pagina di utilizzare lo stato grafico appena creato, quindi disegniamo un rettangolo. Le coordinate seguono il sistema di coordinate PDF (origine nell'angolo inferiore sinistro).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Perché è importante*: `SetGraphicsState("GS0")` cambia il contesto di disegno alle impostazioni di trasparenza definite in precedenza. Il metodo `Rectangle` definisce la forma, e `Stroke` rende il contorno con l'opacità specificata. Se desideri anche un rettangolo riempito, sostituisci `Stroke()` con `FillAndStroke()`.

## Passo 5: Salvare il PDF modificato mantenendo la trasparenza

Infine, scrivi il documento nuovamente su disco. Il file di output contiene il nuovo stato grafico, il rettangolo disegnato e le informazioni di trasparenza.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Perché è importante*: Salvare il documento finalizza tutte le modifiche. Il file risultante può essere aperto in qualsiasi visualizzatore PDF, e il rettangolo apparirà con un'opacità di riempimento del 50 %.

### Risultato atteso

Quando apri `output_with_extgstate.pdf` dovresti vedere un rettangolo il cui bordo è completamente opaco e il cui interno è semi‑trasparente, consentendo al contenuto della pagina sottostante di intravedersi.

## Casi limite e consigli pratici

| Situazione | Regolazione consigliata |
|-----------|------------------------|
| **Pagine multiple** | Itera su `pdfDocument.Pages` e ripeti i passi 2‑4 per ogni pagina di destinazione. |
| **Valori di opacità diversi** | Modifica i valori `CosPdfNumber` per `CA` (contorno) e `ca` (riempimento) a qualsiasi numero compreso tra `0` (completamente trasparente) e `1` (completamente opaco). |
| **Modalità di fusione personalizzate** | Sostituisci `"Normal"` con `"Multiply"`, `"Screen"` o qualsiasi modalità di fusione PDF‑standard supportata dal tuo visualizzatore. |
| **Rettangolo riempito** | Chiama `canvas.FillAndStroke()` invece di `canvas.Stroke()` per applicare sia il riempimento che il contorno. |
| **Riutilizzare lo stesso stato grafico** | Puoi chiamare `canvas.SetGraphicsState("GS0")` prima di disegnare un numero qualsiasi di forme sulla stessa pagina. |

**Consiglio professionale:** Ispeziona sempre il dizionario delle risorse dopo aver aggiunto un nuovo `ExtGState`. Se il dizionario non esiste, crealo prima:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Esempio completo, eseguibile

Di seguito è riportato un programma autonomo che puoi copiare in un'applicazione console e eseguire immediatamente (sostituisci `YOUR_DIRECTORY` con un percorso reale).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Eseguendo il programma si genera `output_with_extgstate.pdf`, che dimostra **add transparency to PDF**, **draw rectangle on PDF** e **save PDF with transparency** tutti in un unico flusso.

## Conclusione

Ora sai come **add transparency to PDF** file, **draw rectangle on PDF** e **save PDF with transparency** usando Aspose.PDF per .NET. Il processo ruota attorno alla creazione di un `ExtGState` personalizzato, alla sua applicazione al canvas e al salvataggio delle modifiche. Con questi blocchi di costruzione puoi estendere la tecnica ad altre forme, più pagine o valori di opacità dinamici.

**Passi successivi**

* Esplora altri primitivi di disegno come `canvas.Ellipse`, `canvas.Path` o `canvas.TextFragment` riutilizzando lo stesso stato grafico.
* Combina la trasparenza con sovrapposizioni di immagini per creare filigrane (`canvas.Image` + `ExtGState` personalizzato).
* Consulta la documentazione di Aspose.PDF sui **graphics state parameters** per effetti di composizione avanzati.

Buona programmazione e goditi la flessibilità visiva che la trasparenza porta ai tuoi flussi di lavoro PDF!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}