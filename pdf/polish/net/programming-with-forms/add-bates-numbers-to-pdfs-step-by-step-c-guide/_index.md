---
category: general
date: 2026-02-12
description: Szybko dodawaj numery Bates do plików PDF. Dowiedz się, jak dodać pole
  tekstowe do PDF, dodać pole formularza do PDF oraz dodać numery stron do PDF przy
  użyciu Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: pl
og_description: Dodaj numery Bates do dokumentów PDF w C#. Ten przewodnik pokazuje,
  jak dodać pole tekstowe PDF, dodać pole formularza PDF oraz dodać numery stron PDF
  przy użyciu Aspose.PDF.
og_title: Dodaj numery Bates do plików PDF – Kompletny samouczek C#
tags:
- PDF
- C#
- Aspose.PDF
title: Dodaj numery Bates do plików PDF – Przewodnik krok po kroku w C#
url: /pl/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj numery Bates do PDF – Kompletny przewodnik C#

Czy kiedykolwiek potrzebowałeś **dodać numery bates** do stosu prawnych plików PDF, ale nie wiedziałeś od czego zacząć? Nie jesteś sam. W wielu kancelariach i projektach e‑discovery, znakowanie każdej strony unikalnym identyfikatorem to codzienne zadanie, a robienie tego ręcznie to koszmar.  

Dobre wieści? Dzięki kilku linijkom C# i Aspose.PDF możesz zautomatyzować cały proces. W tym samouczku przeprowadzimy Cię przez **jak dodać numery bates**, posypiemy pole tekstowe na każdej stronie i zapisujemy czysty, przeszukiwalny PDF — bez żadnego wysiłku.

> **Co otrzymasz:** w pełni działający przykład kodu, wyjaśnienia, dlaczego każda linia ma znaczenie, wskazówki dotyczące przypadków brzegowych oraz szybka lista kontrolna do weryfikacji wyniku.  

Omówimy także powiązane zadania, takie jak **add text field pdf**, **add form field pdf** i **add page numbers pdf**, abyś miał zestaw narzędzi gotowy na każde wyzwanie związane z automatyzacją dokumentów.

---

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+)  
- Visual Studio 2022 (lub dowolne IDE, które preferujesz)  
- Ważna licencja Aspose.PDF for .NET (bezpłatna wersja próbna działa do testów)  
- Plik PDF źródłowy o nazwie `source.pdf` umieszczony w folderze, do którego możesz odwołać się  

Jeśli którykolwiek z tych elementów jest Ci nieznany, po prostu zatrzymaj się i zainstaluj brakujący komponent przed kontynuacją. Poniższe kroki zakładają, że już dodałeś pakiet NuGet Aspose.PDF:

```bash
dotnet add package Aspose.Pdf
```

---

## Jak dodać numery bates do PDF przy użyciu Aspose.PDF

Poniżej znajduje się kompletny, gotowy do skopiowania program. Ładuje PDF, tworzy **pole tekstowe** na każdej stronie, zapisuje sformatowany numer Bates i na końcu zapisuje zmodyfikowany plik.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Dlaczego to działa

- **`Document`** jest punktem wejścia; reprezentuje cały plik PDF.  
- **`Rectangle`** określa, gdzie pole znajduje się na stronie. Liczby są w punktach (1 pt ≈ 1/72 in). Dostosuj współrzędne, jeśli potrzebujesz numeru w innym rogu.  
- **`TextBoxField`** jest *polem formularza*, które może przechowywać dowolny ciąg znaków. Przypisując `Value`, skutecznie **add page numbers pdf** z niestandardowym prefiksem.  
- **`pdfDocument.Form.Add`** rejestruje pole w AcroForm PDF, czyniąc je widocznym w przeglądarkach takich jak Adobe Acrobat.  

Jeśli kiedykolwiek będziesz musiał zmienić wygląd (czcionkę, kolor, rozmiar), możesz dostosować właściwości `TextBoxField` — zobacz dokumentację Aspose dotyczącą `DefaultAppearance` i `Border`.

## Dodawanie pola tekstowego do każdej strony PDF (krok „add text field pdf”)

Czasami potrzebujesz tylko widocznej etykiety, a nie interaktywnego pola formularza. W takim wypadku możesz zamienić `TextBoxField` na `TextFragment` i dodać go bezpośrednio do kolekcji `Paragraphs` strony. Oto szybka alternatywa:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

Podejście **add text field pdf** jest przydatne, gdy finalny dokument będzie tylko do odczytu, podczas gdy metoda **add form field pdf** pozwala później edytować numery.

## Zapisywanie PDF z numerami Bates (moment „add page numbers pdf”)

Po zakończeniu pętli wywołanie `pdfDocument.Save` zapisuje wszystko na dysku. Jeśli musisz zachować oryginalny plik, po prostu zmień ścieżkę wyjściową lub użyj przeciążeń `pdfDocument.Save`, aby strumieniowo przesłać wynik bezpośrednio w odpowiedzi w API webowym.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

To jest najfajniejsze — bez plików tymczasowych, bez dodatkowych bibliotek, tylko Aspose wykonuje ciężką pracę.

## Oczekiwany wynik i szybka weryfikacja

Otwórz `bates.pdf` w dowolnym przeglądarce PDF. Powinieneś zobaczyć małe pole w lewym dolnym rogu każdej strony z tekstem:

```
BATES-00001
BATES-00002
…
```

Jeśli sprawdzisz właściwości dokumentu, zauważysz AcroForm zawierający pola o nazwach `Bates_1`, `Bates_2` itd. To potwierdza, że krok **add form field pdf** zakończył się sukcesem.

## Częste pułapki i wskazówki profesjonalistów

| Problem | Dlaczego się dzieje | Rozwiązanie |
|-------|----------------|-----|
| Numery pojawiają się poza środkiem | Współrzędne Rectangle są względem lewego dolnego rogu strony. | Odwróć wartość Y (`pageHeight - marginTop`) lub użyj `page.PageInfo.Height`, aby obliczyć położenie z górnym marginesem. |
| Pola są niewidoczne w Adobe Reader | Domyślna ramka jest ustawiona na „No”. | Ustaw `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Duże pliki PDF powodują obciążenie pamięci | `using` zwalnia dokument dopiero po zakończeniu pętli. | Przetwarzaj strony w partiach lub użyj `pdfDocument.Save` z `SaveOptions`, które umożliwiają strumieniowanie. |
| Licencja nie została zastosowana | Aspose drukuje znak wodny na pierwszej stronie. | Zarejestruj licencję wcześnie: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

## Rozszerzanie rozwiązania

- **Niestandardowe prefiksy:** Zastąp `"BATES-"` dowolnym ciągiem (`"DOC-"`, `"CASE-"`, …).  
- **Długość wypełnienia zerami:** Zmień `{pageNumber:D5}` na `{pageNumber:D3}` dla trzech cyfr.  
- **Dynamiczne położenie:** Użyj `pdfDocument.Pages[pageNumber].PageInfo.Width`, aby umieścić pole po prawej stronie.  
- **Warunkowe numerowanie:** Pomijaj puste strony, sprawdzając `pdfDocument.Pages[pageNumber].IsBlank`.  

Wszystkie te warianty zachowują podstawowy wzorzec **add bates numbers**, **add text field pdf** i **add form field pdf** niezmieniony.

## Pełny działający przykład (Wszystko w jednym)

Poniżej znajduje się finalny, gotowy do uruchomienia program, który zawiera powyższe wskazówki. Skopiuj go do nowej aplikacji konsolowej i naciśnij F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Uruchom go, otwórz wynik i zobaczysz profesjonalnie wyglądający identyfikator na każdej stronie — dokładnie to, czego oczekuje specjalista ds. wsparcia w postępowaniach sądowych.

## Zakończenie

Właśnie pokazaliśmy **jak dodać numery bates** do dowolnego PDF przy użyciu C# i Aspose.PDF. Tworząc **pole tekstowe** na każdej stronie jednocześnie **add text field pdf**, **add form field pdf** i **add page numbers pdf** w jednym przebiegu. Podejście jest szybkie, skalowalne i łatwe do dostosowania pod niestandardowe prefiksy, różne układy czy logikę warunkową.

Gotowy na kolejne wyzwanie? Spróbuj osadzić kod QR, który prowadzi do oryginalnego pliku sprawy, lub wygeneruj osobną stronę indeksu, która wymienia wszystkie numery Bates wraz z odpowiadającymi im tytułami stron. To samo API pozwala łączyć PDF‑y, wyodrębniać strony i nawet redagować wrażliwe dane — więc nie ma ograniczeń.

Jeśli napotkasz problem, zostaw komentarz poniżej lub sprawdź oficjalną dokumentację Aspose dla bardziej szczegółowych informacji. Szczęśliwego kodowania i niech Twoje PDF‑y zawsze będą idealnie ponumerowane!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}