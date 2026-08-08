---
category: general
date: 2026-06-08
description: Ritaglia l'immagine in PDF usando Aspose.PDF in C#. Scopri come creare
  un PDF con immagine, salvare un PDF con immagine e aggiungere un'immagine a un PDF
  in poche righe.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: it
og_description: Ritaglia l'immagine in PDF usando Aspose.PDF in C#. Questo tutorial
  mostra come creare un PDF con immagine, salvare un PDF con immagine e aggiungere
  rapidamente un'immagine al PDF.
og_title: Ritaglia immagine in PDF con Aspose.PDF – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Ritaglia immagine in PDF con Aspose.PDF – Guida completa
url: /it/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crop Image in PDF with Aspose.PDF – Guida completa

Ti sei mai chiesto come **crop image in PDF** senza dover estrarre un editor grafico? Non sei l'unico. In molti report, fatture o e‑book hai bisogno solo di una porzione di un'immagine—magari l'angolo del logo o un frammento di grafico—e vuoi inserirla direttamente nel PDF.  

Questa guida ti mostra esattamente questo: **create PDF with image**, **add image to PDF**, e poi **crop image in PDF** usando la libreria Aspose.PDF per C#. Alla fine saprai anche come **save PDF with image** così potrai inviare il file a chiunque.

---

## Cosa ti serve

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+)  
- Una copia con licenza o di prova di **Aspose.PDF for .NET** (installa via NuGet `Install-Package Aspose.PDF`)  
- Un file immagine (JPEG/PNG) su disco – lo chiameremo `image.jpg`  
- Qualsiasi IDE a tua scelta (Visual Studio, Rider, VS Code)

È tutto. Nessun servizio aggiuntivo, nessuno strumento esterno.

---

## Passo 1: Configura il progetto e le importazioni

Per prima cosa, crea un'app console e importa gli spazi dei nomi che utilizzeremo. Le istruzioni `using` mantengono il codice ordinato e rendono i passaggi successivi più facili da leggere.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Pro tip:** Se stai usando Visual Studio, fai clic destro sul progetto → *Manage NuGet Packages* → cerca “Aspose.PDF” e installa. La libreria gestisce internamente sia il posizionamento dell'immagine sia il ritaglio, quindi non avrai bisogno di librerie di immagini di terze parti.

---

## Passo 2: Crea PDF con immagine

Ora creiamo realmente **create pdf with image**. Il frammento qui sotto costruisce un nuovo `Document`, aggiunge una pagina vuota e prepara uno stream dell'immagine.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Eseguendo questo codice otterrai un PDF con l'intera immagine ridimensionata alle dimensioni specificate. È un buon controllo preliminare prima di iniziare a ritagliare.

---

## Passo 3: Come aggiungere immagine a PDF (e preparare il ritaglio)

Se conosci già la regione esatta che desideri, puoi saltare il passaggio a dimensione intera e passare direttamente alla parte **how to add image to pdf**. Il metodo `AddImage` accetta tre parametri:

1. **Image stream** – i byte grezzi della tua immagine.  
2. **Placement rectangle** – dove sulla pagina si trova l'immagine.  
3. **Crop rectangle** – la porzione dell'immagine che vuoi effettivamente renderizzare.

Di seguito la versione compatta che esegue sia il posizionamento **e** il ritaglio in una singola chiamata.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Why this works:** Aspose.PDF mappa internamente il rettangolo di ritaglio alle dimensioni in pixel dell'immagine, quindi renderizza solo quella porzione all'interno dell'area `placement`. Non è necessario alcun ulteriore processamento di bitmap, il che significa che mantieni il PDF di dimensioni ridotte.

---

## Passo 4: Come ritagliare immagine PDF – Opzioni avanzate

A volte il ritaglio di un quarto non è sufficiente. Potresti aver bisogno di un rettangolo personalizzato o di preservare il rapporto d'aspetto dell'immagine. Ecco un approccio più flessibile:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Gestione dei casi limite:**  
- **Null streams** – avvolgi sempre il `FileStream` in un blocco `using`, come mostrato, per evitare perdite.  
- **Large images** – se l'immagine di origine è molto grande, considera di ridimensionare il rettangolo `placement`; Aspose effettuerà il downsample automaticamente.  
- **Transparent PNGs** – la libreria rispetta i canali alfa, quindi l'area ritagliata manterrà la trasparenza.

---

## Passo 5: Salva PDF con immagine (e verifica)

Infine, **save pdf with image**. Il metodo `Save` scrive il documento su disco. Puoi anche trasmetterlo a un client web se stai costruendo un'API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

Quando apri `output.pdf`, dovresti vedere solo la porzione ritagliata di `image.jpg` posizionata esattamente dove l'hai definita. Se l'immagine appare distorta, regola la larghezza/altezza del rettangolo `placement` per corrispondere al rapporto d'aspetto del rettangolo di ritaglio.

---

## Domande frequenti e problemi comuni

| Domanda | Risposta |
|----------|--------|
| **Posso ritagliare più immagini sulla stessa pagina?** | Assolutamente. Chiama `page.AddImage` per ogni immagine con i propri rettangoli di posizionamento e ritaglio. |
| **E se la mia immagine è in un formato diverso (es. BMP)?** | Aspose.PDF supporta JPEG, PNG, BMP, GIF e TIFF nativamente. Basta cambiare l'estensione del file. |
| **Ho bisogno di una licenza per l'uso in produzione?** | Una versione di prova funziona fino a 5 pagine. Per le distribuzioni reali, acquista una licenza per rimuovere la filigrana. |
| **Come ruoto l'immagine ritagliata?** | Dopo aver aggiunto l'immagine, recupera l'oggetto `Image` e imposta la sua proprietà `Rotate` (`Rotate = RotationAngle.Rotate90`). |
| **È possibile ritagliare usando percentuali invece di punti assoluti?** | Sì—calcola le dimensioni del rettangolo basandoti su `image.Width * 0.25` ecc., poi converti in punti come mostrato nel Passo 4. |

---

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Esegui il programma, apri `output.pdf` e vedrai solo il quarto in alto a sinistra di `image.jpg` renderizzato nell'angolo in alto a sinistra della pagina. Modifica i valori del rettangolo `crop` per sperimentare diverse sezioni.

---

## Conclusione

Abbiamo illustrato l'intero processo di **crop image in pdf** usando Aspose.PDF per C#. Partendo da un documento nuovo, **create pdf with image**, dimostriamo **how to add image to pdf**, applichiamo un rettangolo personalizzato **how to crop image pdf** e infine **save pdf with image**.  

Ora puoi incorporare immagini ritagliate con precisione in qualsiasi PDF generi—perfetto per fatture, brochure di marketing o report automatizzati. Successivamente, considera di aggiungere didascalie di testo (`TextFragment`) o disegnare forme attorno all'immagine ritagliata per evidenziarla ulteriormente.  

Hai altri scenari di cui sei curioso? Lascia un commento, e buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Set Image Size in a PDF Using Aspose.PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Extract Image Information from PDFs Using Aspose.PDF for .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}