---
category: general
date: 2026-08-08
description: C#에서 Aspose.Pdf를 사용하여 베이츠 번호 매기기 PDF를 추가합니다. 이 튜토리얼에서는 빈 페이지 PDF를 추가하고
  프로그래밍 방식으로 PDF를 생성하는 방법도 보여줍니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: ko
lastmod: 2026-08-08
og_description: C#에서 Aspose.Pdf를 사용해 베이츠 번호 매기기 PDF를 추가하세요. 빈 페이지 PDF 추가, 프로그래밍 방식으로
  PDF 생성, 그리고 몇 분 안에 최종 문서를 저장하는 방법을 배워보세요.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Aspose로 PDF에 베이츠 번호 매기기 추가 – 완전 C# 가이드
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Aspose로 PDF에 베이츠 번호 매기기 – 단계별 가이드
url: /ko/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose를 사용한 베이츠 번호 매기기 PDF 추가 – 단계별 가이드

Aspose.Pdf를 사용한 베이츠 번호 매기기 PDF 추가는 핵심 단계를 이해하면 간단합니다. 빈 페이지 PDF를 추가하거나 프로그래밍 방식으로 PDF를 생성해야 하는 경우에도 이 가이드가 필요한 모든 내용을 다룹니다.

이 튜토리얼에서는 다음을 수행합니다:

* 새 PDF 문서를 처음부터 생성합니다.  
* 베이츠 번호를 표시할 빈 페이지 PDF를 추가합니다.  
* 사용자 정의 접두사가 있는 베이츠 번호 매기기 아티팩트를 구성합니다.  
* PDF를 저장하여 번호가 생성된 파일에 표시되도록 합니다.  

끝까지 진행하면 **CASE‑1000**, **CASE‑1001**, …와 같은 베이츠 번호가 포함된 PDF를 생성하는 완전한 C# 콘솔 애플리케이션을 얻게 됩니다 – 이는 법률 및 전자 증거 발견 워크플로우에서 흔히 요구되는 사항입니다.

## 사전 요구 사항

* .NET 6.0 SDK 이상 (코드는 .NET Framework 4.8에서도 작동합니다).  
* Visual Studio 2022 또는 C# 호환 IDE.  
* 유효한 Aspose.Pdf for .NET 라이선스(또는 무료 평가 키).  
* C# 구문에 대한 기본적인 이해.  

> **프로 팁:** 라이선스 없이 코드를 실행하면 Aspose가 출력 PDF에 작은 워터마크를 추가합니다.

## 단계 1: 프로젝트 설정 및 Aspose.Pdf 가져오기

새 콘솔 프로젝트를 만들고 Aspose.Pdf NuGet 패키지를 추가합니다:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

예제에 필요한 `using` 지시문은 다음과 같습니다:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

이 네임스페이스를 통해 이후에 사용되는 `Document`, `Page`, `BatesNumberingArtifact` 클래스를 사용할 수 있습니다.

## 단계 2: 빈 페이지 PDF 추가

베이츠 번호는 페이지에 부착되어야 하므로, 먼저 번호 매기기 아티팩트를 받을 빈 페이지를 생성합니다.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

`Document` 클래스는 전체 PDF 파일을 나타내며, `Pages.Add()`는 문서의 페이지 컬렉션 끝에 새 빈 페이지를 삽입합니다. 문서가 비어 있기 때문에 이 호출은 첫 페이지도 생성합니다.

## 단계 3: 베이츠 번호 매기기 아티팩트 구성

이제 베이츠 번호의 표시 방식을 정의합니다. `BatesNumberingArtifact`를 사용하면 시작 번호, 접두사, 접미사 및 서식 옵션을 설정할 수 있습니다.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**왜 중요한가:**  
`StartNumber`를 **1000**으로 설정하면 일반적인 법률 사건 파일 규칙에 맞습니다. `Prefix`는 각 번호가 **CASE‑1000**, **CASE‑1001**, …와 같이 표시되도록 하여 검색 및 정렬이 용이합니다.

## 단계 4: 아티팩트를 페이지에 부착

아티팩트는 페이지의 `Artifacts` 컬렉션에 추가되어야 하며, 저장 시 Aspose가 모든 페이지에 렌더링합니다.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

문서를 저장하면 Aspose가 자동으로 모든 페이지에 아티팩트를 반복하고, 각 다음 페이지마다 번호를 증가시킵니다.

## 단계 5: (선택) 추가 페이지 추가

더 많은 페이지가 필요하면 `pdfDocument.Pages.Add()`를 반복하면 됩니다. 이전 단계에서 부착한 베이츠 번호 매기기 아티팩트가 각 새 페이지에 자동으로 나타납니다.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## 단계 6: PDF 저장 – 프로그래밍 방식으로 PDF 생성

마지막으로 문서를 디스크에 저장합니다. 여기서 베이츠 번호가 페이지에 렌더링됩니다.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**예상 결과:**  
*BatesNumberedDocument.pdf*를 열면 3페이지 PDF가 표시됩니다. 각 페이지는 오른쪽 하단에 베이츠 번호를 표시합니다:

* 페이지 1 → **CASE‑1000**  
* 페이지 2 → **CASE‑1001**  
* 페이지 3 → **CASE‑1002**

아티팩트가 페이지 컬렉션에 부착되어 있기 때문에 번호가 자동으로 증가합니다.

## 전체 실행 가능한 예제

모든 내용을 종합하면 복사·붙여넣기·실행할 수 있는 완전한 콘솔 프로그램은 다음과 같습니다:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

`dotnet run`으로 프로그램을 실행합니다. 실행 후 데스크톱에서 파일을 찾아 베이츠 번호를 확인합니다.

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## 일반적인 질문 및 엣지 케이스

### 다른 글꼴이나 위치가 필요하면 어떻게 해야 하나요?

`BatesNumberingArtifact`는 `FontSize`, `FontColor`, `HorizontalAlignment`, `VerticalAlignment`와 같은 속성을 제공합니다. 예시:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### 특정 페이지를 번호 매기기에서 제외하려면 어떻게 해야 하나요?

번호를 매기려는 페이지에 대해 별도의 `BatesNumberingArtifact`를 생성하고 해당 페이지에만 추가합니다. 아티팩트가 부착되지 않은 페이지는 번호가 매겨지지 않습니다.

### 기존 PDF에서도 작동하나요?

예. `new Document()` 대신 기존 파일을 로드합니다:

```csharp
Document pdfDocument = new Document("input.pdf");
```

그런 다음 원하는 페이지에 아티팩트를 부착하고 저장합니다.

## 결론

이제 Aspose.Pdf를 사용하여 **베이츠 번호 매기기 PDF 추가**, **빈 페이지 PDF 추가**, **프로그래밍 방식으로 PDF 생성**을 깔끔하고 재사용 가능한 C# 솔루션으로 수행하는 방법을 알게 되었습니다. 이 접근 방식은 페이지 수, 사용자 정의 접두사 및 스타일 옵션에 관계없이 작동하여 최종 문서를 완전히 제어할 수 있습니다.

다음 단계로 탐색해 볼 수 있습니다:

* **create pdf as** 사용

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 작동 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}