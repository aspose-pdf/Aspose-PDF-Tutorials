---
category: general
date: 2026-02-25
description: samouczek numeracji Bates – dowiedz się, jak dodać numery stron do PDF
  i zastosować niestandardową numerację Bates przy użyciu Aspose.Pdf w C#. Przewodnik
  krok po kroku z pełnym kodem.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: pl
og_description: Poradnik numeracji Bates pokazuje, jak dodać numery stron do PDF oraz
  niestandardową numerację Bates w C#. Pełny kod, wyjaśnienia i wskazówki.
og_title: samouczek numeracji Batesa – Dodaj numery Batesa do plików PDF w C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Samouczek numeracji Batesa: Dodaj numery Batesa do plików PDF w C#'
url: /pl/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# samouczek numeracji Bates – Dodawanie numerów Bates do plików PDF w C#

Zastanawiałeś się kiedyś, jak dodać numerację stron do PDF‑a, jednocześnie wstawiając prawnie stylizowany numer Bates? Nie jesteś sam. W tym **bates numbering tutorial** przejdziemy krok po kroku przez wszystko, co musisz wiedzieć, aby oznaczyć każdą stronę PDF własnym prefiksem, wiodącymi zerami i precyzyjnym położeniem — przy użyciu Aspose.Pdf dla .NET.

Dobra wiadomość? To całkiem proste, gdy zrozumiesz podstawowe koncepcje. Po przeczytaniu tego przewodnika będziesz mieć działający program, który przyjmuje *input.pdf* i generuje *bates_out.pdf* z elegancką etykietą w stylu „ABC‑01000” na każdej stronie. Zanurzmy się.

## Co będzie potrzebne

- **Aspose.Pdf for .NET** (wersja 23.10 lub nowsza). Biblioteka jest komercyjna, ale darmowa wersja próbna w zupełności wystarczy do nauki.
- .NET 6+ SDK (dowolna aktualna wersja).
- Podstawowe środowisko programistyczne C# — Visual Studio, VS Code lub Rider.
- Plik PDF do eksperymentów (dowolny dokument wielostronicowy pokaże efekt).

Nie są wymagane żadne dodatkowe pakiety NuGet poza Aspose.Pdf, a kod działa na Windows, Linux i macOS bez modyfikacji.

## Krok 1: Załaduj źródłowy dokument PDF (bates numbering tutorial – initialization)

Najpierw tworzymy obiekt `Document`, który reprezentuje PDF, który chcemy zmodyfikować. Pomyśl o tym jak o załadowaniu pustego płótna, na którym możesz rysować.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Dlaczego to ważne:** Bez załadowania pliku nie ma czego anotować. Sprawdzenie poprawności zapobiega cichej awarii później, gdy próbujesz dodać elementy do nieistniejącej kolekcji stron.

## Krok 2: Zdefiniuj artefakt numeracji Bates (how to add bates)

Obiekt *BatesNumberingArtifact* informuje Aspose, gdzie i jak narysować identyfikator. Możesz kontrolować prefiks, numer początkowy, wypełnienie zerami, rozmiar czcionki oraz dokładne współrzędne X/Y.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Dlaczego to ważne:** Właściwość `LeadingZeros` zapewnia, że każda etykieta ma tę samą długość, co jest kluczowe w dokumentach prawnych, gdzie wyrównanie ma znaczenie. Dostosuj `X` i `Y`, aby przenieść pieczątkę w prawy‑górny róg, lewy‑dolny lub tam, gdzie wymaga tego Twój proces.

## Krok 3: Dołącz artefakt do każdej strony (add page numbers pdf)

Teraz iterujemy po każdej stronie i dołączamy ten sam artefakt. To właśnie spełnia wymóg *add page numbers pdf* — każda strona otrzymuje własną sekwencyjną etykietę automatycznie.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Dlaczego to ważne:** Dodając artefakt do kolekcji `Artifacts` zamiast ręcznie rysować tekst, pozwalamy Aspose zarządzać logiką numeracji, wiodącymi zerami i renderowaniem. To zmniejsza liczbę błędów i utrzymuje kod zwięzły.

## Krok 4: Zapisz zmodyfikowany PDF (add bates numbering)

Na koniec zapisujemy zmiany do nowego pliku. Dobrą praktyką jest zapisywanie pod inną nazwą, aby zachować oryginał nietknięty.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Dlaczego to ważne:** Metoda `Save` zapisuje cały PDF, wbudowując artefakty jako część strumienia zawartości strony. Powstały plik można otworzyć w dowolnym przeglądarce PDF i wyświetli on numery Bates dokładnie tak, jak określono.

## Pełny działający przykład (Wszystkie kroki razem)

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj‑wklej go do projektu aplikacji konsolowej, zamień ścieżki zastępcze i naciśnij **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Oczekiwany rezultat

Otwórz *bates_out.pdf* w Adobe Reader, Foxit lub dowolnym innym przeglądarce. Powinieneś zobaczyć etykietę taką jak **ABC‑01000** na pierwszej stronie, **ABC‑01001** na drugiej i tak dalej, umieszczoną 50 pt od lewej krawędzi i 30 pt od dolnej. Liczby są wyrównane do prawej dzięki wiodącym zerom, co nadaje dokumentowi czysty, profesjonalny wygląd.

## Typowe warianty i przypadki brzegowe

| Scenariusz | Jak dostosować |
|----------|---------------|
| **Inny prefiks** | Zmien `Prefix = "XYZ"` w definicji artefaktu. |
| **Rozpocznij od własnego numeru** | Ustaw `Start = 5000` (lub dowolną liczbę całkowitą). |
| **Umieść numer w prawym‑górnym rogu** | Użyj `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Zwiększ rozmiar czcionki dla większych dokumentów** | Zmodyfikuj `FontSize = 12` (lub dowolny rozmiar). |
| **Dodaj tło w postaci prostokąta** | Utwórz `RectangleArtifact` i dodaj go przed `BatesNumberingArtifact`. |
| **Pomiń wybrane strony** | Wewnątrz pętli `foreach` dodaj `if (page.Number % 2 == 0) continue;` aby pominąć strony parzyste. |

**Pro tip:** Zawsze najpierw testuj na krótkim PDF‑ie. Szybciej zweryfikujesz położenie, zanim uruchomisz skrypt na pliku o 200 stronach.

## Najczęściej zadawane pytania

- **Czy to działa z zaszyfrowanymi PDF‑ami?**  
  Aspose.Pdf może otworzyć pliki chronione hasłem, jeśli podasz hasło w konstruktorze `Document(string, string)`. Artefakt Bates zostanie zastosowany po odszyfrowaniu.

- **Czy mogę dodać jednocześnie numery Bates i zwykłe numery stron?**  
  Tak. Dodaj `PageNumberArtifact` obok `BatesNumberingArtifact`. Każdy artefakt utrzymuje własny licznik.

- **Co jeśli mój PDF ma różne rozmiary stron?**  
  Wartości `Position` są punktami absolutnymi. Dla dokumentów o mieszanych rozmiarach oblicz pozycję dla każdej strony wewnątrz pętli, używając `page.PageInfo.Width` i `page.PageInfo.Height`.

## Kolejne kroki i tematy pokrewne

Teraz, gdy opanowałeś **bates numbering tutorial**, możesz zgłębić:

- **Dodawanie znaków wodnych** – podobne podejście z artefaktem `TextArtifact`.
- **Scalanie wielu PDF‑ów** – użyj `Document.AppendDocument`.
- **Ekstrahowanie tekstu do indeksowania** – klasa `TextAbsorber`.
- **Automatyzacja przetwarzania wsadowego** – pętla po folderze PDF‑ów i zastosowanie tego samego artefaktu.

Wszystkie te tematy opierają się na tych samych koncepcjach, które właśnie poznałeś, więc jesteś gotowy, by rozbudować swój zestaw narzędzi do automatyzacji PDF.

---

*Miłego kodowania! Jeśli napotkasz problemy lub masz pomysły na dalsze dostosowania, zostaw komentarz poniżej. Świat manipulacji PDF jest ogromny, ale z solidnym **bates numbering tutorial** w ręku jesteś już o krok przed innymi.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}