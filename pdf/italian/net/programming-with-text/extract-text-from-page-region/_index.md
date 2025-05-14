---
"description": "Scopri come estrarre il testo da un'area specifica di un PDF utilizzando Aspose.PDF per .NET con questa guida passo passo. Raccogli e salva il testo dai tuoi documenti in modo efficiente."
"linktitle": "Estrarre il testo dall'area della pagina nel file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Estrarre il testo dall'area della pagina nel file PDF"
"url": "/it/net/programming-with-text/extract-text-from-page-region/"
"weight": 190
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre il testo dall'area della pagina nel file PDF

## Introduzione

Lavorare con i PDF spesso richiede l'estrazione di contenuti specifici, che si tratti di dati da moduli, tabelle o specifiche sezioni di un documento. In questo tutorial, spiegheremo come estrarre testo da una specifica area di un PDF utilizzando Aspose.PDF per .NET. Invece di setacciare un intero documento, individueremo esattamente dove risiede il testo e lo estrarremo in modo efficiente.

## Prerequisiti

Prima di passare al codice, assicurati di avere a disposizione i seguenti elementi:

1. Aspose.PDF per .NET: se non l'hai ancora fatto, scarica e installa la libreria Aspose.PDF per .NET. [Scarica Aspose.PDF per .NET](https://releases.aspose.com/pdf/net/).
2. IDE: qualsiasi ambiente di sviluppo .NET come Visual Studio.
3. .NET Framework: assicurati che il progetto sia configurato con il framework .NET appropriato.
4. Documento PDF: un PDF di esempio da cui estrarremo il testo.

Non dimenticare che puoi [ottenere una prova gratuita](https://releases.aspose.com/) di Aspose.PDF o utilizzare un [licenza temporanea](https://purchase.aspose.com/temporary-license/) per la piena funzionalità.

## Importazione dei pacchetti necessari

Per iniziare a lavorare con Aspose.PDF per .NET, è necessario importare gli spazi dei nomi richiesti nel progetto. Questi pacchetti forniscono le classi e i metodi necessari per la gestione dei documenti PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## Passaggio 1: impostazione della directory dei documenti e caricamento del PDF

Il primo passo è specificare dove si trova il file PDF e caricarlo nel progetto. Puoi utilizzare un percorso di directory locale per il file PDF con cui desideri lavorare.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Apri il documento PDF
Document pdfDocument = new Document(dataDir + "ExtractTextAll.pdf");
```

Questo passaggio garantisce che il file PDF sia caricato correttamente e pronto per essere elaborato. `Document` La classe della libreria Aspose.PDF consente di manipolare il file PDF.

## Passaggio 2: inizializzare l'assorbitore di testo per l'estrazione

In questo passaggio creiamo un `TextAbsorber` oggetto, progettato per estrarre il testo da un documento PDF. L' `TextAbsorber` è flessibile e può essere personalizzato per concentrarsi su regioni o pagine specifiche.

```csharp
// Crea un oggetto TextAbsorber per estrarre il testo
TextAbsorber absorber = new TextAbsorber();
```

IL `TextAbsorber` class è uno strumento potente che cattura tutto il testo entro i limiti specificati.

## Passaggio 3: definire la regione da cui estrarre il testo

Ed è qui che avviene la magia. Invece di estrarre il testo dall'intera pagina, possiamo limitarne l'estrazione a una specifica area rettangolare. Questa è la soluzione perfetta quando si sa esattamente dove si trova il contenuto.

```csharp
// Limita l'estrazione del testo a una regione specifica
absorber.TextSearchOptions.LimitToPageBounds = true;
absorber.TextSearchOptions.Rectangle = new Aspose.Pdf.Rectangle(100, 200, 250, 350);
```

IL `Rectangle` L'oggetto consente di definire le coordinate (in punti) dell'area da cui verrà estratto il testo. L' `TextSearchOptions.LimitToPageBounds` assicura che venga estratto solo il testo all'interno del rettangolo specificato.

## Passaggio 4: accettare l'assorbitore sulla pagina desiderata

Dopo aver impostato la regione, il passo successivo è accettare l' `TextAbsorber` per la pagina specifica da cui si desidera estrarre il testo. Qui ci concentreremo sulla prima pagina del PDF.

```csharp
// Accetta l'assorbitore per la prima pagina
pdfDocument.Pages[1].Accept(absorber);
```

Chiamando il `Accept` nella pagina, insegniamo ad Aspose.PDF a eseguire l'assorbitore e a raccogliere il testo dall'area definita.

## Passaggio 5: recuperare e archiviare il testo estratto

Una volta che l'assorbitore ha svolto il suo lavoro, è il momento di raccogliere il testo estratto e salvarlo. Questo passaggio prevede il recupero del testo e la sua scrittura su un `.txt` file.

```csharp
// Ottieni il testo estratto
string extractedText = absorber.Text;

// Crea uno scrittore per salvare il testo estratto
TextWriter tw = new StreamWriter(dataDir + "extracted-text.txt");

// Scrivi il testo nel file
tw.WriteLine(extractedText);

// Chiudere il flusso
tw.Close();
```

Qui, il `TextWriter` La classe viene utilizzata per scrivere il testo estratto in un file di testo. Questo garantisce che il contenuto estratto venga archiviato in modo sicuro per un utilizzo successivo.

## Conclusione

Estrarre testo da un'area specifica di un documento PDF può essere incredibilmente utile, soprattutto quando si ha a che fare con contenuti strutturati come moduli o tabelle. Utilizzando Aspose.PDF per .NET, è possibile eseguire questa operazione con poche righe di codice. Definendo un'area, inizializzando un `TextAbsorber`e salvando il testo estratto, avrai il pieno controllo su ciò che verrà estratto dal tuo PDF.

Che tu stia lavorando a un piccolo progetto o gestendo documenti di grandi dimensioni, questo metodo fornisce un modo efficiente per estrarre dati rilevanti dai tuoi PDF senza dover esaminare l'intero documento.

## Domande frequenti

### Posso estrarre il testo da più pagine contemporaneamente?
Sì, iterando attraverso il `Pages` raccolta di `pdfDocument`, puoi applicare il `TextAbsorber` su più pagine.

### Cosa succede se il testo si trova in un'area diversa del PDF?
Puoi facilmente regolare il `Rectangle` coordinate che corrispondano alla regione in cui si trova il testo.

### Funziona con i PDF scansionati?
No, i PDF scansionati necessitano dell'OCR (riconoscimento ottico dei caratteri) per convertire le immagini in testo. Anche Aspose.PDF offre funzionalità OCR.

### Esiste un modo per estrarre il testo in base a parole chiave specifiche?
Sì, puoi usare `TextFragmentAbsorber` per l'estrazione di testo basata su parole chiave.

### Come faccio a estrarre il testo da un PDF crittografato?
Per prima cosa dovrai decifrare il PDF inserendo la password corretta, per poi procedere con l'estrazione del testo.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}