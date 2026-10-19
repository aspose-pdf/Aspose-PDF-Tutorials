---
category: general
date: 2026-09-05
description: Dowiedz się, jak dodać stan graficzny PDF przy użyciu Aspose.PDF, aby
  ustawić przezroczystość. Ten przewodnik krok po kroku pokazuje także, jak dodać
  przezroczystość do PDF i efektywnie modyfikować przezroczystość w PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- how to add transparency pdf
- modify pdf transparency
language: pl
lastmod: 2026-09-05
og_description: Dodaj stan graficzny PDF przy użyciu Aspose.PDF. Skorzystaj z tego
  przewodnika, aby dowiedzieć się, jak dodać przezroczystość do PDF i zmodyfikować
  przezroczystość PDF w kilku linijkach kodu C#.
og_image_alt: Screenshot of C# code that adds graphics state pdf to a PDF document
og_title: Dodaj stan graficzny PDF przy użyciu Aspose.PDF – kontroluj przezroczystość
  w C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to add graphics state pdf using Aspose.PDF to set transparency.
    This step‑by‑step guide also shows how to add transparency pdf and modify pdf
    transparency efficiently.
  headline: How to add graphics state pdf and control transparency with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- PDF graphics state
- PDF transparency
- C# PDF manipulation
title: Jak dodać stan graficzny PDF i kontrolować przezroczystość przy użyciu Aspose.PDF
url: /pl/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać stan graficzny PDF i kontrolować przezroczystość przy użyciu Aspose.PDF

Jeśli potrzebujesz **dodać stan graficzny PDF** do istniejącego dokumentu, ten przewodnik pokaże Ci dokładne kroki. Zobaczysz, jak dodać przezroczystość PDF przy użyciu Aspose.PDF dla .NET oraz jak modyfikować przezroczystość PDF bez naruszania pierwotnego układu.

W kolejnych sekcjach przejdziemy przez kompletny, działający przykład, wyjaśnimy, dlaczego każda linia ma znaczenie, i omówimy typowe pułapki. Po zakończeniu będziesz w stanie osadzić własne stany graficzne — takie jak wartości alfa dla obrysu i wypełnienia — na dowolnej stronie PDF.

## Wymagania wstępne

Zanim zaczniesz, upewnij się, że masz:

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+)
* Ważną licencję Aspose.PDF dla .NET lub tymczasowy klucz ewaluacyjny
* Visual Studio 2022 (lub dowolny edytor C#, którego używasz)
* Plik PDF wejściowy (`input.pdf`), do którego masz prawo modyfikacji

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Pdf`.

## Krok 1: Załaduj dokument PDF

Pierwszą operacją jest otwarcie źródłowego PDF. Aspose.PDF opakowuje plik w obiekt `Document`, który daje dostęp do stron, zasobów i struktur PDF niskiego poziomu.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.Xmp;

string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document inside a using block so resources are released automatically.
using (var doc = new Document(inputPath))
{
    // The rest of the code lives inside this block.
}
```

**Dlaczego to ważne:** Otwieranie pliku w instrukcji `using` zapewnia zamknięcie uchwytu pliku nawet w przypadku wystąpienia wyjątku. Obiekt `Document` ładuje również tabelę cross‑reference, co umożliwia późniejszą edycję słowników niskiego poziomu.

## Krok 2: Uzyskaj słownik zasobów pierwszej strony

Każda strona PDF posiada słownik *Resources*, w którym przechowywane są czcionki, XObjecty i stany graficzne (`ExtGState`). Aby wstrzyknąć nowy stan graficzny, najpierw pobieramy ten słownik.

```csharp
// Inside the using block
Page page = doc.Pages[1];                     // Get the first page (pages are 1‑based)
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

**Dlaczego to ważne:** `ExtGState` jest kluczem, pod którym przechowywane są obiekty stanu graficznego. Jeśli strona nie zawiera jeszcze wpisu `ExtGState`, Aspose.PDF automatycznie tworzy pusty słownik, więc kod działa w obu przypadkach.

## Krok 3: Utwórz nowy słownik stanu graficznego

Słownik stanu graficznego definiuje zachowanie operacji rysowania. Dla przezroczystości potrzebujemy `CA` (alpha obrysu), `ca` (alpha wypełnienia) oraz opcjonalnie trybu mieszania (`BM`). Poniższy kod buduje ten słownik.

```csharp
// Create an empty COS dictionary that will become our new graphics state.
CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);

// Define the entries we want: 1.0 stroke opacity, 0.5 fill opacity, Normal blend mode.
var entries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke alpha (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill alpha (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

foreach (var entry in entries)
{
    newGs.Add(entry);
}
```

**Dlaczego to ważne:**  
* `CA` kontroluje nieprzezroczystość ścieżek obrysowanych (linie, obramowania).  
* `ca` kontroluje nieprzezroczystość obiektów wypełnionych (kształty, tekst).  
* `BM` wybiera tryb mieszania; „Normal” jest najczęściej używany i działa we wszystkich przeglądarkach PDF.

### Przypadek brzegowy: brak wpisu `ExtGState`

Jeśli `page.Resources` nie zawiera słownika `ExtGState`, `dictEditor["ExtGState"]` zwróci `null`. W takiej sytuacji możesz utworzyć go ręcznie:

```csharp
if (extGState == null)
{
    extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
    dictEditor["ExtGState"] = extGState;
}
```

Dodanie tego zabezpieczenia sprawia, że tutorial jest odporny na PDF‑y, które nigdy wcześniej nie używały własnych stanów graficznych.

## Krok 4: Dodaj nowy stan graficzny do słownika zasobów

Teraz wiążemy świeżo utworzony słownik z nazwą (np. `GS0`). Strumienie zawartości mogą odwoływać się do tej nazwy, aby zastosować zdefiniowaną przezroczystość.

```csharp
// Register the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);
```

**Dlaczego to ważne:** Operatory treści PDF, takie jak `gs`, przełączają się na nazwany stan graficzny. Dodając `GS0`, umożliwiasz późniejszym strumieniom zawartości użycie ` /GS0 gs ` w celu aktywacji ustawień przezroczystości.

## Krok 5: (Opcjonalnie) Zastosuj stan graficzny do istniejącej zawartości

Jeśli chcesz, aby istniejące elementy bieżącej strony stały się przezroczyste, możesz dodać operator `gs` na początek strumienia zawartości strony. Ten krok jest opcjonalny, ponieważ wiele scenariuszy wymaga stanu graficznego jedynie dla nowo dodawanych obiektów.

```csharp
// Prepend "GS0" graphics state to the page’s content
page.Contents.Insert(0, new OperatorGraphicsState("GS0"));
```

**Dlaczego to ważne:** Bez tej linii strona zachowa pierwotny wygląd. Dodanie operatora zapewnia, że wszystko rysowane po nim dziedziczy nowe wartości nieprzezroczystości.

## Krok 6: Zapisz zmodyfikowany PDF

Na koniec zapisz zaktualizowany dokument na dysku. Możesz nadpisać oryginalny plik lub zapisać go w nowej lokalizacji.

```csharp
string outputPath = @"YOUR_DIRECTORY\output.pdf";
doc.Save(outputPath);
```

**Dlaczego to ważne:** `doc.Save` serializuje zmodyfikowaną tabelę cross‑reference, słowniki zasobów i nowe strumienie zawartości, tworząc prawidłowy PDF, który może otworzyć każdy czytnik.

## Pełny działający przykład

Łącząc wszystkie elementy, oto samodzielny program, który możesz skopiować, wkleić i uruchomić.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Xmp;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Cos;

class AddGraphicsStateExample
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        using (var doc = new Document(inputPath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Access the first page's resource dictionary
            // -----------------------------------------------------------------
            Page page = doc.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary();

            // Ensure ExtGState exists
            if (extGState == null)
            {
                extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
                dictEditor["ExtGState"] = extGState;
            }

            // -----------------------------------------------------------------
            // 3️⃣ Create a new graphics state (transparency settings)
            // -----------------------------------------------------------------
            CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries) newGs.Add(entry);

            // -----------------------------------------------------------------
            // 4️⃣ Register the graphics state as "GS0"
            // -----------------------------------------------------------------
            extGState.Add("GS0", newGs);

            // -----------------------------------------------------------------
            // 5️⃣ (Optional) Apply the graphics state to existing content
            // -----------------------------------------------------------------
            page.Contents.Insert(0, new OperatorGraphicsState("GS0"));

            // -----------------------------------------------------------------
            // 6️⃣ Save the modified PDF
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved with new graphics state at: {outputPath}");
        }
    }
}
```

### Oczekiwany wynik

Po uruchomieniu programu otwórz `output.pdf` w Adobe Acrobat Reader lub dowolnym przeglądarce PDF. Wszystkie wypełnione kształty (np. kolorowe prostokąty) na pierwszej stronie powinny mieć **50 % nieprzezroczystości**, podczas gdy obrysy pozostają w pełni nieprzezroczyste. Jeśli dodałeś opcjonalny operator `gs`, *cała* istniejąca zawartość na tej stronie odziedziczy tę samą przezroczystość.

## Częste pytania i rozwiązywanie problemów

| Pytanie | Odpowiedź |
|----------|-----------|
| **Czy mogę dodać więcej niż jeden stan graficzny?** | Tak. Utwórz dodatkowe słowniki (np. `GS1`, `GS2`) i odwołuj się do nich różnymi operatorami `gs`. |
| **Co jeśli PDF już używa nazwy takiej jak `GS0`?** | Wybierz unikalną nazwę (np. `MyGS`) lub sprawdź istniejące klucze za pomocą `extGState.Keys`. |
| **Czy to działa z zaszyfrowanymi PDF‑ami?** | Dokument musi być otwarty z poprawnym hasłem. Użyj `new Document(inputPath, new LoadOptions { Password = "pwd" })`. |
| **Czy zmiany wpłyną na inne strony?** | Nie. Stan graficzny jest dodawany do zasobów edytowanej strony. Aby wpłynąć na wszystkie strony, powtórz proces dla każdej z nich lub dodaj słownik do zasobów *na poziomie dokumentu*. |
| **Czy to ma wpływ na wydajność?** | Dodanie jednego stanu graficznego jest pomijalne. Duże PDF‑y z wieloma stronami mogą wymagać pętli, ale operacja pozostaje O(liczba stron). |

## Porady profesjonalne

* **Wykorzystuj ponownie stany graficzne:** Jeśli potrzebujesz tej samej przezroczystości na wielu stronach, dodaj słownik do zasobów *dokumentu* (`doc.Resources`) i odwołuj się do niego z każdej strony. To zmniejsza rozmiar pliku.
* **Tryby mieszania:** Eksperymentuj z innymi wartościami `BM`, takimi jak `Multiply`, `Screen` czy `Overlay`, aby uzyskać kreatywne efekty. Nie wszystkie przeglądarki obsługują każdy tryb, więc testuj je z docelową grupą odbiorców.
* **Testowanie:** Zawsze porównuj oryginalny i zmodyfikowany PDF obok siebie. Użyj narzędzia do porównywania PDF, takiego jak `DiffPDF`, aby zweryfikować, że zmiany dotyczą tylko zamierzonych elementów.

## Kolejne kroki

Teraz, gdy wiesz **jak dodać przezroczystość PDF** i **modyfikować przezroczystość PDF**, możesz zgłębiać powiązane tematy:

* **Dodaj stan graficzny PDF** dla efektów overprint i halftone
* **Osadzanie obrazów z własną nieprzezroczystością** przy użyciu `ImageFragment` i stanu graficznego
* **Przetwarzanie wsadowe** wielu PDF‑ów w folderze z równoległością w celu zwiększenia przepustowości
* **Korzystanie z wysokopoziomowego API Aspose.PDF** (`PdfSaveOptions`, `PdfPageEditor`) dla bardziej złożonych przepływów pracy

Śmiało eksperymentuj z różnymi wartościami alfa


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET&#58; Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [How to Add Images to PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}