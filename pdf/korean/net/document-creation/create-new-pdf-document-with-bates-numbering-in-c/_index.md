---
category: general
date: 2026-08-04
description: C#에서 새 PDF 문서를 만들고 Aspose.Pdf를 사용해 베이츠 번호 매김 PDF를 빠르게 추가하세요 – 빈 페이지 PDF와
  사용자 지정 페이지 번호 추가 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: ko
lastmod: 2026-08-04
og_description: C#에서 새 PDF 문서를 생성하고 법률 사건 관리를 위해 베이츠 번호를 자동으로 추가합니다 – 전체 코드 예제 포함.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: C#로 베이츠 번호가 포함된 새 PDF 문서 만들기
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: C#에서 베이츠 번호가 포함된 새 PDF 문서 만들기
url: /ko/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 Bates 번호가 포함된 새 PDF 문서 만들기

C#에서 **새 PDF 문서**를 만들어야 할 때, 이 가이드는 Aspose.Pdf를 사용하여 **Bates 번호가 포함된 PDF**를 **추가하는 방법**을 보여줍니다. **빈 페이지 PDF 추가**, **사용자 지정 페이지 번호 추가** 구성, 최종 파일 저장 방법을 배울 수 있습니다.

이 튜토리얼은 라이브러리 설치부터 법적 사건 파일 표준을 충족하는 PDF 생성까지 모든 단계를 다룹니다. 끝까지 따라 하면 PDF를 생성하고, 빈 페이지를 삽입하고, Bates 번호를 적용하고, 번호 형식을 사용자 지정하는 단일 실행 가능한 프로그램을 만들 수 있습니다.

## 전제 조건

시작하기 전에 다음이 설치되어 있는지 확인하세요:

* .NET 6.0 SDK 이상  
* Visual Studio 2022 (또는 기타 C# IDE)  
* 활성화된 Aspose.Pdf for .NET 라이선스 또는 무료 평가 키  

추가 NuGet 패키지는 필요하지 않습니다; 튜토리얼이 모든 것을 자동으로 설치합니다.

## 1단계: NuGet을 통해 Aspose.Pdf 설치

프로젝트 폴더에서 터미널을 열고 다음을 실행합니다:

```bash
dotnet add package Aspose.Pdf
```

이 명령은 최신 안정 버전의 Aspose.Pdf를 프로젝트에 추가하며, `Document`, `BatesNumbering` 등 PDF 조작에 필요한 클래스를 제공합니다.

## 2단계: 새 PDF 문서 만들기 – 초기 설정

PDF 파일을 만드는 것은 이후 모든 작업의 기반이 됩니다. `Document` 클래스는 전체 PDF 컨테이너를 나타냅니다.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*왜 중요한가*: `Document`를 인스턴스화하면 페이지, 폰트, 그래픽에 필요한 내부 구조가 할당됩니다. `using var`를 사용하면 저장 후 파일이 올바르게 해제됩니다.

## 3단계: 빈 페이지 PDF 추가

내용을 배치하기 전에 PDF에 최소 한 페이지가 있어야 합니다. 빈 페이지를 추가하면 Bates 번호를 위한 깨끗한 캔버스를 얻을 수 있습니다.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

`Pages.Add()` 메서드는 문서의 페이지 컬렉션 끝에 새로운 빈 페이지를 추가합니다. 이후 **사용자 지정 페이지 번호 추가**가 필요할 경우 이 호출을 반복하여 여러 페이지를 추가할 수 있습니다.

## 4단계: Bates 번호 구성 – Bates 추가 방법

Bates 번호는 법률 문서에서 흔히 사용되는 순차 식별자입니다. `BatesNumbering` 클래스를 통해 구성합니다.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*왜 중요한가*: `StartNumber`는 첫 번째 번호를 정의하고, `Prefix`는 읽기 쉬운 라벨을 추가하며, `Increment`는 증가 폭을 제어합니다. `HorizontalAlignment`, `VerticalAlignment`, `FontSize`, `Margins` 등을 조정하여 각 페이지에 표시되는 번호의 모양을 제어할 수 있습니다.

## 5단계: 페이지에 Bates 번호 PDF 적용

번호 옵션이 준비되었으니 이제 페이지(또는 전체 문서)에 적용합니다.

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

`Apply`를 호출하면 기본적으로 페이지 하단에 서식이 지정된 번호가 삽입됩니다. 다른 위치에 번호가 필요하면 `Apply` 호출 전에 `bates.Position`을 설정하세요.

## 6단계: Bates 번호가 적용된 PDF 저장

마지막으로 메모리 상의 문서를 디스크에 기록합니다.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

저장된 파일에는 **CaseA-1000**이라는 Bates 번호가 하단에 표시된 단일 페이지가 포함됩니다. PDF 뷰어에서 열어 번호가 제대로 표시되는지 확인하세요.

## 예상 출력

`BatesNumbered.pdf`를 열면 다음과 같이 표시됩니다:

* 하나의 빈 페이지(추가 페이지를 만든 경우 더 많음)  
* 페이지 하단(기본 위치)에 **CaseA-1000** 텍스트가 표시됨  

같은 `BatesNumbering` 인스턴스를 재사용하여 페이지를 추가하면 번호가 자동으로 증가합니다 (CaseA-1001, CaseA-1002, …).

## 팁: Bates 번호와 함께 사용자 지정 페이지 번호 추가

때때로 Bates 번호와 전통적인 페이지 번호를 모두 표시해야 할 때가 있습니다. Bates 번호 적용 후 `TextFragment`를 추가하면 두 번호를 동시에 표시할 수 있습니다:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

이 스니펫은 **사용자 지정 페이지 번호 추가**를 보여 주면서 Bates 라벨을 유지합니다.

## 엣지 케이스: 여러 페이지에 Bates 번호 적용

문서에 여러 페이지가 포함된 경우, 루프를 사용해 동일한 `BatesNumbering` 인스턴스를 각 페이지에 적용할 수 있습니다:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

루프는 `StartNumber`와 `Increment`에 따라 각 페이지에 순차 번호가 부여되도록 보장합니다.

## 흔히 발생하는 문제와 해결 방법

| 문제 | 발생 원인 | 해결 방법 |
|------|----------|-----------|
| 번호가 중앙에서 벗어남 | 기본 정렬이 레이아웃과 맞지 않음 | `bates.HorizontalAlignment`와 `bates.VerticalAlignment`를 명시적으로 설정 |
| 번호가 기존 내용과 겹침 | 마진이 정의되지 않음 | `bates.Margin`을 조정하거나 `bates.Position`으로 번호 위치 이동 |
| 런타임에 라이선스 예외 발생 | 평가 버전이 출력 제한을 가짐 | 문서 생성 전에 유효한 Aspose.Pdf 라이선스를 적용 (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## 전체 작업 예제

아래는 복사·붙여넣기 후 바로 실행할 수 있는 독립형 프로그램입니다.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하는 관련 주제를 다룹니다. 각 리소스는 단계별 설명과 완전한 코드 예제를 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}