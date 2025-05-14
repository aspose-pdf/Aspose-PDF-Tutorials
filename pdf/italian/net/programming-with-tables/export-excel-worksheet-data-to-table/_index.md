---
"description": "Scopri come esportare i dati di un foglio di lavoro Excel in una tabella PDF utilizzando Aspose.PDF per .NET. Tutorial dettagliato con esempi di codice, prerequisiti e suggerimenti utili."
"linktitle": "Esporta i dati del foglio di lavoro Excel in una tabella"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Esporta i dati del foglio di lavoro Excel in una tabella"
"url": "/it/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Esporta i dati del foglio di lavoro Excel in una tabella

## Introduzione

Hai mai avuto bisogno di esportare dati da un foglio di lavoro Excel in un file PDF, ordinatamente organizzati in una tabella? Immagina di avere una serie di dati in Excel, ma di doverli condividere come PDF dall'aspetto professionale. Può sembrare complicato, vero? Ma con Aspose.PDF per .NET, puoi semplificare questa operazione. In questo tutorial, ti guideremo attraverso il processo di esportazione dei dati di un foglio di lavoro Excel in una tabella all'interno di un documento PDF utilizzando Aspose.PDF per .NET. Ti guideremo passo dopo passo, spiegando ogni passaggio in modo che, anche se sei alle prime armi, ti sentirai un professionista alla fine.

## Prerequisiti

Prima di immergerci nella codifica, prepariamo alcune cose:

1. Aspose.PDF per la libreria .NET: assicurati di avere installata la versione più recente. Puoi [scaricalo qui](https://releases.aspose.com/pdf/net/).
2. Libreria Aspose.Cells per .NET: necessaria per gestire le operazioni di Excel. Scaricala da [Qui](https://releases.aspose.com/cells/net/).
3. Ambiente di sviluppo .NET: uno strumento come Visual Studio è perfetto per la codifica.
4. File Excel: tieni pronto un file Excel con i dati che vuoi esportare.

Se non hai le librerie Aspose.PDF e Aspose.Cells, puoi iniziare con una [prova gratuita](https://releases.aspose.com/).

## Importa pacchetti

Per iniziare, assicurati di aver installato entrambe le librerie Aspose.PDF e Aspose.Cells nel tuo progetto. Puoi installarle utilizzando NuGet Package Manager in Visual Studio.

Ecco come importare i pacchetti necessari nel codice C#:

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

Ora che abbiamo impostato i prerequisiti, vediamo nel dettaglio il processo di esportazione dei dati da un foglio Excel a una tabella in un documento PDF.

## Passaggio 1: caricare la cartella di lavoro di Excel

Per iniziare, devi caricare la cartella di lavoro di Excel nel programma. In questo passaggio, useremo Aspose.Cells per aprire il file Excel.

```csharp
// Percorso verso la directory dei documenti.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Caricare la cartella di lavoro di Excel
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

Spiegazione: qui specifichiamo il percorso della directory in cui si trova il nostro file Excel e carichiamo la cartella di lavoro utilizzando `Aspose.Cells.Workbook`Assicurati di regolare `"YOUR DOCUMENT DIRECTORY"` per indicare la posizione del file.

## Passaggio 2: accedi al primo foglio di lavoro

Dopo aver caricato la cartella di lavoro, dobbiamo accedere al primo foglio di lavoro in cui sono memorizzati i nostri dati.

```csharp
// Accesso al primo foglio di lavoro nel file Excel
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

Spiegazione: questo passaggio è semplice: prendiamo il primo foglio di lavoro dalla cartella di lavoro, che contiene i dati da esportare.

## Passaggio 3: esportare i dati in DataTable

Ora esportiamo i dati dal foglio Excel in un oggetto DataTable, che fungerà da intermediario per il trasferimento dei dati al PDF.

```csharp
// Esportazione del contenuto di 7 righe e 2 colonne a partire dalla prima cella in DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

Spiegazione: Il `ExportDataTable` Il metodo estrae i dati a partire dalla prima cella del foglio di lavoro e si estende su tutte le righe e le colonne. Questi dati vengono quindi memorizzati in un `DataTable` per un ulteriore utilizzo.

## Passaggio 4: creare un nuovo documento PDF

Ora dobbiamo creare un nuovo documento PDF utilizzando Aspose.PDF.

```csharp
// Crea un'istanza di Documento
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// Crea una pagina nell'istanza del documento
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

Spiegazione: qui inizializziamo un nuovo `Aspose.Pdf.Document` e aggiungiamo una pagina. Questa pagina conterrà in seguito la tabella che stiamo creando dai dati di Excel.

## Passaggio 5: creare un oggetto tabella in PDF

Passiamo ora alla creazione di una tabella all'interno del documento PDF.

```csharp
// Crea un oggetto Tabella
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// Aggiungere l'oggetto Tabella alla raccolta dei paragrafi della pagina
page.Paragraphs.Add(table);
```

Spiegazione: Creiamo un `Aspose.Pdf.Table` oggetto e aggiungerlo alla raccolta dei paragrafi della pagina, il che garantisce che la tabella venga visualizzata sulla pagina.

## Passaggio 6: impostare la larghezza e i bordi delle colonne

Le tabelle in PDF richiedono larghezze di colonna definite. Aggiungeremo anche dei bordi per rendere la tabella più leggibile.

```csharp
// Imposta la larghezza delle colonne della tabella
table.ColumnWidths = "40 100 100";

// Imposta il bordo predefinito della cella
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

Spiegazione: Impostiamo le larghezze delle tre colonne e diamo a tutte le celle un bordo predefinito con uno spessore di `0.1F`.

## Passaggio 7: importare i dati da DataTable in una tabella PDF

Adesso è il momento di importare i dati dalla DataTable nella nostra tabella PDF.

```csharp
// Importare dati nell'oggetto Tabella da DataTable
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

Spiegazione: Il `ImportDataTable` metodo trasferisce tutti i dati dal `DataTable` alla tabella PDF. In questo modo la tabella viene popolata con i dati del foglio Excel.

## Passaggio 8: definire lo stile della riga di intestazione

Modifichiamo lo stile della riga di intestazione della tabella modificando il colore di sfondo, il carattere e l'allineamento.

```csharp
// Ottieni la prima riga dalla tabella
Aspose.Pdf.Row headerRow = table.Rows[0];

// Imposta lo stile per la riga dell'intestazione
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

Spiegazione: Eseguiamo un ciclo su tutte le celle della prima riga (intestazione), impostiamo il colore di sfondo su blu, il colore del testo su giallo e allineiamo il testo al centro.

## Passaggio 9: Definisci lo stile delle righe rimanenti

Per differenziare l'intestazione dal resto delle righe, aggiungiamo uno stile diverso per le righe rimanenti.

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

Spiegazione: per tutte le righe, eccetto l'intestazione, impostiamo uno sfondo grigio e il testo bianco.

## Passaggio 10: Salvare il documento PDF

Infine, salva il documento PDF con la tabella.

```csharp
// Salva il PDF
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

Spiegazione: Salviamo il PDF nella directory specificata. Ecco fatto! I tuoi dati Excel sono ora all'interno di una tabella PDF splendidamente formattata.

## Conclusione

Ed ecco fatto! In pochi passaggi, hai esportato i dati da un foglio di lavoro Excel in una tabella all'interno di un PDF utilizzando Aspose.PDF per .NET. Suddividendo il processo e personalizzandolo lungo il percorso, puoi personalizzare l'output e garantire che i dati appaiano puliti e professionali. Così, la prossima volta che qualcuno ti porgerà un file Excel e ti chiederà un report in PDF, saprai esattamente cosa fare.

## Domande frequenti

### Posso personalizzare ulteriormente la tabella?
Assolutamente! Puoi modificare colori, caratteri, allineamento e persino aggiungere bordi a celle specifiche.

### Aspose.PDF per .NET è gratuito?
Offre una prova gratuita, ma per un uso prolungato è necessaria una licenza. Puoi [compralo qui](https://purchase.aspose.com/buy).

### Posso esportare solo righe e colonne specifiche?
Sì, puoi modificare i parametri nel `ExportDataTable` metodo per esportare intervalli specifici.

### Funziona con file Excel di grandi dimensioni?
Sì, Aspose.Cells è progettato per gestire in modo efficiente file Excel di grandi dimensioni.

### Come posso aggiungere altre pagine al PDF?
Puoi usare `pdfDocument.Pages.Add()` per aggiungere tutte le pagine di cui hai bisogno.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}