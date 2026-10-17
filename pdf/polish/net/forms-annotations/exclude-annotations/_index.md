---
title: Porównanie PDF side‑by‑side z wykluczeniem adnotacji przy użyciu Aspose.Pdf for .NET
weight: 101
limit:
description: Przewodnik krok po kroku, jak porównać pliki PDF i wykluczyć obszary adnotacji przy użyciu Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Przewodnik krok po kroku, jak porównać pliki PDF i wykluczyć obszary
    adnotacji przy użyciu Aspose.Pdf for .NET.
  headline: Porównanie PDF side‑by‑side z wykluczeniem adnotacji przy użyciu Aspose.Pdf
    for .NET
  type: TechArticle
- description: Przewodnik krok po kroku, jak porównać pliki PDF i wykluczyć obszary
    adnotacji przy użyciu Aspose.Pdf for .NET.
  name: Porównanie PDF side‑by‑side z wykluczeniem adnotacji przy użyciu Aspose.Pdf
    for .NET
  steps:
  - name: Zdefiniuj ścieżki plików dla głównego PDF, drugiego PDF oraz wyjściowego
      PDF z różnicami.
    text: Zdefiniuj ścieżki plików dla głównego PDF, drugiego PDF oraz wyjściowego
      PDF z różnicami.
  - name: Sprawdź, czy oba pliki PDF wejściowe istnieją, i w razie braku któregoś
      przerwij działanie z komunikatem o błędzie.
    text: Sprawdź, czy oba pliki PDF wejściowe istnieją, i w razie braku któregoś
      przerwij działanie z komunikatem o błędzie.
  - name: Otwórz oba pliki PDF jako obiekty Document (pdfA i pdfB) w bloku using,
      aby były automatycznie zwalniane.
    text: Otwórz oba pliki PDF jako obiekty Document (pdfA i pdfB) w bloku using,
      aby były automatycznie zwalniane.
  - name: Zbierz prostokąty ograniczające każdą adnotację w pdfA i zapisz je w zmiennej
      ignoredRectsA.
    text: Zbierz prostokąty ograniczające każdą adnotację w pdfA i zapisz je w zmiennej
      ignoredRectsA.
  - name: Zbierz prostokąty ograniczające każdą adnotację w pdfB i zapisz je w zmiennej
      ignoredRectsB.
    text: Zbierz prostokąty ograniczające każdą adnotację w pdfB i zapisz je w zmiennej
      ignoredRectsB.
  - name: Utwórz obiekt SideBySideComparisonOptions i przypisz wcześniej zebrane prostokąty
      adnotacji do właściwości ExcludeAreas1 i ExcludeAreas2, aby te obszary były
      pomijane podczas porównania.
    text: Utwórz obiekt SideBySideComparisonOptions i przypisz wcześniej zebrane prostokąty
      adnotacji do właściwości ExcludeAreas1 i ExcludeAreas2, aby te obszary były
      pomijane podczas porównania.
  - name: Uruchom porównanie PDF side‑by‑side, używając obu obiektów Document oraz
      skonfigurowanych opcji, zapisując wynik do zmiennej outputPdf.
    text: Uruchom porównanie PDF side‑by‑side, używając obu obiektów Document oraz
      skonfigurowanych opcji, zapisując wynik do zmiennej outputPdf.
  - name: Zwolnij obiekty Document i opuść blok using.
    text: Zwolnij obiekty Document i opuść blok using.
  - name: Wyświetl komunikat potwierdzający, że porównanie zostało zakończone oraz
      podaj lokalizację zapisanego PDF z różnicami.
    text: Wyświetl komunikat potwierdzający, że porównanie zostało zakończone oraz
      podaj lokalizację zapisanego PDF z różnicami.
  type: HowTo
- questions:
  - answer: Tak. Kod po prostu nie dodaje żadnych prostokątów do odpowiadającej listy
      `ignoredRects`, więc `ExcludeAreas1`/`ExcludeAreas2` otrzymują pustą tablicę
      i porównywarka przetwarza całą stronę.
    question: Co się stanie, jeśli strona PDF nie zawiera adnotacji – czy porównanie
      nadal zadziała?
  - answer: Ustaw `ExcludeAreas1` (lub `ExcludeAreas2`) na zebrane prostokąty i pozostaw
      drugą właściwość jako pustą tablicę; porównywarka będzie ignorować regiony tylko
      w określonym dokumencie.
    question: Czy mogę wykluczyć adnotacje tylko z jednego dokumentu, pozostawiając
      adnotacje drugiego w wyniku porównania?
  - answer: Nakładające się prostokąty są łączone wewnętrznie przez porównywarkę,
      więc granice adnotacji są bezpiecznie wykluczane bez podwójnego liczenia.
    question: Czy nakładające się prostokąty adnotacji powodują problemy z `ExcludeAreas`?
  - answer: Tak, ustaw `compareOpts.ExcludeTables = true;` – ten flag działa razem
      z `ExcludeAreas1`/`ExcludeAreas2`, aby również wykluczyć regiony tabel.
    question: Czy istnieje sposób, aby wykluczyć tabele oprócz adnotacji, używając
      tego samego obiektu opcji?
  - answer: Kod sprawdza `if (a != null && a.Rect != null)` przed dodaniem do listy,
      więc prostokąty o wartości null są po prostu pomijane i żaden wyjątek nie jest
      rzucany.
    question: Co się stanie, jeśli właściwość `Rect` adnotacji jest null – czy kod
      rzuci wyjątek?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Porównaj pliki PDF bez adnotacji
og_description: Uruchom porównanie PDF side‑by‑side, które pomija wszystkie oznaczenia adnotacji.
og_image_alt: Poradnik pokazujący porównanie PDF side‑by‑side, które wyklucza regiony adnotacji przy użyciu Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Porównanie PDF side‑by‑side z wykluczeniem adnotacji przy użyciu Aspose.Pdf
Ten tutorial pokazuje, jak porównać dwa pliki PDF przy użyciu Aspose.Pdf for .NET, ignorując wszelką zawartość adnotacji. Wyodrębnia prostokąty ograniczające wszystkie adnotacje z każdego dokumentu, przekazuje te regiony do SideBySideComparisonOptions, a następnie uruchamia porównanie side‑by‑side. Wynikiem jest PDF z różnicami, który podkreśla jedynie zmiany niebędące adnotacjami.

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

**Q: Co się stanie, jeśli strona PDF nie zawiera adnotacji – czy porównanie nadal zadziała?**  
A: Tak. Kod po prostu nie dodaje żadnych prostokątów do odpowiadającej listy `ignoredRects`, więc `ExcludeAreas1`/`ExcludeAreas2` otrzymują pustą tablicę i porównywarka przetwarza całą stronę.

**Q: Czy mogę wykluczyć adnotacje tylko z jednego dokumentu, pozostawiając adnotacje drugiego w wyniku porównania?**  
A: Ustaw `ExcludeAreas1` (lub `ExcludeAreas2`) na zebrane prostokąty i pozostaw drugą właściwość jako pustą tablicę; porównywarka będzie ignorować regiony tylko w określonym dokumencie.

**Q: Czy nakładające się prostokąty adnotacji powodują problemy z `ExcludeAreas`?**  
A: Nakładające się prostokąty są łączone wewnętrznie przez porównywarkę, więc granice adnotacji są bezpiecznie wykluczane bez podwójnego liczenia.

**Q: Czy istnieje sposób, aby wykluczyć tabele oprócz adnotacji, używając tego samego obiektu opcji?**  
A: Tak, ustaw `compareOpts.ExcludeTables = true;` – ten flag działa razem z `ExcludeAreas1`/`ExcludeAreas2`, aby również wykluczyć regiony tabel.

**Q: Co się stanie, jeśli właściwość `Rect` adnotacji jest null – czy kod rzuci wyjątek?**  
A: Kod sprawdza `if (a != null && a.Rect != null)` przed dodaniem do listy, więc prostokąty o wartości null są po prostu pomijane i żaden wyjątek nie jest rzucany.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}