---
category: general
date: 2026-04-06
description: Crea PDF da JPG rapidamente e impara come ritagliare l'immagine nel PDF,
  aggiungere una nuova pagina PDF e convertire JPG in PDF con ritaglio usando C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: it
og_description: Crea PDF da JPG e ritaglia l'immagine nel PDF con C#. Scopri come
  aggiungere una nuova pagina PDF e convertire JPG in PDF con ritaglio.
og_title: Crea PDF da JPG in C# – Guida passo passo
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Crea PDF da JPG in C# – Guida completa con ritaglio e nuove pagine
url: /it/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF da JPG in C# – Guida completa con ritaglio e nuove pagine

Hai mai avuto bisogno di **create PDF from JPG** ma non sapevi come mantenere solo la parte che ti serve? Non sei solo. In molte app—pensa a fatture, ricevute o fotolibri—gli sviluppatori devono trasformare un'immagine in un PDF scartando i bordi indesiderati.  

In questo tutorial percorreremo una soluzione completa, pronta‑all'uso, che **creates PDF from JPG**, ti mostra come **crop image in PDF**, e dimostra il **how to add new pdf page** quando hai bisogno di più di un'immagine. Alla fine saprai anche come **convert JPG to PDF with crop** e **insert image into PDF C#** usando la libreria Aspose.Pdf.

## Cosa imparerai

- Configura Aspose.Pdf in un progetto .NET (nessuna configurazione complessa richiesta).  
- Carica un JPEG, definisci l'area da mantenere e ritagliala inserendola in una pagina PDF.  
- Aggiungi pagine aggiuntive allo stesso documento, permettendoti di creare PDF multi‑pagina da molte immagini.  
- Salva il file finale e verifica l'output.  

**Prerequisiti:** .NET 6+ (o .NET Framework 4.6+), Visual Studio 2022 o qualsiasi editor tu preferisca, e un riferimento NuGet a `Aspose.Pdf`. Non sono necessari altri servizi esterni.

![Create PDF from JPG example](image.jpg){: .align-center alt="Esempio di creazione PDF da JPG che mostra un'immagine ritagliata posizionata su una pagina PDF"}

---

## Passo 1: Installa Aspose.Pdf e prepara il tuo progetto

Prima di tutto—aggiungi il pacchetto Aspose.Pdf. Apri un terminale nella cartella della tua soluzione e esegui:

```bash
dotnet add package Aspose.Pdf
```

Quella singola riga scarica tutto il necessario: le classi `Document`, `Rectangle` e `Page` che utilizzeremo più avanti. Secondo la mia esperienza, il metodo NuGet è il modo più pulito per rimanere aggiornati senza impazzire con i DLL.

> **Suggerimento:** Se stai puntando a .NET Framework, usa il pacchetto `Aspose.Pdf.NET`; l'API è identica.

---

## Passo 2: Carica il JPEG e definisci le dimensioni della pagina

Abbiamo bisogno di una tela che corrisponda alle dimensioni desiderate per la pagina PDF finale. Il codice qui sotto crea un nuovo `Document` e apre l'immagine sorgente come stream.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Perché un rettangolo? In Aspose.Pdf un `Rectangle` rappresenta sia le dimensioni della pagina sia l'area dell'immagine da visualizzare. Separando la *pagina* dall'*area di ritaglio* ottieni un controllo più preciso su ciò che finisce nel PDF.

---

## Passo 3: Scegli l'area di ritaglio (quartiere in alto a sinistra)

Supponiamo tu abbia bisogno solo del quarto in alto a sinistra della foto. Calcoliamo quell'area rispetto alle dimensioni della pagina:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

Il costruttore `Rectangle` accetta i valori **lower‑left X/Y** e **upper‑right X/Y**. Aggiungendo metà dell'altezza a `LLY` spostiamo la parte inferiore del ritaglio verso l'alto, scartando efficacemente la metà inferiore dell'immagine. Regola questi calcoli se ti serve una porzione diversa.

> **Perché ritagliare prima di aggiungere?**  
> Il ritaglio sul lato PDF evita di creare un bitmap temporaneo su disco, risparmiando I/O e memoria. Aspose gestisce i calcoli per te, e il risultato è un PDF pulito e amico dei vettori.

---

## Passo 4: Aggiungi una nuova pagina e inserisci l'immagine ritagliata

Ora posizioniamo effettivamente l'immagine su una pagina PDF. Qui è dove la keyword **how to add new pdf page** brilla.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` takes three arguments:

1. **Stream** – il JPEG sorgente.  
2. **Page rectangle** – definisce le dimensioni della pagina (il nostro `pageBounds`).  
3. **Crop rectangle** – indica ad Aspose quale parte dell'immagine renderizzare.

Se ti servono più pagine, ripeti semplicemente il pattern `Add` + `AddImage` con un nuovo `imageStream` ogni volta. Questo soddisfa il requisito **how to add new pdf page** mantenendo il codice ordinato.

---

## Passo 5: Salva il PDF e verifica il risultato

L'ultimo passo è una singola riga, ma non sottovalutarlo—salvare nel percorso corretto garantisce che il file possa essere aperto da qualsiasi visualizzatore PDF.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

Quando apri `cropped_image.pdf`, dovresti vedere una singola pagina che contiene solo il quarto in alto a sinistra del JPEG originale, perfettamente centrato nella pagina 600 × 800.

---

## Esempio completo funzionante (tutti i passi combinati)

Di seguito trovi il programma completo che puoi copiare‑incollare in un'app console. Compila così com'è, assumendo che tu abbia installato Aspose.Pdf e posizionato un JPEG nella posizione specificata.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Output previsto

- **File:** `cropped_image.pdf` (≈ 30 KB).  
- **Contenuto:** Una pagina, 600 × 800 punti, che mostra il quarto in alto a sinistra di `photo.jpg`.  
- **Comportamento:** Nessuna distorsione; l'immagine mantiene la sua risoluzione originale entro i limiti del ritaglio.

---

## Domande frequenti e casi particolari

### E se devo mantenere l'intera immagine, non solo un quarto?

Imposta semplicemente `cropArea` uguale a `pageBounds`:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### Posso usare una dimensione di pagina diversa (es. A4)?

Assolutamente. Sostituisci i valori di `pageBounds` con le dimensioni di una pagina A4 in punti (595 × 842):

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

Il rettangolo di ritaglio può rimanere lo stesso o essere ricalcolato per adattarsi al nuovo rapporto d'aspetto.

### Come aggiungere più immagini, ognuna su una propria pagina?

Itera su una collezione di percorsi file:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### E la trasparenza o le immagini PNG?

Aspose.Pdf tratta i PNG allo stesso modo dei JPEG. Se la sorgente ha un canale alfa, il PDF lo manterrà, a condizione che la versione PDF supporti la trasparenza (il default è adeguato).

### Funziona su .NET Core su Linux?

Sì. Aspose.Pdf è cross‑platform; assicurati solo che `imageStream` punti a un percorso file valido sul sistema operativo di destinazione. Non vengono usate API specifiche di Windows.

---

## Suggerimenti e migliori pratiche

- **Gestione della memoria:** Avvolgi sempre gli stream in istruzioni `using` (come mostrato) per evitare blocchi sui file.  
- **Prestazioni:** Se elabori decine di immagini, considera di riutilizzare una singola istanza `Document` e chiamare `pdfDocument.Pages.Add()` per ogni immagine.  
- **Gestione degli errori:** Avvolgi l'intera routine in un blocco `try/catch` e registra `PdfException` per il troubleshooting.  
- **Controllo della qualità:** Aspose.Pdf ti permette di impostare la risoluzione dell'immagine tramite `ImageFragment`. Per scansioni ad alta DPI, imposta `ImageFragment.Resolution = 300;`.  
- **Sicurezza:** Se il PDF sarà condiviso esternamente, puoi aggiungere la crittografia con `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

## Conclusione

Abbiamo appena coperto come **create PDF from JPG** in C#, **crop image in PDF**, e **add new PDF page** per creare documenti multi‑pagina. Lo stesso schema ti permette di **convert JPG to PDF with crop** e **insert image into PDF C#** per qualsiasi scenario—da semplici ricevute a complessi fotolibri.  

Provalo: modifica la logica di ritaglio, sperimenta con pagine A4, o concatenare più immagini. La libreria Aspose.Pdf rende queste operazioni semplici, e il codice sopra è un riferimento solido e citabile che puoi incollare in qualsiasi progetto.

### Prossimi passi

- **Aggiungi annotazioni di testo** al PDF (es. didascalie sotto ogni immagine).  
- **Crea automaticamente un indice** per PDF multi‑pagina.  
- **Unisci più PDF** usando `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

Ognuno di questi argomenti si basa sui fondamenti appena appresi, quindi sei ben posizionato per esplorarli

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}