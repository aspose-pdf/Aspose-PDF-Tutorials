---
"description": "Aspose.PDF for .NET을 사용하여 PDF에서 이미지 주위에 텍스트를 배치하는 방법을 알아보세요. 단계별 가이드를 따라 이미지와 텍스트가 나란히 배치된 전문적인 PDF를 만들어 보세요."
"linktitle": "PDF 파일에서 이미지 주위에 텍스트 배치"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에서 이미지 주위에 텍스트 배치"
"url": "/ko/net/programming-with-text/placing-text-around-image/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에서 이미지 주위에 텍스트 배치

## 소개

PDF 파일에서 이미지 주위에 텍스트를 배치하려고 했지만 쉽지 않았던 경험이 있으신가요? 그렇다면 잘 찾아오셨습니다! Aspose.PDF for .NET을 사용하면 몇 줄의 코드만으로 이미지 주위에 텍스트를 배치할 수 있어 이 과정이 훨씬 간편해집니다. 보고서, 문서 또는 프레젠테이션을 만들 때 이 기능은 콘텐츠 레이아웃을 개선하고 시각적으로 더욱 매력적으로 만드는 훌륭한 방법입니다. 오늘은 Aspose.PDF for .NET을 사용하여 PDF 문서에서 이미지 주위에 텍스트를 배치하는 방법을 살펴보겠습니다.

## 필수 조건

코드 작성에 앞서 모든 준비가 완료되었는지 확인해 보겠습니다. 필요한 것은 다음과 같습니다.

- .NET용 Aspose.PDF: 여기에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/).
- Visual Studio: 원활하게 따라가려면 최신 버전이 설치되어 있는지 확인하세요.
- .NET Framework: 이 예제에서는 .NET을 사용하므로 .NET 개발에 적합한 환경이 설정되어 있는지 확인하세요.
- 임시 면허: 임시 면허를 요청할 수 있습니다. [여기](https://purchase.aspose.com/temporary-license/) 제품을 평가하는 경우.

아직 .NET용 Aspose.PDF를 설정하지 않은 경우 다음 설치 지침을 따르세요. [선적 서류 비치](https://reference.aspose.com/pdf/net/).

## 네임스페이스 가져오기

코딩을 시작하기 전에 필요한 네임스페이스를 가져와야 합니다. 다음은 이를 위한 코드 조각입니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

이러한 네임스페이스는 다음과 같은 클래스에 대한 액세스를 제공하므로 필수적입니다. `Document`, `Page`, `Image`, 그리고 `HtmlFragment`PDF를 만들고 조작하는 데 사용됩니다.

이제 기본적인 내용은 끝났으니, Aspose.PDF for .NET을 사용하여 PDF 파일의 이미지 주위에 텍스트를 배치하는 방법을 알아보겠습니다. 단계별로 안내해 드리겠습니다.

## 1단계: 문서 개체 인스턴스화

먼저 PDF 문서를 만들어야 합니다. Aspose.PDF에서는 다음을 인스턴스화하여 이 작업을 수행합니다. `Document` 객체입니다. 이 객체는 앞으로 추가할 모든 콘텐츠의 기반이 됩니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

여기서는 빈 PDF 문서를 만들었습니다. 아직 페이지가 없지만, 걱정하지 마세요. 다음 단계에서 페이지를 추가할 것입니다.

## 2단계: 문서에 페이지 추가

이제 문서가 완성되었으니 페이지를 추가할 차례입니다. 빈 종이를 만들어서 내용을 추가한다고 생각해 보세요.

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

이 코드는 문서에 새 페이지를 추가합니다. 기본적으로 페이지는 비어 있지만, 이제 이 부분을 변경해 보겠습니다.

## 3단계: 콘텐츠를 구성하기 위한 표 만들기

이미지와 텍스트를 제대로 정렬하기 위해 표를 사용하겠습니다. PDF의 표는 Word 문서나 HTML처럼 레이아웃을 구성하는 데 도움이 될 수 있습니다.

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
page.Paragraphs.Add(table1);
```

이 스니펫은 표를 만들어 페이지에 추가합니다. 표를 이미지와 텍스트를 정렬하는 프레임워크로 생각하면 됩니다.

## 4단계: 표의 열 너비 설정

이제 표를 추가했으니 열 너비를 정의해야 합니다. 이렇게 하면 이미지와 텍스트 크기가 페이지에 적절하게 표시됩니다.

```csharp
table1.ColumnWidths = "120 270";
```

이 줄은 두 열의 너비를 설정합니다. 하나는 이미지용이고 다른 하나는 텍스트용입니다. 이미지나 텍스트에 더 많은 공간이 필요하거나 더 적은 공간이 필요하면 이 값을 조정하세요.

## 5단계: 여백 및 패딩 정의

모든 것이 깔끔하게 보이도록 표에 여백과 패딩을 추가해 보겠습니다.

```csharp
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;
table1.DefaultCellPadding = margin;
```

이러한 설정을 사용하면 표의 간격이 일관되므로 콘텐츠가 시각적으로 매력적으로 보입니다.

## 6단계: 표에 이미지 삽입

이제 재미있는 부분, 이미지 추가를 시작해 보겠습니다. 여기서는 Aspose 로고를 추가하지만, 원하는 이미지를 자유롭게 사용하세요.

```csharp
Aspose.Pdf.Row row1 = table1.Rows.Add();
Aspose.Pdf.Image logo = new Aspose.Pdf.Image();
logo.File = dataDir + "aspose-logo.jpg";
logo.FixHeight = 120;
logo.FixWidth = 110;
row1.Cells.Add();
row1.Cells[0].Paragraphs.Add(logo);
```

무슨 일이 일어나고 있는지 알려드리겠습니다.
- 귀하가 지정한 디렉토리에서 이미지를 로드합니다.
- 이미지의 높이와 너비를 설정합니다.
- 마지막으로, 표의 첫 번째 셀에 이미지를 추가합니다.

## 7단계: 이미지 옆에 텍스트 추가

이제 이미지가 제자리에 배치되었으니 옆에 텍스트를 추가해 보겠습니다. 이 예시에서는 HTML 형식의 텍스트를 사용하여 콘텐츠의 스타일을 지정하겠습니다.

```csharp
string TitleString = "<font face=\"Arial\" size=6 color=\"#101090\"><b> Aspose.Pdf for .NET</b></font>";
string BodyString1 = "<font face=\"Arial\" size=2><br/>Aspose.Pdf for .NET is a non-graphical PDF document reporting component that enables .NET applications to <b>create PDF documents from scratch</b> without utilizing Adobe Acrobat.</font>";

Aspose.Pdf.HtmlFragment TitleText = new Aspose.Pdf.HtmlFragment(TitleString + BodyString1);
row1.Cells.Add();
row1.Cells[1].Paragraphs.Add(TitleText);
```

이 블록은 이미지 옆 셀에 스타일이 적용된 제목과 설명을 추가합니다. HTML 태그를 사용하여 텍스트 서식을 지정하여 더욱 세부적으로 사용자 지정할 수 있습니다.

## 8단계: 수직 정렬 조정

기본적으로 표 셀의 내용이 원하는 대로 정렬되지 않을 수 있습니다. 이 경우, 텍스트가 셀 상단에 정렬되도록 해야 합니다.

```csharp
row1.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
```

이렇게 하면 텍스트가 셀의 맨 위에 표시되어 레이아웃이 깔끔하고 전문적으로 유지됩니다.

## 9단계: 이미지와 설명 아래에 더 많은 텍스트 추가

이미지와 텍스트 아래에 더 많은 콘텐츠를 포함하고 싶을 수도 있습니다. 이를 위해 표에 행을 하나 더 추가해 보겠습니다.

```csharp
Aspose.Pdf.Row SecondRow = table1.Rows.Add();
SecondRow.Cells.Add();
SecondRow.Cells[0].ColSpan = 2;
SecondRow.Cells[0].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;

string SecondRowString = "<font face=\"Arial\" size=2>Aspose.Pdf for .NET supports the creation of PDF files through API and XML or XSL-FO templates.</font>";
Aspose.Pdf.HtmlFragment SecondRowText = new Aspose.Pdf.HtmlFragment(SecondRowString);
SecondRow.Cells[0].Paragraphs.Add(SecondRowText);
```

여기서는 레이아웃의 균형을 유지하기 위해 두 열에 걸쳐 추가 텍스트가 있는 행을 추가했습니다.

## 10단계: PDF 문서 저장

마지막으로, 변경 사항을 볼 수 있도록 문서를 저장해야 합니다.

```csharp
doc.Save(dataDir + "PlacingTextAroundImage_out.pdf");
```

이렇게 하면 우리가 원하는 대로 이미지와 텍스트가 포맷된 PDF가 저장됩니다.

## 결론

PDF에서 이미지 주위에 텍스트를 배치하는 것은 어려운 작업처럼 보일 수 있지만, Aspose.PDF for .NET은 이 과정을 간소화합니다. 표, 이미지, 스타일이 적용된 텍스트를 활용하여 최소한의 노력으로 전문가 수준의 PDF를 만들 수 있습니다. 몇 줄의 코드만으로 콘텐츠를 원하는 위치에 정확하게 배치하여 문서를 세련되고 체계적으로 정리할 수 있습니다.

## 자주 묻는 질문

### 이 방법을 사용하면 텍스트와 함께 여러 이미지를 배치할 수 있나요?
네, 표에 행과 셀을 더 추가하여 추가 이미지와 텍스트를 포함하면 됩니다.

### 이미지의 정렬을 변경할 수 있나요?
물론입니다! 셀의 정렬 속성을 조정하여 이미지 정렬을 수정할 수 있습니다.

### 텍스트의 스타일을 추가로 지정하려면 어떻게 해야 하나요?
HTML 태그를 사용할 수 있습니다. `HtmlFragment` 굵게, 기울임체 또는 다른 글꼴 등 다양한 스타일을 적용하는 데 반대합니다.

### 텍스트와 이미지 사이의 간격을 조절할 수 있나요?
네, 사용 중 `MarginInfo` 객체를 사용하면 요소 사이의 패딩과 여백을 제어할 수 있습니다.

### 텍스트에 링크를 추가할 수 있나요?
물론입니다! 다음을 사용하여 HTML 형식의 텍스트에 하이퍼링크를 삽입할 수 있습니다. `<a>` 꼬리표.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}