---
category: general
date: 2026-08-04
description: Aggiungi un rettangolo al PDF usando C#. Scopri come disegnare una forma
  in PDF con C# e Aspose.Pdf in un esempio chiaro e completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: it
lastmod: 2026-08-04
og_description: Aggiungi un rettangolo al PDF usando C#. Questo tutorial mostra come
  disegnare forme in PDF con C# in modo rapido e affidabile.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Aggiungi un rettangolo al PDF con C# – guida completa di programmazione
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aggiungi un rettangolo al PDF con C# – guida passo‑a‑passo
url: /it/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere un rettangolo a PDF con C# – guida passo‑passo

Se hai bisogno di **add rectangle to PDF** file da un'applicazione C#, questa guida ti mostra esattamente come farlo. Vedrai un esempio completo e eseguibile che disegna una forma in PDF C# usando la libreria Aspose.Pdf, e comprenderai perché ogni riga di codice è importante.

Disegnare forme nei PDF è una necessità comune per generatori di report, modelli di fatture e branding personalizzato dei documenti. Alla fine di questo tutorial potrai inserire qualsiasi annotazione rettangolare, modificarne dimensioni, colore o posizione, e salvare il documento modificato senza perdere il contenuto esistente.

**Cosa imparerai**

* Come caricare un PDF esistente con Aspose.Pdf.
* Come definire i limiti del rettangolo e creare una forma rettangolare.
* Come aggiungere il rettangolo alla collezione di paragrafi di una pagina.
* Come salvare il PDF aggiornato e verificare il risultato.
* Varianti per più pagine, trasparenza e stili di linea personalizzati.

**Prerequisiti**

* .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.7+).
* Visual Studio 2022 o qualsiasi IDE C#.
* Un riferimento NuGet a `Aspose.Pdf` (versione di prova gratuita o licenziata).
* Un file PDF di input chiamato `input.pdf` posizionato in una cartella a tua scelta.

---

## Come disegnare una forma in PDF C# – configurare il progetto

1. **Crea un nuovo progetto console**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Aggiungi il pacchetto Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Posiziona `input.pdf`** nella directory del progetto (o in qualsiasi cartella a cui fai riferimento in seguito).

Il progetto è ora pronto per compilare il codice che **add rectangle to PDF** file.

---

## Passo 1: Caricare il documento PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*La classe `Document` analizza il file ed espone una collezione `Pages`. Il caricamento è la prima operazione necessaria prima che possa avvenire qualsiasi disegno.*

---

## Passo 2: Scegliere la pagina di destinazione

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Se devi aggiungere il rettangolo a una pagina diversa, sostituisci l'indice con il numero di pagina desiderato. La libreria genera un'eccezione quando l'indice è fuori intervallo, quindi assicurati che il PDF contenga un numero sufficiente di pagine.*

---

## Passo 3: Definire i limiti del rettangolo

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Il sistema di coordinate utilizza punti (1 pt = 1/72 pollice). L'esempio crea un rettangolo largo 250 pt e alto 100 pt vicino alla parte superiore della pagina. Regola i numeri per adattarli al tuo layout.*

---

## Passo 4: Creare la forma rettangolo

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*La classe `Rectangle` eredita da `GraphicalObject`. Impostare `FillColor` e `Border` è opzionale, ma dimostra come controllare l'aspetto quando **how to draw shape in PDF C#** oltre un semplice contorno.*

---

## Passo 5: Aggiungere il rettangolo alla pagina

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*I paragrafi sono il contenitore per qualsiasi oggetto disegnabile. Inserendo la forma in `Paragraphs`, Aspose.Pdf la renderizza quando il documento viene salvato.*

---

## Passo 6: Salvare il PDF modificato

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Il salvataggio crea un nuovo file così il `input.pdf` originale rimane invariato. Puoi sovrascrivere il file sorgente passando lo stesso percorso, ma mantenere un backup è una buona pratica.*

---

## Codice sorgente completo (eseguibile)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Output previsto** – Apri `output.pdf` in qualsiasi visualizzatore PDF. Dovresti vedere un rettangolo riempito di blu vicino all'angolo in alto a destra della prima pagina, contornato da un bordo grigio scuro.

---

## Come disegnare una forma in PDF C# su più pagine

Se devi **add rectangle to PDF** su ogni pagina, itera sulla collezione `Pages`:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Questo modello riutilizza gli stessi limiti su ogni pagina. Regola le coordinate per pagina se ti servono posizioni diverse.*

---

## Problemi comuni e consigli di best‑practice

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| Il rettangolo appare fuori dalla pagina | Le coordinate sono misurate dal basso‑sinistra; usare un sistema di coordinate orientato verso l'alto può creare confusione. | Ricorda che l'asse Y cresce verso l'alto. Usa valori che rientrano nelle dimensioni della pagina (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| La forma è invisibile | Opacità di riempimento impostata a `0` o larghezza del bordo impostata a `0`. | Assicurati che `FillOpacity` sia maggiore di `0` e che `Border.Width` sia almeno `0.5`. |
| Il salvataggio genera `AccessDeniedException` | Il file di output è aperto in un altro programma. | Chiudi eventuali visualizzatori prima di eseguire il codice, oppure salva in un percorso diverso. |
| Il rettangolo si sovrappone al contenuto esistente | Non è stato impostato alcun controllo di layering. | Usa la proprietà `ZIndex` (valori più alti vengono renderizzati sopra) se hai bisogno di controllare il layering. |

---

## Estendere il rettangolo – gradienti, rotazione e trasparenza

Aspose.Pdf supporta grafica avanzata. Per creare un rettangolo ruotato con un gradiente lineare:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Lo stesso schema di codice dimostra **how to draw shape in PDF C#** con effetti visivi più ricchi.*

---

## Verificare il risultato programmaticamente

Puoi confermare che il rettangolo sia stato aggiunto controllando il conteggio dei paragrafi della pagina:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Se il conteggio è aumentato di uno dopo l'inserimento, l'operazione è riuscita.

---

## Conclusione

Ora sai come **add rectangle to PDF** file usando C#. Il tutorial ha coperto il caricamento di un documento, la definizione dei limiti, la creazione di una forma rettangolare, l'inserimento nella pagina e il salvataggio del risultato. Hai anche visto come gestire più pagine, evitare errori comuni e applicare stili avanzati.

Successivamente, esplora argomenti correlati come **how to draw shape in PDF C#** per cerchi, poligoni o percorsi liberi, e impara a combinare forme con testo e immagini per creare report PDF completi.

Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiungere timbri di pagina nei PDF usando Aspose.PDF per .NET | Guida a filigrane e sfondi](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [Come aggiungere un timbro immagine a un PDF usando Aspose.PDF per .NET: Guida completa](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Come aggiungere una filigrana immagine rotante ai PDF usando Aspose.PDF per .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}