---
category: general
date: 2026-07-20
description: Jak dodać numerację Bates do pliku PDF przy użyciu Aspose.Pdf. Dowiedz
  się, jak dodać numery Bates do PDF i dodać pieczątkę na każdej stronie szybko i
  niezawodnie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: pl
lastmod: 2026-07-20
og_description: Jak dodać numerację Batesa do pliku PDF za pomocą Aspose.Pdf. Ten
  przewodnik pokazuje, jak dodać numery Batesa do PDF i oznaczyć każdą stronę w kilku
  linijkach kodu C#.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: Jak dodać numerację Bates w PDF – Kompletny samouczek Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: Jak dodać numerację Bates w pliku PDF przy użyciu Aspose – Przewodnik krok
  po kroku
url: /pl/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać numerację Bates w PDF przy użyciu Aspose – Przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak dodać numerację Bates** do dokumentu prawnego, nie tracąc godzin w interfejsie graficznym? Nie jesteś jedyny. W wielu kancelariach, agencjach rządowych i nawet dużych przedsiębiorstwach, znakowanie każdej strony unikalnym identyfikatorem to codzienne zadanie — a jedynie jedna linia C# może uczynić to dziecinnie prostym.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje dokładnie **jak dodać numerację Bates** przy użyciu biblioteki Aspose.Pdf. Po zakończeniu będziesz także wiedział, jak **dodawać numery Bates do plików PDF** oraz **dodawać znaczek do każdej strony** przy użyciu kilku linijek kodu. Bez magii, tylko jasne wyjaśnienia i praktyczne wskazówki.

## Czego się nauczysz

- Załadujesz istniejący PDF przy pomocy Aspose.Pdf.
- Utworzysz `BatesNumberingStamp` i dostosujesz jego wygląd.
- Przejdziesz po każdej stronie i **dodasz znaczek do każdej strony** automatycznie.
- Zapiszesz wynik jako nowy PDF, który będzie zawierał profesjonalny numer Bates na każdej kartce.

### Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7+).
- Ważna licencja Aspose.Pdf for .NET (lub tymczasowy klucz ewaluacyjny).
- Oryginalny plik PDF, który chcesz ponumerować (nazwijmy go `Original.pdf`).

Jeśli spełniasz te trzy warunki, możesz od razu przystąpić do działania.

---

## Krok 1: Przygotuj projekt i zainstaluj Aspose.Pdf

Najpierw utwórz nowy projekt konsolowy (lub dodaj kod do istniejącego). Następnie pobierz pakiet NuGet:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Jeśli pracujesz w sieci korporacyjnej, upewnij się, że źródło NuGet jest skonfigurowane tak, aby mogło sięgnąć `https://www.nuget.org`.

## Krok 2: Załaduj źródłowy dokument PDF

Załadowanie PDF jest tak proste, jak podanie ścieżki do pliku. Klasa `Document` reprezentuje cały plik.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

Dlaczego logujemy liczbę stron? Ponieważ numeracja Bates musi być kolejna na *wszystkich* stronach, a przydatne jest sprawdzenie, że nie załadowaliśmy przypadkowo innego pliku.

## Krok 3: Utwórz znaczek numeracji Bates

Serce operacji to `BatesNumberingStamp`. Pozwala on zdefiniować prefiks, separator, wypełnienie cyfr oraz to, czy znacznik ma być traktowany jako *artifact* (tj. niewidoczny dla narzędzi ekstrakcji tekstu).

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**Dlaczego te ustawienia?**  
- `StartingNumber = 1000` naśladuje typowy rejestr sądowy, który już ma pewne zaległości.  
- `NumberOfDigits = 5` zapewnia, że liczby takie jak `01000`, `01001` itp. będą ładnie wyrównane.  
- `Artifact = true` jest niezbędne, gdy PDF będzie poddawany OCR lub procesom e‑discovery; liczby pozostają widoczne dla ludzi, ale są ignorowane przez silniki wyszukiwania tekstu.

## Krok 4: Dodaj znacznik do każdej strony

Teraz iterujemy po `document.Pages` i stosujemy ten sam znacznik do każdej strony. Aspose automatycznie zwiększa numerację za Ciebie.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **Częste pytanie:** *Czy mogę kontrolować, gdzie pojawia się znacznik?*  
> Oczywiście. `BatesNumberingStamp` dziedziczy po `Stamp`, więc możesz ustawić właściwości takie jak `HorizontalAlignment`, `VerticalAlignment`, `XIndent` i `YIndent` przed pętlą. Dla zwięzłości pozostaniemy przy domyślnym prawym dolnym rogu.

## Krok 5: Zapisz zmodyfikowany PDF

Na koniec utrwal zmiany. Możesz nadpisać oryginalny plik lub zapisać w nowej lokalizacji — tutaj zachowamy obie kopie.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

Po otwarciu `BatesNumbered.pdf` każda strona wyświetli znacznik podobny do:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

gdzie `00123` to całkowita liczba stron, a prefiks `ABC-` pozostaje stały.

---

## Pełny działający przykład

Skopiuj cały blok poniżej do nowego pliku `Program.cs` i uruchom go. Dostosuj ścieżki plików do swojego środowiska.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**Oczekiwany wynik w konsoli:**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

Otwórz zapisany plik i zobaczysz kolejno numerowane strony — dokładnie to, czego oczekujesz, **dodając numery Bates do PDF**.

---

## Zaawansowane modyfikacje (opcjonalnie)

| Cel | Jak to osiągnąć |
|------|-------------------|
| **Zmień kolor znacznika** | Ustaw `batesStamp.Color = Color.FromRgb(255, 0, 0);` przed pętlą. |
| **Umieść znacznik w nagłówku** | Dostosuj właściwości `HorizontalAlignment` i `VerticalAlignment` zgodnie z zakomentowanym kodem. |
| **Pomiń wybrane strony** | Dodaj warunek `if (page.Number % 2 == 0) continue;` wewnątrz `foreach`. |
| **Użyj własnej czcionki** | Przypisz `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **Spraw, aby znacznik był widoczny dla OCR** | Ustaw `Artifact = false`. |

Te warianty pozwalają **dodawać znacznik do każdej strony**, zachowując jednocześnie przejrzystą logikę podstawową.

---

## Najczęściej zadawane pytania

**P: Czy to działa z PDF‑ami zabezpieczonymi hasłem?**  
O: Tak. Załaduj dokument przy pomocy obiektu `PdfLoadOptions`, który zawiera hasło, a potem postępuj dokładnie tak, jak pokazano.

**P: Co zrobić, jeśli potrzebuję różnych prefiksów dla poszczególnych spraw?**  
O: Utwórz kilka instancji `BatesNumberingStamp`, skonfiguruj każdą z własnym `Prefix` i zastosuj je tylko do odpowiednich zakresów stron.

**P: Czy biblioteka jest darmowa?**  
O: Aspose.Pdf oferuje 30‑dniowy okres próbny. Do użytku produkcyjnego potrzebna jest licencja, ale interfejs API pozostaje taki sam.

---

## Podsumowanie

Właśnie pokazaliśmy, **jak dodać numerację Bates** do dowolnego PDF przy użyciu Aspose.Pdf, zademonstrowaliśmy, jak **dodawać numery Bates do PDF** w czysty, powtarzalny sposób oraz przedstawiliśmy najprostszy sposób **dodawania znacznika do każdej strony** przy użyciu jednej pętli. Kod jest w pełni samodzielny, działa w kilka sekund i może być włączony do większych potoków przetwarzania dokumentów bez modyfikacji.

Gotowy na kolejny wyzwanie? Spróbuj wygenerować stronę tytułową, która wymienia zakres numerów Bates, lub osadzić kod QR obok każdego znacznika. Możliwości są nieograniczone, a wzorzec, którego nauczyłeś się dzisiaj, przyda Ci się wszędzie tam, gdzie trzeba zautomatyzować metadane PDF.

Jeśli ten przewodnik okazał się pomocny, udostępnij go, zostaw komentarz lub zapoznaj się z innymi naszymi tutorialami o łączeniu PDF, znakowaniu wodnym i podpisach cyfrowych. Szczęśliwego kodowania!

## Co warto nauczyć się dalej?

Poniższe tutoriale obejmują tematy blisko powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}