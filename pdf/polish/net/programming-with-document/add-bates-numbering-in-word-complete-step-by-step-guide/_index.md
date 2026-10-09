---
category: general
date: 2026-06-21
description: Szybko dodaj numerację Batesa w Wordzie. Dowiedz się, jak dodać numerację
  Batesa, zastosować ją w dokumentach prawnych i zautomatyzować numerację przy użyciu
  C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: pl
og_description: Dodaj numerację Bates w Wordzie przy użyciu C#. Ten przewodnik pokazuje,
  jak dodać numerację Bates, zastosować ją w dokumentach prawnych i zautomatyzować
  proces.
og_title: Dodaj numerację Bates w Word – pełny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Dodaj numerację Bates w Wordzie – Kompletny przewodnik krok po kroku
url: /pl/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj numerację Bates w Word – Kompletny przewodnik krok po kroku

Zastanawiałeś się kiedyś, jak dodać numerację Bates do pliku Word bez ręcznego wpisywania każdego numeru? Nie jesteś sam. Wielu prawników, asystentów prawnych i specjalistów ds. e‑discovery potrzebuje niezawodnego sposobu na **dodanie numeracji Bates** do setek stron, a robienie tego ręcznie to koszmar.

W tym samouczku przeprowadzimy Cię przez czyste rozwiązanie w C#, które **stosuje numerację Bates** do pliku `.docx`, wyjaśni, dlaczego każda linia ma znaczenie, i pokaże, jak dostosować kod do potrzeb prawnych. Po zakończeniu będziesz w stanie wygenerować idealnie ponumerowany dokument w kilka sekund — bez dodatkowych wtyczek.

## Czego się nauczysz

- Dokładny kod potrzebny do **dodania numeracji Bates** do dokumentu Word.
- Jak działa klasa `BatesNumberingOptions` i dlaczego możesz chcieć zmienić prefiks lub wartość początkową.
- Wskazówki dotyczące używania tego podejścia w dużych aktach spraw, w tym kwestie pamięciowe.
- Szybki przegląd wymagań wstępnych, abyś mógł skopiować‑wkleić rozwiązanie i uruchomić je już dziś.

**Wymagania wstępne**  
- .NET 6+ (lub .NET Framework 4.7.2+, jeśli wolisz starszy runtime).  
- Odwołanie do biblioteki Aspose.Words for .NET (lub dowolnego podobnego API, które udostępnia `AddBatesNumbering`).  
- Podstawowa znajomość C# i Visual Studio (lub ulubionego IDE).

Jeśli spełniasz te warunki, zanurzmy się.

## Krok 1: Utwórz projekt i zaimportuj bibliotekę

Najpierw utwórz nową aplikację konsolową (lub zintegrować z istniejącą usługą). Następnie dodaj pakiet NuGet Aspose.Words:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Użyj darmowej licencji ewaluacyjnej do testów; dodaje mały znak wodny, ale w pozostałych aspektach działa tak samo jak pełna wersja.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Te dyrektywy `using` wprowadzają klasy `Document` i `BatesNumberingOptions` do zakresu, co jest niezbędne w późniejszym kroku **zastosowania numeracji Bates**.

## Krok 2: Załaduj dokument źródłowy

Potrzebujesz pliku Word, na którym będziesz pracować. Poniższy kod ładuje `input.docx` z folderu, który wskażesz. Zamień `"YOUR_DIRECTORY"` na rzeczywistą ścieżkę na swoim komputerze.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Dlaczego najpierw ładujemy plik? Obiekt `Document` parsuje cały pakiet Worda do pamięci, co pozwala nam manipulować nagłówkami, stopkami i układem stron przed zapisaniem. Jeśli plik jest ogromny (np. 10 000 stron), rozważ użycie `LoadOptions` z `LoadFormat.Docx`, aby strumieniowo wczytywać sekcje zamiast ładować wszystko naraz.

## Krok 3: Skonfiguruj opcje numeracji Bates

Tutaj dzieje się magia. Mówisz bibliotece, jakiego prefiksu użyć (`"ABC-"` w przykładzie) i od którego numeru rozpocząć liczenie (`1000`). Obie wartości są w pełni konfigurowalne.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Dlaczego prefiks?** W praktyce prawnej prefiksy często identyfikują sprawę lub stronę produkującą (`"ABC-"` może oznaczać *Acme Bank Corp.*). Rozpoczęcie od `1000` jest powszechne, ponieważ wiele kancelarii rezerwuje pierwsze 999 numerów dla wewnętrznych wersji roboczych.

Jeśli pracujesz z **numeracją Bates dla dokumentów prawnych**, możesz także ustawić `batesOptions.Position` na `Header` lub `Footer` oraz dostosować wyrównanie zgodnie z wymogami sądu. Biblioteka obsługuje te zmiany od razu.

## Krok 4: Zastosuj numerację Bates w całym dokumencie

Teraz faktycznie wstawiamy numery. Metoda `AddBatesNumbering` przechodzi przez każdą stronę, wstawia sformatowany ciąg i aktualizuje wewnętrzną liczbę stron dokumentu.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Za kulisami Aspose.Words tworzy ukryte pole na każdej stronie, które renderuje się jako `ABC-1000`, `ABC-1001` i tak dalej. Ponieważ jest to pole, później możesz edytować prefiks lub numer początkowy bez konieczności regenerowania całego pliku — przydatne przy **jak dodać numerację Bates** po zmianie żądania discovery.

## Krok 5: Zapisz zmodyfikowany dokument

Na koniec zapisz wynik do nowego pliku. Zachowanie oryginału nietkniętego jest dobrą praktyką, szczególnie przy dowodach, które muszą pozostać nienaruszone.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Masz teraz `output.docx` z kolejno numerowanymi numerami Bates na każdej stronie. Otwórz go w Wordzie, a zobaczysz numery dokładnie tam, gdzie je określiłeś (domyślnie w stopce). Rozmiar pliku może nieco wzrosnąć z powodu dodatkowych pól, ale jest to znikoma cena w porównaniu z korzyściami.

### Oczekiwany wynik

| Strona | Numer Bates |
|--------|-------------|
| 1      | ABC-1000    |
| 2      | ABC-1001    |
| …      | …           |
| N      | ABC‑(1000 + N‑1) |

Jeśli otworzysz widok „Field Codes” w Wordzie (`Alt+F9`), zobaczysz coś w stylu `{ BATES \* MERGEFORMAT ABC-1000 }` na każdej stronie.

## Przypadki brzegowe i najczęstsze pytania

### Co jeśli dokument już zawiera numery stron?

Metoda `AddBatesNumbering` **nie** nadpisze istniejących pól numeracji stron; po prostu doda nowe pole. Jeśli chcesz zastąpić istniejące numery, usuń je najpierw lub ustaw `batesOptions.Position` na tę samą lokalizację, co aktualne numery stron.

### Czy mogę pominąć niektóre strony (np. stronę tytułową)?

Tak. Użyj przeciążenia, które przyjmuje `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Jest to przydatne, gdy potrzebujesz **numeracji Bates dla dokumentów prawnych**, które zaczynają się po stronie tytułowej.

### Jak zmienić format numeracji (liczby rzymskie, litery)?

Klasa `BatesNumberingOptions` obsługuje właściwość `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Ustaw ją przed wywołaniem `AddBatesNumbering`. Ta elastyczność pomaga, gdy sąd wymaga konkretnego stylu.

### Co z wydajnością przy ogromnych plikach?

Wczytanie pliku Word o wielkości 2 GB może pochłonąć dużo RAMu. Aby to ograniczyć, przetwarzaj dokument w kawałkach przy użyciu narzędzia `DocumentSplitter`, zastosuj numerację Bates do każdego fragmentu, a następnie scal części z powrotem. Ten wzorzec utrzymuje zużycie pamięci pod kontrolą, jednocześnie pozwalając **zastosować numerację Bates** efektywnie.

## Pełny działający przykład

Łącząc wszystko razem, oto gotowy do uruchomienia program konsolowy:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Uruchom program, otwórz `output.docx` i zobacz czystą serię numerów gotową do składania, discovery lub złożenia w sądzie.

## Zakończenie

Teraz dokładnie wiesz, **jak dodać numerację Bates** do dokumentu Word przy użyciu C#. Kroki — ładowanie, konfiguracja, zastosowanie i zapis — są proste, a jednocześnie na tyle elastyczne, by spełnić **numerację Bates dla procesów prawnych**, własne prefiksy oraz przetwarzanie wsadowe na dużą skalę.

Jeśli chcesz pójść dalej, rozważ:

- Integrację kodu z API webowym, aby koledzy mogli wgrywać pliki i natychmiast otrzymywać ponumerowane PDF‑y.  
- Dodanie obsługi błędów dla brakujących plików lub problemów z uprawnieniami (krótkie `try/catch` wokół `Document.Load`).  
- Eksplorację innych funkcji Aspose.Words, takich jak znaki wodne lub redakcja, aby stworzyć pełny zestaw narzędzi e‑discovery.

Śmiało eksperymentuj z różnymi prefiksami, numerami początkowymi lub nawet łącz różne schematy numeracji w jednym dokumencie. Świat **zastosowania numeracji Bates** jest zaskakująco wszechstronny, gdy masz już podstawową logikę pod ręką.

Masz pytania lub trudny scenariusz? zostaw komentarz poniżej, a wspólnie znajdziemy rozwiązanie. Szczęśliwego kodowania!


## Co powinieneś nauczyć się dalej?


Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz wyczerpujące wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Zastosuj styl numeracji w nagłówku PDF przy użyciu Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Zastosuj styl numeracji w nagłówku PDF przy użyciu Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Zastosuj styl numeracji w nagłówku PDF przy użyciu Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}