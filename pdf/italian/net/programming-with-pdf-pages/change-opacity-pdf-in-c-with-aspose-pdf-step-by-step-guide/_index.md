---
category: general
date: 2026-08-11
description: Modifica l'opacità di un PDF usando Aspose.Pdf in C#. Scopri come aggiungere
  trasparenza alle pagine PDF, impostare lo stato grafico e salvare rapidamente il
  risultato.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change opacity PDF
- how to add transparency
- add pdf transparency
language: it
lastmod: 2026-08-11
og_description: Modifica l'opacità di un PDF con Aspose.Pdf in C#. Segui questa guida
  per vedere come aggiungere trasparenza a qualsiasi documento PDF, personalizzare
  gli stati grafici e esportare il risultato.
og_image_alt: Screenshot illustrating change opacity PDF example in C# code
og_title: Modifica l'opacità di un PDF in C# – tutorial completo su Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  headline: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  name: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
    text: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
  - name: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
    text: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
  - name: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
    text: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
  - name: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
    text: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Modifica l'opacità di un PDF in C# con Aspose.Pdf – guida passo‑passo
url: /it/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifica l'opacità PDF in C# con Aspose.Pdf – guida passo‑passo

Se hai bisogno di **cambiare l'opacità PDF** dei file in modo programmatico, questo tutorial ti mostra esattamente come fare. Utilizzando Aspose.Pdf per .NET puoi controllare la trasparenza degli oggetti grafici, del testo e delle immagini senza uscire dal tuo codice C#.

Nelle sezioni seguenti imparerai **come aggiungere trasparenza** a una pagina PDF, cosa significano gli oggetti di stato grafico sottostanti e come salvare il documento modificato. La guida copre anche le difficoltà comuni quando **aggiungi trasparenza PDF** e offre consigli per scenari reali.

## Cosa otterrai

* Caricare un documento PDF esistente.
* Creare un nuovo dizionario di stato grafico che definisce i valori di opacità.
* Inserire lo stato grafico nel dizionario delle risorse della pagina.
* Salvare il documento con l'effetto **cambio opacità PDF** aggiornato.

Non sono necessari strumenti esterni—solo la libreria Aspose.Pdf per .NET (versione 23.10 o successiva) e un ambiente di sviluppo .NET.

## Prerequisiti

* .NET 6.0 (o .NET Framework 4.7.2+) installato.
* Visual Studio 2022 o qualsiasi IDE compatibile con C#.
* Un riferimento al pacchetto NuGet `Aspose.Pdf`.
* Un file PDF di input (`input.pdf`) situato in una directory scrivibile.

> **Suggerimento:** Quando testi le modifiche di opacità, lavora con un PDF che contiene già grafica vettoriale o testo; le immagini raster ignorano i parametri `ca` e `CA` a meno che non siano inserite all'interno di un gruppo di trasparenza.

## Modifica l'opacità PDF con Aspose.Pdf

Il fulcro della soluzione è modificare il dizionario **ExtGState** (stato grafico esterno) di una pagina. Questo dizionario memorizza parametri come **ca** (opacità del tratto) e **CA** (opacità del riempimento). Aggiungendo una nuova voce è possibile fare riferimento ad essa successivamente nei flussi di contenuto.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;

class ChangeOpacityPdfExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        using (var document = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 2: Access the first page and its resource dictionary
            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Step 3: Create a new graphics state dictionary with desired opacity values
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                // Fill opacity (CA) – 1.0 means fully opaque
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                // Stroke opacity (ca) – 0.5 makes lines semi‑transparent
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                // Blend mode (BM) – Normal is the default blend mode
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // Step 4: Add the new graphics state to the ExtGState dictionary
            // “GS0” is the identifier you will reference later in the content stream
            extGState.Add("GS0", newGraphicsState);

            // Optional: Demonstrate usage by drawing a semi‑transparent rectangle
            // This part shows how the new graphics state affects drawing commands.
            var canvas = new Aspose.Pdf.Drawing.Graphic(page);
            canvas.SetGraphicsState("GS0"); // Apply the opacity settings
            canvas.Rectangle(100, 500, 200, 600);
            canvas.FillColor = Color.FromRgb(255, 0, 0); // Red fill
            canvas.StrokeColor = Color.FromRgb(0, 0, 255); // Blue border
            canvas.Draw();

            // Step 5: Save the modified PDF
            document.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF saved with changed opacity.");
    }
}
```

### Perché funziona

* **ExtGState** è una risorsa PDF che memorizza parametri grafici riutilizzabili. Aggiungendo una voce personalizzata (`GS0`) crei una configurazione di opacità riutilizzabile.
* La chiave **ca** controlla l'opacità delle operazioni di tratto (linee, bordi). La chiave **CA** controlla le operazioni di riempimento (forme colorate, testo). Impostando `ca = 0.5` i tratti diventano trasparenti al 50 %, mentre `CA = 1` mantiene i riempimenti completamente opachi.
* La chiamata `SetGraphicsState("GS0")` indica ad Aspose.Pdf di emettere l'operatore `/GS0 gs` nel flusso di contenuto, attivando le nuove impostazioni di trasparenza per tutti i comandi di disegno successivi.

## Come aggiungere trasparenza al contenuto esistente

Se hai già testo o immagini sulla pagina e vuoi renderli semi‑trasparenti senza ridisegnarli, puoi inserire un operatore **gs** prima del contenuto esistente. Il frammento seguente dimostra come anteporre l'operatore al flusso di contenuto della pagina.

```csharp
// Retrieve the existing content stream
var content = page.Contents[1];
var originalBytes = content.ToByteArray();

// Build the new content with the graphics state applied
var gsOperator = System.Text.Encoding.ASCII.GetBytes("/GS0 gs\n");
var newBytes = new List<byte>(gsOperator);
newBytes.AddRange(originalBytes);

// Replace the page content
page.Contents[1].Replace(newBytes.ToArray());
```

### Casi limite e considerazioni

| Situazione | Gestione consigliata |
|------------|----------------------|
| **Pagine multiple** | Itera su `document.Pages` e ripeti i passaggi 2‑4 per ogni pagina che desideri modificare. |
| **Opacità diversa per elemento** | Crea stati grafici aggiuntivi (`GS1`, `GS2`, …) con valori `ca`/`CA` distinti e applicali in modo selettivo. |
| **PDF con voci ExtGState esistenti** | Usa `dictEditor["ExtGState"]` in modo sicuro; se la chiave non esiste, crea un nuovo `CosPdfDictionary` e assegnalo a `page.Resources`. |
| **Gruppi di trasparenza** | Per composizioni complesse (ad es., immagini sovrapposte), imposta il dizionario `/Group` con `S /Transparency` e `CS /DeviceRGB`. Questo va oltre il semplice **cambio opacità PDF**, ma può essere necessario per layout avanzati. |

## Aggiungi trasparenza PDF alla grafica vettoriale

Oltre ai rettangoli, puoi applicare lo stesso stato grafico a qualsiasi disegno vettoriale—linee, curve o anche testo. Ecco un rapido esempio che scrive testo semi‑trasparente:

```csharp
var textFragment = new TextFragment("Transparent text")
{
    Position = new Position(100, 400),
    TextState = { FontSize = 36, ForegroundColor = Color.Black }
};
page.Paragraphs.Add(textFragment);

// Apply the graphics state to the text fragment
textFragment.TextState.GraphicsState = "GS0";
```

La proprietà `GraphicsState` di `TextState` indica al motore PDF di renderizzare il testo usando l'opacità definita in `GS0`. Questo è il modo più semplice per **aggiungere trasparenza PDF** al contenuto testuale.

## Problemi comuni quando si modifica l'opacità PDF

1. **Dizionario ExtGState mancante** – Alcuni PDF non contengono una voce `ExtGState` di default. In tal caso, creane uno:  
   ```csharp
   if (!dictEditor.ContainsKey("ExtGState"))
       dictEditor.Add("ExtGState", new CosPdfDictionary(document));
   ```
2. **Nome risorsa errato** – Il nome che usi in `SetGraphicsState` deve corrispondere esattamente alla chiave aggiunta (`GS0`). Un errore di battitura porta al rendering predefinito, completamente opaco.
3. **Sovrascrittura di stati grafici esistenti** – Aggiungere una nuova voce non sostituisce quelle esistenti. Se riutilizzi un nome già presente, potresti alterare involontariamente altri elementi della pagina che lo referenziano.
4. **Compatibilità del visualizzatore** – I visualizzatori PDF più vecchi (pre‑1.4) potrebbero ignorare la trasparenza. Assicurati che il tuo pubblico utilizzi un visualizzatore moderno come Adobe Reader DC o il visualizzatore PDF integrato di Chrome.

## Esempio completo funzionante

Di seguito trovi il programma completo e autonomo che puoi copiare, incollare ed eseguire. Include tutte le direttive `using` necessarie, la gestione degli errori e i commenti.



## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiungere un timbro di testo a PDF usando Aspose.PDF .NET: Guida completa](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Come aggiungere timbri di pagina nei PDF usando Aspose.PDF per .NET: Guida completa](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Come aggiungere timbri di pagina nei PDF usando Aspose.PDF per .NET | Guida a filigrane e sfondi](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}