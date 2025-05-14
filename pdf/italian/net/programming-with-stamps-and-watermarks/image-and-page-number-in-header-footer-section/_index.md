---
"description": "Scopri come aggiungere un'immagine e i numeri di pagina all'intestazione e al piè di pagina del tuo PDF utilizzando Aspose.PDF per .NET in questo tutorial passo passo."
"linktitle": "Immagine e numero di pagina nella sezione intestazione/piè di pagina"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Immagine e numero di pagina nella sezione intestazione/piè di pagina"
"url": "/it/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Immagine e numero di pagina nella sezione intestazione/piè di pagina

## Introduzione

Quando si tratta di creare documenti PDF di livello professionale, avere il controllo su dettagli minori come intestazioni e piè di pagina è essenziale. Vuoi che i tuoi documenti abbiano un aspetto curato e ben organizzato, giusto? Bene, con Aspose.PDF per .NET, puoi aggiungere immagini e numeri di pagina senza problemi alle sezioni di intestazione e piè di pagina del tuo documento. In questo tutorial, ti guideremo passo dopo passo, rendendolo semplice da seguire.

## Prerequisiti

Prima di addentrarci nei dettagli di questo tutorial, assicurati di aver sistemato quanto segue:

1. .NET Framework: è necessario avere installata sul computer una qualsiasi versione di .NET Framework. Se non ce l'hai, puoi scaricarla facilmente dal sito web di Microsoft.
2. Aspose.PDF per .NET: poiché utilizzeremo Aspose.PDF, assicurati di averlo installato nel tuo progetto. Puoi scaricare una versione di prova. [Qui](https://releases.aspose.com/pdf/net/).
3. Conoscenza di base di C#: la familiarità con la programmazione di base di C# ti aiuterà sicuramente a comprendere il codice senza troppi problemi.
4. Un file immagine: avrai bisogno di un'immagine da inserire nell'intestazione del tuo documento PDF, ad esempio un logo. Salvala in una directory accessibile. 
5. IDE: utilizza l'ambiente di sviluppo integrato (IDE) di tua scelta, come Visual Studio, per lavorare con il tuo progetto .NET.

Una volta che avrai preparato tutti i prerequisiti, sarai pronto per creare un favoloso file PDF!

## Importa pacchetti

Per iniziare a utilizzare Aspose.PDF per .NET, è necessario importare gli spazi dei nomi necessari. All'inizio del file C#, aggiungere:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Image;
```

Questi namespace ti forniranno l'accesso alle classi necessarie per la manipolazione dei file PDF.

Ora passiamo al dunque! Segui questi passaggi per creare il tuo documento PDF, inserendo un'immagine nell'intestazione e i numeri di pagina nel piè di pagina.

## Passaggio 1: imposta la directory dei documenti

Ogni buon progetto inizia con l'organizzazione. Definisci la directory dei documenti in cui salverai i file e dove risiederanno le immagini. Ecco come fare:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ricordati di sostituire `"YOUR DOCUMENT DIRECTORY"` con il percorso effettivo in cui desideri salvare il PDF e dove si trova l'immagine.

## Passaggio 2: creare un nuovo documento PDF

Ora creeremo un nuovo documento PDF in cui avverrà tutta la magia:

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

A questo punto, hai creato un documento PDF vuoto. Interessante, vero?

## Passaggio 3: aggiungere una pagina al documento

Un PDF è fatto di pagine. Aggiungiamo una nuova pagina al nostro documento usando:

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

Ora hai una tela su cui puoi iniziare a progettare!

## Passaggio 4: creare la sezione dell'intestazione

L'intestazione conterrà l'immagine (ad esempio un logo) che desideri visualizzare. Crea la sezione dell'intestazione con il seguente codice:

```csharp
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
page.Header = header;
```

Ora hai un'intestazione che puoi personalizzare!

## Passaggio 5: aggiungere un'immagine all'intestazione

Ora arriviamo alla parte divertente! Devi aggiungere l'immagine all'intestazione. Per prima cosa, crea un oggetto immagine:

```csharp
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
```

Imposta il percorso del file dell'immagine:

```csharp
image1.File = dataDir + "aspose-logo.jpg";
```

Infine, aggiungi l'immagine all'intestazione:

```csharp
header.Paragraphs.Add(image1);
```

Congratulazioni! Hai appena aggiunto un'immagine all'intestazione del tuo PDF.

## Passaggio 6: creare la sezione piè di pagina

Ora lavoriamo sul piè di pagina. Analogamente al processo per l'intestazione, creiamo un oggetto piè di pagina:

```csharp
Aspose.Pdf.HeaderFooter footer = new Aspose.Pdf.HeaderFooter();
page.Footer = footer;
```

Qui inserirai il numero di pagina. 

## Passaggio 7: aggiungere testo al piè di pagina

Crea un frammento di testo che conterrà il numero di pagina:

```csharp
Aspose.Pdf.Text.TextFragment txt = new Aspose.Pdf.Text.TextFragment("Page: ($p of $P ) ");
```

Quindi aggiungi questo frammento di testo al piè di pagina:

```csharp
footer.Paragraphs.Add(txt);
```

Hai visto quanto è stato facile? Hai impostato il numero di pagina in modo dinamico!

## Passaggio 8: salvare il documento PDF

L'ultimo passo della nostra avventura è salvare il documento. Usa questo comando per salvare il PDF appena creato:

```csharp
doc.Save(dataDir + "ImageAndPageNumberInHeaderFooter_out.pdf");
```

Ed ecco fatto, il tuo PDF è pronto e caricato con un'immagine di intestazione e i numeri di pagina nel piè di pagina!

## Conclusione

Ed ecco fatto! Hai appena creato un PDF con un'immagine nell'intestazione e numeri di pagina dinamici nel piè di pagina utilizzando Aspose.PDF per .NET. È incredibile come poche righe di codice possano dare vita a un risultato così raffinato. Che si tratti di un report aziendale o di un documento personalizzato, l'aggiunta di questi elementi cambia il tono e la professionalità del tuo PDF.

## Domande frequenti

### Posso usare Aspose.PDF su qualsiasi piattaforma .NET?
Sì, Aspose.PDF per .NET supporta più piattaforme .NET, tra cui .NET Framework, .NET Core e altre ancora.

### È disponibile una versione di prova gratuita per Aspose.PDF?
Assolutamente! Puoi scaricare una versione di prova gratuita. [Qui](https://releases.aspose.com/).

### Quali formati di immagine sono supportati per le intestazioni?
Aspose.PDF supporta i formati immagine più comuni, come JPG, PNG e BMP, per intestazioni e piè di pagina.

### Posso personalizzare il formato del numero di pagina?
Sì, puoi personalizzare facilmente il testo e il formato del piè di pagina in base alle tue esigenze.

### È disponibile supporto tecnico?
Sì, Aspose offre supporto dedicato tramite il suo forum. Puoi contattarci per ricevere assistenza. [Qui](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}