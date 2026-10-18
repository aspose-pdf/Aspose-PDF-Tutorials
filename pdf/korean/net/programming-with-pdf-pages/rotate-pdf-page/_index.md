---
title: Aspose.PDF for .NET을 사용하여 단일 PDF 페이지를 180도 회전하기
weight: 260
limit:
description: Aspose.PDF for .NET을 사용하여 PDF의 세 번째 페이지를 180° 회전하는 방법을 배워보세요.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.PDF for .NET을 사용하여 PDF의 세 번째 페이지를 180° 회전하는 방법을 배워보세요.
  headline: Aspose.PDF for .NET을 사용하여 단일 PDF 페이지를 180도 회전하기
  type: TechArticle
- description: Aspose.PDF for .NET을 사용하여 PDF의 세 번째 페이지를 180° 회전하는 방법을 배워보세요.
  name: Aspose.PDF for .NET을 사용하여 단일 PDF 페이지를 180도 회전하기
  steps:
  - name: 이 파일은 설명용 주석만 포함하고 실행 가능한 코드는 없으며, 원본 예제의 자리표시자 역할을 합니다.
    text: 이 파일은 설명용 주석만 포함하고 실행 가능한 코드는 없으며, 원본 예제의 자리표시자 역할을 합니다.
  type: HowTo
- questions:
  - answer: 'SDK의 페이지 컬렉션을 0부터 시작하는 인덱스로 사용하세요. 예: `pdfDocument.Pages[2]`는 세 번째 페이지에
      해당합니다.'
    question: PDF에서 회전할 세 번째 페이지를 어떻게 지정하나요?
  - answer: 회전 속성은 0, 90, 180, 270도 네 가지 표준 값만 허용하며, 다른 값은 가장 가까운 허용 각도로 반올림됩니다.
    question: 180도가 아닌 다른 각도로 페이지를 회전할 수 있나요?
  - answer: 회전은 메모리 상의 `PdfDocument`에만 적용됩니다. 변경 사항을 새 파일에 기록하려면 `pdfDocument.Save("output.pdf")`(또는
      유사한 저장 메서드)를 호출해야 하며, 원본 파일은 그대로 유지됩니다.
    question: 페이지를 회전하면 원본 파일이 자동으로 수정되나요?
  - answer: SDK는 주석 및 양식 필드의 위치를 자동으로 재계산하여 새로운 방향에 맞게 올바르게 정렬되도록 합니다.
    question: 페이지가 회전된 후 주석이나 양식 필드는 어떻게 되나요?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: Aspose.PDF를 사용하여 PDF 페이지를 180° 회전하기
og_description: 몇 줄의 Aspose.PDF for .NET 코드만으로 PDF의 세 번째 페이지를 손쉽게 뒤집어 보세요.
og_image_alt: Aspose.PDF for .NET을 사용하여 PDF의 세 번째 페이지를 180도 회전하는 코드를 보여주는 가이드.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF for .NET을 사용하여 단일 PDF 페이지를 180도 회전하기
이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF 문서의 세 번째 페이지를 180도 회전하는 방법을 배웁니다. 예제는 PDF를 로드하고, 3페이지를 선택한 뒤 회전을 적용하고, 업데이트된 파일을 저장하는 과정을 단계별로 보여줍니다. 이 방법을 사용하면 나머지 페이지의 방향은 그대로 두고 특정 페이지만 뒤집을 수 있습니다.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: PDF에서 회전할 세 번째 페이지를 어떻게 지정하나요?**  
A: SDK의 페이지 컬렉션을 0부터 시작하는 인덱스로 사용하세요. 예: `pdfDocument.Pages[2]`는 세 번째 페이지에 해당합니다.

**Q: 180도가 아닌 다른 각도로 페이지를 회전할 수 있나요?**  
A: 회전 속성은 0, 90, 180, 270도 네 가지 표준 값만 허용하며, 다른 값은 가장 가까운 허용 각도로 반올림됩니다.

**Q: 페이지를 회전하면 원본 파일이 자동으로 수정되나요?**  
A: 회전은 메모리 상의 `PdfDocument`에만 적용됩니다. 변경 사항을 새 파일에 기록하려면 `pdfDocument.Save("output.pdf")`(또는 유사한 저장 메서드)를 호출해야 하며, 원본 파일은 그대로 유지됩니다.

**Q: 페이지가 회전된 후 주석이나 양식 필드는 어떻게 되나요?**  
A: SDK는 주석 및 양식 필드의 위치를 자동으로 재계산하여 새로운 방향에 맞게 올바르게 정렬되도록 합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}