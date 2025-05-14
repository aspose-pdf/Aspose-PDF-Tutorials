---
"description": "이 자세하고 단계별 튜토리얼을 통해 Aspose.PDF for .NET을 사용하여 PDF 파일에서 콜아웃 속성을 설정하는 방법을 알아보세요."
"linktitle": "PDF 파일에서 콜아웃 속성 설정"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에서 콜아웃 속성 설정"
"url": "/ko/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에서 콜아웃 속성 설정

## 소개

전문적이고 시각적으로 매력적인 PDF 문서를 만들려면 특정 콘텐츠에 주의를 끌 수 있는 주석을 추가해야 하는 경우가 많습니다. 이러한 주석 중 하나는 만화에 나오는 말풍선과 같은 콜아웃입니다. 콜아웃은 PDF 파일의 텍스트를 명확하게 하거나 강조하는 데 도움이 됩니다. Aspose.PDF for .NET을 사용하면 이러한 주석을 문서에 매우 쉽게 추가할 수 있습니다. 이 튜토리얼에서는 이 강력한 라이브러리를 사용하여 PDF 파일에 콜아웃 속성을 설정하는 방법을 살펴보겠습니다. 숙련된 개발자든 초보자든 이 가이드를 마치면 PDF 파일에서 콜아웃을 사용하는 방법을 명확하게 이해하게 될 것입니다.

## 필수 조건

코드를 살펴보기 전에, 시작하는 데 필요한 필수 사항을 살펴보겠습니다.

1. Aspose.PDF for .NET: Aspose.PDF for .NET 라이브러리가 설치되어 있는지 확인하세요. 다음에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/).
2. IDE: Visual Studio와 같은 개발 환경.
3. .NET Framework: 컴퓨터에 .NET이 설치되어 있는지 확인하세요.
4. 임시 라이센스: 제한 없이 Aspose.PDF의 모든 기능을 사용해보고 싶으시다면 [임시 면허](https://purchase.aspose.com/temporary-license/).

## 패키지 가져오기

코드 작성을 시작하기 전에 PDF 파일과 주석 작업을 할 수 있는 필수 패키지를 가져와야 합니다.

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

이러한 가져오기는 PDF 문서를 조작하고 콜아웃과 같은 주석을 만드는 데 필요한 모든 클래스와 메서드를 제공합니다.

## 1단계: PDF 문서 초기화

이 여정의 첫 번째 단계는 콜아웃 주석을 추가할 새 PDF 문서를 만드는 것입니다. 빈 캔버스를 만들어 요소를 추가하는 것처럼 생각하면 됩니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 새 PDF 문서 초기화
Document doc = new Document();
```
여기서 우리는 새로운 것을 만들고 있습니다 `Document` PDF 파일로 사용될 객체입니다. `dataDir` 변수는 작업이 끝난 후 PDF 파일을 저장할 디렉토리로 설정됩니다.

## 2단계: 문서에 새 페이지 추가

PDF 문서는 여러 페이지로 구성될 수 있으며, 이 단계에서는 문서에 새 페이지를 추가합니다. 이 페이지에 설명선 주석이 배치됩니다.

```csharp
// 문서에 새 페이지 추가
Page page = doc.Pages.Add();
```
그만큼 `Pages.Add()` 이 방법은 새 페이지를 추가하는 데 사용됩니다. `doc` 객체입니다. 새 페이지는 다음 위치에 저장됩니다. `page` 나중에 주석을 추가할 때 사용할 변수입니다.

## 3단계: 기본 모양 정의

설명선과 마찬가지로 주석도 시각적으로 원하는 대로 꾸밀 수 있습니다. 이 단계에서는 설명선 내 텍스트의 모양을 정의해 보겠습니다.

```csharp
// 주석의 기본 모양을 정의합니다.
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
우리는 만듭니다 `DefaultAppearance` 텍스트 색상과 글꼴 크기를 정의하는 객체입니다. 여기서는 텍스트가 빨간색이고 글꼴 크기가 10으로 설정됩니다. 이 모양은 콜아웃 주석에 적용됩니다.

## 4단계: 자유 텍스트 주석 만들기

이제 실제 주석을 만들 차례입니다. 자유 텍스트 주석을 사용하면 특정 텍스트와 스타일을 적용한 콜아웃을 추가할 수 있습니다.

```csharp
// 콜아웃이 있는 FreeTextAnnotation 만들기
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
우리는 만듭니다 `FreeTextAnnotation` 특정 좌표를 가진 객체로, 페이지에서의 위치를 정의합니다. `Intent` 로 설정됩니다 `FreeTextCallout`, 이것이 콜아웃 주석임을 나타냅니다. `EndingStyle` 로 설정됩니다 `OpenArrow`즉, 콜아웃 라인은 열린 화살표로 끝납니다.

## 5단계: 콜아웃 라인 포인트 정의

콜아웃 주석에는 관심 영역을 가리키는 선이 있습니다. 여기서는 이 선을 구성하는 점들을 정의하겠습니다.

```csharp
// 콜아웃 라인의 포인트를 정의합니다
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
그만큼 `Callout` 속성은 배열입니다 `Point` 각 객체는 페이지의 좌표를 나타냅니다. 이러한 점은 콜아웃 선의 경로를 정의하여 고전적인 말풍선 모양을 만듭니다.

## 6단계: 페이지에 주석 추가

주석을 만들고 구성한 후 다음 단계는 이를 페이지에 추가하는 것입니다.

```csharp
// 페이지에 주석을 추가합니다
page.Annotations.Add(fta);
```
그만큼 `Annotations.Add()` 이 방법은 앞서 만든 페이지에 주석을 배치하는 데 사용됩니다. 이 단계는 PDF 페이지에 콜아웃을 효과적으로 "그립니다".

## 7단계: 서식 있는 텍스트 콘텐츠 설정

콜아웃 주석에는 서식 있는 텍스트를 포함할 수 있으므로, 풍선 안에 서식 있는 콘텐츠를 넣을 수 있습니다. 샘플 텍스트를 추가해 보겠습니다.

```csharp
// 주석에 대한 서식 있는 텍스트를 설정합니다.
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">이것은 샘플입니다</span></p></body>";
```
그만큼 `RichText` 속성은 HTML 콘텐츠로 설정됩니다. 이를 통해 콜아웃 내에서 글꼴 크기, 색상, 스타일 지정 등 세부적인 서식을 지정할 수 있습니다.

## 8단계: PDF 문서 저장

마지막으로 모든 설정을 완료한 후 문서를 저장해야 합니다. 이 단계를 통해 콜아웃 주석이 포함된 PDF 생성이 완료됩니다.

```csharp
// 문서를 저장하세요
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
그만큼 `Save()` 이 메서드는 지정된 디렉터리에 "SetCalloutProperty.pdf"라는 파일 이름으로 문서를 저장합니다. 이것으로 PDF 생성 과정이 완료됩니다.

## 결론

자, 이제 완성되었습니다! Aspose.PDF for .NET을 사용하여 콜아웃 주석이 있는 PDF 문서를 만들었습니다. 이 주석은 문서의 특정 부분을 강조하거나 설명하는 데 매우 유용합니다. Aspose.PDF는 PDF 조작을 간편하고 유연하게 만들어 주는 강력한 API를 제공합니다. 주석 추가, 문서 변환, 복잡한 PDF 작업 등 어떤 작업이든 Aspose.PDF가 해결해 드립니다.

## 자주 묻는 질문

### 콜아웃의 모양을 추가로 사용자 지정할 수 있나요?

물론입니다! 선 색상, 두께, 텍스트 글꼴 및 스타일 등 다양한 부분을 사용자 지정할 수 있습니다.

### 한 페이지에 여러 개의 콜아웃을 추가할 수 있나요?

네, 각 주석에 대해 단계를 반복하여 필요한 만큼 많은 콜아웃을 추가할 수 있습니다.

### 콜아웃의 위치를 어떻게 바꾸나요?

좌표를 수정하기만 하면 됩니다. `Rectangle` 그리고 `Callout` 주석의 위치를 변경하는 속성입니다.

### Aspose.PDF를 사용하여 다른 유형의 주석을 추가할 수 있나요?

네, Aspose.PDF는 강조 표시, 스탬프, 파일 첨부 등 다양한 주석 유형을 지원합니다.

### 서식 있는 텍스트 콘텐츠는 HTML로 제한됩니까?

그만큼 `RichText` 이 속성은 HTML 하위 집합을 지원하므로 스타일이 지정된 텍스트와 기본 서식을 포함할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}