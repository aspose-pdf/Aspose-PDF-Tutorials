---
"date": "2025-04-11"
"description": "Dowiedz się, jak efektywnie dodawać i dostosowywać spis treści z numerami stron w dokumentach PDF przy użyciu Aspose.PDF dla platformy .NET, usprawniając w ten sposób nawigację po dokumencie."
"title": "Jak dodać spis treści z numerami stron w plikach PDF za pomocą Aspose.PDF .NET"
"url": "/pl/net/bookmarks-navigation/add-toc-page-numbers-aspose-pdf-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Jak dodać spis treści z numerami stron w plikach PDF za pomocą Aspose.PDF .NET

## Wstęp

W dzisiejszej erze cyfrowej sprawne poruszanie się po długich dokumentach jest niezbędne. Niezależnie od tego, czy zajmujesz się raportami, podręcznikami czy pracami naukowymi, dobrze zorganizowany spis treści (TOC) może znacznie zwiększyć użyteczność. Ten przewodnik pokazuje, jak dodawać i dostosowywać spis treści z numerami stron w plikach PDF przy użyciu Aspose.PDF dla .NET, potężnej biblioteki zaprojektowanej do manipulacji plikami PDF w aplikacjach .NET.

**Czego się nauczysz:**
- Konfigurowanie Aspose.PDF dla .NET
- Ładowanie istniejącego dokumentu PDF do aplikacji
- Tworzenie i dostosowywanie spisu treści z numerami stron
- Zapisywanie zmodyfikowanego pliku PDF

Gotowy, aby usprawnić zarządzanie dokumentami? Zaczynajmy!

### Wymagania wstępne

Przed kontynuowaniem upewnij się, że masz:
- **Biblioteki i zależności**:Plik Aspose.PDF dla .NET dołączono do projektu.
- **Konfiguracja środowiska**: Środowisko programistyczne .NET (np. Visual Studio).
- **Wymagania wstępne dotyczące wiedzy**:Podstawowa znajomość języka C# i obsługi plików w aplikacjach .NET.

### Konfigurowanie Aspose.PDF dla .NET

#### Instalacja
Aby rozpocząć, dodaj bibliotekę Aspose.PDF do swojego projektu, korzystając z jednej z poniższych metod:

**Interfejs wiersza poleceń .NET:**
```bash
dotnet add package Aspose.PDF
```

**Menedżer pakietów:**
```powershell
Install-Package Aspose.PDF
```

**Interfejs użytkownika Menedżera pakietów NuGet:**
Wyszukaj „Aspose.PDF” i zainstaluj najnowszą wersję.

#### Nabycie licencji
Możesz zacząć od bezpłatnej wersji próbnej, aby poznać możliwości Aspose.PDF. W przypadku dłuższego użytkowania rozważ uzyskanie licencji tymczasowej lub jej zakup. Odwiedź [Zakup Aspose](https://purchase.aspose.com/buy) aby uzyskać więcej szczegółów na temat nabywania licencji.

### Przewodnik wdrażania

Gdy już wszystko jest skonfigurowane, możemy dodać do dokumentu PDF niestandardowy spis treści z numerami stron.

#### Załaduj i zmodyfikuj dokument PDF
Najpierw załaduj istniejący dokument PDF do swojej aplikacji. Następnie wstawimy nową stronę na początku tego dokumentu dla naszego spisu treści.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string inFile = "YOUR_DOCUMENT_DIRECTORY/42824.pdf";
string outFile = "YOUR_OUTPUT_DIRECTORY/42824_out.pdf";

// Załaduj dokument PDF
document doc = new Document(inFile);

// Wstaw nową stronę na początku spisu treści
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

#### Utwórz i skonfiguruj informacje o spisie treści
Następnie skonfiguruj spis treści, ustawiając jego tytuł, rozmiar czcionki, styl i dodając prefiks numeracji stron.

```csharp
// Skonfiguruj informacje TOC
tocInfo tocInfo = new TocInfo();
textFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20; // Rozmiar czcionki dla tytułu spisu treści
title.TextState.FontStyle = FontStyles.Bold; // Pogrubiony styl dla podkreślenia
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P"; // Numery stron należy poprzedzać literą „P”
tocPage.TocInfo = tocInfo; // Przypisz informacje TOC do nowej strony
```

#### Dodaj wpisy do spisu treści
Teraz wypełnij spis treści wpisami dla każdej strony dokumentu.

```csharp
for (int i = 1; i < doc.Pages.Count; i++) {
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
textSegment segment2 = new textSegment();

    // Połącz nagłówek ze stroną TOC
    heading2.TocPage = tocPage;

    // Dodaj segment tekstu do nagłówka
    heading2.Segments.Add(segment2); 

    // Ustaw stronę docelową i pozycję dla każdego wpisu
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height; 
    segment2.Text = "P" + i.ToString(); // Tekst niestandardowy z prefiksem „P”

    // Dodaj nagłówek do strony TOC
    tocPage.Paragraphs.Add(heading2);
}
```

#### Zapisz zmodyfikowany dokument PDF
Na koniec zapisz zmodyfikowany dokument z nowo dodanym spisem treści.

```csharp
doc.Save(outFile);
```

### Zastosowania praktyczne

Dodanie niestandardowego spisu treści może znacznie usprawnić nawigację po dokumencie w różnych scenariuszach:
1. **Prace naukowe**:Szybki dostęp do różnych sekcji obszernych dokumentów badawczych.
2. **Instrukcje obsługi**:Popraw komfort użytkowania, umożliwiając szybkie przechodzenie do konkretnych instrukcji lub tematów.
3. **Sprawozdania i propozycje**:Ułatw łatwe odwoływanie się do materiałów podczas prezentacji lub przeglądów.

### Rozważania dotyczące wydajności

Pracując z dużymi plikami PDF, aby uzyskać optymalną wydajność, należy wziąć pod uwagę następujące kwestie:
- **Efektywne zarządzanie pamięcią**:Pozbywaj się przedmiotów niezwłocznie po ich użyciu, aby zwolnić zasoby.
- **Przetwarzanie wsadowe**: Jeżeli to możliwe, obsługuj wiele dokumentów w partiach, aby usprawnić zadania przetwarzania.
- **Operacje asynchroniczne**: W miarę możliwości należy stosować metody asynchroniczne, aby uniknąć blokowania operacji.

### Wniosek

tym samouczku dowiedziałeś się, jak ulepszyć swoje dokumenty PDF, dodając niestandardowy spis treści z numerami stron za pomocą Aspose.PDF dla .NET. Ta możliwość nie tylko usprawnia nawigację po dokumencie, ale także poprawia ogólne wrażenia użytkownika.

Aby jeszcze lepiej poznać możliwości pakietu Aspose.PDF dla platformy .NET, rozważ zapoznanie się z bardziej złożonymi funkcjami i integracjami, gdy już zapoznasz się z podstawami.

### Sekcja FAQ

**1. Czy mogę dodatkowo dostosować wygląd spisu treści?**
Tak, możesz dostosować styl czcionki i kolory, a nawet użyć niestandardowych formatów numeracji, aby dostosować wygląd spisu treści.

**2. Co zrobić, jeśli mój plik PDF ma już zakładki?**
Dostarczony kod skupia się na dodaniu spisu treści, ale można go zintegrować z istniejącymi zakładkami, odpowiednio modyfikując ustawienia docelowe.

**3. Jak postępować z plikami PDF zaszyfrowanymi lub chronionymi hasłem?**
Przed przetworzeniem takich plików należy je odblokować i udostępnić do edycji za pomocą metod deszyfrowania programu Aspose.PDF.

**4. Czy takie podejście nadaje się do przetwarzania wsadowego wielu dokumentów?**
Oczywiście! Możesz przejść przez katalog plików PDF i zastosować tę samą logikę do każdego pliku wydajnie.

**5. Czy mogę zintegrować tę funkcjonalność z aplikacjami internetowymi?**
Tak, Aspose.PDF dla .NET dobrze działa w środowiskach internetowych, takich jak ASP.NET, umożliwiając przetwarzanie plików PDF „w locie”.

### Zasoby
- **Dokumentacja**: [Aspose.PDF dla dokumentacji .NET](https://reference.aspose.com/pdf/net/)
- **Pobierać**: [Najnowsza wersja Aspose.PDF dla .NET](https://releases.aspose.com/pdf/net/)
- **Zakup**: [Kup licencję](https://purchase.aspose.com/buy)
- **Bezpłatna wersja próbna**: [Zacznij od bezpłatnego okresu próbnego](https://releases.aspose.com/pdf/net/)
- **Licencja tymczasowa**: [Uzyskaj tymczasową licencję](https://purchase.aspose.com/temporary-license/)
- **Forum wsparcia**: [Dołącz do społeczności Aspose](https://forum.aspose.com/c/pdf/10)

Mamy nadzieję, że ten przewodnik był pomocny w udoskonaleniu Twoich możliwości zarządzania dokumentami PDF. Miłego kodowania!


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}