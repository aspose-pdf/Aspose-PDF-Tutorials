---
"description": "Scopri come creare un rettangolo pieno in un PDF utilizzando Aspose.PDF per .NET con questo tutorial passo passo. Perfetto per sviluppatori di tutti i livelli."
"linktitle": "Crea rettangolo riempito"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Crea rettangolo riempito"
"url": "/it/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Crea rettangolo riempito

## Introduzione

Hai mai desiderato creare PDF visivamente accattivanti programmando? Se sì, sei nel posto giusto! In questo tutorial, ci immergeremo nel mondo di Aspose.PDF per .NET, una potente libreria che ti permette di manipolare i documenti PDF con facilità. Oggi ci concentreremo sulla creazione di un rettangolo pieno all'interno di un file PDF. Che tu sia uno sviluppatore esperto o alle prime armi, questa guida ti guiderà passo passo in modo semplice e coinvolgente. Quindi, prendi il tuo cappello da programmatore e iniziamo!

## Prerequisiti

Prima di passare al codice, ecco alcune cose che devi sapere:

1. Visual Studio: assicurati di avere Visual Studio installato sul tuo computer. È un IDE fantastico per lo sviluppo .NET.
2. Aspose.PDF per .NET: è necessario scaricare e installare la libreria Aspose.PDF. La trovi qui [Qui](https://releases.aspose.com/pdf/net/).
3. Conoscenza di base di C#: un po' di familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.

## Importa pacchetti

Per iniziare, devi importare i pacchetti necessari nel tuo progetto C#. Ecco come fare:

### Crea un nuovo progetto

Apri Visual Studio e crea un nuovo progetto C#. Per semplicità, puoi scegliere un'applicazione console.

### Aggiungi riferimento Aspose.PDF

1. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni.
2. Seleziona "Gestisci pacchetti NuGet".
3. Cerca "Aspose.PDF" e installa la versione più recente.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Ora che abbiamo impostato tutto, immergiamoci nel codice!

## Passaggio 1: imposta la directory dei documenti

Per prima cosa, devi specificare il percorso in cui verrà salvato il PDF. Questo è fondamentale perché indica al programma dove creare il file.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Sostituire `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo sul tuo computer in cui vuoi salvare il PDF.

## Passaggio 2: creare un'istanza di documento

Successivamente, creeremo un'istanza di `Document` classe. Questa classe rappresenta il documento PDF con cui lavorerai.

```csharp
// Crea istanza del documento
Document doc = new Document();
```

Questa riga inizializza un nuovo documento PDF che possiamo manipolare.

## Passaggio 3: aggiungere una pagina al documento

Ora aggiungiamo una pagina al nostro documento. Ogni PDF ha bisogno di almeno una pagina, giusto?

```csharp
// Aggiungi pagina alla raccolta di pagine del file PDF
Page page = doc.Pages.Add();
```

Questo codice aggiunge una nuova pagina al documento, consentendoci di disegnare forme su di essa.

## Passaggio 4: creare un'istanza del grafico

Per disegnare forme, dobbiamo creare un `Graph` esempio. Pensa a un grafico come a una tela su cui puoi disegnare diverse forme.

```csharp
// Crea istanza del grafico
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

Qui creiamo un grafico con una larghezza di 100 e un'altezza di 400.

## Passaggio 5: aggiungere il grafico alla pagina

Ora che abbiamo il nostro grafico, aggiungiamolo alla pagina creata in precedenza.

```csharp
// Aggiungi oggetto grafico alla raccolta di paragrafi dell'istanza di pagina
page.Paragraphs.Add(graph);
```

Questa linea collega il grafico alla pagina, rendendolo pronto per essere disegnato.

## Passaggio 6: creare un'istanza rettangolare

Ora creeremo un rettangolo che vogliamo riempire di colore.

```csharp
// Crea istanza di Rectangle
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

In questo codice definiamo la posizione e le dimensioni del rettangolo. I parametri rappresentano le coordinate x e y, la larghezza e l'altezza.

## Passaggio 7: specificare il colore di riempimento

Ora scegliamo un colore per il nostro rettangolo. Per questo esempio, lo riempiremo di rosso.

```csharp
// Specificare il colore di riempimento per l'oggetto grafico
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

Questa riga imposta il colore di riempimento del rettangolo sul rosso. Puoi scegliere qualsiasi colore tu voglia!

## Passaggio 8: aggiungere il rettangolo al grafico

Ora che il nostro rettangolo è pronto, è il momento di aggiungerlo al grafico.

```csharp
// Aggiungi un oggetto rettangolo alla raccolta di forme dell'oggetto Grafico
graph.Shapes.Add(rect);
```

Questo codice aggiunge il rettangolo al grafico, rendendolo parte del nostro disegno.

## Passaggio 9: salvare il documento PDF

Infine, dobbiamo salvare il nostro documento nella directory specificata.

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// Salva file PDF
doc.Save(dataDir);
```

Questo codice salva il file PDF con il nome `CreateFilledRectangle_out.pdf` nella directory specificata in precedenza.

## Passaggio 10: messaggio di conferma

Per farci sapere che tutto è andato liscio, possiamo stampare un messaggio di conferma.

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

Questa riga genererà un messaggio nella console, confermando che il rettangolo riempito è stato creato correttamente.

## Conclusione

Ed ecco fatto! Hai creato con successo un rettangolo pieno in un documento PDF utilizzando Aspose.PDF per .NET. Questa potente libreria apre un mondo di possibilità per la manipolazione dei PDF, permettendoti di creare documenti straordinari a livello di programmazione. Che tu stia generando report, fatture o qualsiasi altro tipo di PDF, Aspose.PDF è la soluzione che fa per te.

## Domande frequenti

### Che cos'è Aspose.PDF per .NET?
Aspose.PDF per .NET è una libreria che consente agli sviluppatori di creare, manipolare e convertire documenti PDF a livello di programmazione.

### Posso usare Aspose.PDF gratuitamente?
Sì, Aspose offre una versione di prova gratuita che puoi utilizzare per esplorare le funzionalità della libreria. Puoi scaricarla. [Qui](https://releases.aspose.com/).

### Esiste un modo per ottenere supporto per Aspose.PDF?
Assolutamente! Puoi ottenere supporto tramite il forum di Aspose. [Qui](https://forum.aspose.com/c/pdf/10).

### Come posso acquistare Aspose.PDF?
Puoi acquistare Aspose.PDF visitando la pagina di acquisto [Qui](https://purchase.aspose.com/buy).

### Quali tipi di forme posso creare con Aspose.PDF?
Utilizzando la libreria Aspose.PDF è possibile creare varie forme, tra cui rettangoli, cerchi, linee e altro ancora.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}