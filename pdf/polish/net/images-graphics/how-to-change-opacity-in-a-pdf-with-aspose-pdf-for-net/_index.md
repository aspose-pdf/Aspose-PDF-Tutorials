---
category: general
date: 2026-09-15
description: Jak zmienić przezroczystość w pliku PDF przy użyciu Aspose.Pdf dla .NET
  i dowiedzieć się, jak dodać przezroczystość przy zapisywaniu zmodyfikowanych plików
  PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change opacity
- how to add transparency
- save modified pdf
language: pl
lastmod: 2026-09-15
og_description: Jak zmienić przezroczystość w pliku PDF przy użyciu Aspose.Pdf dla
  .NET, w tym jak dodać przezroczystość i zapisać zmodyfikowane pliki PDF w ciągu
  kilku minut.
og_image_alt: Screenshot showing a PDF page before and after opacity changes
og_title: Jak zmienić przezroczystość w pliku PDF przy użyciu Aspose.Pdf – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: How to change opacity in a PDF using Aspose.Pdf for .NET and learn
    how to add transparency while you save modified PDF files.
  headline: How to change opacity in a PDF with Aspose.Pdf for .NET
  type: TechArticle
tags:
- Aspose.Pdf
- .NET
- PDF manipulation
title: Jak zmienić przezroczystość w pliku PDF przy użyciu Aspose.Pdf dla .NET
url: /pl/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zmienić przezroczystość w pliku PDF przy użyciu Aspose.Pdf dla .NET

Jeśli potrzebujesz **jak zmienić przezroczystość** obiektów w PDF, ten przewodnik pokaże Ci dokładne kroki przy użyciu Aspose.Pdf dla .NET. Zobaczysz także **jak dodać przezroczystość** do stanów graficznych i poznasz prawidłowy sposób **zapisania zmodyfikowanego PDF** bez utraty jakości.

Zmiana przezroczystości jest częstym wymogiem, gdy chcesz nakładać znaki wodne, tworzyć przyciemnione tła lub budować efekty podobne do UI wewnątrz dokumentu. Przykładowy kod poniżej działa z każdym PDF, który Aspose.Pdf potrafi otworzyć, a tutorial przeprowadza Cię przez każdą linię, abyś zrozumiał *dlaczego* ma to znaczenie.

## Czego się nauczysz

- Załadować dokument PDF przy użyciu Aspose.Pdf.
- Edytować słownik zasobów strony, aby utworzyć nowy stan graficzny.
- Zdefiniować przezroczystość obrysu (`CA`), wypełnienia (`ca`) oraz tryb mieszania (`BM`).
- Wstawić stan graficzny do słownika `ExtGState`.
- **Zapisz zmodyfikowane PDF** zachowujące nowe ustawienia przezroczystości.
- Obsłużyć przypadki brzegowe, takie jak brak wpisów `ExtGState` lub dokumenty wielostronicowe.

### Wymagania wstępne

| Wymaganie | Powód |
|-----------|-------|
| .NET 6.0 lub nowszy | Dostarcza środowisko uruchomieniowe dla kodu C#. |
| Aspose.Pdf for .NET (pakiet NuGet `Aspose.Pdf`) | Udostępnia API do manipulacji PDF użyte w przykładzie. |
| Podstawowa znajomość C# | Potrzebna do zrozumienia składni i struktury projektu. |
| Plik wejściowy PDF (`input.pdf`) | Plik, który będziesz modyfikować. |

> **Pro tip:** Zainstaluj pakiet poleceniem `dotnet add package Aspose.Pdf` przed rozpoczęciem.

## Krok 1: Załaduj dokument PDF

Pierwszą operacją jest otwarcie pliku źródłowego. Użycie bloku `using` zapewnia prawidłowe zwolnienie zasobów, co zapobiega blokadom plików w systemie Windows.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

> **Dlaczego to ważne:** Otwarcie dokumentu tworzy jego reprezentację w pamięci, którą możesz edytować. Instrukcja `using` zapewnia zwolnienie zasobów, co jest niezbędne, gdy później **zapiszesz zmodyfikowany PDF** w tym samym folderze.

## Krok 2: Pobierz pierwszą stronę i jej słownik zasobów

Ustawienia przezroczystości znajdują się w słowniku zasobów strony. Dla uproszczenia skupiamy się na pierwszej stronie, ale ta sama logika działa dla dowolnego indeksu strony.

```csharp
// Step 2: Retrieve the first page and its resources
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

> **Dlaczego to ważne:** `Resources` zawiera obiekty takie jak czcionki, obrazy oraz słownik `ExtGState`, w którym przechowywane są stany graficzne. Edycja tego słownika jest jedynym sposobem na wpływanie na przezroczystość poleceń rysujących, które odwołują się do tego stanu.

## Krok 3: Upewnij się, że istnieje słownik ExtGState

Jeśli PDF już zawiera wpis `ExtGState`, możemy go ponownie użyć. W przeciwnym razie musimy utworzyć nowy słownik, aby uniknąć `KeyNotFoundException`.

```csharp
// Step 3: Get or create the ExtGState dictionary
Aspose.Pdf.CosCosPdfDictionary extGStateDict;

if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and attach it
    extGStateDict = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

> **Dlaczego to ważne:** PDF‑y są elastyczne; niektóre pliki nigdy nie definiują `ExtGState`. Utworzenie go zapewnia miejsce dla kolejnych parametrów przezroczystości.

## Krok 4: Zbuduj nowy stan graficzny z wartościami przezroczystości

Stan graficzny (`GS`) przechowuje parametry renderowania. Klucze `CA` (przezroczystość obrysu) i `ca` (przezroczystość wypełnienia) przyjmują wartości od `0` (całkowicie przezroczyste) do `1` (w pełni nieprzezroczyste). Klucz `BM` wybiera tryb mieszania; `"Normal"` jest najczęściej używany.

```csharp
// Step 4: Create a graphics state dictionary and set opacity parameters
var graphicsState = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA", new Aspose.Pdf.CosPdfNumber(1.0)),   // stroke opacity (fully opaque)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca", new Aspose.Pdf.CosPdfNumber(0.5)), // fill opacity (50% transparent)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM", new Aspose.Pdf.CosPdfName("Normal")) // blend mode
};

foreach (var p in parameters)
{
    graphicsState.Add(p);
}
```

> **Dlaczego to ważne:** Ustawienie `ca` na `0.5` mówi rendererowi PDF, aby rysował wypełnione kształty z połową przezroczystości. Dostosuj wartości liczbowe do swoich wymagań projektowych. Wpis `BM` jest opcjonalny, ale wyjaśnia, jak przezroczysty content miesza się z obiektami leżącymi pod spodem.

## Krok 5: Zarejestruj nowy stan graficzny w słowniku ExtGState

Każdy stan graficzny musi mieć unikalną nazwę (np. `"GS0"`). Możesz ponownie użyć istniejącej nazwy, jeśli chcesz nadpisać stan, ale użycie nowego identyfikatora zapobiega niezamierzonym skutkom ubocznym.

```csharp
// Step 5: Add the graphics state to ExtGState with a unique name
extGStateDict.Add("GS0", graphicsState);
```

> **Dlaczego to ważne:** Po zapisaniu stanu możesz odwołać się do niego w strumieniach zawartości strony przy użyciu operatora `/GS0`. To jest mechanizm, który faktycznie **jak dodać przezroczystość** do poleceń rysujących.

## Krok 6: Zapisz zmodyfikowany PDF

Po zaktualizowaniu słownika zasobów zapisz zmiany na dysku. Możesz nadpisać oryginalny plik lub utworzyć nowy; w przykładzie tworzony jest `output.pdf`, aby zachować źródło nietknięte.

```csharp
// Step 6: Save the modified PDF
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Dlaczego to ważne:** Metoda `Save` serializuje obiekty w pamięci, w tym nowy stan graficzny, do prawidłowego pliku PDF. To ostatni krok w **jak zmienić przezroczystość** i **zapisaniu zmodyfikowanego PDF**.

## Pełny, gotowy do uruchomienia przykład

Połączenie wszystkich elementów daje Ci samodzielny program, który możesz skopiować do aplikacji konsolowej.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Collections;

class Program
{
    static void Main()
    {
        // Path to the source PDF
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";

        // Load the document
        using var pdfDocument = new Document(pdfPath);

        // Work with the first page
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState exists
        CosCosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create a new graphics state with opacity settings
        var graphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
        };
        foreach (var p in parameters)
            graphicsState.Add(p);

        // Add the state to ExtGState under the name "GS0"
        extGStateDict.Add("GS0", graphicsState);

        // Save the result
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        Console.WriteLine("Opacity changed and PDF saved successfully.");
    }
}
```

### Oczekiwany rezultat

Otwórz `output.pdf` w dowolnym przeglądarce PDF. Każda treść, która później odwołuje się do stanu graficznego `GS0` (np. prostokąt rysowany poleceniem `/GS0 gs`), pojawi się z **50 % przezroczystością wypełnienia**, podczas gdy obrys pozostanie w pełni nieprzezroczysty. Jeśli dodasz takie polecenia rysujące za pomocą API `Page.Contents.Add` Aspose.Pdf, efekt przezroczystości będzie widoczny od razu.

## Obsługa wielu stron i wielu stanów graficznych

- **Wiele stron:** Iteruj po `pdfDocument.Pages` i powtarzaj kroki 2‑5 dla każdej strony, którą chcesz zmodyfikować. Pamiętaj, aby używać odrębnych nazw stanów (`GS1`, `GS2`, …), jeśli strony wymagają różnych poziomów przezroczystości.
- **Ponowne użycie istniejącego stanu:** Jeśli PDF już zawiera stan o nazwie `"GS0"` i chcesz jedynie zmienić jego przezroczystość, pobierz go za pomocą `extGStateDict["GS0"]` zamiast tworzyć nowy wpis.
- **Wskazówka wydajnościowa:** Dodawanie wielu stanów graficznych może zwiększyć rozmiar pliku. Konsoliduj identyczne ustawienia przezroczystości w jednym stanie i odwołuj się do niego z wielu stron.

## Typowe pułapki i jak ich unikać

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| `KeyNotFoundException` przy `"ExtGState"` | PDF nie posiada tego słownika. | Utwórz go, jak pokazano w Kroku 3. |
| Przezroczystość nie jest widoczna | Strumień zawartości nie odwołuje się do nowego stanu. | Wstaw `/GS0 gs` przed poleceniami rysującymi lub użyj API `Graphics` Aspose.Pdf z parametrem `GraphicsState`. |
| Wyjściowy PDF jest uszkodzony | Próba zapisu do folderu tylko do odczytu. | Upewnij się, że ścieżka docelowa jest zapisywalna i nie jest tym samym plikiem, który jest nadal otwarty. |
| Wartości przezroczystości > 1 lub < 0 | Przypadkowe podanie procentów zamiast ułamków. | Używaj liczb w przedziale od `0.0` do `1.0`. |

## Kolejne kroki

Teraz, gdy wiesz **jak zmienić przezroczystość** i **jak dodać przezroczystość**, możesz zgłębiać powiązane tematy:

- **jak dodać przezroczystość** do obrazów przy użyciu obiektów `Image` i właściwości `Transparency`.
- Łączenie wielu PDF‑ów przy zachowaniu stanów graficznych.
- Korzystanie z opcji **zapisz zmodyfikowany PDF** takich jak `PdfSaveOptions`, aby kompresować lub szyfrować wynik.

Eksperymentuj z różnymi wartościami `ca` i `CA`, trybami mieszania jak `"Multiply"` czy `"Screen"` i obserwuj, jak wpływają na wygląd końcowy. Techniki opisane tutaj stanowią solidną podstawę do zaawansowanego stylizowania PDF‑ów w


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}