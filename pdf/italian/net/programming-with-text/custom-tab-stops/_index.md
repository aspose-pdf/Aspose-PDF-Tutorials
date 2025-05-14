---
"description": "Scopri come impostare tabulazioni personalizzate in un PDF utilizzando Aspose.PDF per .NET. Questo tutorial illustra passo dopo passo come allineare il testo in modo professionale."
"linktitle": "Tabulazione personalizzata nel file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Tabulazione personalizzata nel file PDF"
"url": "/it/net/programming-with-text/custom-tab-stops/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tabulazione personalizzata nel file PDF

## Introduzione

Hai mai dovuto formattare il testo in un PDF e desiderato avere un controllo preciso sull'allineamento di ogni parola? Ecco perché le tabulazioni tornano utili! Proprio come nei documenti Word, puoi utilizzare tabulazioni personalizzate per allineare perfettamente il testo in punti specifici del PDF. Che tu voglia allineare il contenuto a destra, al centro o a sinistra, Aspose.PDF per .NET semplifica le cose. In questo tutorial, ti guideremo nell'impostazione di tabulazioni personalizzate nel tuo file PDF utilizzando Aspose.PDF per .NET. Al termine, sarai in grado di creare un documento perfettamente allineato con facilità.

## Prerequisiti

Prima di iniziare, ecco cosa ti servirà per seguire questo tutorial:

- Aspose.PDF per .NET: è necessario che la libreria Aspose.PDF sia installata. È possibile [scaricalo qui](https://releases.aspose.com/pdf/net/).
- Ambiente di sviluppo .NET: assicurati di avere Visual Studio o un altro IDE configurato per eseguire le applicazioni .NET.
- Nozioni di base di C#: scriveremo il codice in C#, quindi è consigliata una certa familiarità con il linguaggio.
- Licenza temporanea: puoi utilizzare la [licenza temporanea](https://purchase.aspose.com/temporary-license/) per sbloccare tutte le funzionalità di Aspose.PDF per .NET.

Una volta che tutto è pronto, passiamo all'importazione dei pacchetti necessari e alla configurazione dell'ambiente.

## Importa pacchetti

Per iniziare, è necessario importare gli spazi dei nomi Aspose.PDF. Ecco come fare:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Queste due linee sono essenziali. `Aspose.Pdf` lo spazio dei nomi fornisce la struttura del documento, mentre `Aspose.Pdf.Text` ci dà accesso a funzionalità specifiche del testo, come le tabulazioni personalizzate.

Analizziamo nel dettaglio il processo di impostazione delle tabulazioni personalizzate in un PDF. Analizzeremo ogni passaggio in dettaglio per assicurarci che tu capisca esattamente cosa sta succedendo.

## Passaggio 1: creare un nuovo documento PDF

La prima cosa da fare è creare un nuovo documento PDF. Consideralo come una tela. Aggiungerai le pagine e poi inserirai il testo formattato su di esse.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document _pdfdocument = new Document();
Page page = _pdfdocument.Pages.Add();
```

In questo frammento:
- Creiamo un nuovo `Document` oggetto.
- Aggiungiamo una nuova pagina al documento utilizzando `Pages.Add()`Qui inseriremo il testo con le tabulazioni.

## Passaggio 2: impostare le tabulazioni

Ora che abbiamo un documento vuoto, è il momento di definire le tabulazioni. Le tabulazioni controllano l'allineamento del testo in diverse posizioni sulla pagina. Ad esempio, potresti voler allineare una parte del testo a destra e un'altra al centro o a sinistra.

```csharp
Aspose.Pdf.Text.TabStops ts = new Aspose.Pdf.Text.TabStops();
Aspose.Pdf.Text.TabStop ts1 = ts.Add(100);
ts1.AlignmentType = TabAlignmentType.Right;
ts1.LeaderType = TabLeaderType.Solid;
```

Qui, noi:
- Inizializza un `TabStops` oggetto che conterrà le nostre tabulazioni personalizzate.
- Aggiungere una tabulazione al segno dei 100 pixel utilizzando `ts.Add(100)`. Definisce dove verrà inserita la tabulazione.
- Imposta il tipo di allineamento su `Right`, il che significa che il testo che tocca questa tabulazione verrà allineato a destra.
- Definisci un tipo di linea guida. Le linee guida sono i punti o i trattini che riempiono lo spazio prima della tabulazione. In questo caso, utilizziamo una linea continua.

## Passaggio 3: aggiungere più tabulazioni

Possiamo aggiungere tutte le tabulazioni che vogliamo. In questo esempio, aggiungeremo una tabulazione allineata al centro e una allineata a sinistra.

```csharp
Aspose.Pdf.Text.TabStop ts2 = ts.Add(200);
ts2.AlignmentType = TabAlignmentType.Center;
ts2.LeaderType = TabLeaderType.Dash;

Aspose.Pdf.Text.TabStop ts3 = ts.Add(300);
ts3.AlignmentType = TabAlignmentType.Left;
ts3.LeaderType = TabLeaderType.Dot;
```

- La seconda tabulazione è impostata a 200 pixel con allineamento centrale e un trattino iniziale.
- La terza tabulazione è posizionata a 300 pixel, si allinea a sinistra e utilizza una linea tratteggiata.

## Passaggio 4: creare testo con tabulazioni

Ora che le tabulazioni sono impostate, è il momento di creare del testo che le utilizzi. Puoi pensare a queste tabulazioni come a guide invisibili che aiutano ad allineare il contenuto in diverse posizioni.

```csharp
TextFragment header = new TextFragment("This is an example of forming a table with TAB stops", ts);
TextFragment text0 = new TextFragment("#$TABHead1 #$TABHead2 #$TABHead3", ts);
TextFragment text1 = new TextFragment("#$TABdata11 #$TABdata12 #$TABdata13", ts);
```

- `TextFragment` rappresenta un pezzo di testo.
- Utilizziamo i marcatori di tabulazione (`#$TAB`) per indicare al PDF dove applicare le tabulazioni.
- Ad esempio, in `text0`, `#$TABHead1` si allineerà in base alla prima tabulazione, `#$TABHead2` si allineerà al secondo e così via.

## Passaggio 5: aggiungere segmenti al testo

A volte, potresti voler dividere il testo in più segmenti, ognuno con la propria tabulazione. È qui che `TextSegment` torna utile.

```csharp
TextFragment text2 = new TextFragment("#$TABdata21 ", ts);
text2.Segments.Add(new TextSegment("#$TAB"));
text2.Segments.Add(new TextSegment("data22 "));
text2.Segments.Add(new TextSegment("#$TAB"));
text2.Segments.Add(new TextSegment("data23"));
```

In questo caso:
- Iniziamo con `#$TABdata21`, che si allinea alla prima tabulazione.
- Aggiungiamo altri segmenti come `data22` E `data23`, ciascuna allineata a diverse tabulazioni.

## Passaggio 6: aggiungere testo alla pagina PDF

Ora che abbiamo creato tutti i frammenti di testo, è il momento di aggiungerli alla pagina.

```csharp
page.Paragraphs.Add(header);
page.Paragraphs.Add(text0);
page.Paragraphs.Add(text1);
page.Paragraphs.Add(text2);
```

Questo codice aggiunge ogni `TextFragment` alla pagina PDF, assicurandosi che il testo sia formattato in base alle tabulazioni.

## Passaggio 7: salvare il documento PDF

Infine, dobbiamo salvare il documento nella directory specificata.

```csharp
dataDir = dataDir + "CustomTabStops_out.pdf";
_pdfdocument.Save(dataDir);
Console.WriteLine("\nCustom tab stops setup successfully.\nFile saved at " + dataDir);
```

- Il file PDF viene salvato con le tabulazioni personalizzate applicate.
- Viene visualizzato un messaggio per confermare la creazione corretta del file.

## Conclusione

Ed ecco fatto! Seguendo questa guida, hai imparato a creare tabulazioni personalizzate in un documento PDF utilizzando Aspose.PDF per .NET. Le tabulazioni consentono di allineare il testo in modo strutturato e visivamente accattivante, rendendo i tuoi PDF più professionali. Che tu stia allineando dettagli di fatture, tabelle o qualsiasi altra forma di dati, questa funzione ti offre il controllo completo sul posizionamento del testo.

## Domande frequenti

### Posso applicare le tabulazioni ai PDF esistenti?  
Sì, puoi modificare i PDF esistenti aggiungendo tabulazioni personalizzate per allineare il testo.

### Quali sono i tipi di leader disponibili?  
È possibile scegliere tra tipi di carattere continuo, tratteggiato, punteggiato e altri per riempire lo spazio prima della tabulazione.

### Posso aggiungere più tipi di allineamento su una singola riga?  
Assolutamente! Come mostrato nell'esempio, puoi combinare allineamenti a destra, a sinistra e al centro sulla stessa riga.

### C'è un limite al numero di tabulazioni che posso aggiungere?  
No, puoi aggiungere tutti i punti di tabulazione di cui hai bisogno per soddisfare i tuoi requisiti di progettazione.

### Posso personalizzare la posizione delle tabulazioni?  
Sì, puoi definire la posizione esatta in pixel di ogni tabulazione in base alle tue esigenze di layout.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}