---
"description": "Scopri come specificare l'interlinea in un PDF utilizzando Aspose.PDF per .NET con questa guida passo passo. Perfetta per gli sviluppatori che desiderano una formattazione del testo precisa."
"linktitle": "Specificare l'interlinea nel file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Specificare l'interlinea nel file PDF"
"url": "/it/net/programming-with-text/specify-line-spacing/"
"weight": 510
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Specificare l'interlinea nel file PDF

## Introduzione

Hai mai avuto difficoltà a controllare l'interlinea in un file PDF? Forse hai trovato del testo troppo compresso o semplicemente non curato come vorresti. In questo tutorial, ti mostreremo come specificare facilmente l'interlinea in un PDF utilizzando Aspose.PDF per .NET. Utilizzeremo una semplice guida passo passo per passare da un PDF vuoto a uno che include l'interlinea personalizzata. Questa soluzione è perfetta se hai bisogno di precisione nel layout del testo per documenti come report, fatture o certificati.

## Prerequisiti

Prima di passare al codice, assicuriamoci di avere tutto ciò che serve:

1. Aspose.PDF per .NET installato. Se non lo hai, scaricalo da [Pagina di download di Aspose.PDF](https://releases.aspose.com/pdf/net/).
2. Un ambiente di sviluppo .NET (come Visual Studio).
3. Un file di font TrueType (`.ttf`) che useremo nell'esempio. Puoi usare qualsiasi font, ma per questa guida useremo il `HPSimplified.TTF` font.
4. Conoscenza di base di C# e manipolazione PDF.

Se siete pronti, passiamo all'importazione dei pacchetti necessari.

## Importa pacchetti

Nel tuo progetto C#, dovrai importare gli spazi dei nomi Aspose.PDF per utilizzare le funzionalità PDF. Ecco come fare:

```csharp
using Aspose.Pdf.Text;
using System.IO;
```

Questi namespace consentono di creare e manipolare documenti PDF, nonché di lavorare con la formattazione del testo e le opzioni dei caratteri.

Suddivideremo il tutto in passaggi brevi, così potrai seguirli facilmente. Ogni passaggio si concentrerà su una parte fondamentale del processo, dalla configurazione del PDF alla definizione dell'interlinea.

## Passaggio 1: imposta il progetto e definisci la directory dei documenti

La prima cosa che dobbiamo fare è definire dove si trovano i nostri file. Questo aiuta il programma a sapere dove trovare il font e dove salvare il PDF risultante.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string fontFile = dataDir + "HPSimplified.TTF";
```

In questo passaggio sostituirai `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo in cui memorizzi i tuoi file. Qui sarà dove posizionerai il file del font (`HPSimplified.TTF`) e dove verrà salvato il PDF.

## Passaggio 2: carica un documento PDF

Ora dobbiamo creare un nuovo documento PDF. Per questa guida, inizieremo con un documento vuoto, ma puoi anche caricare un PDF esistente, se necessario.

```csharp
Document doc = new Document();
```

Questo crea un nuovo documento PDF vuoto. Facile, vero?

## Passaggio 3: imposta le opzioni di formattazione del testo

Ed è qui che avviene la magia. Specifichiamo la modalità di interlinea per il testo che vogliamo aggiungere al PDF. Aspose.PDF ci offre diverse opzioni, ma in questa guida useremo `LineSpacingMode.FullSize`, che garantisce il pieno rispetto della spaziatura delle linee.

```csharp
TextFormattingOptions formattingOptions = new TextFormattingOptions();
formattingOptions.LineSpacing = TextFormattingOptions.LineSpacingMode.FullSize;
```

Questo codice imposta la modalità di spaziatura delle linee su `FullSize`assicurando che il testo venga visualizzato con la spaziatura corretta. Ci sono altre opzioni come `Proportional` se desideri comportamenti di spaziatura diversi, ma per ora, atteniamoci a `FullSize`.

## Passaggio 4: creare un frammento di testo

Ora creeremo il testo vero e proprio che verrà inserito nel PDF. Questo testo rispetterà l'interlinea che abbiamo definito.

```csharp
TextFragment textFragment = new TextFragment("Hello world");
```

Abbiamo creato un frammento di testo con la stringa `"Hello world"`Naturalmente puoi personalizzare questo testo come preferisci.

## Passaggio 5: carica e applica un font personalizzato

Per far risaltare il testo, caricheremo un font TrueType personalizzato da un file. Questo passaggio è facoltativo, ma può aggiungere un tocco professionale ai tuoi PDF.

```csharp
if (fontFile != "")
{
    using (FileStream fontStream = System.IO.File.OpenRead(fontFile))
    {
        textFragment.TextState.Font = FontRepository.OpenFont(fontStream, FontTypes.TTF);
```

Qui carichiamo il file del font e lo applichiamo al frammento di testo. Se il percorso del file è valido, il font viene utilizzato. In caso contrario, viene applicato il font predefinito.

## Passaggio 6: imposta la posizione e la formattazione del testo

Ora dobbiamo posizionare il testo sul PDF. Applicheremo anche le opzioni di formattazione create in precedenza.

```csharp
textFragment.Position = new Position(100, 600);
textFragment.TextState.FormattingOptions = formattingOptions;
```

IL `Position` Il metodo imposta le coordinate in cui il testo apparirà sulla pagina (in questo caso, 100 unità da sinistra e 600 unità dal basso). Qui vengono applicate le opzioni di formattazione, inclusa la modalità di interlinea.

## Passaggio 7: aggiungere testo alla pagina PDF

Ora che il testo è formattato e posizionato, è il momento di aggiungerlo al documento PDF.

```csharp
var page = doc.Pages.Add();
page.Paragraphs.Add(textFragment);
```

Questo codice crea una nuova pagina nel documento PDF e vi aggiunge il frammento di testo.

## Passaggio 8: salva il PDF

Siamo arrivati al passaggio finale! Ora che tutto è pronto, salviamo il PDF.

```csharp
dataDir = dataDir + "SpecifyLineSpacing_out.pdf";
doc.Save(dataDir);
```

In questo modo il PDF verrà salvato con la spaziatura delle righe specificata e il file sarà pronto!

## Conclusione

Ed è tutto! Hai appena creato un documento PDF con interlinea personalizzata utilizzando Aspose.PDF per .NET. È uno strumento potente che ti permette di controllare ogni aspetto dei tuoi file PDF, e questo è solo un esempio di ciò che puoi ottenere. Dal posizionamento del testo alla formattazione, le possibilità sono infinite.

Se desideri approfondire la manipolazione dei PDF, Aspose.PDF offre una vasta gamma di funzionalità da esplorare. Non esitare a sperimentare e a spingerti oltre i limiti di ciò che puoi fare con i tuoi documenti!

## Domande frequenti

### Posso adattare la spaziatura delle linee ad altre modalità?  
Sì, puoi usare altre modalità come `PropOtional` or `Fixed` a seconda delle vostre esigenze.

### È possibile caricare i font dal sistema invece che da un file?  
Sì, puoi caricare i font installati dal sistema utilizzando `FontRepository`.

### Posso usare Aspose.PDF per .NET con altri formati di file?  
Assolutamente sì! Aspose.PDF per .NET supporta una varietà di formati come XML, HTML e altri.

### Ho bisogno di una licenza per utilizzare Aspose.PDF per .NET?  
Sì, per la piena funzionalità avrai bisogno di una licenza, che puoi ottenere [Qui](https://purchase.aspose.com/buy).

### Come faccio a impostare la spaziatura delle righe per più paragrafi?  
Puoi applicare `TextFormattingOptions` a ciascuno `TextFragment` O `TextParagraph` per controllare la spaziatura tra più righe o paragrafi.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}