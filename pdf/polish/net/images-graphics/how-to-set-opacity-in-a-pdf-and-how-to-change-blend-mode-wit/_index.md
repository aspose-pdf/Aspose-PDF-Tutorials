---
category: general
date: 2026-11-19
description: Dowiedz się, jak ustawić przezroczystość i zmienić tryb mieszania w pliku
  PDF przy użyciu Aspose.Pdf. Przewodnik krok po kroku w C# dotyczący grafiki transparentnej.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set opacity
- how to change blend
- Aspose.Pdf graphics state
- PDF transparency C#
- modify PDF resources
language: pl
lastmod: 2026-11-19
og_description: Jak ustawić przezroczystość i zmienić tryb mieszania w pliku PDF przy
  użyciu Aspose.Pdf. Przejdź przez ten kompletny samouczek C#, aby uczynić grafikę
  przezroczystą.
og_image_alt: Code editor showing C# example that sets PDF opacity and blend mode
og_title: Jak ustawić przezroczystość i zmienić tryb mieszania w pliku PDF przy użyciu
  Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to set opacity and how to change blend mode in a PDF using
    Aspose.Pdf. Step‑by‑step C# guide for transparent graphics.
  headline: How to set opacity in a PDF and how to change blend mode with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Jak ustawić przezroczystość w PDF i jak zmienić tryb mieszania przy użyciu
  Aspose.Pdf
url: /pl/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić przezroczystość i jak zmienić tryb mieszania w PDF przy użyciu Aspose.Pdf

Jeśli potrzebujesz **jak ustawić przezroczystość** dla obiektów w PDF, ten przewodnik pokazuje dokładne kroki. Zawiera również informacje o **jak zmienić tryb mieszania**, aby nowy stan graficzny mieszał się poprawnie z zawartością strony.

W tym samouczku:

* Wczytać istniejący PDF przy użyciu Aspose.Pdf.
* Uzyskać dostęp do słownika zasobów strony.
* Utworzyć nowy słownik stanu graficznego definiujący przezroczystość linii, wypełnienia oraz tryb mieszania.
* Dodać stan graficzny do kolekcji `ExtGState`.
* Zapisz zaktualizowany PDF.

Nie są wymagane żadne zewnętrzne narzędzia — wystarczy biblioteka Aspose.Pdf for .NET oraz środowisko programistyczne .NET.

## Prerequisites

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+).
* Pakiet NuGet Aspose.Pdf dla .NET (`Install-Package Aspose.Pdf`).
* Plik PDF o nazwie `input.pdf` znajdujący się w zapisywalnym folderze (zastąp `YOUR_DIRECTORY` swoją rzeczywistą ścieżką).

## Step 1: Install Aspose.Pdf and set up the project

Utwórz nowy projekt konsolowy i dodaj odwołanie do Aspose.Pdf:

```bash
dotnet new console -n PdfOpacityDemo
cd PdfOpacityDemo
dotnet add package Aspose.Pdf
```

Plik projektu zawiera teraz zestaw Aspose.Pdf, który udostępnia klasy `Document`, `DictionaryEditor` i `CosPdfDictionary` używane później.

## Step 2: Load the PDF document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

// Load the existing PDF
Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

**Why this matters:** Ładowanie dokumentu tworzy reprezentację w pamięci, którą możesz modyfikować. Bez tego kroku słowniki zasobów są niedostępne.

## Step 3: Get the first page and its resource dictionary

```csharp
// Retrieve the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Open the page’s resource dictionary for editing
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);
```

**Explanation:** Słownik `Resources` zawiera obiekty takie jak czcionki, obrazy i kolekcję `ExtGState`. Edycja go pozwala wstrzyknąć nowe stany graficzne kontrolujące przezroczystość i mieszanie.

## Step 4: Access (or create) the ExtGState dictionary

```csharp
// Try to get the existing ExtGState dictionary; create it if missing
CosPdfDictionary extGStateDict = null;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and add it to resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourceEditor["ExtGState"] = extGStateDict;
}
```

**Why this step is needed:** Wpis `ExtGState` przechowuje obiekty stanu graficznego. Jeśli nie istnieje, musisz go utworzyć przed dodaniem nowych wpisów.

## Step 5: Create a new graphics state with opacity and blend mode

```csharp
// Create a new empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Set stroke opacity (CA) – 1 = fully opaque, 0 = fully transparent
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Set fill opacity (ca) – 0.5 = 50 % transparent fill
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Set blend mode (BM) – "Normal" is the default; other options: Multiply, Screen, Overlay, etc.
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**How this solves the problem:**  
* `CA` kontroluje przezroczystość ścieżek rysowanych (np. linii).  
* `ca` kontroluje przezroczystość wypełnionych kształtów (np. prostokątów).  
* `BM` określa, jak nowe elementy graficzne są kompozytowane z istniejącą zawartością strony. Zmiana trybu mieszania to dokładnie **jak zmienić tryb mieszania** w PDF.

## Step 6: Register the graphics state in the ExtGState collection

```csharp
// Use a unique key for the new graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

Teraz strona może odwoływać się do tego stanu graficznego pod nazwą `/GS0`. Każdy strumień zawartości, który ustawi `/GS0 gs`, użyje zdefiniowanej przezroczystości i trybu mieszania.

## Step 7: Apply the graphics state to existing content (optional)

Jeśli chcesz zmodyfikować istniejące polecenia rysowania, możesz dodać operator stanu graficznego na początek strumienia zawartości strony:

```csharp
// Retrieve the content stream as a string
string pageContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string modifiedContent = "GS0 gs\n" + pageContent;

// Replace the original content
firstPage.Contents[1].Replace(modifiedContent);
```

**Note:** Ten krok jest opcjonalny. Jeśli później dodasz nowe polecenia rysowania, po prostu rozpocznij strumień od `GS0 gs`.

## Step 8: Save the modified PDF

```csharp
pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");
```

Wynikowy `out.pdf` zawiera stan graficzny, w którym przezroczystość wypełnienia wynosi 50 % i tryb mieszania to `Normal`. Każda zawartość używająca `/GS0 gs` zostanie wyrenderowana z określoną przezroczystością.

## Full working example

Poniżej pełny program, który możesz skopiować i wkleić do `Program.cs`, a następnie uruchomić:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

class Program
{
    static void Main()
    {
        // 1. Load the PDF document
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get the first page and its resource dictionary
        Page firstPage = pdfDocument.Pages[1];
        DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

        // 3. Access or create the ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourceEditor["ExtGState"] = extGStateDict;
        }

        // 4. Define a new graphics state with opacity and blend mode
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity (fully opaque)
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity (50 % transparent)
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode (Normal)

        // 5. Add the graphics state to ExtGState collection
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Apply the graphics state to existing page content
        if (firstPage.Contents.Count > 0)
        {
            string original = firstPage.Contents[1].ToString();
            string withGs = "GS0 gs\n" + original;
            firstPage.Contents[1].Replace(withGs);
        }

        // 7. Save the updated PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");

        Console.WriteLine("PDF updated successfully – opacity set and blend mode changed.");
    }
}
```

### Expected output

Uruchomienie programu wypisuje:

```
PDF updated successfully – opacity set and blend mode changed.
```

Po otwarciu `out.pdf` w przeglądarce PDF, każdy kształt korzystający z nowo zdefiniowanego stanu graficznego będzie wyświetlany z 50 % przezroczystością wypełnienia, podczas gdy obrysy pozostaną w pełni nieprzezroczyste. Tryb mieszania `Normal` zapewnia, że grafika jest kompozytowana bez specjalnych efektów. Możesz zmienić `"Normal"` na `"Multiply"` lub `"Screen"`, aby zobaczyć **jak zmienić tryb mieszania** dla różnych rezultatów wizualnych.

## Common questions and edge cases

| Pytanie | Odpowiedź |
|----------|--------|
| **Czy mogę ustawić różne wartości przezroczystości dla wielu obiektów?** | Tak. Utwórz dodatkowe stany graficzne (np. `GS1`, `GS2`) z różnymi wartościami `ca`/`CA` i odwołuj się do odpowiedniej nazwy przed rysowaniem każdego obiektu. |
| **Co jeśli PDF już zawiera wpis `ExtGState` o nazwie `GS0`?** | Wybierz unikalny klucz (`GS1`, `MyOpacityState` itp.) lub nadpisz istniejący wpis, jeśli stara definicja nie jest już potrzebna. |
| **Czy tryb mieszania jest ograniczony do `Normal`?** | Nie. Poprawne nazwy to m.in. `Multiply`, `Screen`, `Overlay`, `Darken`, `Lighten`, `ColorDodge`, `ColorBurn`, `HardLight`, `SoftLight`, `Difference`, `Exclusion`, a także `Hue`, `Saturation`, `Color`, `Luminosity`. |
| **Czy to działa z zaszyfrowanymi PDF‑ami?** | Aspose.Pdf może otworzyć zaszyfrowane PDF‑y, jeśli podasz hasło poprzez `Document(string, LoadOptions)`. Manipulacja stanem graficznym działa tak samo po odszyfrowaniu. |
| **Czy zmiany będą dotyczyć wszystkich stron?** | Przykład modyfikuje tylko pierwszą stronę. Aby wpłynąć na każdą stronę, przeiteruj `pdfDocument.Pages` i powtórz kroki 2‑6 dla każdej z nich. |

## Pro tips

* **Ponowne użycie stanów graficznych:** Dodanie stanu graficznego raz i odwoływanie się do niego na wielu stronach zmniejsza rozmiar pliku.
* **Wydajność:** Modyfikowanie dużych PDF‑ów w pamięci może być zasobo‑intensywne. Użyj `pdfDocument.Save(..., SaveOptions)` z aktualizacją przyrostową, jeśli potrzebujesz tylko niewielkich zmian.
* **Testowanie trybów mieszania:** Nie wszystkie przeglądarki PDF renderują każdy tryb mieszania identycznie. Przetestuj wynik w Adobe Acrobat Reader oraz alternatywnej przeglądarce (np. Foxit), aby zweryfikować spójność wizualną.

## Conclusion

Teraz wiesz **jak ustawić przezroczystość** i **jak zmienić tryb mieszania** w PDF przy użyciu Aspose.Pdf for .NET. Edytując słownik `ExtGState`, uzyskujesz precyzyjną kontrolę nad przezroczystością i kompozycją, co umożliwia tworzenie profesjonalnych grafik PDF bez zewnętrznych narzędzi.

Następnie możesz zbadać:

* Dodawanie obrazów z przezroczystym tłem (`jak ustawić przezroczystość` na obrazach).
* Tworzenie wielokrotnego użytku strumieni zawartości, które odwołują się do nowego stanu graficznego.
* Używanie innych trybów mieszania (`jak zmienić tryb mieszania` na `Multiply` lub `Screen`) dla efektów kreatywnych.

Miłego kodowania i ciesz się bardziej dynamicznymi wizualnie PDF‑ami!

## What Should You Learn Next?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zmienić przezroczystość w PDF przy użyciu Aspose.PDF – Kompletny przewodnik](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-change-opacity-in-pdf-with-aspose-pdf-complete-guide/)
- [Jak zmienić przezroczystość w PDF przy użyciu Aspose.Pdf dla .NET](/pdf/english/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/)
- [Jak zmienić przezroczystość PDF przy użyciu Aspose.Pdf w C#](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}