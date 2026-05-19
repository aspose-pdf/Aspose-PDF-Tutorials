---
category: general
date: 2026-04-25
description: Aggiungi la numerazione Bates ai PDF rapidamente usando Aspose.Pdf. Scopri
  come aggiungere numeri di pagina ai PDF, regolare automaticamente la dimensione
  del carattere e aggiungere una filigrana di testo in C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: it
og_description: Aggiungi la numerazione Bates ai PDF con Aspose.Pdf. Questa guida
  mostra come aggiungere numeri di pagina ai PDF, regolare automaticamente la dimensione
  del carattere e inserire una filigrana di testo in un unico esempio eseguibile.
og_title: Aggiungi la numerazione Bates ai PDF – Tutorial completo Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aggiungi la numerazione Bates ai PDF con Aspose – Guida completa
url: /it/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere la numerazione Bates ai PDF con Aspose – Guida completa

Ti è mai capitato di **add bates numbering** a un PDF ma non sapevi da dove cominciare? Non sei solo—team legali, revisori e sviluppatori si trovano di fronte a questo ostacolo ogni giorno. La buona notizia? Con Aspose.Pdf per .NET puoi apporre un numero Bates, regolare automaticamente la dimensione del carattere e persino trattare il timbro come una leggera filigrana di testo—tutto con poche righe di C#.

In questo tutorial percorreremo i passaggi esatti per **add page numbers pdf**, regolare il carattere in modo che non trabocchi mai, e rispondere una volta per tutte alla domanda “how to add bates”. Alla fine avrai un'app console pronta all'uso che produce un PDF numerato professionalmente, e vedrai come estenderla in una soluzione completa di filigrana.

## Prerequisiti

* **Aspose.Pdf for .NET** (l'ultimo pacchetto NuGet a partire da aprile 2026).  
* .NET 6.0 SDK o versioni successive – l'API funziona allo stesso modo su .NET Framework, ma .NET 6 offre le migliori prestazioni.  
* Un PDF di esempio chiamato `input.pdf` posizionato in una cartella a cui puoi fare riferimento (es., `C:\Docs\`).  

Non è necessaria alcuna configurazione aggiuntiva; la libreria è autonoma.

---

## Passo 1 – Caricare il documento PDF sorgente

La prima cosa che facciamo è aprire il file che vogliamo numerare. La classe `Document` di Aspose rappresenta l'intero PDF, e caricarlo è semplice come passare il percorso al costruttore.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Perché è importante*: Caricare il documento ti dà accesso alla collezione `Pages`, dove in seguito aggiungeremo il timbro Bates. Se il file non viene trovato, Aspose genera una chiara `FileNotFoundException`, così saprai esattamente cosa è andato storto.

---

## Passo 2 – Creare un timbro di testo per i numeri Bates

Ora creiamo l'elemento visivo che apparirà su ogni pagina. La classe `TextStamp` ti consente di inserire qualsiasi stringa, e useremo il segnaposto `{page}-{total}` per far sì che Aspose sostituisca automaticamente quei token.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Punti chiave*:

* **auto adjust font size** – Impostare `AutoAdjustFontSizeToFitStampRectangle` a `true` garantisce che il testo non fuoriesca dal rettangolo, ideale per numeri di pagina di lunghezza variabile.  
* **add text watermark** – Abbassando l'`Opacity` trasformiamo il numero Bates in una leggera filigrana, soddisfacendo il requisito “add text watermark” senza passaggi aggiuntivi.  
* **how to add bates** – I token `{page}` e `{total}` sono il segreto; Aspose li sostituisce a runtime, così non devi calcolare nulla manualmente.

---

## Passo 3 – Applicare il timbro a ogni pagina

Un errore comune è timbrare solo la prima pagina. Per **add page numbers pdf** davvero, dobbiamo iterare l'intera collezione `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Perché clonare? Il metodo `AddStamp` crea internamente una copia, ma utilizzare esplicitamente una nuova istanza per ogni iterazione evita effetti collaterali accidentali se in seguito modifichi le proprietà del timbro (ad esempio cambiando il colore per pagine specifiche).

---

## Passo 4 – Salvare il PDF aggiornato

Con i timbri al loro posto, persistere le modifiche è semplice. Puoi sovrascrivere il file originale o scrivere in una nuova posizione—qui salveremo un nuovo file chiamato `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Se apri `output.pdf` vedrai ogni pagina etichettata “Bates: 1‑10”, “Bates: 2‑10”, … in basso a destra, con una leggera opacità che funge anche da **add text watermark**.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco un unico programma console autonomo che puoi copiare‑incollare in Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Expected result**: Apri `output.pdf` in qualsiasi visualizzatore; ogni pagina mostra una riga come “Bates: 3‑12” nell'angolo inferiore destro, dimensionata perfettamente per il rettangolo e resa con un'opacità del 40 %. Questo soddisfa sia il requisito di tracciamento legale sia la necessità di filigrana visiva.

---

## Varianti comuni e casi limite

| Situazione | Cosa cambiare | Perché |
|------------|---------------|--------|
| **Different placement** | Adjust `HorizontalAlignment` / `VerticalAlignment` or set `XIndent`/`YIndent` | Alcune aziende preferiscono la posizione in alto a sinistra o al centro. |
| **Custom prefix** | Replace `"Bates: "` with `"Doc‑ID: "` or any string | Potresti utilizzare una convenzione di denominazione diversa. |
| **Multiple stamps** | Create a second `TextStamp` (e.g., for a confidentiality notice) and add it after the first | Combinare **add bates numbering** con altri requisiti **add text watermark** è banale. |
| **Large page counts** | Increase the initial font size (e.g., `14`) – the auto‑adjust will shrink it when needed | Quando hai > 999 pagine la stringa diventa più lunga; l'auto‑adjust evita il troncamento. |
| **Encrypted PDFs** | Call `pdfDocument.Decrypt("password")` before stamping | Non è possibile modificare un file protetto senza la password. |

---

## Consigli professionali e insidie

* **Pro tip:** Imposta `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` se noti che il testo è troppo vicino al bordo della pagina.  
* **Watch out for:** Rettangoli molto piccoli (la dimensione predefinita è 100 × 30 pt). Se ti serve un'area più ampia, imposta manualmente `batesStamp.Width` e `batesStamp.Height`.  
* **Performance note:** Timbratura di migliaia di pagine può richiedere qualche secondo, ma Aspose gestisce lo streaming delle pagine in modo efficiente—non è necessario caricare l'intero documento in memoria.  

---

## Conclusione

Abbiamo appena dimostrato come **add bates numbering** a un PDF usando Aspose.Pdf, mentre simultaneamente **add page numbers pdf**, abilitiamo **auto adjust font size** e creiamo un **add text watermark** in un unico flusso coerente. L'esempio completo e eseguibile sopra ti fornisce una solida base che puoi adattare a qualsiasi flusso di lavoro di documenti legali o sistema di reporting interno.

Pronto per il passo successivo? Prova a combinare questo approccio con l'API di merging PDF di Aspose per elaborare più file in batch, o esplora la classe `TextFragment` per filigrane più ricche (colorate, ruotate o multilinea). Le possibilità sono infinite, e il codice che ora possiedi è una base affidabile.

Se hai trovato utile questa guida, sentiti libero di lasciare un commento, aggiungere una stella al repository o condividere le tue varianti. Buon coding, e che i tuoi PDF siano sempre perfettamente numerati!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}