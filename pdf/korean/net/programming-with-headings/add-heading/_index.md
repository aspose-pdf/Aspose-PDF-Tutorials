---
title: Aspose.PDF for .NET을 사용하여 PDF에 헤딩, 언어 및 제목 추가
weight: 110
limit:
description: Aspose.PDF for .NET을 사용하여 PDF를 생성하고, 언어와 제목을 설정한 뒤 레벨‑1 헤딩을 추가합니다.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Aspose.PDF for .NET을 사용하여 PDF를 생성하고, 언어와 제목을 설정한 뒤 레벨‑1 헤딩을 추가합니다.
  headline: Aspose.PDF for .NET을 사용하여 PDF에 헤딩, 언어 및 제목 추가
  type: TechArticle
- description: Aspose.PDF for .NET을 사용하여 PDF를 생성하고, 언어와 제목을 설정한 뒤 레벨‑1 헤딩을 추가합니다.
  name: Aspose.PDF for .NET을 사용하여 PDF에 헤딩, 언어 및 제목 추가
  steps:
  - name: 생성된 PDF의 출력 파일 이름을 정의합니다.
    text: 생성된 PDF의 출력 파일 이름을 정의합니다.
  - name: '`using` 블록 안에서 새로운 빈 PDF 문서 인스턴스(`pdfDoc`)를 생성합니다.'
    text: '`using` 블록 안에서 새로운 빈 PDF 문서 인스턴스(`pdfDoc`)를 생성합니다.'
  - name: 태그된 PDF 구조를 작업하기 위해 `ITaggedContent` 인터페이스를 얻습니다.
    text: 태그된 PDF 구조를 작업하기 위해 `ITaggedContent` 인터페이스를 얻습니다.
  - name: 문서의 기본 언어를 English (US)로 설정하고 제목 메타데이터를 할당합니다.
    text: 문서의 기본 언어를 English (US)로 설정하고 제목 메타데이터를 할당합니다.
  - name: 논리 구조 트리의 루트 요소를 가져옵니다.
    text: 논리 구조 트리의 루트 요소를 가져옵니다.
  - name: 레벨‑1 헤더 요소를 만들고, 표시 텍스트를 설정하며, 언어를 지정합니다.
    text: 레벨‑1 헤더 요소를 만들고, 표시 텍스트를 설정하며, 언어를 지정합니다.
  - name: 헤더 요소를 루트에 추가하여 헤딩이 PDF에 표시되도록 합니다.
    text: 헤더 요소를 루트에 추가하여 헤딩이 PDF에 표시되도록 합니다.
  - name: PDF를 지정된 파일에 저장하고 문서 범위를 닫습니다.
    text: PDF를 지정된 파일에 저장하고 문서 범위를 닫습니다.
  - name: 콘솔에 확인 메시지를 출력합니다.
    text: 콘솔에 확인 메시지를 출력합니다.
  type: HowTo
- questions:
  - answer: '`SetLanguage`는 문서 전체 논리 구조의 기본 언어를 정의합니다; 자체 언어가 설정되지 않은 모든 요소는 "en-US"를
      상속합니다.'
    question: '`tagContent.SetLanguage("en-US")`를 호출하면 PDF에 어떤 효과가 있나요?'
  - answer: '`header.Language` 설정은 선택 사항입니다; 예제와 같이 다른 값을 지정하지 않으면 헤딩은 문서의 기본 언어를
      상속합니다.'
    question: 문서에 이미 `SetLanguage`를 호출했는데 `header.Language`를 설정해야 하나요?
  - answer: '`tagContent.CreateHeaderElement(2)`를 사용하여 레벨‑2 헤딩을 만들 수 있습니다; 숫자 인자는
      PDF 구조 트리에서 반영되는 헤딩 레벨을 지정합니다.'
    question: 레벨‑1 헤딩이 아니라 레벨‑2 헤딩을 만들려면 어떻게 해야 하나요?
  - answer: '`SetTitle`은 제공된 문자열을 PDF 문서 메타데이터의 제목 필드에 기록합니다. 이 제목은 PDF 리더에서 확인할 수
      있으며 검색이나 인덱싱에 사용됩니다.'
    question: '`tagContent.SetTitle("PDF Example with Header")`는 무엇을 하나요?'
  - answer: 헤딩 요소가 논리 구조 트리에 추가되지 않으므로 PDF 출력에 나타나지 않으며 접근성 도구에서 헤딩으로 인식되지 않습니다.
    question: '`rootElement.AppendChild(header)`를 생략하면 어떻게 되나요?'
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: PDF에 헤딩을 삽입하고 언어를 설정하기
og_description: .NET 코드 몇 줄로 PDF를 생성하고, 언어와 제목을 설정한 뒤 레벨‑1 헤딩을 추가하는 방법을 배웁니다.
og_image_alt: Aspose.PDF for .NET을 사용하여 PDF에 헤딩을 추가하고, 언어와 제목을 설정하는 방법을 보여주는 가이드
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF for .NET을 사용하여 PDF에 헤딩, 언어 및 제목 추가
이 튜토리얼은 Aspose.PDF for .NET을 사용하여 새 PDF 문서를 만들고, 기본 언어와 문서 제목을 지정하며, 레벨‑1 헤딩을 삽입하는 과정을 단계별로 안내합니다. Document, ITaggedContent, StructureElement, HeaderElement 클래스를 활용하여 접근성 도구에 적합한 올바르게 태그된 PDF를 만드는 방법을 확인할 수 있습니다.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: `tagContent.SetLanguage("en-US")`를 호출하면 PDF에 어떤 효과가 있나요?**  
A: `SetLanguage`는 문서 전체 논리 구조의 기본 언어를 정의합니다; 자체 언어가 설정되지 않은 모든 요소는 "en-US"를 상속합니다.

**Q: 문서에 이미 `SetLanguage`를 호출했는데 `header.Language`를 설정해야 하나요?**  
A: `header.Language` 설정은 선택 사항입니다; 예제와 같이 다른 값을 지정하지 않으면 헤딩은 문서의 기본 언어를 상속합니다.

**Q: 레벨‑1 헤딩이 아니라 레벨‑2 헤딩을 만들려면 어떻게 해야 하나요?**  
A: `tagContent.CreateHeaderElement(2)`를 사용하여 레벨‑2 헤딩을 만들 수 있습니다; 숫자 인자는 PDF 구조 트리에서 반영되는 헤딩 레벨을 지정합니다.

**Q: `tagContent.SetTitle("PDF Example with Header")`는 무엇을 하나요?**  
A: `SetTitle`은 제공된 문자열을 PDF 문서 메타데이터의 제목 필드에 기록합니다. 이 제목은 PDF 리더에서 확인할 수 있으며 검색이나 인덱싱에 사용됩니다.

**Q: `rootElement.AppendChild(header)`를 생략하면 어떻게 되나요?**  
A: 헤딩 요소가 논리 구조 트리에 추가되지 않으므로 PDF 출력에 나타나지 않으며 접근성 도구에서 헤딩으로 인식되지 않습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}