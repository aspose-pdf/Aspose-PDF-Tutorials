---
"description": "Scopri come aggiungere e rimuovere JavaScript da un documento PDF utilizzando Aspose.PDF per .NET. Guida passo passo con tutorial di codice per lo scripting a livello di documento."
"linktitle": "Aggiungi Rimuovi Javascript al documento"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Aggiungi Rimuovi Javascript al documento PDF"
"url": "/it/net/programming-with-document/addremovejavascripttodoc/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi Rimuovi Javascript al documento PDF

## Introduzione

In questa guida, spiegheremo come utilizzare Aspose.PDF per .NET per inserire codice JavaScript in un file PDF e come rimuoverlo quando necessario. Al termine di questo tutorial, avrai una chiara comprensione di come manipolare JavaScript nei PDF senza sforzo.

## Prerequisiti

Prima di immergerci nel codice, ci sono alcune cose che devi impostare:

1. Aspose.PDF per .NET: è necessario che la libreria Aspose.PDF per .NET sia installata nel progetto. Se non è ancora presente, scaricarla da [Pagina di download di Aspose.PDF per .NET](https://releases.aspose.com/pdf/net/).
2. IDE o editor di testo: puoi utilizzare qualsiasi IDE compatibile con .NET, come Visual Studio.
3. Conoscenza di base di C#: questo tutorial presuppone che tu abbia familiarità con C# e con la manipolazione dei PDF.
4. Licenza: assicurati di applicare una licenza valida per evitare limitazioni. Puoi ottenere una licenza temporanea da [Qui](https://purchase.aspose.com/temporary-license/).

## Importa pacchetti

Per iniziare a utilizzare Aspose.PDF per .NET, è necessario importare gli spazi dei nomi necessari nel progetto. Ecco come fare:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Collections;
```

Questi due namespace sono essenziali. `Aspose.Pdf` consente di lavorare con documenti PDF, mentre `System.Collections` verrà utilizzato per gestire le chiavi JavaScript.

Analizziamo l'intero processo di aggiunta e rimozione di JavaScript da un PDF in semplici passaggi.

## Passaggio 1: inizializzare un nuovo documento PDF

La prima cosa da fare è creare un nuovo documento PDF. Questo documento servirà come tela bianca su cui aggiungere JavaScript.

```csharp
Document doc = new Document();
doc.Pages.Add();
```

Qui stiamo inizializzando un nuovo `Document` oggetto e aggiungendovi una pagina vuota. Considera questo come la base del tuo PDF.

## Passaggio 2: aggiungere JavaScript al PDF

Ora che abbiamo un documento, è il momento di aggiungervi del codice JavaScript. Il codice JavaScript nei PDF può essere utilizzato per aggiungere comportamenti personalizzati, come avvisi o convalida dei moduli.

```csharp
doc.JavaScript["func1"] = "function func1() { hello(); }";
doc.JavaScript["func2"] = "function func2() { hello(); }";
```

In questo frammento di codice, stiamo aggiungendo due funzioni JavaScript (`func1` E `func2`) al PDF. Queste funzioni possono svolgere diverse attività, a seconda delle esigenze. Qui, stiamo semplicemente chiamando una funzione segnaposto chiamata `hello()`.

## Passaggio 3: salva il PDF con JavaScript

Dopo aver aggiunto il codice JavaScript desiderato, è il momento di salvare il PDF.

```csharp
doc.Save(dataDir + "AddJavascript.pdf");
```

Questo salverà il documento con JavaScript con il nome `AddJavascript.pdf` nella directory specificata (`dataDir`).

## Passaggio 4: caricare e visualizzare JavaScript nel PDF esistente

Supponiamo di dover controllare o modificare le funzioni JavaScript all'interno di un PDF esistente. Il primo passo è caricare il file PDF e accedere alle chiavi JavaScript.

```csharp
Document doc1 = new Document(dataDir + "AddJavascript.pdf");
IList keys = (System.Collections.IList)doc1.JavaScript.Keys;
```

Stiamo caricando l'esistente `AddJavascript.pdf` e memorizzare le chiavi JavaScript in un elenco. `Keys` La proprietà restituisce i nomi di tutte le funzioni JavaScript associate al documento.

## Passaggio 5: visualizzare le funzioni JavaScript

Possiamo quindi scorrere le funzioni JavaScript per vedere cosa è disponibile nel documento.

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
```

Questo comando visualizzerà il nome di ogni funzione JavaScript e il codice corrispondente nella console. È utile se si desidera verificare quali funzioni sono attualmente presenti nel documento.

## Passaggio 6: rimuovere JavaScript dal PDF

Ora, supponiamo che tu voglia rimuovere una funzione JavaScript specifica, come `func1`Ecco come puoi farlo:

```csharp
doc1.JavaScript.Remove("func1");
Console.WriteLine("Key 'func1' removed ");
```

IL `Remove` Il metodo accetta il nome della funzione JavaScript come argomento e lo elimina dal documento.

## Passaggio 7: verifica la rimozione di JavaScript

Dopo aver rimosso JavaScript, puoi ristampare le funzioni rimanenti per confermarlo `func1` è stato eliminato con successo.

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
Console.WriteLine("Javascript added/removed successfully.");
```

Quest'ultima parte del codice assicura che tutto sia a posto e che le funzioni JavaScript vengano aggiornate correttamente.

## Conclusione

Congratulazioni! Hai appena imparato ad aggiungere e rimuovere codice JavaScript da un documento PDF utilizzando Aspose.PDF per .NET. Questa potente funzionalità può essere utilizzata per una varietà di attività, dall'aggiunta di messaggi dinamici all'esecuzione di calcoli o convalide personalizzati. Manipolando il codice JavaScript all'interno di un PDF, puoi migliorare significativamente l'esperienza utente.

## Domande frequenti

### Posso aggiungere più funzioni JavaScript a un singolo PDF?
Assolutamente! Puoi aggiungere tutte le funzioni JavaScript di cui hai bisogno utilizzando `doc.JavaScript` collezione.

### Cosa succede se provo a rimuovere una funzione JavaScript inesistente?
Se la funzione non esiste, `Remove` il metodo non genererà un errore, ma non rimuoverà nulla.

### È possibile eseguire JavaScript non appena si apre il PDF?
Sì! Puoi configurare JavaScript per l'esecuzione in base a determinati trigger, come l'apertura del documento o il clic su un pulsante.

### Posso modificare il codice JavaScript dopo averlo aggiunto al PDF?
Sì, puoi caricare un PDF esistente, accedere al suo JavaScript, modificare il codice e salvare nuovamente il documento.

### La rimozione di JavaScript influisce sul resto del contenuto del PDF?
No, la rimozione di JavaScript influisce solo sullo script. Il contenuto del PDF rimane invariato.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}