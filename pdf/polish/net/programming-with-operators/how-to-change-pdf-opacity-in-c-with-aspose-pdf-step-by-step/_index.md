---
category: general
date: 2026-10-23
description: Jak zmienić przezroczystość PDF przy użyciu Aspose.Pdf w C#. Dowiedz
  się, jak edytować ExtGState, ustawiać przezroczystość obrysu/wypełnienia oraz stosować
  tryby mieszania w zaledwie kilku linijkach kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change PDF opacity
- Aspose.Pdf opacity
- PDF graphics state
- ExtGState dictionary
- C# PDF manipulation
- PDF blend mode
language: pl
lastmod: 2026-10-23
og_description: Jak zmienić przezroczystość PDF przy użyciu Aspose.Pdf w C#. Skorzystaj
  z tego zwięzłego przewodnika, aby zmodyfikować przezroczystość linii i wypełnienia,
  ustawić tryby mieszania i zapisać zaktualizowany dokument.
og_image_alt: Screenshot of a PDF page with semi‑transparent graphics created by Aspose.Pdf
  in C#
og_title: Jak zmienić przezroczystość PDF w C# – kompletny samouczek Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  headline: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  name: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf;'
  - name: Get the first page and its resource dictionary
    text: '```csharp // Step 2: Get the first page and its resource dictionary var
      firstPage = pdfDocument.Pages[1]; var resourcesEditor = new DictionaryEditor(firstPage.Resources);
      ```'
  - name: Retrieve (or create) the ExtGState dictionary
    text: '```csharp // Step 3: Retrieve the ExtGState dictionary from the page resources
      // If ExtGState does not exist, create an empty one. CosPdfDictionary extGStateDict;
      if (resourcesEditor.ContainsKey("ExtGState")) { extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
      } else { extGStateDic'
  - name: Create a new graphics state dictionary and define opacity entries
    text: '```csharp // Step 4: Create a new graphics state dictionary and define
      its entries var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
      var graphicsStateEntries = new[] { new KeyValuePair<string, ICosPdfPrimitive>("CA",
      new CosPdfNumber(1.0)), // Stroke opacity (fully opaque)'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Step 5: Add the new graphics state to the ExtGState dictionary
      (named "GS0") extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: Save the updated PDF document
    text: '```csharp // Step 6: Save the updated PDF document pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      } ```'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Opacity
- GraphicsState
title: Jak zmienić przezroczystość PDF w C# przy użyciu Aspose.Pdf – przewodnik krok
  po kroku
url: /pl/net/programming-with-operators/how-to-change-pdf-opacity-in-c-with-aspose-pdf-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zmienić przezroczystość PDF w C# przy użyciu Aspose.Pdf – przewodnik krok po kroku

Jeśli potrzebujesz **jak zmienić przezroczystość PDF** dla konkretnych elementów, ten samouczek przedstawia kompletną, działającą rozwiązanie. Zobaczysz, jak edytować słownik ExtGState, ustawić zarówno przezroczystość obrysu, jak i wypełnienia oraz wybrać tryb mieszania — wszystko przy użyciu kilku przejrzystych linii kodu C#.

Zmiana przezroczystości PDF jest przydatna, gdy potrzebujesz znaków wodnych, nakładek graficznych lub subtelnych efektów wizualnych bez konieczności przebudowy całego dokumentu. Poradnik zakłada, że masz podstawowe środowisko C# oraz zainstalowaną bibliotekę Aspose.Pdf dla .NET.

![how to change PDF opacity using Aspose.Pdf in C#](https://example.com/og-image.png)

## Wymagania wstępne

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+)
* Licencjonowana kopia **Aspose.Pdf for .NET** (bezpłatna wersja próbna działa do testów)
* Plik PDF wejściowy znajdujący się w folderze, do którego możesz odwołać się w kodzie
* Visual Studio 2022 lub dowolny edytor C#, którego preferujesz

Nie są wymagane dodatkowe pakiety NuGet — Aspose.Pdf zawiera wszystkie typy użyte w tym samouczku.

## Zrozumienie stanu graficznego PDF

Strona PDF przechowuje parametry rysowania w obiekcie **graphics state**. Słownik **ExtGState** zawiera wpisy takie jak:

* **CA** – przezroczystość obrysu (0 = przezroczysty, 1 = nieprzezroczysty)
* **ca** – przezroczystość wypełnienia
* **BM** – tryb mieszania (np. *Normal*, *Multiply*, *Screen*)

Tworząc nowy słownik stanu graficznego i dodając go do kolekcji ExtGState strony, możesz odwoływać się do tego stanu później w strumieniach zawartości. Takie podejście unika przepisywania całej zawartości strony i działa z dowolnym istniejącym PDF.

## Jak zmienić przezroczystość PDF przy użyciu Aspose.Pdf

Poniższe sześć kroków obejmuje cały proces — od wczytania dokumentu po zapisanie zmodyfikowanego pliku. Każdy krok zawiera dokładny kod, którego potrzebujesz, oraz wyjaśnienie, dlaczego krok jest istotny.

### Krok 1: Wczytaj dokument PDF

```csharp
using Aspose.Pdf;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

**Dlaczego to jest ważne** — Otwieranie pliku przy użyciu `Aspose.Pdf.Document` daje pełny dostęp do wewnętrznej struktury PDF, w tym zasobów strony, w których znajduje się słownik **ExtGState**.

### Krok 2: Pobierz pierwszą stronę i jej słownik zasobów

```csharp
// Step 2: Get the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**Dlaczego to jest ważne** — Każda strona posiada słownik *Resources*, który grupuje czcionki, obrazy i stany graficzne. `DictionaryEditor` zapewnia wygodny dostęp do odczytu/zapisu tej kolekcji.

### Krok 3: Pobierz (lub utwórz) słownik ExtGState

```csharp
// Step 3: Retrieve the ExtGState dictionary from the page resources
// If ExtGState does not exist, create an empty one.
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**Dlaczego to jest ważne** — Niektóre pliki PDF już zawierają wpis **ExtGState**; inne nie. Logika warunkowa zapewnia, że samouczek działa w obu przypadkach, co czyni go odpornym na rzeczywiste pliki.

### Krok 4: Utwórz nowy słownik stanu graficznego i zdefiniuj wpisy przezroczystości

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

**Dlaczego to jest ważne** — Trzy kluczowe wpisy kontrolują sposób renderowania poleceń rysowania:

* `CA = 1.0` utrzymuje linie obrysu w pełni widoczne.
* `ca = 0.5` sprawia, że wypełnione kształty są półprzezroczyste.
* `BM = Normal` używa domyślnego trybu mieszania; możesz zamienić `"Normal"` na `"Multiply"` lub `"Screen"` dla kreatywnych efektów.

### Krok 5: Dodaj nowy stan graficzny do słownika ExtGState

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary (named "GS0")
extGStateDict.Add("GS0", graphicsStateDict);
```

**Dlaczego to jest ważne** — Nazwanie wpisu `"GS0"` tworzy odwołanie, które możesz później użyć w strumieniu zawartości (`/GS0 gs`). Jeśli potrzebujesz wielu wariantów przezroczystości, dodaj dodatkowe wpisy (`"GS1"`, `"GS2"`, …) z różnymi wartościami `CA`/`ca`.

### Krok 6: Zapisz zaktualizowany dokument PDF

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**Dlaczego to jest ważne** — Zapisanie zmian zapisuje zmodyfikowany słownik **ExtGState** z powrotem do pliku. Powstały PDF zawiera teraz wielokrotnie używalny stan graficzny, który może wywołać dowolne polecenie rysujące.

## Zastosowanie nowego stanu graficznego w treści strony

Powyższe kroki jedynie tworzą stan graficzny; musisz go jeszcze odwołać w strumieniu zawartości strony. Oto szybki przykład rysujący półprzezroczysty prostokąt przy użyciu właśnie dodanego stanu:

```csharp
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    var page = pdfDocument.Pages[1];
    var content = new PageContentEditor(page);
    // Begin the graphics state GS0
    content.InsertContent(0, "q /GS0 gs\n"); // Save graphics state and apply GS0
    // Draw a rectangle (100,100) to (300,300)
    content.InsertContent(0, "0.2 0.6 0.8 rg\n"); // Set fill color (light blue)
    content.InsertContent(0, "100 100 200 200 re\n");
    content.InsertContent(0, "f\n"); // Fill rectangle with current fill opacity
    // Restore graphics state
    content.InsertContent(0, "Q\n");
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**Wyjaśnienie** — Operator `q` zapisuje bieżący stan graficzny, `/GS0 gs` stosuje ustawienia przezroczystości, prostokąt jest rysowany, a `Q` przywraca pierwotny stan. Ten fragment możesz umieścić w dowolnym miejscu na stronie, przed lub po istniejącej treści, w zależności od potrzebnej warstwy wizualnej.

## Częste pułapki i jak ich uniknąć

| Objaw | Przyczyna | Rozwiązanie |
|-------|-----------|-------------|
| Przezroczystość nie zmienia się | Strona nie ma wpisu ExtGState lub zawartość nie odwołuje się do nowego stanu. | Sprawdź, czy `ExtGState` istnieje i czy strumień zawartości zawiera `/GS0 gs` (lub wybraną nazwę). |
| Tryb mieszania nie działa | Użycie niekompatybilnej przestrzeni kolorów lub wersji PDF. | Upewnij się, że wersja PDF jest co najmniej 1.4 (wymagana dla przezroczystości) i że nie mieszasz kolorów spot z trybami mieszania. |
| Dokument nie otwiera się w starszych przeglądarkach | Przezroczystość nie jest obsługiwana w PDF 1.3 lub starszych. | Ustaw `pdfDocument.Version = 1.4;` przed zapisem lub jawnie zaktualizuj wersję PDF. |

## Testowanie wyniku

Otwórz `output.pdf` w Adobe Acrobat Reader, Foxit lub dowolnym nowoczesnym przeglądarce PDF. Powinieneś zobaczyć prostokąt renderowany z 50 % przezroczystością wypełnienia, podczas gdy jego obramowanie pozostaje w pełni nieprzezroczyste. Użyj opcji *Edit → Preferences → Accessibility*, aby przełączyć „Use high‑contrast colors” i potwierdzić, że efekt półprzezroczysty pozostaje.

Jeśli potrzebujesz zweryfikować programowo, Aspose.Pdf pozwala odczytać stan graficzny:

```csharp
var gs = pdfDocument.Pages[1].Resources["ExtGState"]["GS0"].ToCosPdfDictionary();
var fillOpacity = ((CosPdfNumber)gs["ca"]).Value; // Should be 0.5
```

## Rozszerzanie techniki

* **Wiele poziomów przezroczystości** — Dodaj więcej wpisów (`"GS1"`, `"GS2"`) z różnymi wartościami `ca` i odwołuj się do nich w potrzebnych miejscach.
* **Różne tryby mieszania** — Zamień `"Normal"` na `"Multiply"` lub `"Screen"` aby uzyskać artystyczne nakładki.
* **Zastosowanie do obrazów** — Użyj tego samego stanu graficznego przed operatorem `Do`, który rysuje obraz XObject.

Te warianty pozwalają tworzyć znaki wodne, podświetlać sekcje lub tworzyć złożone projekty wizualne bez rasteryzacji PDF.

## Podsumowanie

Teraz wiesz **jak zmienić przezroczystość PDF** w C# przy użyciu Aspose.Pdf. Tworząc własny stan graficzny, dodając go do słownika ExtGState strony i wywołując stan w strumieniu zawartości, uzyskujesz precyzyjną kontrolę nad przezroczystością obrysu i wypełnienia oraz trybami mieszania. Pełny przykład jest gotowy do skopiowania, uruchomienia i dostosowania do dowolnego scenariusza manipulacji PDF.

Gotowy na kolejne wyzwanie? Spróbuj połączyć tę technikę z **Aspose.Pdf opacity** na obrazach lub zbadaj efekty **PDF blend mode**, aby uzyskać profesjonalne nakładki. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Zmień przezroczystość PDF przy użyciu Aspose.PDF – Kompletny przewodnik C#](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Zmień przezroczystość PDF w C# przy użyciu Aspose.Pdf – przewodnik krok po kroku](/pdf/english/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/)
- [Jak zmienić przezroczystość PDF w C# przy użyciu Aspose.Pdf](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}