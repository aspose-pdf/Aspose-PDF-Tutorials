---
category: general
date: 2026-03-24
description: PDF 문서를 만들고 태그된 텍스트의 절대 위치를 설정하는 방법을 배웁니다. 이 튜토리얼에서는 span 요소를 추가하는 방법,
  태그된 콘텐츠를 추가하는 방법 및 페이지에 텍스트를 배치하는 방법을 보여줍니다.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: ko
og_description: PDF 문서를 생성하고 절대 위치 설정, span 요소 추가, 페이지에 텍스트를 배치하는 방법을 태그가 지정된 PDF
  콘텐츠와 함께 즉시 확인하세요.
og_title: PDF 문서 만들기 – 태그된 텍스트의 절대 위치 지정
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: PDF 문서 만들기 – 태그된 텍스트의 절대 위치 설정
url: /ko/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF 문서 만들기 – 태그된 텍스트에 절대 위치 지정

접근 가능한 태그 텍스트를 정확히 원하는 위치에 배치해야 할 때가 있나요? 예를 들어 라벨이 정확한 좌표에 있어야 하는 양식형 PDF를 만들거나, 배경 이미지와 완벽히 맞춰야 하는 인증서를 생성하고 싶을 때 말이죠.  

이 가이드에서는 **태그된** 콘텐츠를 **추가하고**, **절대 위치를 설정**하며, **span 요소를 삽입**하는 전체 실행 가능한 예제를 단계별로 살펴봅니다. 외부 참조 없이 복사‑붙여넣기 가능한 코드와 각 라인의 *왜*에 대한 설명을 제공합니다.

## 사전 요구 사항

- .NET 6+ (또는 .NET Framework 4.6+)와 C# 컴파일러  
- NuGet을 통해 설치한 Aspose.Pdf for .NET (작성 시 최신 버전 23.12)  
- C# 문법에 대한 기본적인 이해  

위 조건을 갖췄다면 바로 시작해 보세요.

---

## PDF 문서 만들기 – 절대 위치 지정

먼저 빈 `Document` 객체를 인스턴스화합니다. 이 객체는 전체 PDF 파일을 나타내며 태그‑콘텐츠 트리에 접근할 수 있게 해줍니다.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**왜 중요한가:**  
`Document`는 PDF 구조의 루트입니다. 먼저 생성함으로써 시각 요소(페이지, 그래픽)와 논리 구조(태그) 모두를 담을 캔버스를 확보합니다. `using` 문은 파일을 올바르게 해제하도록 보장해 Windows에서 파일‑핸들 누수를 방지합니다.

---

## 태그된 콘텐츠 활성화 (태그 추가 방법)

태그된 요소를 삽입하기 전에 문서를 *태그된* 상태로 표시해야 합니다. Aspose.Pdf은 자동으로 `TaggedContent` 객체를 만들지만, 플래그를 켜야 합니다.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**내부에서 무슨 일이 일어나나요?**  
`TaggedContent`를 `true`로 설정하면 PDF 리더에게 파일에 논리 구조 트리가 포함되어 있음을 알립니다. 이는 화면 판독기와 `SetPosition` 메서드가 span 요소에서 올바르게 동작하도록 하는 핵심 요소입니다.

---

## 태그‑콘텐츠 트리의 루트 요소 가져오기

루트 요소는 모든 구조 태그(`\<Document>`, `\<Section>`, `\<Span>` 등)의 진입점입니다. PDF의 보이지 않는 “body”라고 생각하면 됩니다.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**루트가 왜 필요한가:**  
후속 태그들은 모두 트리 어딘가에 붙어야 합니다. 그렇지 않으면 접근성 계층에 나타나지 않습니다.

---

## Span 요소 추가 – 인라인 텍스트용 빌딩 블록

`span`은 HTML `<span>`과 동일한 PDF 개념으로, 짧은 텍스트를 정확히 배치하고 싶을 때 사용합니다.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**디자인 노트:**  
보다 풍부한 서식(굵게, 기울임, 하이퍼링크)이 필요하면 span을 `<Paragraph>`에 감싸거나 이후에 `TextFragment` 객체를 사용할 수 있습니다. 절대 위치 지정에는 순수 span이 가장 가볍습니다.

---

## 절대 위치 지정 – X=100, Y=200

이제 재미있는 단계: 페이지의 정확한 위치에 span을 배치합니다. 좌표계는 왼쪽‑하단 모서리(0,0)에서 시작하며 포인트(1 pt ≈ 1/72 in)를 사용합니다.

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**절대 위치 지정이 필요한 이유:**  
인증서, 청구서, 양식 등 픽셀‑정밀 레이아웃이 필요할 때는 상대 흐름(좌‑우 텍스트)만으로는 부족합니다. `SetPosition`은 일반 텍스트 흐름을 우회하고 지정한 위치에 요소를 고정합니다.

---

## Span에 텍스트 추가

span이 배치되었으니 이제 실제 문자열을 삽입합니다.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**팁:**  
Unicode 문자나 오른쪽‑왼쪽 스크립트가 필요하면 문자열을 그대로 전달하면 됩니다. Aspose.Pdf이 인코딩을 자동으로 처리합니다.

---

## Span을 루트 요소에 추가

마지막으로 span을 문서의 논리 트리에 연결해 최종 PDF에 포함되도록 합니다.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**이 단계를 놓치면 어떻게 되나요?**  
span은 메모리에는 존재하지만 파일에 직렬화되지 않아 텍스트가 보이지 않고 접근성 트리도 불완전합니다.

---

## 완전한 실행 예제

아래 코드는 콘솔 앱에 바로 넣을 수 있는 전체 프로그램입니다. 한 페이지 PDF를 만들고, (100, 200) 위치에 태그된 span을 추가한 뒤 `TaggedPositioned.pdf` 파일로 저장합니다.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**예상 결과:**  
`TaggedPositioned.pdf`를 Adobe Acrobat, Foxit 등 뷰어에서 열면 **“Positioned tagged text”** 문구가 페이지 왼쪽 가장자리에서 100 pt, 아래 가장자리에서 200 pt 위치에 정확히 표시됩니다. *Tags* 패널을 확인하면 문서 루트 아래에 `<Span>` 요소가 표시되어 콘텐츠가 올바르게 태그되었음을 확인할 수 있습니다.

---

## 흔히 묻는 질문 및 예외 상황

### 특정 페이지(첫 페이지가 아닌)에서 텍스트를 배치하려면?

`SetPosition` 호출 전에 원하는 페이지를 가져와야 합니다(`var page = pdfDocument.Pages[3];`). span은 자동으로 현재 페이지 컨텍스트에 붙습니다.

### 위치를 인치나 센티미터 단위로 지정할 수 있나요?

`SetPosition`은 포인트를 받습니다. 다음 식으로 변환합니다:  
- **인치 → 포인트:** `points = inches * 72`  
- **센티미터 → 포인트:** `points = cm * 28.3465`

### span의 폰트나 색상을 바꾸려면?

span을 만든 뒤 `TextState`를 가져와 수정합니다.

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### 문서에 이미 기존 태그가 존재한다면?

새 span을 생성해 기존 요소(`rootElement`, 특정 `<Section>` 등)에 추가하면 됩니다. 논리적 계층을 유지해야 화면 판독기가 올바르게 읽을 수 있습니다.

### PDF/A 또는 PDF/UA 준수와 함께 사용할 수 있나요?

가능합니다. 태그된 PDF는 PDF/UA의 핵심 요구사항이며, PDF/A가 필요하면 콘텐츠를 만든 뒤 `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` 를 호출하면 됩니다.

---

## 전문가 팁 및 함정

- **전문가 팁:** 위치 지정 전에 반드시 페이지를 추가하세요. 페이지가 없으면 `SetPosition`이 조용히 실패합니다.
- **단위 주의:** UI 디자인에서 픽셀을 그대로 사용하면 PDF 포인트와 차이가 나서 텍스트가 잘못 배치됩니다. 변환을 반드시 확인하세요.
- **성능 힌트:** 수천 개의 PDF를 생성한다면 단일 `Document` 인스턴스를 재사용하고 각 실행 사이에 `pdfDocument.Pages.Clear()`를 호출해 메모리 사용량을 최소화하세요.
- **접근성 알림:** 태깅은 선택 사항이 아니라 필수입니다(Section 508, EN 301 549 등). `CreateSpanElement`를 사용하면 텍스트가 보조 기술에 의해 탐지됩니다.

---

## 결론

우리는 **PDF 문서를 처음부터 만들고**, **절대 위치를 지정하고**, **span 요소를 추가**했으며, **태그된** 콘텐츠를 삽입해 **페이지에 텍스트를 픽셀‑정밀도로 배치**하는 방법을 살펴보았습니다. 완전한 예제는 바로 실행 가능하고, 설명은 *방법*과 *이유*를 모두 다루어 개발자와 AI 어시스턴트가 신뢰할 수 있는 솔루션을 제공합니다.

다음 단계로 고려해 볼 내용:

- 위치 지정 텍스트 뒤에 이미지를 넣어 워터마크가 있는 인증서 만들기.  
- 절대 배치가 필요한 다중 줄 블록을 위해 `CreateParagraphElement` 사용하기.  
- 엄격한 접근성 감사를 만족시키기 위해 PDF/UA로 내보내기.  

좌표, 폰트, 색상을 자유롭게 바꿔 보세요. 실험이 태그된 PDF 생성 마스터의 가장 빠른 길입니다. 문제가 생기면 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}