---
"description": "Scopri come creare pulsanti di scelta allineati orizzontalmente e verticalmente in un PDF utilizzando Aspose.PDF per .NET con questo tutorial passo passo."
"linktitle": "Pulsanti di scelta orizzontali e verticali"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Pulsanti di scelta orizzontali e verticali"
"url": "/it/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Pulsanti di scelta orizzontali e verticali

## Introduzione

La creazione di moduli PDF interattivi può migliorare significativamente l'esperienza utente, soprattutto quando si tratta di raccogliere informazioni. Uno degli elementi più comuni dei moduli è il pulsante di opzione, che consente agli utenti di selezionare un'opzione da un set. In questo tutorial, esploreremo come creare pulsanti di opzione allineati orizzontalmente e verticalmente utilizzando Aspose.PDF per .NET. Che tu sia uno sviluppatore esperto o alle prime armi, questa guida ti guiderà passo dopo passo attraverso il processo, assicurandoti di comprendere appieno ogni passaggio.

## Prerequisiti

Prima di immergerti nel codice, ecco alcuni prerequisiti che dovresti avere:

1. Aspose.PDF per .NET: assicurati di aver installato la libreria Aspose.PDF. Puoi scaricarla da [sito](https://releases.aspose.com/pdf/net/).
2. Visual Studio: un ambiente di sviluppo in cui puoi scrivere e testare il tuo codice.
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.

## Importa pacchetti

Per iniziare, devi importare i pacchetti necessari nel tuo progetto C#. Ecco come fare:

### Crea un nuovo progetto

Apri Visual Studio e crea un nuovo progetto C#. Per semplicità, puoi scegliere un'applicazione console.

### Aggiungi riferimento Aspose.PDF

1. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni.
2. Seleziona "Gestisci pacchetti NuGet".
3. Cerca "Aspose.PDF" e installa la versione più recente.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

Ora che hai impostato tutto, analizziamo il codice per creare pulsanti di scelta allineati orizzontalmente e verticalmente.

## Passaggio 1: impostare la directory dei documenti

In questo passaggio definiremo il percorso verso la directory in cui verranno archiviati i documenti PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Sostituire `"YOUR DOCUMENT DIRECTORY"` Con il percorso effettivo in cui si desidera salvare il file PDF. Questo è fondamentale perché indica al programma dove cercare i file di input e dove salvare l'output.

## Passaggio 2: caricare il documento PDF esistente

Successivamente, dobbiamo caricare il documento PDF con cui lavoreremo. Questo viene fatto utilizzando `FormEditor` classe.

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

Qui creiamo un'istanza di `FormEditor` e associarlo a un file PDF esistente denominato `input.pdf`Assicurati che questo file esista nella directory specificata.

## Passaggio 3: configurare le proprietà del pulsante di scelta

Ora impostiamo alcune proprietà per i nostri pulsanti di opzione. Tra queste, la distanza tra i pulsanti, il loro orientamento e le loro dimensioni.

```csharp
formEditor.RadioGap = 4; // Distanza tra le opzioni dei pulsanti di scelta
formEditor.RadioHoriz = true; // Impostare su vero per l'allineamento orizzontale
formEditor.RadioButtonItemSize = 20; // Dimensione del pulsante di scelta
formEditor.Facade.BorderWidth = 1; // Larghezza del bordo
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // Colore del bordo
```

Queste proprietà aiuteranno a definire come appariranno i pulsanti di scelta nel PDF. `RadioGap` proprietà controlla lo spazio tra i pulsanti, mentre `RadioHoriz` determina la loro disposizione.

## Passaggio 4: aggiungere pulsanti di scelta orizzontali

Aggiungiamo ora i pulsanti di scelta orizzontali al PDF.

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

In questo codice definiamo gli elementi per i pulsanti di scelta e li aggiungiamo al PDF. `AddField` Il metodo accetta diversi parametri, tra cui il tipo di campo, il nome del campo e le coordinate per il posizionamento.

## Passaggio 5: aggiungere pulsanti di scelta verticali

Successivamente, aggiungeremo i pulsanti di opzione verticali. Per farlo, dobbiamo ripristinare l'orientamento verticale.

```csharp
formEditor.RadioHoriz = false; // Impostare su falso per l'allineamento verticale
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

Proprio come prima, definiamo gli elementi e li aggiungiamo al PDF, ma questa volta saranno allineati verticalmente.

## Passaggio 6: salvare il documento PDF

Infine, dobbiamo salvare il documento PDF modificato.

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

Questo codice salva il PDF con i nuovi pulsanti di opzione aggiunti. Assicurati di controllare la directory specificata per il file di output.

## Conclusione

Creare pulsanti di opzione in un PDF utilizzando Aspose.PDF per .NET è un processo semplice. Seguendo i passaggi descritti in questo tutorial, puoi aggiungere facilmente pulsanti di opzione allineati orizzontalmente e verticalmente ai tuoi moduli PDF. Questo non solo migliora l'interattività dei tuoi documenti, ma migliora anche l'esperienza utente complessiva. Quindi, provalo!

## Domande frequenti

### Che cos'è Aspose.PDF per .NET?
Aspose.PDF per .NET è una potente libreria che consente agli sviluppatori di creare, manipolare e convertire documenti PDF a livello di programmazione.

### Posso usare Aspose.PDF gratuitamente?
Sì, Aspose offre una versione di prova gratuita che puoi utilizzare per valutare la libreria. Puoi scaricarla. [Qui](https://releases.aspose.com/).

### Come posso ottenere supporto per Aspose.PDF?
Puoi ottenere supporto visitando il [Forum di Aspose](https://forum.aspose.com/c/pdf/10).

### È possibile creare altri elementi del modulo con Aspose.PDF?
Assolutamente sì! Aspose.PDF supporta vari elementi dei moduli, inclusi campi di testo, caselle di controllo e menu a discesa.

### Dove posso acquistare Aspose.PDF per .NET?
Puoi acquistare Aspose.PDF per .NET da [pagina di acquisto](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}