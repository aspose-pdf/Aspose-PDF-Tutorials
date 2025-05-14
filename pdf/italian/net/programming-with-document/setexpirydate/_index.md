---
"description": "Scopri come impostare una data di scadenza nei file PDF utilizzando Aspose.PDF per .NET. Migliora la sicurezza dei documenti con questa guida passo passo."
"linktitle": "Imposta la data di scadenza nel file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Imposta la data di scadenza nel file PDF"
"url": "/it/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Imposta la data di scadenza nel file PDF

## Introduzione

Nell'era digitale odierna, gestire e proteggere i documenti è più cruciale che mai. Immagina di inviare un PDF che diventa automaticamente inaccessibile dopo una certa data. Sembra magia, vero? Beh, con Aspose.PDF per .NET, puoi facilmente impostare una data di scadenza per i tuoi file PDF. Questa funzione è particolarmente utile per i documenti sensibili che devono essere protetti dopo un certo periodo di tempo. In questo tutorial, ti guideremo passo dopo passo nella procedura di impostazione di una data di scadenza in un file PDF. Quindi, prendi il tuo cappello da programmatore e iniziamo!

## Prerequisiti

Prima di iniziare, ecco alcune cose che devi sapere:

1. Ambiente di sviluppo: assicurati di aver configurato un ambiente di sviluppo .NET. Potrebbe essere Visual Studio o qualsiasi altro IDE che supporti .NET.
2. Aspose.PDF per .NET: è necessario installare la libreria Aspose.PDF. Se non l'avete ancora fatto, potete scaricarla da [Qui](https://releases.aspose.com/pdf/net/).
3. Conoscenza di base di C#: questo tutorial presuppone una conoscenza di base della programmazione in C#. Se non hai familiarità con C#, non preoccuparti! Lo renderemo semplice e diretto.

## Importa pacchetti

Per iniziare a usare Aspose.PDF, è necessario importare gli spazi dei nomi necessari nel progetto C#. Ecco come fare:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Questi namespace forniscono l'accesso alle funzionalità principali richieste per lavorare con documenti PDF in Aspose.PDF.

## Passaggio 1: imposta la directory dei documenti

Per prima cosa, devi specificare il percorso della directory dei tuoi documenti. È qui che verrà salvato il PDF di output. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Sostituire `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo in cui vuoi salvare il file PDF. È come dire al tuo programma: "Ehi, ecco dove tengo i miei file!"

## Passaggio 2: creare un'istanza dell'oggetto documento

Successivamente, è necessario creare una nuova istanza di `Document` classe. Questa è la tua tela su cui creerai il tuo PDF.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Pensa al `Document` L'oggetto è come un foglio bianco. Puoi aggiungere contenuti a tuo piacimento!

## Passaggio 3: aggiungere una pagina al PDF

Ora che hai impostato il tuo documento, è il momento di aggiungere una pagina. È qui che andranno i tuoi contenuti.

```csharp
doc.Pages.Add();
```

Hai appena creato una nuova pagina nel tuo PDF. È come aggiungere una nuova pagina al tuo quaderno, dove puoi annotare i tuoi pensieri.

## Passaggio 4: aggiungere testo alla pagina

Rendiamo questa pagina un po' più interessante aggiungendo del testo. Aggiungeremo un semplice messaggio "Hello World".

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

Questa riga di codice aggiunge un frammento di testo alla prima pagina del tuo PDF. È come scrivere un titolo in cima alla pagina!

## Passaggio 5: creare JavaScript per la data di scadenza

Ora arriva la parte divertente! Creerai un'azione JavaScript che controllerà la data di scadenza del PDF. Se la data corrente supera la data di scadenza, un messaggio avviserà l'utente.

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

Ecco cosa sta succedendo:
- Definisci l'anno e il mese di scadenza.
- Ottieni la data odierna.
- Si confronta la data odierna con la data di scadenza.
- Se la data odierna è successiva alla data di scadenza, verrà visualizzato un messaggio!

## Passaggio 6: imposta JavaScript come azione di apertura PDF

Ora devi impostare l'azione JavaScript come azione di apertura per il tuo documento PDF. Ciò significa che JavaScript verrà eseguito non appena il PDF verrà aperto.

```csharp
doc.OpenAction = javaScript;
```

Questa riga indica al PDF di eseguire il codice JavaScript quando qualcuno lo apre. È come impostare un promemoria che si attiva non appena si apre il calendario!

## Passaggio 7: salvare il documento PDF

Infine, è il momento di salvare il documento PDF con la funzione data di scadenza. 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

Questa riga salva il PDF nella directory specificata con il nome "SetExpiryDate_out.pdf". È come mettere la tua opera d'arte finita in una cornice!

## Conclusione

Ed ecco fatto! Hai creato con successo un file PDF con data di scadenza utilizzando Aspose.PDF per .NET. Questa funzionalità non solo migliora la sicurezza, ma garantisce anche che le informazioni sensibili siano tenute sotto controllo. Che tu stia inviando contratti, report o altri documenti importanti, impostare una data di scadenza può fare davvero la differenza.

## Domande frequenti

### Che cos'è Aspose.PDF per .NET?
Aspose.PDF per .NET è una potente libreria che consente agli sviluppatori di creare, manipolare e convertire documenti PDF nelle applicazioni .NET.

### Posso usare Aspose.PDF gratuitamente?
Sì, puoi utilizzare una versione di prova gratuita di Aspose.PDF. Puoi scaricarla. [Qui](https://releases.aspose.com/).

### Come posso acquistare Aspose.PDF?
Puoi acquistare Aspose.PDF visitando il [pagina di acquisto](https://purchase.aspose.com/buy).

### Cosa succede se ho bisogno di supporto?
Se hai domande o hai bisogno di assistenza, puoi visitare il [Forum di supporto di Aspose](https://forum.aspose.com/c/pdf/10).

### Posso ottenere una licenza temporanea per Aspose.PDF?
Sì, puoi richiedere una licenza temporanea [Qui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}