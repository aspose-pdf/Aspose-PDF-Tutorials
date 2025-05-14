---
"description": "Aspose.PDF for .NET을 사용하여 PDF의 이미지 크기를 설정하는 방법을 알아보세요. 이 단계별 가이드는 이미지 크기 조정, 페이지 속성 조정, PDF 저장 방법을 안내합니다."
"linktitle": "PDF 파일의 이미지 크기 설정"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일의 이미지 크기 설정"
"url": "/ko/net/programming-with-images/set-image-size/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일의 이미지 크기 설정

## 소개

PDF 작업은 많은 애플리케이션에서 공통적으로 요구되는 기능이며, PDF 파일 내 요소를 조작하는 기능은 매우 중요할 수 있습니다. 보고서 생성기를 구축하든 PDF에 동적 콘텐츠를 추가하든, 문서 내 이미지 크기를 제어하는 것은 필수적인 기능입니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF 파일의 이미지 크기를 설정하는 방법을 안내합니다. 이 강력한 라이브러리는 PDF 콘텐츠에 대한 광범위한 제어 기능을 제공하며, 단계별로 자세히 설명하여 얼마나 쉬운지 보여드리겠습니다. 튜토리얼을 마치면 이미지 크기를 자신 있게 조정하고 이 기능이 PDF 워크플로우를 어떻게 향상시킬 수 있는지 이해하게 될 것입니다.


## 필수 조건

코드를 살펴보기 전에, 이 튜토리얼을 따라가기 위해 꼭 준비해야 할 몇 가지 사항이 있습니다.

1. Aspose.PDF for .NET: 최신 버전의 Aspose.PDF 라이브러리가 설치되어 있는지 확인하세요. [여기서 다운로드하세요](https://releases.aspose.com/pdf/net/).
2. .NET Framework 또는 .NET Core: .NET Framework 또는 .NET Core가 설정된 작업 환경이 있는지 확인하세요.
3. C#에 대한 기본 지식: 프로그래밍 언어로 C#을 사용하므로 이에 익숙해야 합니다.
4. 샘플 이미지: PDF에 삽입할 샘플 이미지가 필요합니다. 원하는 이미지를 사용할 수 있지만, 프로젝트 디렉터리에서 접근할 수 있는지 확인하세요.

## 패키지 가져오기

Aspose.PDF for .NET을 사용하려면 먼저 필요한 네임스페이스를 가져와야 합니다. 간단한 설정은 다음과 같습니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

이제 기본 사항을 살펴보았으니 PDF 문서를 만들고 수정하는 방법으로 넘어가겠습니다.

## 1단계: PDF 문서 초기화

가장 먼저 해야 할 일은 새 PDF 문서를 만드는 것입니다. `Document` 이를 달성하기 위해 Aspose.PDF의 클래스를 사용합니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// 문서 객체 인스턴스화
Document doc = new Document();
```
 
여기서 우리는 인스턴스화합니다 `Document` PDF 파일을 나타내는 객체입니다. 또한 파일이 있는 디렉터리를 지정합니다. `dataDir` 변수입니다. 이는 Aspose.PDF를 사용하여 PDF를 만드는 시작점입니다.

## 2단계: PDF에 새 페이지 추가

문서가 준비되면 페이지를 추가해야 합니다. 모든 PDF에는 최소 한 페이지가 있어야 하므로, 페이지를 하나 추가해 보겠습니다.

```csharp
// PDF 파일의 페이지 컬렉션에 페이지 추가
Aspose.Pdf.Page page = doc.Pages.Add();
```
 
우리는 다음을 사용하여 문서에 새 페이지를 추가합니다. `Pages.Add()` 방법입니다. 이 페이지는 이미지를 배치할 캔버스 역할을 합니다. PDF의 모든 페이지는 기본적으로 텍스트, 이미지 또는 기타 콘텐츠를 추가할 수 있는 빈 공간입니다.

## 3단계: 이미지 인스턴스 생성

이제 PDF에 삽입하려는 이미지를 준비할 시간입니다. Aspose.PDF는 다음을 제공합니다. `Image` 이미지를 처리하는 클래스.

```csharp
// 이미지 인스턴스 생성
Aspose.Pdf.Image img = new Aspose.Pdf.Image();
```
 
우리는 새로운 인스턴스를 생성합니다 `Image` 클래스입니다. 이 객체는 PDF에 추가할 이미지의 속성을 저장합니다. 다음 단계에서 이미지의 크기와 유형을 구성하겠습니다.

## 4단계: 이미지 크기(너비 및 높이) 설정

이제 튜토리얼의 핵심인 이미지 크기 설정에 대해 알아보겠습니다. Aspose.PDF를 사용하면 이미지의 너비와 높이를 포인트 단위로 지정할 수 있습니다.

```csharp
// 이미지 너비와 높이를 포인트 단위로 설정
img.FixWidth = 100;
img.FixHeight = 100;
```
 
그만큼 `FixWidth` 그리고 `FixHeight` 속성을 사용하면 이미지의 정확한 크기를 포인트 단위로 설정할 수 있습니다. 이 예시에서는 이미지 크기를 100x100포인트로 조정합니다. 필요에 따라 이 값을 조정할 수 있습니다.

## 5단계: 이미지 유형 지정

작업 중인 이미지 형식에 따라 이미지 형식을 설정해야 할 수 있습니다. Aspose.PDF는 다양한 이미지 형식을 지원하며, 여기서는 파일 형식을 정의합니다.

```csharp
// 이미지 유형을 SVG로 설정
img.FileType = Aspose.Pdf.ImageFileType.Unknown;
```
 
이 경우에는 파일 유형을 그대로 둡니다. `Unknown`라이브러리가 이미지 유형을 자동으로 감지할 수 있도록 합니다. 특정 파일 유형을 알고 있는 경우 해당 유형을 설정할 수 있습니다(예: `ImageFileType.Jpeg` JPEG 이미지의 경우). 이 단계에서는 Aspose가 이미지를 올바르게 처리하는 방법을 알고 있는지 확인합니다.

## 6단계: 이미지 파일 경로 설정

이제 Aspose에 이미지 파일을 어디에서 찾을지 알려줘야 합니다. 지정된 디렉터리에서 이미지에 접근할 수 있는지 확인하세요.

```csharp
// 소스 파일 경로
img.File = dataDir + "aspose-logo.jpg";
```
 
여기서 이미지의 파일 경로를 설정합니다. 이 경우 이미지는 다음 위치에 있습니다. `dataDir` 폴더이며 이름이 지정됩니다. `aspose-logo.jpg`이것을 이미지 파일의 실제 이름과 위치로 바꿔야 합니다.

## 7단계: 페이지에 이미지 추가

이미지가 구성되고 파일 경로가 설정되었으므로 이제 이미지를 페이지에 추가할 수 있습니다.

```csharp
// 문단 컬렉션에 이미지 추가
page.Paragraphs.Add(img);
```
 
그만큼 `Paragraphs.Add()` 이 방법을 사용하면 페이지에 이미지를 추가할 수 있습니다. `Paragraphs` PDF 페이지에 표시될 항목 목록으로 컬렉션을 정의합니다. 이미지, 텍스트, 도형 등 여러 요소를 이 컬렉션에 추가할 수 있습니다.

## 8단계: 페이지 속성 조정

이미지가 잘 맞도록 페이지 크기를 조정하겠습니다. 이렇게 하면 페이지 크기가 추가하는 콘텐츠와 일치하게 됩니다.

```csharp
// 페이지 속성 설정
page.PageInfo.Width = 800;
page.PageInfo.Height = 800;
```
 
여기서는 페이지 너비와 높이를 800포인트로 설정합니다. 이 단계는 선택 사항이지만, 크기가 조정된 이미지가 페이지에 제대로 적용되도록 보장합니다. 특정 요구 사항에 따라 이 값을 조정할 수 있습니다.

## 9단계: PDF 저장

마지막으로 이미지와 페이지 속성을 구성한 후 PDF를 저장할 수 있습니다.

```csharp
// 결과 PDF 파일을 저장합니다.
dataDir = dataDir + "SetImageSize_out.pdf";
doc.Save(dataDir);
```
 
수정된 문서를 다음과 같이 저장합니다. `SetImageSize_out.pdf` 같은 디렉토리에 있습니다. 이제 이 파일에는 추가한 크기가 조정된 이미지가 포함됩니다.

## 결론

이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF의 이미지 크기를 설정하는 방법을 살펴보았습니다. 문서 생성, 페이지 추가, 이미지 구성, 결과 저장까지 단계별로 살펴보았습니다. 이 단계별 가이드는 Aspose.PDF for .NET을 활용하여 할 수 있는 작업의 시작일 뿐입니다. 이미지 크기 조정 방법을 익혔으니, 이제 텍스트 서식, 표 생성, PDF에 주석 추가 등 다양한 기능을 살펴보세요.

## 자주 묻는 질문

### Aspose.PDF for .NET에서 다양한 이미지 형식을 사용할 수 있나요?  
네, Aspose.PDF는 JPEG, PNG, BMP, SVG 등 다양한 이미지 형식을 지원합니다.

### 이미지의 종횡비를 유지하려면 어떻게 해야 하나요?  
다음 중 하나를 설정하여 종횡비를 유지할 수 있습니다. `FixWidth` 또는 `FixHeight` 다른 차원은 설정하지 않은 채로 둡니다.

### 하나의 PDF 페이지에 여러 이미지를 추가할 수 있나요?  
물론입니다! 이미지 인스턴스를 추가하는 과정을 반복하고 각각을 `Paragraphs` 수집.

### 포인트가 아닌 다른 단위로 이미지 크기를 설정할 수 있나요?  
Aspose.PDF는 주로 포인트 단위로 작동하지만 인치나 밀리미터와 같은 다른 단위도 포인트로 변환할 수 있습니다(1인치 = 72포인트).

### 페이지의 특정 위치에 이미지를 배치하려면 어떻게 해야 하나요?  
설정할 수 있습니다 `Image.LowerLeftX` 그리고 `Image.LowerLeftY` 페이지에 이미지를 배치하기 위한 속성입니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}