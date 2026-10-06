---
category: general
date: 2026-03-24
description: Crea un documento PDF e impara a impostare la posizione assoluta per
  il testo etichettato. Questo tutorial mostra come aggiungere l'elemento span, come
  aggiungere contenuto etichettato e posizionare il testo nella pagina.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: it
og_description: Crea un documento PDF e vedi subito come impostare la posizione assoluta,
  aggiungere un elemento span e posizionare il testo sulla pagina con contenuto PDF
  taggato.
og_title: Crea documento PDF – Posizionamento assoluto del testo etichettato
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Crea documento PDF – Imposta posizione assoluta per il testo etichettato
url: /it/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea documento PDF – Imposta posizione assoluta per testo taggato

Ti è mai capitato di **creare un documento pdf** che contenga testo accessibile e taggato posizionato esattamente dove desideri? Forse stai creando un PDF simile a un modulo in cui l’etichetta deve trovarsi a una coordinata precisa, oppure stai generando un certificato e il nome deve allinearsi perfettamente con un’immagine di sfondo.  

In questa guida percorreremo un esempio completo e eseguibile che mostra **come aggiungere contenuti taggati**, **impostare la posizione assoluta** e **aggiungere un elemento span** così potrai **posizionare il testo sulla pagina** senza indovinare. Nessun riferimento esterno—solo il codice che puoi copiare‑incollare, più le spiegazioni del “perché” dietro ogni riga.

## Prerequisiti

- .NET 6+ (o .NET Framework 4.6+) con un compilatore C#
- Aspose.Pdf per .NET (ultima versione al momento della scrittura, 23.12) installato tramite NuGet
- Familiarità di base con la sintassi C#

Se li hai, iniziamo.

---

## Crea documento PDF – Impostazione della posizione assoluta

La prima cosa che facciamo è istanziare un `Document` vuoto. Questo oggetto rappresenta l’intero file PDF e ci dà accesso all’albero di contenuti taggati.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Perché è importante:**  
`Document` è la radice della struttura PDF. Creandolo per primo garantiamo che ci sia una tela sia per gli elementi visivi (pagine, grafica) sia per la struttura logica (tag). L’istruzione `using` garantisce che il file venga correttamente rilasciato, evitando perdite di handle del file su Windows.

---

## Abilita contenuto taggato (come aggiungere tag)

Prima di poter inserire elementi taggati, il documento deve essere contrassegnato come *taggato*. Aspose.Pdf crea automaticamente un oggetto `TaggedContent`, ma è comunque necessario attivare il flag.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Cosa succede dietro le quinte?**  
Impostare `TaggedContent` su `true` indica ai lettori PDF che il file contiene un albero di struttura logica. Questo è fondamentale per i lettori di schermo e per il corretto funzionamento del metodo `SetPosition` su un elemento span.

---

## Ottieni l'elemento radice dell'albero di contenuti taggati

L'elemento radice è il punto di ingresso per tutti i tag strutturali (come `<Document>`, `<Section>`, `<Span>`). Pensalo come il “body” invisibile del PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Perché abbiamo bisogno della radice:**  
Tutti i tag successivi devono essere collegati da qualche parte nell'albero; altrimenti non appariranno nella gerarchia di accessibilità.

---

## Aggiungi un elemento Span – Il blocco base per testo in linea

Uno *span* è l'equivalente PDF di un `<span>` HTML—perfetto per brevi pezzi di testo che desideri posizionare con precisione.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Nota di progettazione:**  
Se ti serve una formattazione più ricca (grassetto, corsivo, hyperlink), puoi avvolgere lo span in un `<Paragraph>` o usare oggetti `TextFragment` in seguito. Per il posizionamento assoluto, uno span semplice è il più leggero.

---

## Imposta posizione assoluta – X=100, Y=200

Ecco la parte divertente: posizionare lo span in una posizione esatta sulla pagina. Il sistema di coordinate inizia dall'angolo in basso a sinistra (0,0) e utilizza i punti (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Perché il posizionamento assoluto?**  
Quando hai bisogno di un layout pixel‑perfect—pensa a certificati, fatture o moduli—il flusso relativo (come il testo da sinistra a destra) non è sufficiente. `SetPosition` aggira il flusso di testo normale e fissa l'elemento nella posizione specificata.

---

## Aggiungi testo allo Span

Con lo span posizionato, ora iniettiamo la stringa effettiva.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Suggerimento:**  
Se ti servono caratteri Unicode o script da destra a sinistra, passa semplicemente la stringa; Aspose.Pdf gestisce automaticamente la codifica.

---

## Aggiungi lo Span all'elemento radice

Infine, colleghiamo lo span all’albero logico del documento affinché diventi parte del PDF finale.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Cosa succede se dimentichi questo passaggio?**  
Lo span esisterebbe in memoria ma non verrebbe mai serializzato nel file, quindi non vedresti alcun testo e l’albero di accessibilità sarebbe incompleto.

---

## Esempio completo e eseguibile

Di seguito trovi il programma completo che puoi inserire in un'app console. Crea un PDF di una pagina, aggiunge uno span taggato a (100, 200) e salva il file come `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Output previsto:**  
Apri `TaggedPositioned.pdf` in qualsiasi visualizzatore (Adobe Acrobat, Foxit, ecc.). Vedrai la frase **“Positioned tagged text”** esattamente a 100 pt dal bordo sinistro e 200 pt dal bordo inferiore della pagina. Se ispezioni il pannello *Tags*, un elemento `<Span>` sarà elencato sotto la radice del documento, confermando che il contenuto è correttamente taggato.

---

## Domande comuni e casi particolari

### E se devo posizionare il testo su una pagina specifica diversa dalla prima?

Aggiungi la pagina desiderata (`var page = pdfDocument.Pages[3];`) prima di chiamare `SetPosition`. Lo span si collegherà automaticamente al contesto della pagina attiva.

### Posso impostare la posizione in pollici o centimetri?

`SetPosition` accetta punti. Converti usando le formule:  
- **Pollici → punti:** `points = inches * 72`  
- **Centimetri → punti:** `points = cm * 28.3465`

### Come modifico il font o il colore dello span?

Dopo aver creato lo span, puoi recuperare il suo `TextState` e modificarlo:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### E se il documento ha già dei tag esistenti?

Puoi comunque creare un nuovo span e aggiungerlo a qualsiasi elemento esistente (`rootElement`, un `<Section>` specifico, ecc.). Assicurati solo di mantenere una gerarchia logica—i lettori di schermo si aspettano un albero ben strutturato.

### Funziona con la conformità PDF/A o PDF/UA?

Sì. I PDF taggati sono un requisito fondamentale per PDF/UA. Se ti serve PDF/A, imposta `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` dopo aver costruito il contenuto.

---

## Consigli professionali e insidie

- **Consiglio pro:** Aggiungi sempre una pagina prima di posizionare il contenuto. Senza una pagina, `SetPosition` fallisce silenziosamente perché non c’è dove renderizzare.
- **Attenzione alle unità:** Mescolare pixel da un design UI con punti PDF sposterà il tuo testo. Ricontrolla la conversione.
- **Suggerimento di performance:** Se generi migliaia di PDF, riutilizza una singola istanza di `Document` e chiama `pdfDocument.Pages.Clear()` tra le esecuzioni per evitare un'eccessiva allocazione di memoria.
- **Promemoria di accessibilità:** Il tagging non è solo un optional; molte normative (Section 508, EN 301 549) lo richiedono. Usare `CreateSpanElement` garantisce che il testo sia individuabile dalle tecnologie assistive.

---

## Conclusione

Abbiamo appena **creato un documento pdf** da zero, **impostato la posizione assoluta**, **aggiunto un elemento span**, e dimostrato **come aggiungere contenuti taggati** così puoi **posizionare il testo sulla pagina** con precisione pixel‑perfect. L'esempio completo è pronto per l'esecuzione, e la spiegazione ha coperto sia il *come* sia il *perché*—esattamente ciò che gli sviluppatori (e gli assistenti AI) cercano quando hanno bisogno di una soluzione affidabile.

Successivamente, potresti esplorare:
- Aggiungere immagini dietro il testo posizionato per certificati con filigrana.  
- Usare `CreateParagraphElement` per blocchi multilinea che richiedono ancora posizionamento assoluto.  
- Esportare in PDF/UA per soddisfare audit di accessibilità rigorosi.  

Sentiti libero di modificare le coordinate, i font o i colori—sperimentare è il modo più veloce per padroneggiare la generazione di PDF taggati. Se incontri un problema, lascia un commento qui sotto; buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}