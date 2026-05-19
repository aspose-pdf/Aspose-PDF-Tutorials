---
category: general
date: 2026-04-12
description: C#로 Word에 그림을 빠르게 추가하세요. Word에서 그림 위치를 지정하고, docx에 그림을 삽입하며, 고급 레이아웃을
  위한 사용자 정의 XML을 추가하는 방법을 배워보세요.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: ko
og_description: C#로 Word에 그림을 빠르게 추가하세요. Word에서 그림 위치 지정, docx에 그림 삽입, 고급 레이아웃을 위한
  사용자 정의 XML 추가 방법을 배워보세요.
og_title: Word에 그림 추가 – 완전한 C# 프로그래밍 가이드
tags:
- C#
- Word Automation
- Document Generation
title: Word에 그림 추가 – 완전한 C# 프로그래밍 가이드
url: /ko/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Word에 그림 추가 – 완전한 C# 프로그래밍 가이드

Word에 **그림을 추가**해야 할 때, 어디서 시작해야 할지 몰라 고민한 적 있나요? 혼자가 아닙니다. 많은 사무 자동화 프로젝트에서 빠진 조각은 커스텀 XML 파트 안에 들어가는 깔끔하게 배치된 사진이나 다이어그램입니다. 이 가이드는 **Word에서 그림 위치 지정** 방법, 그림을 *.docx* 파일에 삽입하는 방법, 그리고 기본 Word 객체처럼 동작하도록 기본 커스텀 XML을 조정하는 방법을 정확히 보여줍니다.

GemBox.Document 라이브러리를 사용한 실제 예제를 단계별로 살펴보겠습니다 (소형 파일은 무료, 대용량 작업은 상용). 끝까지 진행하면 X = 50, Y = 200 좌표에 그림을 삽입하는 독립 실행형 프로그램을 얻을 수 있습니다. 모호한 “문서 참고” 같은 단축키 없이—명확한 코드와 작동 원리, 그리고 바로 프로젝트에 복사해 사용할 수 있는 팁을 제공합니다.

## 사전 요구 사항

- .NET 6.0 이상 (코드는 .NET Core 3.1에서도 컴파일됩니다)
- **GemBox.Document** NuGet 패키지 (`Install-Package GemBox.Document`)
- 그림을 삽입하려는 위치에 커스텀 XML 태그가 이미 포함된 시작 Word 파일 (`input.docx`)
- 기본 C# 지식 (각 줄이 왜 중요한지 확인할 수 있습니다)

> **Pro tip:** 사전 태그가 있는 문서가 없으면 Word에서 *Content Control* → *XML Mapping Pane* → 커스텀 XML 파트를 매핑하여 만들 수 있습니다. 라이브러리는 해당 컨트롤을 `TaggedContent`로 처리합니다.

## Step 1 – 원본 문서 로드

먼저 기존 *.docx* 파일을 엽니다. `Document`는 모든 GemBox 작업의 진입점입니다.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Why?* 파일을 로드하면 커스텀 XML 컨테이너를 포함한 내부 파트에 접근할 수 있습니다. 이 단계가 없으면 그림을 담을 `TaggedContent` 노드를 찾을 수 없습니다.

## Step 2 – 태그된 콘텐츠 접근 (커스텀 XML 컨테이너)

커스텀 XML은 Word의 *content control* 안에 저장됩니다. GemBox는 이를 `TaggedContent`로 노출합니다.

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

문서에 여러 태그 섹션이 있는 경우, `TaggedContent`는 **첫 번째** 것을 반환합니다. 이름으로 특정 태그를 선택하려면 `doc.TaggedContents`를 열거할 수도 있습니다.

## Step 3 – Figure 요소 생성

`FigureElement`는 그림, 차트 또는 Word가 *shape*으로 취급하는 모든 시각 객체를 나타냅니다. 이를 태그된 컨테이너 안에 생성합니다.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Why create a figure here?* 커스텀 XML 노드에 연결함으로써 Word는 해당 그림이 논리적 섹션에 속한다는 것을 인식합니다. 이는 이후 편집이나 content‑control 기반 워크플로에 매우 중요합니다.

## Step 4 – 그림을 정확히 위치 지정

Word는 포인트(1 pt ≈ 1/72 in)를 사용해 위치를 지정합니다. `PointF` 구조체를 사용하면 X/Y 좌표를 쉽게 설정할 수 있습니다.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **How to position shape word:** `Position` 속성은 `PointF`를 받아 첫 번째 값은 페이지 여백을 기준으로 한 수평 오프셋(왼쪽), 두 번째 값은 수직 오프셋(위)입니다. 이 값을 조정해 배치를 미세 조정하세요.

## Step 5 – Figure를 Tagged Content 트리에 삽입

이제 그림을 커스텀 XML 트리의 루트 요소에 연결합니다. 이렇게 하면 실제로 Word 문서에 shape가 추가됩니다.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

이 시점에서 그림은 문서 안에 존재하지만 아직 이미지 소스가 없습니다. 디스크에 있는 간단한 PNG를 추가해 보겠습니다.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Step 6 – 수정된 문서 저장

마지막으로 변경 사항을 새로운 *.docx* 파일에 기록합니다.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

`output.docx`를 Word에서 열면 지정한 커스텀 XML 블록 안에 그림이 정확히 (50, 200) 위치에 배치된 것을 볼 수 있습니다.

### 전체 작동 예제

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Expected result:** `output.docx`를 열면 지정한 위치에 PNG가 정확히 배치되고, 커스텀 XML 파트 안에 중첩된 것을 확인할 수 있습니다. 문서의 XML을 검사하면 (`.docx` → 압축 해제 → `word/document.xml`), 올바른 `<v:shape>` 좌표를 가진 `<w:pict>` 요소가 보일 것입니다.

## 일반적인 질문 및 엣지 케이스

### 문서에 여러 태그 섹션이 있는 경우는?

태그 이름으로 열거하고 선택하려면 `doc.TaggedContents`를 사용합니다:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### 그림에 캡션을 추가하려면?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Word 2010 및 이후 버전에서도 작동하나요?

예. GemBox.Document는 Open XML 표준을 목표로 하며, Word 2007 이상(2010, 2013, 2016, 2019, Microsoft 365 포함)과 호환됩니다.

### shape를 회전시켜야 하는 경우는?

```csharp
figure.Rotation = 45; // degrees
```

### 래스터 이미지 대신 벡터 그래픽을 추가하려면?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## 프로 팁 및 함정

- **File paths:** `Path.Combine`를 사용해 하드코딩된 구분자를 피하세요, 특히 비 Windows 플랫폼에서.
- **License limits:** 무료 GemBox 라이선스는 문서 크기를 20 KB로 제한합니다. 더 큰 파일은 상용 키를 구매하세요.
- **Performance:** 배치 처리 시 단일 `Document` 인스턴스를 재사용하면 메모리 오버헤드가 크게 감소합니다.
- **Shape overflow:** 그림 크기가 페이지 여백을 초과하면 Word가 잘라냅니다. `figure.Width`와 `figure.Height`를 적절히 조정하세요.

## 결론

이제 **Word에 그림을 추가하는 방법**, **Word에서 그림을 정확히 위치 지정하는 방법**을 알고 있으며, shape가 기본 요소처럼 동작하도록 기본 커스텀 XML을 조작하는 방법도 알게 되었습니다. 완전한 실행 가능한 예제는 문서 로드, `FigureElement` 생성, 좌표 설정, 이미지 첨부, 최종적으로 업데이트된 *.docx* 저장까지 모든 단계를 보여줍니다.

다음으로 **insert figure into docx**를 실험해 보세요—여러 그림을 추가하거나 루프를 사용하거나 실시간으로 차트를 생성할 수 있습니다. 또한 풍부한 콘텐츠 컨트롤을 위해 **how to add custom xml**을 탐색하거나 표와 머리글에서 **how to position shape word**를 배우는 것도 좋습니다. 가능성은 무궁무진하며, 여기서 다룬 기본을 바탕으로 이제 프로처럼 Word 문서를 자동화할 준비가 되었습니다.

코딩을 즐기세요, 그리고 문제가 생기면 언제든 댓글을 남겨 주세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}