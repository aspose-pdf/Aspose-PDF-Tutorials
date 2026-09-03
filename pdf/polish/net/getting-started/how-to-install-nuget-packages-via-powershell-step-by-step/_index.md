---
category: general
date: 2026-02-20
description: Dowiedz się, jak instalować pakiety NuGet przy użyciu PowerShell, uruchomić
  PowerShell jako administrator, wyświetlić listę zainstalowanych pakietów i zweryfikować
  zainstalowany pakiet w kilka minut.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: pl
og_description: jak zainstalować pakiety NuGet przy użyciu PowerShell, uruchomić PowerShell
  jako administrator, wyświetlić listę zainstalowanych pakietów i zweryfikować zainstalowany
  pakiet — kompletny przewodnik.
og_title: Jak zainstalować pakiety NuGet za pomocą PowerShell – szybki przewodnik
tags:
- PowerShell
- NuGet
- Package Management
title: jak zainstalować pakiety NuGet za pomocą PowerShell – krok po kroku
url: /pl/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak zainstalować pakiety nuget za pomocą PowerShell – krok po kroku

Zastanawiałeś się kiedyś **jak zainstalować nuget** bez otwierania Visual Studio? Nie jesteś sam. W wielu pipeline’ach CI lub na świeżych maszynach najszybszą drogą jest uruchomienie PowerShell — najlepiej *run powershell as admin* — i pozwolenie menedżerowi pakietów wykonać swoją pracę.

W tym tutorialu przejdziemy przez cały proces: otworzenie właściwej konsoli, pobranie konkretnej wersji biblioteki i w końcu potwierdzenie, że pakiet naprawdę trafił na Twój system. Po zakończeniu będziesz potrafił **list installed packages**, będziesz wiedział **how to verify package** oraz będziesz pewny, że krok **verify installed package** zakończył się sukcesem za każdym razem.

## Czego się nauczysz

- Jak uruchomić PowerShell z odpowiednimi uprawnieniami.  
- Dokładna składnia polecenia `Install-Package` dla NuGet.  
- Sposoby na **list installed packages** i potwierdzenie numerów wersji.  
- Typowe pułapki (brak uprawnień administratora, niezgodności wersji) i jak ich unikać.  

Nie wymagana jest wcześniejsza znajomość NuGet, wystarczy działająca maszyna z Windows i odrobina ciekawości.

---

## Jak zainstalować pakiety NuGet przy użyciu PowerShell

> **Pro tip:** Jeśli często dodajesz te same pakiety, rozważ umieszczenie ich w pliku skryptu i uruchomienie go z opcją `-File`. Oszczędzasz tym samym wielokrotne wpisywanie tej samej linii.

### Krok 1: Otwórz PowerShell z niezbędnymi uprawnieniami

Pierwszą rzeczą, którą musisz zrobić, jest **run powershell as admin**. Bez podwyższonych uprawnień polecenie `Install-Package` może cicho niepowodzenie lub poprosić o potwierdzenie, którego nie chcesz obsługiwać.

1. Kliknij przycisk Start.  
2. Wpisz **PowerShell**.  
3. Kliknij prawym przyciskiem *Windows PowerShell* i wybierz **Run as administrator**.  

Zobaczysz monit UAC; kliknij **Yes**. Teraz masz sesję z podwyższonymi uprawnieniami gotową do instalacji pakietów.

> *Dlaczego admin?*  
> NuGet zapisuje pliki w globalnym folderze pakietów (`C:\Program Files\PackageManagement\NuGet\Packages` domyślnie). To miejsce jest chronione, więc tylko podwyższony proces może tam zapisywać.

### Krok 2: Zainstaluj wybrany pakiet NuGet i wersję

Po otwarciu konsoli podstawowe polecenie jest proste:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` to nakładka PowerShell na klienta NuGet.  
- `-Version` wymusza dokładną wersję, zapobiegając przypadkowym aktualizacjom.  

Jeśli pominiesz `-Version`, PowerShell pobierze najnowsze stabilne wydanie — czasem to w porządku, czasem potrzebujesz dokładnie tej wersji, którą testowałeś.

#### Co się dzieje „pod maską”?

PowerShell kontaktuje się z skonfigurowanym źródłem pakietów (domyślnie `https://www.nuget.org/api/v2`) i pobiera plik `.nupkg`. Następnie rozpakowuje DLL‑e do globalnego folderu pakietów i rejestruje pakiet w lokalnym dostawcy pakietów. Cały proces zazwyczaj kończy się w kilka sekund, chyba że masz wolne połączenie.

### Krok 3: Zweryfikuj, że pakiet został zainstalowany pomyślnie

Teraz, gdy pakiet jest już na dysku, prawdopodobnie zapytasz: **„Jak zweryfikować pakiet?”** Odpowiedź znajduje się w prostym zapytaniu:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Uruchomienie tego zwróci coś w stylu:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Ten wynik potwierdza dwie rzeczy:

1. Pakiet **Aspose.PDF** jest obecny.  
2. Jego wersja zgadza się z tą, którą podałeś, spełniając wymóg **verify installed package**.

Jeśli chcesz zobaczyć *wszystkie* pakiety na maszynie, usuń filtr `-Name`:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Ten widok **list installed packages** jest przydatny przy audytach lub gdy trzeba posprzątać stare biblioteki.

### Krok 4: Opcjonalnie – obsługa przypadków brzegowych

#### a) Pakiet nie znaleziony lub niezgodna wersja

Jeśli PowerShell zwróci *„Package not found”* lub *„Version not available”*, sprawdź pisownię i numer wersji. NuGet nie rozróżnia wielkości liter, ale zbędna spacja zepsuje polecenie.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Uruchomienie bez uprawnień administratora

Jeśli zapomnisz **run powershell as admin**, cmdlet zgłosi błąd uprawnień. Rozwiązanie polega po prostu na zamknięciu okna i ponownym otwarciu go z podwyższonymi prawami — nie musisz reinstalować niczego.

#### c) Korzystanie z własnego źródła

W środowiskach korporacyjnych możesz mieć wewnętrzny feed NuGet:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

Krok weryfikacji pozostaje taki sam; pamiętaj tylko, aby przy instalacji dodać `-Source`.

---

## Szybka tabela referencyjna

| Działanie                           | Polecenie PowerShell                                        | Dlaczego to ważne |
|-------------------------------------|-------------------------------------------------------------|-------------------|
| Otwórz podwyższoną konsolę           | *Run PowerShell as Administrator*                           | Wymagane do instalacji globalnej |
| Zainstaluj konkretną wersję          | `Install-Package <pkg> -Version <x.y.z>`                    | Gwarantuje powtarzalne buildy |
| Wyświetl pojedynczy pakiet           | `Get-Package -Name <pkg>`                                    | Potwierdza **how to verify package** |
| Wyświetl wszystkie pakiety NuGet      | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Przydatne do **list installed packages** |
| Szukaj dostępnych wersji            | `Find-Package <pkg> -AllVersions`                           | Pomaga, gdy wersja jest nieznana |

---

## Zakończenie

Omówiliśmy **jak zainstalować nuget** przy użyciu PowerShell od początku do końca — otwieranie konsoli **run powershell as admin**, pobieranie konkretnej wersji oraz finalne **list installed packages** w celu **verify installed package**. Mając te polecenia w swoim arsenale, możesz automatyzować zarządzanie bibliotekami na dowolnej maszynie z Windows, niezależnie od tego, czy tworzysz pipeline CI, czy po prostu naprawiasz brakujący DLL na swoim komputerze deweloperskim.

Co dalej? Spróbuj dodać kilka pakietów do jednego skryptu, zbadaj parametr `-Scope`, aby instalować lokalnie dla projektu, lub połącz te polecenia z `Invoke-Expression`, tworząc lekki instalator dla swojego zespołu. A jeśli napotkasz problem, pamiętaj o kroku **how to verify package** — zobaczenie wersji w `Get-Package` to najczęstszy sposób na szybkie wykrycie problemu.

Szczęśliwego PowerShellowania! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}