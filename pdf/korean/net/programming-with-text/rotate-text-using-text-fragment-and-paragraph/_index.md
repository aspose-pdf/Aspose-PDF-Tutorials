---
"description": "Aspose.PDF for .NET을 사용하여 PDF 문서의 텍스트 조각과 문단을 사용하여 텍스트를 회전하는 방법을 알아보세요."
"linktitle": "텍스트 조각과 단락을 사용하여 텍스트 회전"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "텍스트 조각과 단락을 사용하여 텍스트 회전"
"url": "/ko/net/programming-with-text/rotate-text-using-text-fragment-and-paragraph/"
"weight": 400
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 텍스트 조각과 단락을 사용하여 텍스트 회전

## 소개

동적 문서 생성에 있어서 PDF는 최고의 표준입니다. PDF는 보편적인 매력과 기대되는 전문성 덕분에 법률, 교육, 기업 환경 등 다양한 분야에서 널리 사용됩니다. 이 글에서는 Aspose.PDF for .NET을 활용하여 회전된 텍스트 조각이 포함된 PDF 문서를 만드는 방법을 자세히 살펴보겠습니다. 문서에 개성을 더하거나 중요한 정보를 강조하는 데 적합합니다. 시작해 볼까요!

## 필수 조건

기술적인 세부 사항을 살펴보기 전에 몇 가지 사항을 준비했는지 확인하세요.

1. .NET Framework에 대한 기본적인 이해: Aspose.PDF는 .NET 애플리케이션과 원활하게 작동하므로 C# 또는 VB.NET에 익숙하면 도움이 됩니다.
  
2. Aspose.PDF for .NET 라이브러리: Aspose.PDF 라이브러리가 필요합니다. 걱정하지 마세요. 쉽게 다운로드할 수 있습니다! 바로 여기에서 다운로드할 수 있습니다. [.NET용 Aspose.PDF 다운로드](https://releases.aspose.com/pdf/net/).

3. 개발 환경: Visual Studio처럼 .NET 개발을 지원하는 모든 IDE를 사용할 수 있습니다. IDE에서 다운로드한 Aspose.PDF 라이브러리에 액세스할 수 있는지 확인하세요.

4. 임시 라이센스(선택 사항): 무료 평가판으로 시작할 수 있지만 프로덕션 애플리케이션을 빌드해야 하는 경우 임시 라이센스를 취득하는 것을 고려하십시오. [임시 면허](https://purchase.aspose.com/temporary-license/) 완벽한 기능을 위해.

5. 인터넷 연결: 뻔한 얘기처럼 들릴 수 있지만, 추가 지침과 문제 해결을 위해 온라인 문서에 접근하려면 인터넷 연결이 필요합니다.

전제 조건을 정리했다면 이제 실행에 들어갈 차례입니다!

## 패키지 가져오기

코딩 부분을 시작하기 전에 .NET 프로젝트에 필요한 패키지를 가져와야 합니다. 

시작하려면 C# 파일 맨 위에 다음 네임스페이스를 사용하고 있는지 확인하세요.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
```

이를 통해 Aspose.PDF 라이브러리가 제공하는 PDF 문서 조작 기능과 텍스트 기능에 액세스할 수 있습니다.

이제 재밌는 작업이 시작됩니다! 표준 텍스트 조각과 회전된 텍스트 조각을 모두 포함하는 PDF 문서를 생성하는 간단한 애플리케이션을 만들어 보겠습니다. 심호흡을 하고 단계별로 살펴보겠습니다.

## 1단계: 문서 개체 초기화

이 단계에서는 새로운 PDF 문서를 만듭니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 문서 객체 초기화
Document pdfDocument = new Document();
```

이 코드 줄은 콘텐츠를 만들 수 있는 새로운 캔버스를 만들어 줍니다. 마치 캔버스에 새 페인트를 붓는 것과 같다고 생각해 보세요. 정말 신나는 경험이죠!

## 2단계: 페이지 추가

다음으로, 문서에 페이지를 추가해야 합니다. 바로 여기서 마법이 일어날 겁니다.

```csharp
// 특정 페이지 가져오기
Page pdfPage = (Page)pdfDocument.Pages.Add();
```

이 단계를 걸작의 기초를 다지는 과정이라고 생각해 보세요. 페이지가 없으면 아무것도 그리거나 쓸 수 없습니다!

## 3단계: 첫 번째 텍스트 조각 만들기

이제 PDF에 텍스트를 추가해 보겠습니다. 먼저 표준 텍스트 조각부터 시작해 보겠습니다.

```csharp
// 텍스트 조각 만들기
TextFragment textFragment1 = new TextFragment("main text");
// 텍스트 속성 설정
textFragment1.TextState.FontSize = 12;
textFragment1.TextState.Font = FontRepository.FindFont("TimesNewRoman");
```

여기서 우리는 첫 번째 텍스트 조각을 만들었습니다. `textFragment1`또한 글꼴 속성도 설정했습니다. 보기 좋게 만들기 위해서요!

## 4단계: 페이지에 첫 번째 텍스트 조각 추가

텍스트 조각이 준비되었으니, 이제 페이지에 올려볼 차례입니다.

```csharp
pdfPage.Paragraphs.Add(textFragment1);
```

이 코드는 기본적으로 표준 텍스트를 캔버스에 배치합니다. 마치 캔버스에 붓을 대고 작품의 첫 줄을 그리는 것과 같습니다!

## 5단계: 회전된 텍스트 조각 만들기

다음으로, 시선을 사로잡기 위해 회전된 텍스트를 추가해 보겠습니다. 시작해 볼까요?

### 첫 번째 회전된 텍스트 조각 만들기

```csharp
// 텍스트 조각 만들기
TextFragment textFragment2 = new TextFragment("rotated text");
// 텍스트 속성 설정
textFragment2.TextState.FontSize = 12;
textFragment2.TextState.Font = FontRepository.FindFont("TimesNewRoman");
// 회전 설정
textFragment2.TextState.Rotation = 315;
```

이 스니펫에서 우리는 다음과 같은 텍스트 조각을 만들었습니다. `textFragment2`회전 각도를 315도로 설정했는데, 기울기는 잘 맞지만 완전히 뒤집힌 것은 아닙니다. 이는 약간의 개성이 필요한 텍스트를 나타낼 수 있습니다!

### 회전된 텍스트 조각을 페이지에 추가

이제 눈길을 끄는 텍스트를 페이지에 추가할 차례입니다!

```csharp
pdfPage.Paragraphs.Add(textFragment2);
```

멋지죠? 마치 캔버스에 색을 더해 더욱 돋보이게 하는 것 같아요!

### 다른 회전된 텍스트 조각 만들기

좋은 측정을 위해 회전된 텍스트 조각을 하나 더 추가해 보겠습니다.

```csharp
// 텍스트 조각 만들기
TextFragment textFragment3 = new TextFragment("another rotated text");
// 텍스트 속성 설정
textFragment3.TextState.FontSize = 12;
textFragment3.TextState.Font = FontRepository.FindFont("TimesNewRoman");
// 회전 설정
textFragment3.TextState.Rotation = 270;
```

이전과 마찬가지로, 회전된 텍스트를 또 하나 추가하겠습니다. 이번에는 270도 회전해서 거의 뒤집힌 것처럼 보입니다!

## 6단계: 페이지에 두 번째 회전된 텍스트 조각 추가

이제 마지막 마무리를 하겠습니다.

```csharp
pdfPage.Paragraphs.Add(textFragment3);
```

이렇게 하면 캔버스에 여러 개의 회전된 텍스트 조각이 함께 작동합니다!

## 7단계: 문서 저장

이제 환상적인 요소가 가득한 문서가 생겼으니, 저장해서 마무리하겠습니다.

```csharp
// 문서 저장
pdfDocument.Save(dataDir + "TextFragmentTests_Rotated3_out.pdf");
```

자, 이제 여러분의 창의적인 걸작이 PDF 형식으로 저장되었습니다. 마치 갤러리에 전시하는 것처럼, 온 세상이 볼 수 있도록 준비된 것이죠!

## 결론

축하합니다! Aspose.PDF for .NET을 사용하여 표준 텍스트 조각과 회전된 텍스트 조각이 모두 포함된 동적 PDF 문서를 만들었습니다. 이제 정보를 표현하는 방법에 무한한 가능성이 열립니다. 보고서의 핵심 사항을 강조하거나 문서에 시각적인 효과를 더하고 싶을 때 이러한 기법을 사용하면 목표를 달성하는 데 도움이 될 것입니다.

## 자주 묻는 질문

### .NET용 Aspose.PDF란 무엇인가요?

.NET용 Aspose.PDF는 개발자가 .NET 애플리케이션을 사용하여 PDF 파일을 만들고, 조작하고, 변환할 수 있는 강력한 라이브러리입니다.

### 웹 애플리케이션에서 Aspose.PDF를 사용할 수 있나요?

물론입니다! Aspose.PDF는 웹 애플리케이션, 데스크톱 애플리케이션, 서비스 등 모든 .NET 애플리케이션에 통합될 수 있습니다.

### Aspose.PDF에 대한 무료 평가판이 있나요?

네, 구매 전 무료 체험판을 통해 기능을 직접 체험해 보실 수 있습니다. 여기에서 확인해 보세요. [Aspose 무료 체험판](https://releases.aspose.com/).

### Aspose.PDF를 사용하여 PDF의 텍스트를 회전하려면 어떻게 해야 하나요?

텍스트를 설정하여 회전할 수 있습니다. `Rotation` 의 속성 `TextFragment` 이 튜토리얼에서 보여준 것처럼 객체입니다.

### Aspose.PDF에 대한 지원은 어디에서 찾을 수 있나요?

지원이나 문의사항이 있으시면 다음 사이트를 방문하세요. [Aspose 지원 포럼](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}