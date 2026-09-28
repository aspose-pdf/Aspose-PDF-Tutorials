---
category: general
date: 2026-02-25
description: Tutorial sulla numerazione Bates – impara come aggiungere numeri di pagina
  PDF e applicare una numerazione Bates personalizzata usando Aspose.Pdf in C#. Guida
  passo‑passo con codice completo.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: it
og_description: Il tutorial sulla numerazione Bates ti mostra come aggiungere numeri
  di pagina PDF e la numerazione Bates personalizzata in C#. Codice completo, spiegazioni
  e consigli.
og_title: Tutorial di numerazione Bates – Aggiungi numeri Bates ai PDF con C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Tutorial di numerazione Bates: aggiungi numeri Bates ai PDF con C#'
url: /it/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial di numerazione Bates – Aggiungere numeri Bates ai PDF in C#

Ti sei mai chiesto come aggiungere numeri di pagina a un PDF includendo anche un numero Bates in stile legale? Non sei l'unico. In questo **bates numbering tutorial** ti guideremo passo passo su come timbrare ogni pagina di un PDF con un prefisso personalizzato, zeri iniziali e posizionamento preciso—utilizzando Aspose.Pdf per .NET.

La buona notizia? È piuttosto semplice una volta compresi i concetti di base. Alla fine di questa guida avrai un programma eseguibile che prende *input.pdf* e genera *bates_out.pdf* con un’etichetta “ABC‑01000” su ogni pagina. Immergiamoci.

## Cosa ti serve

- **Aspose.Pdf per .NET** (versione 23.10 o successiva). La libreria è commerciale, ma una prova gratuita è più che sufficiente per imparare.
- .NET 6+ SDK (qualsiasi versione recente va bene).
- Un ambiente di sviluppo C# di base—Visual Studio, VS Code o Rider.
- Un PDF di input su cui sperimentare (qualsiasi documento multi‑pagina servirà a illustrare l’effetto).

Non sono necessari pacchetti NuGet aggiuntivi oltre ad Aspose.Pdf, e il codice funziona su Windows, Linux o macOS senza modifiche.

## Passo 1: Caricare il documento PDF sorgente (bates numbering tutorial – initialization)

Per prima cosa creiamo un oggetto `Document` che rappresenta il PDF da modificare. Pensalo come il caricamento di una tela vuota su cui puoi disegnare.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Perché è importante:** Senza caricare il file non c’è nulla da annotare. Il controllo di integrità evita un fallimento silenzioso più avanti quando provi ad aggiungere artefatti a una collezione di pagine inesistente.

## Passo 2: Definire l'artefatto di numerazione Bates (how to add bates)

Un *BatesNumberingArtifact* indica ad Aspose dove e come disegnare l’identificatore. Puoi controllare il prefisso, il numero di partenza, il padding con zeri, la dimensione del font e le coordinate X/Y esatte.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Perché è importante:** La proprietà `LeadingZeros` garantisce che ogni etichetta abbia la stessa lunghezza, fondamentale per i documenti legali dove l’allineamento è cruciale. Regola `X` e `Y` per spostare il timbro in alto‑a‑destra, in basso‑a‑sinistra o dove il tuo flusso di lavoro lo richiede.

## Passo 3: Collegare l'artefatto a ogni pagina (add page numbers pdf)

Ora cicliamo su ogni pagina e aggiungiamo lo stesso artefatto. È qui che il requisito *add page numbers pdf* viene soddisfatto—ogni pagina ottiene automaticamente la sua etichetta sequenziale.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Perché è importante:** Aggiungendo l'artefatto alla collezione `Artifacts` invece di disegnare il testo manualmente, lasciamo ad Aspose la gestione della logica di numerazione, degli zeri iniziali e del rendering. Questo riduce i bug e mantiene il codice conciso.

## Passo 4: Salvare il PDF modificato (add bates numbering)

Infine, persiniamo le modifiche in un nuovo file. È buona pratica scrivere con un nome diverso così da mantenere intatto l’originale.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Perché è importante:** Il metodo `Save` scrive l’intero PDF, incorporando gli artefatti nello stream di contenuto della pagina. Il file risultante può essere aperto con qualsiasi visualizzatore PDF e mostrerà i numeri Bates esattamente come specificato.

## Esempio completo funzionante (Tutti i passaggi combinati)

Di seguito trovi il programma completo, pronto per l’esecuzione. Copialo in un progetto console, sostituisci i percorsi segnaposto e premi **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Risultato atteso

Apri *bates_out.pdf* con Adobe Reader, Foxit o qualsiasi altro visualizzatore. Dovresti vedere un’etichetta tipo **ABC‑01000** sulla prima pagina, **ABC‑01001** sulla seconda, e così via, posizionata a 50 pt dal bordo sinistro e 30 pt dal bordo inferiore. I numeri sono allineati a destra grazie agli zeri iniziali, conferendo al documento un aspetto pulito e professionale.

## Varianti comuni & casi limite

| Scenario | Come regolare |
|----------|---------------|
| **Prefisso diverso** | Cambia `Prefix = "XYZ"` nella definizione dell'artefatto. |
| **Inizio da un numero personalizzato** | Imposta `Start = 5000` (o qualsiasi intero). |
| **Posizionare il numero nell'angolo in alto‑a‑destra** | Usa `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Modificare la dimensione del font per documenti più grandi** | Cambia `FontSize = 12` (o qualsiasi valore). |
| **Aggiungere un rettangolo di sfondo** | Crea un `RectangleArtifact` e aggiungilo prima del `BatesNumberingArtifact`. |
| **Saltare alcune pagine** | All’interno del ciclo `foreach`, aggiungi `if (page.Number % 2 == 0) continue;` per saltare le pagine pari. |

**Consiglio pro:** Prova sempre prima con un PDF breve. È più veloce verificare il posizionamento prima di eseguire lo script su un file di 200 pagine.

## Domande frequenti

- **Funziona con PDF criptati?**  
  Aspose.Pdf può aprire file protetti da password se fornisci la password tramite `Document(string, string)`. L'artefatto Bates verrà comunque applicato dopo la decrittazione.

- **Posso aggiungere sia numeri Bates che numeri di pagina tradizionali?**  
  Sì. Aggiungi un `PageNumberArtifact` accanto al `BatesNumberingArtifact`. Ogni artefatto mantiene il proprio contatore.

- **Cosa succede se il mio PDF ha pagine di dimensioni diverse?**  
  I valori di `Position` sono punti assoluti. Per documenti a pagine miste, calcola la posizione per pagina all’interno del ciclo usando `page.PageInfo.Width` e `page.PageInfo.Height`.

## Prossimi passi & argomenti correlati

Ora che hai padroneggiato il **bates numbering tutorial**, potresti voler approfondire:

- **Aggiungere filigrane** – approccio artefatto simile con `TextArtifact`.
- **Unire più PDF** – usa `Document.AppendDocument`.
- **Estrarre testo per indicizzazione** – classe `TextAbsorber`.
- **Automatizzare l'elaborazione batch** – cicla su una cartella di PDF e applica lo stesso artefatto.

Tutti questi argomenti si basano sugli stessi concetti appena appresi, quindi sei pronto a espandere il tuo toolkit di automazione PDF.

---

*Buona programmazione! Se incontri difficoltà o hai idee per ulteriori personalizzazioni, lascia un commento qui sotto. Il mondo della manipolazione PDF è vasto, ma con un solido **bates numbering tutorial** sotto la cintura, sei già un passo avanti.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}