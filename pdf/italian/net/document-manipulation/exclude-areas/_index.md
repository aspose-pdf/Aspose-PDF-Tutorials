---
title: Confronta PDF ignorando aree specifiche usando Aspose.Pdf per .NET
weight: 201
limit:
description: Impara a confrontare PDF fianco a fianco e a ignorare le regioni selezionate usando Aspose.Pdf per .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Impara a confrontare PDF fianco a fianco e a ignorare le regioni selezionate
    usando Aspose.Pdf per .NET.
  headline: Confronta PDF ignorando aree specifiche usando Aspose.Pdf per .NET
  type: TechArticle
- description: Impara a confrontare PDF fianco a fianco e a ignorare le regioni selezionate
    usando Aspose.Pdf per .NET.
  name: Confronta PDF ignorando aree specifiche usando Aspose.Pdf per .NET
  steps:
  - name: Definisci i percorsi dei file per i due PDF di origine e per il PDF di differenza
      di output.
    text: Definisci i percorsi dei file per i due PDF di origine e per il PDF di differenza
      di output.
  - name: Verifica che entrambi i file PDF di origine esistano e interrompi con un
      messaggio di errore se uno dei due è mancante.
    text: Verifica che entrambi i file PDF di origine esistano e interrompi con un
      messaggio di errore se uno dei due è mancante.
  - name: Crea un array contenente l'area rettangolare da ignorare nel primo PDF.
    text: Crea un array contenente l'area rettangolare da ignorare nel primo PDF.
  - name: Crea un array contenente l'area rettangolare da ignorare nel secondo PDF.
    text: Crea un array contenente l'area rettangolare da ignorare nel secondo PDF.
  - name: Configura il confronto fianco a fianco, assegnando gli array delle aree
      da ignorare alle proprietà appropriate.
    text: Configura il confronto fianco a fianco, assegnando gli array delle aree
      da ignorare alle proprietà appropriate.
  - name: Carica entrambi i PDF ed esegui il confronto fianco a fianco, generando
      il file di differenza nel percorso specificato.
    text: Carica entrambi i PDF ed esegui il confronto fianco a fianco, generando
      il file di differenza nel percorso specificato.
  - name: Stampa un messaggio di conferma che indica che il confronto è stato completato
      e dove è stato salvato il PDF di differenza.
    text: Stampa un messaggio di conferma che indica che il confronto è stato completato
      e dove è stato salvato il PDF di differenza.
  type: HowTo
- questions:
  - answer: Le coordinate sono in punti (1/72 di pollice) con l'origine nell'angolo
      inferiore sinistro della pagina, quindi i primi due numeri rappresentano X/Y
      inferiore sinistro e gli ultimi due X/Y superiore destro.
    question: Quale sistema di coordinate usano i valori `Rectangle` quando si definiscono
      le zone da ignorare?
  - answer: Sì – fornisci più oggetti `Aspose.Pdf.Rectangle` nell'array `ExcludeAreas1`
      (o `ExcludeAreas2`); ogni rettangolo verrà escluso indipendentemente durante
      il confronto.
    question: Posso ignorare più di un'area rettangolare nello stesso documento?
  - answer: No. `ExcludeAreas1` si applica al primo PDF e `ExcludeAreas2` al secondo,
      quindi puoi specificare coordinate diverse per ciascun documento.
    question: I rettangoli da ignorare devono essere identici in entrambi i PDF?
  - answer: Aspose.Pdf ignora silenziosamente i rettangoli che si trovano completamente
      al di fuori della pagina; non hanno alcun effetto sul risultato del confronto.
    question: Cosa succede se un rettangolo è definito al di fuori dei limiti della
      pagina?
  - answer: Gli array `ExcludeAreas` si applicano per pagina, quindi è necessario
      aggiungere lo stesso `Rectangle` alla collezione di ogni pagina (ad esempio,
      iterare su `pdf.Pages` e assegnare l'array) prima di chiamare `SideBySidePdfComparer.Compare`.
    question: Come posso escludere la stessa regione su ogni pagina di un PDF?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Ignora le regioni durante il confronto dei PDF
og_description: Scopri come saltare le aree selezionate in un confronto PDF fianco a fianco e ottenere un PDF di differenza pulito.
og_image_alt: Guida che mostra il confronto PDF fianco a fianco con regioni rettangolari escluse usando Aspose.Pdf per .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Confronta PDF ignorando aree specifiche usando Aspose.Pdf per .NET
Questo tutorial dimostra come confrontare due documenti PDF fianco a fianco con Aspose.Pdf per .NET escludendo le regioni rettangolari designate dall'analisi. Definendo le aree da escludere in ciascun file, il PDF di differenza generato evidenzia solo le modifiche importanti, facilitando la concentrazione sulle differenze rilevanti.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Quale sistema di coordinate usano i valori `Rectangle` quando si definiscono le zone da ignorare?**  
A: Le coordinate sono in punti (1/72 di pollice) con l'origine nell'angolo inferiore sinistro della pagina, quindi i primi due numeri rappresentano X/Y inferiore sinistro e gli ultimi due X/Y superiore destro.

**Q: Posso ignorare più di un'area rettangolare nello stesso documento?**  
A: Sì – fornisci più oggetti `Aspose.Pdf.Rectangle` nell'array `ExcludeAreas1` (o `ExcludeAreas2`); ogni rettangolo verrà escluso indipendentemente durante il confronto.

**Q: I rettangoli da ignorare devono essere identici in entrambi i PDF?**  
A: No. `ExcludeAreas1` si applica al primo PDF e `ExcludeAreas2` al secondo, quindi puoi specificare coordinate diverse per ciascun documento.

**Q: Cosa succede se un rettangolo è definito al di fuori dei limiti della pagina?**  
A: Aspose.Pdf ignora silenziosamente i rettangoli che si trovano completamente al di fuori della pagina; non hanno alcun effetto sul risultato del confronto.

**Q: Come posso escludere la stessa regione su ogni pagina di un PDF?**  
A: Gli array `ExcludeAreas` si applicano per pagina, quindi è necessario aggiungere lo stesso `Rectangle` alla collezione di ogni pagina (ad esempio, iterare su `pdf.Pages` e assegnare l'array) prima di chiamare `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}