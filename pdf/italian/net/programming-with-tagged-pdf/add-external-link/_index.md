---
title: Aggiungi un collegamento esterno taggato con tooltip al PDF usando Aspose.Pdf per .NET
weight: 440
limit:
description: Scopri come aggiungere un collegamento ipertestuale esterno taggato con testo visualizzato e tooltip a un PDF usando Aspose.Pdf per .NET.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Scopri come aggiungere un collegamento ipertestuale esterno taggato
    con testo visualizzato e tooltip a un PDF usando Aspose.Pdf per .NET.
  headline: Aggiungi un collegamento esterno taggato con tooltip al PDF usando Aspose.Pdf
    per .NET
  type: TechArticle
- description: Scopri come aggiungere un collegamento ipertestuale esterno taggato
    con testo visualizzato e tooltip a un PDF usando Aspose.Pdf per .NET.
  name: Aggiungi un collegamento esterno taggato con tooltip al PDF usando Aspose.Pdf
    per .NET
  steps:
  - name: Definisci i percorsi per il PDF di origine e il file di risultato.
    text: Definisci i percorsi per il PDF di origine e il file di risultato.
  - name: Verifica che il PDF di origine esista e interrompi l'esecuzione se non può
      essere trovato.
    text: Verifica che il PDF di origine esista e interrompi l'esecuzione se non può
      essere trovato.
  - name: Apri il documento PDF all'interno di un blocco using per garantire il corretto
      rilascio delle risorse.
    text: Apri il documento PDF all'interno di un blocco using per garantire il corretto
      rilascio delle risorse.
  - name: Ottieni il gestore del contenuto taggato per il documento aperto.
    text: Ottieni il gestore del contenuto taggato per il documento aperto.
  - name: Imposta la lingua del documento su English (US) e assegna al PDF un titolo
      derivato dal nome del file.
    text: Imposta la lingua del documento su English (US) e assegna al PDF un titolo
      derivato dal nome del file.
  - name: Recupera l'elemento radice dell'albero della struttura logica a cui verranno
      aggiunti i nuovi elementi.
    text: Recupera l'elemento radice dell'albero della struttura logica a cui verranno
      aggiunti i nuovi elementi.
  - name: Crea un elemento link, imposta il suo testo visualizzato, l'URL di destinazione
      e il titolo tooltip, quindi inseriscilo nella struttura del documento.
    text: Crea un elemento link, imposta il suo testo visualizzato, l'URL di destinazione
      e il titolo tooltip, quindi inseriscilo nella struttura del documento.
  - name: Salva il PDF aggiornato nel file di risultato specificato.
    text: Salva il PDF aggiornato nel file di risultato specificato.
  - name: Emetti un messaggio di conferma che indica dove è stato salvato il PDF modificato.
    text: Emetti un messaggio di conferma che indica dove è stato salvato il PDF modificato.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` restituisce il contenuto taggato esistente se
      il documento è già taggato; non crea un albero duplicato.'
    question: Cosa succede se il PDF di origine è già taggato – la chiamata a `pdfDoc.TaggedContent`
      creerà un nuovo albero di tag o riutilizzerà quello esistente?
  - answer: Sì – individua il `StructureElement` desiderato (ad esempio un `Div` o
      un `Paragraph` su una pagina) tramite l'albero della struttura logica e chiama
      `AppendChild(externalLink)` su quell'elemento.
    question: Posso posizionare il collegamento ipertestuale su una pagina specifica
      invece di aggiungerlo all'elemento radice?
  - answer: Il tooltip viene visualizzato solo se `externalLink.Title` è impostato
      prima di `pdfDoc.Save`; impostarlo dopo il salvataggio non ha effetto sul PDF
      già scritto.
    question: La proprietà `Title` di `LinkElement` è necessaria perché il tooltip
      appaia, e può essere impostata dopo la chiamata a `Save`?
  - answer: Assegna un `FileSpecification` (ad esempio `new FileSpecification("file:///C:/Docs/manual.pdf")`)
      a `externalLink.Hyperlink` invece di usare `WebHyperlink`.
    question: Come creo un collegamento a un file locale invece di un URL web?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Inserisci un collegamento esterno taggato con tooltip in un PDF
og_description: Incorpora un collegamento ipertestuale accessibile con testo visibile e tooltip nel tuo PDF usando Aspose.Pdf per .NET.
og_image_alt: Guida che mostra come aggiungere un collegamento ipertestuale esterno taggato con tooltip a un PDF usando Aspose.Pdf per .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi un collegamento esterno taggato con tooltip al PDF usando Aspose.Pdf per .NET
Questo tutorial mostra come aprire un PDF esistente con Aspose.Pdf per .NET, creare un collegamento ipertestuale esterno taggato che includa il testo visualizzato e un titolo tooltip, inserire il collegamento nella struttura logica del documento e salvare il file aggiornato. Seguendo i passaggi otterrai un PDF accessibile in cui il collegamento fa parte della gerarchia dei tag e fornisce contesto aggiuntivo ai lettori.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: Cosa succede se il PDF di origine è già taggato – la chiamata a `pdfDoc.TaggedContent` creerà un nuovo albero di tag o riutilizzerà quello esistente?**  
A: `pdfDoc.TaggedContent` restituisce il contenuto taggato esistente se il documento è già taggato; non crea un albero duplicato.

**Q: Posso posizionare il collegamento ipertestuale su una pagina specifica invece di aggiungerlo all'elemento radice?**  
A: Sì – individua il `StructureElement` desiderato (ad esempio un `Div` o un `Paragraph` su una pagina) tramite l'albero della struttura logica e chiama `AppendChild(externalLink)` su quell'elemento.

**Q: La proprietà `Title` di `LinkElement` è necessaria perché il tooltip appaia, e può essere impostata dopo la chiamata a `Save`?**  
A: Il tooltip viene visualizzato solo se `externalLink.Title` è impostato prima di `pdfDoc.Save`; impostarlo dopo il salvataggio non ha effetto sul PDF già scritto.

**Q: Come creo un collegamento a un file locale invece di un URL web?**  
A: Assegna un `FileSpecification` (ad esempio `new FileSpecification("file:///C:/Docs/manual.pdf")`) a `externalLink.Hyperlink` invece di usare `WebHyperlink`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}