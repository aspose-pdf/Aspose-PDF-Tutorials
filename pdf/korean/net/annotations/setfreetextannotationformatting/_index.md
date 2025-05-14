---
"description": "이 단계별 가이드를 통해 Aspose.PDF for .NET을 사용하여 PDF 문서에 자유 텍스트 주석 서식을 설정하는 방법을 알아보세요."
"linktitle": "자유 텍스트 주석 서식 설정"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "자유 텍스트 주석 서식 설정"
"url": "/ko/net/annotations/setfreetextannotationformatting/"
"weight": 140
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 자유 텍스트 주석 서식 설정

## 소개

디지털 시대에 PDF 문서를 조작하고 주석을 추가하는 기능은 다양한 분야의 전문가에게 필수적인 기능이 되었습니다. 과제에 마크업을 하는 교사, 계약서를 검토하는 변호사, 피드백을 공유하는 프로젝트 관리자 등 어떤 직업이든 적절한 도구를 갖추면 큰 차이를 만들 수 있습니다. 이러한 강력한 도구 중 하나는 개발자가 PDF 파일을 쉽게 생성, 편집 및 조작할 수 있도록 지원하는 강력한 라이브러리인 Aspose.PDF for .NET입니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 자유 텍스트 주석 서식을 설정하는 방법을 자세히 살펴보겠습니다. 이 가이드를 마치면 사용자 지정 주석을 사용하여 PDF 문서를 개선하고 워크플로를 더욱 원활하고 효율적으로 만드는 방법을 익힐 수 있을 것입니다.

## 필수 조건

코딩의 핵심을 파고들기 전에, 시작하는 데 필요한 모든 것이 있는지 확인해 보겠습니다. 필요한 준비물은 다음과 같습니다.

1. C#에 대한 기본 지식: C# 프로그래밍에 대한 지식이 있으면 이 튜토리얼에서 제공하는 예제와 코드 조각을 이해하는 데 도움이 됩니다.
2. .NET용 Aspose.PDF: Aspose.PDF 라이브러리가 설치되어 있어야 합니다. 다음에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/).
3. Visual Studio: Visual Studio와 같은 개발 환경을 사용하면 코드를 작성하고 테스트하기가 더 쉬워집니다.
4. PDF 문서: 이 튜토리얼에서는 작업할 샘플 PDF 문서가 필요합니다. 간단한 PDF 문서를 만들거나 인터넷에서 샘플을 다운로드할 수 있습니다.

이러한 전제 조건을 갖추면 PDF 주석의 세계로 뛰어들 준비가 된 것입니다!

## 패키지 가져오기

Aspose.PDF for .NET을 시작하려면 필요한 패키지를 프로젝트에 가져와야 합니다. 방법은 다음과 같습니다.

### 1단계: 새 프로젝트 만들기

Visual Studio를 열고 새 C# 프로젝트를 만듭니다. 간편하게 콘솔 응용 프로그램을 선택할 수 있습니다.

### 2단계: Aspose.PDF 참조 추가

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭합니다.
2. "NuGet 패키지 관리"를 선택하세요.
3. "Aspose.PDF"를 검색하여 최신 버전을 설치하세요.

### 3단계: 네임스페이스 가져오기

C# 파일 맨 위에 Aspose.PDF 네임스페이스를 가져옵니다.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

이제 모든 것을 설정했으니 튜토리얼의 주요 부분인 자유 텍스트 주석 서식 설정으로 넘어가겠습니다.

## 1단계: 문서 디렉토리 정의

먼저, 문서 디렉터리 경로를 지정해야 합니다. 이 경로에 PDF 파일이 저장됩니다. 방법은 다음과 같습니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

바꾸다 `"YOUR DOCUMENT DIRECTORY"` PDF 파일이 저장된 실제 경로를 입력합니다. 이 단계는 프로그램에서 작업하려는 PDF 문서를 어디에서 찾을 수 있는지 알려주기 때문에 매우 중요합니다.

## 2단계: PDF 문서 열기

다음으로, 주석을 달 PDF 문서를 열어야 합니다. 이 작업은 다음을 사용하여 수행됩니다. `Document` Aspose.PDF 라이브러리의 클래스:

```csharp
// 문서 열기
Document pdfDocument = new Document(dataDir + "SetFreeTextAnnotationFormatting.pdf");
```

이 코드 줄은 새로운 것을 초기화합니다. `Document` 객체를 만들고 지정한 PDF 파일을 로드합니다. 파일 이름이 디렉터리에 있는 파일 이름과 일치하는지 확인하세요.

## 3단계: DefaultAppearance 객체 인스턴스화

이제, 만들어 보겠습니다. `DefaultAppearance` 객체입니다. 이 객체는 글꼴, 크기, 색상 등 자유 텍스트 주석의 모양을 정의합니다.

```csharp
// DefaultAppearance 객체 인스턴스화
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 28, System.Drawing.Color.Red);
```

이 예시에서는 Arial 글꼴을 사용하고, 글꼴 크기를 28로 설정하고, 색상은 빨간색으로 선택했습니다. 필요에 맞게 값을 자유롭게 변경하세요!

## 4단계: 자유 텍스트 주석 만들기

모양이 설정되었으니 이제 실제 자유 텍스트 주석을 만들 차례입니다. PDF 파일에서 주석이 표시될 위치를 지정하는 곳입니다.

```csharp
// 주석 만들기
FreeTextAnnotation freetext = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(200, 400, 400, 600), default_appearance);
```

이 라인에서 우리는 새로운 것을 만들고 있습니다 `FreeTextAnnotation` PDF 첫 페이지에 있습니다. 사각형은 주석의 위치와 크기를 정의합니다. 좌표(200, 400, 400, 600)를 조정하여 주석을 원하는 위치에 정확하게 배치할 수 있습니다.

## 5단계: 주석 내용 지정

이제 주석을 만들었으니, 여기에 텍스트를 추가해 보겠습니다.

```csharp
// 주석의 내용을 지정하세요
freetext.Contents = "Free Text";
```

교체할 수 있습니다 `"Free Text"` 주석에 표시할 메시지를 입력하세요. PDF를 보는 모든 사람에게 표시되는 텍스트입니다.

## 6단계: 페이지에 주석 추가

다음으로, 페이지의 주석 컬렉션에 주석을 추가해야 합니다.

```csharp
// 페이지의 주석 컬렉션에 주석 추가
pdfDocument.Pages[1].Annotations.Add(freetext);
```

이 코드 줄은 새로 만든 주석이 PDF 문서에 실제로 추가되도록 합니다. 이 단계를 수행하지 않으면 주석이 최종 출력에 나타나지 않습니다.

## 7단계: 업데이트된 문서 저장

마지막으로 변경 사항을 저장할 차례입니다. 업데이트된 문서의 새 파일 이름을 지정하세요.

```csharp
dataDir = dataDir + "SetFreeTextAnnotationFormatting_out.pdf";
// 업데이트된 문서를 저장합니다
pdfDocument.Save(dataDir);
```

이 코드는 수정된 PDF 파일을 새 이름으로 저장하여 원본 문서는 변경되지 않도록 합니다. 이제 새 PDF 파일을 열어 자유 텍스트 주석이 어떻게 적용되는지 확인해 보세요!

## 결론

축하합니다! Aspose.PDF for .NET을 사용하여 자유 텍스트 주석 서식을 설정하는 방법을 성공적으로 배우셨습니다. 다음 단계를 따라 사용자 지정 주석으로 PDF 문서를 더욱 풍부하고 인터랙티브하며 유익한 정보로 만들 수 있습니다. Aspose.PDF는 주석, 메모 또는 강조 표시를 추가하는 등 작업 흐름을 간소화하는 데 필요한 도구를 제공합니다. 다양한 스타일과 배치를 시도해 보고 PDF를 원하는 대로 만들어 보세요!

## 자주 묻는 질문

### .NET용 Aspose.PDF란 무엇인가요?
.NET용 Aspose.PDF는 개발자가 PDF 문서를 프로그래밍 방식으로 만들고, 편집하고, 조작할 수 있는 라이브러리입니다.

### Aspose.PDF를 무료로 사용할 수 있나요?
네, Aspose는 라이브러리 기능을 체험해 볼 수 있는 무료 체험판을 제공합니다. 다운로드하실 수 있습니다. [여기](https://releases.aspose.com/).

### Aspose.PDF에 대한 지원은 어떻게 받을 수 있나요?
Aspose 포럼을 방문하면 지원을 받을 수 있습니다. [여기](https://forum.aspose.com/c/pdf/10).

### 주석의 모양을 사용자 정의할 수 있나요?
물론입니다! 다음을 사용하여 주석의 글꼴, 크기, 색상 및 기타 속성을 사용자 지정할 수 있습니다. `DefaultAppearance` 수업.

### .NET용 Aspose.PDF는 어디서 구매할 수 있나요?
Aspose.PDF에 대한 라이센스를 구매할 수 있습니다. [여기](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}