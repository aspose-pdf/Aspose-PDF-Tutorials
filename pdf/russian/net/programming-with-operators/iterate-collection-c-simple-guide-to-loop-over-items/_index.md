---
category: general
date: 2026-04-25
description: Быстро перебирайте коллекцию в C# с помощью понятного примера цикла foreach.
  Узнайте, как получить имена объектов и вывести список строк за несколько шагов.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: ru
og_description: Итерация коллекции в C# с помощью цикла foreach. Узнайте, как получить
  имена объектов и эффективно вывести список строк.
og_title: Итерация коллекции C# – пошаговый проход по элементам
tags:
- C#
- collections
- loops
title: Итерация коллекции C# – простой гид по перебору элементов
url: /ru/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Перебор коллекции C# – Как пройтись по элементам с помощью цикла foreach

Когда‑нибудь вам нужно было **перебрать коллекцию C#**, но вы не были уверены, какой конструктор даст самый чистый код? Вы не одиноки. Во многих проектах мы пишем громоздкие циклы `for` только для вывода нескольких строк — теряя время и читаемость. Хорошая новость? Один цикл `foreach` может извлечь каждое имя из объекта и **отобразить список строк** за секунды.

В этом руководстве мы пройдем полный, готовый к запуску пример, показывающий, как **получить имена объектов**, пройтись по элементам и вывести их в консоль. К концу у вас будет самостоятельный фрагмент кода, который можно вставить в любое консольное приложение .NET 6+, а также несколько советов по краевым случаям и производительности.

> **Pro tip:** Если вы работаете с большими коллекциями, рассмотрите использование `Parallel.ForEach` — но это тема для другого дня.

---

## Что вы узнаете

- Как получить коллекцию имён из объекта (`GetSignatureNames` в нашем примере)
- Синтаксис и нюансы **пример цикла foreach** в C#
- Способы **отобразить список строк** в консоли, включая приёмы форматирования
- Распространённые подводные камни при переборе элементов (null‑коллекции, пустые результаты)
- Полную программу, готовую к копированию и запуску сразу

Никакие внешние библиотеки не требуются; достаточно базовой библиотеки классов, поставляемой с .NET. Если у вас установлен .NET SDK, вы готовы к работе.

---

![Диаграмма перебора коллекции C#, показывающая список, переходящий в цикл foreach, а затем в консоль](/images/iterate-collection-csharp.png "диаграмма перебора коллекции c#")

---

## Шаг 1: Создайте примерный объект

Сначала нам нужен объект, который может вернуть коллекцию имён. Представьте, что у вас есть класс `Signature`, содержащий несколько подписей; у каждой подписи есть свойство `Name`. Метод `GetSignatureNames` просто извлекает эти имена в `IEnumerable<string>`.

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

**Почему это важно:** Возвращая `IEnumerable<string>`, мы делаем метод гибким — вызывающие могут перечислять, выполнять запросы или преобразовывать результат без копирования исходного списка. Это также упрощает **перебор элементов** позже.

---

## Шаг 2: Напишите цикл foreach для отображения списка строк

Теперь, когда у нас есть источник имён, давайте действительно **переберём коллекцию C#**. Конструкция `foreach` автоматически берёт каждый элемент из перечисляемого, так что нам не нужно управлять индексной переменной.

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

**Пояснение к коду:**

1. **Создаём экземпляр** `Signature` — теперь у вас есть объект, знающий свои имена.
2. **Получаем** коллекцию через `GetSignatureNames()` — это шаг **получить имена объектов**.
3. **Пример цикла foreach** — `foreach (var name in signatureNames)` автоматически проходит по каждому строковому элементу.
4. **Отображаем** каждое `name` с помощью `Console.WriteLine` — классический способ **отобразить список строк** в консольном приложении.

Поскольку `signatureNames` реализует `IEnumerable<string>`, цикл `foreach` работает «из коробки», управляя перечислителем за кулисами. Не нужно беспокоиться об ошибках off‑by‑one или ручной проверке границ.

---

## Шаг 3: Запустите программу и проверьте вывод

Скомпилируйте и выполните программу (например, `dotnet run` из папки проекта). Вы должны увидеть:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Если ничего не выводится, проверьте, что `GetSignatureNames` не возвращает `null`. Быстрая защита может избавить от головной боли:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Теперь цикл корректно обработает отсутствие коллекции и просто ничего не выведет, вместо того чтобы бросить `NullReferenceException`.

---

## Шаг 4: Общие варианты и краевые случаи

### 4.1 Перебор списка сложных объектов

Часто вместо простых строк вы работаете с объектами, содержащими несколько свойств. В этом случае вы всё равно можете **перебрать элементы** и решить, что отображать:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Здесь мы используем интерполяцию строк для объединения полей — всё ещё цикл `foreach`, но с более богатым выводом.

### 4.2 Преждевременный выход с `break`

Если нужен только первый подходящий элемент, выйдите из цикла:

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

### 4.3 Параллельное перечисление (Продвинуто)

Когда коллекция огромна, а каждая итерация требует значительных вычислений, `Parallel.ForEach` может ускорить процесс:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Помните, `Console.WriteLine` сам по себе потокобезопасен, но порядок вывода будет недетерминированным.

---

## Шаг 5: Советы для чистых и поддерживаемых циклов

- **Отдавайте предпочтение `foreach` вместо `for`**, когда индекс не нужен; это уменьшает количество ошибок off‑by‑one.
- **Используйте `IEnumerable<T>`** в сигнатурах методов, чтобы API оставались гибкими.
- **Защищайте от null** с помощью оператора объединения с null (`??`).
- **Держите тело цикла небольшим** — если пишете много строк, вынесите логику в отдельный метод.
- **Не изменяйте коллекцию во время итерации**; это вызовет `InvalidOperationException`.

---

## Заключение

Мы продемонстрировали, как **перебрать коллекцию C#** с помощью чистого **пример цикла foreach**, получить **имена объектов** и **отобразить список строк** в консоли. Полная программа — определение объекта, получение данных и перебор — работает сразу, предоставляя надёжную основу для любых сценариев, где требуется пройтись по элементам.

Дальше вы можете исследовать:

- Фильтрацию с LINQ перед перебором (`signatureNames.Where(n => n.Contains("a"))`)
- Запись вывода в файл вместо консоли
- Использование `IAsyncEnumerable<T>` для асинхронных потоков

Попробуйте, и вы увидите, насколько универсальна конструкция `foreach`. Есть вопросы о краевых случаях или производительности? Оставляйте комментарий ниже, и happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}