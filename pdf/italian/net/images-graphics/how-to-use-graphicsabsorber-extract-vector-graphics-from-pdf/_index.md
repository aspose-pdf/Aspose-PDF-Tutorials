---
category: general
date: 2026-06-27
description: Come utilizzare GraphicsAbsorber per estrarre grafica vettoriale da file
  PDF. Impara passo passo l'estrazione di grafica con Aspose.Pdf per ottenere un output
  SVG pulito.
draft: false
keywords:
- how to use graphicsabsorber
- extract vector graphics pdf
- how to extract pdf vectors
- aspose pdf graphics extraction
language: it
og_description: Come utilizzare GraphicsAbsorber per estrarre file PDF con grafica
  vettoriale. Questo tutorial ti guida attraverso l'estrazione di grafica con Aspose.Pdf,
  fornendo il codice completo.
og_title: Come utilizzare GraphicsAbsorber – Guida completa ad Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to use GraphicsAbsorber to extract vector graphics PDF files. Learn
    step‑by‑step Aspose.Pdf graphics extraction for clean SVG output.
  headline: How to Use GraphicsAbsorber – Extract Vector Graphics from PDF with Aspose.Pdf
  type: TechArticle
- description: How to use GraphicsAbsorber to extract vector graphics PDF files. Learn
    step‑by‑step Aspose.Pdf graphics extraction for clean SVG output.
  name: How to Use GraphicsAbsorber – Extract Vector Graphics from PDF with Aspose.Pdf
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code works with .NET Core, .NET Framework, and
      .NET 5+). - A valid Aspose.Pdf for .NET license (or a free evaluation key).
      - Basic C# knowledge—no advanced graphics expertise required. - The PDF you
      want to analyze (we’ll use `vector.pdf` as an example).'
  - name: – Load the PDF Document
    text: Before you can extract anything, you need an in‑memory representation of
      the file. Using `using var` ensures the document is disposed automatically,
      which is especially handy in long‑running services.
  - name: – Create a GraphicsAbsorber to Capture Vector Objects
    text: '`GraphicsAbsorber` is a specialized collector that walks through the PDF
      content stream and gathers every drawing operator (lines, curves, shapes, etc.).
      Think of it as a net you throw over the page to catch all vector pieces.'
  - name: – Apply the Absorber to the Desired Page
    text: You can run the absorber on a single page or loop through the whole document.
      Here we focus on the first page for simplicity.
  - name: – Iterate Through Extracted Elements and Display Their Details
    text: Now the fun part—reading the data. Each element tells you which page it
      came from, the number of operators (i.e., drawing commands), and its position
      within the page.
  - name: 'Advanced: Extracting Vectors from All Pages'
    text: 'If you need to **extract vector graphics PDF** files across an entire document,
      just wrap the `Visit` call in a loop:'
  - name: Exporting Extracted Vectors to SVG (Optional)
    text: Aspose.Pdf can render the captured vectors directly to SVG, which is handy
      when you want a web‑ready format.
  - name: Next Steps
    text: '- Dive deeper into **aspose pdf graphics extraction** by exploring `GraphicsAbsorber`’s
      `Operators` collection for fine‑grained path data. - Combine the extracted coordinates
      with a custom SVG builder if you need more control than the built‑in `SvgSaveOptions`.
      - Experiment with rasterizing specific'
  type: HowTo
- questions:
  - answer: '`GraphicsAbsorber.Elements` will be empty; the loop simply skips output.
      No error is thrown.'
    question: What if a page has no vectors?
  - answer: Yes. Set `graphicsAbsorber.OperatorsFilter` to an array of `OperatorType`
      values (e.g., `OperatorType.Path`, `OperatorType.Stroke`). This reduces noise
      when you only care about paths.
    question: Can I filter only certain operator types?
  - answer: Using `using var` ensures each `Document` and `GraphicsAbsorber` is disposed
      promptly. For massive files, process pages one at a time as shown to keep the
      footprint low.
    question: Is the extractor memory‑intensive for large PDFs?
  - answer: 'Load the document with a password: `new Document("file.pdf", new LoadOptions
      { Password = "secret" })`.'
    question: Does this work with encrypted PDFs?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- VectorGraphics
title: Come utilizzare GraphicsAbsorber – Estrarre grafica vettoriale da PDF con Aspose.Pdf
url: /it/net/images-graphics/how-to-use-graphicsabsorber-extract-vector-graphics-from-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare GraphicsAbsorber – Estrarre grafica vettoriale da PDF con Aspose.Pdf

Ti sei mai chiesto **come usare GraphicsAbsorber** quando devi estrarre forme vettoriali da un PDF? Non sei l’unico. Che tu stia costruendo una pipeline design‑to‑code o abbia semplicemente bisogno di SVG puliti per un progetto web, estrarre grafica vettoriale da file PDF può sembrare una ricerca dell’ago in un pagliaio.  

In questa guida ti mostreremo una soluzione concisa, pronta all’uso, che utilizza `GraphicsAbsorber` di Aspose.Pdf. Alla fine saprai esattamente **come estrarre vettori PDF**, vedrai le loro coordinate e avrai una solida base per ulteriori elaborazioni.

## Cosa imparerai

- Caricare un documento PDF con Aspose.Pdf.
- Creare e configurare un `GraphicsAbsorber`.
- Applicare l’assorbitore a una pagina specifica.
- Iterare sugli elementi estratti e leggere i loro dettagli.
- Consigli per gestire PDF multi‑pagina ed esportare in SVG.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona con .NET Core, .NET Framework e .NET 5+).
- Una licenza valida di Aspose.Pdf per .NET (o una chiave di valutazione gratuita).
- Conoscenze di base di C#—non è necessario essere esperti di grafica.
- Il PDF che vuoi analizzare (useremo `vector.pdf` come esempio).

> **Pro tip:** Se non hai ancora una licenza, prendi una chiave temporanea dal sito di Aspose; l’API funziona allo stesso modo durante la valutazione.

<img src="graphicsabsorber-diagram.png" alt="how to use graphicsabsorber diagram" style="max-width:100%;">

## Come utilizzare GraphicsAbsorber – Guida passo‑passo

Di seguito suddividiamo il processo in quattro passaggi logici. Ogni passaggio contiene un breve snippet di codice, una spiegazione del **perché** è importante e un rapido suggerimento per evitare gli errori più comuni.

### Passo 1 – Caricare il documento PDF

Prima di poter estrarre qualcosa, è necessaria una rappresentazione in memoria del file. L’uso di `using var` garantisce che il documento venga smaltito automaticamente, cosa particolarmente utile in servizi a lunga esecuzione.

```csharp
using Aspose.Pdf;
using System;

// Step 1: Load the PDF document
using var document = new Document("YOUR_DIRECTORY/vector.pdf");

// Verify the document loaded correctly
Console.WriteLine($"Document loaded: {document.Pages.Count} page(s) found.");
```

**Perché questo passaggio?**  
`Document` è il punto di ingresso per tutte le operazioni di Aspose.Pdf. Caricarlo una sola volta e riutilizzare l’istanza mantiene basso l’utilizzo di memoria ed evita I/O ripetuti.

### Passo 2 – Creare un GraphicsAbsorber per catturare gli oggetti vettoriali

`GraphicsAbsorber` è un raccoglitore specializzato che percorre lo stream di contenuto del PDF e raccoglie ogni operatore di disegno (linee, curve, forme, ecc.). Pensalo come una rete che lanci sulla pagina per catturare tutti i pezzi vettoriali.

```csharp
using Aspose.Pdf.Vector;

// Step 2: Initialize the GraphicsAbsorber
using var graphicsAbsorber = new GraphicsAbsorber();

// Optional: filter by specific operator types (e.g., only paths)
// graphicsAbsorber.OperatorsFilter = new[] { OperatorType.Path };
```

**Perché questo passaggio?**  
Senza l’assorbitore dovresti analizzare manualmente il contenuto grezzo del PDF—un compito arduo. L’assorbitore astrae questa complessità e ti fornisce una collezione pulita di elementi vettoriali.

### Passo 3 – Applicare l’assorbitore alla pagina desiderata

Puoi eseguire l’assorbitore su una singola pagina o ciclarlo su tutto il documento. Qui ci concentriamo sulla prima pagina per semplicità.

```csharp
// Step 3: Apply the absorber to page 1
graphicsAbsorber.Visit(document.Pages[1]);

Console.WriteLine($"Absorber visited page {document.Pages[1].Number}.");
```

**Perché questo passaggio?**  
`Visit` percorre lo stream di contenuto della pagina fornita e riempie `graphicsAbsorber.Elements`. Se lo salti, la collezione rimane vuota e non estrarrai alcun vettore.

### Passo 4 – Iterare sugli elementi estratti e visualizzare i loro dettagli

Ora la parte divertente—leggere i dati. Ogni elemento indica da quale pagina proviene, il numero di operatori (cioè i comandi di disegno) e la sua posizione nella pagina.

```csharp
// Step 4: Enumerate extracted graphics elements
foreach (var element in graphicsAbsorber.Elements)
{
    Console.WriteLine(
        $"Page {element.SourcePage.Number}: {element.Operators.Count} operators at ({element.Position.X:F2}, {element.Position.Y:F2})");
}
```

**Perché questo passaggio?**  
Vedere il conteggio degli operatori e le coordinate ti aiuta a decidere se un elemento è una linea, una forma o un percorso complesso. Puoi anche alimentare questi dati a strumenti a valle (ad es., generatori SVG).

### Avanzato: Estrarre vettori da tutte le pagine

Se devi **estrarre grafica vettoriale PDF** da un intero documento, avvolgi semplicemente la chiamata `Visit` in un ciclo:

```csharp
foreach (var page in document.Pages)
{
    graphicsAbsorber.Visit(page);
    foreach (var element in graphicsAbsorber.Elements)
    {
        Console.WriteLine(
            $"[Page {page.Number}] {element.Operators.Count} ops at ({element.Position.X:F2},{element.Position.Y:F2})");
    }
    // Clear elements before moving to the next page
    graphicsAbsorber.Elements.Clear();
}
```

**Perché svuotare la collezione?**  
`GraphicsAbsorber.Elements` conserva i dati delle pagine precedenti. Svuotarla evita duplicati e mantiene prevedibile il consumo di memoria.

### Esportare i vettori estratti in SVG (opzionale)

Aspose.Pdf può renderizzare i vettori catturati direttamente in SVG, utile quando vuoi un formato pronto per il web.

```csharp
using Aspose.Pdf.Saving;

// After visiting a page...
var svgSaveOptions = new SvgSaveOptions
{
    PageIndex = 0, // zero‑based index of the page we just visited
    PageCount = 1
};

document.Save("output_page1.svg", svgSaveOptions);
Console.WriteLine("Page saved as SVG.");
```

**Perché esportare?**  
SVG conserva la scalabilità dei vettori, rendendo l’output ideale per design responsivi o per ulteriori modifiche in strumenti come Inkscape.

## Esempio completo funzionante

Copia il codice qui sotto in un nuovo progetto console (`dotnet new console`) ed eseguilo. Dimostra **come usare GraphicsAbsorber**, **estrarre grafica vettoriale PDF** e stampa diagnostica utile.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Vector;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF
        using var document = new Document("YOUR_DIRECTORY/vector.pdf");
        Console.WriteLine($"Loaded PDF with {document.Pages.Count} page(s).");

        // 2️⃣ Create the absorber
        using var absorber = new GraphicsAbsorber();

        // 3️⃣ Visit each page (you can target a single page if you prefer)
        foreach (var page in document.Pages)
        {
            absorber.Visit(page);

            // 4️⃣ Output element details
            foreach (var element in absorber.Elements)
            {
                Console.WriteLine(
                    $"Page {element.SourcePage.Number}: {element.Operators.Count} operators at ({element.Position.X:F2},{element.Position.Y:F2})");
            }

            // Optional: export the page to SVG
            var svgOptions = new SvgSaveOptions
            {
                PageIndex = page.Number - 1,
                PageCount = 1
            };
            document.Save($"page_{page.Number}.svg", svgOptions);
            Console.WriteLine($"Exported page {page.Number} to SVG.");

            // Reset for next iteration
            absorber.Elements.Clear();
        }

        Console.WriteLine("Extraction complete.");
    }
}
```

**Output previsto (esempio):**

```
Loaded PDF with 3 page(s).
Page 1: 42 operators at (72.00,540.00)
Exported page 1 to SVG.
Page 2: 15 operators at (72.00,720.00)
Exported page 2 to SVG.
Page 3: 0 operators at (0.00,0.00)
Exported page 3 to SVG.
Extraction complete.
```

I numeri varieranno in base al contenuto reale di `vector.pdf`, ma dovresti vedere una riga per ogni elemento vettoriale e un file SVG corrispondente per pagina.

## Domande frequenti e casi particolari

- **E se una pagina non contiene vettori?**  
  `GraphicsAbsorber.Elements` sarà vuoto; il ciclo semplicemente non produce output. Nessun errore viene lanciato.

- **Posso filtrare solo certi tipi di operatori?**  
  Sì. Imposta `graphicsAbsorber.OperatorsFilter` su un array di valori `OperatorType` (ad es., `OperatorType.Path`, `OperatorType.Stroke`). Questo riduce il rumore quando ti interessano solo i percorsi.

- **L’estrattore è intensivo in memoria per PDF grandi?**  
  L’uso di `using var` garantisce che ogni `Document` e `GraphicsAbsorber` vengano smaltiti prontamente. Per file molto grandi, elabora le pagine una alla volta come mostrato per mantenere un footprint ridotto.

- **Funziona con PDF criptati?**  
  Carica il documento con una password: `new Document("file.pdf", new LoadOptions { Password = "secret" })`.

## Riepilogo

Abbiamo percorso **come usare GraphicsAbsorber** per **estrarre grafica vettoriale PDF**, esaminato lo scopo di ogni passaggio e fornito un esempio completo e eseguibile. Ora hai una solida base per **estrarre vettori PDF** usando Aspose.Pdf e puoi estendere la logica per esportare SVG, filtrare operatori o integrarla in pipeline grafiche a valle.

### Prossimi passi

- Approfondisci **l’estrazione grafica con Aspose.Pdf** esplorando la collezione `Operators` di `GraphicsAbsorber` per dati di percorso più dettagliati.
- Combina le coordinate estratte con un costruttore SVG personalizzato se hai bisogno di più controllo rispetto alle opzioni predefinite `SvgSaveOptions`.
- Sperimenta la rasterizzazione di vettori specifici, usando `Rasterizer` in combinazione con l’assorbitore.

Hai un PDF complesso o un caso d’uso particolare? Lascia un commento qui sotto e risolviamo insieme. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci alternativi nei tuoi progetti.

- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [How to Extract Watermarks from PDFs Using Aspose.PDF .NET&#58; A Step-by-Step Guide](/pdf/english/net/watermarks-backgrounds/extract-pdf-watermarks-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}