---
category: general
date: 2026-01-15
description: Dodaj numery Bates do swojego PDF szybko za pomocą Aspose.Pdf. Dowiedz
  się, jak dodać stopkę do PDF, dodać numery stron w PDF oraz dodać własne numerowanie
  stron.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: pl
og_description: Szybko dodaj numery Bates do swojego PDF za pomocą Aspose.Pdf. Dowiedz
  się, jak dodać stopkę do PDF, dodać numery stron do PDF oraz dodać własne numerowanie
  stron.
og_title: Dodaj numery Bates do PDF – numerowanie Bates w PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Dodaj numery Bates do PDF – numerowanie Bates PDF
url: /pl/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj numery Batesa do PDF – Kompletny przewodnik

Kiedykolwiek potrzebowałeś **dodać numery Batesa** do PDF, ale nie wiedziałeś od czego zacząć? Nie jesteś sam — zespoły prawne, audytorzy i każdy, kto ma do czynienia z ogromnymi zestawami dokumentów, napotykają ten problem codziennie. Dobra wiadomość? Dzięki Aspose.Pdf dla .NET możesz posypać te numery na każdej stronie w zaledwie kilku linijkach.

W tym tutorialu przeprowadzimy Cię przez cały proces: od pobrania biblioteki Aspose.Pdf, załadowania pliku źródłowego, skonfigurowania *BatesNumberingArtifact*, dołączenia go jako stopki, aż po zapisanie wyniku. Po zakończeniu będziesz także wiedział, jak **dodać stopkę do pdf**, **dodać numery stron pdf**, a nawet **dodać niestandardowe numerowanie stron** dla trudnych przypadków brzegowych.

## Czego będziesz potrzebował

- .NET 6+ (lub .NET4.8, jeśli nadal używasz klasycznego stosu)  
- Odwołanie do pakietu NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- Plik PDF, który chcesz otoczyć (nazwijmy go `source.pdf`)  

To wszystko — żadnych dodatkowych narzędzi, żadnych ciężkich edytorów PDF. Zanurzmy się.

![przykład dodawania numerów Batesa](https://example.com/images/add-bates-numbers.png "przykład dodawania numerów Batesa")

## Krok 1: Dodaj numery Batesa – Załaduj dokument PDF

Najpierw potrzebujemy obiektu `Document`, który reprezentuje PDF, który zamierzamy zmodyfikować. Pomyśl o tym jak o otwarciu dokumentu Word przed rozpoczęciem pisania.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Dlaczego to ważne:** Załadowanie pliku daje dostęp do jego kolekcji `Pages`, w której później dołączymy artefakt numeracji Batesa. Jeśli plik nie zostanie znaleziony, Aspose zgłosi wyraźny `FileNotFoundException`, więc sprawdź dokładnie ścieżkę.

## Krok 2: Skonfiguruj ustawienia numeracji Batesa w PDF

Teraz definiujemy *jak* mają wyglądać numery. `BatesNumberingArtifact` pozwala ustawić prefiks, numer początkowy, wypełnienie cyfr, sufiks oraz położenie. To jest sedno **numeracji Batesa w PDF**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Wskazówka:** Jeśli potrzebujesz, aby numery pojawiały się w nagłówku, zamień `BottomCenter` na `TopCenter`. Enum położenia obsługuje także `BottomLeft`, `BottomRight` i inne, dając elastyczność dla różnych stylów **dodawania stopki do pdf**.

## Krok 3: Dodaj numery stron pdf – Dołącz artefakt do każdej strony

Gdy artefakt jest gotowy, iterujemy po każdej stronie i dodajemy go do kolekcji `Artifacts`. To jest krok, który faktycznie **dodaje numery stron pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Co się dzieje w tle?** Kolekcja `Artifacts` jest renderowana po głównej treści strony, zapewniając, że numer Batesa znajduje się nad istniejącym tekstem, ale pod adnotacjami. Jeśli potrzebujesz, aby numer był za treścią (rzadko), użyj `page.Artifacts.Insert(0, batesArtifact)`.

## Krok 4: Dodaj niestandardowe numerowanie stron – Zapisz zaktualizowany PDF

Na koniec zapisujemy zmodyfikowany dokument na dysk. Plik wyjściowy będzie zawierał numery Batesa jako stałą część każdej strony.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Wskazówka weryfikacyjna:** Otwórz `bates_out.pdf` w dowolnym przeglądarce. Powinieneś zobaczyć coś w stylu `CASE-01000-A` wyśrodkowane na dole każdej strony. Jeśli numery są nieobecne, sprawdź ponownie, czy właściwość `Placement` odpowiada zamierzonemu miejscu.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia program:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Oczekiwany wynik

- **Plik:** `bates_out.pdf` w tym samym folderze co `source.pdf`
- **Wygląd:** Tekst wyśrodkowany na dole `CASE-01000-A`, `CASE-01001-A`, … dla każdej kolejnej strony
- **Zachowanie:** Numery są trwale osadzone; przetrwają drukowanie, spłaszczanie i dalszą edycję.

## Częste warianty i przypadki brzegowe

| Sytuacja | Jak dostosować |
|-----------|----------------|
| **Inna liczba początkowa** | Zmien `StartNumber` na dowolną liczbę całkowitą (np. `StartNumber = 500`). |
| **Literowe sufiksy per tom** | Użyj pętli, aby modyfikować `Suffix` dla każdej strony, lub utwórz wiele artefaktów z różnymi sufiksami. |
| **Numeracja wyrównana do prawej** | Ustaw `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Duże dokumenty (10 000+ stron)** | Rozważ przetwarzanie stron w partiach lub zwiększenie `NumberDigits`, aby uniknąć przepełnienia. |
| **Potrzeba ukrycia numerów na niektórych stronach** | Pomiń te strony w pętli `foreach` (np. `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Uwaga:** Użycie `Prefix` lub `Suffix` zawierającego niedozwolone znaki w nazwach plików (np. `*` lub `?`). Aspose nadal je osadzi, ale mogą powodować problemy przy późniejszym wyodrębnianiu tekstu.

## Wskazówki profesjonalne dla produkcji

- **Cache'uj artefakt**, jeśli przetwarzasz wiele PDF-ów kolejno; stworzenie go raz oszczędza kilka milisekund na plik.  
- **Bezpieczeństwo wątków:** Instancja `BatesNumberingArtifact` nie jest bezpieczna wątkowo, więc każdemu wątkowi przydziel własną kopię.  
- **Wydajność:** Przy masowych partiach wyłącz kompresję PDF (`pdfDocument.Compress = false`) przed zapisem, a następnie w razie potrzeby włącz ponownie.  
- **Testowanie:** Zawsze wykonaj szybki wizualny przegląd pierwszego wygenerowanego PDF, aby upewnić się, że położenie spełnia standardy Twojego zespołu prawnego.

## Podsumowanie

Masz teraz solidny, kompleksowy przepis, jak **dodać numery Batesa** do dowolnego PDF przy użyciu Aspose.Pdf, wraz z opcjami **dodawania stopki do pdf**, **dodawania numerów stron pdf** i **dodawania niestandardowego numerowania stron**. Kod jest w pełni samodzielny, działa z .NET 6 i nowszymi oraz może być wstawiony do dowolnego istniejącego potoku automatyzacji.

Co dalej? Spróbuj zamienić położenie `BottomCenter` na styl nagłówka, eksperymentuj z dynamicznymi prefiksami (np. identyfikatory spraw z bazy danych) lub połącz to z funkcjami ekstrakcji tekstu Aspose, aby wygenerować przeszukiwalny indeks Twoich nowo ponumerowanych dokumentów. Nie ma granic, a Ty właśnie zyskałeś potężne narzędzie do kontroli dokumentów.

Szczęśliwego kodowania i niech Twoje PDF-y zawsze będą idealnie ponumerowane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}