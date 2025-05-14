---
"description": "Scopri come applicare diversi stili di numeri (numeri romani, alfabetici) alle intestazioni di un PDF utilizzando Aspose.PDF per .NET con questa guida dettagliata."
"linktitle": "Applica stile numero nel file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Applica stile numero nel file PDF"
"url": "/it/net/programming-with-headings/apply-number-style/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Applica stile numero nel file PDF

## Introduzione

Ti è mai capitato di dover aggiungere elenchi numerati di grande impatto ai tuoi documenti PDF? Che tu stia formattando documenti legali, report o presentazioni, gli stili di numerazione appropriati sono essenziali per organizzare le informazioni. Con Aspose.PDF per .NET, puoi applicare diversi stili di numerazione alle intestazioni dei tuoi file PDF, creando documenti ben strutturati e professionali. 

## Prerequisiti

Prima di immergerci nella codifica, vediamo cosa ti servirà:

1. Aspose.PDF per .NET: Scarica l'ultima versione di Aspose.PDF da [Qui](https://releases.aspose.com/pdf/net/).
2. Ambiente di sviluppo: assicurati di avere Visual Studio o un altro IDE compatibile con .NET.
3. .NET Framework: assicurati di aver installato .NET Framework 4.0 o versione successiva.
4. Licenza: puoi utilizzare una licenza temporanea da [Qui](https://purchase.aspose.com/temporary-license/) esplorare il [prova gratuita](https://releases.aspose.com/) opzioni.

## Importa pacchetti

Per iniziare, assicurati di aver importato i seguenti namespace nel tuo progetto:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

## Fase 1: Impostazione del documento

Iniziamo creando un nuovo documento PDF e configurandone le impostazioni di pagina. Imposteremo le dimensioni e i margini della pagina per controllare il layout del contenuto.

Spiegazione: in questa fase, impostiamo la struttura di base del PDF, che include la definizione delle dimensioni della pagina, dell'altezza e dei margini per una formattazione coerente.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDoc = new Document();

// Imposta le dimensioni e i margini della pagina
pdfDoc.PageInfo.Width = 612.0;
pdfDoc.PageInfo.Height = 792.0;
pdfDoc.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfDoc.PageInfo.Margin.Left = 72;
pdfDoc.PageInfo.Margin.Right = 72;
pdfDoc.PageInfo.Margin.Top = 72;
pdfDoc.PageInfo.Margin.Bottom = 72;
```

In questo modo, il documento avrà una dimensione di pagina standard, equivalente a una pagina da 8,5 x 11 pollici, e un margine di 72 punti (o 1 pollice) su tutti i lati.

## Passaggio 2: aggiunta di una pagina al PDF

Successivamente aggiungeremo una nuova pagina al documento PDF, dove applicheremo in seguito gli stili di numerazione.

Spiegazione: Ogni PDF richiede pagine! Questo passaggio aggiunge una pagina vuota al PDF e ne imposta i margini in base alle impostazioni a livello di documento.

```csharp
// Aggiungi una nuova pagina al documento PDF
Aspose.Pdf.Page pdfPage = pdfDoc.Pages.Add();
pdfPage.PageInfo.Width = 612.0;
pdfPage.PageInfo.Height = 792.0;
pdfPage.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfPage.PageInfo.Margin.Left = 72;
pdfPage.PageInfo.Margin.Right = 72;
pdfPage.PageInfo.Margin.Top = 72;
pdfPage.PageInfo.Margin.Bottom = 72;
```

## Passaggio 3: creare una casella mobile

Un FloatingBox consente di posizionare contenuti (come testo o titoli) all'interno di un box che si comporta in modo indipendente dal flusso della pagina. Questo è utile quando si desidera il controllo completo sul layout dei contenuti.

Spiegazione: qui stiamo impostando un FloatingBox per contenere le intestazioni a cui verranno applicati gli stili numerici.

```csharp
// Crea un FloatingBox per contenuti strutturati
Aspose.Pdf.FloatingBox floatBox = new Aspose.Pdf.FloatingBox();
floatBox.Margin = pdfPage.PageInfo.Margin;
pdfPage.Paragraphs.Add(floatBox);
```

## Passaggio 4: aggiungere la prima intestazione con numeri romani

Ora arriva la parte interessante! Aggiungiamo la prima intestazione con la numerazione in numeri romani minuscoli.

Spiegazione: applicheremo lo stile NumberingStyle.NumeralsRomanLowercase all'intestazione, che visualizzerà la numerazione in numeri romani (i, ii, iii, ecc.).

```csharp
// Crea il primo titolo con i numeri romani
Aspose.Pdf.Heading heading = new Aspose.Pdf.Heading(1);
heading.IsInList = true;
heading.StartNumber = 1;
heading.Text = "List 1";
heading.Style = NumberingStyle.NumeralsRomanLowercase;
heading.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading);
```

## Passaggio 5: aggiungere una seconda intestazione con numeri romani

A scopo dimostrativo, aggiungiamo una seconda intestazione con numeri romani, ma questa volta inizieremo dal 13.

Spiegazione: la proprietà StartNumber consente di iniziare la numerazione da un numero personalizzato; in questo caso, partiamo da 13.

```csharp
// Crea una seconda intestazione a partire dal numero romano 13
Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
heading2.IsInList = true;
heading2.StartNumber = 13;
heading2.Text = "List 2";
heading2.Style = NumberingStyle.NumeralsRomanLowercase;
heading2.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading2);
```

## Passaggio 6: aggiungere un'intestazione con numerazione alfabetica

Per variare, aggiungiamo una terza intestazione, ma questa volta useremo la numerazione alfabetica in minuscolo (a, b, c, ecc.).

Spiegazione: modificando NumberingStyle in LettersLowercase è possibile applicare la numerazione alfabetica alle intestazioni.

```csharp
// Crea un titolo con numerazione alfabetica
Aspose.Pdf.Heading heading3 = new Aspose.Pdf.Heading(2);
heading3.IsInList = true;
heading3.StartNumber = 1;
heading3.Text = "the value, as of the effective date of the plan, of property to be distributed under the plan on account of each allowed";
heading3.Style = NumberingStyle.LettersLowercase;
heading3.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading3);
```

## Passaggio 7: salvataggio del PDF

Infine, dopo aver applicato tutti gli stili di intestazione e numerazione, salviamo il file PDF nella directory desiderata.

Spiegazione: questo passaggio salva il file PDF contenente tutte le intestazioni formattate con gli stili di numerazione applicati.

```csharp
// Salva il documento PDF
dataDir = dataDir + "ApplyNumberStyle_out.pdf";
pdfDoc.Save(dataDir);
Console.WriteLine("\nNumber style applied successfully in headings.\nFile saved at " + dataDir);
```

## Conclusione

Ed ecco fatto! Hai applicato con successo gli stili di numerazione (numeri romani e alfabetici) alle intestazioni di un file PDF utilizzando Aspose.PDF per .NET. La flessibilità offerta da Aspose.PDF per il controllo del layout di pagina, degli stili di numerazione e del posizionamento dei contenuti ti offre un potente set di strumenti per creare documenti PDF professionali e ben organizzati.

## Domande frequenti

### Posso applicare stili numerici diversi allo stesso documento PDF?  
Sì, Aspose.PDF per .NET consente di combinare diversi stili di numerazione, ad esempio numeri romani, numeri arabi e numerazione alfabetica, all'interno dello stesso documento.

### Come posso personalizzare il numero iniziale delle intestazioni?  
È possibile impostare il numero iniziale per qualsiasi intestazione utilizzando `StartNumber` proprietà.

### Esiste un modo per reimpostare la sequenza di numerazione?  
Sì, puoi reimpostare la numerazione regolando il `StartNumber` proprietà per ogni intestazione.

### Posso applicare lo stile grassetto o corsivo ai titoli oltre alla numerazione?  
Assolutamente! Puoi personalizzare gli stili dei titoli modificando proprietà come carattere, dimensione, grassetto e corsivo utilizzando `TextState` oggetto.

### Come posso ottenere una licenza temporanea per Aspose.PDF?  
È possibile ottenere una licenza temporanea da [Qui](https://purchase.aspose.com/temporary-license/) per testare Aspose.PDF senza restrizioni.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}