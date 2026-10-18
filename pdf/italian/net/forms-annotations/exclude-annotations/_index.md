---
title: Confronto PDF side‑by‑side escludendo le annotazioni con Aspose.Pdf per .NET
weight: 101
limit:
description: Guida passo‑passo per confrontare PDF ed escludere le aree di annotazione usando Aspose.Pdf per .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Guida passo‑passo per confrontare PDF ed escludere le aree di annotazione
    usando Aspose.Pdf per .NET.
  headline: Confronto PDF side‑by‑side escludendo le annotazioni con Aspose.Pdf per
    .NET
  type: TechArticle
- description: Guida passo‑passo per confrontare PDF ed escludere le aree di annotazione
    usando Aspose.Pdf per .NET.
  name: Confronto PDF side‑by‑side escludendo le annotazioni con Aspose.Pdf per .NET
  steps:
  - name: Definisci i percorsi dei file per il PDF primario, il PDF secondario e il
      PDF diff di output.
    text: Definisci i percorsi dei file per il PDF primario, il PDF secondario e il
      PDF diff di output.
  - name: Verifica che entrambi i file PDF di input esistano e interrompi con un messaggio
      di errore se uno dei due è mancante.
    text: Verifica che entrambi i file PDF di input esistano e interrompi con un messaggio
      di errore se uno dei due è mancante.
  - name: Apri i due file PDF come oggetti Document (pdfA e pdfB) all'interno di un
      blocco using in modo che vengano eliminati automaticamente.
    text: Apri i due file PDF come oggetti Document (pdfA e pdfB) all'interno di un
      blocco using in modo che vengano eliminati automaticamente.
  - name: Raccogli i rettangoli di delimitazione di ogni annotazione in pdfA e salvali
      in ignoredRectsA.
    text: Raccogli i rettangoli di delimitazione di ogni annotazione in pdfA e salvali
      in ignoredRectsA.
  - name: Raccogli i rettangoli di delimitazione di ogni annotazione in pdfB e salvali
      in ignoredRectsB.
    text: Raccogli i rettangoli di delimitazione di ogni annotazione in pdfB e salvali
      in ignoredRectsB.
  - name: Crea un oggetto SideBySideComparisonOptions e assegna i rettangoli di annotazione
      precedentemente raccolti a ExcludeAreas1 e ExcludeAreas2 in modo che tali regioni
      vengano ignorate durante il confronto.
    text: Crea un oggetto SideBySideComparisonOptions e assegna i rettangoli di annotazione
      precedentemente raccolti a ExcludeAreas1 e ExcludeAreas2 in modo che tali regioni
      vengano ignorate durante il confronto.
  - name: Esegui il confronto PDF side‑by‑side utilizzando i due oggetti Document
      e le opzioni configurate, scrivendo il risultato in outputPdf.
    text: Esegui il confronto PDF side‑by‑side utilizzando i due oggetti Document
      e le opzioni configurate, scrivendo il risultato in outputPdf.
  - name: Elimina gli oggetti Document e esci dal blocco using.
    text: Elimina gli oggetti Document e esci dal blocco using.
  - name: Stampa un messaggio di conferma che indica che il confronto è completato
      e dove è stato salvato il PDF diff.
    text: Stampa un messaggio di conferma che indica che il confronto è completato
      e dove è stato salvato il PDF diff.
  type: HowTo
- questions:
  - answer: Sì. Il codice semplicemente non aggiunge rettangoli all'elenco `ignoredRects`
      corrispondente, quindi `ExcludeAreas1`/`ExcludeAreas2` ricevono un array vuoto
      e il comparatore elabora l'intera pagina.
    question: Cosa succede se una pagina PDF non ha annotazioni – il confronto funzionerà
      comunque?
  - answer: Imposta `ExcludeAreas1` (o `ExcludeAreas2`) sui rettangoli raccolti e
      lascia l'altra proprietà come array vuoto; il comparatore ignorerà le regioni
      solo nel documento specificato.
    question: Posso escludere solo le annotazioni da un documento mantenendo le annotazioni
      dell'altro nel diff?
  - answer: I rettangoli sovrapposti vengono uniti internamente dal comparatore, quindi
      i limiti di annotazione sovrapposti sono esclusi in modo sicuro senza conteggi
      duplicati.
    question: I rettangoli di annotazione sovrapposti causano problemi con `ExcludeAreas`?
  - answer: Sì, imposta `compareOpts.ExcludeTables = true;` – questa opzione funziona
      insieme a `ExcludeAreas1`/`ExcludeAreas2` per ignorare anche le regioni delle
      tabelle.
    question: Esiste un modo per escludere le tabelle oltre alle annotazioni usando
      lo stesso oggetto di opzioni?
  - answer: Il codice verifica `if (a != null && a.Rect != null)` prima di aggiungere
      alla lista, quindi i rettangoli null vengono semplicemente ignorati e non viene
      generata alcuna eccezione.
    question: Cosa succede se la proprietà `Rect` di un'annotazione è null – il codice
      genererà un'eccezione?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Confronta PDF senza annotazioni
og_description: Esegui un diff PDF side‑by‑side che salta tutti i segni di annotazione.
og_image_alt: Guida che mostra un confronto PDF side‑by‑side che esclude le regioni di annotazione usando Aspose.Pdf per .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Confronto PDF side‑by‑side escludendo le annotazioni con Aspose.Pdf per .NET
Questo tutorial mostra come confrontare due file PDF usando Aspose.Pdf per .NET ignorando qualsiasi contenuto di annotazione. Estrae i riquadri di delimitazione di tutte le annotazioni da ciascun documento, li passa a SideBySideComparisonOptions e poi esegue un confronto side‑by‑side. Il risultato è un PDF diff che evidenzia solo le modifiche non legate alle annotazioni.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: Cosa succede se una pagina PDF non ha annotazioni – il confronto funzionerà comunque?**  
A: Sì. Il codice semplicemente non aggiunge rettangoli all'elenco `ignoredRects` corrispondente, quindi `ExcludeAreas1`/`ExcludeAreas2` ricevono un array vuoto e il comparatore elabora l'intera pagina.

**Q: Posso escludere solo le annotazioni da un documento mantenendo le annotazioni dell'altro nel diff?**  
A: Imposta `ExcludeAreas1` (o `ExcludeAreas2`) sui rettangoli raccolti e lascia l'altra proprietà come array vuoto; il comparatore ignorerà le regioni solo nel documento specificato.

**Q: I rettangoli di annotazione sovrapposti causano problemi con `ExcludeAreas`?**  
A: I rettangoli sovrapposti vengono uniti internamente dal comparatore, quindi i limiti di annotazione sovrapposti sono esclusi in modo sicuro senza conteggi duplicati.

**Q: Esiste un modo per escludere le tabelle oltre alle annotazioni usando lo stesso oggetto di opzioni?**  
A: Sì, imposta `compareOpts.ExcludeTables = true;` – questa opzione funziona insieme a `ExcludeAreas1`/`ExcludeAreas2` per ignorare anche le regioni delle tabelle.

**Q: Cosa succede se la proprietà `Rect` di un'annotazione è null – il codice genererà un'eccezione?**  
A: Il codice verifica `if (a != null && a.Rect != null)` prima di aggiungere alla lista, quindi i rettangoli null vengono semplicemente ignorati e non viene generata alcuna eccezione.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}