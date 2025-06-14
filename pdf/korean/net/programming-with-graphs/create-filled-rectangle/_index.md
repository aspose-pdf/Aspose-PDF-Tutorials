---
"description": "이 단계별 튜토리얼을 통해 Aspose.PDF for .NET을 사용하여 PDF에 채워진 사각형을 만드는 방법을 알아보세요. 모든 수준의 개발자에게 적합합니다."
"linktitle": "채워진 사각형 만들기"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "채워진 사각형 만들기"
"url": "/ko/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 채워진 사각형 만들기

## 소개

시각적으로 매력적인 PDF를 프로그래밍 방식으로 만들고 싶으신가요? 그렇다면 잘 찾아오셨습니다! 이 튜토리얼에서는 PDF 문서를 손쉽게 조작할 수 있는 강력한 라이브러리인 Aspose.PDF for .NET의 세계를 자세히 살펴보겠습니다. 오늘은 PDF 파일 내에 채워진 사각형을 만드는 방법을 중점적으로 살펴보겠습니다. 숙련된 개발자든 초보자든, 이 가이드를 통해 각 단계를 친절하고 재미있게 안내받으실 수 있습니다. 자, 코딩의 꿈을 꾸고 시작해 보세요!

## 필수 조건

코드로 넘어가기 전에 몇 가지 준비해야 할 사항이 있습니다.

1. Visual Studio: 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요. .NET 개발에 매우 유용한 IDE입니다.
2. Aspose.PDF for .NET: Aspose.PDF 라이브러리를 다운로드하여 설치해야 합니다. [여기](https://releases.aspose.com/pdf/net/).
3. C#에 대한 기본 지식: C# 프로그래밍에 대한 약간의 지식은 코드 조각을 더 잘 이해하는 데 도움이 됩니다.

## 패키지 가져오기

시작하려면 C# 프로젝트에 필요한 패키지를 가져와야 합니다. 방법은 다음과 같습니다.

### 새 프로젝트 만들기

Visual Studio를 열고 새 C# 프로젝트를 만듭니다. 간편하게 콘솔 응용 프로그램을 선택할 수 있습니다.

### Aspose.PDF 참조 추가

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭합니다.
2. "NuGet 패키지 관리"를 선택하세요.
3. "Aspose.PDF"를 검색하여 최신 버전을 설치하세요.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

이제 모든 것을 설정했으니 코드를 살펴보겠습니다!

## 1단계: 문서 디렉터리 설정

먼저, PDF 파일이 저장될 경로를 지정해야 합니다. 이 경로는 프로그램이 파일을 생성할 위치를 알려주므로 매우 중요합니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

바꾸다 `"YOUR DOCUMENT DIRECTORY"` PDF를 저장하려는 컴퓨터의 실제 경로를 입력하세요.

## 2단계: 문서 인스턴스 만들기

다음으로, 우리는 인스턴스를 생성합니다. `Document` 클래스입니다. 이 클래스는 작업할 PDF 문서를 나타냅니다.

```csharp
// 문서 인스턴스 생성
Document doc = new Document();
```

이 줄은 조작할 수 있는 새로운 PDF 문서를 초기화합니다.

## 3단계: 문서에 페이지 추가

이제 문서에 페이지를 추가해 보겠습니다. 모든 PDF에는 최소 한 페이지는 있어야 하지 않나요?

```csharp
// PDF 파일의 페이지 컬렉션에 페이지 추가
Page page = doc.Pages.Add();
```

이 코드는 문서에 새 페이지를 추가하여 그 위에 모양을 그릴 수 있게 해줍니다.

## 4단계: 그래프 인스턴스 생성

모양을 그리려면 다음을 만들어야 합니다. `Graph` 예를 들어, 그래프를 다양한 모양을 그릴 수 있는 캔버스라고 생각해 보세요.

```csharp
// 그래프 인스턴스 생성
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

여기서는 너비가 100이고 높이가 400인 그래프를 만들고 있습니다.

## 5단계: 페이지에 그래프 추가

이제 그래프가 생겼으니, 앞서 만든 페이지에 추가해 보겠습니다.

```csharp
// 페이지 인스턴스의 문단 컬렉션에 그래프 객체 추가
page.Paragraphs.Add(graph);
```

이 선은 그래프를 페이지에 연결하여 그림을 그릴 수 있도록 준비합니다.

## 6단계: 사각형 인스턴스 만들기

다음으로, 색으로 채우고 싶은 사각형을 만들어 보겠습니다.

```csharp
// Rectangle 인스턴스 생성
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

이 코드에서는 사각형의 위치와 크기를 정의합니다. 매개변수는 x, y 좌표, 너비, 높이를 나타냅니다.

## 7단계: 채우기 색상 지정

이제 사각형의 색상을 선택해 보겠습니다. 이 예제에서는 빨간색으로 채우겠습니다.

```csharp
// Graph 객체에 대한 채우기 색상 지정
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

이 선은 사각형의 채우기 색을 빨간색으로 설정합니다. 원하는 색을 선택할 수 있습니다!

## 8단계: 그래프에 사각형 추가

사각형이 준비되었으니 이제 그래프에 추가할 차례입니다.

```csharp
// Graph 객체의 모양 컬렉션에 사각형 객체 추가
graph.Shapes.Add(rect);
```

이 코드는 그래프에 사각형을 추가하여 그림의 일부로 만듭니다.

## 9단계: PDF 문서 저장

마지막으로, 문서를 지정된 디렉토리에 저장해야 합니다.

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// PDF 파일 저장
doc.Save(dataDir);
```

이 코드는 PDF 파일을 다음 이름으로 저장합니다. `CreateFilledRectangle_out.pdf` 이전에 지정한 디렉토리에 있습니다.

## 10단계: 확인 메시지

모든 것이 순조롭게 진행되었음을 알려주기 위해 확인 메시지를 인쇄할 수 있습니다.

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

이 줄은 채워진 사각형이 성공적으로 생성되었음을 확인하는 메시지를 콘솔에 출력합니다.

## 결론

자, 이제 완성되었습니다! Aspose.PDF for .NET을 사용하여 PDF 문서에 채워진 사각형을 성공적으로 만들었습니다. 이 강력한 라이브러리는 PDF 조작의 무한한 가능성을 열어주어 프로그래밍 방식으로 멋진 문서를 만들 수 있도록 해줍니다. 보고서, 송장 또는 기타 유형의 PDF를 생성하든 Aspose.PDF가 해결해 드립니다.

## 자주 묻는 질문

### .NET용 Aspose.PDF란 무엇인가요?
.NET용 Aspose.PDF는 개발자가 PDF 문서를 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있는 라이브러리입니다.

### Aspose.PDF를 무료로 사용할 수 있나요?
네, Aspose는 라이브러리 기능을 체험해 볼 수 있는 무료 체험판을 제공합니다. 다운로드하실 수 있습니다. [여기](https://releases.aspose.com/).

### Aspose.PDF에 대한 지원을 받을 수 있는 방법이 있나요?
물론입니다! Aspose 포럼을 통해 지원을 받으실 수 있습니다. [여기](https://forum.aspose.com/c/pdf/10).

### Aspose.PDF를 어떻게 구매할 수 있나요?
구매 페이지를 방문하여 Aspose.PDF를 구매하실 수 있습니다. [여기](https://purchase.aspose.com/buy).

### Aspose.PDF로 어떤 유형의 모양을 만들 수 있나요?
Aspose.PDF 라이브러리를 사용하면 사각형, 원, 선 등 다양한 모양을 만들 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}