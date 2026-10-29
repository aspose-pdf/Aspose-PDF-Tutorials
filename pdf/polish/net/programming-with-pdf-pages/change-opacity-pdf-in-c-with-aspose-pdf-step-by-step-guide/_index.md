---
category: general
date: 2026-08-11
description: Zmień przezroczystość PDF przy użyciu Aspose.Pdf w C#. Dowiedz się, jak
  dodać przezroczystość do stron PDF, ustawić stan graficzny i szybko zapisać wynik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change opacity PDF
- how to add transparency
- add pdf transparency
language: pl
lastmod: 2026-08-11
og_description: Zmień przezroczystość PDF przy użyciu Aspose.Pdf w C#. Skorzystaj
  z tego przewodnika, aby dowiedzieć się, jak dodać przezroczystość do dowolnego dokumentu
  PDF, dostosować stany graficzne i wyeksportować wynik.
og_image_alt: Screenshot illustrating change opacity PDF example in C# code
og_title: Zmieniaj przezroczystość PDF w C# – kompletny samouczek Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  headline: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  name: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
    text: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
  - name: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
    text: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
  - name: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
    text: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
  - name: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
    text: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Zmiana przezroczystości PDF w C# przy użyciu Aspose.Pdf – przewodnik krok po
  kroku
url: /pl/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zmiana przezroczystości PDF w C# przy użyciu Aspose.Pdf – przewodnik krok po kroku

Jeśli potrzebujesz **zmienić przezroczystość PDF** programowo, ten tutorial pokaże Ci dokładnie, jak to zrobić. Korzystając z Aspose.Pdf dla .NET możesz kontrolować przezroczystość obiektów graficznych, tekstu i obrazów bez opuszczania kodu C#.

W kolejnych sekcjach dowiesz się **jak dodać przezroczystość** do strony PDF, co oznaczają leżące u podstaw obiekty stanu graficznego oraz jak zapisać zmodyfikowany dokument. Poradnik obejmuje także typowe pułapki przy **dodawaniu przezroczystości PDF** oraz oferuje wskazówki dla rzeczywistych scenariuszy.

## Co osiągniesz

* Wczytaj istniejący dokument PDF.
* Utwórz nowy słownik stanu graficznego definiujący wartości przezroczystości.
* Wstaw stan graficzny do słownika zasobów strony.
* Zapisz dokument z zaktualizowanym efektem **zmiany przezroczystości PDF**.

Nie są wymagane żadne zewnętrzne narzędzia — wystarczy biblioteka Aspose.Pdf dla .NET (wersja 23.10 lub nowsza) oraz środowisko programistyczne .NET.

## Wymagania wstępne

* Zainstalowany .NET 6.0 (lub .NET Framework 4.7.2+).
* Visual Studio 2022 lub dowolne IDE kompatybilne z C#.
* Odwołanie do pakietu NuGet `Aspose.Pdf`.
* Plik PDF wejściowy (`input.pdf`) znajdujący się w katalogu z prawami zapisu.

> **Wskazówka:** Podczas testowania zmian przezroczystości, pracuj z plikiem PDF, który już zawiera grafikę wektorową lub tekst; obrazy rastrowe ignorują parametry `ca` i `CA`, chyba że są umieszczone wewnątrz grupy przezroczystości.

## Zmiana przezroczystości PDF przy użyciu Aspose.Pdf

Sednem rozwiązania jest modyfikacja słownika **ExtGState** (external graphics state) strony. Słownik ten przechowuje parametry takie jak **ca** (przezroczystość linii) i **CA** (przezroczystość wypełnienia). Dodając nowy wpis, możesz odwoływać się do niego później w strumieniach zawartości.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;

class ChangeOpacityPdfExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        using (var document = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 2: Access the first page and its resource dictionary
            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Step 3: Create a new graphics state dictionary with desired opacity values
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                // Fill opacity (CA) – 1.0 means fully opaque
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                // Stroke opacity (ca) – 0.5 makes lines semi‑transparent
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                // Blend mode (BM) – Normal is the default blend mode
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // Step 4: Add the new graphics state to the ExtGState dictionary
            // “GS0” is the identifier you will reference later in the content stream
            extGState.Add("GS0", newGraphicsState);

            // Optional: Demonstrate usage by drawing a semi‑transparent rectangle
            // This part shows how the new graphics state affects drawing commands.
            var canvas = new Aspose.Pdf.Drawing.Graphic(page);
            canvas.SetGraphicsState("GS0"); // Apply the opacity settings
            canvas.Rectangle(100, 500, 200, 600);
            canvas.FillColor = Color.FromRgb(255, 0, 0); // Red fill
            canvas.StrokeColor = Color.FromRgb(0, 0, 255); // Blue border
            canvas.Draw();

            // Step 5: Save the modified PDF
            document.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF saved with changed opacity.");
    }
}
```

### Dlaczego to działa

* **ExtGState** jest zasobem PDF, który przechowuje wielokrotnie używane parametry graficzne. Dodając własny wpis (`GS0`) tworzysz konfigurowalną przezroczystość do ponownego użycia.
* Klucz **ca** kontroluje przezroczystość operacji rysowania linii (linie, obramowania). Klucz **CA** kontroluje operacje wypełniania (kształty kolorowe, tekst). Ustawienie `ca = 0.5` sprawia, że linie są w 50 % przezroczyste, natomiast `CA = 1` pozostawia wypełnienia w pełni nieprzezroczyste.
* Wywołanie `SetGraphicsState("GS0")` instruuje Aspose.Pdf, aby w strumieniu zawartości wygenerował operator `/GS0 gs`, aktywując nowe ustawienia przezroczystości dla wszystkich kolejnych poleceń rysowania.

## Jak dodać przezroczystość do istniejącej zawartości

Jeśli na stronie już znajdują się tekst lub obrazy i chcesz je uczynić półprzezroczystymi bez ponownego rysowania, możesz wstrzyknąć operator **gs** przed istniejącą zawartością. Poniższy fragment kodu pokazuje, jak dodać ten operator na początek strumienia zawartości strony.

```csharp
// Retrieve the existing content stream
var content = page.Contents[1];
var originalBytes = content.ToByteArray();

// Build the new content with the graphics state applied
var gsOperator = System.Text.Encoding.ASCII.GetBytes("/GS0 gs\n");
var newBytes = new List<byte>(gsOperator);
newBytes.AddRange(originalBytes);

// Replace the page content
page.Contents[1].Replace(newBytes.ToArray());
```

### Przypadki brzegowe i uwagi

| Sytuacja | Zalecane postępowanie |
|-----------|----------------------|
| **Wiele stron** | Przejdź pętlą przez `document.Pages` i powtórz kroki 2‑4 dla każdej strony, którą chcesz zmodyfikować. |
| **Różna przezroczystość dla elementów** | Utwórz dodatkowe stany graficzne (`GS1`, `GS2`, …) z odrębnymi wartościami `ca`/`CA` i stosuj je selektywnie. |
| **PDF‑y z istniejącymi wpisami ExtGState** | Bezpiecznie użyj `dictEditor["ExtGState"]`; jeśli klucz nie istnieje, utwórz nowy `CosPdfDictionary` i przypisz go do `page.Resources`. |
| **Grupy przezroczystości** | Dla złożonego kompozytu (np. nakładających się obrazów) ustaw słownik `/Group` z `S /Transparency` oraz `CS /DeviceRGB`. To wykracza poza podstawowe **zmiany przezroczystości PDF**, ale może być wymagane w zaawansowanych układach. |

## Dodaj przezroczystość PDF do grafiki wektorowej

Poza prostokątami, możesz zastosować ten sam stan graficzny do dowolnego rysunku wektorowego — linii, krzywych czy nawet tekstu. Oto szybki przykład, który zapisuje półprzezroczysty tekst:

```csharp
var textFragment = new TextFragment("Transparent text")
{
    Position = new Position(100, 400),
    TextState = { FontSize = 36, ForegroundColor = Color.Black }
};
page.Paragraphs.Add(textFragment);

// Apply the graphics state to the text fragment
textFragment.TextState.GraphicsState = "GS0";
```

Właściwość `GraphicsState` klasy `TextState` instruuje silnik PDF, aby renderował tekst z użyciem przezroczystości zdefiniowanej w `GS0`. To najprostszy sposób na **dodanie przezroczystości PDF** do treści tekstowej.

## Typowe pułapki przy zmianie przezroczystości PDF

1. **Brak słownika ExtGState** – Niektóre pliki PDF nie zawierają domyślnie wpisu `ExtGState`. W takim przypadku należy go utworzyć:
   ```csharp
   if (!dictEditor.ContainsKey("ExtGState"))
       dictEditor.Add("ExtGState", new CosPdfDictionary(document));
   ```
2. **Nieprawidłowa nazwa zasobu** – Nazwa użyta w `SetGraphicsState` musi dokładnie odpowiadać kluczowi, który dodano (`GS0`). Błąd literowy skutkuje domyślnym, w pełni nieprzezroczystym renderowaniem.
3. **Nadpisywanie istniejących stanów graficznych** – Dodanie nowego wpisu nie zastępuje istniejących. Jeśli ponownie użyjesz nazwy, która już istnieje, możesz nieumyślnie zmienić inne elementy strony, które się do niej odwołują.
4. **Kompatybilność przeglądarek** – Starsze przeglądarki PDF (przed wersją 1.4) mogą ignorować przezroczystość. Upewnij się, że docelowi odbiorcy używają nowoczesnego przeglądarki, takiej jak Adobe Reader DC lub wbudowany podgląd PDF w Chrome.

## Pełny działający przykład

Poniżej znajduje się kompletny, samodzielny program, który możesz skopiować, wkleić i uruchomić. Zawiera wszystkie niezbędne dyrektywy `using`, obsługę błędów oraz komentarze.



## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak dodać znak wodny tekstowy do PDF przy użyciu Aspose.PDF .NET: Kompletny przewodnik](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Jak dodać znaki wodne stron w PDF przy użyciu Aspose.PDF dla .NET: Kompletny przewodnik](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Jak dodać znaki wodne stron w PDF przy użyciu Aspose.PDF dla .NET | Przewodnik po znakach wodnych i tła](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}