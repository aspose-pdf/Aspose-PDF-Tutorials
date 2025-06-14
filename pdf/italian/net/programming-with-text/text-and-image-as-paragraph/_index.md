---
"description": "Crea PDF con testo e immagini utilizzando Aspose.PDF per .NET. Scopri come aggiungere testo e immagini in linea passo dopo passo."
"linktitle": "Testo e immagine come paragrafo nel file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Testo e immagine come paragrafo nel file PDF"
"url": "/it/net/programming-with-text/text-and-image-as-paragraph/"
"weight": 530
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Testo e immagine come paragrafo nel file PDF

## Introduzione

Nel mondo digitale odierno, i PDF sono un formato di documento universale che la maggior parte di noi incontra quotidianamente. Che si tratti di un report, di un eBook o di una fattura aziendale, i PDF semplificano la condivisione di informazioni su diverse piattaforme. Ma cosa succede se si desidera personalizzare un PDF tramite codice? È qui che entra in gioco Aspose.PDF per .NET. In questo tutorial, vi guideremo nell'inserimento di testo e immagini come paragrafi in linea in un file PDF utilizzando Aspose.PDF per .NET.

## Prerequisiti

Prima di immergerci nel codice, assicuriamoci di avere tutto il necessario per seguirlo senza problemi:

- Libreria Aspose.PDF per .NET: è necessario installare Aspose.PDF per .NET. È possibile scaricarlo. [Qui](https://releases.aspose.com/pdf/net/).
- Visual Studio: funzionerà correttamente qualsiasi versione che supporti .NET.
- Nozioni di base di C#: una certa familiarità con C# sarà utile, ma non preoccuparti: ti guiderò passo passo!
- Documento PDF pronto: se vuoi aggiungere un'immagine personalizzata, tienila a portata di mano.

Puoi anche ottenere una prova gratuita della biblioteca [Qui](https://releases.aspose.com/), oppure se stai lavorando a un progetto su larga scala, prendi in considerazione l'acquisto [Qui](https://purchase.aspose.com/buy)Hai bisogno di maggiori dettagli? Consulta la documentazione. [Qui](https://reference.aspose.com/pdf/net/).

## Importa pacchetti

Per iniziare a utilizzare Aspose.PDF per .NET, è necessario importare gli spazi dei nomi richiesti. Questi spazi dei nomi consentono al codice C# di interagire con le funzionalità di Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

Semplice, vero? Ora passiamo alla parte divertente: creare il tuo file PDF.

## Guida passo passo: creazione di un PDF con testo e immagine in linea

Proviamo a scomporre il tutto in passaggi semplici e digeribili. Immagina di comporre un puzzle: ogni passaggio equivale a trovare e posizionare il pezzo giusto.

## Passaggio 1: inizializzare il documento PDF

Il primo passo è inizializzare un nuovo documento PDF utilizzando Aspose.PDF. Questo documento servirà da base per l'aggiunta di testo e immagini.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Crea un'istanza del documento
Document doc = new Document();
```

Cosa sta succedendo qui? Stiamo semplicemente creando un nuovo documento usando il `Document` classe e definire la directory in cui si desidera salvare il PDF. È come aprire una nuova tela per il tuo capolavoro!

## Passaggio 2: aggiungi una pagina al tuo PDF

Un documento non serve a molto senza pagine, vero? Aggiungiamo una pagina vuota al tuo documento.

```csharp
// Aggiungi pagina alla raccolta di pagine dell'istanza del documento
Page page = doc.Pages.Add();
```

Questo frammento di codice aggiunge una nuova pagina alla raccolta di pagine del tuo documento. Immagina di aprire una pagina vuota in un blocco note.

## Passaggio 3: aggiungere il testo come paragrafo

Successivamente, aggiungeremo un paragrafo di testo. Qui potrai inserire il tuo messaggio o titolo.

```csharp
// Crea frammento di testo
TextFragment text = new TextFragment("Hello World.. ");
// Aggiungi frammento di testo alla raccolta di paragrafi dell'oggetto Pagina
page.Paragraphs.Add(text);
```

Qui creiamo un `TextFragment` oggetto per contenere il testo "Hello World...", che viene poi aggiunto alla pagina come paragrafo. È come scrivere la prima frase del tuo documento PDF.

## Passaggio 4: aggiungere un'immagine come paragrafo in linea

Ora che abbiamo il testo, rendiamo il tutto più interessante aggiungendo un'immagine come paragrafo in linea. Un paragrafo in linea significa semplicemente che l'immagine apparirà subito dopo il testo, proprio come le immagini vengono visualizzate nei documenti Word.

```csharp
// Crea un'istanza di immagine
Aspose.Pdf.Image image = new Aspose.Pdf.Image();
// Imposta l'immagine come paragrafo in linea in modo che appaia subito dopo 
// L'oggetto paragrafo precedente (TextFragment)
image.IsInLineParagraph = true;
// Specificare il percorso del file immagine 
image.File = dataDir + "aspose-logo.jpg";
```

In questo frammento, creiamo un `Image` object, indicagli di allinearsi in linea con il testo e specifica il percorso del file immagine. Questo equivale a incollare un'immagine subito dopo una frase in un documento. Puoi sostituire "aspose-logo.jpg" con l'immagine desiderata.

## Passaggio 5: imposta la dimensione dell'immagine (facoltativo)

Vuoi ridimensionare l'immagine? Nessun problema. Aspose.PDF ti offre la possibilità di regolare altezza e larghezza dell'immagine prima di aggiungerla al documento.

```csharp
// Imposta l'altezza dell'immagine (facoltativo)
image.FixHeight = 30;
// Imposta la larghezza dell'immagine (facoltativo)
image.FixWidth = 100;
```

Questa parte è facoltativa, ma ti aiuta a controllare le dimensioni dell'immagine nel tuo PDF. È come ridimensionare una foto prima di stamparla.

## Passaggio 6: aggiungere l'immagine alla raccolta di paragrafi

Abbiamo preparato l'immagine. Ora inseriamola nel documento come paragrafo in linea.

```csharp
// Aggiungi immagine alla raccolta di paragrafi dell'oggetto pagina
page.Paragraphs.Add(image);
```

Questa riga aggiunge l'immagine subito dopo il testo nella raccolta di paragrafi. È come premere il pulsante "Inserisci immagine" in un editor di testo.

## Passaggio 7: aggiungere un altro paragrafo di testo in linea

E se volessi aggiungere altro testo subito dopo l'immagine? Proviamo a farlo inserendo un altro frammento di testo in linea.

```csharp
// Reinizializza l'oggetto TextFragment con contenuti diversi
text = new TextFragment(" Hello Again..");
// Imposta TextFragment come paragrafo in linea
text.IsInLineParagraph = true;
// Aggiungi il TextFragment appena creato alla raccolta di paragrafi della pagina
page.Paragraphs.Add(text);
```

Stiamo riutilizzando il `TextFragment` Oggetto qui con nuovo testo ("Ciao di nuovo...") e inserendolo in linea, subito dopo l'immagine. Questo conferisce al PDF un aspetto fluido e coerente.

## Passaggio 8: salvare il documento PDF

Ci siamo quasi! Ora salviamo il documento nella directory specificata.

```csharp
dataDir = dataDir + "TextAndImageAsParagraph_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nText and image added successfully as inline paragraphs.\nFile saved at " + dataDir);
```

Quest'ultimo passaggio salva il file nella tua directory con il nome "TextAndImageAsParagraph_out.pdf". Congratulazioni: hai creato un PDF con testo e immagini in linea!

## Conclusione

Ed ecco fatto: creare un PDF con testo e immagini come paragrafi in linea utilizzando Aspose.PDF per .NET è semplice come seguire questi passaggi. Con poche righe di codice, puoi aggiungere contenuti dinamici ai tuoi file PDF, rendendoli visivamente più accattivanti e professionali. Che si tratti di un report aziendale o di un eBook, avere il controllo sul layout dei tuoi PDF può fare la differenza.

## Domande frequenti

### Posso aggiungere più immagini come paragrafi in linea?  
Sì, puoi aggiungere più immagini creando immagini separate `Image` oggetti e aggiungerli alla raccolta di paragrafi.

### Posso controllare la posizione del testo e dell'immagine nel PDF?  
Sì, utilizzando proprietà come i margini, puoi controllare il posizionamento preciso del testo e delle immagini.

### Aspose.PDF per .NET è gratuito?  
No, è un prodotto con licenza, ma puoi ottenerne uno [prova gratuita](https://releases.aspose.com/) o acquistare una licenza [Qui](https://purchase.aspose.com/buy).

### Posso aggiungere collegamenti ipertestuali al testo?  
Sì, Aspose.PDF consente di aggiungere collegamenti ipertestuali all'interno di frammenti di testo. Controlla la sezione [documentazione](https://reference.aspose.com/pdf/net/) per maggiori dettagli.

### Posso personalizzare il carattere e lo stile del testo?  
Assolutamente! Puoi personalizzare facilmente font, colori e altre proprietà di stile dei frammenti di testo.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}