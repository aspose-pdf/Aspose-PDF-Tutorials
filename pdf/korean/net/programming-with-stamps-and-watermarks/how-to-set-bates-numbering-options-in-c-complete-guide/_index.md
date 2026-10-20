---
category: general
date: 2026-08-14
description: GroupDocs를 사용하여 C#에서 베이츠 번호 매기기 옵션을 설정하는 방법. Word를 PDF로 변환할 때 사용자 정의
  접두사와 시작 번호를 추가하는 단계별 튜토리얼을 따라보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: ko
lastmod: 2026-08-14
og_description: C#에서 베이츠 번호 매기기 옵션을 빠르게 설정하는 방법. 이 가이드는 Word를 PDF로 변환할 때 사용자 지정 접두사와
  시작 번호를 추가하는 방법을 보여줍니다.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: C#에서 베이츠 번호 매기기 옵션 설정 방법 – 단계별 튜토리얼
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: C#에서 베이츠 번호 매기기 옵션 설정 방법 – 완전 가이드
url: /ko/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 베이츠 번호 매기기 옵션 설정 방법 – 완전 가이드

C#에서 **베이츠 번호 매기기 옵션 설정 방법**이 필요하다면, 이 가이드는 정확한 단계들을 안내합니다. 시작 번호를 설정하고, 접두사를 추가하며, GroupDocs API를 사용해 Word 문서를 PDF로 변환하면서 번호 매기기를 적용하는 방법을 배울 수 있습니다.

문서 처리는 법적 또는 보관 목적을 위해 각 페이지에 고유 식별자를 부여해야 할 때가 많습니다. 이 튜토리얼을 마치면 소송 지원 도구든 자동 보고서 생성기든 관계없이 .NET 프로젝트에 바로 삽입할 수 있는 재사용 가능한 코드 조각을 얻게 됩니다. 외부 도구는 필요 없습니다—GroupDocs.Conversion 라이브러리와 몇 줄의 C#만 있으면 됩니다.

## 필요한 사항

시작하기 전에 다음이 설치되어 있는지 확인하세요:

* .NET 6.0 SDK 이상 설치  
* Visual Studio 2022(또는 .NET을 지원하는 IDE)  
* 유효한 GroupDocs.Conversion 라이선스(무료 체험판도 테스트에 사용 가능)  
* 번호를 매기고 싶은 샘플 Word 문서 (`input.docx`)  

이 전제 조건들은 추가 설정 없이 코드를 실행할 수 있게 해 줍니다.

## 베이츠 번호 매기기 옵션 설정 방법 – 개요

**베이츠 번호 매기기 옵션 설정 방법**의 핵심은 세 가지 객체에 있습니다:

1. `Document` – 소스 파일을 로드합니다.  
2. `BatesNumberingOptions` – 시작 번호, 접두사 및 기타 서식 세부 정보를 보관합니다.  
3. `AddBatesNumbering` – 각 페이지에 번호를 삽입하는 메서드입니다.

각 요소가 존재하는 이유를 이해하면 사용자 지정 글꼴이나 다국어 번호 매기기와 같은 복잡한 시나리오에도 솔루션을 쉽게 적용할 수 있습니다.

## 단계 1: GroupDocs.Conversion NuGet 패키지 설치

솔루션 폴더에서 터미널을 열고 다음을 실행하세요:

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API**는 튜토리얼 후반에 사용할 `Document` 클래스와 `AddBatesNumbering` 확장 메서드를 제공합니다.

## 단계 2: 소스 문서 로드

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*왜 이 단계인가?*  
파일을 로드하면 변환 엔진이 조작할 수 있는 메모리 내 표현이 생성됩니다. `Document` 인스턴스가 없으면 베이츠 번호 매기기나 다른 변환을 적용할 수 없습니다.

## 단계 3: 베이츠 번호 매기기 옵션 생성

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*왜 이 단계인가?*  
`BatesNumberingOptions`는 **베이츠 번호 매기기 옵션 설정** 시 필요할 수 있는 모든 설정을 캡슐화합니다. `StartNumber`와 `Prefix`를 조정하면 출력이 케이스 관리 시스템과 일치하도록 할 수 있습니다. `Position` 속성은 시각적 배치를 제어하는데, 이는 종종 규정 준수 요구 사항이 됩니다.

## 단계 4: 문서에 베이츠 번호 매기기 적용

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

`AddBatesNumbering` 메서드는 로드된 `Document`의 각 페이지를 순회하면서 구성된 문자열을 삽입합니다. 메서드가 메모리 내 표현에서 작동하기 때문에 저장하기 전에 워터마킹과 같은 추가 처리 단계를 체인처럼 연결할 수 있습니다.

## 단계 5: 결과를 PDF로 변환 및 저장

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*왜 이 단계인가?*  
PDF는 법률 문서의 일반적인 최종 형식입니다. `PdfConvertOptions` 객체를 사용하면 출력물을 세밀하게 조정할 수 있지만 기본 번호 매기기에는 필요하지 않습니다. `Save` 호출은 완전히 번호가 매겨진 PDF를 디스크에 기록합니다.

## 완전한 실행 예제

모든 코드를 합치면 다음과 같은 독립 실행형 콘솔 애플리케이션을 컴파일하고 실행할 수 있습니다:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**예상 출력**

프로그램을 실행하면 `output.pdf`가 생성되며, 각 페이지에 `CASE-1000`, `CASE-1001` 등과 같은 라벨이 오른쪽 바닥글에 표시됩니다. PDF 뷰어에서 열어 번호가 의도대로 나타나는지 확인하세요.

## 일반적인 함정 및 모범 사례

| 문제 | 발생 원인 | 예방 방법 |
|-------|----------------|-----------------|
| **상대 경로가 `FileNotFoundException`을 발생시킴** | 콘솔 앱의 작업 디렉터리가 Visual Studio와 다를 수 있습니다. | 절대 경로를 사용하거나 `Path.Combine(AppContext.BaseDirectory, "input.docx")`를 사용하세요. |
| **번호가 기존 바닥글과 겹침** | 소스 문서에 선택한 바닥글 영역에 이미 내용이 있으면 새 번호가 가려질 수 있습니다. | `Position`을 다른 값(예: `HeaderLeft`)으로 선택하거나 소스 템플릿을 조정하세요. |
| **대용량 문서는 느림** | 베이츠 번호 매기기가 각 페이지를 순회하므로 파일 크기에 따라 메모리 사용량이 증가합니다. | 500페이지를 초과하면 `Document.Split`을 사용해 문서를 청크 단위로 처리하세요. |
| **라이선스 만료** | GroupDocs 무료 체험판은 30일 후 만료되어 `AddBatesNumbering`에서 예외가 발생합니다. | 문서를 로드하기 전에 유효한 라이선스 키를 적용하세요: `License license = new License(); license.SetLicense("license.lic");`. |

**Pro tip:** 케이스마다 다른 번호 형식이 필요하면(예: `2023-CASE-001`) `BatesNumberingOptions`를 만들기 전에 접두사를 동적으로 구성하세요.

## 솔루션 확장

동일한 **Bates numbering C#** 접근 방식은 `.txt`, `.html` 또는 이미지와 같은 다른 소스 형식에서도 작동합니다. `Document` 객체를 만들 때 파일 확장자를 바꾸기만 하면 변환 엔진이 나머지를 처리합니다.

또한 **document conversion C#**을 OCR과 결합해 스캔된 PDF를 처리할 수도 있습니다:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## 결론

이제 C#에서 **베이츠 번호 매기기 옵션 설정 방법**을 처음부터 끝까지 알게 되었습니다. `BatesNumberingOptions` 객체를 생성하고, `AddBatesNumbering`으로 적용한 뒤 PDF로 저장하면 법적 요구 사항을 충족하는 고유 식별 문서를 자동으로 생성할 수 있습니다.  

이후에는 **C# PDF generation**, **document conversion C#**, 워터마킹 및 디지털 서명과 같은 고급 **GroupDocs API** 기능을 탐색해 보세요. 다양한 접두사, 위치 및 번호 형식을 실험해 워크플로에 맞게 최적화하십시오.

코딩 즐겁게 하세요!

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하여 밀접하게 관련된 주제를 다룹니다. 각 리소스에는 완전한 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 적용할 수 있는 다양한 구현 방식을 탐색할 수 있습니다.

- [C#에서 베이츠 번호 매기기 PDF 추가 – 완전 가이드](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [Aspose.PDF for .NET을 사용해 PDF에 페이지 번호 추가 및 맞춤 설정 방법 | 문서 조작 가이드](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF for .NET을 사용해 PDF에 텍스트 스탬프 바닥글 추가 방법&#58; 단계별 가이드](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}