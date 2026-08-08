---
category: general
date: 2026-05-27
description: Aggiungi numerazione Bates a PDF usando Aspose.Pdf in C#. Scopri come
  aggiungere rapidamente la numerazione Bates, personalizzare il formato e automatizzare
  l’etichettatura dei documenti legali.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: it
og_description: Aggiungi la numerazione Bates a PDF con Aspose.Pdf in C#. Questa guida
  mostra come aggiungere la numerazione Bates, configurare i prefissi e salvare il
  risultato.
og_title: Aggiungi la numerazione Bates a PDF in C# – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Aggiungi la numerazione Bates ai PDF in C# – Guida completa
url: /it/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere numerazione Bates a PDF in C# – Guida completa

Ti sei mai chiesto **come aggiungere la numerazione Bates** a un PDF senza passare ore a usare strumenti manuali? Non sei solo: i team legali, gli auditor e gli specialisti di e‑discovery hanno tutti bisogno di un modo affidabile per **aggiungere numerazione Bates PDF** ai file in modo programmatico.  

In questo tutorial percorreremo una soluzione concisa, end‑to‑end, usando Aspose.Pdf per .NET, così potrai inserire i numeri Bates su qualsiasi documento con poche righe di codice C#.

## Cosa imparerai

- Come aprire un PDF esistente con Aspose.Pdf  
- Come creare un artefatto di numerazione Bates e perfezionarne il formato  
- Come collegare l'artefatto a ogni pagina (o solo alla prima)  
- Come salvare il file aggiornato e verificarne il risultato  

Non è necessaria alcuna esperienza pregressa con Aspose—basta una conoscenza di base di C# e .NET. Alla fine avrai uno snippet riutilizzabile da copiare‑incollare in qualsiasi progetto.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7+)  
- Pacchetto NuGet Aspose.Pdf per .NET (`Install-Package Aspose.Pdf`)  
- Un file PDF di origine che desideri etichettare (posizionalo in una cartella a cui puoi fare riferimento)

> **Consiglio:** Se non hai ancora una licenza, Aspose offre una chiave temporanea gratuita che rimuove le filigrane di valutazione.

## Passo 1 – Aprire il documento PDF di origine  

Per prima cosa abbiamo bisogno di un oggetto `Document` che rappresenti il file su disco. Pensalo come il caricamento di una tela vuota su cui dipingeremo i numeri Bates.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Perché è importante:** Aprire il documento all'interno di un blocco `using` garantisce che tutte le risorse non gestite vengano rilasciate tempestivamente, cosa particolarmente importante per PDF di grandi dimensioni.

## Passo 2 – Creare un artefatto di numerazione Bates  

Un *BatesNumberingArtifact* è il modo di Aspose per descrivere come devono apparire i numeri. Puoi impostare un prefisso, il numero iniziale, l'incremento e persino una stringa di formato personalizzata.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Perché potresti modificare questi valori:**  
- **Prefix** è utile per ID di caso (“CASE‑”, “DOC‑”).  
- **StartNumber** ti consente di continuare una serie precedente.  
- **Increment** può essere impostato a 2 se ti serve una numerazione dispari/pari.  
- **Format** supporta qualsiasi formato composito .NET; `{0:D5}` garantisce cinque cifre con zeri iniziali.

## Passo 3 – Collegare l'artefatto alle pagine desiderate  

Puoi aggiungere l'artefatto a una singola pagina, a un intervallo o all'intero documento. Per la maggior parte dei flussi di lavoro legali lo colleghiamo a *tutte* le pagine, ma l'esempio qui sotto mostra il caso minimo—l'aggiunta alla prima pagina.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Se devi coprire tutte le pagine, itera su di esse:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Perché questo passo è cruciale:** Gli artefatti vengono renderizzati *dopo* il contenuto della pagina, quindi i numeri appaiono sopra il testo esistente senza alterare il layout originale.

## Passo 4 – Salvare il PDF modificato  

Infine, scrivi le modifiche su disco. Puoi sovrascrivere l'originale o creare un nuovo file—qui genereremo una copia fresca chiamata `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Quando apri `bates.pdf` vedrai “ABC01000” (o qualunque formato tu abbia scelto) stampato nella posizione predefinita—di solito nell'angolo in basso a destra.

## Esempio completo funzionante  

Mettendo tutto insieme, ecco il programma completo che puoi compilare ed eseguire:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Output previsto

Quando esegui il programma, la console stampa:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Aprendo `bates.pdf` vedrai il prefisso “ABC” seguito da una sequenza a cinque cifre con zeri iniziali su ogni pagina—esattamente quello che il codice è stato scritto per fare.

## Domande frequenti e casi particolari

### Posso posizionare il numero Bates altrove?

Sì. Usa la proprietà `Location` del `BatesNumberingArtifact` (ad es., `Location = new Position(10, 10)`) per posizionare il numero a coordinate X/Y personalizzate. Puoi anche impostare `HorizontalAlignment` e `VerticalAlignment` per un controllo più fine.

### E se il mio PDF ha migliaia di pagine?

Aspose.Pdf gestisce lo streaming delle pagine in modo efficiente, ma è comunque consigliabile elaborare in batch se incontri limiti di memoria. La classe `Document` supporta anche `PdfConverter` per salvataggi incrementali.

### Come cambio il font o il colore?

Avvolgi l'artefatto in un oggetto `TextState`:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### È necessaria una licenza per l'uso in produzione?

Una versione con licenza rimuove le filigrane di valutazione e sblocca le prestazioni complete. La versione di prova gratuita è sufficiente per test e proof‑of‑concept.

## Verifica – Controllo visivo rapido  

Se preferisci una verifica automatizzata, Aspose può estrarre il testo di una pagina e confermare la presenza del prefisso:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Eseguendo questo dopo il passo di salvataggio verrà stampato `Bates number verified.` se tutto è andato a buon fine.

## Conclusione  

Ora sai **come aggiungere numerazione Bates PDF** usando Aspose.Pdf in C#. Dall'apertura del documento alla configurazione dell'artefatto, dal collegamento alle pagine al salvataggio del risultato, il processo è lineare e completamente scriptabile.  

Passi successivi? Prova a sperimentare con:

- Valori `Prefix` diversi per più lotti di casi  
- `Location` e `TextState` personalizzati per il branding  
- Aggiunta di prefissi specifici per pagina (ad es., “VOL‑1‑”, “VOL‑2‑”) modificando `StartNumber` ad ogni iterazione del ciclo  

Queste modifiche ti permettono di adattare la soluzione a quasi qualsiasi flusso di lavoro legale o di archiviazione.  

Hai altre domande su **come aggiungere numerazione Bates** per PDF multilingua o file criptati? Lascia un commento qui sotto, e buona programmazione!

## Tutorial correlati

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Different Headers in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}