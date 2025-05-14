---
"description": "Sfrutta la potenza di Aspose.PDF per .NET. Scopri come impostare JavaScript nei campi dei moduli con la nostra guida passo passo."
"linktitle": "Imposta Java Script"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Imposta Java Script"
"url": "/it/net/programming-with-forms/set-java-script/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Imposta Java Script

## Introduzione

La creazione di PDF dinamici e interattivi può migliorare significativamente l'esperienza utente, soprattutto quando si integrano moduli e campi in un documento. Una potente libreria che rende possibile tutto questo è Aspose.PDF per .NET. In questo articolo, approfondiremo la configurazione di JavaScript per i campi modulo utilizzando Aspose.PDF, garantendo che i PDF non solo abbiano un aspetto gradevole, ma funzionino anche in modo impeccabile.

## Prerequisiti

Prima di iniziare a scrivere codice, assicuriamoci di avere tutto il necessario per seguire il tutto senza intoppi:

- Visual Studio (o qualsiasi IDE .NET): assicurati di averlo installato e configurato correttamente.
  
- Libreria Aspose.PDF: ti servirà la versione più recente di questa libreria. Puoi scaricarla. [Qui](https://releases.aspose.com/pdf/net/).

- Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.

- File PDF: dovresti avere un file PDF pronto per il test. Nel nostro esempio, useremo un file denominato `SetJavaScript.pdf`.

- Directory dei documenti: scopri dove sono archiviati i file dei tuoi documenti. Faremo riferimento a questo percorso nel nostro codice.

Una volta soddisfatti questi prerequisiti, quali strumenti utilizzeremo? Scopriamo cosa può fare Aspose.PDF.

## Importa pacchetti

Per iniziare, devi includere gli spazi dei nomi necessari nel tuo progetto C#. Apri il file C# principale e aggiungi le seguenti istruzioni di importazione:

```csharp
using System;
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Questi namespace forniscono l'accesso alle funzionalità PDF e relative ai moduli all'interno della libreria Aspose.PDF.

Pronti a rendere interattivo il vostro PDF? Indossate il vostro cappello da programmatori e analizziamolo passo dopo passo!

## Passaggio 1: definire il percorso del documento

Per prima cosa, dobbiamo specificare la posizione del nostro file PDF. Questo è il punto di partenza per tutto ciò che seguirà. Ecco come fare:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Sostituire `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo in cui si trova il tuo file PDF. Immagina di impostare le coordinate di una mappa del tesoro: devi sapere dove la "X" indica il punto!

## Passaggio 2: caricare il documento PDF

Una volta definita la directory, caricheremo il nostro file PDF. 

```csharp
Document doc = new Document(dataDir + "SetJavaScript.pdf");
```

Questa riga apre il file PDF specificato e lo prepara per la manipolazione. 

## Passaggio 3: accedi al campo del modulo

Ora vogliamo accedere al campo del modulo in cui applicheremo il nostro JavaScript. 

```csharp
TextBoxField field = (TextBoxField)doc.Form["textbox1"];
```

Qui, supponiamo che ci sia una casella di testo nel tuo PDF denominata `textbox1`Se non hai un campo con questo nome, puoi rinominarlo o modificare il codice di conseguenza. 

## Passaggio 4: imposta le azioni JavaScript

Ora aggiungiamo qualche funzionalità alla nostra casella di testo! Imposteremo azioni JavaScript che verranno attivate in base a determinati eventi. 

```csharp
field.Actions.OnModifyCharacter = new JavascriptAction("AFNumber_Keystroke(2, 1, 1, 0, \"\", true)");
field.Actions.OnFormat = new JavascriptAction("AFNumber_Format(2, 1, 1, 0, \"\", true)");
```

Ecco cosa sta succedendo:
- OnModifyCharacter: questa funzione JavaScript specifica il comportamento del campo quando un carattere viene modificato. In questo caso, consente due cifre decimali dopo il numero, senza separatore.
- OnFormat: garantisce che quando l'utente formatta il numero, questo rispetti la stessa regola.

Impostando queste azioni, stiamo sostanzialmente dando una personalità alla nostra casella di testo, come se le stessimo insegnando un passo di danza!

## Passaggio 5: inizializzare il valore del campo

Ora diamo un punto di partenza alla nostra casella di testo impostando un valore iniziale. 

```csharp
field.Value = "123";
```

Questa riga imposta "123" come valore precompilato nella casella di testo. È come preparare un palco per uno spettacolo.

## Passaggio 6: salvare il PDF modificato

Infine, dopo aver apportato tutte queste modifiche, dobbiamo salvare il documento.

```csharp
dataDir = dataDir + "Restricted_out.pdf";
doc.Save(dataDir);
```

Questo aggiorna il file originale con le tue modifiche e lo salva come `Restricted_out.pdf`Considerate questo come il suggello del destino del nostro PDF: una volta salvato, è pronto per il mondo!

## Passaggio 7: conferma il successo

Infine, controlliamo che tutto sia andato liscio. 

```csharp
Console.WriteLine("\nJavaScript on form field setup successfully.\nFile saved at " + dataDir);
```

L'esecuzione di questo messaggio ti rassicurerà che l'operazione è stata completata con successo, proprio come ricevere un applauso dal pubblico dopo una grande esibizione.

## Conclusione

Congratulazioni! Hai configurato correttamente JavaScript per i campi modulo in un PDF utilizzando Aspose.PDF per .NET. Questo tutorial non solo ti ha fornito gli strumenti per migliorare l'interazione con l'utente, ma ti ha anche permesso di personalizzare i tuoi documenti come un professionista. Che tu stia lavorando con moduli in fatture, sondaggi o altri PDF interattivi, le possibilità sono davvero infinite.

### Domande frequenti

### Che cos'è Aspose.PDF per .NET?  
Aspose.PDF è una libreria progettata per creare, modificare e manipolare file PDF all'interno di applicazioni .NET, offrendo potenti funzionalità PDF.

### Ho bisogno di una licenza per utilizzare Aspose.PDF?  
Sebbene sia disponibile una prova gratuita, è necessaria una licenza per un utilizzo completo e senza limitazioni. È possibile acquistare una licenza. [Qui](https://purchase.aspose.com/buy).

### Posso impostare JavaScript su altri tipi di campi del modulo?  
Assolutamente! Aspose.PDF consente azioni JavaScript su vari campi del modulo, come caselle di controllo, pulsanti di opzione e menu a discesa.

### Come posso ottenere supporto per i problemi relativi ad Aspose.PDF?  
Puoi accedere al supporto tramite il loro [foro](https://forum.aspose.com/c/pdf/10) per qualsiasi domanda o problema.

### Esiste un modo per provare Aspose.PDF senza acquistarlo?  
Sì! Aspose fornisce un [prova gratuita](https://releases.aspose.com/) per testare le funzionalità della libreria prima di procedere all'acquisto.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}