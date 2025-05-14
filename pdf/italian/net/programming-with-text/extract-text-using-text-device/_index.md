---
"description": "Scopri come estrarre il testo da un documento PDF utilizzando il dispositivo di testo in Aspose.PDF per .NET."
"linktitle": "Estrarre il testo utilizzando il dispositivo di testo"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Estrarre il testo utilizzando il dispositivo di testo"
"url": "/it/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre il testo utilizzando il dispositivo di testo

## Introduzione

Estrarre testo da un PDF può essere complicato, soprattutto quando si tratta di documenti con formati diversi, font incorporati o layout complessi. Ma con Aspose.PDF per .NET, questo processo diventa un gioco da ragazzi! Che tu voglia convertire pagine di un PDF in testo normale per ulteriori analisi o semplicemente estrarre sezioni specifiche, Aspose.PDF è la soluzione che fa per te. In questo tutorial, spiegheremo passo dopo passo come estrarre testo da un PDF utilizzando la classe TextDevice in Aspose.PDF. Forniremo anche spiegazioni chiare, così potrai applicare gli stessi metodi ai tuoi progetti con facilità.

## Prerequisiti

Prima di iniziare a scrivere il codice, assicurati di avere tutto a posto per seguire la procedura. Ecco cosa ti servirà:

1. Aspose.PDF per .NET: Scarica l'ultima versione da [Pagina di download di Aspose.PDF per .NET](https://releases.aspose.com/pdf/net/).
2. Ambiente di sviluppo: Visual Studio o qualsiasi altro ambiente di sviluppo C#.
3. .NET Framework: assicurati che il progetto sia destinato a .NET Framework 4.x o versione successiva.
4. File PDF di input: un file PDF che utilizzerai per l'estrazione del testo. Salvalo in una directory sul tuo computer (lo chiameremo `YOUR DOCUMENT DIRECTORY`).

## Importa pacchetti

Nella parte superiore del codice dovrai importare gli spazi dei nomi necessari per lavorare con Aspose.PDF:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## Passaggio 1: carica il documento PDF

Prima di estrarre il testo, dobbiamo caricare il documento PDF in memoria. In questo passaggio, aprirai il PDF utilizzando Aspose.PDF. `Document` classe. Questo ti permetterà di accedere a tutte le pagine e ai contenuti all'interno del file.

```csharp
// Definisci il percorso del tuo documento PDF
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Carica il documento PDF
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Qui stiamo usando `Document pdfDocument = new Document(dataDir + "input.pdf");` per caricare il PDF. Il `dataDir` La variabile contiene il percorso della directory del file PDF. Questo ci darà accesso all'intero documento, permettendoci di scorrere le pagine ed estrarne il contenuto.

## Passaggio 2: impostare uno String Builder per l'archiviazione del testo

Ora che il documento è caricato, abbiamo bisogno di un modo per memorizzare il testo estratto. Per questo, useremo un `StringBuilder` che consente un'efficiente concatenazione di stringhe.

```csharp
// StringBuilder per contenere il testo estratto
StringBuilder builder = new StringBuilder();
```

Inizializziamo un `StringBuilder` istanza, che raccoglierà il testo estratto da ogni pagina. È un modo più efficiente per gestire stringhe di grandi dimensioni rispetto alla normale concatenazione di stringhe in un ciclo.

## Passaggio 3: scorrere le pagine PDF

Successivamente, analizzeremo ogni pagina del documento PDF per estrarne il testo. Elaboreremo ogni pagina singolarmente utilizzando `TextDevice` classe responsabile della conversione del contenuto PDF in formato testo.

```csharp
// Sfoglia tutte le pagine del PDF
foreach (Page pdfPage in pdfDocument.Pages)
{
    // Elaborare ogni pagina per l'estrazione del testo
}
```

Questo ciclo attraversa ogni pagina del PDF (`pdfDocument.Pages`). Per ogni pagina, estrarremo il testo e lo aggiungeremo al nostro `StringBuilder`.

## Passaggio 4: estrarre il testo da ogni pagina

Ora, impostiamo il processo di estrazione del testo per ogni pagina. Qui creeremo un `TextDevice` oggetto e utilizzarlo per elaborare le pagine PDF. L' `TextDevice` estrae testo grezzo o formattato in base alle opzioni di estrazione da noi impostate.

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // Creare un dispositivo di testo per l'estrazione del testo
    TextDevice textDevice = new TextDevice();
    
    // Imposta le opzioni di estrazione del testo in modalità "Pure"
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // Estrarre il testo dalla pagina corrente e salvarlo nel flusso di memoria
    textDevice.Process(pdfPage, textStream);

    // Convertire il flusso di memoria in testo
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // Aggiungi il testo estratto a StringBuilder
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`: IL `TextDevice` La classe viene utilizzata per estrarre il testo dal PDF.
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`: Questa opzione estrae il testo grezzo senza mantenere alcuna formattazione come caratteri o posizioni. Puoi anche usare `TextFormattingMode.Raw` se hai bisogno di un maggiore controllo sulla formattazione.
- `textDevice.Process(pdfPage, textStream);`: Elabora ogni pagina del PDF e memorizza il testo estratto in un `MemoryStream`.
- Infine, convertiamo il testo dal `MemoryStream` a una stringa e aggiungerla a `StringBuilder`.

## Passaggio 5: salva il testo estratto in un file

Dopo aver elaborato tutte le pagine, il testo viene memorizzato nel `StringBuilder`L'ultimo passaggio consiste nel salvare il testo estratto in un file.

```csharp
// Definisci il percorso di output per il file di testo
dataDir = dataDir + "input_Text_Extracted_out.txt";

// Salva il testo estratto in un file
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`: Questo scrive l'intero contenuto del `StringBuilder` in un file di testo.
- Il percorso per il file di output viene impostato aggiungendo un nome file (`"input_Text_Extracted_out.txt"`) al `dataDir` sentiero.

## Conclusione

Estrarre testo da un PDF utilizzando Aspose.PDF per .NET è un processo semplice ed efficiente. Seguendo i passaggi descritti in questa guida, è possibile aprire facilmente documenti PDF, scorrere le pagine ed estrarre testo in un file di testo. Questo è particolarmente utile per l'elaborazione di grandi volumi di dati PDF, l'analisi del testo o la conversione di documenti per ulteriori elaborazioni.

Con Aspose.PDF, non sei limitato all'estrazione di testo: puoi gestire annotazioni, manipolare immagini o persino convertire i PDF in altri formati come HTML o Word. La flessibilità e la potenza di questa libreria la rendono uno strumento prezioso per la gestione dei PDF nelle applicazioni .NET.

## Domande frequenti

### Aspose.PDF può estrarre testo da PDF basati su immagini?
No, Aspose.PDF è progettato per estrarre testo da PDF basati su contenuti. Per i PDF basati su immagini, è necessaria la tecnologia OCR.

### Aspose.PDF mantiene la formattazione durante l'estrazione del testo?
Per impostazione predefinita, il testo viene estratto senza formattazione, ma è possibile modificare le opzioni di estrazione se si desidera mantenere una certa formattazione.

### Posso estrarre il testo da un intervallo di pagine specifico?
Sì, puoi modificare il codice in modo che esegua il ciclo su un intervallo specifico di pagine anziché su tutte le pagine.

### Quali sono le modalità di estrazione del testo in Aspose.PDF?
Aspose.PDF offre due modalità: Raw e Pure. La modalità Raw cerca di mantenere il layout originale, mentre la modalità Pure estrae solo il testo senza formattazione.

### Aspose.PDF per .NET è compatibile con .NET Core?
Sì, Aspose.PDF per .NET è completamente compatibile con .NET Core e .NET Framework.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}