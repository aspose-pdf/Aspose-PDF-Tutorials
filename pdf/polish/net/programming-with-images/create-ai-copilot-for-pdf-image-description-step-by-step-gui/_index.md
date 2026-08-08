---
category: general
date: 2026-08-04
description: Utwórz AI Copilot, aby generować opisy obrazów dla plików PDF. Dowiedz
  się, jak konfigurować opcje obrazu OpenAI i efektywnie wyodrębniać opisy obrazów.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: pl
lastmod: 2026-08-04
og_description: Utwórz AI Copilot, aby generować opisy obrazów dla plików PDF. Ten
  poradnik pokazuje, jak skonfigurować opcje obrazu OpenAI, uruchomić copilot i wyodrębnić
  opis obrazu w C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Stwórz AI Copilot do opisu obrazów w PDF – kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: Stwórz AI Copilot do opisu obrazów w PDF – przewodnik krok po kroku
url: /pl/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz AI Copilot do opisu obrazów w PDF – kompletny przewodnik

Jeśli potrzebujesz **utworzyć AI Copilot**, który automatycznie generuje opisy dla obrazów osadzonych w pliku PDF, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Nauczysz się konfigurować opcje obrazu OpenAI, uruchamiać copilota i **wyodrębniać opis obrazu** bez wychodzenia z projektu C#.

Generowanie treści tekstowej dla obrazów w PDF jest powszechnym wymogiem w zakresie dostępności, indeksowania treści oraz automatycznego raportowania. Po zakończeniu tego samouczka będziesz posiadać wielokrotnego użytku komponent, który **generuje opis obrazu** dla dowolnego dokumentu PDF, na który wskażesz.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 lub nowszy zainstalowany  
* Licencję Aspose.Pdf.AI (lub darmową wersję próbną)  
* Klucz API OpenAI, którego może używać klient Aspose  
* Visual Studio 2022 (lub dowolne IDE obsługujące C#)  

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Pdf.AI`.

## Krok 1: Skonfiguruj klienta Aspose.Pdf.AI

Pierwszym krokiem jest utworzenie klienta AI z danymi uwierzytelniającymi. Klient obsługuje komunikację z usługą OpenAI w tle.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Dlaczego to ważne:** `AiClient` kapsułkuje wszystkie ustawienia na poziomie żądania (klucz API, limit czasu, polityka ponawiania). Utworzenie go raz i ponowne użycie w wielu instancjach copilotów zmniejsza obciążenie i zapewnia spójne uwierzytelnianie.

## Krok 2: Utwórz copilot opisu obrazu

Teraz tworzysz **AI copilot**, który odczyta PDF i wygeneruje opis dla każdego obrazu. Metoda fabryczna `CreateImageDescriptionCopilot` przyjmuje klienta oraz zestaw opcji definiujących sposób generowania opisu.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Dlaczego to ważne:**  
* `OpenAIImageDescriptionOptions` (czyli **OpenAI image options**) pozwalają precyzyjnie dostroić model językowy. Dostosowanie temperatury lub modelu może poprawić trafność opisów technicznych diagramów w porównaniu z naturalnymi zdjęciami.  
* Określenie ścieżki dokumentu informuje copilot, który PDF ma skanować. Copilot wyodrębnia każdy obraz rastrowy, wysyła go do modelu i zwraca opis czytelny dla człowieka.

## Krok 3: Asynchronicznie pobierz wygenerowany opis

Copilot działa asynchronicznie, ponieważ może wymagać przesłania kilku megabajtów danych obrazu i oczekiwania na odpowiedź modelu. Użyj `await`, aby zapewnić zakończenie wywołania przed dostępem do wyniku.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Dlaczego to ważne:** Metoda zwraca `Dictionary<int, string>`, które mapuje każdą stronę (lub indeks obrazu) na jego opis. Obsługa `AiException` pozwala wyświetlić błędy sieciowe lub limitów zamiast awarii aplikacji.

## Krok 4: Wyświetl lub zapisz opis

Możesz wypisać opisy w konsoli, pliku logu lub osadzić je ponownie w PDF jako tekst alternatywny dla dostępności. Poniżej szybki przykład zapisujący wynik do pliku JSON do późniejszego wykorzystania.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Dlaczego to ważne:** Przechowywanie wyniku jako JSON zachowuje powiązanie między każdą stroną a jej opisem, co ułatwia dalsze procesy (indeksowanie wyszukiwania, renderowanie UI itp.) w konsumowaniu danych.

## Obsługa wielu obrazów na jednej stronie

Jeśli strona zawiera kilka obrazów, copilot zwraca połączony opis oddzielony znakami nowej linii. Aby je podzielić, przeanalizuj surowy wynik i podziel go po `\n\n` (podwójny znak nowej linii). Oto metoda pomocnicza:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Następnie możesz iterować po każdym pojedynczym opisie obrazu i zapisywać je osobno, jeśli zajdzie taka potrzeba.

## Przypadek brzegowy: duże PDF‑y i zarządzanie limitem czasu

Przetwarzanie PDF‑a większego niż 100 MB może przekroczyć domyślne limity czasu HTTP. Dostosuj ustawienie limitu czasu klienta przy tworzeniu `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Zwiększenie limitu czasu zapobiega przedwczesnemu zakończeniu, gdy usługa przetwarza wiele obrazów wysokiej rozdzielczości.

## Pro tip: buforuj wyniki, aby obniżyć koszty

OpenAI pobiera opłatę za token, a opis obrazu może być powtarzalny w kolejnych wersjach tego samego raportu. Buforuj wyjściowy JSON i używaj go ponownie, gdy hash PDF‑a zgadza się z wcześniej przetworzonym plikiem. Dzięki temu oszczędzasz pieniądze i przyspieszasz kolejne uruchomienia.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Zapisz hash obok pliku JSON; jeśli hash się zgadza przy późniejszym uruchomieniu, pomiń wywołanie AI.

## Pełny, gotowy do uruchomienia przykład

Łącząc wszystko razem, oto samodzielna aplikacja konsolowa, którą możesz wkleić do nowego projektu .NET.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Oczekiwany wynik (skrócony)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

Program odczytuje `AnnualReport.pdf`, tworzy **AI copilot** i zapisuje plik JSON, który mapuje każdą stronę na wygenerowany opis.

## Często zadawane pytania

* **Czy to działa z zaszyfrowanymi PDF‑ami?**  
  Tak, ale musisz podać hasło przy tworzeniu copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Czy mogę ograniczyć przetwarzanie do konkretnych stron?**  
  Użyj `imageOptions.WithPageRange(1, 10)`, aby ograniczyć copilot do stron 1‑10.

* **Co jeśli obraz zawiera tekst?**  
  Model stara się opisać treść wizualną; do ekstrakcji tekstu w stylu OCR powinieneś użyć `CreateTextExtractionCopilot`.

## Zakończenie

Teraz wiesz, jak **utworzyć AI Copilot**, który **generuje opis obrazu** dla plików PDF, jak skonfigurować **OpenAI image options** oraz jak programowo **wyodrębniać opis obrazu** w C#. Pełny przykład demonstruje najlepsze praktyki, takie jak obsługa asynchroniczna, zarządzanie błędami i buforowanie wyników.

Następnie możesz rozważyć:

* Dodanie wygenerowanych opisów z powrotem do PDF jako tekst alternatywny w celu poprawy dostępności (`PdfDocument` → `PdfImage.AlternativeText`).  
* Wykorzystanie tego samego wzorca copilot do **generowania raportów PDF z opisem obrazów** w trybie wsadowym.  
* Eksperymentowanie z różnymi modelami OpenAI lub ustawieniami temperatury, aby dopasować styl opisu.

Śmiało dostosowuj kod, testuj większe dokumenty i integruj wynik z własnym potokiem indeksowania. Szczęśliwego kodowania!


## Co powinieneś nauczyć się dalej?


Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz krok po kroku wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i poznać alternatywne podejścia implementacyjne w własnych projektach.

- [Create Pdf With Tagged Image In Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Create Pdf With Tagged Image](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Create Tagged Pdf Image Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}