---
category: general
date: 2026-02-14
description: Dodaj numerację Bates do plików PDF w swoich dokumentach bez wysiłku.
  Dowiedz się, jak dodać numery stron w stopce i kolejno numerować PDF za pomocą Aspose.Pdf
  w kilka minut.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: pl
og_description: Szybko dodaj numerację Bates do PDF. Ten przewodnik pokazuje, jak
  dodać numery stron w stopce oraz kolejno numerowane PDF przy użyciu Aspose.Pdf,
  z pełnym kodem i wskazówkami.
og_title: Dodaj numerację Bates do PDF – samouczek C# krok po kroku
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Dodaj numerację Bates do PDF – Kompletny przewodnik C#
url: /pl/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

numbers PDF** files with a custom prefix, font size, and alignment. By the end you’ll have a ready‑to‑run C# program, a clear understanding of why each setting matters, and a few pro tips to avoid the most common pitfalls."

Translate accordingly.

Proceed similarly for other sections.

Make sure bullet points remain bullet list.

Preserve code block placeholders.

Make sure to keep markdown formatting.

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj numerację Bates do PDF – Kompletny przewodnik C#

Czy kiedykolwiek potrzebowałeś **add Bates numbering PDF** plików, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam. Zespoły prawne, audytorzy i wszyscy, którzy obsługują duże zestawy dokumentów, ciągle pytają: „Jak dodać numery Bates bez psucia układu?” Dobrą wiadomością jest to, że z Aspose.Pdf dla .NET możesz wstrzyknąć te numery jako prostą stopkę — bez ręcznej edycji.

W tym tutorialu przeprowadzimy Cię przez praktyczne, kompleksowe rozwiązanie, które nie tylko **adds footer page numbers**, ale także pozwala **add sequential numbers PDF** plikom z własnym prefiksem, rozmiarem czcionki i wyrównaniem. Po zakończeniu będziesz mieć gotowy do uruchomienia program w C#, jasne zrozumienie, dlaczego każde ustawienie ma znaczenie, oraz kilka profesjonalnych wskazówek, jak uniknąć najczęstszych pułapek.

## Co się nauczysz

- Jak załadować istniejący PDF i przygotować go do numeracji Bates.  
- Które właściwości **BatesNumberingOptions** kontrolują wygląd i położenie.  
- Jak zastosować numerację do każdej strony jednym wywołaniem.  
- Sposoby dostosowania prefiksu, numeru początkowego i marginesów dla różnych formatów prawnych.  
- Obsługa przypadków brzegowych — co zrobić z zaszyfrowanymi PDF‑ami lub dokumentami, które już zawierają stopki.

**Wymagania wstępne**: .NET 6+ (lub .NET Framework 4.7+), najnowsza wersja Aspose.Pdf (przykład używa 23.10) oraz plik PDF, do którego masz prawo modyfikacji. Nie są potrzebne inne biblioteki firm trzecich.

---

## Krok 1 – Załaduj PDF, który chcesz ponumerować

Pierwszą rzeczą, którą robimy, jest utworzenie instancji `Document`, wskazującej na plik źródłowy. Użycie wzorca `using var` zapewnia automatyczne zwolnienie uchwytu pliku.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Dlaczego to ważne:** Aspose.Pdf wczytuje całą strukturę PDF do pamięci, co pozwala nam manipulować stronami, adnotacjami i metadanymi bez modyfikacji oryginalnego pliku na dysku. Jeśli PDF jest zabezpieczony hasłem, możesz przekazać hasło do konstruktora — zobacz notatkę „Encrypted PDFs” na końcu.

---

## Krok 2 – Zdefiniuj opcje numeracji Bates

Numery Bates to w zasadzie stopki stron z konfigurowalnym prefiksem i licznikem sekwencyjnym. Klasa `BatesNumberingOptions` umożliwia precyzyjne dostrojenie każdego aspektu wizualnego.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Szybka wskazówka

- **Prefix**: Użyj krótkiego, unikalnego identyfikatora (np. numeru sprawy), aby stopka była czytelna.  
- **StartNumber**: Firmy prawne często zaczynają od `1` lub własnego offsetu; wybierz to, co pasuje do Twojego systemu archiwizacji.  
- **Margins**: Dolny margines `20` punktów utrzymuje tekst z dala od przypisów lub podpisów, które mogą już znajdować się przy krawędzi strony.

---

## Krok 3 – Zastosuj numerację do wszystkich stron

Po skonfigurowaniu opcji właściwe wstawienie to jednowierszowy kod. Aspose.Pdf obsługuje paginację, aktualizuje istniejące strumienie treści i automatycznie respektuje rotację strony.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **Co się dzieje pod maską?** Biblioteka iteruje po każdym obiekcie `Page`, tworzy `TextFragment` zawierający prefiks i bieżący licznik, a następnie rysuje go przy użyciu układu współrzędnych strony. Ponieważ ustawiliśmy `HorizontalAlignment.Right` i `VerticalAlignment.Bottom`, tekst przykleja się do dolnego‑prawego rogu, niezależnie od rozmiaru strony.

---

## Krok 4 – Zapisz zmodyfikowany PDF

Na koniec zapisz wynik do nowego pliku. Nadpisanie oryginału jest możliwe, ale zachowanie kopii ułatwia kontrolę wersji.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Jeśli potrzebujesz zachować oryginalne metadane (autor, data utworzenia), Aspose.Pdf kopiuje je domyślnie. Możesz także podać obiekt `SaveOptions` w celu zapewnienia zgodności z PDF/A lub kompresji.

---

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Wklej go do projektu aplikacji konsolowej, dostosuj ścieżki plików i naciśnij **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Oczekiwany rezultat:** Każda strona `output.pdf` wyświetla teraz stopkę w formacie `ABC-1000`, `ABC-1001`, … umieszczoną w dolnym‑prawym rogu. Otwórz plik w dowolnym czytniku PDF, aby to zweryfikować.

---

## Obsługa typowych wariantów

### Dodawanie wyłącznie numerów stron w stopce

Jeśli potrzebujesz tylko prostych numerów stron bez prefiksu, ustaw `Prefix = ""` i ewentualnie dostosuj margines, aby uniknąć kolizji ze istniejącymi stopkami.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Użycie innego wyrównania

Dokumenty prawne czasem wymagają wyśrodkowania numeru na dole. Zmień wyrównanie:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Praca z zaszyfrowanymi PDF‑ami

Gdy źródłowy PDF jest zabezpieczony hasłem, przekaż je w następujący sposób:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

Reszta przepływu pozostaje niezmieniona.

### Pomijanie istniejących stopek

Jeśli dokument już zawiera stopkę, której nie chcesz nadpisać, możesz dodać własny ciąg znaków, aby nowy numer był wyraźny, lub ręcznie iterować po stronach i dodawać `TextFragment` tylko tam, gdzie stopka jest nieobecna. Klasa `Page` udostępnia kolekcje `Annotations` i `Contents` do precyzyjnej kontroli.

---

## Porady profesjonalne i pułapki

- **Unikaj przycinania**: Bardzo małe dolne marginesy mogą spowodować odcięcie tekstu na drukarkach. Przetestuj na wydruku fizycznym, jeśli zamierzasz dystrybuować wersje papierowe.  
- **Wydajność**: Dodanie numeracji Bates do 500‑stronnicowego PDF zajmuje mniej niż sekundę na nowoczesnym laptopie, ale przy dużych partiach warto rozważyć przetwarzanie równoległe — pamiętaj jednak, że `Document` nie jest wątkowo‑bezpieczny, więc każdy wątek potrzebuje własnej instancji.  
- **Kompatybilność wersji**: Kod działa z Aspose.Pdf 23.10 i nowszymi. W starszych wersjach nazwy właściwości są takie same, ale konstruktor `MarginInfo` może wymagać argumentów typu `float`.  
- **Zgodność prawna**: Niektóre jurysdykcje wymagają umieszczenia numeru Bates w określonym miejscu (np. dolny‑lewy róg). Dostosuj odpowiednio `HorizontalAlignment`.

---

## Zakończenie

Pokazaliśmy, jak **add Bates numbering PDF** pliki przy użyciu Aspose.Pdf dla .NET, obejmując wszystko od ładowania dokumentu po zapis finalnej wersji ze schludną stopką. Modyfikując kilka właściwości, możesz także **add footer page numbers**, **add sequential numbers PDF**, lub dostosować wygląd do dowolnego standardu prawnego.

Gotowy na kolejny krok? Spróbuj połączyć tę technikę z ekstrakcją tekstu OCR, aby osadzić wyszukiwalne słowa kluczowe obok numerów Bates, lub zautomatyzuj proces dla całych folderów przy użyciu `Directory.GetFiles`. Możliwości są nieograniczone, a fundament, który teraz posiadasz, ułatwi dalsze rozszerzenia.

Miłego kodowania i niech Twoje PDF‑y zawsze będą idealnie ponumerowane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}