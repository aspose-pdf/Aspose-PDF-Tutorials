---
"description": "Scopri come posizionare il testo attorno alle immagini nei PDF utilizzando Aspose.PDF per .NET. Segui la nostra guida passo passo per creare PDF professionali con immagini e testo affiancati."
"linktitle": "Inserimento di testo attorno all'immagine in un file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Inserimento di testo attorno all'immagine in un file PDF"
"url": "/it/net/programming-with-text/placing-text-around-image/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Inserimento di testo attorno all'immagine in un file PDF

## Introduzione

Hai mai provato a posizionare del testo attorno a un'immagine in un file PDF, ma l'hai trovato difficile? Se sì, sei nel posto giusto! Aspose.PDF per .NET semplifica questo processo, permettendoti di posizionare il testo accanto alle immagini con poche righe di codice. Che tu stia creando report, documenti o presentazioni, questa funzionalità è un modo fantastico per migliorare il layout dei tuoi contenuti e renderli visivamente più accattivanti. Oggi ti mostreremo come utilizzare Aspose.PDF per .NET per posizionare del testo attorno alle immagini in un documento PDF.

## Prerequisiti

Prima di iniziare a scrivere il codice, assicuriamoci di aver configurato tutto correttamente. Ecco cosa ti servirà:

- Aspose.PDF per .NET: puoi scaricarlo da [Qui](https://releases.aspose.com/pdf/net/).
- Visual Studio: assicurati di avere installata la versione più recente per procedere senza problemi.
- .NET Framework: questo esempio utilizza .NET, quindi assicurati che il tuo ambiente sia configurato per lo sviluppo .NET.
- Una licenza temporanea: puoi richiedere una licenza temporanea [Qui](https://purchase.aspose.com/temporary-license/) se stai valutando il prodotto.

Se non hai ancora configurato Aspose.PDF per .NET, segui le istruzioni di installazione in [documentazione](https://reference.aspose.com/pdf/net/).

## Importa spazi dei nomi

Prima di iniziare a scrivere codice, dobbiamo importare i namespace necessari. Ecco il frammento di codice per farlo:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Questi namespace sono essenziali in quanto forniscono l'accesso a classi come `Document`, `Page`, `Image`, E `HtmlFragment`, che utilizzeremo per creare e manipolare il PDF.

Ora che abbiamo impostato la base, vediamo come posizionare il testo attorno a un'immagine in un file PDF utilizzando Aspose.PDF per .NET. Ti guideremo passo dopo passo.

## Passaggio 1: creare un'istanza dell'oggetto documento

Per prima cosa, devi creare un documento PDF. In Aspose.PDF, questo si fa istanziando un `Document` oggetto. Questo oggetto servirà da base per tutti i contenuti che aggiungeremo.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Qui abbiamo creato un documento PDF vuoto. Non ha ancora pagine, ma non preoccuparti, ne aggiungeremo una nel prossimo passaggio.

## Passaggio 2: aggiungere una pagina al documento

Ora che abbiamo il nostro documento, è il momento di aggiungere una pagina. Immagina di creare un foglio bianco su cui aggiungere i tuoi contenuti.

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

Questo codice aggiunge una nuova pagina al documento. Di default, la pagina è vuota, ma stiamo per modificarla.

## Passaggio 3: creare una tabella per organizzare i contenuti

Per mantenere l'immagine e il testo correttamente allineati, useremo una tabella. Le tabelle nei PDF possono aiutare a strutturare il layout, proprio come nei documenti Word o HTML.

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
page.Paragraphs.Add(table1);
```

Questo frammento crea una tabella e la aggiunge alla pagina. Considera la tabella come la struttura su cui allineare immagine e testo.

## Passaggio 4: impostare la larghezza delle colonne per la tabella

Ora che abbiamo aggiunto una tabella, dobbiamo definire la larghezza delle colonne. Questo garantisce che l'immagine e il testo abbiano le dimensioni appropriate sulla pagina.

```csharp
table1.ColumnWidths = "120 270";
```

Questa riga imposta la larghezza di due colonne: una per l'immagine e una per il testo. Regola questi valori se l'immagine o il testo necessitano di più o meno spazio.

## Passaggio 5: definire margini e spaziatura

Per assicurarci che tutto sia in ordine, aggiungiamo margini e spaziatura alla tabella.

```csharp
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;
table1.DefaultCellPadding = margin;
```

Queste impostazioni garantiscono che la spaziatura della tabella sia uniforme, rendendo il contenuto visivamente accattivante.

## Passaggio 6: inserire un'immagine nella tabella

Ora passiamo alla parte divertente: aggiungere un'immagine. In questo caso, aggiungeremo il logo di Aspose, ma sentiti libero di usare qualsiasi immagine tu preferisca.

```csharp
Aspose.Pdf.Row row1 = table1.Rows.Add();
Aspose.Pdf.Image logo = new Aspose.Pdf.Image();
logo.File = dataDir + "aspose-logo.jpg";
logo.FixHeight = 120;
logo.FixWidth = 110;
row1.Cells.Add();
row1.Cells[0].Paragraphs.Add(logo);
```

Ecco cosa sta succedendo:
- Carichiamo l'immagine dalla directory specificata.
- Impostiamo l'altezza e la larghezza dell'immagine.
- Infine, aggiungiamo l'immagine alla prima cella della tabella.

## Passaggio 7: aggiungere testo accanto all'immagine

Ora che l'immagine è al suo posto, aggiungiamo del testo accanto. In questo esempio, useremo testo in formato HTML per formattare il contenuto.

```csharp
string TitleString = "<font face=\"Arial\" size=6 color=\"#101090\"><b> Aspose.Pdf for .NET</b></font>";
string BodyString1 = "<font face=\"Arial\" size=2><br/>Aspose.Pdf for .NET is a non-graphical PDF document reporting component that enables .NET applications to <b>create PDF documents from scratch</b> without utilizing Adobe Acrobat.</font>";

Aspose.Pdf.HtmlFragment TitleText = new Aspose.Pdf.HtmlFragment(TitleString + BodyString1);
row1.Cells.Add();
row1.Cells[1].Paragraphs.Add(TitleText);
```

Questo blocco aggiunge un titolo e una descrizione formattati nella cella accanto all'immagine. Puoi formattare il testo utilizzando tag HTML per una maggiore personalizzazione.

## Passaggio 8: regolare l'allineamento verticale

Per impostazione predefinita, il contenuto delle celle di una tabella potrebbe non essere allineato come desiderato. In questo caso, vogliamo assicurarci che il testo sia allineato al bordo superiore della cella.

```csharp
row1.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
```

In questo modo il testo viene visualizzato nella parte superiore della cella, mantenendo un layout pulito e professionale.

## Passaggio 9: aggiungere altro testo sotto l'immagine e la descrizione

Potresti voler includere più contenuto sotto l'immagine e il testo. Aggiungiamo un'altra riga alla tabella a questo scopo.

```csharp
Aspose.Pdf.Row SecondRow = table1.Rows.Add();
SecondRow.Cells.Add();
SecondRow.Cells[0].ColSpan = 2;
SecondRow.Cells[0].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;

string SecondRowString = "<font face=\"Arial\" size=2>Aspose.Pdf for .NET supports the creation of PDF files through API and XML or XSL-FO templates.</font>";
Aspose.Pdf.HtmlFragment SecondRowText = new Aspose.Pdf.HtmlFragment(SecondRowString);
SecondRow.Cells[0].Paragraphs.Add(SecondRowText);
```

Qui abbiamo aggiunto un'altra riga con testo aggiuntivo, che occupa entrambe le colonne per mantenere l'equilibrio nel layout.

## Passaggio 10: Salvare il documento PDF

Infine, dobbiamo salvare il documento in modo da poter visualizzare le modifiche.

```csharp
doc.Save(dataDir + "PlacingTextAroundImage_out.pdf");
```

In questo modo il PDF viene salvato con l'immagine e il testo formattati esattamente come li desideriamo.

## Conclusione

Inserire il testo attorno alle immagini in un PDF può sembrare un compito arduo, ma Aspose.PDF per .NET semplifica il processo. Sfruttando tabelle, immagini e testo formattato, è possibile creare PDF dall'aspetto professionale con il minimo sforzo. Con poche righe di codice, è possibile posizionare il contenuto esattamente dove si desidera, conferendo ai documenti un aspetto curato e ben organizzato.

## Domande frequenti

### Posso usare questo metodo per inserire più immagini con testo?
Sì, basta aggiungere più righe e celle alla tabella per includere immagini e testo aggiuntivi.

### Posso modificare l'allineamento dell'immagine?
Assolutamente! Puoi modificare l'allineamento dell'immagine modificando le proprietà di allineamento della cella.

### Come posso formattare ulteriormente il testo?
È possibile utilizzare i tag HTML all'interno di `HtmlFragment` oggetto per applicare vari stili come grassetto, corsivo o tipi di carattere diversi.

### Posso controllare la spaziatura tra il testo e l'immagine?
Sì, utilizzando il `MarginInfo` L'oggetto consente di controllare la spaziatura e i margini tra gli elementi.

### È possibile aggiungere dei link al testo?
Certamente! Puoi incorporare collegamenti ipertestuali nel testo formattato in HTML utilizzando `<a>` etichetta.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}