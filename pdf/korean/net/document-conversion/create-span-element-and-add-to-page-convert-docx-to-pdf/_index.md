---
category: general
date: 2026-03-27
description: C#에서 span 요소를 생성하고 DOCX를 PDF로 변환하면서 페이지에 span을 추가하고 PDF로 저장하는 방법을 배웁니다.
  개발자를 위한 단계별 가이드.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: ko
og_description: C#에서 span 요소를 생성하고 DOCX를 PDF로 변환하면서 페이지에 span을 추가하는 방법을 배우고, PDF로
  저장하세요. 전체 코드 예제가 포함되어 있습니다.
og_title: span 요소를 생성하고 페이지에 추가 – DOCX를 PDF로 변환
tags:
- C#
- DocumentProcessing
- PDFConversion
title: span 요소를 생성하고 페이지에 추가 – DOCX를 PDF로 변환
url: /ko/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# span 요소 생성 및 페이지에 추가 – DOCX를 PDF로 변환

DOCX 파일에 **span 요소**를 만드는 것은 정밀한 레이아웃 제어가 필요할 때 흔히 수행되는 작업입니다. 이 튜토리얼에서는 페이지에 **span을 추가하는 방법**, **DOCX를 PDF로 변환하는 방법**, 그리고 **PDF로 저장하는 방법**을 몇 가지 간단한 단계로 보여드립니다.  

Word 문서를 보면서 “정확한 좌표에 작은 텍스트 상자를 넣을 수 있으면 좋겠어”라고 생각해 본 적이 있다면, 바로 여기가 맞는 곳입니다. 소스 파일을 로드하는 단계부터 깔끔한 PDF 출력까지 전체 워크플로우를 함께 살펴보겠습니다.

## What you’ll accomplish

이 가이드를 끝까지 따라오면 다음을 할 수 있게 됩니다:

* `Document` 클래스를 사용해 `.docx` 파일을 로드합니다.  
* `TaggedContent` API로 **span 요소**를 **생성**합니다.  
* 선택한 페이지의 정확한 X/Y 좌표에 해당 span을 **배치**합니다.  
* 페이지가 첫 번째가 아니어도 **요소를 페이지에 추가**할 수 있습니다.  
* 단일 `Save` 호출로 **DOCX를 PDF로 변환**하고 **PDF로 저장**합니다.

외부 도구 없이, 신비한 설정 없이—그냥 프로젝트에 복사‑붙여넣기 할 수 있는 순수 C# 코드만 있으면 됩니다.

## Prerequisites

* .NET 6+ (또는 라이브러리가 지원하는 최신 .NET 런타임)  
* `Document`, `TaggedContent`, `Position` 등을 제공하는 문서 처리 SDK  
* 기본적인 C# 문법 이해 – `Console.WriteLine`을 쓸 수 있으면 충분합니다.

> **Pro tip:** SDK 버전을 최신 상태로 유지하세요; 2026년 3월 현재 최신 릴리스(v3.2)에는 페이지‑레벨 작업을 위한 성능 개선이 포함되어 있습니다.

---

![Diagram illustrating how to create span element and place it on a PDF page](https://example.com/images/create-span-element.png "Create span element placement diagram")

## Create span element – Position and Add to Page

아래는 소스 DOCX를 로드하고 최종 PDF를 작성하는 전체 실행 가능한 코드입니다. 콘솔 앱에 그대로 붙여넣고 경로만 조정한 뒤 실행해 보세요.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Step‑by‑step explanation

#### Step 1 – Load the DOCX document  
`Document` 객체를 `input.docx`에 연결해 인스턴스화합니다. 이 객체는 메모리 상에 전체 Word 파일을 나타내며 페이지, 콘텐츠, 메타데이터에 접근할 수 있게 해줍니다.  

#### Step 2 – Create a span element  
`TaggedContent.CreateSpanElement()` 호출은 가벼운 인라인 컨테이너를 반환합니다. 텍스트, 이미지 또는 다른 인라인 요소를 담을 수 있는 작고 보이지 않는 박스로 생각하면 됩니다. `span.Text`에 텍스트를 넣는 것은 선택 사항이지만 디버깅에 유용합니다.

#### Step 3 – Position the span  
`new Position(50, 750)`은 span의 좌상단 모서리를 왼쪽 여백에서 50 pt, 페이지 상단에서 750 pt 떨어진 위치에 설정합니다. 값은 절대 좌표이므로 원하는 어디든 정확히 배치할 수 있어 정밀 레이아웃에 적합합니다.

#### Step 4 – Add span to the target page  
`doc.Pages[1].Add(span)`은 두 번째 페이지에 span을 삽입합니다. API는 0부터 시작하는 인덱스를 사용하므로 페이지 0이 첫 번째 페이지입니다. 첫 페이지에 추가하려면 `doc.Pages[0]`을 사용하면 됩니다.

#### Step 5 – Convert DOCX to PDF and save as PDF  
`doc.Save("output.pdf")` 호출은 두 가지 작업을 수행합니다: 수정된 문서를 디스크에 **쓰기**하고, 파일 확장자가 `.pdf`이기 때문에 내용을 **PDF로 변환**합니다. 별도의 변환 단계가 필요 없으며, 이것이 **PDF로 저장**하는 가장 간단한 방법입니다.

---

## How to add span on a different page (advanced)

페이지 인덱스를 미리 알 수 없는 경우도 있습니다. 페이지 번호(사람이 읽는 형태)나 특정 키워드를 검색해 페이지를 찾을 수 있습니다.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Why this matters:** 페이지 수가 변동하는 보고서에서는 `Pages[1]`을 하드코딩하면 레이아웃이 깨질 수 있습니다. 이 스니펫은 **span을 동적으로 추가**하는 견고한 패턴을 보여줍니다.

---

## Common pitfalls and how to avoid them

| Issue | What happens | Fix |
|-------|--------------|-----|
| **Span not visible** | 좌표가 페이지 밖에 있거나 span의 너비/높이가 0입니다. | `Position` 값을 다시 확인하고 PDF 뷰어의 눈금자를 사용하세요. |
| **Wrong page index** | 페이지 0에 추가했지만 페이지 2에 있어야 합니다. | API는 0‑베이스임을 기억하고, 사람 친화적인 페이지 번호에 1을 더하세요. |
| **Saving overwrites source** | `doc.Save("input.docx")`가 원본 파일을 덮어씁니다. | 변환 시에는 항상 새 경로(`output.pdf`)에 저장하세요. |
| **Missing SDK reference** | `Document` 클래스를 찾을 수 없어 컴파일 오류가 발생합니다. | NuGet 패키지를 설치하세요: `dotnet add package DocumentProcessing.SDK`. |

---

## Verifying the result

프로그램을 실행한 뒤 `output.pdf`를 任意의 PDF 뷰어에서 열어 보세요. 두 번째 페이지의 (50, 750) 위치에 “Hello, world!” 텍스트가 정확히 표시되어야 합니다. 텍스트가 다른 위치에 나타나면 `Position` 값을 조정하고 다시 실행합니다.  

자동화 테스트가 필요하면 PDF 파서(예: iTextSharp)를 사용해 텍스트 좌표를 프로그램matically 검증할 수 있습니다.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Next steps

* **Style the span** – `span.Font`, `span.Color` 등 스타일 속성을 탐색해 보세요.  
* **Add images** – 그래픽을 삽입하려면 span 대신 `CreateImageElement()`를 사용합니다.  
* **Batch processing** – 폴더에 있는 여러 DOCX 파일을 반복 처리합니다

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}