---
title: Aspose.Pdf for .NET을 사용하여 PDF의 테이블 셀 배경, 테두리 및 패딩을 사용자 지정합니다.
weight: 101
limit:
description: Aspose.Pdf for .NET을 사용하여 두 열 테이블이 포함된 PDF를 만들고 각 셀에 사용자 정의 배경색, 테두리 및 패딩을 적용하는 방법을 배웁니다.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.Pdf for .NET을 사용하여 두 열 테이블이 포함된 PDF를 만들고 각 셀에 사용자 정의 배경색, 테두리
    및 패딩을 적용하는 방법을 배웁니다.
  headline: Aspose.Pdf for .NET을 사용하여 PDF의 테이블 셀 배경, 테두리 및 패딩을 사용자 지정합니다.
  type: TechArticle
- description: Aspose.Pdf for .NET을 사용하여 두 열 테이블이 포함된 PDF를 만들고 각 셀에 사용자 정의 배경색, 테두리
    및 패딩을 적용하는 방법을 배웁니다.
  name: Aspose.Pdf for .NET을 사용하여 PDF의 테이블 셀 배경, 테두리 및 패딩을 사용자 지정합니다.
  steps:
  - name: using 블록 안에서 새 빈 PDF 문서를 생성합니다.
    text: using 블록 안에서 새 빈 PDF 문서를 생성합니다.
  - name: PDF 문서에 빈 페이지를 추가합니다.
    text: PDF 문서에 빈 페이지를 추가합니다.
  - name: 두 개의 200포인트 열, 얇은 검은색 외부 테두리, 기본 셀 패딩 5포인트를 가진 Table 객체를 인스턴스화합니다.
    text: 두 개의 200포인트 열, 얇은 검은색 외부 테두리, 기본 셀 패딩 5포인트를 가진 Table 객체를 인스턴스화합니다.
  - name: 테이블에 첫 번째 행을 추가합니다.
    text: 테이블에 첫 번째 행을 추가합니다.
  - name: 첫 번째 셀을 생성하고, 텍스트 "First cell"을 삽입한 뒤, 연한 노란색 배경, 빨간색 2포인트 테두리, 4포인트 마진을
      설정합니다.
    text: 첫 번째 셀을 생성하고, 텍스트 "First cell"을 삽입한 뒤, 연한 노란색 배경, 빨간색 2포인트 테두리, 4포인트 마진을
      설정합니다.
  - name: 두 번째 셀을 생성하고, 텍스트 "Second cell"을 추가한 뒤, 연한 초록색 배경, 파란색 2포인트 테두리, 4포인트 마진을
      부여합니다.
    text: 두 번째 셀을 생성하고, 텍스트 "Second cell"을 추가한 뒤, 연한 초록색 배경, 파란색 2포인트 테두리, 4포인트 마진을
      부여합니다.
  - name: 테이블에 두 번째 행을 추가합니다.
    text: 테이블에 두 번째 행을 추가합니다.
  - name: 세 번째 셀을 생성하고, "Third cell"을 삽입한 뒤, 연한 청록색 배경, 어두운 회색 2포인트 테두리, 4포인트 마진을
      설정합니다.
    text: 세 번째 셀을 생성하고, "Third cell"을 삽입한 뒤, 연한 청록색 배경, 어두운 회색 2포인트 테두리, 4포인트 마진을
      설정합니다.
  - name: 네 번째 셀을 생성하고, "Fourth cell"을 추가한 뒤, 연한 핑크색 배경, 보라색 2포인트 테두리, 4포인트 마진을 부여합니다.
    text: 네 번째 셀을 생성하고, "Fourth cell"을 추가한 뒤, 연한 핑크색 배경, 보라색 2포인트 테두리, 4포인트 마진을 부여합니다.
  - name: 완전히 스타일링된 테이블을 페이지에 추가하여 PDF에 표시되도록 합니다.
    text: 완전히 스타일링된 테이블을 페이지에 추가하여 PDF에 표시되도록 합니다.
  - name: PDF 문서를 파일에 저장하고 using 블록을 닫습니다.
    text: PDF 문서를 파일에 저장하고 using 블록을 닫습니다.
  - name: 콘솔에 확인 메시지를 출력합니다.
    text: 콘솔에 확인 메시지를 출력합니다.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding`은 모든 셀에 기본 패딩을 제공하지만, `Margin`을 할당하면(예: `cellA1.Margin
      = new MarginInfo(...)`) 해당 셀에 대해 마진 값이 기본 패딩을 덮어씁니다.'
    question: '`Table`에 설정된 `DefaultCellPadding`이 `Margin`이 정의된 셀에도 영향을 미칩니까?'
  - answer: '`Table.Border`가 없으면 전체 테이블을 둘러싼 외부 사각형이 생략되고, 설정한 개별 셀 테두리(예: `cellA2.Border`)만
      표시됩니다.'
    question: '`Table` 객체에서 `Border` 속성을 제거하면 PDF는 어떻게 보일까요?'
  - answer: '예, 특정 `BorderSide`를 사용하여 `BorderInfo`를 생성하고(예: `new BorderInfo(BorderSide.Left,
      3, Aspose.Pdf.Color.Black)`) 이를 셀의 `Border` 속성에 할당하면 됩니다.'
    question: 셀마다 서로 다른 테두리 두께를 지정할 수 있나요?
  - answer: '`Row newRow = dataTable.Rows.Add();`와 같이 새 `Row`를 인스턴스화한 뒤, 이전 행과 동일하게
      `newRow.Cells`에 셀을 추가합니다.'
    question: 위에 표시된 코드 이후에 테이블에 세 번째 행을 추가하려면 어떻게 해야 하나요?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: PDF 테이블 셀 스타일링 – 배경, 테두리, 패딩
og_description: Aspose.Pdf for .NET을 사용하여 PDF의 테이블 셀을 사용자 정의 색상, 테두리 및 간격으로 빠르게 포맷합니다.
og_image_alt: Aspose.Pdf for .NET을 사용하여 PDF의 테이블 셀 배경색, 테두리 및 패딩을 스타일링하는 방법을 보여주는 가이드
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET을 사용하여 PDF의 테이블 셀 배경, 테두리 및 패딩을 사용자 지정합니다.
이 튜토리얼에서는 PDF 문서를 생성하고, 두 열 테이블을 추가하며, 각 셀의 모양을 정확히 제어하는 방법을 보여줍니다. 배경색을 설정하고, 테두리를 정의하며, 패딩을 조정함으로써 테이블 데이터를 돋보이게 하고 깔끔하게 만들 수 있습니다. 예제는 Aspose.Pdf Document 및 Table 클래스를 사용하여 각 스타일 옵션을 시연합니다.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


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

**Q: `Table`에 설정된 `DefaultCellPadding`이 `Margin`이 정의된 셀에도 영향을 미칩니까?**  
A: `DefaultCellPadding`은 모든 셀에 기본 패딩을 제공하지만, `Margin`을 할당하면(예: `cellA1.Margin = new MarginInfo(...)`) 해당 셀에 대해 마진 값이 기본 패딩을 덮어씁니다.

**Q: `Table` 객체에서 `Border` 속성을 제거하면 PDF는 어떻게 보일까요?**  
A: `Table.Border`가 없으면 전체 테이블을 둘러싼 외부 사각형이 생략되고, 설정한 개별 셀 테두리(예: `cellA2.Border`)만 표시됩니다.

**Q: 셀마다 서로 다른 테두리 두께를 지정할 수 있나요?**  
A: 예, 특정 `BorderSide`를 사용하여 `BorderInfo`를 생성하고(예: `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) 이를 셀의 `Border` 속성에 할당하면 됩니다.

**Q: 위에 표시된 코드 이후에 테이블에 세 번째 행을 추가하려면 어떻게 해야 하나요?**  
A: `Row newRow = dataTable.Rows.Add();`와 같이 새 `Row`를 인스턴스화한 뒤, 이전 행과 동일하게 `newRow.Cells`에 셀을 추가합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}