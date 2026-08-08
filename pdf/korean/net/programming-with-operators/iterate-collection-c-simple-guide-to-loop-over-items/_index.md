---
category: general
date: 2026-04-25
description: C#에서 컬렉션을 빠르게 반복하는 명확한 foreach 루프 예제. 객체 이름을 가져오고 문자열 목록을 표시하는 방법을 몇
  단계만에 배우세요.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: ko
og_description: foreach 루프 예제를 사용하여 C#에서 컬렉션을 반복합니다. 객체 이름을 가져오고 문자열 목록을 효율적으로 표시하는
  방법을 알아보세요.
og_title: C# 컬렉션 순회 – 단계별 아이템 루프
tags:
- C#
- collections
- loops
title: C# 컬렉션 반복 – 항목을 순회하는 간단 가이드
url: /ko/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 컬렉션 반복 C# – Foreach 루프 예제로 항목을 순회하는 방법

컬렉션을 **iterate collection C#** 해야 하는데 어떤 구문이 가장 깔끔한 코드를 제공하는지 몰라 고민한 적 있나요? 당신만 그런 것이 아닙니다. 많은 프로젝트에서 우리는 몇 개의 문자열을 출력하기 위해 장황한 `for` 루프를 작성하곤 합니다—시간도 낭비하고 가독성도 떨어집니다. 좋은 소식은? 단 하나의 `foreach` 루프만으로 객체에서 모든 이름을 추출하고 **display string list** 를 몇 초 만에 보여줄 수 있다는 것입니다.

이 튜토리얼에서는 **객체 이름을 가져오기**, 항목을 순회하기, 그리고 콘솔에 출력하기 위한 완전하고 실행 가능한 예제를 단계별로 살펴봅니다. 마지막까지 따라오면 .NET 6+ 콘솔 앱에 바로 넣을 수 있는 자체 포함 스니펫과 엣지 케이스 및 성능에 대한 몇 가지 팁을 얻을 수 있습니다.

> **Pro tip:** 대용량 컬렉션을 다룰 때는 `Parallel.ForEach` 사용을 고려해 보세요—하지만 이는 다음 기회에 다루겠습니다.

---

## 배울 내용

- 객체(`GetSignatureNames` 샘플)에서 이름 컬렉션을 가져오는 방법
- C#에서 **foreach loop example** 의 문법 및 세부 사항
- 콘솔에 **display string list** 하는 다양한 방법과 포맷팅 요령
- 항목을 순회할 때 흔히 마주치는 함정(null 컬렉션, 빈 결과)
- 즉시 실행 가능한 전체 프로그램 코드 복사‑붙여넣기

외부 라이브러리는 필요 없습니다; .NET에 기본으로 포함된 클래스 라이브러리만 있으면 됩니다. .NET SDK가 설치돼 있다면 바로 시작할 수 있습니다.

---

![컬렉션을 순회하는 C# 다이어그램: 리스트가 foreach 루프로 흐른 뒤 콘솔에 출력되는 모습](/images/iterate-collection-csharp.png "컬렉션 순회 C# 다이어그램")

---

## Step 1: 샘플 객체 설정

먼저—이름 컬렉션을 반환할 수 있는 객체가 필요합니다. 여러 서명을 보유하고 있는 `Signature` 클래스를 상상해 보세요; 각 서명은 `Name` 속성을 가지고 있습니다. `GetSignatureNames` 메서드는 이러한 이름들을 `IEnumerable<string>` 형태로 추출합니다.

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

**왜 중요한가:** `IEnumerable<string>`을 반환함으로써 메서드가 유연해집니다—호출자는 결과를 열거하거나, 쿼리하거나, 복사 없이 변환할 수 있습니다. 또한 나중에 **loop over items** 할 때도 쉽게 사용할 수 있습니다.

---

## Step 2: Foreach 루프 작성하여 문자열 리스트 출력

이제 이름 소스가 준비됐으니 실제로 **iterate collection C#** 해봅시다. `foreach` 구문은 열거형에서 각 요소를 자동으로 꺼내므로 인덱스 변수를 관리할 필요가 없습니다.

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

**코드 설명:**

1. **Instantiate** `Signature` – 이제 자신의 이름을 알고 있는 객체가 생겼습니다.
2. **Retrieve** `GetSignatureNames()` 로 컬렉션을 가져옵니다 – 이것이 **get object names** 단계입니다.
3. **Foreach loop example** – `foreach (var name in signatureNames)` 가 각 문자열을 자동으로 순회합니다.
4. **Display** `Console.WriteLine` 로 각 `name` 을 출력합니다 – 콘솔 앱에서 **display string list** 하는 고전적인 방법이죠.

`signatureNames` 가 `IEnumerable<string>`을 구현하고 있기 때문에 `foreach` 루프는 별도 설정 없이 바로 동작하며, 인덱스 오류나 수동 범위 검사를 신경 쓸 필요가 없습니다.

---

## Step 3: 프로그램 실행 및 출력 확인

프로그램을 컴파일하고 실행합니다(예: 프로젝트 폴더에서 `dotnet run`). 다음과 같은 결과가 표시되어야 합니다:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

출력이 전혀 나타나지 않으면 `GetSignatureNames` 가 `null` 을 반환하고 있는지 확인하세요. 간단한 방어 코드를 추가하면 문제를 예방할 수 있습니다:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

이제 컬렉션이 없을 경우 루프가 조용히 종료되고 `NullReferenceException` 이 발생하지 않습니다.

---

## Step 4: 일반적인 변형 및 엣지 케이스

### 4.1 복합 객체 리스트 순회

보통 문자열이 아니라 여러 속성을 가진 객체를 다루게 됩니다. 이 경우에도 **loop over items** 하면서 어떤 정보를 출력할지 결정할 수 있습니다:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

여기서는 문자열 보간을 사용해 필드를 결합했습니다— 여전히 `foreach` 루프이며, 출력이 더 풍부해졌을 뿐입니다.

### 4.2 `break` 로 조기 종료

첫 번째 매칭 이름만 필요하다면 루프를 빠져나갑니다:

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

### 4.3 병렬 열거 (고급)

컬렉션이 방대하고 각 반복이 CPU 집약적이라면 `Parallel.ForEach` 로 속도를 높일 수 있습니다:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

`Console.WriteLine` 자체는 스레드‑안전하지만 출력 순서는 예측할 수 없게 됩니다.

---

## Step 5: 깔끔하고 유지보수 가능한 루프를 위한 팁

- 인덱스가 필요 없을 때는 **Prefer `foreach` over `for`** — 오프‑바이‑원 버그를 줄여줍니다.
- 메서드 시그니처에 **Use `IEnumerable<T>`** 를 사용해 API 유연성을 유지합니다.
- **Guard against null** 컬렉션을 널 병합 연산자(`??`) 로 처리합니다.
- **루프 본문을 작게** 유지하세요—많은 코드를 작성하게 되면 메서드로 추출합니다.
- **Iterating 중 컬렉션을 수정하지** 마세요; `InvalidOperationException` 이 발생합니다.

---

## 결론

우리는 **iterate collection C#** 를 깔끔한 **foreach loop example** 로 구현하고, **object names** 를 가져와 콘솔에 **display string list** 하는 방법을 시연했습니다. 객체 정의, 이름 추출, 순회까지 포함된 전체 프로그램은 그대로 실행 가능하며, 항목을 순회해야 하는 모든 시나리오에 탄탄한 기반을 제공합니다.

다음 단계로 시도해 볼 수 있는 내용:

- 루프 전에 LINQ 로 필터링 (`signatureNames.Where(n => n.Contains("a"))`)
- 콘솔 대신 파일에 출력하기
- 비동기 스트림을 위한 `IAsyncEnumerable<T>` 사용하기

한 번 직접 해보고 `foreach` 구문의 다재다능함을 체감해 보세요. 엣지 케이스나 성능에 대한 질문이 있으면 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}