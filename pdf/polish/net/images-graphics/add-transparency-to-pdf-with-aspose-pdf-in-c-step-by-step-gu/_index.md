---
category: general
date: 2026-03-19
description: Dodaj przezroczystość do PDF przy użyciu Aspose.PDF dla C#. Dowiedz się,
  jak ustawić krycie, tryb mieszania i ExtGState w zaledwie kilku linijkach kodu.
draft: false
keywords:
- add transparency to pdf
- Aspose PDF transparency
- C# PDF graphics state
- PDF blend mode
- set PDF opacity
language: pl
og_description: Szybko dodaj przezroczystość do pliku PDF. Ten przewodnik pokazuje,
  jak kontrolować krycie i tryb mieszania przy użyciu Aspose.PDF w C#.
og_title: Dodaj przezroczystość do PDF za pomocą Aspose PDF – Kompletny samouczek
  C#
tags:
- Aspose.PDF
- C#
title: Dodaj przezroczystość do PDF za pomocą Aspose PDF w C# – Przewodnik krok po
  kroku
url: /pl/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj przezroczystość do PDF przy użyciu Aspose PDF w C# – Kompletny tutorial

Zastanawiałeś się kiedyś, **jak dodać przezroczystość do plików PDF** bez walki z niskopoziomową składnią PDF? Nie jesteś sam. Wielu programistów potrzebuje szybkiego sposobu na uczynienie kształtów lub tekstu półprzezroczystymi — pomyśl o znakach wodnych, nakładkach graficznych lub subtelnym wskazaniu UI wewnątrz dokumentu.  

W tym przewodniku przejdziemy przez **kompletny, gotowy do uruchomienia przykład**, który pokazuje dokładnie, jak ustawić przezroczystość wypełnienia, przezroczystość obrysu i tryb mieszania przy użyciu Aspose.PDF dla .NET. Po zakończeniu będziesz mieć PDF, w którym prostokąt wyświetla się z 50 % przezroczystością, oraz zrozumiesz, dlaczego słownik ExtGState jest kluczem do osiągnięcia tego efektu.

Omówimy wszystko, co potrzebne: wymagany pakiet NuGet, sam kod, wyjaśnienia każdej linii oraz kilka wskazówek dotyczących przypadków brzegowych, takich jak starsze przeglądarki PDF. Bez odwołań zewnętrznych — tylko samodzielne rozwiązanie, które możesz skopiować‑wkleić i uruchomić już dziś.

## Co będzie potrzebne

- **Aspose.PDF for .NET** (v23.12 lub nowszy). Instalacja przez NuGet: `Install-Package Aspose.PDF`.
- Środowisko programistyczne .NET (Visual Studio, Rider lub `dotnet` CLI).
- Przykładowy plik PDF o nazwie `input.pdf` umieszczony w katalogu, którym zarządzasz (tutorial używa `YOUR_DIRECTORY/` jako symbolu zastępczego).

To wszystko. Jeśli masz już te elementy, przejdźmy do działania.

## Dodaj przezroczystość do PDF – przegląd

Sednem nadania przezroczystości w PDF jest **stan graficzny** (`ExtGState`). Dodając własny obiekt stanu graficznego do słownika zasobów strony, możesz określić:

| Właściwość | Znaczenie |
|------------|-----------|
| `ca` | Przezroczystość wypełnienia (0 = całkowicie przezroczyste, 1 = nieprzezroczyste). |
| `CA` | Przezroczystość obrysu (ta sama skala). |
| `BM` | Tryb mieszania (np. `Normal`, `Multiply`). |

Utworzymy nowy stan graficzny, wstawimy go do słownika `ExtGState` strony, a następnie odwołamy się do niego przy rysowaniu. Poniższy fragment kodu robi dokładnie to.

![add transparency to pdf diagram](add_transparency_to_pdf.png){alt="dodaj przezroczystość do pdf"}

## Krok 1: Konfiguracja projektu i wczytanie PDF

Najpierw tworzymy prostą aplikację konsolową (lub dowolny projekt C#) i wczytujemy źródłowy PDF.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;          // For low‑level PDF operators
using Aspose.Pdf.Text;               // Optional, if you want to add text later
using Aspose.Pdf.XObjects;          // For image handling, not needed here

// Define the folder that contains the PDF file
string inputDir = @"YOUR_DIRECTORY/";

// Load the PDF document
using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
{
    // All subsequent steps go inside this using block
```

**Dlaczego to ważne:**  
`Document` jest punktem wejścia do każdej manipulacji PDF przy użyciu Aspose. Umieszczenie go w instrukcji `using` zapewnia prawidłowe zwolnienie wszystkich zasobów przy zapisywaniu pliku później.

## Krok 2: Dostęp do pierwszej strony i jej zasobów

Potrzebujemy słownika zasobów pierwszej strony, ponieważ właśnie tam znajduje się kolekcja `ExtGState`.

```csharp
    // Grab the first page (pages are 1‑based in Aspose)
    Page firstPage = pdfDocument.Pages[1];

    // Helper to edit dictionaries (resources, etc.)
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);

    // Retrieve the existing ExtGState dictionary, or create a new one if missing
    CosPdfDictionary extGStateDict;
    if (resourcesEditor.ContainsKey("ExtGState"))
    {
        extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
    }
    else
    {
        extGStateDict = new CosPdfDictionary(pdfDocument);
        resourcesEditor.Add("ExtGState", extGStateDict);
    }
```

**Wyjaśnienie:**  
Jeśli strona już posiada wpis `ExtGState`, używamy go ponownie; w przeciwnym razie tworzymy nowy słownik. Takie podejście zapobiega błędom typu null‑reference przy pracy z PDF‑ami, które nie mają żadnych stanów graficznych.

## Krok 3: Utworzenie nowego stanu graficznego z żądaną przezroczystością

Teraz definiujemy rzeczywiste wartości przezroczystości.

```csharp
    // Create an empty dictionary that will represent our new graphics state
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Stroke opacity – fully opaque (1.0)
    newGraphicsState.Add("CA", new CosPdfNumber(1));

    // Fill opacity – 50 % transparent (0.5)
    newGraphicsState.Add("ca", new CosPdfNumber(0.5));

    // Blend mode – Normal is the default, but you can experiment with Multiply, Screen, etc.
    newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**Dlaczego te klucze?**  
- `CA` kontroluje przezroczystość obrysów (linie, krawędzie).  
- `ca` kontroluje przezroczystość wypełnień (stałe kształty, tekst).  
- `BM` wybiera sposób, w jaki przezroczysty obiekt miesza się z zawartością pod spodem. Użycie `"Normal"` zapewnia przewidywalny wynik wizualny we wszystkich przeglądarkach.

## Krok 4: Zarejestrowanie stanu graficznego w zasobach strony

Nadajemy naszemu stanowi graficznemu nazwę (`GS0`) i dodajemy go do słownika `ExtGState`.

```csharp
    // Add the graphics state to the ExtGState dictionary with a unique name
    extGStateDict.Add("GS0", newGraphicsState);
```

**Wskazówka:**  
Jeśli potrzebujesz wielu przezroczystych obiektów o różnych poziomach przezroczystości, utwórz dodatkowe wpisy (`GS1`, `GS2`, …) i odpowiednio dostosuj wartości `ca`/`CA`.

## Krok 5: Narysowanie przezroczystego prostokąta przy użyciu nowego stanu graficznego

Po skonfigurowaniu stanu graficznego możemy narysować coś, co rzeczywiście go wykorzystuje. Poniżej dodajemy półprzezroczysty niebieski prostokąt do strony.

```csharp
    // Prepare a content stream for the page (adds to existing content)
    var canvas = new Aspose.Pdf.Drawing.Graphic(firstPage);

    // Set the graphics state we just created
    canvas.SetGraphicsState("GS0");

    // Choose a fill color (blue) and draw the rectangle
    canvas.SetColor(new Aspose.Pdf.Drawing.Color(0, 0, 255)); // RGB blue
    canvas.Rectangle(100, 500, 200, 100); // x, y, width, height

    // Close the canvas to flush commands
    canvas.Close();
```

**Co zobaczysz:**  
Po otwarciu wygenerowanego PDF, niebieski prostokąt pojawi się w określonym miejscu, ale zawartość strony pod nim będzie nadal widoczna, ponieważ przezroczystość wypełnienia wynosi 0,5. Jeśli przeanalizujesz PDF narzędziem takim jak „Edit PDF” w Adobe Acrobat, zobaczysz obiekt `ExtGState` (`GS0`) powiązany z tym prostokątem.

## Krok 6: Zapisz zaktualizowany PDF

Na koniec zapisujemy zmodyfikowany dokument na dysku.

```csharp
    // Save the document with a new name so the original stays untouched
    pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
}
```

To cały przepływ pracy. Uruchom aplikację konsolową, otwórz `ExtGStateAdded.pdf` i sprawdź przezroczystą nakładkę.

---

## Pełny działający przykład (Gotowy do kopiowania)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddTransparencyDemo
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF file
        string inputDir = @"YOUR_DIRECTORY/";

        // Step 2: Load the PDF document
        using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
        {
            // Step 3: Get the first page and its resource dictionary
            Page firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", extGStateDict);
            }

            // Step 4: Create a new graphics state with opacity and blend mode settings
            CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity (fully opaque)
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));       // fill opacity (50% transparent)
            newGraphicsState.Add("BM", new CosPdfName("Normal"));   // blend mode

            // Step 5: Add the new graphics state to the page resources
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 6: Draw a rectangle using the new graphics state
            var canvas = new Graphic(firstPage);
            canvas.SetGraphicsState("GS0");
            canvas.SetColor(new Color(0, 0, 255)); // blue fill
            canvas.Rectangle(100, 500, 200, 100);
            canvas.Close();

            // Step 7: Save the updated PDF document
            pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
        }

        Console.WriteLine("PDF with transparency created successfully.");
    }
}
```

**Oczekiwany rezultat:**  
Otwarcie `ExtGStateAdded.pdf` pokazuje niebieski prostokąt w pozycji (100, 500) z 50 % przezroczystością wypełnienia. Pod prostokątem pozostaje widoczny wszelki istniejący tekst lub obrazy.

---

## Najczęściej zadawane pytania i przypadki brzegowe

### Czy to działa w starszych przeglądarkach PDF?
Większość nowoczesnych przeglądarek (Adobe Reader, Foxit, Chrome) obsługuje podstawowe klucze `ca`/`CA`. Bardzo stare czytniki mogą je zignorować i renderować kształt jako w pełni nieprzezroczysty.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}