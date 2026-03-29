---
category: general
date: 2026-03-29
description: Come firmare un PDF con una firma digitale e aggiungere un'immagine ritagliata
  in C#. Impara ad aggiungere una firma digitale al PDF, ritagliare l'immagine per
  il PDF e inserire l'immagine nel PDF facilmente.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: it
og_description: Come firmare un PDF con una firma digitale e incorporare un'immagine
  ritagliata usando Aspose.Pdf in C#. Segui questa guida per una soluzione completa.
og_title: Come firmare PDF e aggiungere immagini – tutorial C# passo passo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Come firmare PDF e aggiungere immagini – Guida completa C#
url: /it/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come firmare PDF e aggiungere immagini – Guida completa C#

Ti sei mai chiesto **come firmare PDF** in modo programmatico inserendo anche un'immagine personalizzata? Forse stai costruendo un flusso di approvazione e hai bisogno di una firma legalmente vincolante *e* di una miniatura della foto del firmatario nella stessa pagina. In breve, vuoi **add digital signature pdf** content, crop that picture, e poi **add image to pdf** senza sforzo.  

Questo tutorial ti guida passo passo—dalla lettura di un certificato ECDSA PKCS#7 al ritaglio di un JPEG e al suo inserimento nella pagina firmata. Alla fine avrai un unico file C# eseguibile che firma la pagina 1, ritaglia una foto a 400 × 400 px e la posiziona in modo preciso. Nessuno script esterno, nessuna magia, solo codice chiaro e spiegazioni.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.7+)
- **Aspose.Pdf for .NET** pacchetto NuGet (versione 23.9 o più recente)
- Un certificato ECDSA P‑256 in formato PKCS#7 (`.pfx`) e la relativa password
- Un’immagine JPEG da incorporare (ad es., `photo.jpg`)

> **Consiglio esperto:** Tieni il file del certificato fuori dal controllo del codice sorgente e proteggi la password con un gestore di segreti.

---

## Passo 1: Configurare il progetto e le importazioni

Per prima cosa, crea un’app console (o integra questo codice in un servizio esistente). Aggiungi il riferimento a Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Quindi includi gli spazi dei nomi necessari:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

Queste istruzioni `using` ti danno accesso alle classi `Document`, `Signature` e `Rectangle` che utilizzeremo più avanti.

## Passo 2: Caricare il PDF e preparare la firma

Apriremo un PDF esistente (`source.pdf`) e creeremo un oggetto **digital signature pdf** che utilizza una firma PKCS#7 detached. Il certificato è una chiave ECDSA P‑256, ampiamente accettata per la conformità.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Perché è importante:** L’utilizzo di una firma PKCS#7 detached mantiene intatto il contenuto originale del PDF mentre incorpora un hash crittografico. Questo è l’approccio standard del settore per PDF legalmente vincolanti.

## Passo 3: Applicare la firma digitale a una pagina specifica

Ora posizioneremo il campo firma visibile sulla **pagina 1**. Il rettangolo definisce dove appare la casella della firma (le coordinate sono in punti, dove 1 inch = 72 punti).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

Se non ti serve una casella visibile, imposta `isVisible` a `false`. Il `signatureRect` può essere regolato per adattarsi al layout del tuo documento.

## Passo 4: Aprire lo stream dell’immagine e definire le aree di ritaglio

Leggeremo il file JPEG in uno stream e specificheremo un **source rectangle** che seleziona i primi 400 × 400 pixel in alto a sinistra. Questa è l’operazione **crop image for pdf**.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Caso limite:** Se la tua immagine è più piccola di 400 × 400, il ritaglio verrà automaticamente limitato alle dimensioni reali dell’immagine—non verrà sollevata alcuna eccezione.

## Passo 5: Definire dove deve apparire l’immagine ritagliata

Successivamente, imposta il **destination rectangle** sulla pagina PDF. In questo esempio posizioniamo l’immagine a (50, 50) con una dimensione di 200 × 200 punti (≈2,78 pollici quadrati).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

Sentiti libero di sperimentare: cambia le coordinate X/Y per spostare l’immagine, o modifica larghezza/altezza per scalare.

## Passo 6: Inserire l’immagine ritagliata nella pagina firmata

Infine, aggiungiamo l’immagine alla **pagina 1** (la stessa pagina che ora contiene la firma). L’overload `AddImage` che utilizziamo accetta i rettangoli di origine e destinazione, eseguendo effettivamente il ritaglio e il posizionamento in una sola chiamata.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

Dietro le quinte, Aspose.Pdf estrae la regione di 400 × 400 pixel, la ridimensiona a 200 × 200 punti e la scrive nello stream di contenuto del PDF.

## Passo 7: Salvare il PDF firmato e arricchito di immagine

Dopo tutte le modifiche, persisti il documento. Puoi sovrascrivere l’originale o scrivere in un nuovo file.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

Quando apri `output_signed.pdf` in Adobe Acrobat o in qualsiasi visualizzatore PDF, vedrai:

- Un campo firma visibile alle coordinate specificate.
- La foto ritagliata posizionata a (50, 50) sulla pagina 1.
- La firma digitale convalidata (a condizione che il visualizzatore riconosca il tuo certificato).

## Domande frequenti (FAQ)

| Question | Answer |
|----------|--------|
| **Posso firmare una pagina diversa?** | Modifica l'argomento `pageNumber` in `signature.Sign` a qualsiasi indice di pagina valido (basato su 1). |
| **E se ho bisogno di più firme?** | Crea una nuova istanza `Signature` per ogni pagina o posizione, riutilizzando lo stesso `pkcsSignature` se si applica lo stesso certificato. |
| **Il ritaglio dell'immagine è limitato a rettangoli?** | Sì, `AddImage` di Aspose.Pdf funziona con regioni rettangolari. Per forme complesse dovresti pre‑processare l'immagine (ad es., usando System.Drawing) prima di incorporarla. |
| **Come rendere la firma invisibile?** | Imposta `isVisible` a `false` e ometti `signatureRect`. La firma sarà comunque crittograficamente valida. |
| **Quali formati posso incorporare oltre a JPEG?** | PNG, BMP, GIF e TIFF sono tutti supportati. Basta cambiare il percorso del file e assicurarsi che lo stream legga i byte corretti. |

## Esempio completo funzionante

Di seguito trovi il programma completo, autonomo. Copialo in `Program.cs`, adatta i percorsi e avvialo.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Risultato atteso:** Aprendo `output_signed.pdf` vedrai un campo firma (100 × 100 → 300 × 300 punti) e un’immagine di 200 × 200 punti derivata dall’angolo in alto a sinistra di `photo.jpg`. La firma si convalida con il certificato ECDSA fornito.

## Conclusioni

Abbiamo coperto **come firmare PDF**, come **add digital signature pdf** a una pagina specifica, come **crop image for pdf**, e infine come **add image to pdf** usando Aspose.Pdf in C#. L’intero flusso—dalla lettura del certificato al salvataggio del documento finale—entra in un unico file sorgente chiaro e leggibile.

Se sei pronto per la prossima sfida, considera:

- Aggiungere **multiple signatures** su pagine diverse (usa il concetto di “digital signature pdf page”).
- Incorporare **QR code** che puntano a servizi di verifica.
- Automatizzare il processo in un’API ASP.NET Core per la generazione di PDF on‑the‑fly.

Ricorda, la chiave per un’automazione PDF robusta è una chiara separazione delle preoccupazioni: gestione della firma, elaborazione dell’immagine e assemblaggio finale del documento. Gioca con le coordinate, cambia il formato dell’immagine o sperimenta con il timestamping—il tuo workflow è ora completamente estensibile.

Hai domande, scenari limite o un caso d’uso interessante da condividere? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}