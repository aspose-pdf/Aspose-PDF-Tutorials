---
"description": "Scopri come rimuovere i collegamenti ipertestuali dai documenti HTML dopo averli convertiti in PDF utilizzando Aspose.PDF per .NET in questa guida dettagliata."
"linktitle": "Rimuovere i collegamenti ipertestuali dopo la conversione da HTML"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Rimuovere i collegamenti ipertestuali dopo la conversione da HTML"
"url": "/it/net/document-conversion/remove-hyperlinks-after-converting-from-html/"
"weight": 250
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rimuovere i collegamenti ipertestuali dopo la conversione da HTML

## Introduzione

Nell'era digitale, convertire documenti HTML in PDF è un'operazione comune. Tuttavia, a volte potrebbe essere necessario rimuovere i collegamenti ipertestuali dal PDF convertito per vari motivi, ad esempio per migliorare la leggibilità o impedire la navigazione indesiderata. In questo tutorial, esploreremo come ottenere questo risultato utilizzando Aspose.PDF per .NET. 

## Prerequisiti

Prima di immergerti nel codice, assicurati di avere i seguenti prerequisiti:

1. Visual Studio: assicurati di aver installato Visual Studio sul tuo computer. Questo sarà il tuo ambiente di sviluppo.
2. Aspose.PDF per .NET: è necessaria la libreria Aspose.PDF. È possibile scaricarla da [Qui](https://releases.aspose.com/pdf/net/).
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio il codice.

## Importa pacchetti

Per iniziare, devi importare i pacchetti necessari nel tuo progetto C#. Ecco come fare:

1. Apri il tuo progetto Visual Studio.
2. Fai clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e seleziona "Gestisci pacchetti NuGet".
3. Cercare `Aspose.PDF` e installarlo.

```csharp
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.IO;
```

Ora che hai impostato tutto, analizziamo il processo di rimozione dei collegamenti ipertestuali da un file HTML dopo averlo convertito in PDF.

## Passaggio 1: impostare la directory dei documenti

Per prima cosa, devi specificare il percorso della directory dei documenti. È qui che si trova il tuo file HTML e dove verrà salvato il PDF di output.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Sostituire `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo in cui è archiviato il file HTML.

## Passaggio 2: caricare il documento HTML

Successivamente, caricherai il documento HTML utilizzando `Document` classe di Aspose.PDF. Questa classe permette di lavorare facilmente con i documenti PDF.

```csharp
Document doc = new Document(dataDir + "SampleHtmlFile.html", new HtmlLoadOptions());
```

Qui stiamo caricando il file HTML denominato `SampleHtmlFile.html`Assicurati che questo file esista nella directory specificata.

## Passaggio 3: salvare il documento nel flusso di memoria

Prima di iniziare a elaborare le annotazioni, dobbiamo salvare il documento in un flusso di memoria. Questo passaggio è fondamentale perché prepara il documento per ulteriori elaborazioni.

```csharp
doc.Save(new MemoryStream());
```

Questa riga salva il documento in memoria, consentendoci di lavorarci senza doverlo ancora scrivere sul disco.

## Passaggio 4: scorrere le annotazioni

Ora esamineremo le annotazioni presenti nel documento. Le annotazioni sono elementi come link, commenti ed evidenziazioni. Siamo specificamente interessati alle annotazioni sui link.

```csharp
foreach (Annotation a in doc.Pages[1].Annotations)
{
    if (a.AnnotationType == AnnotationType.Link)
    {
        // Elaborare l'annotazione del collegamento
    }
}
```

In questo ciclo, controlliamo se il tipo di annotazione è un collegamento. In tal caso, procediamo con i passaggi successivi.

## Passaggio 5: rimuovere l'azione del collegamento ipertestuale

Per ogni annotazione di collegamento, dobbiamo verificare se ha un'azione di collegamento ipertestuale. In tal caso, rimuoveremo il collegamento ipertestuale impostandone l'URI a una stringa vuota.

```csharp
LinkAnnotation la = (LinkAnnotation)a;
if (la.Action is GoToURIAction)
{
    GoToURIAction gta = (GoToURIAction)la.Action;
    gta.URI = "";
```

Questo frammento di codice garantisce che l'azione del collegamento ipertestuale venga effettivamente rimossa.

## Fase 6: Assorbimento di frammenti di testo

Successivamente, assorbiremo i frammenti di testo associati all'annotazione del link. Questo ci permetterà di manipolare l'aspetto del testo.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
tfa.TextSearchOptions = new TextSearchOptions(a.Rect);
doc.Pages[a.PageIndex].Accept(tfa);
```

Qui creiamo un `TextFragmentAbsorber` e imposta le opzioni di ricerca sul rettangolo dell'annotazione. Questo ci aiuta a trovare il testo collegato.

## Passaggio 7: modifica l'aspetto del testo

Una volta ottenuti i frammenti di testo, possiamo modificarne l'aspetto. In questo caso, rimuoveremo la sottolineatura e cambieremo il colore del testo in nero.

```csharp
foreach (TextFragment tf in tfa.TextFragments)
{
    tf.TextState.Underline = false;
    tf.TextState.ForegroundColor = Color.Black;
}
```

Questo passaggio migliora la leggibilità del testo rimuovendo lo stile dei collegamenti ipertestuali.

## Passaggio 8: Elimina l'annotazione

Dopo aver modificato il testo, possiamo eliminare in tutta sicurezza l'annotazione del collegamento dal documento.

```csharp
doc.Pages[a.PageIndex].Annotations.Delete(a);
}
```

Questa riga rimuove il collegamento ipertestuale dal PDF, assicurando che non esista più nell'output finale.

## Passaggio 9: salvare il documento modificato

Infine, dobbiamo salvare il documento modificato in un nuovo file PDF. Questo è l'ultimo passaggio del nostro processo.

```csharp
doc.Save(dataDir + "RemoveHyperlinksFromText_out.pdf");
```

Questa riga salva il documento con i collegamenti ipertestuali rimossi, creando un nuovo file PDF denominato `RemoveHyperlinksFromText_out.pdf`.

## Conclusione

Ed ecco fatto! Hai rimosso con successo i collegamenti ipertestuali da un documento HTML dopo averlo convertito in PDF utilizzando Aspose.PDF per .NET. Questo processo non solo migliora la leggibilità del tuo PDF, ma ti dà anche il controllo sul contenuto che presenti. 

## Domande frequenti

### Posso rimuovere i collegamenti ipertestuali da qualsiasi documento PDF?
Sì, puoi rimuovere i collegamenti ipertestuali da qualsiasi documento PDF utilizzando Aspose.PDF per .NET.

### Aspose.PDF è gratuito?
Aspose.PDF offre una prova gratuita, ma per usufruire di tutte le funzionalità è necessario acquistare una licenza. Controlla [pagina di acquisto](https://purchase.aspose.com/buy).

### Cosa succede se riscontro problemi durante l'utilizzo di Aspose.PDF?
Puoi cercare aiuto su [forum di supporto](https://forum.aspose.com/c/pdf/10).

### Posso convertire altri formati di file in PDF utilizzando Aspose?
Sì, Aspose supporta vari formati di file per la conversione in PDF.

### Dove posso scaricare Aspose.PDF per .NET?
Puoi scaricarlo da [collegamento per il download](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}