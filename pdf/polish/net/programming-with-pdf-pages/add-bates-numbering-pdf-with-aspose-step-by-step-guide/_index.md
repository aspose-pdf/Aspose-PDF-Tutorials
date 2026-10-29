---
category: general
date: 2026-08-08
description: Dodaj numerację Batesa do pliku PDF przy użyciu Aspose.Pdf w C#. Ten
  tutorial pokazuje również, jak dodać pustą stronę do PDF i generować PDF programowo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: pl
lastmod: 2026-08-08
og_description: Dodaj numerację Bates do pliku PDF przy użyciu Aspose.Pdf w C#. Dowiedz
  się, jak dodać pustą stronę do PDF, generować PDF programowo i zapisać finalny dokument
  w kilka minut.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Dodaj numerację Bates do PDF za pomocą Aspose – kompletny przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Dodaj numerację Bates w PDF przy użyciu Aspose – przewodnik krok po kroku
url: /pl/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj bates numbering pdf przy użyciu Aspose – przewodnik krok po kroku

Dodanie bates numbering pdf przy użyciu Aspose.Pdf jest proste, gdy zrozumiesz podstawowe kroki. Jeśli potrzebujesz także dodać pustą stronę pdf lub generować pdf programowo, ten przewodnik zawiera wszystko, czego potrzebujesz.

W tym samouczku:

* Utwórz nowy dokument PDF od podstaw.  
* Dodaj pustą stronę pdf, która będzie zawierać numery Bates.  
* Skonfiguruj artefakt numeracji Bates z niestandardowym prefiksem.  
* Zapisz PDF, aby numery pojawiły się w wygenerowanym pliku.  

Po zakończeniu będziesz mieć w pełni działającą aplikację konsolową C#, która generuje PDF zawierający numery Bates, takie jak **CASE‑1000**, **CASE‑1001**, … – typowe wymaganie w procesach prawnych i e‑discovery.

## Wymagania wstępne

* .NET 6.0 SDK lub nowszy (kod działa również z .NET Framework 4.8).  
* Visual Studio 2022 lub dowolne IDE kompatybilne z C#.  
* Ważna licencja Aspose.Pdf for .NET (lub darmowy klucz ewaluacyjny).  
* Podstawowa znajomość składni C#.

> **Wskazówka:** Jeśli uruchomisz kod bez licencji, Aspose doda małą znak wodny do wyjściowego PDF.

## Krok 1: Skonfiguruj projekt i zaimportuj Aspose.Pdf

Utwórz nowy projekt konsolowy i dodaj pakiet NuGet Aspose.Pdf:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Dyrektywy `using` wymagane w przykładzie:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Te przestrzenie nazw dają dostęp do klas `Document`, `Page` i `BatesNumberingArtifact` używanych później.

## Krok 2: Dodaj pustą stronę pdf

Numer Bates musi być przypisany do strony, więc najpierw tworzymy pustą stronę, która otrzyma artefakt numeracji.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

Klasa `Document` reprezentuje cały plik PDF, natomiast `Pages.Add()` wstawia nową, pustą stronę na końcu kolekcji stron dokumentu. Ponieważ dokument zaczyna się pusty, to wywołanie tworzy również pierwszą stronę.

## Krok 3: Skonfiguruj artefakt numeracji Bates

Teraz definiujemy, jak mają wyglądać numery Bates. `BatesNumberingArtifact` pozwala ustawić numer początkowy, prefiks, sufiks oraz opcje formatowania.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Dlaczego to ważne:**  
Ustawienie `StartNumber` na **1000** odpowiada typowym konwencjom nazw plików spraw prawnych. `Prefix` zapewnia, że każdy numer pojawia się jako **CASE‑1000**, **CASE‑1001**, … co ułatwia wyszukiwanie i sortowanie.

## Krok 4: Dołącz artefakt do strony

Artefakt musi zostać dodany do kolekcji `Artifacts` strony, aby Aspose renderował go na każdej stronie podczas zapisywania.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Gdy dokument zostanie zapisany, Aspose automatycznie powiela artefakt na wszystkich stronach, zwiększając numer dla każdej kolejnej strony.

## Krok 5: (Opcjonalnie) Dodaj dodatkowe strony

Jeśli potrzebujesz więcej stron, po prostu powtórz `pdfDocument.Pages.Add()`. Artefakt numeracji Bates, który dołączyłeś w poprzednim kroku, automatycznie pojawi się na każdej nowej stronie.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Krok 6: Zapisz PDF – generuj pdf programowo

Na koniec zapisz dokument na dysku. To jest moment, w którym numery Bates są renderowane na stronach.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Oczekiwany rezultat:**  
Otwórz *BatesNumberedDocument.pdf* i zobaczysz trzy‑stronicowy PDF. Każda strona wyświetla numer Bates w prawym dolnym rogu:

* Strona 1 → **CASE‑1000**  
* Strona 2 → **CASE‑1001**  
* Strona 3 → **CASE‑1002**

Numery są automatycznie zwiększane, ponieważ artefakt jest dołączony do kolekcji stron.

## Pełny, działający przykład

Łącząc wszystko razem, oto kompletny program konsolowy, który możesz skopiować, wkleić i uruchomić:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Uruchom program poleceniem `dotnet run`. Po wykonaniu znajdź plik na pulpicie i zweryfikuj numery Bates.

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję innej czcionki lub pozycji?

`BatesNumberingArtifact` udostępnia właściwości takie jak `FontSize`, `FontColor`, `HorizontalAlignment` i `VerticalAlignment`. Na przykład:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Jak wykluczyć konkretną stronę z numeracji?

Utwórz osobny `BatesNumberingArtifact` dla stron, które chcesz numerować i dodaj go tylko do tych stron. Strony bez dołączonego artefaktu pozostaną nieponumerowane.

### Czy to działa z istniejącymi plikami PDF?

Tak. Zamiast `new Document()`, wczytaj istniejący plik:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Następnie dołącz artefakt do wybranych stron i zapisz.

## Zakończenie

Teraz wiesz, jak **add bates numbering pdf** przy użyciu Aspose.Pdf, jak **add blank page pdf**, oraz jak **generate pdf programmatically** w czystym, wielokrotnie używalnym rozwiązaniu C#. Podejście działa z dowolną liczbą stron, niestandardowymi prefiksami i opcjami stylizacji, dając pełną kontrolę nad ostatecznym dokumentem.

Kolejne kroki, które możesz rozważyć:

* Use **create pdf as

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak dodać i dostosować numery stron w PDF przy użyciu Aspose.PDF dla .NET | Przewodnik po manipulacji dokumentami](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Jak dodać pustą stronę na końcu PDF przy użyciu Aspose.PDF dla .NET | Przewodnik krok po kroku](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Utwórz dokument PDF przy użyciu Aspose.PDF – Dodaj stronę, kształt i zapisz](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}