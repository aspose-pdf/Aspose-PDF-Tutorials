---
category: general
date: 2026-10-07
description: Dodaj stan graficzny PDF przy użyciu Aspose.Pdf w C#, aby zmodyfikować
  przezroczystość PDF. Postępuj zgodnie z tym przewodnikiem krok po kroku, aby osadzić
  niestandardowe stany graficzne i kontrolować krycie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: pl
lastmod: 2026-10-07
og_description: Dodaj stan graficzny PDF przy użyciu Aspose.Pdf w C#. Dowiedz się,
  jak zmodyfikować przezroczystość PDF, tworząc niestandardowy słownik stanu graficznego.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Dodaj stan graficzny PDF przy użyciu Aspose.Pdf – kontroluj przezroczystość
  PDF
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Dodaj stan graficzny PDF przy użyciu Aspose.Pdf w C#
url: /pl/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj stan graficzny PDF przy użyciu Aspose.Pdf w C#

Jeśli potrzebujesz **add graphics state pdf** do dokumentu, ten tutorial pokazuje dokładnie, jak to zrobić przy użyciu Aspose.Pdf dla .NET. Po zakończeniu przewodnika będziesz także wiedział, jak **modify PDF transparency**, umożliwiając ustawienie własnych wartości nieprzezroczystości dla dowolnej operacji rysowania.

Praca ze stanami graficznymi PDF pozwala kontrolować takie parametry jak szerokość linii, tryb mieszania i, co najważniejsze w tym artykule, przezroczystość treści. Poniższe kroki są przeznaczone dla programistów, którzy czują się komfortowo w C# i chcą gotowe rozwiązanie, które można od razu uruchomić, bez przeszukiwania oficjalnej dokumentacji SDK.

## Czego się nauczysz

* Jak utworzyć nowy słownik stanu graficznego i wypełnić go wpisami `CA`, `ca` i `BM`.  
* Jak wstawić ten słownik do zasobu `ExtGState` strony, aby PDF go rozpoznał.  
* Jak wartości `ca` (obrys) i `CA` (wypełnienie) wpływają na **modify PDF transparency** dla kolejnych poleceń rysowania.  
* Typowe pułapki, takie jak kolizje nazw i kompatybilność wersji, plus profesjonalne wskazówki dotyczące późniejszego rozszerzania stanu graficznego.

**Wymagania wstępne**

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+).  
* Ważna licencja Aspose.Pdf dla .NET (darmowa wersja ewaluacyjna działa do testów).  
* Visual Studio 2022 lub dowolne IDE C#, które preferujesz.

---

## Krok 1: Zainstaluj Aspose.Pdf dla .NET

Add the NuGet package to your project:

```bash
dotnet add package Aspose.Pdf
```

Pakiet zawiera przestrzeń nazw `Aspose.Pdf`, która udostępnia klasy `Document`, `DictionaryEditor` i `CosPdfDictionary` używane później.

> **Wskazówka:** Jeśli planujesz przetwarzać wiele plików PDF w partii, włącz **License** wcześnie w `Program.cs`, aby uniknąć znaku wodnego wersji ewaluacyjnej.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Krok 2: Zdefiniuj ścieżki wejścia i wyjścia

Musisz wskazać SDK istniejący plik PDF (`input.pdf`) i określić, gdzie zostanie zapisany zmodyfikowany plik (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Dlaczego to ważne:** Używanie ścieżek bezwzględnych zapobiega, aby SDK szukało w niewłaściwym katalogu roboczym, co jest częstą przyczyną `FileNotFoundException`.

## Krok 3: Otwórz PDF i zlokalizuj zasoby pierwszej strony

Słownik `ExtGState` znajduje się wewnątrz słownika zasobów każdej strony. Dla uproszczenia edytujemy pierwszą stronę, ale to samo podejście działa dla dowolnego indeksu strony.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Przypadek brzegowy:** Jeśli strona nie ma wpisu `ExtGState`, musisz go utworzyć:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Krok 4: Zbuduj nowy słownik stanu graficznego

Stan graficzny to zbiór par klucz/wartość opisujących zachowanie operacji rysowania. Do przezroczystości potrzebujemy trzech kluczy:

| Klucz | Znaczenie | Typowa wartość |
|-----|---------|---------------|
| `CA` | Nieprzezroczystość wypełnienia (0 = przezroczysty, 1 = nieprzezroczysty) | `1` (w pełni nieprzezroczysty) |
| `ca` | Nieprzezroczystość obrysu (ta sama skala) | `0.5` (50 % przezroczysty) |
| `BM` | Tryb mieszania (np. `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Dlaczego te wartości?**  
`ca = 0.5` sprawia, że każdy obrysowany kształt (linie, obramowania) jest wyświetlany z 50 % nieprzezroczystością, podczas gdy `CA = 1` pozostawia wypełnione kształty w pełni nieprzezroczyste. Dostosuj obie liczby, aby uzyskać dokładny efekt **modify PDF transparency**, którego potrzebujesz.

## Krok 5: Wstaw stan graficzny do słownika ExtGState

Musisz nadać nowemu stanowi unikalną nazwę (np. `GS0`). Jeśli nazwa już istnieje, Aspose.Pdf nadpisze istniejący wpis, co może zepsuć inne treści, które na nim polegają.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Teraz zasoby strony wiedzą o `GS0`. Aby faktycznie go użyć, odwołałbyś się do stanu graficznego w strumieniu zawartości za pomocą operatora `gs` (np. `GS0 gs`). Aspose.Pdf pozwala wstrzykiwać surowe operatory PDF, jeśli potrzebujesz rysować własne kształty.

## Krok 6: Zapisz zmodyfikowany PDF

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

Wynikowy `output.pdf` zawiera taką samą treść wizualną jak oryginał, ale wszelkie kolejne polecenia rysowania, które wybiorą `GS0`, będą respektować zdefiniowane ustawienia przezroczystości.

### Oczekiwany rezultat

Otwórz `output.pdf` w Adobe Acrobat lub dowolnym przeglądarce PDF. Jeśli dodasz nową linię obrysowaną przy użyciu stanu graficznego `GS0` (np. poprzez `pdfDocument.Pages[1].Contents.Add(...)`), linia będzie wyglądać półprzezroczysto, podczas gdy wypełnienia pozostaną nieprzezroczyste. To pokazuje, że pomyślnie **add graphics state pdf** i **modify PDF transparency**.

---

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do aplikacji konsolowej. Zawiera ładowanie licencji, obsługę błędów oraz komentarze wyjaśniające każdy nieoczywisty krok.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## Co powinieneś się nauczyć dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Dodaj przezroczystość do PDF przy użyciu Aspose PDF w C# – przewodnik krok po kroku](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Dodaj przezroczystość do PDF przy użyciu Aspose – kompletny przewodnik C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Jak dodać znak wodny obrazu do PDF przy użyciu Aspose.PDF dla .NET: Kompletny przewodnik](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}