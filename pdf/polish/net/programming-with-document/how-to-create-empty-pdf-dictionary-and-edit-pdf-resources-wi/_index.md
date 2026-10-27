---
category: general
date: 2026-10-26
description: Naucz się tworzyć pusty słownik PDF i edytować zasoby PDF przy użyciu
  Aspose.PDF dla C#. Przewodnik krok po kroku z pełnym przykładem kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: pl
lastmod: 2026-10-26
og_description: Utwórz pusty słownik PDF i edytuj zasoby PDF przy użyciu Aspose.PDF
  dla C#. Przejdź przez ten kompletny samouczek, aby modyfikować stany graficzne w
  plikach PDF.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Utwórz pusty słownik PDF i edytuj zasoby PDF w C# – przewodnik Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Jak utworzyć pusty słownik PDF i edytować zasoby PDF przy użyciu Aspose.PDF
  w C#
url: /pl/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć pusty słownik PDF i edytować zasoby PDF przy użyciu Aspose.PDF w C#

Jeśli potrzebujesz **utworzyć pusty słownik PDF** i następnie **edytować zasoby PDF** w aplikacji C#, ten przewodnik pokaże Ci dokładne kroki. Zobaczysz kompletny, działający przykład, który dodaje niestandardowy stan graficzny do pierwszej strony istniejącego pliku PDF.

Praca z niskopoziomowymi obiektami PDF może wydawać się przytłaczająca, ale Aspose.PDF udostępnia przejrzyste API do manipulacji słownikami. Po zakończeniu tego samouczka zrozumiesz, dlaczego każda operacja ma znaczenie i jak dostosować kod do innych typów zasobów.

## Wymagania wstępne

* .NET 6.0 (lub nowszy) zainstalowany.
* Licencjonowana kopia **Aspose.PDF for .NET** – darmowa wersja próbna działa do testów.
* IDE, takie jak Visual Studio 2022.
* Plik PDF o nazwie `input.pdf` umieszczony w folderze, do którego możesz odwoływać się w kodzie.

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Pdf`.

## Krok 1: Konfiguracja projektu i importowanie przestrzeni nazw

Utwórz nowy projekt konsolowy i dodaj pakiet Aspose.PDF:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

W pliku `Program.cs` zaimportuj przestrzenie nazw, które będziesz używać:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Te importy udostępniają klasy `Document`, `DictionaryEditor` oraz COS (Canonical Object Structure), które pozwalają **utworzyć pusty słownik PDF** oraz modyfikować istniejące słowniki zasobów.

## Krok 2: Zdefiniuj folder zawierający pliki PDF

Określ katalog, w którym znajduje się `input.pdf`. Użycie ścieżki bezwzględnej eliminuje niejasności, gdy program uruchamiany jest z innego katalogu roboczego.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

Zastąp `C:\PdfDemo\` ścieżką na swoim komputerze. Przechowywanie ścieżki w zmiennej ułatwia jej ponowne użycie zarówno dla plików wejściowych, jak i wyjściowych.

## Krok 3: Otwórz źródłowy dokument PDF

Wczytaj PDF, który chcesz zmodyfikować, wewnątrz bloku `using`, aby uchwyt pliku został zwolniony automatycznie.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

Otwarcie dokumentu daje dostęp do jego kolekcji stron, słowników zasobów oraz niskopoziomowych obiektów COS.

## Krok 4: Uzyskaj dostęp do pierwszej strony i jej słownika zasobów

Pierwsza strona jest indeksowana jako `1` (strony PDF są numerowane od 1). Pobierz słownik `Resources` tej strony i opakuj go w `DictionaryEditor`, aby umożliwić bezpieczną edycję.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` abstrahuje podstawową strukturę COS, umożliwiając odczyt lub tworzenie wpisów bez uszkadzania pliku PDF.

## Krok 5: **Utworzyć pusty słownik PDF** dla nowego stanu graficznego

Stan graficzny kontroluje przezroczystość, tryb mieszania i inne parametry rysowania. Aby dodać niestandardowy stan, najpierw potrzebujesz pustego słownika, a następnie wypełnić go wymaganymi wpisami.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

Wywołanie `CreateEmptyDictionary` jest rdzeniem **tworzenia pustego słownika PDF**. Zwraca ono słownik COS należący do tego samego dokumentu, zapewniając integralność odwołań krzyżowych.

### Wypełnij wpisy stanu graficznego

Dodaj standardowe klucze:

* `CA` – stała alfa przy rysowaniu (zakres 0 – 1).
* `ca` – stała alfa przy nie‑rysowaniu.
* `BM` – nazwa trybu mieszania.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Każdy wpis jest dodawany do właśnie utworzonego pustego słownika. Oddzielenie definicji od pętli wstawiania utrzymuje kod czytelnym i ułatwia późniejsze rozszerzenie o dodatkowe klucze.

### Zarejestruj nowy stan graficzny w słowniku zasobów

Nadaj stanowi nazwę (`GS0`) i dodaj go do słownika `ExtGState`, który znajduje się w zasobach strony.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Teraz słownik zasobów strony zawiera odwołanie do niestandardowego stanu graficznego, który możesz później zastosować w strumieniach zawartości.

## Krok 6: Zapisz zaktualizowany PDF

Na koniec zapisz zmodyfikowany dokument do nowego pliku. Zachowanie oryginału nietkniętego pomaga zweryfikować zmiany.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

Gdy otworzysz `output.pdf` w przeglądarce obsługującej inspekcję stanów graficznych (np. Adobe Acrobat Pro), zobaczysz, że słownik `ExtGState` zawiera wpis o nazwie `GS0` z wartościami, które zdefiniowałeś.

## Pełny kod źródłowy

Połączenie wszystkich elementów daje samodzielny program:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje:

```
PDF updated successfully.
```

i tworzy `output.pdf` w tym samym folderze. Otwarcie pliku ujawnia nowy wpis w **Resources → ExtGState → GS0** z ustawionymi przez Ciebie parametrami.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Jak dostosować kod |
|-----------|-----------------------|
| **Wiele stron** potrzebuje tego samego stanu graficznego | Utwórz słownik raz, a następnie dodaj to samo odwołanie `GS0` do słownika `ExtGState` każdej strony. |
| **Inny tryb mieszania** (np. `Multiply`) | Zmień wartość `CosPdfName("Normal")` na `CosPdfName("Multiply")`. |
| **Brak istniejącego słownika ExtGState** | Przed dostępem do `resourcesEditor["ExtGState"]` sprawdź `resourcesEditor.ContainsKey("ExtGState")`. Jeśli brak, utwórz nowy pusty słownik i dodaj go do `firstPage.Resources`. |
| **Duże pliki PDF** powodują obciążenie pamięci | Użyj przeciążenia `PdfDocument.Load`, które strumieniuje strony, lub przetwarzaj strony pojedynczo wewnątrz bloku `using`. |
| **Potrzeba edycji innych zasobów** (czcionki, XObjecty) | Zastąp `"ExtGState"` przez `"Font"` lub `"XObject"` w wyszukiwaniu `resourcesEditor`, a następnie zastosuj ten sam schemat tworzenia pustego słownika i jego wypełniania. |

Te warianty pokazują, jak ten sam wzorzec **utworzyć pusty słownik PDF** stosuje się do dowolnego typu zasobu, który chcesz **edytować zasoby PDF**.

## Porady profesjonalne

* **Zweryfikuj wynik** – po zapisaniu otwórz PDF w narzędziu, które może wyświetlić surowy słownik zasobów (np. `PDFDebugger` z PDF‑Box), aby upewnić się, że wpis istnieje.
* **Ponownie używaj słowników** – jeśli dodajesz ten sam stan graficzny do wielu stron, przechowuj słownik w zmiennej i odwołuj się do niego, zamiast tworzyć go za każdym razem.
* **Kompatybilność wersji** – kod działa z Aspose.PDF 23.12 i nowszymi. Wcześniejsze wersje mogą wymagać `CosDictionary` zamiast `CosPdfDictionary`.

## Zakończenie

Teraz wiesz, jak **utworzyć pusty słownik PDF** i **edytować zasoby PDF** przy użyciu Aspose.PDF dla C#. Samouczek obejmował otwieranie dokumentu, dostęp do słownika zasobów strony, budowanie niestandardowego stanu graficznego, rejestrowanie go oraz zapisywanie wyniku. Od tego momentu możesz eksperymentować z innymi typami zasobów, łączyć wiele stanów graficznych lub zintegrować tę technikę w większym potoku przetwarzania PDF.

---

*Gotowy, aby odkrywać dalej? Spróbuj dodać niestandardowy **ExtGState** do strumienia zawartości lub manipulować słownikiem **Font**, aby osadzić nowe czcionki. Oba podejścia stosują ten sam wzorzec tworzenia pustego słownika i edycji zasobów PDF.*

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Edytuj słownik zasobów PDF przy użyciu Aspose.PDF – przewodnik C#](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Utwórz niestandardowy stan graficzny w PDF przy użyciu Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Jak utworzyć pusty stan graficzny w PDF przy użyciu C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}