---
category: general
date: 2026-10-07
description: Dowiedz się, jak dodać numerację Batesa do pliku PDF przy użyciu C#.
  Ten przewodnik krok po kroku obejmuje także numerację stron PDF oraz inne sztuczki
  związane z numeracją.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: pl
lastmod: 2026-10-07
og_description: Szybko dodaj numerację Batesa do pliku PDF. Postępuj zgodnie z tym
  samouczkiem, aby opanować numerację stron PDF, numerować strony PDF i zautomatyzować
  śledzenie dokumentów.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Dodaj numerację Bates do plików PDF w C# – kompletny przewodnik Aspose
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
title: Jak dodać numerację Batesa do pliku PDF przy użyciu Aspose.Pdf
url: /pl/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać numerację Bates do pliku PDF przy użyciu Aspose.Pdf

Jeśli potrzebujesz **dodać numerację bates** do pliku PDF, ten przewodnik pokaże Ci dokładnie, jak to zrobić w C#. Niezależnie od tego, czy przygotowujesz pakiety prawne, zarządzasz aktami spraw, czy po prostu chcesz niezawodną **numerację stron pdf**, poniższe kroki dostarczą Ci kompletne, gotowe do uruchomienia rozwiązanie.

W tym tutorialu nauczysz się:

* Załadować istniejący plik PDF.
* Skonfigurować opcje numeracji Bates, takie jak prefiks, numer początkowy, wypełnienie cyfr, separator i sufiks.
* Zastosować numerację na każdej stronie.
* Zapisać zaktualizowany dokument.

Do wykonania nie są wymagane żadne zewnętrzne narzędzia poza biblioteką Aspose.Pdf for .NET, a kod działa z .NET 6+ oraz .NET Framework 4.7.2+.  

---

## Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet package `Aspose.Pdf`) | Udostępnia klasy `Document` i `BatesNumberingOptions` używane w kodzie. |
| **.NET SDK** (6.0 or later recommended) | Umożliwia kompilację i uruchomienie aplikacji konsolowej w C#. |
| **A source PDF** you want to number | W tutorialu używany jest `source.pdf` jako przykład; zamień ścieżkę na własny plik. |
| **Write permission** to the output folder | Wywołanie `Save` musi zapisać nowy plik. |

Możesz zainstalować bibliotekę przy użyciu następującego polecenia CLI:

```bash
dotnet add package Aspose.Pdf
```

---

## Krok 1: Utwórz nowy projekt konsolowy

Otwórz terminal i uruchom:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Tworzy to minimalny projekt C#, który wypełnimy kodem potrzebnym do **dodania numeracji bates**.

---

## Krok 2: Dodaj wymagane dyrektywy `using`

Otwórz `Program.cs` i dodaj przestrzenie nazw na początku pliku:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` daje dostęp do klasy `Document` służącej do ładowania i zapisywania plików PDF.  
* `Aspose.Pdf.Text` zawiera `BatesNumberingOptions`, obiekt definiujący sposób wyświetlania numerów.

---

## Krok 3: Załaduj źródłowy PDF

Pierwsza wykonywalna linia ładuje PDF, który chcesz ponumerować. Zamień `"YOUR_DIRECTORY/source.pdf"` na rzeczywistą ścieżkę do swojego pliku.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Jeśli plik nie zostanie znaleziony, Aspose zgłasza `FileNotFoundException`. Aby tego uniknąć, możesz najpierw zweryfikować ścieżkę:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Krok 4: Zdefiniuj opcje numeracji Bates

`BatesNumberingOptions` pozwala kontrolować każdy wizualny element numeracji. Poniższy przykład przedstawia typową konfigurację dla akt prawnych:

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

**Dlaczego każda właściwość ma znaczenie**

| Właściwość | Cel |
|----------|---------|
| `Prefix` | Umożliwia grupowanie dokumentów według projektu, klienta lub sprawy. |
| `StartNumber` | Ustawia początkowy licznik; przydatne, gdy masz już istniejące ponumerowane pliki. |
| `Digits` | Zapewnia jednolitą szerokość, ułatwiając sortowanie. |
| `Separator` | Poprawia czytelność, szczególnie przy łączeniu prefiksu i sufiksu. |
| `Suffix` | Pozwala dodać rok, wersję lub dowolny identyfikator końcowy. |

Możesz także kontrolować położenie (góra, dół, lewo, prawo) oraz styl czcionki, odwołując się do `batesOptions.Position` i `batesOptions.Font`. Dla większości scenariuszy domyślne ustawienia (dolny‑prawy, 12‑pt Times New Roman) działają dobrze.

---

## Krok 5: Zastosuj numerację na każdej stronie

Wywołanie `pdf.BatesNumbering.Add` wstawia numery na każdej stronie w kolejności ich występowania.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Jeśli potrzebujesz **ponumerować strony pdf** tylko w wybranym podzbiorze (np. pominąć stronę tytułową), możesz zamiast tego przekazać `PageCollection`:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Krok 6: Zapisz zaktualizowany PDF

Na koniec zapisz zmodyfikowany dokument na dysk. Nazwa pliku zazwyczaj odzwierciedla, że PDF zawiera teraz numery Bates.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Jeśli folder wyjściowy nie istnieje, Aspose utworzy go automatycznie. Jednak powinieneś upewnić się, że masz uprawnienia do zapisu, aby uniknąć `UnauthorizedAccessException`.

---

## Pełny, gotowy do uruchomienia przykład

Łącząc wszystkie elementy, oto kompletny program, który możesz skopiować, wkleić i uruchomić:

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

**Oczekiwany wynik** (konsola):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Otwórz `bates_numbered.pdf` i zobaczysz, że każda strona jest oznaczona np. `CASE-001000-2025`, `CASE-001001-2025` itd., umieszczona w domyślnym prawym dolnym rogu.

---

## Najczęściej zadawane pytania (FAQ)

### 1. Czy mogę zmienić położenie numerów?
Tak. Ustaw `batesOptions.Position = new Position(10, 10, 10, 10);`, gdzie cztery wartości oznaczają marginesy od góry, dołu, lewej i prawej krawędzi. Aspose udostępnia także predefiniowane wyliczenia, takie jak `BatesNumberingPosition.BottomCenter`.

### 2. Co jeśli mój PDF już zawiera numery stron?
Dodanie numeracji Bates **nałoży się** na istniejące numery. Aby uniknąć wizualnego bałaganu, ukryj oryginalne numery (jeśli są częścią warstwy tekstowej) lub dostosuj rozmiar czcionki i położenie w `batesOptions`.

### 3. Czy to działa z zaszyfrowanymi PDF‑ami?
Aspose może otworzyć PDF‑y zabezpieczone hasłem, jeśli podasz hasło:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

### 4. Jak **ponumerować strony pdf** prostym licznikem sekwencyjnym (bez prefiksu/sufiksu)?
Wystarczy ustawić `Prefix = string.Empty` oraz `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Czy mogę użyć tego podejścia w ASP.NET Core do serwowania PDF‑ów w locie?
Oczywiście. Załaduj dokument, zastosuj numerację, a następnie zapisz strumień w odpowiedzi HTTP:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Przypadki brzegowe i wskazówki najlepszych praktyk

| Sytuacja | Zalecane podejście |
|-----------|----------------------|
| **Large PDFs (hundreds of pages)** | Wywołaj `pdf.BatesNumbering.Add` **po** wykonaniu wszelkich transformacji na poziomie stron, aby uniknąć wielokrotnego przetwarzania tych samych stron. |
| **Custom fonts** | Ustaw `batesOptions.Font = FontRepository.FindFont("Arial")` i dostosuj `batesOptions.FontSize`, aby uzyskać lepszą czytelność w zeskanowanych dokumentach. |
| **Performance‑critical batch jobs** | Używaj jednej instancji `Document` przy przetwarzaniu wielu plików w pętli; zwalniaj ją po każdej iteracji, aby zwolnić pamięć. |
| **International characters** | Używaj czcionek zgodnych z Unicode (np. `Times New Roman Unicode`), aby zapewnić prawidłowe wyświetlanie prefiksu lub sufiksu. |
| **Version compatibility** | Kod działa z Aspose.Pdf 23.10 i nowszymi. Jeśli celujesz w starszą wersję, sprawdź dokumentację API pod kątem zmian nazw właściwości. |

---

## Podsumowanie

Teraz wiesz, jak **dodać numerację bates** do pliku PDF przy użyciu Aspose.Pdf for .NET. Tutorial obejmował ładowanie PDF‑a, konfigurowanie `BatesNumberingOptions`, zastosowanie numerów na każdej stronie oraz zapis wyniku. Dzięki tym elementom możesz także wdrożyć ogólną **numerację stron pdf**, **ponumerować strony pdf** własnym formatem i zintegrować proces z większymi pipeline‑ami automatyzacji.

**Kolejne kroki**

* Zbadaj dalej API **bates numbering pdf**, aby dostosować czcionkę, kolor i położenie.  
* Połącz tę technikę z **digital signatures**, aby tworzyć niezmienialne prawne pakiety.  
* Zapoznaj się z możliwościami **PDF merging** Aspose, jeśli musisz połączyć wiele aktów przed numeracją.

Śmiało eksperymentuj z różnymi prefiksami, sufiksami i długościami cyfr, aby dopasować je do standardów archiwizacji w Twojej organizacji. Powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz krok po kroku wyjaśnienia, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}