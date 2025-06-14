---
"description": "Scopri come cercare testo e aggiungere collegamenti ipertestuali nei PDF utilizzando Aspose.PDF per .NET con il nostro tutorial passo dopo passo."
"linktitle": "Cerca testo e aggiungi collegamento ipertestuale"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Cerca testo e aggiungi collegamento ipertestuale"
"url": "/it/net/programming-with-text/search-text-and-add-hyperlink/"
"weight": 450
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cerca testo e aggiungi collegamento ipertestuale

## Introduzione

Stai cercando un modo non solo per manipolare i PDF, ma anche per migliorarli inserendo collegamenti ipertestuali? Beh, sei nel posto giusto! Con la potente libreria Aspose.PDF per .NET, puoi cercare schemi di testo nei tuoi documenti PDF e aggiungere collegamenti ipertestuali senza problemi. Immagina di avere un documento che non solo trasmette informazioni, ma collega anche i lettori a risorse pertinenti semplicemente cliccando su un collegamento. Interessante, vero? In questo tutorial, ti guideremo passo dopo passo su come cercare testo utilizzando espressioni regolari e aggiungere collegamenti ipertestuali nei tuoi PDF. Che tu sia uno sviluppatore esperto o alle prime armi, troverai questo processo semplice e gratificante.

## Prerequisiti

Prima di addentrarci nei dettagli, assicuriamoci di avere tutto il necessario per seguire il tutorial. Ecco una comoda checklist:

- .NET Framework: sul computer dovrebbe essere installato .NET Framework (versione 4.0 o successiva).
- Libreria Aspose.PDF per .NET: non dimenticare di scaricare e aggiungere un riferimento alla libreria Aspose.PDF nel tuo progetto. Puoi trovarla [Qui](https://releases.aspose.com/pdf/net/).
- IDE: per scrivere ed eseguire il codice è necessario un ambiente di sviluppo integrato (IDE) come Visual Studio.
- File PDF di esempio: scarica un file PDF di esempio su cui testare il codice. Puoi creare un PDF semplice o utilizzare uno dei tuoi documenti esistenti.

Una volta spuntati tutti gli elementi presenti in questa lista, saremo pronti a partire!

## Importa pacchetti

Il primo passo del nostro percorso è importare i pacchetti necessari. È qui che indichiamo al nostro progetto quali strumenti utilizzeremo. Ecco come fare:

Nel tuo file C#, inizia includendo i seguenti namespace nella parte superiore:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

Importando questi namespace, consenti al tuo programma di accedere a tutte le fantastiche funzionalità offerte da Aspose.PDF.

Ora che siamo tutti pronti, è il momento di passare all'azione. Lo faremo in una serie di passaggi, quindi seguiteci attentamente!

### Passaggio 1: imposta la directory dei documenti

Per prima cosa, dovrai specificare dove sono archiviati i tuoi file PDF. Modifica il `dataDir` variabile per puntare alla directory del documento. Ecco come fare:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Assicurati di sostituire `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo per arrivare ai tuoi documenti.

### Passaggio 2: creare un TextFragmentAbsorber

Successivamente, abbiamo bisogno di uno strumento per trovare il testo che vogliamo collegare. Inserisci il `TextFragmentAbsorber`Questo piccolo strumento ci aiuterà a cercare lo specifico schema di testo nel nostro PDF.

```csharp
TextFragmentAbsorber absorber = new TextFragmentAbsorber("\\d{4}-\\d{4}");
```

Qui stiamo cercando uno schema specifico: quattro cifre, un trattino, seguiti da altre quattro cifre (come un numero di telefono o l'anno).

### Passaggio 3: abilitare la ricerca tramite espressioni regolari

Stiamo già utilizzando un'espressione regolare per trovare il nostro modello di testo, ma dobbiamo assicurarci che il nostro `absorber` sa di essere abilitato. Questo è fondamentale per il corretto funzionamento della ricerca.

```csharp
absorber.TextSearchOptions = new TextSearchOptions(true);
```

### Passaggio 4: inizializzare PdfContentEditor

Ora che abbiamo pronto il nostro assorbitore, abbiamo bisogno di un `PdfContentEditor` per lavorare con il nostro file PDF. Questa classe ci permette di associarlo al nostro PDF e manipolarlo.

```csharp
PdfContentEditor editor = new PdfContentEditor();
```

### Passaggio 5: associa il file PDF di origine

Una volta pronto il nostro editor di contenuti, è il momento di associarlo al file PDF su cui vogliamo lavorare.

```csharp
editor.BindPdf(dataDir + "SearchRegularExpressionPage.pdf");
```

Assicurati di sostituire `"SearchRegularExpressionPage.pdf"` con il nome del tuo file PDF.

### Passaggio 6: accettare l'assorbitore per la pagina

Dobbiamo far sapere al nostro editor che vogliamo effettuare una ricerca in una pagina specifica del documento. In questo caso, scegliamo la Pagina 1.

```csharp
editor.Document.Pages[1].Accept(absorber);
```

### Fase 7: Prepararsi a scorrere i frammenti di testo

Ora siamo pronti per scorrere tutti i frammenti di testo trovati dal nostro assorbitore. Ne modifichiamo l'aspetto e impostiamo il nostro collegamento ipertestuale.

```csharp
int[] dashArray = { };
String[] LEArray = { };
Color blue = Color.Blue;
```

Qui impostiamo alcuni parametri, come il colore del nostro collegamento ipertestuale.

### Passaggio 8: scorrere ogni frammento di testo

Per ogni frammento di testo che corrisponde alla nostra ricerca, ne cambieremo il colore e creeremo un collegamento ipertestuale. Ecco come appare:

```csharp
foreach (TextFragment textFragment in absorber.TextFragments)
{
    textFragment.TextState.ForegroundColor = Aspose.Pdf.Color.Blue;
    Rectangle rect = new Rectangle((int)textFragment.Rectangle.LLX,
        (int)Math.Round(textFragment.Rectangle.LLY), (int)Math.Round(textFragment.Rectangle.Width + 2),
        (int)Math.Round(textFragment.Rectangle.Height + 1));
    Enum[] actionName = new Enum[2] { Aspose.Pdf.Annotations.PredefinedAction.Document_AttachFile, Aspose.Pdf.Annotations.PredefinedAction.Document_ExtractPages };
    
    editor.CreateWebLink(rect, "http://www.aspose.com", 1, blu, actionName);
    editor.CreateLine(rect, "", (float)textFragment.Rectangle.LLX + 1, (float)textFragment.Rectangle.LLY - 1,
        (float)textFragment.Rectangle.URX, (float)textFragment.Rectangle.LLY - 1, 1, 1, blue, "S", dashArray, LEArray);
}
```

### Passaggio 9: Salva il PDF modificato

Ci siamo quasi! Ora è il momento di salvare le modifiche in un nuovo file PDF.

```csharp
dataDir = dataDir + "SearchTextAndAddHyperlink_out.pdf";
editor.Save(dataDir);
```

### Passaggio 10: chiudere l'editor

Infine, non dimenticare di chiudere il documento per rilasciare risorse!

```csharp
editor.Close();
Console.WriteLine("\nText replaced and hyperlink added successfully based on a regular expression.\nFile saved at " + dataDir);
```

Ora hai appena creato un PDF con un collegamento ipertestuale generato dinamicamente in base ai risultati di ricerca. Fantastico!

## Conclusione

Ed ecco fatto! Seguendo questi passaggi, hai imparato come cercare in un PDF e aggiungere collegamenti ipertestuali utilizzando la libreria Aspose.PDF per .NET. Questo può aprire un mondo di possibilità, soprattutto se lavori con documenti che richiedono interattività. Immagina di aggiungere link a risorse correlate, siti web di riferimento o persino pagine interne, il tutto con poche righe di codice!
## Domande frequenti

### Che cos'è Aspose.PDF per .NET?  
Aspose.PDF per .NET è una libreria che consente agli sviluppatori di creare, manipolare e gestire documenti PDF nelle applicazioni .NET.

### Come posso scaricare Aspose.PDF per .NET?  
Puoi scaricare la libreria [Qui](https://releases.aspose.com/pdf/net/).

### Posso provare Aspose.PDF gratuitamente?  
Assolutamente! Puoi ottenere una prova gratuita. [Qui](https://releases.aspose.com/).

### È disponibile supporto per i prodotti Aspose?  
Sì, puoi trovare supporto e discussioni della comunità [Qui](https://forum.aspose.com/c/pdf/10).

### Come posso ottenere una licenza temporanea per Aspose.PDF?  
Puoi richiedere una licenza temporanea [Qui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}