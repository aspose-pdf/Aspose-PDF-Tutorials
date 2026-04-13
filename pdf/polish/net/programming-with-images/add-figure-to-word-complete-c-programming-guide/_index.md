---
category: general
date: 2026-04-12
description: Dodaj rysunek do Worda szybko przy użyciu C#. Dowiedz się, jak pozycjonować
  rysunek w Wordzie, wstawiać rysunek do pliku docx oraz dodawać niestandardowy XML
  dla zaawansowanego układu.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: pl
og_description: Dodaj rysunek do Worda szybko przy użyciu C#. Dowiedz się, jak pozycjonować
  rysunek w Wordzie, wstawiać rysunek do pliku docx i dodawać niestandardowy XML dla
  zaawansowanego układu.
og_title: Dodaj rysunek do Worda – Kompletny przewodnik programowania w C#
tags:
- C#
- Word Automation
- Document Generation
title: Dodaj rysunek do Worda – Kompletny przewodnik programowania w C#
url: /pl/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj rysunek do Word – Kompletny przewodnik programowania w C#

Kiedykolwiek potrzebowałeś **dodać rysunek do Word**, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam. W wielu projektach automatyzacji biura brakującym elementem jest ładnie umieszczony obraz lub diagram, który znajduje się wewnątrz niestandardowej części XML. Ten przewodnik pokazuje dokładnie, jak **ustawić rysunek w Word**, wstawić go do pliku *.docx* i nawet zmodyfikować leżący pod spodem niestandardowy XML, aby kształt zachowywał się jak każdy natywny obiekt Word.

Przejdziemy przez praktyczny przykład z użyciem biblioteki GemBox.Document (darmowej dla małych plików, komercyjnej dla większych obciążeń). Po zakończeniu będziesz mieć samodzielny, uruchamialny program, który umieszcza rysunek w współrzędnych X = 50, Y = 200 wewnątrz kontenera z treścią otagowaną. Bez niejasnych „zobacz dokumentację” skrótów — tylko przejrzysty kod, wyjaśnienie dlaczego działa i wskazówki, które możesz od razu skopiować do własnego projektu.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod kompiluje się także z .NET Core 3.1)
- Pakiet NuGet **GemBox.Document** (`Install-Package GemBox.Document`)
- Plik Word startowy (`input.docx`) zawierający już niestandardowy znacznik XML, w którym ma pojawić się rysunek
- Podstawowa znajomość C# (zobaczysz, dlaczego każda linijka ma znaczenie)

> **Pro tip:** Jeśli nie masz dokumentu z wstępnie otagowanym miejscem, możesz go utworzyć w Wordzie, wstawiając *Content Control* → *XML Mapping Pane* → mapując niestandardową część XML. Biblioteka potraktuje ten kontroler jako `TaggedContent`.

## Krok 1 – Załaduj dokument źródłowy

Pierwszą rzeczą, którą robimy, jest otwarcie istniejącego pliku *.docx*. `Document` jest punktem wejścia dla wszystkich operacji GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Dlaczego?* Ładowanie pliku daje dostęp do jego wewnętrznych części, w tym wszelkich kontenerów niestandardowego XML. Bez tego nie moglibyśmy zlokalizować węzła `TaggedContent`, który będzie przechowywał nasz rysunek.

## Krok 2 – Uzyskaj dostęp do otagowanej treści (konteneru niestandardowego XML)

Niestandardowy XML jest przechowywany wewnątrz *content control* w Wordzie. GemBox udostępnia go jako `TaggedContent`.

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Jeśli dokument ma wiele otagowanych sekcji, `TaggedContent` zwraca **pierwszą** z nich. Możesz także przeiterować `doc.TaggedContents`, aby wybrać konkretny znacznik po nazwie.

## Krok 3 – Utwórz element rysunku

`FigureElement` reprezentuje obraz, wykres lub dowolny obiekt wizualny, który Word traktuje jako *shape*. Utworzymy go wewnątrz otagowanego kontenera.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Dlaczego tworzyć rysunek tutaj?* Przypisując go do węzła niestandardowego XML, Word wie, że rysunek należy do tej logicznej sekcji, co jest kluczowe przy późniejszej edycji lub przepływach opartych na kontrolkach treści.

## Krok 4 – Precyzyjnie pozycjonuj rysunek

Word używa punktów (1 pt ≈ 1/72 in) do pozycjonowania. Struktura `PointF` pozwala łatwo ustawić współrzędne X/Y.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Jak pozycjonować shape w Word:** Właściwość `Position` przyjmuje `PointF`, gdzie pierwsza wartość to przesunięcie poziome (lewo), a druga to przesunięcie pionowe (góra) względem marginesu strony. Dostosuj te liczby, aby precyzyjnie ustawić położenie.

## Krok 5 – Wstaw rysunek do drzewa otagowanej treści

Teraz dołączamy rysunek do elementu głównego drzewa niestandardowego XML. To fizycznie dodaje kształt do dokumentu Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

W tym momencie rysunek istnieje w dokumencie, ale nie ma jeszcze źródła obrazu. Dodajmy prosty plik PNG z dysku.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Krok 6 – Zapisz zmodyfikowany dokument

Na koniec zapisujemy zmiany do nowego pliku *.docx*.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Gdy otworzysz `output.docx` w Wordzie, zobaczysz obraz umieszczony dokładnie w (50, 200) wewnątrz bloku niestandardowego XML, który wybrałeś.

### Pełny działający przykład

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Oczekiwany rezultat:** Otwierając `output.docx`, PNG znajduje się dokładnie tam, gdzie określono, zagnieżdżony w części niestandardowego XML. Jeśli przejrzysz XML dokumentu (`.docx` → rozpakuj → `word/document.xml`), zobaczysz element `<w:pict>` z prawidłowymi współrzędnymi `<v:shape>`.

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, gdy dokument ma wiele otagowanych sekcji?

Użyj `doc.TaggedContents`, aby przeiterować i wybrać po nazwie znacznika:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Jak dodać podpis do rysunku?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Czy to działa w Word 2010 i nowszych wersjach?

Tak. GemBox.Document opiera się na standardzie Open XML, który jest kompatybilny z Word 2007 + (w tym 2010, 2013, 2016, 2019 oraz Microsoft 365).

### Co zrobić, gdy trzeba obrócić kształt?

```csharp
figure.Rotation = 45; // degrees
```

### Jak dodać grafikę wektorową zamiast rastrowego obrazu?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro tipy i pułapki

- **Ścieżki plików:** Używaj `Path.Combine`, aby uniknąć twardo zakodowanych separatorów, szczególnie na platformach nie‑Windowsowych.
- **Limity licencji:** Darmowa licencja GemBox ogranicza rozmiar dokumentu do 20 KB. Dla większych plików zakup klucz komercyjny.
- **Wydajność:** Ponowne użycie jednej instancji `Document` przy przetwarzaniu wsadowym znacząco zmniejsza zużycie pamięci.
- **Przepełnienie kształtu:** Jeśli wymiary rysunku przekraczają marginesy strony, Word go przytnie. Dostosuj `figure.Width` i `figure.Height` odpowiednio.

## Podsumowanie

Teraz wiesz, **jak dodać rysunek do Word**, precyzyjnie **pozycjonować rysunek w Word**, oraz manipulować leżącym pod spodem niestandardowym XML, aby kształt zachowywał się jak każdy natywny element. Kompletny, uruchamialny przykład demonstruje każdy krok — od ładowania dokumentu, tworzenia `FigureElement`, ustawiania współrzędnych, dołączania obrazu i ostatecznego zapisu zaktualizowanego *.docx*.

Następnie spróbuj eksperymentować z **insert figure into docx**, dodając wiele rysunków, używając pętli lub generując wykresy w locie. Możesz także zbadać **how to add custom xml** dla bogatszych kontrolek treści lub nauczyć się **how to position shape word** w tabelach i nagłówkach. Możliwości są nieograniczone, a dzięki podstawom opisanym tutaj jesteś gotów automatyzować dokumenty Word jak profesjonalista.

Miłego kodowania i śmiało zostaw komentarz, jeśli napotkasz jakiekolwiek problemy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}