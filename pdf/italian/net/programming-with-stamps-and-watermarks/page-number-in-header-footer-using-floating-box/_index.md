---
"description": "Aggiungi facilmente i numeri di pagina nell'intestazione e nel piè di pagina del tuo PDF utilizzando una casella mobile con Aspose.PDF per .NET in questo tutorial passo dopo passo."
"linktitle": "Numero di pagina nell'intestazione e nel piè di pagina tramite casella mobile"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Numero di pagina nell'intestazione e nel piè di pagina tramite casella mobile"
"url": "/it/net/programming-with-stamps-and-watermarks/page-number-in-header-footer-using-floating-box/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Numero di pagina nell'intestazione e nel piè di pagina tramite casella mobile

## Introduzione

Quando si tratta di gestire i documenti PDF a livello di codice, Aspose.PDF per .NET si distingue come uno strumento eccezionale. Semplifica il modo in cui creiamo, modifichiamo e manipoliamo i file PDF nelle applicazioni .NET. Che tu stia generando fatture, report o qualsiasi altro tipo di documento, aggiungere numeri di pagina in modo elegante può migliorare la professionalità e l'organizzazione dei tuoi PDF. In questo tutorial, approfondiamo come aggiungere numeri di pagina nell'intestazione e nel piè di pagina del tuo PDF utilizzando un riquadro mobile. Pronti a iniziare? Iniziamo!

## Prerequisiti

Prima di iniziare questo entusiasmante viaggio nel regno della manipolazione dei PDF, ecco alcune cose che devi sapere:

### Configurazione dell'ambiente .NET
Assicuratevi di avere un ambiente di sviluppo .NET. Potete usare Visual Studio, una scelta diffusa tra gli sviluppatori per le applicazioni .NET.

### Libreria Aspose.PDF
Installa la libreria Aspose.PDF. Puoi scaricarla facilmente dal sito web:

- [Scarica Aspose.PDF per .NET](https://releases.aspose.com/pdf/net/)

### Conoscenza di base della programmazione C#
Una conoscenza di base del linguaggio C# ti aiuterà ad apprendere i concetti e gli spezzoni di codice presentati in questo tutorial.

### Accesso alla documentazione
È sempre utile avere il [Documentazione Aspose.PDF](https://reference.aspose.com/pdf/net/) utile per la consultazione e l'esplorazione più approfondita di eventuali funzionalità aggiuntive.

## Importa pacchetti

Per iniziare, dovrai importare i pacchetti necessari nel tuo progetto. Questo garantirà che l'assembly Aspose.PDF sia accessibile e utilizzabile nel tuo codice. Ecco come fare:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ora, scomponiamo il processo di aggiunta dei numeri di pagina utilizzando un riquadro mobile in passaggi gestibili. Seguiteci mentre spiegheremo tutto.

## Passaggio 1: configura l'ambiente del documento

Iniziamo specificando la directory in cui verrà archiviato il documento PDF. Questo è fondamentale perché determina dove verrà salvato il file di output.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Sostituire `YOUR DOCUMENT DIRECTORY` con il percorso di tua scelta in cui vuoi salvare il file PDF di output.

## Passaggio 2: creare un'istanza del documento

Il passaggio successivo è la creazione di un nuovo documento PDF. Ciò comporta l'utilizzo di `Document` classe dalla libreria Aspose.PDF.

```csharp
// Crea un'istanza del documento
Aspose.Pdf.Document pdf = new Aspose.Pdf.Document();
```
Qui creiamo una nuova istanza di `Document` classe, che funge da tela per la nostra manipolazione.

## Passaggio 3: aggiungi una nuova pagina

Ora aggiungiamo una pagina al nostro documento PDF. Ogni PDF ha bisogno di almeno una pagina, giusto?

```csharp
// Aggiungere una pagina al documento PDF
Aspose.Pdf.Page page = pdf.Pages.Add();
```
Questo frammento di codice aggiunge una nuova pagina al nostro documento, rendendolo pronto a ricevere contenuti, tra cui la nostra casella mobile con i numeri di pagina.

## Passaggio 4: creare una casella mobile

Successivamente, è il momento di creare la nostra casella mobile che conterrà il numero di pagina. `FloatingBox` La classe ci consente di posizionare liberamente i contenuti sulla pagina.

```csharp
// Inizializza una nuova istanza della classe FloatingBox
Aspose.Pdf.FloatingBox box1 = new Aspose.Pdf.FloatingBox(140, 80);
```
Qui, i parametri `(140, 80)` Specifica la larghezza e l'altezza del riquadro mobile. Puoi regolare questi valori in base alle tue preferenze di layout.

## Fase 5: Posizionamento della scatola galleggiante

Il posizionamento è fondamentale! Devi determinare dove apparirà il numero di pagina sulla pagina. Lavorerai con `Left` E `Top` proprietà per specificare la posizione.

```csharp
// Valore float che indica la posizione a sinistra del paragrafo
box1.Left = 2;
// Valore float che indica la posizione superiore del paragrafo
box1.Top = 10;
```
Questi valori determinano il posizionamento del riquadro mobile sulla pagina. Sentiti libero di sperimentarli per trovare la soluzione migliore per il tuo documento.

## Passaggio 6: aggiungere testo con la macro del numero di pagina

Ora aggiungeremo una stringa che mostra dinamicamente il numero di pagina. È qui che avviene la magia!

```csharp
// Aggiungere le macro alla raccolta di paragrafi del FloatingBox
box1.Paragraphs.Add(new Aspose.Pdf.Text.TextFragment("Page: ($p/ $P )"));
```
In questo caso, `($p/ $P)` è una macro che visualizzerà il numero di pagina corrente (`$p`) e il numero totale di pagine (`$P`). Di conseguenza, formatta il testo in modo che venga visualizzato qualcosa del tipo "Pagina: 1/5".

## Passaggio 7: aggiungere la casella mobile alla pagina

È il momento di aggiungere la casella mobile, insieme al testo del numero di pagina, alla pagina appena creata.

```csharp
// Aggiungi un floatingBox alla pagina
page.Paragraphs.Add(box1);
```
Questa riga sostanzialmente incorpora la casella mobile nella pagina, rendendola parte del layout del documento. 

## Passaggio 8: salva il documento

Infine, non dimenticare di salvare il tuo lavoro! L'ultimo passaggio è salvare il documento PDF con un nome file appropriato.

```csharp
// Salva il documento
pdf.Save(dataDir + "PageNumberinHeaderFooterUsingFloatingBox_out.pdf");
```
Assicurati che il percorso specificato includa il nome file desiderato. Ora il tuo fantastico PDF con i numeri di pagina è stato creato! 

## Conclusione

Ed ecco fatto, gente! Aggiungere i numeri di pagina all'intestazione e al piè di pagina del vostro PDF utilizzando Aspose.PDF per .NET è semplicissimo. Con poche righe di codice, avete intrapreso un percorso verso la padronanza dell'elaborazione dei documenti nelle vostre applicazioni. Non esitate a sperimentare con layout e formattazioni diversi: dopotutto, la creatività non ha limiti! Pronti a generare quel documento professionale? Indossate il vostro cappello da programmatori e iniziate a sperimentare.

## Domande frequenti

### Posso personalizzare l'aspetto del testo del numero di pagina?  
Sì, puoi personalizzare le proprietà del testo, come la dimensione del carattere, il colore e lo stile, regolando il `TextFragment` proprietà.

### Aspose.PDF è gratuito?  
Sebbene Aspose.PDF offra una prova gratuita, è un prodotto a pagamento per l'uso in produzione. Puoi [compralo qui](https://purchase.aspose.com/buy).

### Dove posso trovare una documentazione più dettagliata?  
Puoi trovare una documentazione completa su [Sito di documentazione di Aspose.PDF](https://reference.aspose.com/pdf/net/).

### Come faccio ad applicare intestazioni e piè di pagina a più pagine?  
È possibile scorrere tutte le pagine del documento e applicare la casella mobile a ciascuna di esse in modo simile.

### Cosa succede se ho bisogno di supporto per funzionalità aggiuntive?  
Per qualsiasi ulteriore domanda o supporto, puoi visitare il [Forum Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}