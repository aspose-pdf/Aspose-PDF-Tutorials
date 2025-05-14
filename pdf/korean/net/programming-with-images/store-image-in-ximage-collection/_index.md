---
"description": "이 단계별 가이드를 통해 Aspose.PDF for .NET을 사용하여 XImage 컬렉션에 이미지를 저장하는 방법을 알아보세요."
"linktitle": "XImage 컬렉션에 이미지 저장"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "XImage 컬렉션에 이미지 저장"
"url": "/ko/net/programming-with-images/store-image-in-ximage-collection/"
"weight": 290
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# XImage 컬렉션에 이미지 저장

## 소개

오늘날의 디지털 시대에는 프로그래밍 방식으로 문서를 처리하고 조작하는 것이 많은 애플리케이션에 필수적입니다. Aspose.PDF for .NET은 개발자가 PDF 파일을 손쉽게 작업할 수 있도록 지원하여 워크플로를 개선하고 동적 콘텐츠를 제작할 수 있도록 합니다. 이 가이드에서는 XImage 컬렉션에 이미지를 저장하는 과정을 자세히 살펴보겠습니다. XImage는 PDF에 시각적 요소를 직접 삽입할 수 있는 중요한 기능입니다. 멋진 콘텐츠를 제작하는 여정을 시작해 보세요.

## 필수 조건

코드와 프로세스를 자세히 살펴보기 전에 몇 가지 사항을 준비해야 합니다.

- .NET 환경: 컴퓨터에 .NET Framework가 설치되어 있어야 합니다. 프로젝트 요구 사항에 따라 적절한 버전을 선택하세요.
- .NET용 Aspose.PDF: Aspose.PDF 라이브러리가 있는지 확인하세요. 다음에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/) 또는 무료 체험판으로 시작하세요 [여기](https://releases.aspose.com/).
- 이미지 파일: PDF에 저장할 이미지 파일(JPG 또는 PNG 등)도 필요합니다. 이 예시에서는 "aspose-logo.jpg"라는 파일을 사용하겠습니다.
- C#에 대한 기본적인 이해: C# 프로그래밍에 대한 지식이 있으면 원활하게 따라갈 수 있습니다.

## 패키지 가져오기

Aspose.PDF for .NET을 사용하려면 필요한 네임스페이스를 가져와야 합니다. 이 단계를 통해 라이브러리가 제공하는 모든 기능을 활용할 수 있는 기반이 마련됩니다.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Operators;
```

이러한 네임스페이스를 가져오면 Aspose.PDF에서 문서 생성, 이미지 처리 등 다양한 기능을 사용할 수 있습니다.

이를 관리하기 쉬운 단계로 나누어서 따라하기 쉽게 만들어 보겠습니다.

## 1단계: 문서 디렉터리 설정

가장 먼저 해야 할 일은 무엇일까요? 문서를 저장할 위치를 정의하는 것입니다. 문서 디렉터리 경로를 저장하는 변수를 설정해야 합니다. PDF 파일은 여기에 저장됩니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 실제 문서 디렉토리로 바꾸세요.
```

## 2단계: 문서 초기화

이제 새 PDF 문서를 만들 차례입니다. 이 단계에서 PDF가 실제로 생성됩니다. 

```csharp
Aspose.Pdf.Document document = new Document();
```

여기서는 캔버스 역할을 할 새로운 Document 객체를 인스턴스화합니다.

## 3단계: 새 페이지 추가

모든 걸작에는 캔버스가 필요하죠, 그렇죠? 우리의 경우에는 문서 안에 작업할 페이지가 필요합니다.

```csharp
document.Pages.Add();
Page page = document.Pages[1]; // 첫 번째 페이지를 받으세요.
```

문서에 새 페이지를 추가합니다. 이제 이 페이지에서 작업을 진행해 보겠습니다.

## 4단계: 이미지 파일 로드

다음으로, 프로그램에 이미지를 불러와야 합니다. 이 단계는 책을 펼치고 읽는 것과 매우 유사합니다. 즉, 콘텐츠를 사용하려면 먼저 콘텐츠에 접근해야 합니다.

```csharp
using (FileStream imageStream = new FileStream(dataDir + "aspose-logo.jpg", FileMode.Open))
{
```

이 줄은 이미지 파일을 스트림으로 열어서 PDF에 조작하고 내장할 수 있게 해줍니다.

## 5단계: 페이지 리소스에 이미지 추가

이제 이미지를 준비했으니 페이지 리소스에 추가할 차례입니다. 이는 기본적으로 PDF에 "안녕하세요, 기억해두셨으면 하는 멋진 이미지가 있어요!"라고 말하는 것입니다.

```csharp
page.Resources.Images.Add(imageStream, ImageFilterType.Flate);
XImage ximage = page.Resources.Images[page.Resources.Images.Count];
```

이 코드는 PDF에 이미지를 추가하고 이를 다음에 할당하는 힘든 작업을 수행합니다. `XImage` 나중에 참조할 수 있는 변수입니다.

## 6단계: 이미지 그리기 준비

이제 재미있는 부분, 페이지에 이미지를 배치하는 단계입니다. 이미지가 원하는 위치에 정확히 배치되도록 좌표를 설정해야 합니다.

```csharp
page.Contents.Add(new GSave());
```

이 줄은 나중에 복원할 수 있도록 그래픽 상태를 저장합니다. 마치 아무것도 변경하기 전에 설정 상태를 스냅샷으로 찍는 것과 같습니다.

## 7단계: 이미지 위치 및 크기 정의

이제 이미지를 얼마나 크고 어디에 배치할지 정의하세요.

```csharp
int lowerLeftX = 0;
int lowerLeftY = 0;
int upperRightX = 600;
int upperRightY = 600;
Aspose.Pdf.Rectangle rectangle = new Aspose.Pdf.Rectangle(lowerLeftX, lowerLeftY, upperRightX, upperRightY);
```

이 코드 블록은 이미지가 들어갈 사각형의 크기를 설정하여, 본질적으로 페이지에 이미지를 배치하는 역할을 합니다.

## 8단계: 변환 행렬 만들기 

이미지 배치 방식을 제어하기 위해 변환 행렬을 정의합니다. 이 행렬은 이미지가 대상 좌표에 어떻게 나타나는지 결정합니다.

```csharp
Matrix matrix = new Matrix(new double[] { rectangle.URX - rectangle.LLX, 0, 0, rectangle.URY - rectangle.LLY, rectangle.LLX, rectangle.LLY });
```

여행을 떠나기 전에 지도를 그리는 것과 같다고 생각하시면 됩니다. 이미지가 페이지에 어떻게 표시될지 결정하는 데 도움이 됩니다.

## 9단계: 페이지에 이미지 배치

이제 PDF에 이미지를 넣을 위치를 알려줄 차례입니다.

```csharp
page.Contents.Add(new ConcatenateMatrix(matrix));
page.Contents.Add(new Do(ximage.Name));
page.Contents.Add(new GRestore());
```

여기서는 방금 설정한 매트릭스에 따라 이미지를 실제로 그리는 명령을 PDF의 콘텐츠 스트림에 추가합니다.

## 10단계: 문서 저장

드디어 우리 걸작을 구할 수 있게 됐네요! 이제 여러분의 모든 노력이 결실을 맺어 실질적인 결과물로 탄생하는 순간입니다.

```csharp
document.Save(dataDir + "FlateDecodeCompression.pdf");
```

Aspose.PDF에 제공된 파일 이름으로 문서를 저장하도록 설정했습니다. 이 코드를 실행하면 지정된 디렉터리에서 새로 생성된 PDF 파일과 내장된 이미지를 확인할 수 있습니다.

## 결론

자, 이제 끝입니다! Aspose.PDF for .NET을 사용하여 XImage 컬렉션에 이미지를 하나씩 저장하는 방법을 배웠습니다. 코드가 완성되어 유용한 결과물을 만들어내는 모습을 보니 뿌듯하지 않나요? 애플리케이션을 개발하든, 보고서 자동화를 원하든, 이 가이드는 훌륭한 기초 자료가 될 것입니다. Aspose.PDF의 강력한 기능은 이 작업 외에도 다양한 작업에 도움이 될 수 있으니, 계속해서 살펴보세요!

## 자주 묻는 질문

### Aspose.PDF의 이미지에는 어떤 파일 형식이 지원됩니까?
Aspose.PDF는 JPG, PNG, BMP, GIF 등 다양한 이미지 형식을 지원합니다.

### PDF에 이미지를 추가할 때 이미지 크기를 변경할 수 있나요?
네, 사각형에 정의된 좌표를 조정하면 PDF에 표시되는 이미지의 크기를 변경할 수 있습니다.

### Aspose.PDF를 사용하려면 라이선스가 필요합니까?
Aspose는 무료 체험판과 다양한 구매 옵션을 제공합니다. [여기](https://purchase.aspose.com/buy).

### 문제가 발생하면 어떻게 지원을 받을 수 있나요?
Aspose 커뮤니티에서 도움을 요청할 수 있습니다. [여기](https://forum.aspose.com/c/pdf/10).

### PDF에 추가된 이미지에 압축을 적용할 수 있는 방법이 있나요?
네, PDF에 이미지를 추가할 때 이미지 필터 유형을 지정하여 Flate와 같은 압축 방법을 사용할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}