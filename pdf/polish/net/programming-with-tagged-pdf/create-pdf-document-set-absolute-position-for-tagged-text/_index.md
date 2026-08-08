---
category: general
date: 2026-03-24
description: Utwórz dokument PDF i dowiedz się, jak ustawić absolutną pozycję dla
  oznaczonego tekstu. Ten samouczek pokazuje, jak dodać element span, jak dodać oznaczoną
  treść oraz jak pozycjonować tekst na stronie.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: pl
og_description: Utwórz dokument PDF i od razu zobacz, jak ustawić pozycję absolutną,
  dodać element span oraz pozycjonować tekst na stronie z oznakowaną zawartością PDF.
og_title: Utwórz dokument PDF – pozycjonowanie absolutne oznaczonego tekstu
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Utwórz dokument PDF – ustaw absolutną pozycję dla tekstu oznaczonego
url: /pl/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz dokument PDF – Ustaw pozycję bezwzględną dla tekstu otagowanego

Czy kiedykolwiek potrzebowałeś **utworzyć dokument pdf**, który zawiera dostępny, otagowany tekst umieszczony dokładnie tam, gdzie tego chcesz? Być może tworzysz PDF w stylu formularza, w którym etykieta musi znajdować się w precyzyjnych współrzędnych, lub generujesz certyfikat i imię musi idealnie wyrównać się z obrazem tła.  

W tym przewodniku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje **jak dodać otagowaną** treść, **ustawić pozycję bezwzględną** oraz **dodać element span**, abyś mógł **umieścić tekst na stronie** bez zgadywania. Bez zewnętrznych odnośników – tylko kod, który możesz skopiować‑wkleić, oraz wyjaśnienia „dlaczego” stojące za każdą linią.

## Wymagania wstępne

- .NET 6+ (lub .NET Framework 4.6+) z kompilatorem C#  
- Aspose.Pdf for .NET (najświeższa wersja w momencie pisania, 23.12) zainstalowana przez NuGet  
- Podstawowa znajomość składni C#  

Jeśli masz to wszystko, zaczynamy.

---

## Utwórz dokument PDF – ustawianie pozycji bezwzględnej

Pierwszą rzeczą, którą robimy, jest utworzenie pustego `Document`. Ten obiekt reprezentuje cały plik PDF i daje dostęp do drzewa treści otagowanej.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Dlaczego to ważne:**  
`Document` jest korzeniem struktury PDF. Tworząc go najpierw, zapewniamy płótno zarówno dla elementów wizualnych (strony, grafika), jak i struktury logicznej (tagi). Instrukcja `using` gwarantuje prawidłowe zwolnienie pliku, co zapobiega wyciekom uchwytów plików w systemie Windows.

---

## Włącz treść otagowaną (Jak dodać tagi)

Zanim będziemy mogli wstawić jakiekolwiek otagowane elementy, dokument musi być oznaczony jako *tagowany*. Aspose.Pdf automatycznie tworzy obiekt `TaggedContent`, ale nadal trzeba włączyć odpowiednią flagę.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Co dzieje się „pod maską”?**  
Ustawienie `TaggedContent` na `true` informuje czytniki PDF, że plik zawiera drzewo struktury logicznej. Jest to kluczowe dla czytników ekranu oraz dla poprawnego działania metody `SetPosition` na elemencie span.

---

## Pobierz element główny drzewa treści otagowanej

Element główny jest punktem wejścia dla wszystkich tagów strukturalnych (takich jak `<Document>`, `<Section>`, `<Span>`). Można go traktować jako niewidzialne „body” dokumentu PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Dlaczego potrzebujemy elementu głównego:**  
Wszystkie kolejne tagi muszą być dołączone gdzieś w drzewie; w przeciwnym razie nie pojawią się w hierarchii dostępności.

---

## Dodaj element Span – podstawowy blok dla tekstu inline

*Span* jest odpowiednikiem HTML‑owego `<span>` w PDF – idealny dla krótkich fragmentów tekstu, które chcesz precyzyjnie pozycjonować.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Uwaga projektowa:**  
Jeśli potrzebujesz bogatszego formatowania (pogrubienie, kursywa, hiperłącza), możesz owinąć span w `<Paragraph>` lub później użyć obiektów `TextFragment`. Dla pozycjonowania bezwzględnego zwykły span jest najlżejszy.

---

## Ustaw pozycję bezwzględną – X=100, Y=200

Teraz przychodzi najciekawsza część: umieszczenie span w dokładnym miejscu na stronie. System współrzędnych zaczyna się w lewym dolnym rogu (0,0) i używa punktów (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Dlaczego pozycjonowanie bezwzględne?**  
Kiedy potrzebny jest układ piksel‑perfekcyjny – myśl o certyfikatach, fakturach lub formularzach – przepływ relatywny (np. tekst od lewej do prawej) nie wystarcza. `SetPosition` omija normalny przepływ tekstu i przypina element dokładnie tam, gdzie określisz.

---

## Dodaj tekst do span

Po ustawieniu span, wstrzykujemy rzeczywisty ciąg znaków.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Wskazówka:**  
Jeśli potrzebujesz znaków Unicode lub skryptów od prawej do lewej, po prostu przekaż ciąg; Aspose.Pdf automatycznie obsługuje kodowanie.

---

## Dołącz span do elementu głównego

Na koniec przyłączamy span do logicznego drzewa dokumentu, aby stał się częścią finalnego PDF.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Co się stanie, jeśli pominiesz ten krok?**  
Span będzie istnieł w pamięci, ale nigdy nie zostanie zapisany do pliku, więc nie zobaczysz tekstu, a drzewo dostępności będzie niekompletne.

---

## Pełny, uruchamialny przykład

Poniżej znajduje się kompletny program, który możesz wkleić do aplikacji konsolowej. Tworzy on jednosktronicowy PDF, dodaje otagowany span w (100, 200) i zapisuje plik jako `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Oczekiwany wynik:**  
Otwórz `TaggedPositioned.pdf` w dowolnym przeglądarce (Adobe Acrobat, Foxit itp.). Zobaczysz frazę **„Positioned tagged text”** dokładnie 100 pt od lewej krawędzi i 200 pt od dolnej krawędzi strony. Jeśli sprawdzisz panel *Tags*, zobaczysz element `<Span>` wymieniony pod korzeniem dokumentu, co potwierdza, że treść jest prawidłowo otagowana.

---

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli muszę pozycjonować tekst na konkretnej stronie innej niż pierwsza?

Dodaj stronę, której potrzebujesz (`var page = pdfDocument.Pages[3];`) przed wywołaniem `SetPosition`. Span automatycznie przyłączy się do aktywnego kontekstu strony.

### Czy mogę ustawić pozycję w calach lub centymetrach?

`SetPosition` przyjmuje punkty. Konwersję wykonaj według wzorów:  
- **Cale → punkty:** `points = inches * 72`  
- **Centymetry → punkty:** `points = cm * 28.3465`

### Jak zmienić czcionkę lub kolor span?

Po utworzeniu span możesz pobrać jego `TextState` i zmodyfikować go:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Co jeśli dokument już zawiera istniejące tagi?

Wciąż możesz utworzyć nowy span i dołączyć go do dowolnego istniejącego elementu (`rootElement`, konkretnego `<Section>` itp.). Upewnij się tylko, że zachowujesz logiczną hierarchię – czytniki ekranu oczekują dobrze ustrukturyzowanego drzewa.

### Czy to działa z zgodnością PDF/A lub PDF/UA?

Tak. Tagi PDF są podstawowym wymogiem dla PDF/UA. Jeśli potrzebujesz PDF/A, ustaw `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` po zbudowaniu zawartości.

---

## Pro tipy i pułapki

- **Pro tip:** Zawsze dodawaj stronę przed pozycjonowaniem treści. Bez strony `SetPosition` cicho nie zadziała, bo nie ma gdzie renderować.
- **Uważaj na jednostki:** Mieszanie pikseli z projektu UI z punktami PDF spowoduje niewłaściwe rozmieszczenie tekstu. Podwójnie sprawdź konwersję.
- **Wskazówka wydajnościowa:** Jeśli generujesz tysiące PDF‑ów, ponownie używaj jednej instancji `Document` i wywołuj `pdfDocument.Pages.Clear()` pomiędzy uruchomieniami, aby uniknąć nadmiernego przydziału pamięci.
- **Przypomnienie o dostępności:** Tagowanie to nie tylko „miły dodatek”; wiele regulacji (Section 508, EN 301 549) tego wymaga. Użycie `CreateSpanElement` zapewnia, że tekst jest wykrywalny przez technologie wspomagające.

---

## Zakończenie

Właśnie **utworzyliśmy dokument pdf** od podstaw, **ustawiliśmy pozycję bezwzględną**, **dodaliśmy element span** i zademonstrowaliśmy **jak dodać otagowaną** treść, aby **pozycjonować tekst na stronie** z dokładnością do punktu. Pełny przykład jest gotowy do uruchomienia, a wyjaśnienia obejmują zarówno *jak*, jak i *dlaczego* – dokładnie to, czego programiści (i asystenci AI) szukają, gdy potrzebują niezawodnego rozwiązania.

Następnie możesz eksplorować:

- Dodawanie obrazów za tekstem w celu uzyskania znaków wodnych w certyfikatach.  
- Użycie `CreateParagraphElement` dla bloków wielowierszowych, które nadal wymagają pozycjonowania bezwzględnego.  
- Eksport do PDF/UA, aby spełnić rygorystyczne audyty dostępności.  

Śmiało modyfikuj współrzędne, czcionki lub kolory – eksperymentowanie to najszybsza droga do opanowania generowania otagowanych PDF‑ów. Jeśli napotkasz problem, zostaw komentarz poniżej; powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}