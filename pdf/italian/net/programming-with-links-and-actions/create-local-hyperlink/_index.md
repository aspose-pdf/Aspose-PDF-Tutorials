---
"description": "Scopri come creare senza sforzo collegamenti ipertestuali locali nei file PDF utilizzando Aspose.PDF per .NET con la nostra guida dettagliata."
"linktitle": "Crea un collegamento ipertestuale locale nel file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Crea un collegamento ipertestuale locale nel file PDF"
"url": "/it/net/programming-with-links-and-actions/create-local-hyperlink/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Crea un collegamento ipertestuale locale nel file PDF

## Introduzione

In questa guida, ti guideremo attraverso il processo di creazione di collegamenti ipertestuali locali in un file PDF utilizzando Aspose.PDF per .NET. Analizzeremo ogni passaggio in modo chiaro, in modo che anche i meno esperti nel mondo della manipolazione dei PDF possano seguirlo senza problemi.

## Prerequisiti

Prima di immergerci a capofitto nel codice, assicuriamoci di avere tutto ciò che ti serve:

1. Visual Studio: ti servirà per sviluppare le tue applicazioni .NET. Scaricalo da [sito web](https://visualstudio.microsoft.com/).
2. Aspose.PDF per .NET: puoi scaricare questa libreria tramite [link per il download qui](https://releases.aspose.com/pdf/net/)È dotato di una vasta gamma di funzionalità per la manipolazione dei PDF.
3. Conoscenza di base di C#: un po' di familiarità con la programmazione C# sarà utile, ma non preoccupatevi: analizzeremo il codice riga per riga.
4. .NET Framework: assicurati di aver installato .NET Framework sul tuo computer. Puoi verificare i requisiti su Aspose.PDF. [documentazione](https://reference.aspose.com/pdf/net/).

Una volta impostati questi prerequisiti, sarai pronto per imparare a creare collegamenti ipertestuali locali nei tuoi documenti PDF!

## Importa pacchetti

Ora che hai tutto pronto, è il momento di importare i pacchetti necessari nel tuo progetto C#. La libreria Aspose.PDF contiene tutte le classi di cui abbiamo bisogno. Ecco come fare:

### Apri il tuo progetto

Apri il tuo progetto .NET esistente o creane uno nuovo in Visual Studio. Se stai iniziando da zero, seleziona "Crea un nuovo progetto" dalla schermata iniziale.

### Aggiungi riferimento a Aspose.PDF

Fai clic con il pulsante destro del mouse su "Dipendenze" nella cartella del progetto in Esplora soluzioni. Seleziona "Gestisci pacchetti NuGet", quindi cerca `Aspose.PDF`Installa l'ultima versione disponibile. Avrai a disposizione tutti gli strumenti necessari per creare e manipolare i PDF.

### Importa spazi dei nomi

Nella parte superiore del file .cs, aggiungi le direttive using per la libreria Aspose.PDF in questo modo:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

In questo modo potrai accedere alle funzionalità della biblioteca.

Analizziamo il processo di creazione di collegamenti ipertestuali locali in semplici passaggi. Ogni passaggio verrà spiegato in modo esaustivo per aiutarti a comprenderne la logica.

## Passaggio 1: impostare l'istanza del documento

In questo passaggio creerai una nuova istanza della classe Document, che rappresenta il file PDF con cui lavorerai.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Imposta la directory dei tuoi documenti
Document doc = new Document(); // Crea istanza del documento
```
IL `dataDir` La variabile è dove risiederà il tuo PDF appena creato. Dovrai sostituirla `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo sul tuo sistema. Il `Document` La classe crea un nuovo documento PDF in cui possiamo aggiungere pagine e collegamenti.

## Passaggio 2: aggiungere una pagina al documento

Ora dovrai aggiungere una pagina al tuo documento PDF. 

```csharp
Page page = doc.Pages.Add(); // Aggiungi pagina alla raccolta di pagine
```
IL `Pages.Add()` Il metodo aggiunge una nuova pagina al documento. È qui che conterranno tutti i tuoi contenuti.

## Passaggio 3: creare un frammento di testo

Ora creiamo un pezzo di testo che fungerà da collegamento cliccabile.

```csharp
Aspose.Pdf.Text.TextFragment text = new Aspose.Pdf.Text.TextFragment("link page number test to page 7");
```
IL `TextFragment` Rappresenta un segmento di testo nel PDF. Qui creiamo un link che indica agli utenti che li porterà a pagina 7.

## Passaggio 4: creare un collegamento ipertestuale locale

Ed è qui che avviene la magia! Devi creare un collegamento ipertestuale locale che indichi al frammento di testo dove puntare.

```csharp
Aspose.Pdf.LocalHyperlink link = new Aspose.Pdf.LocalHyperlink(); // Crea collegamento ipertestuale locale
link.TargetPageNumber = 7; // Imposta la pagina di destinazione per l'istanza del collegamento
text.Hyperlink = link; // Imposta collegamento ipertestuale TextFragment
```
IL `LocalHyperlink` La classe è ciò che ci permette di puntare ad altre pagine nello stesso documento. Impostando `TargetPageNumber` a 7, si indica al collegamento ipertestuale di passare a quella pagina specifica quando si fa clic.

## Passaggio 5: aggiungere il frammento di testo alla pagina

Dopo aver impostato il collegamento ipertestuale, è il momento di aggiungere il nostro frammento di testo alla pagina che abbiamo creato.

```csharp
page.Paragraphs.Add(text); // Aggiungi testo alla raccolta di paragrafi della pagina
```
Questa riga aggiunge il testo cliccabile alla raccolta di paragrafi della pagina.

## Passaggio 6: creare un altro frammento di testo (facoltativo)

Aggiungiamo un altro collegamento ipertestuale per tornare alla pagina 1.

```csharp
text = new TextFragment("link page number test to page 1"); // Crea un nuovo TextFragment
text.IsInNewPage = true; // Aggiungilo a una nuova pagina
```
Creazione di un nuovo `TextFragment` per il secondo collegamento, impostiamo `IsInNewPage` su vero, indicando che il testo verrà inserito in una nuova pagina.

## Passaggio 7: impostare il secondo collegamento ipertestuale locale

Proprio come prima, creerai un altro collegamento ipertestuale locale per la pagina 1.

```csharp
link = new LocalHyperlink(); // Crea un'altra istanza di collegamento ipertestuale locale
link.TargetPageNumber = 1; // Imposta la pagina di destinazione per il secondo collegamento ipertestuale
text.Hyperlink = link; // Imposta collegamento per il secondo TextFragment
```
Questo collegamento ipertestuale punta alla pagina 1, consentendo agli utenti di tornare indietro quando raggiungono la seconda pagina.

## Passaggio 8: aggiungere il secondo frammento di testo alla nuova pagina

Ora aggiungiamo questo testo alla sua pagina.

```csharp
page.Paragraphs.Add(text); // Aggiungi testo alla raccolta di paragrafi dell'oggetto pagina
```
Simile al passaggio 5, questa riga aggiunge il nuovo testo del collegamento ipertestuale alla pagina appena creata.

## Passaggio 9: Salvare il documento

Finalmente è arrivato il momento di salvare il tuo duro lavoro! 

```csharp
dataDir = dataDir + "CreateLocalHyperlink_out.pdf"; // Specificare il nome del file di output
doc.Save(dataDir); // Salva il documento aggiornato
Console.WriteLine("\nLocal hyperlink created successfully.\nFile saved at " + dataDir);
```
Questo combina il percorso della directory con il nome del file. `Save()` Il metodo salva il documento e un messaggio di conferma ti informa che tutto è andato liscio!

## Conclusione

Creare collegamenti ipertestuali locali nei file PDF utilizzando Aspose.PDF per .NET non è solo un trucco interessante; è una funzionalità pratica che migliora la navigazione e l'esperienza utente. Ora hai le conoscenze necessarie per indirizzare i tuoi lettori direttamente alle informazioni di cui hanno bisogno. Ripensa alla nostra analogia iniziale: niente più anime perse che vagano tra pagine infinite.

## Domande frequenti

### Che cos'è Aspose.PDF per .NET?
Aspose.PDF per .NET è una libreria che consente agli sviluppatori di creare, manipolare e convertire documenti PDF a livello di programmazione utilizzando il framework .NET.

### Posso creare collegamenti ipertestuali a pagine web esterne?
Sì, Aspose.PDF supporta anche la creazione di collegamenti ipertestuali a URL esterni oltre ai collegamenti ipertestuali locali all'interno del PDF.

### Esiste una prova gratuita per Aspose.PDF?
Assolutamente! Puoi accedere alla prova gratuita da [sito](https://releases.aspose.com/).

### Quali linguaggi di programmazione supporta Aspose?
Aspose offre librerie per vari linguaggi di programmazione, tra cui Java, C++ e Python, tra gli altri.

### Come posso ottenere supporto per i prodotti Aspose?
Puoi cercare supporto tramite [Forum Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}