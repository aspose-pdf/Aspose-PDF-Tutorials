---
category: general
date: 2026-08-20
description: Aspose.Pdf를 사용하여 PDF에서 사용자 정의 그래픽 상태를 생성합니다. 몇 단계만으로 PDF 리소스를 편집하고 투명도를
  추가하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: ko
lastmod: 2026-08-20
og_description: Aspose.Pdf를 사용하여 PDF에서 사용자 정의 그래픽 상태를 생성합니다. 이 튜토리얼에서는 PDF 리소스를 편집하고
  투명도를 빠르게 추가하는 방법을 보여줍니다.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: PDF에서 사용자 정의 그래픽 상태 만들기 – Aspose.Pdf 가이드
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Aspose.Pdf를 사용하여 PDF에서 사용자 정의 그래픽 상태 만들기
url: /ko/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf를 사용하여 PDF에서 사용자 정의 그래픽 상태 만들기

PDF에서 **create custom graphics state**를 만들어야 한다면, 이 가이드는 Aspose.Pdf for .NET을 사용하여 정확히 어떻게 하는지 보여줍니다. 튜토리얼이 끝날 때쯤이면 **edit PDF resources**를 수행하고, 새로운 graphics‑state 사전을 삽입하며, **add transparency PDF** 콘텐츠를 C# 프로젝트를 떠나지 않고 추가할 수 있게 됩니다.

전체 실행 가능한 예제와 각 라인이 왜 중요한지에 대한 설명, 그리고 다중 페이지 문서나 다양한 블렌드 모드를 처리하기 위한 팁을 확인할 수 있습니다. 외부 도구는 필요 없으며—Aspose.Pdf 라이브러리와 기본 .NET 개발 환경만 있으면 됩니다.

## 사전 요구 사항

* .NET 6.0 이상 (코드는 .NET Framework 4.7+에서도 작동합니다)
* 라이선스가 있는 **Aspose.Pdf for .NET** 사본 (무료 체험판으로 테스트 가능)
* `input.pdf` 라는 이름의 입력 PDF 파일을 코드에서 참조할 수 있는 폴더에 배치
* Visual Studio 2022 또는 C# 개발을 지원하는 모든 IDE

이 튜토리얼은 기본 C# 구문과 PDF 페이지 개념에 익숙하다고 가정합니다.

## 단계 1: 소스 PDF 로드 및 첫 페이지 접근

첫 번째 작업은 PDF 파일을 열고 수정하려는 리소스를 가진 페이지를 가져오는 것입니다. Aspose.Pdf는 각 페이지를 `Page` 객체로 나타내며, 모든 페이지는 그래픽 상태, 폰트, XObject 등을 저장하는 **resource dictionary**를 포함합니다.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*왜 중요한가:* `Document` 클래스는 파일을 메모리로 로드하고, `Pages[1]`은 첫 페이지의 resource dictionary에 직접 접근할 수 있게 해줍니다. 여기서 그래픽 상태가 존재합니다.

## 단계 2: 리소스 사전을 편집하기 위해 열기

Aspose.Pdf는 리소스 사전을 일반 .NET `Dictionary`처럼 다룰 수 있게 해주는 `DictionaryEditor` 도우미를 제공합니다. 이를 통해 `ExtGState`와 같은 항목을 읽고, 추가하고, 교체하는 것이 간단해집니다.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*왜 중요한가:* `DictionaryEditor`는 저수준 COS 객체를 추상화하여, PDF 규격을 유지하면서 익숙한 키/값 쌍으로 작업할 수 있게 해줍니다.

## 단계 3: ExtGState 사전 가져오기(또는 생성하기)

**ExtGState** 항목은 페이지의 모든 외부 graphics‑state 객체를 보관합니다. 사전이 존재하지 않으면 Aspose.Pdf가 빈 사전을 생성합니다.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*왜 중요한가:* `ExtGState` 항목이 없으면 나중에 `KeyNotFoundException`이 발생합니다. 이 방어 코드는 이전에 사용자 정의 그래픽 상태를 정의한 적이 없는 PDF에서도 코드를 작동하게 하며, **edit PDF resources** 견고성의 필수 요소입니다.

## 단계 4: 사용자 정의 그래픽 상태 사전 만들기

그래픽 상태는 그리기 작업이 어떻게 렌더링되는지를 설명합니다. **add transparency PDF**를 위해서는 `ca`(채우기 불투명도)와 `CA`(스트로크 불투명도) 항목을 설정하고, 필요에 따라 블렌드 모드(`BM`)를 지정해야 합니다. 아래 코드는 이러한 매개변수를 사용하여 새로운 사전을 구축합니다.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*왜 중요한가:* `ca`와 `CA` 항목은 각각 채우기와 스트로크 작업의 투명도를 제어합니다. `BM`을 설정하면 다양한 합성 효과를 실험할 수 있으며, 이는 나중에 반투명 도형이나 이미지와 같은 **add transparency PDF** 콘텐츠를 추가할 때 유용합니다.

## 단계 5: 새로운 그래픽 상태를 고유 이름으로 등록하기

`ExtGState` 사전의 각 그래픽 상태는 고유한 이름(`GS0`, `GS1` 등)을 가져야 합니다. 기존 항목과 충돌하지 않는 이름이면 무엇이든 선택할 수 있습니다.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*왜 중요한가:* 새로운 사전을 `GS0` 아래에 삽입함으로써 페이지 콘텐츠 스트림에서 해당 상태에 접근할 수 있게 됩니다. 조건부 블록은 처음에 `ExtGState`가 없던 PDF에서도 해당 항목이 존재하도록 보장하며, 이는 또 다른 **edit PDF resources** 보호 장치입니다.

## 단계 6: 페이지 콘텐츠에서 사용자 정의 그래픽 상태 사용하기 (선택 사항)

이전 단계들은 그래픽 상태를 *정의*했을 뿐입니다. 실제 효과를 보려면 페이지의 콘텐츠 스트림에서 이를 참조해야 합니다. 아래는 방금 만든 상태를 사용하여 반투명 사각형을 그리는 간단한 예시입니다.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*왜 중요한가:* `SetExtGState` 연산자(`gs`)는 PDF 렌더러에게 `GS0`에 정의된 매개변수를 적용하도록 지시합니다. 사각형은 채우기 불투명도 50%로 표시되고, 스트로크는 완전 불투명하게 유지됩니다.

## 단계 7: 수정된 PDF 저장하기

마지막으로 변경 사항을 디스크에 기록합니다. 원본 파일을 덮어쓰거나 새 파일을 만들 수 있습니다.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

`output_with_custom_gs.pdf`를 PDF 뷰어에서 열면 첫 페이지에 반투명 사각형이 표시됩니다. 이는 **create custom graphics state**, **edit PDF resources**, **add transparency PDF** 콘텐츠를 성공적으로 수행했음을 확인시켜 줍니다.

## 일반적인 변형 및 엣지 케이스

| 상황 | 조정 방법 |
|-----------|----------------|
| **여러 페이지에 동일한 상태가 필요함** | 그래픽 상태를 한 번만 등록(단계 1‑5)하고, 모든 페이지의 콘텐츠 스트림에서 `GS0`를 참조합니다. |
| **요소별로 다른 불투명도** | 다른 `ca`/`CA` 값을 가진 추가 상태(`GS1`, `GS2`, …)를 정의하고 `SetExtGState`를 사용해 전환합니다. |
| **Normal이 아닌 블렌드 모드** | `BM` 항목에서 `"Normal"`을 `"Multiply"`, `"Screen"` 또는 기타 PDF 표준 블렌드 모드로 교체합니다. |
| **이름 충돌** | 추가하기 전에 `extGStateDict.ContainsKey(yourName)`를 확인하고 필요하면 고유한 접미사를 선택합니다. |
| **PDF에 이미 ExtGState 사전이 존재함** | 단계 3의 코드는 이미 기존 사전을 재사용하므로 추가 처리가 필요하지 않습니다. |

**Pro tip:** 대용량 PDF 작업 시, `Document` 사용을 `using` 블록으로 감싸(예시와 같이) 네이티브 리소스를 즉시 해제하세요. 또한 리소스 편집 후 PDF/A 또는 PDF/X 준수를 보장하려면 Aspose.Pdf의 `PdfCompliance` 속성을 활성화하는 것을 고려하십시오.

## 전체 작업 예제

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 보여준 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방법을 탐색하는 데 도움을 줍니다.

- [Aspose로 PDF 만들기 – 양식 필드 및 페이지 추가](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Aspose.PDF .NET을 사용하여 PDF에 사용자 정의 테이블 만들기](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Aspose Pdf Net으로 사용자 정의 PDF 스탬프 만들기](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}