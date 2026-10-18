---
category: general
date: 2026-02-09
description: Verifica la firma PDF con Aspose.PDF in C#. Scopri come aggiungere un
  rettangolo al PDF, salvare il PDF aggiornato e utilizzare le funzionalità di firma
  di Aspose PDF.
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: it
og_description: Verifica la firma PDF in C# rapidamente. Questa guida mostra come
  aggiungere grafica al PDF, salvare il PDF aggiornato e utilizzare le API di firma
  PDF di Aspose.
og_title: Verifica la firma PDF e aggiungi un rettangolo PDF – Guida completa di Aspose
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: Verifica la firma PDF e aggiungi un rettangolo al PDF con Aspose
url: /it/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# verifica firma PDF e aggiungi rettangolo PDF con Aspose

Hai mai dovuto **verificare la firma PDF** in un progetto C# ma non sapevi da dove cominciare? Non sei solo: le firme digitali sono indispensabili per la conformità, e molti sviluppatori incontrano difficoltà quando devono anche modificare il documento successivamente.  

In questo tutorial percorreremo un esempio completo e funzionante che **verifica la firma PDF**, aggiunge un **rettangolo** alla prima pagina, controlla che la forma rimanga entro i limiti della pagina e infine **salva il PDF aggiornato**—tutto usando le moderne API di Aspose.PDF. Alla fine avrai un unico programma autonomo da inserire in qualsiasi soluzione .NET.

## Cosa imparerai

- Caricare un PDF firmato con Aspose.PDF.  
- Utilizzare le classi **aspose pdf signature** per verificare ogni firma e rilevare compromissioni.  
- **Aggiungere rettangolo PDF** in modo sicuro, assicurandoti che rientri nella pagina.  
- **Salvare PDF aggiornato** mantenendo le firme esistenti.  
- Suggerimenti, gestione dei casi limite e errori comuni.

Nessuna documentazione esterna è necessaria—tutto ciò che ti serve è qui.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7+).  
- Pacchetto NuGet Aspose.PDF per .NET (≥ 23.10). Installa con:

```bash
dotnet add package Aspose.Pdf
```

- Un file PDF firmato chiamato `signed.pdf` collocato in una cartella a tua scelta (sostituisci `YOUR_DIRECTORY` nel codice).  
- Familiarità di base con C# e Visual Studio o VS Code.

> **Pro tip:** Se non hai a disposizione un PDF firmato, Aspose fornisce un file demo gratuito sul loro sito che puoi scaricare per i test.

---

## verifica firma PDF – Passo dopo passo

La prima cosa da fare è aprire il documento e scorrere tutte le firme digitali. Aspose.PDF offre due metodi utili: `VerifySignature` indica se il controllo crittografico è superato, mentre il più recente `IsSignatureCompromised` segnala eventuali manomissioni avvenute dopo la firma.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**Perché è importante:**  
- `VerifySignature` da solo conferma solo che il certificato del firmatario è ancora attendibile.  
- `IsSignatureCompromised` rileva modifiche sottili—come l’aggiunta di un oggetto nascosto—così sai se il contenuto visivo del PDF è stato alterato dopo la firma.

**Output previsto** (esempio con due firme):

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

Se qualche firma restituisce `compromised=True`, dovresti interrompere l’elaborazione o avvisare l’utente, perché l’integrità del documento non può essere garantita.

---

## aggiungi rettangolo PDF a una pagina

Ora che abbiamo confermato che le firme sono intatte (o almeno siamo consapevoli di eventuali compromissioni), aggiungiamo un semplice rettangolo grafico. È utile per timbrare “Revisionato”, evidenziare sezioni o semplicemente attirare l’attenzione su una zona.

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**Cosa significano i numeri:**  
- Il sistema di coordinate PDF parte dall’angolo in basso a sinistra.  
- Nell’esempio, il rettangolo si estende per 100 punti in orizzontale e 100 punti in verticale, posizionato più o meno al centro di una tipica pagina A4.

> **Nota:** Aspose supporta anche `AddEllipse`, `AddPolygon`, ecc., se ti servono forme più complesse.

---

## verifica i limiti grafici – assicurati che il rettangolo rientri

Prima di confermare le modifiche, è consigliabile verificare che la grafica rimanga all’interno dell’area stampabile della pagina. Il nuovo metodo `CheckGraphicsBounds` fa esattamente questo.

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

Se `shapeFits` restituisce `false`, dovrai regolare le coordinate del rettangolo—magari riducendolo o spostandolo più in basso nella pagina. Questo evita ritagli accidentali che possono apparire poco professionali, soprattutto quando il PDF viene stampato.

---

## salva PDF aggiornato – conserva firme e nuove grafiche

Infine, scriviamo il documento modificato su disco. Il metodo `Save` rispetta le firme esistenti; non le invaliderà a meno che il contenuto non sia realmente cambiato (cosa già verificata con `IsSignatureCompromised`).

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**Perché usare un nuovo file?**  
Salvare sopra l’originale potrebbe cancellare le firme originali, rendendo impossibile confrontare gli stati prima/dopo. Scrivendo su `output.pdf` mantieni la sorgente per scopi di audit.

---

## Esempio completo, eseguibile

Di seguito trovi il programma completo da copiare‑incollare in una console app. Tutti i passaggi sono combinati, i commenti spiegano ogni blocco e vedrai l’output console previsto alla fine.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**Output console previsto** (supponendo una firma valida e non compromessa):

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

Se una firma è compromessa, vedrai `compromised=True` e potrai decidere se continuare.

---

## Domande frequenti e gestione dei casi limite

| Domanda | Risposta |
|----------|----------|
| **E se il PDF non ha firme?** | `GetSignNames()` restituisce una collezione vuota; il ciclo salta semplicemente e puoi comunque aggiungere grafiche. |
| **Posso aggiungere più rettangoli?** | Sì—basta chiamare `AddRectangle` più volte con diversi oggetti `Rectangle`. |
| **Cosa fare con PDF protetti da password?** | Caricali con `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` prima della verifica. |
| **L’aggiunta di grafiche invalida una firma valida?** | Solo se la firma copre la pagina dove inserisci le grafiche. Usa `IsSignatureCompromised` per rilevare questo; altrimenti la firma rimane intatta. |
| **Devo chiudere le risorse?** | Gli oggetti Aspose.PDF sono gestiti; lo smaltimento è opzionale, ma puoi avvolgere il codice in un blocco `using` per maggiore sicurezza. |

---

## Pro tip per l’uso in produzione

- **Elaborazione batch:** Incapsula l’intera routine in un metodo che accetta percorsi di input/output; poi passa una lista di file a un `Parallel.ForEach` per velocizzare.  
- **Logging:** Sostituisci `Console.WriteLine` con un logger appropriato (es. Serilog) per registrare i risultati della verifica nei log di audit.  
- **Policy di firma:** Combina `VerifySignature` con un controllo di revoca del certificato (OCSP/CRL) per una conformità più rigorosa.  
- **Stile grafico:** Usa `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });` per far risaltare il rettangolo.  
- **Blocco versione:** Fissa la versione del pacchetto NuGet Aspose.PDF per evitare rotture dovute a aggiornamenti della libreria.

---

## Conclusione

Ora disponi di un esempio solido, end‑to‑end, che **verifica la firma PDF**, **aggiunge rettangolo PDF** e **salva il PDF aggiornato** usando le ultime API di Aspose.PDF. Il codice controlla le firme compromesse, garantisce che le grafiche rimangano entro i limiti della pagina e preserva le firme digitali originali—esattamente ciò che richiede un flusso di lavoro di conformità reale.

Prossimi passi consigliati:

- Aggiungere **grafica PDF** come filigrane o codici QR.  
- Usare l’API **aspose pdf signature** per creare nuove firme programmaticamente.  
- Automatizzare il processo in un servizio web ASP.NET Core per la validazione dei documenti al volo.

Provalo, modifica le coordinate del rettangolo e osserva come la libreria reagisce a diverse strutture PDF. Buona programmazione, e che i tuoi PDF rimangano sia firmati che eleganti! 

![verify pdf signature example](image.png "verify pdf signature example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}