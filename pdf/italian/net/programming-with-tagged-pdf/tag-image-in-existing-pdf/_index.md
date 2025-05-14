---
"description": "Scopri come taggare le immagini nei PDF esistenti utilizzando Aspose.PDF per .NET. Guida passo passo per migliorare l'accessibilità con la conformità PDF/UA."
"linktitle": "Tagga l'immagine nel PDF esistente"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Tagga l'immagine nel PDF esistente"
"url": "/it/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tagga l'immagine nel PDF esistente

## Introduzione

In questo tutorial, ti guideremo attraverso l'aggiunta di tag a un'immagine in un PDF esistente utilizzando Aspose.PDF per .NET. Al termine di questa guida, sarai in grado di impostare testo alternativo per le immagini, modificare gli attributi di layout e garantire che il tuo PDF sia conforme agli standard di accessibilità.

## Prerequisiti

Prima di iniziare, vediamo cosa ti servirà per iniziare:

- Aspose.PDF per .NET: assicurati di aver scaricato e installato la versione più recente di Aspose.PDF per .NET. [Scarica qui](https://releases.aspose.com/pdf/net/).
- .NET Framework: assicurati di aver configurato un ambiente di sviluppo .NET come Visual Studio.
- Nozioni di base sulla struttura del PDF: familiarità con gli elementi della struttura del PDF quali paragrafi, intervalli, tabelle e immagini.
- Una licenza valida: puoi acquistare una licenza [Qui](https://purchase.aspose.com/buy) o usarne uno temporaneo [Qui](https://purchase.aspose.com/temporary-license/).

## Importa pacchetti

Per iniziare a programmare, è necessario importare gli spazi dei nomi essenziali da Aspose.PDF per .NET. Questi forniranno accesso alle classi e ai metodi necessari per manipolare il documento PDF.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ora che abbiamo impostato la situazione, scomponiamo il processo di taggatura di un'immagine in più passaggi.

## Passaggio 1: caricare il documento PDF esistente

Il primo passo è caricare il file PDF con cui si desidera lavorare. Può essere qualsiasi file PDF contenente un'immagine a cui si desidera aggiungere tag.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// Apri il documento
Document document = new Document(inFile);
```

- Sostituire `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo del file.
- IL `Document` La classe ti permette di caricare un PDF esistente. Modificherai questo PDF per taggare l'immagine.

## Passaggio 2: accedere al contenuto taggato e all'elemento della struttura radice

Una volta aperto il PDF, il passo successivo è accedere al contenuto taggato e identificare l'elemento della struttura radice. Questo è fondamentale perché consente di navigare tra gli elementi del PDF e apportare modifiche.

```csharp
// Ottieni contenuto taggato ed elemento della struttura radice
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` fornisce accesso agli elementi strutturati nel PDF.
- IL `RootElement` è l'elemento strutturale più in alto, dal quale è possibile passare ad altri elementi come paragrafi, tabelle e immagini.

## Passaggio 3: imposta il titolo per il documento PDF con tag

L'aggiunta di un titolo al documento PDF taggato garantisce che il documento sia etichettato correttamente, il che è utile per l'accessibilità e la conformità PDF/UA.

```csharp
// Imposta il titolo per il documento PDF taggato
taggedContent.SetTitle("Document with images");
```

- Impostando un titolo per il PDF taggato si migliora l'accessibilità e si rende più chiaro il documento per gli screen reader e le tecnologie assistive.

## Passaggio 4: trova e tagga l'immagine

Ora, troviamo l'elemento immagine (chiamato `FigureElement` in Aspose.PDF), impostare un testo alternativo e configurare gli attributi di layout.

```csharp
// Passa attraverso tutti gli elementi della figura (immagini) e imposta il testo alternativo e gli attributi di layout
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // Imposta testo alternativo per la figura
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // Crea e imposta l'attributo BBox (riquadro di delimitazione)
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // Imposta gli attributi di layout per la figura
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- Questo codice esegue un ciclo attraverso tutti i `FigureElement` oggetti nella struttura radice, che rappresentano immagini.
- Imposta il testo alternativo per l'accessibilità (gli screen reader lo useranno per descrivere l'immagine).
- Il riquadro di delimitazione (`BBox`) specifica le coordinate per il layout dell'immagine, assicurando che venga visualizzata correttamente nel documento.

## Passaggio 5: modificare gli elementi Span all'interno della tabella

In alcuni casi, potrebbe essere necessario modificare gli elementi span all'interno di una tabella. Qui mostreremo come trovare un `SpanElement` e spostarlo in un paragrafo.

```csharp
// Trova gli elementi della tabella, dello span e del paragrafo
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// Sposta l'elemento span nel paragrafo
spanElement.ChangeParentElement(paragraph);
```

- Qui, localizziamo il `TableElement`, `SpanElement`, E `ParagraphElement` all'interno del PDF.
- Utilizzando il `ChangeParentElement` metodo, spostiamo l'intervallo nel paragrafo per garantire la corretta etichettatura e struttura.

## Passaggio 6: salvare il documento e convalidare la conformità PDF/UA

Una volta apportate tutte le modifiche, il passaggio finale consiste nel salvare il PDF aggiornato e verificare se è conforme agli standard PDF/UA.

```csharp
// Salva il documento PDF aggiornato
document.Save(outFile);

// Convalida la conformità PDF/UA
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- IL `Validate` Il metodo controlla il documento PDF rispetto agli standard PDF/UA e registra i risultati.
- Garantire la conformità aiuta a migliorare l'accessibilità e a soddisfare i requisiti normativi per la pubblicazione dei documenti.

## Conclusione

In questo tutorial, vi abbiamo mostrato come taggare le immagini in un PDF esistente utilizzando Aspose.PDF per .NET. Impostando il testo alternativo, modificando gli attributi di layout e convalidando il documento per la conformità PDF/UA, potete garantire che i vostri PDF siano accessibili e rispettino gli standard moderni. Aspose.PDF semplifica l'utilizzo di elementi strutturati, offrendovi il controllo sul layout e sull'accessibilità del documento.

## Domande frequenti

### A cosa serve Aspose.PDF per .NET?
Aspose.PDF per .NET è una potente libreria utilizzata per creare, modificare e manipolare documenti PDF a livello di programmazione in un ambiente .NET.

### Come posso garantire la conformità PDF/UA?
Puoi usare Aspose.PDF `Validate` Metodo per verificare la conformità PDF/UA dopo aver apportato modifiche al documento.

### Cos'è il testo alternativo nei PDF?
Il testo alternativo è una descrizione aggiunta alle immagini nei PDF per migliorarne l'accessibilità, soprattutto per gli utenti che utilizzano lettori di schermo.

### Posso manipolare tabelle e intervalli in un PDF con Aspose.PDF?
Sì, Aspose.PDF consente di manipolare tabelle, intervalli e altri elementi strutturati all'interno di un documento PDF.

### Dove posso scaricare Aspose.PDF per .NET?
Puoi scaricare l'ultima versione di Aspose.PDF per .NET [Qui](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}