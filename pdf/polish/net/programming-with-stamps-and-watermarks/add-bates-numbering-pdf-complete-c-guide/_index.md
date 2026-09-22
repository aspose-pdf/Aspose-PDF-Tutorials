---
category: general
date: 2026-03-22
description: Szybko dodaj numerację Bates do pliku PDF przy użyciu Aspose.Pdf. Dowiedz
  się, jak dodać numerację Bates, kolejno numerowane strony, niestandardową stopkę
  w PDF oraz artefakt do PDF w kilka minut.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: pl
og_description: Dodaj numerację Bates do PDF przy użyciu Aspose.Pdf. Ten przewodnik
  pokazuje, jak dodać numerację Bates, dodać kolejno numerowane strony, dodać niestandardową
  stopkę do PDF oraz dodać artefakt do PDF.
og_title: Dodaj numerację Bates w PDF – Samouczek C# krok po kroku
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Dodaj numerację Bates do PDF – Kompletny przewodnik C#
url: /pl/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodawanie numeracji Bates w PDF – Kompletny przewodnik C#

Czy kiedykolwiek musiałeś **add bates numbering pdf** w partii dokumentów prawnych, ale nie wiedziałeś, od czego zacząć? Nie jesteś pierwszy – wielu programistów napotyka ten problem przy tworzeniu narzędzi do zarządzania sprawami. Dobra wiadomość? Dzięki Aspose.Pdf możesz **add bates**, **add sequential page numbers** i nawet **add custom footer pdf** w kilku linijkach kodu.  

W tym samouczku przeprowadzimy Cię przez cały proces, od instalacji biblioteki po zapisanie finalnego pliku, a także podpowiemy, jak **add artifact to pdf** bez uszkadzania istniejącej zawartości. Na koniec będziesz mieć gotowy fragment kodu, który możesz wkleić do dowolnego projektu .NET.

## Co będzie potrzebne

- .NET 6+ (kod działa zarówno na .NET Core, jak i .NET Framework)  
- Ważna licencja Aspose.Pdf for .NET (możesz rozpocząć od darmowej wersji ewaluacyjnej)  
- Plik PDF wejściowy (`input.pdf`) umieszczony w folderze, do którego masz dostęp  
- Visual Studio, Rider lub dowolny edytor C#, którego używasz  

To wszystko – poza Aspose.Pdf nie potrzebujesz dodatkowych pakietów NuGet.

## Krok 1: Instalacja Aspose.Pdf przez NuGet

Na początek – pobierzmy bibliotekę na nasz komputer. Otwórz terminal w katalogu projektu i uruchom:

```bash
dotnet add package Aspose.Pdf
```

Albo, jeśli korzystasz z konsoli Menedżera Pakietów w Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*Pro tip:* Po instalacji sprawdź, czy folder `Aspose.Pdf` pojawił się w `Dependencies → Packages` w eksploratorze rozwiązań.

## Krok 2: Załadowanie źródłowego dokumentu PDF

Teraz tworzymy obiekt `Document`, który reprezentuje PDF, który chcemy otagować. Użycie instrukcji `using` zapewnia automatyczne zwolnienie uchwytu pliku.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Dlaczego `using var`? Gwarantuje zwolnienie zasobów nawet w przypadku wystąpienia wyjątku, co zapobiega problemom z blokowaniem pliku przy późniejszej próbie nadpisania go.

## Krok 3: Utworzenie i skonfigurowanie artefaktu numeracji Bates

Numer Bates to w zasadzie artefakt tekstowy, który żyje w logicznej strukturze PDF. Możesz traktować go jak **custom footer pdf**, ponieważ pojawia się na każdej stronie, nie będąc częścią strumienia zawartości strony.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Dlaczego te ustawienia mają znaczenie

- **Prefix**: Przydatny do rozróżniania typów dokumentów (np. „INV‑” dla faktur).  
- **Start**: Ustawia pierwszą liczbę; możesz pobrać ją z bazy danych, jeśli potrzebna jest ciągłość między plikami.  
- **Format**: `"0000"` wymusza wyświetlanie czterech cyfr, zapewniając wyrównanie przy rosnących numerach.  
- **X/Y**: Współrzędne mierzone są od lewego dolnego rogu, więc `Y = 20` umieszcza tekst tuż nad dolnym marginesem strony. Dostosuj `X`, jeśli chcesz wyrównać numer do lewej lub wyśrodkować go.

Jeśli zamiast numerów Bates potrzebujesz **add sequential page numbers**, po prostu pomiń `Prefix` i zmień `Format` na `"###"` lub inny wybrany wzorzec.

## Krok 4: Zastosowanie artefaktu do wszystkich stron

Aspose.Pdf pozwala dołączyć artefakt do całego dokumentu jednym wywołaniem. To najefektywniejszy sposób na **add artifact to pdf** bez ręcznego iterowania po każdej stronie.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

W tle Aspose dodaje artefakt do słownika strony każdej strony, co oznacza, że numeracja staje się częścią logicznej struktury PDF – idealna do późniejszego wyodrębniania lub wyszukiwania.

## Krok 5: Zapisz zaktualizowany PDF

Na koniec zapisz zmiany na dysku. Możesz nadpisać oryginał lub zapisać do nowego pliku; to drugie jest bezpieczniejsze podczas rozwoju.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Po otwarciu `output.pdf` w przeglądarce zobaczysz „INV‑1000”, „INV‑1001”, … w prawym dolnym rogu każdej strony.

### Weryfikacja wyniku

Otwórz PDF w Adobe Acrobat lub dowolnym podglądzie i poszukaj numerów. Jeśli chcesz potwierdzić programowo, możesz odczytać artefakt:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Ten fragment wypisuje etykietę Bates dla każdej strony – przydatne w testach automatycznych.

## Przypadki brzegowe i najczęstsze pytania

### Co zrobić, jeśli mój PDF już ma stopkę?

Dodanie artefaktu nie nadpisze istniejących stopek, ponieważ artefakty znajdują się w osobnej warstwie. Jeśli jednak obawy budzi nakładanie się wizualne, zmień współrzędną `Y` lub zwiększ offset `X`, aby przesunąć numer Bates w inne miejsce.

### Czy mogę użyć innej czcionki lub koloru?

Oczywiście. `BatesNumberingArtifact` dziedziczy po `Artifact`, więc możesz ustawić `Font`, `FontColor`, a nawet `Opacity`. Przykład:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Jak zresetować licznik dla nowego dokumentu?

Wystarczy zmienić `Start` przed wywołaniem `AddArtifact`. Jeśli generujesz wiele PDF‑ów w pętli, utrzymuj licznik w logice aplikacji.

### Czy to podejście działa z zaszyfrowanymi PDF‑ami?

Aspose.Pdf może otworzyć zaszyfrowane PDF‑y, jeśli podasz hasło:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Po odszyfrowaniu te same kroki dodawania artefaktu działają bez zarzutu.

## Pełny działający przykład

Poniżej kompletny, gotowy do uruchomienia program. Wklej go do aplikacji konsolowej, dopasuj ścieżki i naciśnij **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Oczekiwany wynik:** Konsola wypisuje „Bates numbering added successfully!” a `output.pdf` zawiera kolejno etykiety takie jak `INV‑1000`, `INV‑1001`, itp., umieszczone w prawym dolnym rogu każdej strony.

## Szybkie podsumowanie

- **Główny cel:** **add bates numbering pdf** przy użyciu Aspose.Pdf.  
- Omówiliśmy **how to add bates**, **add sequential page numbers** oraz **add custom footer pdf** za pomocą jednego artefaktu.  
- Samouczek pokazał, jak **add artifact to pdf**, radzić sobie z przypadkami brzegowymi i weryfikować rezultat.  

## Co dalej?

- **Dynamiczne prefiksy:** Pobieraj wartości z bazy danych, aby generować „CASE‑2023‑001”, „CASE‑2023‑002”, …  
- **Warunkowe położenie:** Użyj wykrywania rozmiaru strony (`page.MediaBox`), aby wyśrodkować numery na stronach w orientacji poziomej.  
- **Połączenie z watermarkami:** Dodaj półprzezroczyste logo obok numeru Bates w celu brandingu.  

Eksperymentuj – może odkryjesz lepszy sposób na przetwarzanie tysięcy plików jednocześnie. Jeśli napotkasz problemy, zostaw komentarz lub zajrzyj do oficjalnej dokumentacji Aspose (są naprawdę przejrzyste). Szczęśliwego kodowania!  

![przykład dodawania numeracji bates pdf](https://example.com/bates-numbering-screenshot.png "Zrzut ekranu pokazujący add bates numbering pdf w przeglądarce PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}