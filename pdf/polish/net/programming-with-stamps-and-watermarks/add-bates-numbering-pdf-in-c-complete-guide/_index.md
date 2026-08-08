---
category: general
date: 2026-05-27
description: Dodaj numerację Bates do PDF przy użyciu Aspose.Pdf w C#. Dowiedz się,
  jak szybko dodać numerację Bates, dostosować format i zautomatyzować oznaczanie
  dokumentów prawnych.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: pl
og_description: Dodaj numerację Bates do pliku PDF przy użyciu Aspose.Pdf w C#. Ten
  przewodnik pokazuje, jak dodać numerację Bates, skonfigurować prefiksy i zapisać
  wynik.
og_title: Dodaj numerację Bates do PDF w C# – Poradnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Dodaj numerację Bates w PDF w C# – Kompletny przewodnik
url: /pl/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodawanie numeracji Bates w PDF w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak dodać numerację Bates** do pliku PDF bez spędzania godzin na ręcznych narzędziach? Nie jesteś sam — zespoły prawne, audytorzy i specjaliści ds. e‑discovery potrzebują niezawodnego sposobu na **dodawanie numeracji Bates PDF** programowo.  

W tym samouczku przeprowadzimy Cię przez zwięzłe, kompleksowe rozwiązanie z użyciem Aspose.Pdf dla .NET, dzięki czemu w kilka linijek kodu C# możesz nanieść numerację Bates na dowolny dokument.

## Co się nauczysz

- Jak otworzyć istniejący PDF przy pomocy Aspose.Pdf  
- Jak utworzyć artefakt numeracji Bates i dopasować jego format  
- Jak dołączyć artefakt do każdej strony (lub tylko do pierwszej)  
- Jak zapisać zaktualizowany plik i zweryfikować wynik  

Nie wymagana jest wcześniejsza znajomość Aspose — wystarczy podstawowa wiedza o C# i .NET. Po zakończeniu będziesz mieć gotowy fragment kodu, który możesz skopiować i wkleić do dowolnego projektu.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7+)  
- Pakiet NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)  
- Plik PDF, który chcesz otagować (umieść go w folderze, do którego masz dostęp)

> **Wskazówka:** Jeśli nie masz jeszcze licencji, Aspose oferuje darmowy tymczasowy klucz, który usuwa znaki wodne wersji ewaluacyjnej.

## Krok 1 – Otwórz źródłowy dokument PDF  

Najpierw potrzebujemy obiektu `Document`, który reprezentuje plik na dysku. To jak załadowanie pustego płótna, na które później naniesiemy numery Bates.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Dlaczego to ważne:** Otwieranie dokumentu w bloku `using` zapewnia szybkie zwolnienie wszystkich niezarządzanych zasobów, co jest szczególnie istotne przy dużych plikach PDF.

## Krok 2 – Utwórz artefakt numeracji Bates  

`BatesNumberingArtifact` to sposób Aspose na opisanie wyglądu numerów. Możesz ustawić prefiks, numer początkowy, przyrost oraz własny ciąg formatowania.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Dlaczego możesz chcieć zmienić te wartości:**  
- **Prefix** przydaje się do identyfikatorów spraw („CASE‑”, „DOC‑”).  
- **StartNumber** pozwala kontynuować poprzednią serię.  
- **Increment** można ustawić na 2, jeśli potrzebujesz numeracji nieparzyste/parzyste.  
- **Format** obsługuje dowolny .NET‑owy format złożony; `{0:D5}` zapewnia pięć cyfr z wiodącymi zerami.

## Krok 3 – Dołącz artefakt do wybranych stron  

Artefakt możesz dodać do jednej strony, zakresu lub całego dokumentu. W typowych procesach prawniczych najczęściej dołączamy go do *każdej* strony, ale poniższy przykład pokazuje minimalny przypadek — dodanie go do pierwszej strony.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Jeśli potrzebujesz objąć wszystkie strony, przeiteruj je:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Dlaczego ten krok jest kluczowy:** Artefakty są renderowane *po* zawartości strony, więc numery pojawiają się na wierzchu istniejącego tekstu, nie zmieniając pierwotnego układu.

## Krok 4 – Zapisz zmodyfikowany PDF  

Na koniec zapisz zmiany na dysku. Możesz nadpisać oryginał lub utworzyć nowy plik — w tym przykładzie generujemy nową kopię o nazwie `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Kiedy otworzysz `bates.pdf`, zobaczysz „ABC01000” (lub dowolny wybrany format) naniesiony w domyślnej lokalizacji — zazwyczaj w prawym dolnym rogu.

## Pełny działający przykład  

Łącząc wszystkie elementy, oto kompletny program, który możesz skompilować i uruchomić:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Oczekiwany wynik

Po uruchomieniu programu konsola wypisze:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Otwierając `bates.pdf` zobaczysz prefiks „ABC” po którym następuje pięciocyfrowa sekwencja z wiodącymi zerami na każdej stronie — dokładnie to, co kod miał wykonać.

## Częste pytania i przypadki brzegowe

### Czy mogę umieścić numer Bates w innym miejscu?

Tak. Użyj właściwości `Location` artefaktu `BatesNumberingArtifact` (np. `Location = new Position(10, 10)`) aby ustawić numer w dowolnych współrzędnych X/Y. Możesz także ustawić `HorizontalAlignment` i `VerticalAlignment` dla większej kontroli.

### Co jeśli mój PDF ma tysiące stron?

Aspose.Pdf strumieniuje strony efektywnie, ale warto przetwarzać je partiami, jeśli napotkasz limity pamięci. Klasa `Document` obsługuje także `PdfConverter` do zapisu przyrostowego.

### Jak zmienić czcionkę lub kolor?

Umieść artefakt w obiekcie `TextState`:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Czy potrzebuję licencji do użytku produkcyjnego?

Wersja licencjonowana usuwa znaki wodne wersji ewaluacyjnej i odblokowuje pełną wydajność. Darmowa wersja próbna sprawdza się w testach i proof‑of‑concept.

## Weryfikacja – szybka kontrola wizualna  

Jeśli wolisz automatyczną weryfikację, Aspose może wyodrębnić tekst ze strony i potwierdzić obecność prefiksu:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Uruchomienie tego po kroku zapisu wypisze `Bates number verified.` jeśli wszystko przebiegło pomyślnie.

## Podsumowanie  

Teraz wiesz **jak dodać numerację Bates PDF** przy użyciu Aspose.Pdf w C#. Od otwarcia dokumentu, przez konfigurację artefaktu, jego dołączenie do stron, po zapis wyniku — proces jest prosty i w pełni skryptowalny.  

Co dalej? Wypróbuj:

- Różne wartości `Prefix` dla wielu partii spraw  
- Niestandardowe `Location` i `TextState` dla brandingu  
- Dodawanie prefiksów specyficznych dla stron (np. „VOL‑1‑”, „VOL‑2‑”) poprzez modyfikację `StartNumber` w pętli  

Te modyfikacje pozwolą dostosować rozwiązanie do niemal każdego procesu prawnego lub archiwizacyjnego.  

Masz więcej pytań o **jak dodać numerację Bates** do wielojęzycznych PDF‑ów lub zaszyfrowanych plików? Zostaw komentarz poniżej i powodzenia w kodowaniu!

## Powiązane samouczki

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Different Headers in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}