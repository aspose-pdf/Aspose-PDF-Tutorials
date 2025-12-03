---
date: '2025-12-01'
description: Dowiedz się, jak tworzyć dostępne pliki PDF, generować tabele PDF oraz
  oznaczać pliki PDF dla czytników ekranu przy użyciu Aspise.PDF dla Javy.
keywords:
- accessible PDFs with Java
- Aspose.PDF for Java
- tagged PDF creation
language: pl
title: Tworzenie dostępnego PDF z oznaczonymi treściami w Javie przy użyciu Aspose.PDF
url: /java/advanced-features/create-accessible-pdfs-tagged-content-java-aspose-pdf/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Utwórz dostępny PDF z oznaczonymi treściami w Javie przy użyciu Aspose.PDF

Tworzenie **accessible PDF** jest niezbędne, aby zapewnić, że wszyscy użytkownicy, w tym osoby korzystające z technologii wspomagających, mogą czytać i wchodzić w interakcję z Twoją treścią. W tym samouczku dowiesz się, jak **create accessible PDF** z oznaczonymi treściami, generować tabele PDF oraz ustawiać język dokumentu, aby czytniki ekranu mogły poprawnie interpretować strukturę.

## Szybkie odpowiedzi
- **Jaką bibliotekę powinienem używać?** Aspose.PDF for Java.  
- **Jak długo trwa implementacja?** Około 15‑20 minut dla podstawowego oznaczonego PDF.  
- **Czy potrzebna jest licencja?** Bezpłatna wersja próbna działa w fazie rozwoju; stała licencja jest wymagana w produkcji.  
- **Czy mogę generować tabele?** Tak – API umożliwia tworzenie i stylizowanie tabel PDF z oznaczoną strukturą.  
- **Jak sprawić, by PDF był czytelny dla czytników ekranu?** Oznacz treść, ustaw język i podaj tekst alternatywny dla elementów strukturalnych.

## Co to jest „create accessible pdf”?
**Accessible PDF** zawiera logiczną strukturę (tagi), opisującą nagłówki, tabele, akapity i inne elementy. Struktura ta umożliwia czytnikom ekranu i innym narzędziom wspomagającym prezentację dokumentu w sposób zrozumiały dla użytkowników z wadami wzroku lub poznawczymi.

## Dlaczego warto oznaczyć PDF?
Oznaczanie PDF (proces **how to tag pdf**) daje Ci:
- **Ulepszoną nawigację** dla czytników ekranu i użytkowników korzystających z klawiatury.  
- **Zgodność** z wytycznymi WCAG 2.1 oraz standardem dostępności PDF/UA.  
- **Lepszą przeszukiwalność**, ponieważ tekst jest indeksowany semantycznie.  

## Wymagania wstępne
Zanim rozpoczniesz, upewnij się, że masz:
- Zainstalowany Java Development Kit (JDK).  
- IDE, takie jak IntelliJ IDEA lub Eclipse.  
- Podstawową znajomość Javy oraz koncepcji PDF.  

### Wymagane biblioteki i zależności
Dodaj Aspose.PDF for Java do swojego projektu przy użyciu Maven lub Gradle.

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Uzyskanie licencji
Aspose.PDF for Java oferuje bezpłatną wersję próbną. Tymczasową licencję możesz uzyskać [tutaj](https://purchase.aspose.com/temporary-license/). Do użytku produkcyjnego należy zakupić pełną licencję.

## Konfiguracja Aspose.PDF for Java
Jeśli nie korzystasz z Maven/Gradle, pobierz plik JAR ze [strony wydania Aspose](https://releases.aspose.com/pdf/java/) i dodaj go do ścieżki kompilacji projektu.

Oto prosty fragment kodu, który weryfikuje konfigurację, tworząc pusty PDF:

```java
import com.aspose.pdf.Document;

public class PdfCreator {
    public static void main(String[] args) {
        // Initialize Aspose.PDF
        Document doc = new Document();
        
        // Save the empty document to check setup
        doc.save("output/EmptyDocument.pdf");
        
        System.out.println("Setup complete and document created successfully.");
    }
}
```

## Przewodnik implementacji

### Tworzenie nowego PDF z oznaczonymi treściami
**Przegląd** – Oznaczone treści zapewniają logiczną hierarchię, która zwiększa dostępność. Poniższe kroki prowadzą przez tworzenie PDF, włączanie oznaczania i wypełnianie stylizowanej tabeli.

#### Krok 1: Inicjalizacja dokumentu i włączenie oznaczania
Najpierw utwórz instancję `Document` i uzyskaj interfejs `ITaggedContent`. Dodatkowo **set the PDF language** (krok **set pdf language**) tak, aby czytniki ekranu znały lokalizację dokumentu.

```java
import com.aspose.pdf.*;

public class TaggedPdfCreator {
    public static void main(String[] args) {
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        // Create a new PDF document
        Document document = new Document();

        // Obtain tagged content
        ITaggedContent taggedContent = document.getTaggedContent();
        
        // Set the title and language for accessibility purposes
        taggedContent.setTitle("Example table row style");
        taggedContent.setLanguage("en-US");

        // Proceed to add structured elements
    }
}
```

#### Krok 2: Dodawanie elementów struktury (How to generate PDF table)
Następnie zdefiniuj element główny i utwórz strukturę tabeli z nagłówkiem, ciałem i stopką. To demonstruje funkcję **generate pdf table**, zachowując pełne oznaczenie treści.

```java
import com.aspose.pdf.tagged.logicalstructure.elements.bls.*;

// Get root structure element
StructureElement rootElement = taggedContent.getRootElement();

// Create a new table structure element
TableElement tableElement = taggedContent.createTableElement();
rootElement.appendChild(tableElement);

// Add header, body, and footer to the table
TableTHeadElement tableTHeadElement = tableElement.createTHead();
TableTBodyElement tableTBodyElement = tableElement.createTBody();
TableTFootElement tableTFootElement = tableElement.createTFoot();
```

#### Krok 3: Wypełnianie elementów tabeli (Styling rows for screen reader PDF)
Teraz dodajemy wiersze, stylizujemy je i podajemy tekst alternatywny. Tekst alternatywny zapewnia zrozumiałość tabeli dla użytkowników **screen reader PDF**.

```java
int rowCount = 7;
int colCount = 3;

// Add a header row with column titles
TableTRElement headTrElement = tableTHeadElement.createTR();
headTrElement.setAlternativeText("Head Row");
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTHElement thElement = headTrElement.createTH();
    thElement.setText(String.format("Head %s", colIndex));
}

// Add rows to the table body with styled cells
for (int rowIndex = 0; rowIndex < rowCount; rowIndex++) {
    TableTRElement trElement = tableTBodyElement.createTR();
    trElement.setAlternativeText(String.format("Row %s", rowIndex));

    // Set row styles
    trElement.setBackgroundColor(Color.getLightSeaGreen());
    trElement.setBorder(new BorderInfo(BorderSide.All, 0.75F, Color.getDarkGray()));
    trElement.setDefaultCellBorder(new BorderInfo(BorderSide.All, 0.50F, Color.getBlue()));
    trElement.setMinRowHeight(100.0);
    trElement.setFixedRowHeight(120.0);

    // Set default text state for cells in this row
    TextState cellTextState = new TextState();
    cellTextState.setForegroundColor(Color.getRed());
    trElement.setDefaultCellTextState(cellTextState);

    // Add cells to the row
    for (int colIndex = 0; colIndex < colCount; colIndex++) {
        TableTDElement tdElement = trElement.createTD();
        tdElement.setText(String.format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}

// Add a footer row to the table
TableTRElement footTrElement = tableTFootElement.createTR();
footTrElement.setAlternativeText("Foot Row");
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTDElement tdElement = footTrElement.createTD();
    tdElement.setText(String.format("Foot %s", colIndex));
}
```

### Zapisywanie dokumentu PDF
Na koniec zapisz dokument. Zapisany plik zachowuje wszystkie tagi, ustawienia języka oraz strukturę tabeli, co czyni go w pełni gotowym do **create accessible pdf** i dystrybucji.

```java
// Save the tagged PDF document
document.save(outputDir + "/StyleTableRow.pdf");
System.out.println("Document saved successfully.");
```

## Praktyczne zastosowania
Tworzenie dostępnych PDF jest kluczowe w wielu rzeczywistych scenariuszach:

1. **Materiały edukacyjne** – Zapewnij inkluzywne podręczniki i materiały dla wszystkich studentów.  
2. **Publikacje rządowe** – Spełnij wymogi prawne dotyczące dostępności dokumentów publicznych.  
3. **Raporty korporacyjne** – Umożliw akcjonom i pracownikom dostęp do sprawozdań finansowych przy użyciu czytników ekranu.  

## Wydajność
Podczas pracy z dużymi PDF:

- Monitoruj zużycie pamięci; zwalniaj zasoby na bieżąco.  
- Minimalizuj liczbę dynamicznych elementów, które dodajesz.  
- Stosuj najlepsze praktyki Javy dotyczące garbage collection i ponownego użycia obiektów.  

## Typowe problemy i rozwiązania
| Problem | Rozwiązanie |
|---------|-------------|
| Tagi nie pojawiają się w czytniku PDF | Upewnij się, że `taggedContent` został pobrany oraz że `setTitle`/`setLanguage` zostały wywołane przed dodaniem elementów. |
| Komórki tabeli nie mają tekstu alternatywnego | Użyj `setAlternativeText` dla każdego `TableTRElement` oraz dla wierszy nagłówka/stopki. |
| Duże pliki powodują OutOfMemoryError | Przetwarzaj dokument w sekcjach lub zwiększ rozmiar sterty JVM (`-Xmx`). |

## Najczęściej zadawane pytania

**Q: Jak mogę zweryfikować, że mój PDF jest naprawdę dostępny?**  
A: Skorzystaj z narzędzi takich jak Adobe Acrobat Accessibility Checker lub otwórz plik w czytniku ekranu (NVDA, JAWS), aby potwierdzić prawidłową nawigację.

**Q: Czy Aspose.PDF obsługuje inne języki niż angielski?**  
A: Tak. Ustaw kod języka za pomocą `taggedContent.setLanguage("fr-FR")` dla francuskiego, `es-ES` dla hiszpańskiego itp.

**Q: Czy mogę dodać obrazy z tekstem alternatywnym do oznaczonego PDF?**  
A: Oczywiście. Użyj klasy `Image` i ustaw jej właściwość `AlternativeText`, aby opisać zawartość wizualną.

**Q: Czy istnieje limit liczby wierszy, które mogę wygenerować w tabeli PDF?**  
A: Nie ma sztywnego limitu, ale bardzo duże tabele mogą zwiększyć zużycie pamięci; rozważ paginację lub podział dokumentu.

**Q: Czy wygenerowany PDF będzie działał we wszystkich czytnikach ekranu?**  
A: Gdy tagi, język i tekst alternatywny są poprawnie ustawione, PDF spełnia standard PDF/UA i powinien być czytelny przez większość głównych czytników ekranu.

## Podsumowanie
Masz teraz kompletny, krok po kroku przewodnik, jak **create accessible PDF** z oznaczonymi treściami, generować stylizowane tabele i zapewnić kompatybilność z czytnikami ekranu. Dzięki Aspose.PDF for Java możesz wbudować dostępność bezpośrednio w proces generowania PDF, dostarczając inkluzywną treść każdej grupie odbiorców.

### Kolejne kroki
- Poznaj dodatkowe funkcje oznaczania, takie jak nagłówki, listy i linki.  
- Zintegruj ten przepływ pracy z istniejącymi usługami Java lub zadaniami wsadowymi.  
- Podziel się doświadczeniami i zadawaj pytania na [forum Aspose PDF](https://forum.aspose.com/c/pdf/10).

---

**Ostatnia aktualizacja:** 2025-12-01  
**Testowano z:** Aspose.PDF for Java 25.3  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
