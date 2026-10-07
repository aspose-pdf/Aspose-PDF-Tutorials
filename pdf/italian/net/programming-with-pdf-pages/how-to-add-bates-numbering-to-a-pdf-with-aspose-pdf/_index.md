---
category: general
date: 2026-10-07
description: Scopri come aggiungere la numerazione Bates a un PDF usando C#. Questa
  guida passo‑passo copre anche la numerazione delle pagine PDF e altri trucchi di
  numerazione.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: it
lastmod: 2026-10-07
og_description: Aggiungi rapidamente la numerazione Bates a un PDF. Segui questo tutorial
  per padroneggiare la numerazione delle pagine PDF, numerare le pagine PDF e automatizzare
  il tracciamento dei documenti.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Aggiungi la numerazione Bates ai PDF in C# – guida completa di Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Come aggiungere la numerazione Bates a un PDF con Aspose.Pdf
url: /it/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere la numerazione Bates a un PDF con Aspose.Pdf

Se hai bisogno di **aggiungere la numerazione bates** a un PDF, questa guida ti mostra esattamente come farlo in C#. Che tu stia preparando fascicoli legali, gestendo fascicoli di caso, o semplicemente voglia una **numerazione delle pagine PDF** affidabile, i passaggi seguenti ti forniscono una soluzione completa e eseguibile.

In questo tutorial imparerai a:

* Caricare un file PDF esistente.
* Configurare le opzioni di numerazione Bates come prefisso, numero iniziale, riempimento cifre, separatore e suffisso.
* Applicare la numerazione a ogni pagina.
* Salvare il documento aggiornato.

Non sono necessari strumenti esterni oltre alla libreria Aspose.Pdf per .NET, e il codice funziona con .NET 6+ così come con .NET Framework 4.7.2+.  

---

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| **Aspose.Pdf for .NET** (pacchetto NuGet `Aspose.Pdf`) | Fornisce le classi `Document` e `BatesNumberingOptions` utilizzate nel codice. |
| **.NET SDK** (consigliato 6.0 o successivo) | Ti consente di compilare ed eseguire l'applicazione console C#. |
| **Un PDF di origine** che desideri numerare | Il tutorial utilizza `source.pdf` come esempio; sostituisci il percorso con il tuo file. |
| **Permesso di scrittura** sulla cartella di output | La chiamata `Save` deve scrivere il nuovo file. |

Puoi installare la libreria con il seguente comando CLI:

```bash
dotnet add package Aspose.Pdf
```

---

## Passo 1: Crea un nuovo progetto console

Apri un terminale ed esegui:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Questo crea un progetto C# minimale che riempiremo con il codice necessario per **aggiungere la numerazione bates**.

---

## Passo 2: Aggiungi le direttive `using` richieste

Apri `Program.cs` e aggiungi gli spazi dei nomi all'inizio del file:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` ti dà accesso alla classe `Document` per caricare e salvare PDF.  
* `Aspose.Pdf.Text` contiene `BatesNumberingOptions`, l'oggetto che definisce come appaiono i numeri.

---

## Passo 3: Carica il PDF di origine

La prima riga operativa carica il PDF che desideri numerare. Sostituisci `"YOUR_DIRECTORY/source.pdf"` con il percorso reale del tuo file.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Se il file non viene trovato, Aspose lancia una `FileNotFoundException`. Per evitarlo, potresti validare il percorso in anticipo:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Passo 4: Definisci le opzioni di numerazione Bates

`BatesNumberingOptions` ti permette di controllare ogni elemento visivo della numerazione. L'esempio sotto mostra una configurazione tipica per fascicoli legali:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Perché ogni proprietà è importante**

| Proprietà | Scopo |
|----------|---------|
| `Prefix` | Ti aiuta a raggruppare i documenti per progetto, cliente o caso. |
| `StartNumber` | Imposta il contatore iniziale; utile quando hai già file numerati. |
| `Digits` | Garantisce una larghezza uniforme, facilitando l'ordinamento. |
| `Separator` | Migliora la leggibilità, specialmente quando si combinano prefisso e suffisso. |
| `Suffix` | Ti permette di aggiungere un anno, una versione o qualsiasi identificatore finale. |

Puoi anche controllare la posizione (top, bottom, left, right) e lo stile del carattere accedendo a `batesOptions.Position` e `batesOptions.Font`. Per la maggior parte degli scenari i valori predefiniti (in basso‑a‑destra, Times New Roman 12 pt) funzionano bene.

---

## Passo 5: Applica la numerazione a ogni pagina

Chiamando `pdf.BatesNumbering.Add` inserisci i numeri su ogni pagina nell'ordine in cui compaiono.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Se hai bisogno di **numerare le pagine PDF** solo su un sottoinsieme (ad esempio, saltare la pagina di copertina), puoi passare una `PageCollection` invece:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Passo 6: Salva il PDF aggiornato

Infine, scrivi il documento modificato su disco. Il nome del file di solito riflette il fatto che il PDF ora contiene numeri Bates.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Se la cartella di output non esiste, Aspose la crea automaticamente. Tuttavia, dovresti assicurarti di avere i permessi di scrittura per evitare una `UnauthorizedAccessException`.

---

## Esempio completo, eseguibile

Mettiamo insieme tutti i pezzi: ecco un programma completo che puoi copiare, incollare ed eseguire:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Output previsto** (console):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Apri `bates_numbered.pdf` e vedrai ogni pagina etichettata con qualcosa come `CASE-001000-2025`, `CASE-001001-2025`, ecc., posizionata nell'angolo in basso‑a‑destra predefinito.

---

## Domande frequenti (FAQ)

### 1. Posso cambiare la posizione dei numeri?
Sì. Imposta `batesOptions.Position = new Position(10, 10, 10, 10);` dove i quattro valori rappresentano i margini dal top, bottom, left e right. Aspose fornisce anche enum predefiniti come `BatesNumberingPosition.BottomCenter`.

### 2. E se il mio PDF contiene già numeri di pagina?
L'aggiunta dei numeri Bates **si sovrapporrà** a quelli esistenti. Per evitare confusione visiva, nascondi i numeri originali (se fanno parte di un livello di testo) o regola la dimensione del carattere e la posizione in `batesOptions`.

### 3. Questo funziona con PDF criptati?
Aspose può aprire PDF protetti da password se fornisci la password:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

### 4. Come **numerare le pagine PDF** con un semplice contatore sequenziale (senza prefisso/suffisso)?
Imposta semplicemente `Prefix = string.Empty` e `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Posso usare questo approccio in ASP.NET Core per servire PDF al volo?
Assolutamente. Carica il documento, applica la numerazione, poi scrivi lo stream nella risposta HTTP:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Casi limite e consigli di best‑practice

| Situazione | Approccio consigliato |
|-----------|----------------------|
| **PDF di grandi dimensioni (centinaia di pagine)** | Chiama `pdf.BatesNumbering.Add` **dopo** aver eseguito eventuali trasformazioni a livello di pagina per evitare di rielaborare le stesse pagine più volte. |
| **Font personalizzati** | Imposta `batesOptions.Font = FontRepository.FindFont("Arial")` e regola `batesOptions.FontSize` per una migliore leggibilità sui documenti scansionati. |
| **Job batch critici per le prestazioni** | Riutilizza una singola istanza `Document` quando elabori molti file in un ciclo; disposiziona dell'oggetto dopo ogni iterazione per liberare memoria. |
| **Caratteri internazionali** | Usa font compatibili Unicode (ad esempio, `Times New Roman Unicode`) per garantire che il prefisso o suffisso venga visualizzato correttamente. |
| **Compatibilità di versione** | Il codice funziona con Aspose.Pdf 23.10 e versioni successive. Se punti a una versione più vecchia, controlla la documentazione API per eventuali modifiche ai nomi delle proprietà. |

---

## Conclusione

Ora sai come **aggiungere la numerazione bates** a un PDF usando Aspose.Pdf per .NET. Il tutorial ha coperto il caricamento di un PDF, la configurazione di `BatesNumberingOptions`, l'applicazione dei numeri a ciascuna pagina e il salvataggio del risultato. Con questi blocchi di costruzione puoi anche implementare la **numerazione delle pagine PDF** generica, **numerare le pagine PDF** con formati personalizzati e integrare il processo in pipeline di automazione più ampie.

**Passi successivi**

* Esplora ulteriormente l'API **bates numbering pdf** per personalizzare font, colore e posizione.  
* Combina questa tecnica con **digital signatures** per creare fascicoli legali a prova di manomissione.  
* Approfondisci le capacità di **PDF merging** di Aspose se devi concatenare più fascicoli prima della numerazione.

Sentiti libero di sperimentare con prefissi, suffissi e lunghezze di cifra diverse per adeguarle agli standard di archiviazione della tua organizzazione. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea documento PDF C# – Guida all'aggiunta della numerazione Bates](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [Come aggiungere la numerazione Bates in PDF con C# – Guida completa](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Tutorial Aspose PDF – Inserisci una pagina vuota e aggiorna la numerazione Bates](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}