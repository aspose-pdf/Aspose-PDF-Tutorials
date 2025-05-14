---
"description": "Guida passo passo per modificare l'orientamento delle pagine di un PDF con Aspose.PDF per .NET. Facile da seguire e implementare nei tuoi progetti."
"linktitle": "Cambia orientamento"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Cambia orientamento"
"url": "/it/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cambia orientamento

## Introduzione

Ti è mai capitato di avere difficoltà con un file PDF in cui l'orientamento delle pagine è semplicemente... sbagliato? Forse hai a che fare con un documento scansionato o creato in modo errato e le pagine devono essere ruotate per avere un senso. Fortunatamente, Aspose.PDF per .NET offre un modo semplice e potente per manipolare i file PDF in qualsiasi modo immaginabile, incluso cambiare l'orientamento delle pagine. Che tu voglia passare da verticale a orizzontale o viceversa, questa guida ti guiderà passo dopo passo nella procedura.

Quindi, se sei pronto a immergerti e ruotare le pagine PDF con facilità, iniziamo!

## Prerequisiti

Prima di entrare nei dettagli di come modificare l'orientamento delle pagine nel tuo PDF, vediamo brevemente cosa ti occorre:

- Aspose.PDF per .NET: assicurati di aver installato la libreria Aspose.PDF per .NET. In caso contrario, puoi [scaricalo qui](https://releases.aspose.com/pdf/net/).
- Un ambiente di sviluppo .NET: puoi utilizzare Visual Studio, JetBrains Rider o qualsiasi IDE preferito per lavorare con .NET.
- Conoscenza di base di C#: sebbene questa guida sia semplice, una conoscenza di base di C# la renderà ancora più facile da seguire.
- Un file PDF: l'esempio seguente presuppone che tu abbia un file PDF con più pagine. Se non ne hai uno a portata di mano, crea o scarica un PDF di esempio con cui lavorare.

Inoltre, se stai appena iniziando, puoi provare Aspose.PDF con un [licenza temporanea gratuita](https://purchase.aspose.com/temporary-license/) prima di decidere di [acquista la versione completa](https://purchase.aspose.com/buy).

## Importa spazi dei nomi

Prima di poter modificare l'orientamento delle pagine del PDF, è necessario importare gli spazi dei nomi necessari nel progetto C#. Assicurarsi di disporre di quanto segue:

```csharp
using System.IO;
using Aspose.Pdf;
```

Dopo aver importato questo, passiamo alla parte principale del tutorial.

## Passaggio 1: caricare il documento PDF

La prima cosa che dobbiamo fare è caricare il file PDF che desideri modificare. Puoi usare `Document` classe dallo spazio dei nomi Aspose.PDF per aprire il PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Questa riga carica il PDF dalla directory specificata. Assicurati di sostituire `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo del tuo file. Il `"input.pdf"` è il PDF di cui vuoi modificare l'orientamento.

## Passaggio 2: scorrere ogni pagina

Ora che abbiamo caricato il documento, scorriamo ogni pagina del PDF. Useremo un `foreach` per scorrere ogni pagina, consentendoci di applicare la modifica di orientamento a tutte.

```csharp
foreach (Page page in doc.Pages)
{
    // Manipola ogni pagina
}
```

Questo ciclo itererà attraverso tutte le pagine del documento.

## Passaggio 3: Ottieni il MediaBox della pagina

Ogni pagina di un PDF ha un `MediaBox` che definisce i confini della pagina. Dobbiamo accedervi per determinare l'orientamento corrente e modificarlo.

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

IL `MediaBox` ci fornisce le dimensioni della pagina, come larghezza, altezza e posizionamento.

## Passaggio 4: scambia larghezza e altezza

Per cambiare l'orientamento della pagina da verticale a orizzontale o viceversa, basta invertire i valori di larghezza e altezza. Questo passaggio regolerà le dimensioni della pagina.

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

Questo codice scambia l'altezza e la larghezza e riposiziona l'angolo inferiore sinistro (`LLY`) in modo che il contenuto si adatti perfettamente dopo la rotazione.

## Passaggio 5: aggiorna MediaBox e CropBox

Ora che abbiamo la nuova altezza e larghezza, applichiamo le modifiche alla pagina `MediaBox` E `CropBox`. IL `CropBox` è essenziale se il documento originale ne aveva uno, assicurando la corretta visualizzazione dell'intera pagina.

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

Questo passaggio ridimensiona la pagina in base alle nuove dimensioni appena calcolate.

## Passaggio 6: ruota la pagina

Infine, impostiamo l'angolo di rotazione della pagina. Aspose.PDF semplifica enormemente questa operazione. Possiamo ruotare la pagina di 90 gradi per passare dall'orientamento verticale a quello orizzontale e viceversa.

```csharp
page.Rotate = Rotation.on90;
```

Questo codice ruota la pagina di 90 gradi, invertendo l'orientamento desiderato.

## Passaggio 7: salvare il PDF di output

Dopo aver applicato le modifiche di orientamento a tutte le pagine, salviamo il documento modificato in un nuovo file. 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

Assicurati di fornire un nuovo nome di file (in questo caso, `ChangeOrientation_out.pdf`) per salvare l'output. In questo modo, non sovrascrivi il file originale.

### Conclusione

Ed ecco fatto! Cambiare l'orientamento delle pagine di un file PDF utilizzando Aspose.PDF per .NET è semplicissimo: basta caricare il documento, scorrere le pagine, regolare il MediaBox e salvare il file aggiornato. Che tu abbia a che fare con un documento scansionato male o con la necessità di ruotare le pagine per adattarle alle tue esigenze di formattazione, questa guida passo passo ti aiuterà.

## Domande frequenti

### Posso ruotare pagine specifiche invece di tutte le pagine del PDF?  
Sì, puoi modificare il ciclo in modo che punti a pagine specifiche utilizzando il loro indice anziché eseguire il ciclo su tutte le pagine.

### Che cosa è il `MediaBox`?  
IL `MediaBox` Definisce le dimensioni e la forma della pagina in un file PDF. È qui che viene inserito il contenuto della pagina.

### Aspose.PDF per .NET funziona con altri formati di file?  
Sì, Aspose.PDF può gestire vari formati di file, tra cui HTML, XML, XPS e altri.

### Esiste una versione gratuita di Aspose.PDF per .NET?  
Sì, puoi iniziare con un [prova gratuita](https://releases.aspose.com/) o richiedi un [licenza temporanea](https://purchase.aspose.com/temporary-license/).

### Posso annullare le modifiche una volta salvate?  
Una volta salvato il documento, le modifiche saranno definitive. Assicurati di lavorare su una copia o di conservare un backup del file originale.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}