---
category: general
date: 2026-10-10
description: Dowiedz się, jak zmienić przezroczystość PDF w C# przy użyciu Aspose.PDF.
  Ten przewodnik krok po kroku obejmuje przezroczystość PDF, edycję stanu graficznego
  oraz manipulację słownikiem ExtGState.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.PDF graphics state
- PDF opacity
- C# PDF manipulation
- ExtGState dictionary
language: pl
lastmod: 2026-10-10
og_description: Zmieniaj przejrzystość PDF w C# przy użyciu Aspose.PDF. Skorzystaj
  z tego zwięzłego samouczka, aby edytować przezroczystość PDF, obiekty stanu graficznego
  oraz słownik ExtGState.
og_image_alt: Screenshot showing C# code that changes PDF transparency using Aspose.PDF
og_title: Zmiana przezroczystości PDF w C# – kompletny przewodnik Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to change PDF transparency in C# using Aspose.PDF. This step‑by‑step
    guide covers PDF opacity, graphics state editing, and ExtGState dictionary manipulation.
  headline: How to change PDF transparency in C# with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF transparency
- Graphics state
title: Jak zmienić przezroczystość PDF w C# przy użyciu Aspose.PDF
url: /pl/net/programming-with-operators/how-to-change-pdf-transparency-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zmienić przezroczystość PDF w C# przy użyciu Aspose.PDF

Jeśli potrzebujesz **zmienić przezroczystość PDF** w projekcie C#, ten przewodnik pokaże Ci kompletną, gotową do uruchomienia rozwiązanie. Edytując stan graficzny PDF możesz kontrolować krycie linii (stroke opacity), krycie wypełnienia (fill opacity) oraz tryb mieszania (blend mode) bez konieczności tworzenia dokumentu od nowa.  

Zobaczysz, jak wczytać PDF, zmodyfikować **słownik ExtGState**, ustawić pożądaną **przezroczystość PDF** i zapisać wynik — wszystko przy użyciu biblioteki Aspose.PDF. Nie są wymagane żadne zewnętrzne narzędzia, a kod działa z .NET 6+.

## Wymagania wstępne

- Visual Studio 2022 (lub dowolne IDE C#)  
- .NET 6 lub nowszy runtime  
- Pakiet NuGet Aspose.PDF for .NET (`Install-Package Aspose.PDF`)  
- Plik PDF o nazwie `input.pdf` w folderze, którym zarządzasz  

Posiadanie ich zapewnia, że samouczek uruchomi się bez brakujących zależności.

## Krok 1: Wczytaj dokument PDF

Pierwszą operacją jest otwarcie istniejącego pliku PDF. Aspose.PDF reprezentuje PDF jako obiekt `Document`, który zapewnia pełny dostęp do stron, zasobów i słowników niskiego poziomu.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Cosmos;

// Load the source PDF
var document = new Document("YOUR_DIRECTORY/input.pdf");
```

*Dlaczego to ważne:* Wczytanie pliku tworzy model w pamięci, który możesz modyfikować. Klasa `Document` abstrakcyjnie reprezentuje strukturę PDF, jednocześnie udostępniając obiekty niskiego poziomu potrzebne do zmiany przezroczystości.

## Krok 2: Pobierz pierwszą stronę i jej słownik zasobów

Ustawienia przezroczystości znajdują się w słowniku zasobów strony pod wpisem **ExtGState**. Musisz uzyskać ten słownik, zanim będziesz mógł dodać lub edytować stany graficzne.

```csharp
// Get the first page (pages are 1‑based)
var page = document.Pages[1];

// The DictionaryEditor simplifies access to resource entries
var resourcesEditor = new DictionaryEditor(page.Resources);
```

*Dlaczego to ważne:* Kolekcja `Resources` zawiera czcionki, obrazy i stany graficzne używane przez stronę. Edytując ją, wpływasz tylko na wybraną stronę, pozostawiając resztę dokumentu nietkniętą.

## Krok 3: Uzyskaj (lub utwórz) słownik ExtGState

Jeśli PDF już zawiera słownik `ExtGState`, możesz go ponownie użyć; w przeciwnym razie Aspose.PDF utworzy pusty, gdy dodasz pierwszy wpis.

```csharp
// Retrieve the ExtGState dictionary; create if missing
var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
               ?? new CosPdfDictionary(document);
```

*Dlaczego to ważne:* Słownik `ExtGState` przechowuje **obiekty stanu graficznego**. Każdy obiekt definiuje parametry takie jak krycie linii (`CA`), krycie wypełnienia (`ca`) i tryb mieszania (`BM`). Zmiana tych wartości bezpośrednio wpływa na to, jak PDF renderuje elementy przezroczyste.

## Krok 4: Zdefiniuj nowy stan graficzny z żądaną przezroczystością

Utwórz nowy stan graficzny (`GS0`) i ustaw jego parametry. Poniższy przykład ustawia 100 % krycie linii, 50 % krycie wypełnienia oraz standardowy tryb mieszania „Normal”.

```csharp
// Name for the new graphics state
string graphicsStateName = "GS0";

// Create an empty dictionary for the graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

// Populate the dictionary with transparency parameters
var graphicsStateEntries = new[]
{
    // Stroke opacity (CA) – 1 = fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // Fill opacity (ca) – 0.5 = 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – "Normal" is the most common mode
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Dlaczego to ważne:* Wpis `CA` kontroluje, jak linie (obrysy, krawędzie) się mieszają, podczas gdy `ca` wpływa na wypełnienia (kształty, tekst). Dostosowanie tych wartości jest sednem **zmiany przezroczystości PDF**. Tryb mieszania określa, jak przezroczysta zawartość współdziała z leżącą pod nią grafiką.

## Krok 5: Wstaw nowy stan graficzny do słownika ExtGState

Teraz dodaj stan graficzny do kolekcji `ExtGState` strony i upewnij się, że strona odwołuje się do niego.

```csharp
// Add the new graphics state to the ExtGState dictionary
extGState.Add(graphicsStateName, newGraphicsState);

// Update the Resources dictionary with the modified ExtGState
resourcesEditor["ExtGState"] = extGState;
```

*Dlaczego to ważne:* Dodanie wpisu rejestruje stan graficzny w PDF. Każda kolejna operacja rysowania, która wybierze `GS0`, użyje zdefiniowanych przez Ciebie wartości krycia.

## Krok 6: Zastosuj stan graficzny do zawartości strony (opcjonalne, ale typowe)

Jeśli chcesz, aby istniejąca zawartość na stronie przyjęła nową przezroczystość, musisz dodać na początek operator `gs`, który wybiera stan graficzny. Poniżej znajduje się prosty sposób na dodanie tego operatora do zawartości strony.

```csharp
// Create a content stream that selects the new graphics state
var selectStateOperator = new GraphicsStateOperator(graphicsStateName);

// Insert the operator at the beginning of the page's content
page.Contents.Insert(0, selectStateOperator);
```

*Dlaczego to ważne:* Bez tego kroku stan graficzny istnieje, ale nigdy nie jest używany. Operator `gs` (`GraphicsStateOperator`) instruuje renderera PDF, aby zastosował zdefiniowane ustawienia krycia do wszystkiego, co następuje później.

## Krok 7: Zapisz zmodyfikowany PDF

Na koniec zapisz zaktualizowany dokument na dysku.

```csharp
document.Save("YOUR_DIRECTORY/output.pdf");
```

Wynikowy `output.pdf` będzie renderowany z określonym przez Ciebie kryciem wypełnienia (50 % przezroczystości), zachowując jednocześnie oryginalny układ.

---

## Pełny kod źródłowy (do uruchomienia)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cosmos;
using System.Collections.Generic;

class ChangePdfTransparency
{
    static void Main()
    {
        // 1️⃣ Load the PDF
        var document = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Get first page and its resource dictionary
        var page = document.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3️⃣ Access (or create) the ExtGState dictionary
        var extGState = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                       ?? new CosPdfDictionary(document);

        // 4️⃣ Define a new graphics state (GS0) with desired opacity
        string gsName = "GS0";
        var newGs = CosPdfDictionary.CreateEmptyDictionary(document);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGs.Add(e);

        // 5️⃣ Add the graphics state to ExtGState and update resources
        extGState.Add(gsName, newGs);
        resourcesEditor["ExtGState"] = extGState;

        // 6️⃣ Apply the graphics state to existing content (optional)
        var gsOperator = new GraphicsStateOperator(gsName);
        page.Contents.Insert(0, gsOperator);

        // 7️⃣ Save the modified PDF
        document.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**Oczekiwany wynik:** Otworzenie `output.pdf` w Adobe Acrobat lub dowolnym przeglądarce PDF pokazuje, że wszystkie wypełnione kształty na pierwszej stronie są renderowane z 50 % kryciem, podczas gdy linie pozostają w pełni nieprzezroczyste. Zmiana wizualna potwierdza, że pomyślnie **zmieniłeś przezroczystość PDF**.

---

## Częste pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| *Czy mogę zmienić przezroczystość konkretnego obiektu zamiast całej strony?* | Tak. Zamiast wstawiać operator `gs` na początku strony, umieść go bezpośrednio przed poleceniami rysowania, które dotyczą danego obiektu. Użyj `page.Contents.Insert(index, gsOperator)`, gdzie `index` wskazuje pożądaną pozycję. |
| *Co zrobić, jeśli PDF już ma wpis ExtGState o nazwie „GS0”?* | Wybierz unikalną nazwę (np. `GS1`) lub nadpisz istniejący wpis, jeśli zamierzasz go zastąpić. Klucz słownika musi być unikalny w ramach zasobów strony. |
| *Czy wartość `ca` jest ograniczona do 0‑1?* | Tak. `ca` (krycie wypełnienia) i `CA` (krycie linii) przyjmują wartości od 0 (całkowicie przezroczyste) do 1 (całkowicie nieprzezroczyste). Wartości poza tym zakresem są ograniczane. |
| *Czy to działa z PDF‑ami używającymi zgodności PDF/A lub PDF/X?* | Modyfikacja stanu graficznego może naruszyć ścisłą zgodność. Jeśli musisz zachować zgodność, zweryfikuj wynik przy użyciu walidatora PDF/A i odpowiednio dostosuj słownik (np. dodaj wpisy `/PDFXConformance`). |
| *Czy mogę ustawić inny tryb mieszania, np. „Multiply”?* | Oczywiście. Zastąp `new CosPdfName("Normal")` na `new CosPdfName("Multiply")` lub dowolny tryb mieszania zdefiniowany w specyfikacji PDF. |

---

## Wskazówki i najlepsze praktyki (E‑E‑A‑T)

- **Pro tip:** Przechowuj w pamięci słownik `ExtGState` po pierwszej modyfikacji, jeśli planujesz edytować wiele stron; zmniejsza to narzut tworzenia obiektów.  
- **Uwaga:** Ponowne użycie tej samej nazwy stanu graficznego na różnych stronach bez aktualizacji zasobów może powodować nieoczekiwane mieszanie krycia. Zawsze ograniczaj nazwę do strony lub używaj globalnie unikalnego identyfikatora.  
- **Wydajność:** W przypadku dużych PDF‑ów rozważ przetwarzanie stron równolegle (`Parallel.ForEach`), ale synchronizuj dostęp do obiektu `Document`, aby uniknąć problemów z bezpieczeństwem wątków.  
- **Testowanie:** Zweryfikuj zmiany przezroczystości w co najmniej dwóch przeglądarkach (Adobe Acrobat Reader oraz wtyczka PDF w przeglądarce), ponieważ niektóre przeglądarki obsługują tryby mieszania inaczej.  

---

## Zakończenie

Teraz wiesz, jak **zmienić przezroczystość PDF** w C# poprzez edycję **słownika ExtGState** przy użyciu Aspose.PDF. Samouczek obejmował wczytywanie PDF, tworzenie własnego stanu graficznego, zastosowanie go do zawartości strony oraz zapis zaktualizowanego pliku.  

Od tego momentu możesz zgłębiać bardziej zaawansowane tematy **manipulacji PDF w C#**, takie jak warstwowanie wielu stanów graficznych, stosowanie różnych wartości **przezroczystości PDF** dla poszczególnych obiektów lub integrację z wysokopoziomowymi API Aspose.PDF do wstawiania tekstu i obrazów.  

Śmiało eksperymentuj z innymi trybami mieszania, poziomami krycia lub zastosowaniem stanu graficznego tylko do wybranych stron. Jeśli napotkasz problemy, dokumentacja Aspose.PDF dostarcza głębszych informacji na temat modelu obiektowego PDF i obsługi stanu graficznego.  

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Zmień przezroczystość PDF przy użyciu Aspose.PDF – Kompletny przewodnik C#](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Dodaj przezroczystość do PDF przy użyciu Aspose PDF w C# – Przewodnik krok po kroku](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Dodaj przezroczystość do PDF przy użyciu Aspose – Kompletny przewodnik C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}