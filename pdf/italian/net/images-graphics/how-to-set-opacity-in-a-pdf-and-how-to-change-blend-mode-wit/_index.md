---
category: general
date: 2026-11-19
description: Scopri come impostare l'opacità e come cambiare la modalità di fusione
  in un PDF usando Aspose.Pdf. Guida passo‑passo in C# per grafica trasparente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set opacity
- how to change blend
- Aspose.Pdf graphics state
- PDF transparency C#
- modify PDF resources
language: it
lastmod: 2026-11-19
og_description: Come impostare l'opacità e cambiare la modalità di fusione in un PDF
  usando Aspose.Pdf. Segui questo tutorial completo in C# per rendere trasparenti
  le grafiche.
og_image_alt: Code editor showing C# example that sets PDF opacity and blend mode
og_title: Come impostare l'opacità e cambiare la modalità di fusione in un PDF con
  Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to set opacity and how to change blend mode in a PDF using
    Aspose.Pdf. Step‑by‑step C# guide for transparent graphics.
  headline: How to set opacity in a PDF and how to change blend mode with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Come impostare l'opacità in un PDF e come cambiare la modalità di fusione con
  Aspose.Pdf
url: /it/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare l'opacità e come cambiare la modalità di fusione in un PDF con Aspose.Pdf

Se hai bisogno di **come impostare l'opacità** per gli oggetti all'interno di un PDF, questa guida mostra i passaggi esatti. Copre anche **come cambiare la modalità di fusione** in modo che il nuovo stato grafico si fonda correttamente con il contenuto della pagina.

In questo tutorial imparerai a:

* Caricare un PDF esistente con Aspose.Pdf.
* Accedere al dizionario delle risorse della pagina.
* Creare un nuovo dizionario di stato grafico che definisce l'opacità del tratto, l'opacità di riempimento e la modalità di fusione.
* Aggiungere lo stato grafico alla collezione `ExtGState`.
* Salvare il PDF aggiornato.

Non sono necessari strumenti esterni: basta la libreria Aspose.Pdf per .NET e un ambiente di sviluppo .NET.

## Prerequisiti

* .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+).
* Pacchetto NuGet Aspose.Pdf per .NET (`Install-Package Aspose.Pdf`).
* Un file PDF denominato `input.pdf` situato in una cartella scrivibile (sostituisci `YOUR_DIRECTORY` con il percorso reale).

## Step 1: Install Aspose.Pdf and set up the project

Crea un nuovo progetto console e aggiungi il riferimento a Aspose.Pdf:

```bash
dotnet new console -n PdfOpacityDemo
cd PdfOpacityDemo
dotnet add package Aspose.Pdf
```

Il file di progetto ora include l'assembly Aspose.Pdf, che fornisce le classi `Document`, `DictionaryEditor` e `CosPdfDictionary` utilizzate più avanti.

## Step 2: Load the PDF document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

// Load the existing PDF
Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

**Perché è importante:** Il caricamento del documento crea una rappresentazione in memoria che puoi modificare. Senza questo passaggio i dizionari delle risorse non sono accessibili.

## Step 3: Get the first page and its resource dictionary

```csharp
// Retrieve the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Open the page’s resource dictionary for editing
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);
```

**Spiegazione:** Il dizionario `Resources` contiene oggetti come font, immagini e la collezione `ExtGState`. Modificarlo ti consente di inserire nuovi stati grafici che controllano opacità e fusione.

## Step 4: Access (or create) the ExtGState dictionary

```csharp
// Try to get the existing ExtGState dictionary; create it if missing
CosPdfDictionary extGStateDict = null;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and add it to resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourceEditor["ExtGState"] = extGStateDict;
}
```

**Perché è necessario questo passaggio:** L'elemento `ExtGState` contiene gli oggetti di stato grafico. Se non esiste, devi crearlo prima di aggiungere nuove voci.

## Step 5: Create a new graphics state with opacity and blend mode

```csharp
// Create a new empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Set stroke opacity (CA) – 1 = fully opaque, 0 = fully transparent
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Set fill opacity (ca) – 0.5 = 50 % transparent fill
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Set blend mode (BM) – "Normal" is the default; other options: Multiply, Screen, Overlay, etc.
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**Come risolve il problema:**  
* `CA` controlla l'opacità dei percorsi tracciati (ad es., linee).  
* `ca` controlla l'opacità delle forme riempite (ad es., rettangoli).  
* `BM` definisce come i nuovi grafici vengono compositi con il contenuto esistente della pagina. Cambiare la modalità di fusione è esattamente **come cambiare la fusione** per il PDF.

## Step 6: Register the graphics state in the ExtGState collection

```csharp
// Use a unique key for the new graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

Ora la pagina può fare riferimento a questo stato grafico tramite il nome `/GS0`. Qualsiasi stream di contenuto che imposta `/GS0 gs` utilizzerà l'opacità e la modalità di fusione definite.

## Step 7: Apply the graphics state to existing content (optional)

Se desideri modificare i comandi di disegno esistenti, puoi anteporre l'operatore di stato grafico allo stream di contenuto della pagina:

```csharp
// Retrieve the content stream as a string
string pageContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string modifiedContent = "GS0 gs\n" + pageContent;

// Replace the original content
firstPage.Contents[1].Replace(modifiedContent);
```

**Nota:** Questo passaggio è opzionale. Se aggiungi nuovi comandi di disegno in seguito, basta iniziare lo stream con `GS0 gs`.

## Step 8: Save the modified PDF

```csharp
pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");
```

Il file `out.pdf` risultante contiene uno stato grafico in cui l'opacità di riempimento è al 50 % e la modalità di fusione è `Normal`. Qualsiasi contenuto che utilizza `/GS0 gs` verrà renderizzato con la trasparenza specificata.

## Full working example

Di seguito trovi il programma completo che puoi copiare‑incollare in `Program.cs` ed eseguire:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

class Program
{
    static void Main()
    {
        // 1. Load the PDF document
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get the first page and its resource dictionary
        Page firstPage = pdfDocument.Pages[1];
        DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

        // 3. Access or create the ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourceEditor["ExtGState"] = extGStateDict;
        }

        // 4. Define a new graphics state with opacity and blend mode
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity (fully opaque)
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity (50 % transparent)
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode (Normal)

        // 5. Add the graphics state to ExtGState collection
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Apply the graphics state to existing page content
        if (firstPage.Contents.Count > 0)
        {
            string original = firstPage.Contents[1].ToString();
            string withGs = "GS0 gs\n" + original;
            firstPage.Contents[1].Replace(withGs);
        }

        // 7. Save the updated PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");

        Console.WriteLine("PDF updated successfully – opacity set and blend mode changed.");
    }
}
```

### Expected output

L'esecuzione del programma stampa:

```
PDF updated successfully – opacity set and blend mode changed.
```

Quando apri `out.pdf` in un visualizzatore PDF, qualsiasi forma che utilizza lo stato grafico appena definito apparirà con il 50 % di trasparenza di riempimento mentre i tratti rimarranno completamente opachi. La modalità di fusione `Normal` garantisce che i grafici siano compositi senza effetti speciali. Puoi cambiare `"Normal"` in `"Multiply"` o `"Screen"` per vedere **come cambiare la fusione** per risultati visivi diversi.

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| **Posso impostare valori di opacità diversi per più oggetti?** | Sì. Crea stati grafici aggiuntivi (ad es., `GS1`, `GS2`) con valori `ca`/`CA` differenti e fai riferimento al nome appropriato prima di disegnare ciascun oggetto. |
| **E se il PDF contiene già una voce `ExtGState` denominata `GS0`?** | Scegli una chiave univoca (`GS1`, `MyOpacityState`, ecc.) oppure sovrascrivi la voce esistente se la vecchia definizione non è più necessaria. |
| **La modalità di fusione è limitata a `Normal`?** | No. I nomi validi includono `Multiply`, `Screen`, `Overlay`, `Darken`, `Lighten`, `ColorDodge`, `ColorBurn`, `HardLight`, `SoftLight`, `Difference`, `Exclusion`, e `Hue`, `Saturation`, `Color`, `Luminosity`. |
| **Funziona con PDF criptati?** | Aspose.Pdf può aprire PDF criptati se fornisci la password tramite `Document(string, LoadOptions)`. La manipolazione dello stato grafico funziona allo stesso modo dopo la decrittazione. |
| **Le modifiche influenzeranno tutte le pagine?** | L'esempio modifica solo la prima pagina. Per influenzare tutte le pagine, itera su `pdfDocument.Pages` e ripeti i passaggi 2‑6 per ciascuna pagina. |

## Pro tips

* **Riutilizza gli stati grafici:** Aggiungere uno stato grafico una sola volta e fare riferimento ad esso su più pagine riduce le dimensioni del file.
* **Performance:** Modificare PDF di grandi dimensioni in memoria può richiedere molta RAM. Usa `pdfDocument.Save(..., SaveOptions)` con aggiornamento incrementale se ti servono solo piccole modifiche.
* **Test delle modalità di fusione:** Non tutti i visualizzatori PDF rendono identicamente ogni modalità di fusione. Verifica l'output in Adobe Acrobat Reader e in un visualizzatore alternativo (ad es., Foxit) per assicurarti della coerenza visiva.

## Conclusion

Ora sai **come impostare l'opacità** e **come cambiare la modalità di fusione** in un PDF usando Aspose.Pdf per .NET. Modificando il dizionario `ExtGState` ottieni un controllo granulare su trasparenza e composizione, consentendo grafiche PDF di livello professionale senza strumenti esterni.

Successivamente, potresti approfondire:

* Aggiungere immagini con sfondi trasparenti (**come impostare l'opacità** sulle immagini).
* Creare stream di contenuto riutilizzabili che fanno riferimento al nuovo stato grafico.
* Utilizzare altre modalità di fusione (**come cambiare la fusione** in `Multiply` o `Screen`) per effetti creativi.

Buona programmazione e divertiti a rendere i tuoi PDF più dinamici dal punto di vista visivo!

## What Should You Learn Next?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Change Opacity in PDF with Aspose.PDF – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-change-opacity-in-pdf-with-aspose-pdf-complete-guide/)
- [How to change opacity in a PDF with Aspose.Pdf for .NET](/pdf/english/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/)
- [How to change PDF transparency using Aspose.Pdf in C#](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}