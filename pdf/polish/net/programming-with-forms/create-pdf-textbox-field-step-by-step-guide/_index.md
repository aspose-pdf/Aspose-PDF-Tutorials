---
category: general
date: 2026-06-21
description: Utwórz pole tekstowe PDF przy użyciu C# i dowiedz się, jak duplikować
  pole formularza PDF lub dodać pole tekstowe do formularza PDF w zaledwie kilku linijkach
  kodu.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: pl
og_description: Szybko utwórz pole tekstowe PDF. Ten przewodnik pokazuje, jak skopiować
  pole formularza PDF i dodać pole tekstowe do formularza PDF przy użyciu nowoczesnej
  biblioteki PDF w C#.
og_title: Utwórz pole tekstowe PDF – Kompletny samouczek C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Tworzenie pola tekstowego PDF – przewodnik krok po kroku
url: /pl/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Textbox Field – Kompletny samouczek C#

Kiedykolwiek potrzebowałeś **create PDF textbox field**, ale nie byłeś pewien, które wywołania API użyć? Nie jesteś sam. Niezależnie od tego, czy tworzysz portal do podpisywania umów, czy prosty arkusz zbierania danych, dodawanie interaktywnych pól tekstowych do PDF jest podstawową umiejętnością każdego developera automatyzacji formularzy.  

W tym przewodniku przeprowadzimy praktyczny przykład, który nie tylko **adds textbox to PDF form**, ale także pokaże, jak **duplicate PDF form field**, aby to samo wprowadzenie pojawiało się na wielu stronach. Po zakończeniu będziesz mieć uruchamialny program, który możesz wstawić do dowolnego projektu .NET.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (kod działa również z .NET Core)  
- Nowoczesna biblioteka PDF dla C# – poniższy fragment używa **PDFTron SDK**, ale koncepcje można zastosować w iText 7, PdfSharp lub innych bibliotekach.  
- Visual Studio 2022 (lub dowolne IDE, które lubisz)

To wszystko – bez dodatkowych usług, bez niejasnych zależności. Jeśli już masz PDF, który chcesz rozszerzyć, po prostu wskaż go w kodzie.

---

## Krok 1: Skonfiguruj projekt i zaimportuj SDK

Najpierw utwórz aplikację konsolową:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Dodaj pakiet PDFTron NuGet:

```bash
dotnet add package PDFTron.NET
```

Teraz otwórz `Program.cs` i zaimportuj niezbędne przestrzenie nazw:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** Jeśli używasz innej biblioteki, zamień instrukcje `using` na ich odpowiedniki (np. `iText.Kernel.Pdf` dla iText 7).

## Krok 2: Zainicjalizuj dokument PDF i formularz

Zaczniemy od nowego PDF, który zawiera dwie strony – stronę źródłową z oryginalnym polem tekstowym oraz stronę docelową dla duplikatu.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

Obiekt `Form` to miejsce, w którym znajdują się wszystkie pola interaktywne. Jeśli dokument nie miał jeszcze formularza, `GetForm()` tworzy go dla nas.

## Krok 3: **Create PDF Textbox Field** na pierwszej stronie

Teraz przechodzi do sedna naszego samouczka – tworzenia pola tekstowego. Współrzędne prostokąta podawane są w punktach (1 cal = 72 punkty). Przykład umieszcza pole w pobliżu górnego‑środka pierwszej strony.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Dlaczego od razu ustawiamy `Value`? Wstępne wypełnienie pola daje użytkownikom wskazówkę co do oczekiwanego wpisu i jednocześnie pokazuje, że pole jest w pełni funkcjonalne.

## Krok 4: Dodaj pole do formularza – **Add Textbox to PDF Form**

Następnie rejestrujemy pole w formularzu, używając logicznej nazwy. Ta nazwa będzie używana później, gdy będziesz musiał odczytać lub zmodyfikować dane pola programowo.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Wybór przejrzystej nazwy (np. `"multiBox"`) ułatwia późniejsze zrozumienie kodu, szczególnie gdy masz dziesiątki pól.

## Krok 5: **Duplicate PDF Form Field** na innej stronie

Częstym wymaganiem jest wyświetlenie tego samego pola na wielu stronach – pomyśl o polu „Customer Name”, które pojawia się na każdej stronie faktury. PDFTron pozwala nam sklonować adnotację widgetu, będącą wizualną reprezentacją pola.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Sklonowany widget korzysta z tych samych danych podstawowych co oryginalne pole tekstowe. Gdy użytkownik wpisze coś w jednej instancji, druga aktualizuje się automatycznie – to magia **duplicate PDF form field**.

## Krok 6: Zapisz dokument i posprzątaj

Na koniec zapisz PDF na dysku i zamknij środowisko PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Uruchomienie programu generuje dwustronicowy PDF (`output.pdf`). Otwórz go w Adobe Acrobat Reader, kliknij pole tekstowe na stronie 1, wpisz coś, a następnie przejdź do strony 2 – ten sam tekst pojawi się natychmiast. To w pełni funkcjonalny przykład **create pdf textbox field** z duplikowanym polem.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Oczekiwany wynik:** Plik o nazwie `output.pdf` zawierający dwie strony. Obie strony wyświetlają to samo edytowalne pole tekstowe oznaczone „Sample”. Edycja jednego pola natychmiast aktualizuje drugie.

---

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję pola na *więcej* niż dwóch stronach?

Po prostu powtórz kroki klonowania i dodawania dla każdej dodatkowej strony. Obiekt danych pozostaje ten sam, więc wszystkie widgety są zsynchronizowane.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Jak zmienić wygląd (czcionkę, obramowanie, tło)?

Każdy `Widget` posiada metody `SetBorderColor`, `SetBorderWidth` oraz `SetBackgroundColor`. Możesz także przypisać ciąg domyślnego wyglądu (`DA`), aby kontrolować czcionkę i rozmiar.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Czy mogę ustawić pole jako tylko do odczytu po wypełnieniu przez użytkownika?

Tak. Ustaw flagę `ReadOnly` na polu po zebraniu danych lub przełącz ją w zależności od przepływu pracy.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Co z PDF‑ami, które już zawierają formularz?

Jeśli dokument już posiada AcroForm, `doc.GetForm()` po prostu go zwraca. Możesz wtedy dodawać nowe pola bez zakłócania istniejących. Upewnij się tylko, że używasz unikalnych nazw pól.

---

## Wskazówki dla projektów w rzeczywistym świecie

- **Naming convention:** Dodawaj prefiks do nazw pól, wskazujący na stronę lub sekcję (np. `invoice_customer_name`), aby uniknąć kolizji.  
- **Validation:** Użyj akcji JavaScript (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) jeśli potrzebujesz walidacji po stronie klienta.  
- **Performance:** Pracując z dużymi PDF‑ami, wywołaj `doc.Lock()` przed operacjami masowymi, aby zmniejszyć obciążenie I/O.  
- **Accessibility:** Ustaw właściwość `AlternateName`, aby czytniki ekranu mogły opisać pole.

---

## Zakończenie

Właśnie **created a PDF textbox field**, pokazaliśmy, jak **duplicate PDF form field** na wielu stronach i przedstawiliśmy najprostszy sposób **add textbox to PDF form** przy użyciu C#. Pełny, uruchamialny kod znajduje się powyżej i możesz go rozbudować o stylizację, walidację lub dodatkowe strony w razie potrzeby.

Gotowy na kolejny krok? Spróbuj osadzić listę rozwijaną (`ChoiceField`) lub widget podpisu, albo zbadaj, jak spłaszczyć formularz po wprowadzeniu danych w celu archiwizacji. PDFTron SDK (lub dowolna podobna biblioteka) dostarcza elementy konstrukcyjne — twoja wyobraźnia decyduje o ostatecznym kształcie.

Jeśli napotkasz problem, zostaw komentarz poniżej lub sprawdź oficjalną dokumentację biblioteki; zawiera ona mnóstwo przykładów uzupełniających to, co tutaj omówiliśmy. Szczęśliwego kodowania i niech twoje formularze zawsze będą zsynchronizowane!

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak utworzyć PDF za pomocą Aspose – Dodaj pole formularza i strony](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Dodaj pole formularza w dokumencie PDF przy użyciu Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Dodaj pole formularza w dokumencie PDF przy użyciu Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}