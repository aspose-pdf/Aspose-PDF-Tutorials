---
"date": "2025-04-11"
"description": "Dowiedz się, jak skutecznie dodawać znaczniki daty i godziny lub adnotacje do dokumentów PDF za pomocą Aspose.PDF dla .NET. Ulepsz zarządzanie dokumentami dzięki tym prostym krokom."
"title": "Dodawanie znaczników daty i godziny do plików PDF za pomocą Aspose.PDF dla .NET"
"url": "/pl/net/document-manipulation/aspose-pdf-net-date-time-stamps-annotations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Dodawanie znaczników daty i godziny do plików PDF za pomocą Aspose.PDF dla .NET

## Wstęp

W dzisiejszej erze cyfrowej skuteczne zarządzanie dokumentami jest kluczowe dla firm i osób prywatnych. Dodawanie znaczników daty i godziny lub adnotacji do plików PDF może poprawić integralność i organizację danych. Ten samouczek pokazuje, jak zintegrować te funkcje za pomocą Aspose.PDF dla .NET.

**Najważniejsze wnioski:**
- Dodaj bieżącą datę i godzinę jako znaczniki tekstowe na określonej stronie pliku PDF.
- Utwórz adnotacje tekstowe w wybranych miejscach dokumentu.
- Stosuj najlepsze praktyki, aby uzyskać optymalną wydajność Aspose.PDF dla .NET.

## Wymagania wstępne
Przed rozpoczęciem upewnij się, że masz:

### Wymagane biblioteki i wersje
- **Aspose.PDF dla .NET**: Solidna biblioteka do manipulacji PDF bez Adobe Acrobat. Użyj wersji 21.x lub nowszej.

### Wymagania dotyczące konfiguracji środowiska
- Środowisko programistyczne z .NET Framework 4.5+ lub .NET Core 2.0+
- Visual Studio lub inne środowisko IDE obsługujące programowanie w języku C#

### Wymagania wstępne dotyczące wiedzy
- Podstawowa znajomość struktur projektów C# i .NET
- Znajomość obsługi plików w strukturze katalogów

## Konfigurowanie Aspose.PDF dla .NET
Zainstaluj Aspose.PDF korzystając z jednej z następujących metod:

**Korzystanie z interfejsu wiersza poleceń .NET:**
```bash
dotnet add package Aspose.PDF
```

**Korzystanie z Menedżera pakietów:**
```powershell
Install-Package Aspose.PDF
```

**Za pomocą interfejsu użytkownika Menedżera pakietów NuGet:**
- Otwórz Menedżera pakietów NuGet w swoim środowisku IDE.
- Wyszukaj „Aspose.PDF” i zainstaluj najnowszą wersję.

### Etapy uzyskania licencji
Aby w pełni wykorzystać Aspose.PDF:
1. **Bezpłatna wersja próbna:** Pobierz tymczasową licencję, aby zapoznać się ze wszystkimi funkcjami.
2. **Licencja tymczasowa:** W razie konieczności poproś o rozszerzoną licencję ewaluacyjną.
3. **Zakup:** Kup licencję na użytkowanie długoterminowe na stronie internetowej Aspose.

Zainicjuj swoją licencję w kodzie:
```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to License File");
```

## Przewodnik wdrażania
Dodajmy znaczniki daty i godziny do plików PDF.

### Funkcja 1: Dodaj znacznik daty i godziny do pliku PDF
Funkcja ta dodaje bieżącą datę i godzinę w postaci znacznika tekstowego na pierwszej stronie określonego dokumentu PDF.

#### Wdrażanie krok po kroku

##### 1. Otwórz istniejący dokument PDF
Załaduj dokument docelowy:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/AddTextStamp.pdf");
```

##### 2. Pobierz bieżącą datę i godzinę jako ciąg
Sformatuj bieżącą datę i godzinę:
```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

##### 3. Utwórz stempel tekstowy z bieżącą datą i godziną
Utwórz `TextStamp` wystąpienie przy użyciu sformatowanego ciągu:
```csharp
TextStamp textStamp = new TextStamp(annotationText);
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

##### 4. Dodaj stempel tekstowy do pierwszej strony
Dodaj pieczątkę na pierwszej stronie dokumentu:
```csharp
document.Pages[1].AddStamp(textStamp);
```

##### 5. Utwórz i dodaj adnotację FreeTextAnnotation (opcjonalnie)
W przypadku bardziej złożonych adnotacji utwórz `FreeTextAnnotation`:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(document.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance)
{
    Name = "Stamp",
    Contents = textStamp.Value
};
textAnnotation.Border = new Border(textAnnotation) { Width = 0 };
document.Pages[1].Annotations.Add(textAnnotation);
```

##### 6. Zapisz zmodyfikowany dokument
Zapisz zmiany:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/AddDateTimeStamp_out.pdf";
document.Save(outputDir);
```

### Funkcja 2: Dodaj adnotację FreeText do pliku PDF
Dodawaj dowolne adnotacje tekstowe w dowolnym miejscu dokumentu PDF.

#### Wdrażanie krok po kroku

##### 1. Otwórz istniejący dokument PDF
Załaduj dokument docelowy:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/Sample.pdf");
```

##### 2. Zdefiniuj obszar prostokąta do adnotacji
Określ, gdzie na stronie chcesz umieścić adnotację:
```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(100, 400, 200, 450);
```

##### 3. Utwórz adnotację FreeTextAnnotation o określonym wyglądzie i lokalizacji
Zainicjuj adnotację, podając żądane ustawienia tekstu i wyglądu:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 12, System.Drawing.Color.Blue);
FreeTextAnnotation freeTextAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], rect, default_appearance)
{
    Contents = "This is a sample annotation",
    Title = "Sample Annotation"
};
```

##### 4. Ustaw styl obramowania i dodaj adnotację
Upewnij się, że styl obramowania odpowiada Twoim potrzebom (w tym przypadku jest niewidoczny):
```csharp
freeTextAnnotation.Border = new Border(freeTextAnnotation) { Width = 0 };
pdfDocument.Pages[1].Annotations.Add(freeTextAnnotation);
```

##### 5. Zapisz zmodyfikowany dokument
Zapisz dokument z nowo dodaną adnotacją:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/FreeTextAnnotation_out.pdf";
document.Save(outputDir);
```

## Zastosowania praktyczne
Dodawanie znaczników daty i adnotacji do plików PDF jest przydatne w wielu branżach:
- **Dokumenty prawne**:Zapewnia zgodność poprzez oznaczanie zmian znacznikami czasu.
- **Prace naukowe**:Ułatwia wspólną edycję dzięki adnotacjom.
- **Rejestry finansowe**:Prowadzi dokładne ścieżki audytu z raportami oznaczonymi znacznikiem czasu.
- **Dokumentacja techniczna**:Podświetla aktualizacje i ważne uwagi w instrukcjach.

## Rozważania dotyczące wydajności
Aby uzyskać optymalną wydajność podczas korzystania z Aspose.PDF dla .NET:
- **Przetwarzanie wsadowe**:Przetwarzaj wiele plików PDF w partiach, aby zmniejszyć obciążenie.
- **Zarządzanie pamięcią**: Używać `Dispose` metody zwalniania zasobów pamięci po przetworzeniu każdego dokumentu.
- **Zoptymalizowane czcionki i obrazy**: Aby zmniejszyć rozmiar pliku, należy ograniczyć rodzaje czcionek i rozdzielczości obrazów.

## Wniosek
Zintegrowanie Aspose.PDF dla .NET umożliwia dodawanie funkcji datowania i adnotacji do dokumentów PDF, zwiększając funkcjonalność. Te narzędzia poprawiają integralność danych i usprawniają zarządzanie dokumentami.

Eksperymentuj z różnymi konfiguracjami i odkryj dodatkowe funkcje udostępniane przez Aspose.PDF, które spełnią Twoje potrzeby.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}