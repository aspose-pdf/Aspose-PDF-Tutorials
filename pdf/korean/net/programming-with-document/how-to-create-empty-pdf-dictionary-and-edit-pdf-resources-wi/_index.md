---
category: general
date: 2026-10-26
description: Aspose.PDF for C#를 사용하여 빈 PDF 사전을 만들고 PDF 리소스를 편집하는 방법을 배웁니다. 단계별 가이드와
  전체 코드 예제.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: ko
lastmod: 2026-10-26
og_description: Aspose.PDF for C#를 사용하여 빈 PDF 사전을 만들고 PDF 리소스를 편집하세요. PDF에서 그래픽 상태를
  수정하는 전체 튜토리얼을 따라보세요.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: C#에서 빈 PDF 사전 만들기 및 PDF 리소스 편집 – Aspose.PDF 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Aspose.PDF를 사용하여 C#에서 빈 PDF 사전 만들기 및 PDF 리소스 편집 방법
url: /ko/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF를 사용하여 C#에서 빈 PDF 사전 만들기 및 PDF 리소스 편집 방법

C# 애플리케이션에서 **빈 PDF 사전**을 **생성**하고 **PDF 리소스를 편집**해야 할 경우, 이 가이드는 정확한 단계별 절차를 보여줍니다. 기존 PDF의 첫 페이지에 사용자 정의 그래픽 상태를 추가하는 완전한 실행 예제를 확인할 수 있습니다.

저수준 PDF 객체를 다루는 것은 다소 복잡하게 느껴질 수 있지만, Aspose.PDF는 사전 조작을 위한 명확한 API를 제공합니다. 이 튜토리얼을 마치면 각 작업이 왜 중요한지, 그리고 다른 리소스 유형에 코드를 어떻게 적용할 수 있는지 이해하게 됩니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* .NET 6.0 (또는 그 이후 버전) 설치
* **Aspose.PDF for .NET** 라이선스 사본 – 무료 체험판으로 테스트 가능
* Visual Studio 2022와 같은 IDE
* 코드에서 참조할 수 있는 폴더에 `input.pdf` 파일이 위치해 있어야 함

`Aspose.Pdf` 외에 추가 NuGet 패키지는 필요하지 않습니다.

## Step 1: Set up the project and import namespaces

새 콘솔 프로젝트를 만들고 Aspose.PDF 패키지를 추가합니다:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

`Program.cs` 파일에서 사용할 네임스페이스를 가져옵니다:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

이러한 import는 `Document`, `DictionaryEditor`, 그리고 COS (Canonical Object Structure) 클래스를 노출시켜 **빈 PDF 사전** 객체를 만들고 기존 리소스 사전을 수정할 수 있게 합니다.

## Step 2: Define the folder that contains the PDF files

`input.pdf`가 들어 있는 디렉터리를 지정합니다. 절대 경로를 사용하면 프로그램이 다른 작업 디렉터리에서 실행될 때 발생할 수 있는 모호성을 피할 수 있습니다.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

`C:\PdfDemo\`를 자신의 머신에 맞는 경로로 교체하세요. 경로를 변수에 저장하면 입력 파일과 출력 파일 모두에 쉽게 재사용할 수 있습니다.

## Step 3: Open the source PDF document

`using` 블록 안에서 수정하려는 PDF를 로드하면 파일 핸들이 자동으로 해제됩니다.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

문서를 열면 페이지 컬렉션, 리소스 사전, 저수준 COS 객체에 접근할 수 있게 됩니다.

## Step 4: Access the first page and its resource dictionary

첫 페이지는 `1`부터 인덱싱됩니다 (PDF 페이지는 1‑베이스). 페이지의 `Resources` 사전을 가져오고 `DictionaryEditor`로 래핑하여 안전하게 편집할 수 있도록 합니다.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor`는 기본 COS 구조를 추상화하여 PDF를 손상시키지 않으면서 항목을 읽거나 생성할 수 있게 해줍니다.

## Step 5: **Create empty PDF dictionary** for a new graphics state

그래픽 상태는 투명도, 블렌드 모드 등 그리기 매개변수를 제어합니다. 사용자 정의 상태를 추가하려면 먼저 빈 사전을 만든 뒤 필요한 항목을 채워야 합니다.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

`CreateEmptyDictionary` 호출이 **빈 PDF 사전** 객체를 만드는 핵심 부분입니다. 동일 문서에 속하는 COS 사전을 반환하므로 교차 참조 무결성이 보장됩니다.

### Populate the graphics state entries

표준 키들을 추가합니다:

* `CA` – 스트로크 알파 상수 (범위 0 – 1)
* `ca` – 비스트로크 알파 상수
* `BM` – 블렌드 모드 이름

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

각 항목은 방금 만든 빈 사전에 추가됩니다. 정의와 삽입 루프를 분리하면 코드 가독성이 높아지고 나중에 추가 키를 쉽게 확장할 수 있습니다.

### Register the new graphics state in the resource dictionary

상태에 이름(`GS0`)을 지정하고 페이지 리소스 내부에 있는 `ExtGState` 사전에 추가합니다.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

이제 페이지의 리소스 사전에 사용자 정의 그래픽 상태에 대한 참조가 포함되며, 이후 콘텐츠 스트림에 적용할 수 있습니다.

## Step 6: Save the updated PDF

마지막으로 수정된 문서를 새 파일에 저장합니다. 원본을 그대로 두면 변경 사항을 검증하기가 쉽습니다.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

그래픽 상태 검사를 지원하는 뷰어(예: Adobe Acrobat Pro)에서 `output.pdf`를 열면 `ExtGState` 사전에 `GS0`라는 이름의 항목이 정의한 값과 함께 존재하는 것을 확인할 수 있습니다.

## Full source code

모든 조각을 합치면 다음과 같은 독립 실행형 프로그램이 됩니다:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Expected output

프로그램을 실행하면 다음과 같이 출력됩니다:

```
PDF updated successfully.
```

그리고 동일 폴더에 `output.pdf`가 생성됩니다. 파일을 열면 **Resources → ExtGState → GS0** 아래에 설정한 파라미터가 포함된 새로운 항목이 표시됩니다.

## Common variations and edge cases

| 상황 | 코드 적용 방법 |
|-----------|-----------------------|
| **여러 페이지**에 동일한 그래픽 상태가 필요함 | 사전을 한 번만 만든 뒤 각 페이지의 `ExtGState` 사전에 동일한 `GS0` 참조를 추가합니다. |
| **다른 블렌드 모드** (예: `Multiply`) | `CosPdfName("Normal")` 값을 `CosPdfName("Multiply")` 로 변경합니다. |
| **ExtGState 사전이 존재하지 않음** | `resourcesEditor["ExtGState"]`에 접근하기 전에 `resourcesEditor.ContainsKey("ExtGState")` 를 확인합니다. 없으면 새 빈 사전을 만들고 `firstPage.Resources`에 추가합니다. |
| **대용량 PDF**로 메모리 압박 발생 | 페이지를 스트리밍하는 `PdfDocument.Load` 오버로드를 사용하거나 `using` 블록 안에서 페이지를 하나씩 처리합니다. |
| **다른 리소스** (폰트, XObject) 편집 필요 | `resourcesEditor` 조회에서 `"ExtGState"`를 `"Font"` 또는 `"XObject"` 로 교체하고, 빈 사전을 만들고 채우는 동일 패턴을 따릅니다. |

이러한 변형을 통해 **빈 PDF 사전 만들기** 패턴이 **PDF 리소스 편집**에 어떻게 적용되는지 확인할 수 있습니다.

## Pro tips

* **결과 검증** – 저장 후 PDF‑Box의 `PDFDebugger`와 같이 원시 리소스 사전을 표시할 수 있는 도구로 PDF를 열어 항목이 존재하는지 확인합니다.
* **사전 재사용** – 동일 그래픽 상태를 여러 페이지에 추가할 경우 사전을 변수에 저장하고 재참조하여 매번 새로 만들지 않도록 합니다.
* **버전 호환성** – 코드는 Aspose.PDF 23.12 이상에서 동작합니다. 이전 버전에서는 `CosDictionary` 대신 `CosPdfDictionary`를 사용해야 할 수 있습니다.

## Conclusion

이제 Aspose.PDF for C#를 사용해 **빈 PDF 사전** 객체를 만들고 **PDF 리소스**를 편집하는 방법을 알게 되었습니다. 문서 열기, 페이지 리소스 사전 접근, 사용자 정의 그래픽 상태 구축, 등록, 저장까지 전체 흐름을 다루었습니다. 이제 다른 리소스 유형을 실험하거나 여러 그래픽 상태를 결합하거나 이 기술을 더 큰 PDF 처리 파이프라인에 통합할 수 있습니다.

---

*더 탐구하고 싶나요? 콘텐츠 스트림에 사용자 정의 **ExtGState**를 추가하거나 **Font** 사전을 조작해 새 폰트를 삽입해 보세요. 두 경우 모두 빈 사전을 만들고 PDF 리소스를 편집하는 동일한 패턴을 따릅니다.*


## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 다룬 기술을 기반으로 하며, 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 단계별 코드 예제와 설명을 제공합니다.

- [Edit PDF Resource Dictionary with Aspose.PDF – C# Guide](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}