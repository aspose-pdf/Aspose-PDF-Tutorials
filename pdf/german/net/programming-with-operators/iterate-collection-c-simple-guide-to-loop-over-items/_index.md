---
category: general
date: 2026-04-25
description: Durchlaufen Sie eine Sammlung in C# schnell mit einem klaren foreach‑Schleifenbeispiel.
  Lernen Sie, wie Sie Objektnamen erhalten und eine Zeichenkettenliste in nur wenigen
  Schritten anzeigen.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: de
og_description: Iteriere eine Sammlung in C# mit einem foreach‑Schleifenbeispiel.
  Erfahre, wie du Objektnamen erhältst und eine Zeichenkettenliste effizient anzeigst.
og_title: Durchlaufen einer Sammlung in C# – Schritt für Schritt über Elemente iterieren
tags:
- C#
- collections
- loops
title: Sammlung iterieren in C# – Einfache Anleitung zum Durchlaufen von Elementen
url: /de/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterate Collection C# – Wie man mit einer Foreach‑Schleife über Elemente iteriert

Haben Sie schon einmal **iterate collection C#** benötigt, waren sich aber nicht sicher, welche Konstruktion den saubersten Code liefert? Sie sind nicht allein. In vielen Projekten schreiben wir umständliche `for`‑Schleifen, nur um ein paar Strings auszugeben – das kostet Zeit und Lesbarkeit. Die gute Nachricht? Eine einzige `foreach`‑Schleife kann jeden Namen aus einem Objekt holen und **display string list** in Sekundenschnelle anzeigen.

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das zeigt, wie man **object names** erhält, über Elemente iteriert und sie in der Konsole ausgibt. Am Ende haben Sie ein eigenständiges Snippet, das Sie in jede .NET 6+ Konsolen‑App einbinden können, plus ein paar Tipps für Sonderfälle und Performance.

> **Pro‑Tipp:** Wenn Sie mit großen Sammlungen arbeiten, sollten Sie `Parallel.ForEach` in Betracht ziehen – aber das ist ein Thema für einen anderen Tag.

---

## Was Sie lernen werden

- Wie man eine Sammlung von Namen aus einem Objekt abruft (`GetSignatureNames` in unserem Beispiel)
- Die Syntax und Feinheiten eines **foreach loop example** in C#
- Möglichkeiten, **display string list** in der Konsole auszugeben, inklusive Formatierungstricks
- Häufige Fallstricke beim Durchlaufen von Elementen (null‑Sammlungen, leere Ergebnisse)
- Ein vollständiges, copy‑paste‑fertiges Programm, das Sie sofort ausführen können

Es werden keine externen Bibliotheken benötigt; nur die Basisklassenbibliothek, die mit .NET geliefert wird. Wenn das .NET SDK installiert ist, können Sie loslegen.

---

![Iteriere Sammlung C# Diagramm, das eine Liste zeigt, die in eine foreach‑Schleife fließt und dann zur Konsole gelangt](/images/iterate-collection-csharp.png "iterate collection c# diagram")

---

## Schritt 1: Das Beispielobjekt einrichten

Zuerst benötigen wir ein Objekt, das eine Sammlung von Namen zurückgeben kann. Stellen Sie sich vor, Sie haben eine `Signature`‑Klasse, die mehrere Signaturen enthält; jede Signatur hat eine `Name`‑Eigenschaft. Die Methode `GetSignatureNames` extrahiert diese Namen einfach in ein `IEnumerable<string>`.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace IterateCollectionDemo
{
    // A minimal representation of the object you might be working with
    public class Signature
    {
        private readonly List<string> _names = new()
        {
            "Alice Johnson",
            "Bob Smith",
            "Charlie Davis"
        };

        // This method mimics the real‑world API that returns a collection of names
        public IEnumerable<string> GetSignatureNames()
        {
            // Using LINQ to return a read‑only IEnumerable<string>
            return _names.AsReadOnly();
        }
    }
}
```

**Warum das wichtig ist:** Durch die Rückgabe von `IEnumerable<string>` bleibt die Methode flexibel – Aufrufer können enumerieren, abfragen oder das Ergebnis konvertieren, ohne die zugrunde liegende Liste zu kopieren. Das erleichtert später das **loop over items**.

---

## Schritt 2: Die Foreach‑Schleife schreiben, um die String‑Liste anzuzeigen

Jetzt, wo wir eine Quelle von Namen haben, können wir **iterate collection C#**. Das `foreach`‑Konstrukt zieht automatisch jedes Element aus dem Enumerable, sodass wir keine Index‑Variable verwalten müssen.

```csharp
using System;

namespace IterateCollectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Instantiate the object that holds our signatures
            var signature = new Signature();

            // Step 2: Retrieve the collection of signature names from the signature object
            var signatureNames = signature.GetSignatureNames();

            // Step 3: Loop over items and output each name to the console
            foreach (var name in signatureNames)
            {
                Console.WriteLine(name);
            }

            // Keep the console window open when debugging locally
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Erklärung des Codes:**

1. **Instantiate** `Signature` – Sie haben nun ein Objekt, das seine eigenen Namen kennt.
2. **Retrieve** die Sammlung über `GetSignatureNames()` – das ist der Schritt **get object names**.
3. **Foreach loop example** – `foreach (var name in signatureNames)` iteriert automatisch über jeden String.
4. **Display** jedes `name` mit `Console.WriteLine` – die klassische Art, **display string list** in einer Konsolen‑App auszugeben.

Da `signatureNames` `IEnumerable<string>` implementiert, funktioniert die `foreach`‑Schleife sofort und übernimmt den Enumerator im Hintergrund. Keine Sorge mehr über Off‑by‑One‑Fehler oder manuelle Grenzprüfungen.

---

## Schritt 3: Das Programm ausführen und die Ausgabe prüfen

Kompilieren und starten Sie das Programm (z. B. `dotnet run` im Projektordner). Sie sollten sehen:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Falls nichts ausgegeben wird, prüfen Sie, ob `GetSignatureNames` `null` zurückgibt. Eine kurze defensive Prüfung kann Kopfschmerzen sparen:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Jetzt behandelt die Schleife eine fehlende Sammlung elegant und gibt einfach nichts aus, anstatt eine `NullReferenceException` zu werfen.

---

## Schritt 4: Häufige Varianten & Sonderfälle

### 4.1 Über eine Liste komplexer Objekte iterieren

Oft arbeitet man nicht nur mit einfachen Strings, sondern mit Objekten, die mehrere Eigenschaften besitzen. In diesem Fall können Sie immer noch **loop over items** und entscheiden, was angezeigt wird:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Hier verwenden wir String‑Interpolation, um Felder zu kombinieren – immer noch eine `foreach`‑Schleife, nur mit reichhaltigerer Ausgabe.

### 4.2 Früher Abbruch mit `break`

Wenn Sie nur den ersten passenden Namen benötigen, brechen Sie die Schleife ab:

```csharp
foreach (var name in signatureNames)
{
    if (name.StartsWith("B"))
    {
        Console.WriteLine(name);
        break; // stops after the first B‑name
    }
}
```

### 4.3 Parallele Enumeration (Fortgeschritten)

Wenn die Sammlung riesig ist und jede Iteration CPU‑intensiv, kann `Parallel.ForEach` die Ausführung beschleunigen:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Denken Sie daran, dass `Console.WriteLine` selbst thread‑sicher ist, die Ausgabereihenfolge jedoch nicht deterministisch ist.

---

## Schritt 5: Tipps für saubere und wartbare Schleifen

- **Prefer `foreach` over `for`** wenn Sie keinen Index benötigen; das reduziert Off‑by‑One‑Bugs.
- **Use `IEnumerable<T>`** in Methodensignaturen, um APIs flexibel zu halten.
- **Guard against null** Sammlungen mit dem Null‑Coalescing‑Operator (`??`).
- **Keep the loop body small** – wenn Sie viele Zeilen schreiben, extrahieren Sie eine Methode.
- **Avoid modifying the collection** während der Iteration; das wirft eine `InvalidOperationException`.

---

## Fazit

Wir haben gezeigt, wie man **iterate collection C#** mit einem sauberen **foreach loop example** verwendet, **object names** abruft und **display string list** in der Konsole ausgibt. Das vollständige Programm – Objektdefinition, Abruf und Iteration – läuft sofort und bietet Ihnen eine solide Basis für jedes Szenario, in dem Sie über Elemente iterieren müssen.

Von hier aus können Sie weitergehen zu:

- Filtern mit LINQ vor dem Durchlaufen (`signatureNames.Where(n => n.Contains("a"))`)
- Die Ausgabe in eine Datei schreiben statt in die Konsole
- `IAsyncEnumerable<T>` für asynchrone Streams nutzen

Probieren Sie das aus, und Sie werden sehen, wie vielseitig das `foreach`‑Konstrukt wirklich ist. Fragen zu Sonderfällen oder Performance? Hinterlassen Sie einen Kommentar unten, und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}