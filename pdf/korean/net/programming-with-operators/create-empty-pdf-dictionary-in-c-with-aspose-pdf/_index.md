---
category: general
date: 2026-08-14
description: Aspose.Pdf를 사용하여 C#에서 빈 PDF 사전을 생성하고 – ExtGState 컬렉션에 그래픽 상태를 추가하고 PDF를
  프로그래밍 방식으로 수정하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: ko
lastmod: 2026-08-14
og_description: Aspose.Pdf를 사용하여 C#에서 빈 PDF 사전을 생성합니다. 이 완전한 가이드를 따라 PDF의 ExtGState
  컬렉션에 사용자 정의 그래픽 상태를 추가하세요.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: C#에서 빈 PDF 사전 만들기 – Aspose.Pdf 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose.Pdf를 사용하여 C#에서 빈 PDF 사전 만들기
url: /ko/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#와 Aspose.Pdf를 사용하여 빈 PDF 사전 만들기

PDF 파일을 다루는 동안 **create empty PDF dictionary** 객체를 만들어야 할 경우, 이 가이드는 Aspose.Pdf 라이브러리를 사용해 C#에서 정확히 어떻게 수행하는지 보여줍니다. 사용자 정의 그래픽 상태를 구축하든, 새로운 리소스를 추가하든, 나중에 사용할 템플릿을 준비하든, 아래 단계는 완전하고 실행 가능한 솔루션을 제공합니다.

PDF를 로드하고, 첫 번째 페이지의 리소스 사전에 접근하고, 새로운 `CosPdfDictionary`를 만든 뒤 이를 `ExtGState` 컬렉션에 삽입하는 방법을 배웁니다. 튜토리얼이 끝날 때쯤이면 새로 만든 사전이 포함된 `output.pdf` 파일을 얻게 됩니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- .NET 6.0 이상 (.NET Framework 4.6+에서도 동작합니다)
- Visual Studio 2022 또는 선호하는 C# IDE
- Aspose.Pdf for .NET 라이선스(또는 임시 평가 키)
- **input.pdf** 라는 샘플 PDF 파일을 직접 관리하는 폴더에 배치 (폴더 경로는 `dataDir` 로 사용됩니다)

`Aspose.Pdf` 외에 추가 NuGet 패키지는 필요하지 않습니다.

## Step 1: Set up the project and reference Aspose.Pdf

1. Visual Studio에서 새로운 **Console App** 프로젝트를 생성합니다.  
2. **NuGet Package Manager**를 열고 `Aspose.Pdf`를 설치합니다:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. `Program.cs` 상단에 다음 `using` 지시문을 추가합니다:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *왜 이 네임스페이스인가요?* `Aspose.Pdf`는 핵심 `Document` 클래스를 제공하고, `Aspose.Pdf.Operators.Gfx`는 `CosPdfDictionary`, `CosPdfNumber` 및 **create empty PDF dictionary** 구조를 만들 때 필요한 저수준 PDF 객체들을 제공합니다.

## Step 2: Load the source PDF

첫 번째 작업은 기존 PDF 파일을 `Document` 인스턴스로 로드하는 것입니다. 이를 통해 모든 페이지, 리소스 및 저수준 사전에 접근할 수 있습니다.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*설명*: `Document`는 파일을 메모리로 읽어 내부 구조를 준비합니다. `using` 문은 처리가 끝난 후 파일 핸들이 해제되도록 보장합니다.

## Step 3: Access the first page’s resource dictionary

각 PDF 페이지에는 폰트, 이미지, ExtGState 객체 및 기타 공유 리소스를 그룹화하는 **Resources** 사전이 있습니다. 새로운 그래픽 상태를 삽입하려면 이 사전을 편집해야 합니다.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor`는 PDF 사전을 C# `Dictionary<string, object>`처럼 다룰 수 있게 해주는 도우미 클래스입니다.

## Step 4: Retrieve (or create) the ExtGState collection

`ExtGState`는 불투명도, 블렌드 모드, 선 두께와 같은 그래픽 상태 객체를 보관합니다. 소스 PDF에 이미 `ExtGState` 항목이 있으면 재사용하고, 없으면 새로운 빈 사전을 생성합니다.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*왜 이 검사를 하나요?* 일부 PDF는 `ExtGState` 항목 자체를 생략합니다. 두 경우를 모두 처리함으로써 튜토리얼이 어떤 입력 파일에도 견고하게 동작합니다.

## Step 5: **Create empty PDF dictionary** for a new graphics state

이제 실제로 새로운 그래픽 상태 매개변수를 정의하는 **create empty PDF dictionary** 객체를 생성합니다. 사전은 비어 있는 상태에서 시작하며, 필요한 키들을 추가합니다:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### What each entry does

| 키 | 형식 | 의미 |
|-----|------|---------|
| **CA** | `CosPdfNumber` | 스트로크 불투명도 (범위 0‑1). |
| **ca** | `CosPdfNumber` | 채우기 불투명도 (범위 0‑1). |
| **BM** | `CosPdfName`   | 블렌드 모드; `"Normal"`이 가장 일반적입니다. |

**빈 PDF 사전**으로 시작했기 때문에 어떤 항목을 추가할지 완전히 제어할 수 있습니다. 필요에 따라 `LW`(선 두께)나 `LC`(선 캡)와 같은 추가 그래픽 상태 매개변수로 사전을 확장할 수 있습니다.

## Step 6: Insert the new graphics state into ExtGState

`ExtGState` 사전은 각 항목이 이름(`GS0`, `GS1` 등)으로 식별되는 맵처럼 동작합니다. 고유 키 아래에 방금 만든 사전을 추가합니다.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

여러 상태를 추가하려면 접미사(`GS1`, `GS2`, …)를 증가시켜 이름 충돌을 방지하세요.

## Step 7: Save the modified PDF

마지막으로 변경 내용을 디스크에 저장합니다. `Save` 메서드는 업데이트된 사전을 자동으로 직렬화합니다.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

任意의 PDF 뷰어에서 `output.pdf`를 열고 **Resources → ExtGState** 항목을 확인해 보세요(대부분의 뷰어는 이를 숨기지만 Adobe Acrobat Preflight이나 PDF‑Tron 같은 도구에서는 확인할 수 있습니다). 정의한 불투명도와 블렌드 모드 값이 포함된 `GS0` 항목이 보일 것입니다.

## Complete working example

모든 코드를 하나로 합치면 다음과 같이 `Program.cs`에 복사‑붙여넣기만 하면 실행할 수 있는 전체 프로그램이 됩니다:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**예상 출력** – 콘솔에 확인 메시지가 출력되고, `output.pdf`에 `ExtGState` 아래 새로운 `GS0` 항목이 포함됩니다. `gs` 연산자를 통해 `GS0`을 참조하는 페이지를 렌더링하면 스트로크는 완전 불투명하고, 채우기는 50 % 투명하게 표시됩니다.

## Common questions and edge‑case handling

| 질문 | 답변 |
|----------|--------|
| *PDF에 페이지가 여러 개 있는 경우는 어떻게 하나요?* | 예제는 첫 번째 페이지(`Pages[1]`)를 대상으로 합니다. 모든 페이지에 적용하려면 `pdfDocument.Pages`를 순회하면서 각 페이지의 리소스에 대해 3‑5 단계를 반복하면 됩니다. |
| *이미 “GS0”라는 ExtGState 항목이 있는 페이지에 사전을 추가할 수 있나요?* | 가능합니다. 하지만 기존 항목을 덮어쓰지 않도록 다른 키(`GS1`, `GS2`, …)를 사용해야 합니다. |
| *저장 후에도 사전을 수정하는 것이 안전한가요?* | `Save`를 호출하면 메모리상의 표현이 파일과 분리됩니다. 필요하다면 `Document` 객체를 계속 편집하고 다시 `Save`를 호출할 수 있습니다. |
| *Aspose.Pdf를 사용하려면 라이선스가 필요한가요?* |  |

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 적용할 수 있는 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.PDF for .NET을 사용하여 PDF에서 점선 만들기: 단계별 가이드](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Aspose.PDF .NET을 사용하여 PDF에서 그래픽 제거하기: 완전 가이드](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Aspose.PDF for .NET을 사용하여 다중 레이어 PDF 만들기: 종합 가이드](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}