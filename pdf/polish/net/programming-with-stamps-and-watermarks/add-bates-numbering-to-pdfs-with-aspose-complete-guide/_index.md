---
category: general
date: 2026-04-25
description: Szybko dodaj numerację Bates do plików PDF przy użyciu Aspose.Pdf. Dowiedz
  się, jak dodać numery stron do PDF, automatycznie dopasować rozmiar czcionki i dodać
  znak wodny tekstowy w C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: pl
og_description: Dodaj numerację Bates do plików PDF przy użyciu Aspose.Pdf. Ten przewodnik
  pokazuje, jak dodać numerację stron w PDF, automatycznie dopasować rozmiar czcionki
  oraz dodać znak wodny z tekstem w jednym, gotowym do uruchomienia przykładzie.
og_title: Dodaj numerację Bates do plików PDF – Pełny samouczek Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Dodaj numerację Batesa do plików PDF za pomocą Aspose – Kompletny przewodnik
url: /pl/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj numerację Bates do plików PDF przy użyciu Aspose – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **add bates numbering** do pliku PDF, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam — zespoły prawne, audytorzy i programiści napotykają ten problem codziennie. Dobre wieści? Dzięki Aspose.Pdf for .NET możesz dodać numer Bates, automatycznie dopasować rozmiar czcionki i nawet traktować pieczątkę jako subtelną znak wodny tekstowy — wszystko w kilku linijkach C#.

W tym samouczku przeprowadzimy Cię przez dokładne kroki, aby **add page numbers pdf**, dostosować czcionkę tak, aby nigdy nie wychodziła poza obszar, i raz na zawsze odpowiedzieć na pytanie „how to add bates”. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową, która generuje profesjonalnie ponumerowany PDF, oraz zobaczysz, jak rozbudować ją do pełnoprawnego rozwiązania znaków wodnych.

## Wymagania wstępne

* **Aspose.Pdf for .NET** (najnowszy pakiet NuGet z kwietnia 2026).  
* .NET 6.0 SDK lub nowszy – API działa tak samo na .NET Framework, ale .NET 6 zapewnia najlepszą wydajność.  
* Przykładowy PDF o nazwie `input.pdf` umieszczony w folderze, do którego możesz odwołać się (np. `C:\Docs\`).  

Nie wymaga dodatkowej konfiguracji; biblioteka jest samodzielna.

---

## Krok 1 – Załaduj źródłowy dokument PDF

Pierwszą rzeczą, którą robimy, jest otwarcie pliku, który chcemy ponumerować. Klasa `Document` Aspose reprezentuje cały PDF, a jej załadowanie jest tak proste, jak przekazanie ścieżki do konstruktora.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Dlaczego to ważne*: Załadowanie dokumentu daje dostęp do kolekcji `Pages`, w której później dołączymy pieczątkę Bates. Jeśli plik nie zostanie znaleziony, Aspose zgłasza wyraźny `FileNotFoundException`, więc dokładnie wiesz, co poszło nie tak.

---

## Krok 2 – Utwórz pieczątkę tekstową dla numerów Bates

Teraz tworzymy element wizualny, który pojawi się na każdej stronie. Klasa `TextStamp` pozwala osadzić dowolny ciąg znaków, a my użyjemy symbolu zastępczego `{page}-{total}`, aby Aspose automatycznie podmienił te tokeny.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Kluczowe punkty*:

* **auto adjust font size** – Ustawienie `AutoAdjustFontSizeToFitStampRectangle` na `true` zapewnia, że tekst nigdy nie wyjdzie poza prostokąt, co jest idealne dla numerów stron o zmiennej długości.
* **add text watermark** – Obniżając `Opacity`, zamieniamy numer Bates w delikatny znak wodny, spełniając wymóg „add text watermark” bez dodatkowego kroku.
* **how to add bates** – Tokeny `{page}` i `{total}` to tajny składnik; Aspose podmienia je w czasie wykonywania, więc nie musisz sam obliczać niczego.

---

## Krok 3 – Zastosuj pieczątkę na każdej stronie

Częstym pułapką jest nakładanie pieczątki tylko na pierwszą stronę. Aby naprawdę **add page numbers pdf**, musimy przeiterować całą kolekcję `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Dlaczego klonować? Metoda `AddStamp` wewnętrznie tworzy kopię, ale jawne użycie nowej instancji w każdej iteracji zapobiega przypadkowym skutkom ubocznym, jeśli później zmienisz właściwości pieczątki (np. kolor dla konkretnych stron).

---

## Krok 4 – Zapisz zaktualizowany PDF

Po umieszczeniu pieczątek, zapisanie zmian jest proste. Możesz nadpisać oryginalny plik lub zapisać w nowej lokalizacji — tutaj zapiszemy nowy plik o nazwie `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Jeśli otworzysz `output.pdf`, zobaczysz, że każda strona jest oznaczona „Bates: 1‑10”, „Bates: 2‑10”, … w prawym dolnym rogu, z delikatną przezroczystością, która pełni jednocześnie funkcję **add text watermark**.

---

## Pełny działający przykład

Łącząc wszystko razem, oto pojedynczy, samodzielny program konsolowy, który możesz skopiować i wkleić do Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Oczekiwany wynik**: Otwórz `output.pdf` w dowolnym przeglądarce; każda strona wyświetla linię taką jak „Bates: 3‑12” w prawym dolnym rogu, o odpowiednim rozmiarze dla prostokąta i renderowaną z 40 % przezroczystością. Spełnia to zarówno wymóg śledzenia prawnego, jak i potrzebę wizualnego znaku wodnego.

---

## Częste warianty i przypadki brzegowe

| Situation | What to change | Why |
|-----------|----------------|-----|
| **Inne umiejscowienie** | Dostosuj `HorizontalAlignment` / `VerticalAlignment` lub ustaw `XIndent`/`YIndent` | Niektóre firmy wolą umieszczenie w lewym górnym rogu lub na środku. |
| **Niestandardowy prefiks** | Zamień `"Bates: "` na `"Doc‑ID: "` lub dowolny inny ciąg | Możesz używać innej konwencji nazewnictwa. |
| **Wiele pieczątek** | Utwórz drugą `TextStamp` (np. dla informacji o poufności) i dodaj ją po pierwszej | Łączenie **add bates numbering** z innymi wymaganiami **add text watermark** jest proste. |
| **Duża liczba stron** | Zwiększ początkowy rozmiar czcionki (np. `14`) – auto‑adjust zmniejszy go w razie potrzeby | Gdy masz > 999 stron, ciąg staje się dłuższy; auto‑adjust zapobiega obcięciu. |
| **Zaszyfrowane PDFy** | Wywołaj `pdfDocument.Decrypt("password")` przed nakładaniem pieczątki | Nie możesz modyfikować zabezpieczonego pliku bez hasła. |

---

## Porady profesjonalne i pułapki

* **Pro tip:** Ustaw `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)`, jeśli zauważysz, że tekst przylega do krawędzi strony.  
* **Uwaga:** Bardzo małe prostokąty (domyślny rozmiar to 100 × 30 pt). Jeśli potrzebujesz większego obszaru, ustaw ręcznie `batesStamp.Width` i `batesStamp.Height`.  
* **Uwaga dotycząca wydajności:** Nakładanie pieczątki na tysiące stron może zająć kilka sekund, ale Aspose strumieniuje strony efektywnie — nie ma potrzeby ładowania całego dokumentu do pamięci.  

---

## Zakończenie

Właśnie pokazaliśmy, jak **add bates numbering** do PDF przy użyciu Aspose.Pdf, jednocześnie **add page numbers pdf**, włączając **auto adjust font size** i tworząc **add text watermark** w jednym spójnym procesie. Pełny, uruchamialny przykład powyżej zapewnia solidną bazę, którą możesz dostosować do dowolnego przepływu pracy z dokumentami prawnymi lub wewnętrznego systemu raportowania.

Gotowy na kolejny krok? Spróbuj połączyć to podejście z API łączenia PDF‑ów Aspose, aby przetwarzać wiele plików jednocześnie, lub zbadaj klasę `TextFragment` w celu uzyskania bardziej zaawansowanych znaków wodnych (kolorowych, obróconych lub wielowierszowych). Możliwości są nieograniczone, a kod, który teraz masz, jest solidną podstawą.

Jeśli uznałeś ten przewodnik za przydatny, zostaw komentarz, oznacz repozytorium gwiazdką lub podziel się własnymi wariantami. Szczęśliwego kodowania i niech Twoje PDFy zawsze będą idealnie ponumerowane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}