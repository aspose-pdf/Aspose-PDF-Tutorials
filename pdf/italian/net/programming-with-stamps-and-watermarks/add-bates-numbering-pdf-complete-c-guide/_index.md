---
category: general
date: 2026-03-22
description: Aggiungi rapidamente la numerazione Bates a PDF con Aspose.Pdf. Scopri
  come aggiungere Bates, aggiungere numeri di pagina sequenziali, aggiungere un piè
  di pagina personalizzato al PDF e aggiungere un artefatto al PDF in pochi minuti.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: it
og_description: Aggiungi la numerazione Bates a PDF usando Aspose.Pdf. Questa guida
  mostra come aggiungere Bates, aggiungere numeri di pagina sequenziali, aggiungere
  un piè di pagina personalizzato al PDF e aggiungere un artefatto al PDF.
og_title: Aggiungi numerazione Bates a PDF – Tutorial passo passo C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Aggiungi numerazione Bates al PDF – Guida completa C#
url: /it/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere la Numerazione Bates PDF – Guida Completa in C#

Hai mai dovuto **add bates numbering pdf** a un batch di documenti legali ma non sapevi da dove cominciare? Non sei il primo—molti sviluppatori incontrano lo stesso ostacolo quando costruiscono strumenti di gestione dei casi. La buona notizia? Con Aspose.Pdf puoi **add bates**, **add sequential page numbers** e persino **add custom footer pdf** in poche righe di codice.  

In questo tutorial percorreremo l’intero processo, dall’installazione della libreria al salvataggio del file finale, inserendo consigli su come **add artifact to pdf** senza rompere il contenuto esistente. Alla fine avrai uno snippet pronto all’uso da inserire in qualsiasi progetto .NET.

## Cosa Ti Serve

- .NET 6+ (il codice funziona sia su .NET Core che su .NET Framework)  
- Una licenza valida di Aspose.Pdf per .NET (puoi iniziare con una valutazione gratuita)  
- Un PDF di input (`input.pdf`) posizionato in una cartella a cui puoi fare riferimento  
- Visual Studio, Rider o qualsiasi editor C# tu preferisca  

Tutto qui—nessun pacchetto NuGet aggiuntivo oltre a Aspose.Pdf.

## Passo 1: Installa Aspose.Pdf via NuGet

Prima di tutto—portiamo la libreria sulla tua macchina. Apri un terminale nella cartella del progetto ed esegui:

```bash
dotnet add package Aspose.Pdf
```

Oppure, se usi la Console di Gestione Pacchetti di Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*Pro tip:* Dopo l’installazione, verifica che la cartella `Aspose.Pdf` compaia sotto `Dependencies → Packages` nell’esploratore soluzioni.

## Passo 2: Carica il Documento PDF di Origine

Ora creiamo un oggetto `Document` che rappresenta il PDF che vogliamo timbrare. L’uso della dichiarazione `using` garantisce il rilascio automatico del handle del file.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Perché usare `using var`? Garantisce lo smaltimento anche in caso di eccezione, evitando problemi di blocco del file quando poi provi a sovrascrivere lo stesso file.

## Passo 3: Crea e Configura un Artifact di Numerazione Bates

Un numero Bates è essenzialmente un artifact di testo che vive nella struttura logica del PDF. Puoi trattarlo come un **custom footer pdf** perché appare su ogni pagina senza far parte dello stream di contenuto della pagina.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Perché Queste Impostazioni Sono Importanti

- **Prefix**: Utile per distinguere i tipi di documento (es. “INV‑” per fatture).  
- **Start**: Imposta il primo numero; puoi prelevarlo da un database se ti serve continuità tra file.  
- **Format**: `"0000"` forza una visualizzazione a quattro cifre, garantendo l’allineamento quando i numeri crescono.  
- **X/Y**: Le coordinate sono misurate dal angolo in basso a sinistra, quindi `Y = 20` posiziona il testo appena sopra il margine della pagina. Regola `X` se vuoi l’allineamento a sinistra o centrato.

Se ti serve **add sequential page numbers** invece dei numeri Bates, basta omettere `Prefix` e modificare `Format` in `"###"` o qualsiasi altro modello preferisci.

## Passo 4: Applica l’Artifact a Tutte le Pagine

Aspose.Pdf ti permette di collegare un artifact all’intero documento con una singola chiamata. Questo è il modo più efficiente per **add artifact to pdf** senza iterare manualmente su ogni pagina.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Dietro le quinte, Aspose aggiunge l’artifact al dizionario della pagina di ogni pagina, il che significa che la numerazione diventa parte della struttura logica del PDF—perfetta per estrazioni o ricerche successive.

## Passo 5: Salva il PDF Aggiornato

Infine, scrivi le modifiche su disco. Puoi sovrascrivere l’originale o salvare in un nuovo file; quest’ultimo è più sicuro durante lo sviluppo.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Quando apri `output.pdf` in un visualizzatore, vedrai “INV‑1000”, “INV‑1001”, … in basso‑a‑destra di ogni pagina.

### Verifica del Risultato

Apri il PDF in Adobe Acrobat o in qualsiasi visualizzatore e cerca i numeri. Se vuoi confermare programmaticamente, puoi leggere nuovamente l’artifact:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Questa snippet stampa l’etichetta Bates di ogni pagina—utile per test automatizzati.

## Casi Limite & Domande Frequenti

### E se il Mio PDF Ha già un Footer?

Aggiungere un artifact non sovrascrive i footer esistenti perché gli artifact risiedono in un livello separato. Tuttavia, se la sovrapposizione visiva è un problema, modifica la coordinata `Y` o aumenta l’offset `X` per spostare il numero Bates fuori dal modo.

### Posso Usare un Font o un Colore Differente?

Assolutamente. Il `BatesNumberingArtifact` eredita da `Artifact`, quindi puoi impostare `Font`, `FontColor` e persino `Opacity`. Esempio:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Come Resetto il Contatore per un Nuovo Documento?

Basta cambiare `Start` prima di chiamare `AddArtifact`. Se generi molti PDF in un ciclo, mantieni un contatore in corso nella logica della tua applicazione.

### Questo Approccio è Compatibile con PDF Cifrati?

Aspose.Pdf può aprire PDF cifrati se fornisci la password:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Dopo la decrittazione, gli stessi passaggi per aggiungere l’artifact funzionano perfettamente.

## Esempio Completo Funzionante

Di seguito trovi il programma completo, pronto da eseguire. Incollalo in un’app console, regola i percorsi e premi **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Output previsto:** la console stampa “Bates numbering added successfully!” e `output.pdf` contiene etichette sequenziali come `INV‑1000`, `INV‑1001`, ecc., posizionate in basso‑a‑destra di ogni pagina.

## Riepilogo Rapido

- **Obiettivo principale:** **add bates numbering pdf** usando Aspose.Pdf.  
- Abbiamo coperto **how to add bates**, **add sequential page numbers**, e **add custom footer pdf** tramite un unico artifact.  
- Il tutorial ha mostrato come **add artifact to pdf**, gestire i casi limite e verificare il risultato.  

## Cosa Viene Dopo?

- **Prefissi dinamici:** estrai valori da un database per generare “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Posizionamento condizionale:** usa il rilevamento della dimensione della pagina (`page.MediaBox`) per centrare i numeri su pagine in modalità landscape.  
- **Combina con filigrane:** aggiungi un logo semi‑trasparente accanto al numero Bates per il branding.  

Sperimenta pure—potresti scoprire un modo più intelligente per processare migliaia di file in batch. Se incontri problemi, lascia un commento o consulta la documentazione ufficiale di Aspose (è sorprendentemente chiara). Buona programmazione!  

![esempio di aggiunta di numerazione Bates PDF](https://example.com/bates-numbering-screenshot.png "Screenshot che mostra l'aggiunta di numerazione Bates PDF in un visualizzatore PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}