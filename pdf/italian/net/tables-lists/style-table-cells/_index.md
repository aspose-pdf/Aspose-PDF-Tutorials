---
title: Personalizza lo sfondo, i bordi e il padding delle celle della tabella nei PDF con Aspose.Pdf per .NET
weight: 101
limit:
description: Scopri come creare un PDF con una tabella a due colonne e applicare colori di sfondo personalizzati, bordi e padding a ogni cella usando Aspose.Pdf per .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Scopri come creare un PDF con una tabella a due colonne e applicare
    colori di sfondo personalizzati, bordi e padding a ogni cella usando Aspose.Pdf
    per .NET.
  headline: Personalizza lo sfondo, i bordi e il padding delle celle della tabella
    nei PDF con Aspose.Pdf per .NET
  type: TechArticle
- description: Scopri come creare un PDF con una tabella a due colonne e applicare
    colori di sfondo personalizzati, bordi e padding a ogni cella usando Aspose.Pdf
    per .NET.
  name: Personalizza lo sfondo, i bordi e il padding delle celle della tabella nei
    PDF con Aspose.Pdf per .NET
  steps:
  - name: Crea un nuovo documento PDF vuoto all'interno di un blocco using.
    text: Crea un nuovo documento PDF vuoto all'interno di un blocco using.
  - name: Aggiungi una pagina vuota al documento PDF.
    text: Aggiungi una pagina vuota al documento PDF.
  - name: Istanzia un oggetto Table con due colonne da 200 punti, un sottile bordo
      esterno nero e un padding predefinito delle celle di 5 punti.
    text: Istanzia un oggetto Table con due colonne da 200 punti, un sottile bordo
      esterno nero e un padding predefinito delle celle di 5 punti.
  - name: Aggiungi la prima riga alla tabella.
    text: Aggiungi la prima riga alla tabella.
  - name: Crea la prima cella, inserisci il testo "First cell", imposta uno sfondo
      giallo chiaro, un bordo rosso di 2 punti e un margine di 4 punti.
    text: Crea la prima cella, inserisci il testo "First cell", imposta uno sfondo
      giallo chiaro, un bordo rosso di 2 punti e un margine di 4 punti.
  - name: Crea la seconda cella, aggiungi il testo "Second cell", assegna uno sfondo
      verde chiaro, un bordo blu di 2 punti e un margine di 4 punti.
    text: Crea la seconda cella, aggiungi il testo "Second cell", assegna uno sfondo
      verde chiaro, un bordo blu di 2 punti e un margine di 4 punti.
  - name: Aggiungi la seconda riga alla tabella.
    text: Aggiungi la seconda riga alla tabella.
  - name: Crea la terza cella, inserisci "Third cell", imposta uno sfondo ciano chiaro,
      un bordo grigio scuro di 2 punti e un margine di 4 punti.
    text: Crea la terza cella, inserisci "Third cell", imposta uno sfondo ciano chiaro,
      un bordo grigio scuro di 2 punti e un margine di 4 punti.
  - name: Crea la quarta cella, aggiungi "Fourth cell", assegna uno sfondo rosa chiaro,
      un bordo viola di 2 punti e un margine di 4 punti.
    text: Crea la quarta cella, aggiungi "Fourth cell", assegna uno sfondo rosa chiaro,
      un bordo viola di 2 punti e un margine di 4 punti.
  - name: Aggiungi la tabella completamente formattata alla pagina affinché sia visibile
      nel PDF.
    text: Aggiungi la tabella completamente formattata alla pagina affinché sia visibile
      nel PDF.
  - name: Salva il documento PDF su un file e chiudi il blocco using.
    text: Salva il documento PDF su un file e chiudi il blocco using.
  - name: Stampa un messaggio di conferma sulla console.
    text: Stampa un messaggio di conferma sulla console.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` fornisce un padding di base per ogni cella, ma se
      assegni un `Margin` (ad esempio, `cellA1.Margin = new MarginInfo(...)`) i valori
      del margine sovrascrivono il padding predefinito per quella specifica cella.'
    question: Il `DefaultCellPadding` impostato sul `Table` influisce sulle celle
      che hanno anche un `Margin` definito?
  - answer: Senza `Table.Border`, il rettangolo esterno intorno all'intera tabella
      viene omesso; saranno visibili solo i bordi delle singole celle che imposti
      (ad esempio, `cellA2.Border`).
    question: Come apparirà il PDF se rimuovo la proprietà `Border` dall'oggetto `Table`?
  - answer: Sì, crea un `BorderInfo` con un `BorderSide` specifico (ad esempio, `new
      BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) e assegnalo alla proprietà
      `Border` della cella.
    question: Posso assegnare a una cella una larghezza del bordo diversa su ciascun
      lato?
  - answer: Istanzia un nuovo `Row` con `Row newRow = dataTable.Rows.Add();` e poi
      aggiungi le celle a `newRow.Cells` proprio come nelle righe precedenti.
    question: Come aggiungo una terza riga alla tabella dopo il codice mostrato?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: Stile delle celle della tabella PDF – Sfondo, Bordo, Padding
og_description: Formatta rapidamente le celle di una tabella in un PDF con colori, bordi e spaziature personalizzati usando Aspose.Pdf per .NET.
og_image_alt: Guida che mostra come stilizzare il colore di sfondo, il bordo e il padding delle celle di una tabella in un PDF usando Aspose.Pdf per .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Personalizza lo sfondo, i bordi e il padding delle celle della tabella nei PDF con Aspose.Pdf per .NET
In questo tutorial vedrai come generare un documento PDF, aggiungere una tabella a due colonne e controllare con precisione l'aspetto di ogni cella. Impostando i colori di sfondo, definendo i bordi e regolando il padding, puoi far risaltare i dati della tabella e renderli curati. L'esempio utilizza le classi Aspose.Pdf Document e Table per dimostrare ogni opzione di stile.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Il `DefaultCellPadding` impostato sul `Table` influisce sulle celle che hanno anche un `Margin` definito?**  
A: `DefaultCellPadding` fornisce un padding di base per ogni cella, ma se assegni un `Margin` (ad esempio, `cellA1.Margin = new MarginInfo(...)`) i valori del margine sovrascrivono il padding predefinito per quella specifica cella.

**Q: Come apparirà il PDF se rimuovo la proprietà `Border` dall'oggetto `Table`?**  
A: Senza `Table.Border`, il rettangolo esterno intorno all'intera tabella viene omesso; saranno visibili solo i bordi delle singole celle che imposti (ad esempio, `cellA2.Border`).

**Q: Posso assegnare a una cella una larghezza del bordo diversa su ciascun lato?**  
A: Sì, crea un `BorderInfo` con un `BorderSide` specifico (ad esempio, `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) e assegnalo alla proprietà `Border` della cella.

**Q: Come aggiungo una terza riga alla tabella dopo il codice mostrato?**  
A: Istanzia un nuovo `Row` con `Row newRow = dataTable.Rows.Add();` e poi aggiungi le celle a `newRow.Cells` proprio come nelle righe precedenti.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}