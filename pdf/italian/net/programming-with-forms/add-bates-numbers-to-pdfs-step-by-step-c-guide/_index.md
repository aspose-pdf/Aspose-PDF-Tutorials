---
category: general
date: 2026-02-12
description: Aggiungi numeri Bates ai file PDF rapidamente. Scopri come aggiungere
  un campo di testo PDF, un campo modulo PDF e i numeri di pagina PDF usando Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: it
og_description: Aggiungi numeri Bates ai documenti PDF in C#. Questa guida mostra
  come aggiungere un campo di testo PDF, aggiungere un campo modulo PDF e aggiungere
  numeri di pagina PDF con Aspose.PDF.
og_title: Aggiungi numeri Bates ai PDF – Tutorial completo C#
tags:
- PDF
- C#
- Aspose.PDF
title: Aggiungi numeri Bates ai PDF – Guida passo‑passo C#
url: /it/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi numeri Bates ai PDF – Guida completa C#  

Ti è mai capitato di dover **aggiungere numeri Bates** a una pila di PDF legali senza sapere da dove cominciare? Non sei l'unico. In molti studi legali e progetti di e‑discovery, timbrare ogni pagina con un identificatore unico è un compito quotidiano, e farlo manualmente è un incubo.  

La buona notizia? Con poche righe di C# e Aspose.PDF puoi automatizzare l’intero processo. In questo tutorial vedremo **come aggiungere numeri Bates**, inserire un campo di testo su ogni pagina e salvare un PDF pulito e ricercabile—senza sudare.  

> **Cosa otterrai:** un esempio di codice completamente eseguibile, spiegazioni sul perché ogni riga è importante, consigli per i casi limite e una rapida checklist per verificare il risultato.  

Tratteremo anche attività correlate come **add text field pdf**, **add form field pdf** e **add page numbers pdf**, così avrai una cassetta degli attrezzi pronta per qualsiasi sfida di automazione documentale.  

---  

## Prerequisiti  

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+)  
- Visual Studio 2022 (o qualsiasi IDE tu preferisca)  
- Una licenza valida di Aspose.PDF per .NET (la versione di prova gratuita è sufficiente per i test)  
- Un PDF di origine chiamato `source.pdf` collocato in una cartella a cui puoi fare riferimento  

Se qualcuno di questi elementi ti è sconosciuto, fermati e installa ciò che manca prima di proseguire. I passaggi seguenti presumono che tu abbia già aggiunto il pacchetto NuGet Aspose.PDF:  

```bash
dotnet add package Aspose.Pdf
```

---  

## Come aggiungere numeri Bates a un PDF con Aspose.PDF  

Di seguito trovi il programma completo, pronto per il copia‑incolla. Carica un PDF, crea un **campo casella di testo** su ogni pagina, scrive un numero Bates formattato e infine salva il file modificato.  

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Perché funziona  

- **`Document`** è il punto di ingresso; rappresenta l’intero file PDF.  
- **`Rectangle`** definisce dove il campo vive sulla pagina. I numeri sono espressi in punti (1 pt ≈ 1/72 in). Regola le coordinate se vuoi il numero in un angolo diverso.  
- **`TextBoxField`** è un *campo modulo* che può contenere qualsiasi stringa. Assegnando `Value` aggiungiamo effettivamente **add page numbers pdf** con un prefisso personalizzato.  
- **`pdfDocument.Form.Add`** registra il campo nell’AcroForm del PDF, rendendolo visibile in visualizzatori come Adobe Acrobat.  

Se mai dovessi cambiare l’aspetto (font, colore, dimensione) puoi modificare le proprietà di `TextBoxField`—consulta la documentazione Aspose per `DefaultAppearance` e `Border`.  

---  

## Aggiungere un campo di testo a ogni pagina PDF (passo “add text field pdf”)  

A volte vuoi solo un’etichetta visibile, non un campo modulo interattivo. In tal caso puoi sostituire `TextBoxField` con un `TextFragment` e aggiungerlo direttamente alla collezione `Paragraphs` della pagina. Ecco un’alternativa rapida:  

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

L’approccio **add text field pdf** è utile quando il documento finale sarà di sola lettura, mentre il metodo **add form field pdf** mantiene i numeri modificabili in seguito.  

---  

## Salvare il PDF con i numeri Bates (momento “add page numbers pdf”)  

Al termine del ciclo, chiamare `pdfDocument.Save` scrive tutto su disco. Se devi preservare il file originale, cambia semplicemente il percorso di output o usa le overload di `pdfDocument.Save` per inviare il risultato direttamente a una risposta in una Web API.  

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Questa è la parte più pulita—nessun file temporaneo, nessuna libreria aggiuntiva, solo Aspose che si occupa del lavoro pesante.  

---  

## Risultato atteso & verifica rapida  

Apri `bates.pdf` in qualsiasi visualizzatore PDF. Dovresti vedere una piccola casella nell’angolo inferiore sinistro di ogni pagina con il testo:  

```
BATES-00001
BATES-00002
…
```

Se controlli le proprietà del documento, noterai un AcroForm contenente campi chiamati `Bates_1`, `Bates_2`, ecc. Questo conferma che il passo **add form field pdf** è riuscito.  

---  

## Problemi comuni & consigli esperti  

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| I numeri appaiono fuori centro | Le coordinate del rettangolo sono relative all’angolo inferiore sinistro della pagina. | Inverti il valore Y (`pageHeight - marginTop`) o usa `page.PageInfo.Height` per calcolare una posizione con margine superiore. |
| I campi sono invisibili in Adobe Reader | Il bordo predefinito è impostato su “No”. | Imposta `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| PDF di grandi dimensioni causano pressione sulla memoria | `using` rilascia il documento solo dopo la fine del ciclo. | Processa le pagine a blocchi o usa `pdfDocument.Save` con `SaveOptions` che abilita lo streaming. |
| Licenza non applicata | Aspose stampa una filigrana sulla prima pagina. | Registra la licenza subito: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---  

## Estendere la soluzione  

- **Prefissi personalizzati:** Sostituisci `"BATES-"` con qualsiasi stringa (`"DOC-"`, `"CASE-"`, …).  
- **Lunghezza con zero padding:** Cambia `{pageNumber:D5}` in `{pageNumber:D3}` per tre cifre.  
- **Posizionamento dinamico:** Usa `pdfDocument.Pages[pageNumber].PageInfo.Width` per posizionare il campo sul lato destro.  
- **Numerazione condizionale:** Salta le pagine vuote verificando `pdfDocument.Pages[pageNumber].IsBlank`.  

Tutte queste varianti mantengono intatto il modello di base di **add bates numbers**, **add text field pdf** e **add form field pdf**.  

---  

## Esempio completo (tutto in uno)  

Di seguito trovi il programma finale, pronto per l’esecuzione, che incorpora i suggerimenti sopra. Copialo in una nuova console app e premi F5.  

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Eseguilo, apri il risultato e vedrai un identificatore dall’aspetto professionale su ogni pagina—esattamente ciò che si aspetta uno specialista di supporto legale.  

---  

## Conclusione  

Abbiamo appena dimostrato **come aggiungere numeri Bates** a qualsiasi PDF usando C# e Aspose.PDF. Creando un **campo casella di testo** su ogni pagina, aggiungiamo simultaneamente **add text field pdf**, **add form field pdf** e **add page numbers pdf** in un’unica passata. L’approccio è veloce, scalabile e facile da personalizzare per prefissi, layout diversi o logica condizionale.  

Pronto per la prossima sfida? Prova a incorporare un codice QR che rimandi al file del caso originale, o genera una pagina indice separata che elenchi tutti i numeri Bates con i relativi titoli di pagina. La stessa API ti permette di unire PDF, estrarre pagine e persino redigere dati sensibili—il cielo è il limite.  

Se incontri difficoltà, lascia un commento qui sotto o consulta la documentazione ufficiale di Aspose per approfondimenti. Buona programmazione, e che i tuoi PDF rimangano sempre perfettamente numerati!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}