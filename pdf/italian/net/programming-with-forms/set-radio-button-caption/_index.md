---
"description": "Scopri come impostare le didascalie dei pulsanti di opzione nei PDF utilizzando Aspose.PDF per .NET. Questa guida dettagliata ti guiderà passo passo nel caricamento, nella modifica e nel salvataggio dei tuoi moduli PDF."
"linktitle": "Imposta la didascalia del pulsante di scelta"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Imposta la didascalia del pulsante di scelta"
"url": "/it/net/programming-with-forms/set-radio-button-caption/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Imposta la didascalia del pulsante di scelta

## Introduzione

Se ti stai cimentando nella manipolazione di PDF con Aspose.PDF per .NET, ti aspetta una vera sorpresa! Oggi ci concentreremo su una funzionalità pratica: l'impostazione delle didascalie dei pulsanti di opzione nei moduli PDF. I pulsanti di opzione sono essenziali per i moduli utente in cui è necessario scegliere tra una serie di opzioni. Immaginali come domande a risposta multipla in cui è consentita una sola risposta. Questo tutorial ti guiderà attraverso il processo di aggiornamento delle didascalie dei pulsanti di opzione in un modulo PDF, in modo che i tuoi documenti siano interattivi e intuitivi. 

## Prerequisiti

Prima di immergerti nel codice, ecco alcune cose che devi assicurarti di avere:

1. Aspose.PDF per .NET: assicurati di aver installato la libreria Aspose.PDF. Questa libreria ti aiuterà a manipolare i file PDF a livello di codice.
2. Ambiente di sviluppo: dovresti avere configurato un ambiente di sviluppo .NET, come Visual Studio.
3. Esempio di modulo PDF: per questo tutorial, avrai bisogno di un esempio di modulo PDF con pulsanti di opzione. Puoi utilizzare qualsiasi modulo PDF esistente o crearne uno nuovo con pulsanti di opzione.
4. Conoscenza di base di C#: questa guida presuppone una conoscenza di base dei concetti di programmazione C# e .NET.

Se non hai ancora installato Aspose.PDF per .NET o hai bisogno di una licenza temporanea, puoi [scaricalo qui](https://releases.aspose.com/pdf/net/) O [ottenere una licenza temporanea](https://purchase.aspose.com/temporary-license/).

## Importa pacchetti

Per iniziare, è necessario importare i pacchetti necessari nel progetto C#. Ecco come includere la libreria Aspose.PDF:

```csharp
using System;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
using Aspose.Pdf.Text;
```

Assicurati di aggiungere questi pacchetti al tuo progetto tramite NuGet o il tuo metodo preferito.

## Passaggio 1: carica il modulo PDF

Per prima cosa, è necessario caricare il modulo PDF che contiene i pulsanti di scelta. `Aspose.Pdf.Facades.Form` La classe viene utilizzata a questo scopo. Ecco come fare:

```csharp
// Definisci il percorso verso la directory dei tuoi documenti
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Carica il modulo PDF di origine
Aspose.Pdf.Facades.Form form1 = new Aspose.Pdf.Facades.Form(dataDir + "RadioButtonField.pdf");
Document PDF_Template_PDF_HTML = new Document(dataDir + "RadioButtonField.pdf");
```

In questo frammento di codice:
- `dataDir` specifica il percorso in cui si trova il PDF.
- `Form` La classe viene utilizzata per interagire con i campi del modulo all'interno del PDF.
- `Document` La classe fornisce l'accesso alle pagine del documento PDF.

## Passaggio 2: scorrere i campi dei pulsanti di scelta

Successivamente, dovrai scorrere i campi del modulo per identificare e manipolare i campi dei pulsanti di scelta:

```csharp
foreach (var item in form1.FieldNames)
{
    Console.WriteLine(item.ToString());
    Dictionary<string, string> radioOptions = form1.GetButtonOptionValues(item);
```

In questo ciclo:
- `FieldNames` fornisce un elenco di tutti i nomi dei campi nel PDF.
- `GetButtonOptionValues(item)` recupera le opzioni disponibili per ciascun pulsante di scelta.

## Passaggio 3: modificare le opzioni del pulsante di scelta

Una volta identificati i campi del pulsante di opzione, è possibile modificarne le opzioni. Per farlo, è necessario eseguire il cast del campo in `RadioButtonField` e aggiornarne le opzioni:

```csharp
    if (item.Contains("radio1"))
    {
        Aspose.Pdf.Forms.RadioButtonField field0 = PDF_Template_PDF_HTML.Form[item] as Aspose.Pdf.Forms.RadioButtonField;
        Aspose.Pdf.Forms.RadioButtonOptionField fieldoption = new Aspose.Pdf.Forms.RadioButtonOptionField();
        fieldoption.OptionName = "Yes";
        fieldoption.PartialName = "Yesname";
```

Qui:
- Controlliamo se il nome del campo contiene "radio1" per identificare il campo specifico del pulsante di scelta che vogliamo modificare.
- `RadioButtonField` viene convertito dai campi del modulo per apportare modifiche specifiche.

## Passaggio 4: imposta la didascalia per il pulsante di scelta

Per impostare o aggiornare la didascalia per il pulsante di scelta, sarà necessario creare un `TextFragment` utilizzare `TextBuilder` per posizionarlo nella posizione desiderata:

```csharp
        var updatedFragment = new Aspose.Pdf.Text.TextFragment("test123");
        updatedFragment.TextState.Font = FontRepository.FindFont("Arial");
        updatedFragment.TextState.FontSize = 10;
        updatedFragment.TextState.LineSpacing = 6.32f;

        // Crea oggetto TextParagraph
        TextParagraph par = new TextParagraph();
        // Imposta la posizione del paragrafo
        par.Position = new Position(field0.Rect.LLX, field0.Rect.LLY + updatedFragment.TextState.FontSize);
        // Specificare la modalità di interruzione di parola
        par.FormattingOptions.WrapMode = TextFormattingOptions.WordWrapMode.ByWords;
        // Aggiungi un nuovo TextFragment al paragrafo
        par.AppendLine(updatedFragment);
        // Aggiungere il TextParagraph utilizzando TextBuilder
        TextBuilder textBuilder = new TextBuilder(PDF_Template_PDF_HTML.Pages[1]);
        textBuilder.AppendParagraph(par);
```

In questa parte:
- `TextFragment` viene utilizzato per definire il testo e il suo aspetto.
- `TextParagraph` aiuta a posizionare e formattare il testo.
- `TextBuilder` aggiunge il testo alla pagina specificata del PDF.

## Passaggio 5: salvare il PDF aggiornato

Infine, salva il PDF aggiornato in un nuovo file:

```csharp
        field0.DeleteOption("item1");
    }
}
PDF_Template_PDF_HTML.Save(dataDir + "RadioButtonField_out.pdf");
```

Ciò garantirà che:
- Le modifiche vengono applicate al PDF.
- L'opzione originale del pulsante di scelta è stata rimossa come specificato.

## Conclusione

Modificare le didascalie dei pulsanti di opzione in un modulo PDF utilizzando Aspose.PDF per .NET può migliorare notevolmente l'interattività e l'usabilità dei documenti. Con i passaggi descritti in questo tutorial, puoi caricare facilmente un PDF, aggiornare le opzioni dei pulsanti di opzione e salvare le modifiche. Questo approccio è utile per la gestione dei moduli e garantisce che i PDF soddisfino esattamente le esigenze dei tuoi utenti. Scopri Aspose.PDF ed esplora le sue funzionalità per altre manipolazioni PDF!

## Domande frequenti

### Posso aggiornare più campi dei pulsanti di scelta contemporaneamente?
Sì, puoi scorrere tutti i campi dei pulsanti di scelta e applicare le modifiche necessarie.

### Ho bisogno di una licenza per utilizzare Aspose.PDF?
È possibile iniziare con una prova gratuita, ma per un utilizzo prolungato è necessaria una licenza. [Ottieni una licenza qui](https://purchase.aspose.com/buy).

### Come posso testare le modifiche prima di salvare il PDF?
Puoi visualizzare l'anteprima del PDF nel tuo ambiente di sviluppo oppure utilizzare un visualizzatore PDF per verificare le modifiche.

### Aspose.PDF è compatibile con tutte le versioni di .NET?
Aspose.PDF supporta diverse versioni di .NET. Assicurati di verificare la compatibilità con la tua versione specifica di .NET.

### Posso manipolare altri campi del modulo in modo simile?
Sì, tecniche simili possono essere applicate ad altri tipi di campi modulo nei documenti PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}