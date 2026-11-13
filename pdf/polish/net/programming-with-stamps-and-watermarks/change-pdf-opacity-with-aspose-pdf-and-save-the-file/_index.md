---
category: general
date: 2026-11-12
description: Dowiedz się, jak zmienić przezroczystość PDF przy użyciu Aspose.Pdf,
  dodać przezroczystość, ustawić tryb mieszania oraz zapisać zmodyfikowany PDF w C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: pl
lastmod: 2026-11-12
og_description: Zmieniaj przezroczystość PDF za pomocą Aspose.Pdf, dowiedz się, jak
  dodać przezroczystość, ustawić tryb mieszania i zapisać zmodyfikowane pliki PDF
  w C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Zmieniaj przezroczystość PDF przy użyciu Aspose.Pdf – dodaj przezroczystość
  i zapisz
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Zmień przezroczystość PDF za pomocą Aspose.Pdf i zapisz plik
url: /pl/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zmieniaj przezroczystość PDF przy użyciu Aspose.Pdf i zapisz plik

Jeśli potrzebujesz **zmienić przezroczystość PDF** w dokumencie, Aspose.Pdf udostępnia prosty interfejs API pozwalający dostosować zarówno przezroczystość linii (stroke), jak i wypełnienia. Ten tutorial pokazuje dokładnie **jak dodać przezroczystość**, **jak ustawić tryb mieszania** oraz **zapisz zmodyfikowane pliki PDF** przy użyciu kilku linii kodu C#.

Przejdziesz przez każdy krok — od załadowania istniejącego PDF po zdefiniowanie nowego stanu graficznego i zapisanie zmian. Po zakończeniu tego przewodnika będziesz mógł:

* Zmniejszyć widoczność grafiki wektorowej lub obrazów.
* Zastosować niestandardowy tryb mieszania, taki jak *Normal* lub *Multiply*.
* Wyeksportować zaktualizowany plik bez utraty pozostałej zawartości.

Jedynym wymogiem wstępnym jest działające środowisko programistyczne .NET oraz odwołanie do biblioteki Aspose.Pdf (wersja 23.9 lub nowsza). Nie są wymagane żadne zewnętrzne narzędzia.

## Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| .NET 6.0 SDK lub nowszy | Gwarantuje kompatybilność z najnowszymi API Aspose.Pdf. |
| Pakiet NuGet Aspose.Pdf dla .NET | Dostarcza klasy `Document`, `CosPdfDictionary` i powiązane klasy używane w kodzie. |
| Plik PDF do edycji (np. `input.pdf`) | Służy jako źródło do zmian przezroczystości. |

Install the NuGet package with:

```bash
dotnet add package Aspose.Pdf
```

## Zmieniaj przezroczystość PDF przy użyciu Aspose.Pdf

### Krok 1: Załaduj dokument PDF

Rozpocznij od utworzenia instancji `Document`, która wskazuje na Twój plik źródłowy. Konstruktor wczytuje cały PDF do pamięci, umożliwiając manipulację jego wewnętrznymi obiektami.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Dlaczego ten krok?** Ładowanie pliku tworzy manipulowalny model obiektowy. Wszystkie późniejsze zmiany działają na tej reprezentacji w pamięci, zapewniając, że oryginalny plik pozostaje nienaruszony, dopóki nie zapiszesz go wyraźnie.

### Krok 2: Uzyskaj dostęp do zasobów pierwszej strony

Każda strona PDF przechowuje *słownik zasobów*, który zawiera obiekty takie jak czcionki, obrazy i stany graficzne. Musisz edytować ten słownik, aby wstawić nowy wpis `ExtGState`.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Wskazówka:** Jeśli Twój PDF zawiera wiele stron, które wymagają tej samej przezroczystości, powtórz ten krok dla każdej strony lub udostępnij pojedynczy `ExtGState` między stronami.

### Krok 3: Upewnij się, że słownik ExtGState istnieje

`ExtGState` to słownik przechowujący niestandardowe stany graficzne. Jeśli nie istnieje, kod tworzy go automatycznie.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Dlaczego ten krok?** Bez kontenera `ExtGState` każda próba odwołania się do nowego stanu graficznego zakończy się niepowodzeniem, co spowoduje, że PDF zignoruje ustawienia przezroczystości.

### Krok 4: Zdefiniuj nowy stan graficzny (ExtGState)

Stan graficzny definiuje, jak zachowują się operacje rysowania. Poniższy słownik ustawia przezroczystość linii (`CA`), przezroczystość wypełnienia (`ca`) oraz tryb mieszania (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Jak ustawić przezroczystość wypełnienia:** Wpis `ca` kontroluje przezroczystość wypełnionych kształtów (tekst, ścieżki). Dostosuj wartość liczbową pomiędzy `0` (całkowicie przezroczyste) a `1` (całkowicie nieprzezroczyste) zgodnie z wymaganiami projektu.  
> **Jak ustawić tryb mieszania:** Wpis `BM` wybiera algorytm kompozycji. Typowe wartości to `Normal`, `Multiply`, `Screen` i `Overlay`. Wybierz tę, która odpowiada Twoim zamierzeniom wizualnym.

### Krok 5: Zarejestruj stan graficzny w słowniku zasobów

Nadaj nowemu stanowi nazwę (np. `GS0`) i dodaj go do słownika `ExtGState`. Ta nazwa będzie później odwoływana w strumieniu zawartości strony.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Profesjonalna wskazówka:** Używaj konwencji nazewnictwa takiej jak `GS0`, `GS1`, … przy tworzeniu wielu stanów. Zapobiega to kolizjom nazw i ułatwia debugowanie.

### Krok 6: Zastosuj stan graficzny do zawartości strony

Aby rzeczywiście zobaczyć efekt przezroczystości, wstaw operator `/GS0 gs` przed poleceniami rysowania, które chcesz objąć. Poniższy przykład rysuje półprzezroczysty prostokąt.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Dlaczego operatory `q` i `Q`?** Dodają i usuwają stan graficzny ze stosu, zapewniając, że zmiana przezroczystości wpływa tylko na prostokąt, a nie na resztę strony.

### Krok 7: Zapisz zmodyfikowany PDF

Na koniec zapisz zaktualizowany dokument na dysku. Metoda `Save` nadpisuje docelowy plik lub tworzy nowy, jeśli nie istnieje.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Jak zapisać zmodyfikowany PDF:** Wywołanie `Save` zapisuje wszystkie modyfikacje w pamięci, w tym nowy `ExtGState`, do określonej ścieżki. Możesz także przesłać wynik do `MemoryStream` w odpowiedziach sieciowych.

## Pełny działający przykład

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zapisać zmodyfikowany PDF przy użyciu Aspose.Pdf i dodać przezroczystość](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Jak dodać przezroczystość do PDF przy użyciu Aspose.PDF w C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Jak dodać stan graficzny do PDF i kontrolować przezroczystość przy użyciu Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}