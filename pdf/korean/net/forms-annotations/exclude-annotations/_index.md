---
title: Aspose.Pdf for .NET을 사용한 주석 제외 사이드‑바이‑사이드 PDF 비교
weight: 101
limit:
description: Aspose.Pdf for .NET을 사용하여 PDF를 비교하고 주석 영역을 제외하는 단계별 가이드.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.Pdf for .NET을 사용하여 PDF를 비교하고 주석 영역을 제외하는 단계별 가이드.
  headline: Aspose.Pdf for .NET을 사용한 주석 제외 사이드‑바이‑사이드 PDF 비교
  type: TechArticle
- description: Aspose.Pdf for .NET을 사용하여 PDF를 비교하고 주석 영역을 제외하는 단계별 가이드.
  name: Aspose.Pdf for .NET을 사용한 주석 제외 사이드‑바이‑사이드 PDF 비교
  steps:
  - name: 주 PDF, 보조 PDF 및 출력 차이 PDF의 파일 경로를 정의합니다.
    text: 주 PDF, 보조 PDF 및 출력 차이 PDF의 파일 경로를 정의합니다.
  - name: 두 입력 PDF 파일이 모두 존재하는지 확인하고, 하나라도 없을 경우 오류 메시지를 표시하고 중단합니다.
    text: 두 입력 PDF 파일이 모두 존재하는지 확인하고, 하나라도 없을 경우 오류 메시지를 표시하고 중단합니다.
  - name: 두 PDF 파일을 Document 객체(pdfA 및 pdfB)로 열고 using 블록 내에서 사용하여 자동으로 해제되도록 합니다.
    text: 두 PDF 파일을 Document 객체(pdfA 및 pdfB)로 열고 using 블록 내에서 사용하여 자동으로 해제되도록 합니다.
  - name: pdfA의 모든 주석에 대한 경계 사각형을 수집하여 ignoredRectsA에 저장합니다.
    text: pdfA의 모든 주석에 대한 경계 사각형을 수집하여 ignoredRectsA에 저장합니다.
  - name: pdfB의 모든 주석에 대한 경계 사각형을 수집하여 ignoredRectsB에 저장합니다.
    text: pdfB의 모든 주석에 대한 경계 사각형을 수집하여 ignoredRectsB에 저장합니다.
  - name: SideBySideComparisonOptions 객체를 생성하고 이전에 수집한 주석 사각형을 ExcludeAreas1 및 ExcludeAreas2에
      할당하여 비교 시 해당 영역을 무시하도록 합니다.
    text: SideBySideComparisonOptions 객체를 생성하고 이전에 수집한 주석 사각형을 ExcludeAreas1 및 ExcludeAreas2에
      할당하여 비교 시 해당 영역을 무시하도록 합니다.
  - name: 두 Document 객체와 구성된 옵션을 사용하여 사이드‑바이‑사이드 PDF 비교를 실행하고 결과를 outputPdf에 기록합니다.
    text: 두 Document 객체와 구성된 옵션을 사용하여 사이드‑바이‑사이드 PDF 비교를 실행하고 결과를 outputPdf에 기록합니다.
  - name: Document 객체를 해제하고 using 블록을 종료합니다.
    text: Document 객체를 해제하고 using 블록을 종료합니다.
  - name: 비교가 완료되었으며 차이 PDF가 저장된 위치를 나타내는 확인 메시지를 출력합니다.
    text: 비교가 완료되었으며 차이 PDF가 저장된 위치를 나타내는 확인 메시지를 출력합니다.
  type: HowTo
- questions:
  - answer: 예. 코드는 해당 `ignoredRects` 리스트에 사각형을 추가하지 않을 뿐이므로 `ExcludeAreas1`/`ExcludeAreas2`는
      빈 배열을 받게 되고 비교자는 전체 페이지를 처리합니다.
    question: PDF 페이지에 주석이 없으면 어떻게 되나요 – 비교가 여전히 작동합니까?
  - answer: '`ExcludeAreas1`(또는 `ExcludeAreas2`)을 수집된 사각형으로 설정하고 다른 속성은 빈 배열로 두면,
      비교자는 지정된 문서의 영역만 무시합니다.'
    question: 한 문서의 주석만 제외하고 다른 문서의 주석은 차이에 포함하도록 할 수 있나요?
  - answer: 겹치는 사각형은 비교자에 의해 내부적으로 병합되므로, 겹치는 주석 경계가 중복 계산 없이 안전하게 제외됩니다.
    question: 겹치는 주석 사각형이 `ExcludeAreas`에 문제를 일으키나요?
  - answer: 예, `compareOpts.ExcludeTables = true;` 로 설정하면 이 플래그가 `ExcludeAreas1`/`ExcludeAreas2`와
      함께 작동하여 표 영역도 무시합니다.
    question: 같은 옵션 객체를 사용하여 주석 외에 표도 제외할 수 있는 방법이 있나요?
  - answer: 코드는 리스트에 추가하기 전에 `if (a != null && a.Rect != null)` 를 확인하므로 null 사각형은
      그냥 건너뛰며 예외가 발생하지 않습니다.
    question: 주석의 `Rect` 속성이 null이면 어떻게 되나요 – 코드가 예외를 발생합니까?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: 주석 없이 PDF 비교
og_description: 모든 주석 표시를 건너뛰는 사이드‑바이‑사이드 PDF 차이를 실행합니다.
og_image_alt: Aspose.Pdf for .NET을 사용하여 주석 영역을 제외하는 사이드‑바이‑사이드 PDF 비교를 보여주는 가이드
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET을 사용한 주석 제외 사이드‑바이‑사이드 PDF 비교
이 튜토리얼은 Aspose.Pdf for .NET을 사용하여 두 PDF 파일을 비교하면서 모든 주석 내용을 무시하는 방법을 보여줍니다. 각 문서에서 모든 주석의 경계 상자를 추출하고 해당 영역을 SideBySideComparisonOptions에 전달한 뒤 사이드‑바이‑사이드 비교를 수행합니다. 결과는 주석이 아닌 변경 사항만 강조 표시된 차이 PDF입니다.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: PDF 페이지에 주석이 없으면 어떻게 되나요 – 비교가 여전히 작동합니까?**  
A: 예. 코드는 해당 `ignoredRects` 리스트에 사각형을 추가하지 않을 뿐이므로 `ExcludeAreas1`/`ExcludeAreas2`는 빈 배열을 받게 되고 비교자는 전체 페이지를 처리합니다.

**Q: 한 문서의 주석만 제외하고 다른 문서의 주석은 차이에 포함하도록 할 수 있나요?**  
A: `ExcludeAreas1`(또는 `ExcludeAreas2`)을 수집된 사각형으로 설정하고 다른 속성은 빈 배열로 두면, 비교자는 지정된 문서의 영역만 무시합니다.

**Q: 겹치는 주석 사각형이 `ExcludeAreas`에 문제를 일으키나요?**  
A: 겹치는 사각형은 비교자에 의해 내부적으로 병합되므로, 겹치는 주석 경계가 중복 계산 없이 안전하게 제외됩니다.

**Q: 같은 옵션 객체를 사용하여 주석 외에 표도 제외할 수 있는 방법이 있나요?**  
A: 예, `compareOpts.ExcludeTables = true;` 로 설정하면 이 플래그가 `ExcludeAreas1`/`ExcludeAreas2`와 함께 작동하여 표 영역도 무시합니다.

**Q: 주석의 `Rect` 속성이 null이면 어떻게 되나요 – 코드가 예외를 발생합니까?**  
A: 코드는 리스트에 추가하기 전에 `if (a != null && a.Rect != null)` 를 확인하므로 null 사각형은 그냥 건너뛰며 예외가 발생하지 않습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}