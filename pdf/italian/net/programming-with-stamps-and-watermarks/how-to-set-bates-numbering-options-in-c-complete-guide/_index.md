---
category: general
date: 2026-08-14
description: Come impostare le opzioni di numerazione Bates in C# usando GroupDocs.
  Segui questo tutorial passo passo per aggiungere prefissi personalizzati e numeri
  di avvio durante la conversione da Word a PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: it
lastmod: 2026-08-14
og_description: Come impostare rapidamente le opzioni di numerazione Bates in C#.
  Questa guida ti mostra come aggiungere prefissi personalizzati e numeri iniziali
  durante la conversione da Word a PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Come impostare le opzioni di numerazione Bates in C# – tutorial passo passo
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Come impostare le opzioni di numerazione Bates in C# – guida completa
url: /it/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare le opzioni di numerazione Bates in C# – guida completa

Se hai bisogno di **come impostare le opzioni di numerazione Bates** in C#, questa guida ti accompagna passo passo. Imparerai a configurare il numero di partenza, aggiungere un prefisso e applicare la numerazione durante la conversione di un documento Word in PDF usando le API GroupDocs.

L'elaborazione dei documenti spesso richiede identificatori univoci su ogni pagina per scopi legali o di archiviazione. Alla fine di questo tutorial avrai uno snippet riutilizzabile da inserire in qualsiasi progetto .NET, sia che tu stia costruendo uno strumento di supporto legale o un generatore di report automatizzato. Non servono strumenti esterni—solo la libreria GroupDocs.Conversion e poche righe di C#.

## Cosa ti serve

Prima di iniziare, assicurati di avere:

* .NET 6.0 SDK o versioni successive installate  
* Visual Studio 2022 (o qualsiasi IDE che supporti .NET)  
* Una licenza valida di GroupDocs.Conversion (la versione di prova gratuita è sufficiente per i test)  
* Un documento Word di esempio (`input.docx`) che desideri numerare  

Questi prerequisiti garantiscono che il codice funzioni senza configurazioni aggiuntive.

## Come impostare le opzioni di numerazione Bates – panoramica

Il cuore di **come impostare le opzioni di numerazione Bates** risiede in tre oggetti:

1. `Document` – carica il file sorgente.  
2. `BatesNumberingOptions` – contiene il numero di partenza, il prefisso e altri dettagli di formattazione.  
3. `AddBatesNumbering` – il metodo che inserisce la numerazione in ogni pagina.

Comprendere perché esiste ciascun elemento ti aiuta ad adattare la soluzione a scenari più complessi, come font personalizzati o numerazione multilingue.

## Passo 1: Installa il pacchetto NuGet GroupDocs.Conversion

Apri un terminale nella cartella della tua soluzione ed esegui:

```bash
dotnet add package GroupDocs.Conversion
```

Le **GroupDocs API** forniscono la classe `Document` e il metodo di estensione `AddBatesNumbering` usati più avanti nel tutorial.

## Passo 2: Carica il documento sorgente

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Perché questo passo?*  
Il caricamento del file crea una rappresentazione in memoria che il motore di conversione può manipolare. Senza un'istanza di `Document` non è possibile applicare la numerazione Bates né altre trasformazioni.

## Passo 3: Crea le opzioni di numerazione Bates

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Perché questo passo?*  
`BatesNumberingOptions` racchiude tutte le impostazioni necessarie quando **si impostano le opzioni di numerazione Bates**. Modificando `StartNumber` e `Prefix` puoi allineare l'output al tuo sistema di gestione dei casi. La proprietà `Position` controlla il posizionamento visivo, spesso requisito di conformità.

## Passo 4: Applica la numerazione Bates al documento

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

Il metodo `AddBatesNumbering` scorre ogni pagina del `Document` caricato e inserisce la stringa configurata. Poiché il metodo opera sulla rappresentazione in memoria, puoi concatenare ulteriori passaggi di elaborazione (ad esempio, l'aggiunta di filigrane) prima del salvataggio.

## Passo 5: Converti e salva il risultato come PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Perché questo passo?*  
Il salvataggio in PDF è un formato finale comune per i documenti legali. L'oggetto `PdfConvertOptions` consente di perfezionare l'output, ma non è obbligatorio per la numerazione di base. La chiamata `Save` scrive il PDF completamente numerato su disco.

## Esempio completo, eseguibile

Mettendo insieme tutti i passaggi, ecco un'applicazione console autonoma che puoi compilare ed eseguire:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Output previsto**

L'esecuzione del programma crea `output.pdf` in cui ogni pagina mostra un'etichetta come `CASE-1000`, `CASE-1001`, ecc., posizionata nel piè di pagina destro. Apri il PDF con qualsiasi visualizzatore per verificare che i numeri compaiano correttamente.

## Problemi comuni e migliori pratiche

| Problema | Perché si verifica | Come evitarlo |
|----------|--------------------|---------------|
| **I percorsi relativi causano `FileNotFoundException`** | La directory di lavoro di un'app console può differire da quella di Visual Studio. | Usa percorsi assoluti o `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **La numerazione si sovrappone ai piè di pagina esistenti** | Se il documento sorgente contiene già contenuti nell'area del piè di pagina scelta, il nuovo numero può rimanere nascosto. | Scegli una `Position` diversa (ad esempio `HeaderLeft`) o modifica il modello di origine. |
| **Documenti di grandi dimensioni risultano lenti** | La numerazione Bates itera su ogni pagina; l'uso di memoria cresce con le dimensioni del file. | Processa il documento a blocchi usando `Document.Split` se superi le 500 pagine. |
| **Scadenza della licenza** | La versione di prova di GroupDocs scade dopo 30 giorni, generando un'eccezione su `AddBatesNumbering`. | Applica una chiave di licenza valida prima di caricare il documento: `License license = new License(); license.SetLicense("license.lic");`. |

**Consiglio professionale:** se ti serve un formato numerico diverso per caso (ad esempio `2023-CASE-001`), genera il prefisso in modo dinamico prima di creare `BatesNumberingOptions`.

## Estendere la soluzione

Lo stesso approccio **Bates numbering C#** funziona con altri formati sorgente come `.txt`, `.html` o anche immagini. Basta cambiare l'estensione del file quando costruisci l'oggetto `Document`, e il motore di conversione gestirà il resto.

Puoi anche combinare **document conversion C#** con OCR per PDF scansionati:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Conclusione

Ora sai **come impostare le opzioni di numerazione Bates** in C# dall'inizio alla fine. Creando un oggetto `BatesNumberingOptions`, applicandolo con `AddBatesNumbering` e salvando il risultato in PDF, puoi automatizzare la produzione di documenti legalmente conformi e univocamente identificati.  

Da qui puoi esplorare argomenti correlati come **C# PDF generation**, **document conversion C#**, o funzionalità avanzate dell'**GroupDocs API** come filigrane e firme digitali. Sperimenta con prefissi, posizioni e formati numerici diversi per adattarli al tuo flusso di lavoro.

Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Aggiungi numerazione Bates PDF in C# – Guida completa](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [Come aggiungere e personalizzare i numeri di pagina nei PDF usando Aspose.PDF per .NET | Guida alla manipolazione dei documenti](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Come aggiungere un piè di pagina con timbro di testo nei PDF usando Aspose.PDF per .NET: Guida passo‑a‑passo](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}