---
"description": "Aspose.PDF for .NET을 사용하여 PDF 파일의 텍스트를 회전하는 방법을 단계별 가이드와 함께 알아보세요. 위치 지정부터 회전까지 다양한 텍스트 조작 기법을 알아보세요."
"linktitle": "PDF 파일에서 텍스트 조각을 사용하여 텍스트 회전"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에서 텍스트 조각을 사용하여 텍스트 회전"
"url": "/ko/net/programming-with-text/rotate-text-using-text-fragment/"
"weight": 390
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에서 텍스트 조각을 사용하여 텍스트 회전

## 소개

PDF를 만드는 것도 중요하지만, 특정 요구 사항에 맞게 PDF를 조작하는 것은 정말 중요합니다. 바로 이 부분에서 마법 같은 일이 일어납니다! PDF에서 텍스트를 회전하는 방법을 궁금해하신 적 있으신가요? 보고서를 작성하든, 맞춤 디자인 문서를 만들든, 텍스트 조각을 회전하면 PDF를 더욱 시각적으로 멋지게 만들 수 있습니다. 이 튜토리얼에서는 PDF 문서를 원활하게 조작할 수 있는 강력한 라이브러리인 Aspose.PDF for .NET을 사용하여 텍스트를 회전하는 방법을 살펴보겠습니다.

## 필수 조건

코드로 들어가기 전에 필요한 도구와 설정을 간략하게 살펴보겠습니다. 모든 것이 준비되어 있어야 쉽게 따라올 수 있습니다.

### .NET 라이브러리용 Aspose.PDF
먼저, 프로젝트에 Aspose.PDF for .NET을 설치해야 합니다. 이 라이브러리에는 PDF 파일을 프로그래밍 방식으로 생성, 수정 및 관리하는 데 도움이 되는 기능이 포함되어 있습니다. 아직 다운로드하지 않으셨다면 다음 위치에서 다운로드할 수 있습니다.
- [.NET용 Aspose.PDF 다운로드](https://releases.aspose.com/pdf/net/)

이 튜토리얼에서는 최신 버전의 라이브러리를 사용하고 있는지 확인하세요.

### 개발 환경
Visual Studio와 같은 .NET 개발 환경도 필요합니다. Visual Studio는 C# 개발을 위한 필수 IDE로, 코딩 경험을 원활하고 효율적으로 만들어 줄 것입니다.

### 임시 또는 정식 면허
Aspose.PDF 무료 체험판으로 시작할 수 있지만, 제약을 피하고 싶다면 임시 라이선스나 정식 라이선스를 사용하는 것이 좋습니다. 라이선스를 받는 방법은 다음과 같습니다.
- [무료 체험](https://releases.aspose.com/)
- [임시 면허](https://purchase.aspose.com/temporary-license/)
- [정식 라이센스 구매](https://purchase.aspose.com/buy)

이러한 필수 사항을 모두 준비했다면 다음으로 넘어가겠습니다!

## 패키지 가져오기

코딩을 시작하기 전에 Aspose.PDF에 포함된 필수 네임스페이스를 가져와야 합니다. 이는 문서, 페이지, 텍스트 조각 등을 작업하는 데 매우 중요합니다. C# 파일 시작 부분에 다음 코드를 추가하세요.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
```

이제 예제 코드를 단계별로 나누어 전문가처럼 텍스트를 회전하는 방법을 알아보겠습니다!

## 1단계: 문서 개체 초기화

모든 PDF 조작은 PDF 문서를 만들거나 불러오는 것부터 시작됩니다. 여기에서는 Aspose.PDF를 사용하여 새 PDF 문서를 처음부터 초기화해 보겠습니다.

우리는 새로운 것을 만들고 있습니다 `Document` PDF 파일을 나타내는 개체입니다. 처음에는 이 문서가 비어 있습니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
// 문서 객체 초기화
Document pdfDocument = new Document();
```

설명:  
- `dataDir`: 최종 PDF가 저장되는 디렉토리입니다.
- `Document pdfDocument = new Document();`: 새롭고 비어 있는 PDF 문서를 초기화합니다. 

## 2단계: 문서에 페이지 추가

다음으로, 문서에 페이지를 추가해야 합니다. PDF는 기본적으로 여러 페이지의 모음이므로, 콘텐츠를 추가하려면 최소 한 페이지가 필요합니다.

```csharp
// 특정 페이지 가져오기
Page pdfPage = (Page)pdfDocument.Pages.Add();
```

페이지를 추가하지 않으면 그림을 그리거나 텍스트를 배치할 캔버스가 없습니다!

## 3단계: 첫 번째 텍스트 조각 만들기

이제 흥미로운 부분입니다! PDF에 텍스트 조각을 추가해 보겠습니다. 텍스트 조각은 글꼴, 크기, 위치와 같은 특정 속성을 가진 텍스트 조각입니다.

```csharp
// 텍스트 조각 만들기
TextFragment textFragment1 = new TextFragment("main text");
textFragment1.Position = new Position(100, 600);
textFragment1.TextState.FontSize = 12;
textFragment1.TextState.Font = FontRepository.FindFont("TimesNewRoman");
```

- TextFragment("main text"): 이것은 "main text"라는 내용으로 새로운 텍스트 조각을 생성합니다.
- Position(100, 600): 페이지에서 텍스트의 위치를 정의합니다. 첫 번째 숫자는 x 좌표이고, 두 번째 숫자는 y 좌표입니다.
- TextState.FontSize: 텍스트의 글꼴 크기를 설정합니다.
- FontRepository.FindFont: 텍스트에 적용할 지정된 글꼴을 찾습니다.

## 4단계: 회전된 텍스트 조각 만들기

더 많은 텍스트 조각을 추가해 보겠습니다. 이번에는 다른 각도로 회전시켜 보겠습니다!

### 텍스트 조각을 45도 회전

```csharp
// 회전된 텍스트 조각 만들기
TextFragment textFragment2 = new TextFragment("rotated text");
textFragment2.Position = new Position(200, 600);
textFragment2.TextState.FontSize = 12;
textFragment2.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment2.TextState.Rotation = 45;
```

여기서 중요한 변화는 다음과 같습니다.
- TextState.Rotation: 이 속성은 텍스트 조각의 회전 각도를 설정하며, 이 경우 45도입니다.

### 텍스트 조각을 90도 회전

```csharp
// 회전된 텍스트 조각 만들기
TextFragment textFragment3 = new TextFragment("rotated text");
textFragment3.Position = new Position(300, 600);
textFragment3.TextState.FontSize = 12;
textFragment3.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment3.TextState.Rotation = 90;
```

이 경우 회전 각도는 90도입니다.

## 5단계: PDF 페이지에 텍스트 조각 추가

이제 모든 텍스트 조각을 준비했으므로 TextBuilder 클래스를 사용하여 PDF 페이지에 추가할 차례입니다.

```csharp
// TextBuilder 객체 생성
TextBuilder textBuilder = new TextBuilder(pdfPage);
// PDF 페이지에 텍스트 조각 추가
textBuilder.AppendText(textFragment1);
textBuilder.AppendText(textFragment2);
textBuilder.AppendText(textFragment3);
```

TextBuilder 클래스는 단일 페이지에 여러 텍스트 조각을 추가하는 데 도움이 되며, 이를 개별적으로 조작할 수 있는 유연성을 제공합니다.

## 6단계: PDF 문서 저장

마지막으로, 지정된 디렉터리에 문서를 저장하세요. 이 단계를 거치지 않으면 모든 노력이 허공으로 사라지게 됩니다!

```csharp
// 문서 저장
pdfDocument.Save(dataDir + "TextFragmentTests_Rotated1_out.pdf");
```

Aspose.PDF for .NET을 사용하여 PDF 파일의 텍스트를 성공적으로 회전했습니다. 이제 PDF 파일을 열어 회전된 텍스트 조각을 확인할 수 있습니다!

## 결론

PDF에서 텍스트를 회전하면 문서에 전문적인 느낌을 더하여 시각적으로 매력적이고 독창적으로 만들 수 있습니다. Aspose.PDF for .NET을 사용하면 텍스트 조각을 매우 쉽게 조작하여 콘텐츠 표시 방식을 완벽하게 제어할 수 있습니다. 이제 텍스트 회전 방법을 배웠으니, 프로젝트의 필요에 맞게 다양한 각도와 레이아웃을 실험해 보세요.

## 자주 묻는 질문

### 텍스트 조각을 원하는 각도로 회전할 수 있나요?
네! 설정할 수 있습니다 `TextState.Rotation` 텍스트를 필요에 따라 회전하려면 속성을 원하는 각도(음수 각도 포함)로 조정합니다.

### 각 텍스트 조각에 다른 글꼴을 사용할 수 있나요?
물론입니다. 각 텍스트 조각의 글꼴을 사용자 지정할 수 있습니다. `FontRepository.FindFont` 그리고 적용하고 싶은 글꼴을 전달하세요.

### Aspose.PDF는 여러 페이지로 구성된 PDF를 지원합니까?
네, PDF 문서에 여러 페이지를 추가하고 각 페이지를 개별적으로 조작할 수 있습니다.

### 추가할 수 있는 텍스트 조각의 수에 제한이 있나요?
아니요, 필요한 만큼 텍스트 조각을 추가할 수 있습니다. 페이지에 제대로 배치되었는지만 확인하세요.

### 텍스트 조각을 추가한 후에 수정할 수 있나요?
네, 텍스트 조각을 추가한 후에도 해당 속성을 업데이트하거나 페이지에서 제거할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}