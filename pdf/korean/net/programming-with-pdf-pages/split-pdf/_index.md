---
title: Aspose.Pdf for .NET을 사용하여 열 번째 페이지 이후 PDF 분할
weight: 360
limit:
description: Aspose.Pdf for .NET을 사용하여 열 번째 페이지 직후에 PDF 문서를 분할하는 단계별 코드.
keywords: [pdf split, Aspose.Pdf for .NET, split PDF after page, extract pages from PDF, c# pdf split, pdf pagination]
url: /net/programming-with-pdf-pages/split-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.Pdf for .NET을 사용하여 열 번째 페이지 직후에 PDF 문서를 분할하는 단계별 코드.
  headline: Aspose.Pdf for .NET을 사용하여 열 번째 페이지 이후 PDF 분할
  type: TechArticle
- description: Aspose.Pdf for .NET을 사용하여 열 번째 페이지 직후에 PDF 문서를 분할하는 단계별 코드.
  name: Aspose.Pdf for .NET을 사용하여 열 번째 페이지 이후 PDF 분할
  steps:
  - name: 헤더 주석은 예제의 목적을 설명하고 전체 코드가 이동되었음을 알리며 최신 소스에 대한 링크를 제공합니다.
    text: 헤더 주석은 예제의 목적을 설명하고 전체 코드가 이동되었음을 알리며 최신 소스에 대한 링크를 제공합니다.
  - name: 스텁 라인은 아무 작업도 수행하지 않으며 원래 URL을 작동 상태로 유지하기 위해 존재합니다.
    text: 스텁 라인은 아무 작업도 수행하지 않으며 원래 URL을 작동 상태로 유지하기 위해 존재합니다.
  type: HowTo
- questions:
  - answer: Aspose.Pdf는 오류를 발생시키지 않으며, `Split` 메서드는 열 번째 이후에 시작할 페이지가 없기 때문에 원본 문서를
      그대로 반환합니다.
    question: 원본 PDF에 열 페이지보다 적은 페이지가 있으면 어떻게 되나요?
  - answer: '`PdfDocument` 인스턴스에서 `PdfDocument.Split(pageNumber)`를 호출하고 `pageNumber`에
      `10`을 전달하여 두 개의 별도 문서를 생성합니다.'
    question: PDF를 열 번째 페이지에서 분할할 때 사용되는 클래스와 메서드는 무엇인가요?
  - answer: 예, Aspose.Pdf는 결과 분할 문서에서 모든 페이지 수준 객체(북마크, 주석, 양식 필드 등)를 보존하여 원본 페이지에
      연결된 상태로 유지합니다.
    question: 분할 후에도 북마크, 주석 및 양식 필드가 원래 페이지에 그대로 유지되나요?
  - answer: '`Split`을 호출하면 두 개의 `PdfDocument` 객체를 받게 되며, 첫 번째에는 `Save(\"FirstPart.pdf\")`를,
      두 번째에는 `Save(\"SecondPart.pdf\")`를 호출하여 각각 별도의 파일 이름을 지정해야 합니다.'
    question: 분할로 생성된 두 부분의 출력 파일 이름은 어떻게 지정해야 하나요?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/split-pdf/og-image.png
og_title: 페이지 10 이후 PDF 분할
og_description: Aspose.Pdf for .NET을 사용하여 페이지 10에서 PDF를 분할하는 간단한 튜토리얼.
og_image_alt: Aspose.Pdf for .NET을 사용하여 열 번째 페이지 이후에 PDF를 분할하는 방법을 보여주는 가이드
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET을 사용하여 열 번째 페이지 이후 PDF 분할
PDF를 별개의 문서로 분할하면 배포와 처리를 단순화할 수 있습니다. 이 튜토리얼에서는 Aspose.Pdf for .NET을 사용하여 열 번째 페이지 직후에 PDF를 분할하고 두 개의 별도 파일을 만드는 방법을 단계별로 안내합니다. 몇 줄의 C# 코드만으로 처음 열 페이지와 나머지 페이지를 추출하는 과정을 따라해 보세요.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/split-pdf" >}}


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

**Q: 원본 PDF에 열 페이지보다 적은 페이지가 있으면 어떻게 되나요?**  
A: Aspose.Pdf는 오류를 발생시키지 않으며, `Split` 메서드는 열 번째 이후에 시작할 페이지가 없기 때문에 원본 문서를 그대로 반환합니다.

**Q: PDF를 열 번째 페이지에서 분할할 때 사용되는 클래스와 메서드는 무엇인가요?**  
A: `PdfDocument` 인스턴스에서 `PdfDocument.Split(pageNumber)`를 호출하고 `pageNumber`에 `10`을 전달하여 두 개의 별도 문서를 생성합니다.

**Q: 분할 후에도 북마크, 주석 및 양식 필드가 원래 페이지에 그대로 유지되나요?**  
A: 예, Aspose.Pdf는 결과 분할 문서에서 모든 페이지 수준 객체(북마크, 주석, 양식 필드 등)를 보존하여 원본 페이지에 연결된 상태로 유지합니다.

**Q: 분할로 생성된 두 부분의 출력 파일 이름은 어떻게 지정해야 하나요?**  
A: `Split`을 호출하면 두 개의 `PdfDocument` 객체를 받게 되며, 첫 번째에는 `Save(\"FirstPart.pdf\")`를, 두 번째에는 `Save(\"SecondPart.pdf\")`를 호출하여 각각 별도의 파일 이름을 지정해야 합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}