---
"description": "Scopri come impostare un nome di font predefinito per il rendering di PDF in immagini utilizzando Aspose.PDF per .NET. Questa guida illustra i prerequisiti, le istruzioni dettagliate e le domande frequenti."
"linktitle": "Imposta il nome del font predefinito"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Imposta il nome del font predefinito"
"url": "/it/net/document-conversion/set-default-font-name/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Imposta il nome del font predefinito

## Introduzione

Hai mai provato a convertire un documento PDF in un'immagine ma hai scoperto che i font non sono corretti? Forse il testo appare distorto o il font originale non è supportato. È qui che impostare un font predefinito può essere la soluzione! Utilizzando Aspose.PDF per .NET, puoi facilmente impostare un font predefinito per il rendering del tuo PDF, garantendo un aspetto nitido e professionale. In questo tutorial, ti guideremo attraverso l'impostazione del nome del font predefinito durante il rendering di un PDF in un'immagine. Al termine di questa guida, avrai le competenze necessarie per affrontare qualsiasi sfida di rendering PDF che ti si presenterà. Pronto? Iniziamo!

## Prerequisiti

Prima di passare al codice, ecco alcune cose che devi sapere:

- Aspose.PDF per .NET: questa potente libreria è quella che useremo per manipolare il nostro documento PDF. Puoi scaricarla da [Sito web di Aspose](https://releases.aspose.com/pdf/net/).
- Visual Studio: assicurati di avere Visual Studio installato sul tuo computer. Questo sarà il nostro ambiente di sviluppo.
- .NET Framework: assicurati di aver installato .NET Framework. Aspose.PDF per .NET supporta diverse versioni, quindi consulta la documentazione per trovare quella più adatta alle tue esigenze.
- Un documento PDF: avrai bisogno di un documento PDF di esempio con cui lavorare. Se non ne hai uno, crea un PDF semplice o scarica un esempio online.

Una volta impostato tutto, siamo pronti per iniziare a programmare!

## Importa pacchetti

Prima di immergerci nel codice, è fondamentale importare i pacchetti necessari. Questo ci garantisce l'accesso a tutte le classi e i metodi necessari per il nostro progetto.

```csharp
using Aspose.Pdf.Devices;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Queste importazioni sono fondamentali perché introducono gli spazi dei nomi necessari per gestire la manipolazione dei PDF, il rendering delle immagini e le operazioni di flusso dei file.

## Passaggio 1: imposta il percorso del progetto e del documento

Per prima cosa, impostiamo il percorso della directory in cui si trova il documento PDF. Questo sarà il punto di partenza per la manipolazione del file PDF.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```
Qui, `dataDir` è la directory in cui risiede il tuo documento PDF. Assicurati di sostituire `"YOUR DOCUMENT DIRECTORY"` Con il percorso effettivo del documento. Questo è essenziale perché il codice deve sapere da dove recuperare il file PDF.

## Passaggio 2: caricare il documento PDF

Ora che abbiamo il percorso del documento, il passo successivo è caricare il documento PDF nella memoria, così da poter iniziare a lavorarci.

```csharp
using (Document pdfDocument = new Document(dataDir + "input.pdf"))
```
Noi usiamo il `Document` classe della libreria Aspose.PDF per caricare il nostro file PDF. Questa classe fornisce vari metodi e proprietà per lavorare con il documento PDF. La `"input.pdf"` Deve essere sostituito con il nome effettivo del file PDF. Questo file verrà utilizzato come input per il rendering.

## Passaggio 3: creare un flusso di immagini per l'output

Una volta caricato il documento, dobbiamo impostare un flusso per salvare l'immagine renderizzata. È qui che verrà memorizzata l'immagine di output.

```csharp
using (FileStream imageStream = new FileStream(dataDir + "SetDefaultFontName.png", FileMode.Create))
```
IL `FileStream` La classe viene utilizzata per creare un nuovo file in cui verrà salvata l'immagine renderizzata. In questo esempio, salviamo l'immagine come `"SetDefaultFontName.png"`. IL `FileMode.Create` assicura che venga creato un nuovo file o che un file esistente venga sovrascritto.

## Passaggio 4: imposta la risoluzione per l'immagine

Prima di convertire il PDF in un'immagine, è fondamentale impostare la risoluzione. Questa determina la qualità e la nitidezza dell'immagine di output.

```csharp
Resolution resolution = new Resolution(300);
```
IL `Resolution` La classe imposta la risoluzione dell'immagine di output. Qui abbiamo scelto una risoluzione di 300 DPI (punti per pollice), standard per immagini di alta qualità. Questo garantisce che il testo e la grafica nel PDF vengano visualizzati in modo chiaro e senza perdite di dettaglio.

## Passaggio 5: configurare il dispositivo PNG

Ora dobbiamo configurare il dispositivo che gestirà il rendering del PDF in un'immagine PNG.

```csharp
PngDevice pngDevice = new PngDevice(resolution);
```
IL `PngDevice` La classe è responsabile del rendering del documento PDF in un'immagine PNG. Passando il `resolution` oggetto, ci assicuriamo che l'immagine venga creata con i DPI specificati.

## Passaggio 6: imposta il nome del font predefinito

Ecco la parte critica: impostare il nome del font predefinito. Questo sarà il font di riserva nel caso in cui il font originale nel PDF non sia disponibile.

```csharp
RenderingOptions ro = new RenderingOptions();
ro.DefaultFontName = "Arial";
pngDevice.RenderingOptions = ro;
```
Creiamo un'istanza di `RenderingOptions` e imposta il suo `DefaultFontName` proprietà a `"Arial"`Ciò significa che se il font originale nel PDF non è presente, verrà utilizzato Arial. Questo passaggio è fondamentale per mantenere la leggibilità e l'aspetto del testo nell'immagine renderizzata.

## Passaggio 7: Trasforma la pagina PDF in un'immagine

Infine, una volta impostato tutto, possiamo trasformare la prima pagina del documento PDF in un'immagine e salvarla utilizzando il flusso di file creato in precedenza.

```csharp
pngDevice.Process(pdfDocument.Pages[1], imageStream);
```
IL `Process` metodo del `PngDevice` La classe viene utilizzata per trasformare la pagina PDF specificata (in questo caso, la prima pagina) in un'immagine. L'output viene quindi salvato in `imageStream`Questo passaggio converte la pagina PDF in un'immagine PNG con la risoluzione specificata e il font predefinito.

## Passaggio 8: chiudere il flusso di file e il documento PDF

Dopo aver renderizzato l'immagine, è essenziale chiudere il flusso di file e il documento PDF per liberare risorse.

```csharp
imageStream.Close();
pdfDocument.Dispose();
```
Chiusura del `imageStream` assicura che il file venga salvato correttamente e che nessun dato venga perso. Lo smaltimento del `pdfDocument` Libera memoria e risorse, prevenendo potenziali perdite di memoria.

## Conclusione

Ed ecco fatto! Con poche righe di codice, hai imparato come impostare un nome di font predefinito durante il rendering di un PDF in un'immagine utilizzando Aspose.PDF per .NET. Questa abilità è incredibilmente utile, soprattutto quando si ha a che fare con PDF che potrebbero contenere font non supportati. Impostando un font predefinito, garantisci che le immagini renderizzate mantengano la loro leggibilità e il loro aspetto professionale.

## Domande frequenti

### Cosa succede se il font predefinito specificato non è installato sul sistema?
Se il font predefinito specificato nel `RenderingOptions` non è installato sul sistema, Aspose.PDF utilizzerà un font di fallback definito dal sistema.

### Posso usare font diversi da Arial come font predefinito?
Assolutamente! Puoi impostare qualsiasi font installato sul tuo sistema come predefinito.

### È possibile convertire più pagine di un PDF in immagini in una sola volta?
Sì, puoi scorrere le pagine del tuo PDF ed eseguire il rendering di ogni pagina singolarmente utilizzando lo stesso procedimento.

### L'impostazione di una risoluzione elevata influisce sulle prestazioni del rendering PDF?
Sì, risoluzioni più elevate produrranno file immagine più grandi e potrebbero aumentare i tempi di rendering, ma produrranno anche immagini più nitide.

### Posso convertire il PDF in altri formati immagine oltre a PNG?
Sì, Aspose.PDF supporta il rendering in vari formati immagine, quali JPEG, BMP e TIFF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}