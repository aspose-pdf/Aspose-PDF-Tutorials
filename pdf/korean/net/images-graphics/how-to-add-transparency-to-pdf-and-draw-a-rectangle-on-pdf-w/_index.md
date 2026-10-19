---
category: general
date: 2026-09-12
description: Aspose.PDF를 사용하여 C#에서 PDF에 투명도를 추가하고, PDF에 사각형을 그리며, 투명도가 적용된 PDF를 저장하는
  방법을 단계별로 배웁니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: ko
lastmod: 2026-09-12
og_description: Aspose.PDF를 사용하여 C#에서 PDF에 투명도를 추가하고, PDF에 사각형을 그린 후 투명도가 적용된 PDF를
  저장합니다. 이 전체 튜토리얼을 따라보세요.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: PDF에 투명도 추가 및 사각형 그리기 – 완전 C# 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Aspose.PDF를 사용하여 PDF에 투명도를 추가하고 사각형을 그리는 방법
url: /ko/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF로 PDF에 투명도 추가 및 사각형 그리기

PDF 파일에 **투명도 추가**가 필요하다면, 이 가이드는 C#에서 정확히 수행하는 방법을 보여줍니다. 또한 **PDF에 사각형 그리기**와 최종적으로 **투명도가 적용된 PDF 저장** 방법을 배워 보고서를 비롯한 인보이스, 혹은 모든 문서 자동화 워크플로우에 재사용할 수 있습니다.

이 튜토리얼에서 여러분은:

* 기존 PDF 문서를 로드합니다.
* 스트로크와 채우기 불투명도를 정의하는 사용자 지정 그래픽 상태를 생성합니다.
* 해당 그래픽 상태를 캔버스에 적용하고 사각형을 그립니다.
* 투명도 설정을 유지하면서 수정된 파일을 저장합니다.

Aspose.PDF for .NET 라이브러리 외에 외부 도구가 필요하지 않으며, 모든 코드 라인마다 설명이 제공되어 각 단계가 왜 중요한지 이해할 수 있습니다.

## 사전 요구 사항

* .NET 6.0 이상 (코드는 .NET Framework 4.7+에서도 작동합니다).
* 라이선스가 있거나 평가판인 **Aspose.PDF for .NET**. NuGet을 통해 설치합니다:

```bash
dotnet add package Aspose.Pdf
```

* 프로젝트에서 참조할 수 있는 폴더에 배치된 입력 PDF(`input.pdf`).

## 단계 1: PDF 문서 로드

첫 번째 작업은 소스 파일을 여는 것입니다. `using` 문을 사용하면 문서가 적절히 해제되어 나중에 저장하려 할 때 발생할 수 있는 파일 잠금 문제를 방지합니다.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*왜 중요한가*: 문서를 로드하면 페이지 컬렉션, 리소스 사전, 그리고 그리기에 필요한 캔버스 객체에 접근할 수 있습니다.

## 단계 2: 첫 번째 페이지의 리소스 사전 접근

각 PDF 페이지에는 글꼴, 이미지, 그래픽 상태와 같은 객체를 저장하는 **리소스 사전**이 있습니다. 새로운 투명도 설정을 도입하려면 `ExtGState` 항목을 편집해야 합니다.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*왜 중요한가*: `DictionaryEditor`를 사용하면 문서 구조를 손상시키지 않고 저수준 PDF 객체를 읽고 수정할 수 있습니다.

## 단계 3: 투명도 값을 가진 사용자 지정 그래픽 상태 생성

그래픽 상태(`ExtGState`)는 그리기 작업이 어떻게 렌더링되는지를 제어합니다. 두 가지 불투명도 매개변수를 정의합니다:

* **CA** – 스트로크 불투명도(도형의 외곽선).
* **ca** – 채우기 불투명도(도형 내부).

또한 블렌드 모드(`BM`)를 “Normal”로 설정합니다. 이는 가장 일반적인 합성 연산입니다.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*왜 중요한가*: `ExtGState` 사전에 `GS0`를 추가하면 캔버스가 그리기 전에 활성화할 수 있는 재사용 가능한 참조가 생성됩니다. `0.5`의 채우기 불투명도는 사각형을 반투명하게 만들어 **PDF에 투명도 추가** 목표를 달성합니다.

## 단계 4: 그래픽 상태 적용 및 사각형 그리기

이제 페이지의 캔버스에 방금 만든 그래픽 상태를 사용하도록 지시하고, 사각형을 그립니다. 좌표는 PDF 좌표계(좌하단이 원점)를 따릅니다.

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*왜 중요한가*: `SetGraphicsState("GS0")`는 이전에 정의한 투명도 설정으로 그리기 컨텍스트를 전환합니다. `Rectangle` 메서드는 형태를 정의하고, `Stroke`는 지정된 불투명도로 외곽선을 렌더링합니다. 채워진 사각형이 필요하면 `Stroke()`를 `FillAndStroke()`로 교체하십시오.

## 단계 5: 투명도 유지하면서 수정된 PDF 저장

마지막으로 문서를 디스크에 다시 씁니다. 출력 파일에는 새로운 그래픽 상태, 그려진 사각형, 그리고 투명도 정보가 포함됩니다.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*왜 중요한가*: 문서를 저장하면 모든 변경 사항이 최종 확정됩니다. 결과 파일은 모든 PDF 뷰어에서 열 수 있으며, 사각형은 50 % 채우기 불투명도로 표시됩니다.

### 예상 결과

`output_with_extgstate.pdf`를 열면 테두리는 완전히 불투명하고 내부는 반투명한 사각형이 표시되어, 아래 페이지 내용이 비쳐 보이게 됩니다.

## 엣지 케이스 및 실용 팁

| 상황 | 권장 조정 |
|-----------|------------------------|
| **여러 페이지** | `pdfDocument.Pages`를 순회하고 각 대상 페이지에 대해 단계 2‑4를 반복합니다. |
| **다른 불투명도 값** | `CA`(스트로크)와 `ca`(채우기)의 `CosPdfNumber` 값을 `0`(완전 투명)과 `1`(완전 불투명) 사이의 원하는 숫자로 변경합니다. |
| **사용자 정의 블렌드 모드** | `"Normal"`을 `"Multiply"`, `"Screen"` 또는 뷰어가 지원하는 PDF 표준 블렌드 모드로 교체합니다. |
| **채워진 사각형** | `canvas.Stroke()` 대신 `canvas.FillAndStroke()`를 호출하여 채우기와 외곽선을 모두 적용합니다. |
| **동일 그래픽 상태 재사용** | 같은 페이지에 여러 도형을 그리기 전에 `canvas.SetGraphicsState("GS0")`를 호출하면 됩니다. |

**프로 팁:** 새로운 `ExtGState`를 추가한 후 항상 리소스 사전을 확인하십시오. 사전이 존재하지 않으면 먼저 생성합니다:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## 전체 실행 가능한 예제

아래는 콘솔 애플리케이션에 복사하여 바로 실행할 수 있는 독립형 프로그램입니다 (`YOUR_DIRECTORY`를 실제 경로로 교체하십시오).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

프로그램을 실행하면 `output_with_extgstate.pdf`가 생성되며, 이는 **PDF에 투명도 추가**, **PDF에 사각형 그리기**, **투명도가 적용된 PDF 저장**을 한 흐름에서 모두 보여줍니다.

## 결론

이제 Aspose.PDF for .NET을 사용하여 **PDF에 투명도 추가**, **PDF에 사각형 그리기**, 그리고 **투명도가 적용된 PDF 저장** 방법을 알게 되었습니다. 이 과정은 사용자 지정 `ExtGState`를 생성하고 캔버스에 적용한 뒤 변경 사항을 저장하는 흐름으로 이루어집니다. 이러한 기본 요소를 활용하면 다른 도형, 여러 페이지, 동적 불투명도 값 등으로 기술을 확장할 수 있습니다.

**다음 단계**

* 동일한 그래픽 상태를 재사용하면서 `canvas.Ellipse`, `canvas.Path`, `canvas.TextFragment`와 같은 다른 그리기 기본 요소를 탐색합니다.
* 투명도를 이미지 오버레이와 결합하여 워터마크(`canvas.Image` + 사용자 지정 `ExtGState`)를 생성합니다.
* 고급 합성 효과를 위해 **그래픽 상태 매개변수**에 대한 Aspose.PDF 문서를 검토합니다.

코딩을 즐기시고, 투명도가 PDF 워크플로우에 제공하는 시각적 유연성을 만끽하세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}