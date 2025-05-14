---
"description": "이 단계별 튜토리얼에서는 Aspose.PDF for .NET의 Floating Box를 사용하여 PDF 머리글과 바닥글에 페이지 번호를 쉽게 추가하는 방법을 소개합니다."
"linktitle": "플로팅 박스를 사용하여 머리글 바닥글에 페이지 번호 표시"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "플로팅 박스를 사용하여 머리글 바닥글에 페이지 번호 표시"
"url": "/ko/net/programming-with-stamps-and-watermarks/page-number-in-header-footer-using-floating-box/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 플로팅 박스를 사용하여 머리글 바닥글에 페이지 번호 표시

## 소개

PDF 문서를 프로그래밍 방식으로 관리할 때 Aspose.PDF for .NET은 탁월한 도구로 손꼽힙니다. .NET 애플리케이션에서 PDF 파일을 생성, 편집 및 조작하는 방식을 간소화합니다. 송장, 보고서 등 어떤 유형의 문서를 생성하든 페이지 번호를 매끄럽게 추가하면 PDF의 전문성과 구성이 향상될 수 있습니다. 이 튜토리얼에서는 플로팅 박스를 사용하여 PDF의 머리글과 바닥글에 페이지 번호를 추가하는 방법을 자세히 알아보겠습니다. 시작할 준비가 되셨나요? 시작해 볼까요!

## 필수 조건

PDF 조작의 영역으로의 흥미진진한 여행을 시작하기 전에 꼭 필요한 몇 가지 사항이 있습니다.

### .NET 환경 설정
.NET 개발 환경이 있는지 확인하세요. .NET 애플리케이션 개발자들 사이에서 인기 있는 Visual Studio를 사용할 수 있습니다.

### Aspose.PDF 라이브러리
Aspose.PDF 라이브러리를 설치하세요. 웹사이트에서 쉽게 다운로드할 수 있습니다.

- [.NET용 Aspose.PDF 다운로드](https://releases.aspose.com/pdf/net/)

### C# 프로그래밍에 대한 기본 지식
C#에 대한 기본적인 이해는 이 튜토리얼에서 제시되는 개념과 코딩 조각을 파악하는 데 도움이 됩니다.

### 문서에 대한 액세스
항상 다음을 갖는 것이 유익합니다. [Aspose.PDF 문서](https://reference.aspose.com/pdf/net/) 추가 기능에 대한 참고 및 심층 탐색에 편리합니다.

## 패키지 가져오기

시작하려면 프로젝트에 필요한 패키지를 가져와야 합니다. 이렇게 하면 Aspose.PDF 어셈블리를 코드에서 사용할 수 있습니다. 방법은 다음과 같습니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

이제 플로팅 박스를 사용하여 페이지 번호를 추가하는 과정을 단계별로 나누어 살펴보겠습니다. 단계별 안내를 따라가세요.

## 1단계: 문서 환경 설정

PDF 문서가 저장될 디렉터리를 지정하는 것부터 시작해 보겠습니다. 이 디렉터리는 출력 파일이 저장되는 위치를 결정하므로 매우 중요합니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

바꾸다 `YOUR DOCUMENT DIRECTORY` 출력 PDF 파일을 저장할 경로를 선택하세요.

## 2단계: 문서 인스턴스화

다음 단계는 새 PDF 문서를 만드는 것입니다. 여기에는 `Document` Aspose.PDF 라이브러리의 클래스입니다.

```csharp
// 문서 인스턴스 인스턴스화
Aspose.Pdf.Document pdf = new Aspose.Pdf.Document();
```
여기서 우리는 새로운 인스턴스를 생성합니다. `Document` 클래스는 우리가 조작할 수 있는 캔버스 역할을 합니다.

## 3단계: 새 페이지 추가

이제 PDF 문서에 페이지를 추가해 보겠습니다. 모든 PDF에는 최소 한 페이지는 있어야 하지 않나요?

```csharp
// PDF 문서에 페이지 추가
Aspose.Pdf.Page page = pdf.Pages.Add();
```
이 코드 조각은 문서에 새 페이지를 추가하여 페이지 번호가 적힌 떠 있는 상자를 비롯한 콘텐츠를 받을 수 있도록 준비합니다.

## 4단계: 떠다니는 상자 만들기

다음으로, 페이지 번호를 담을 플로팅 박스를 만들 차례입니다. `FloatingBox` 클래스를 사용하면 페이지에 콘텐츠를 자유롭게 배치할 수 있습니다.

```csharp
// FloatingBox 클래스의 새 인스턴스를 초기화합니다.
Aspose.Pdf.FloatingBox box1 = new Aspose.Pdf.FloatingBox(140, 80);
```
여기서 매개변수는 `(140, 80)` 플로팅 박스의 너비와 높이를 지정합니다. 레이아웃 설정에 따라 값을 조정할 수 있습니다.

## 5단계: 플로팅 박스 위치 지정

위치 지정이 핵심입니다! 페이지 번호가 페이지에 어디에 표시될지 결정해야 합니다. `Left` 그리고 `Top` 위치를 지정하는 속성입니다.

```csharp
// 문단의 왼쪽 위치를 나타내는 Float 값
box1.Left = 2;
// 문단의 최상위 위치를 나타내는 Float 값
box1.Top = 10;
```
이 값들은 페이지에서 플로팅 박스의 위치를 결정합니다. 자유롭게 값을 조정하여 문서에 가장 잘 어울리는지 확인해 보세요.

## 6단계: 페이지 번호 매크로를 사용하여 텍스트 추가

이제 페이지 번호를 동적으로 표시하는 문자열을 추가해 보겠습니다. 바로 여기서 마법이 일어납니다!

```csharp
// FloatingBox의 문단 컬렉션에 매크로를 추가합니다.
box1.Paragraphs.Add(new Aspose.Pdf.Text.TextFragment("Page: ($p/ $P )"));
```
이 경우에는, `($p/ $P)` 현재 페이지 번호를 표시하는 매크로입니다.`$p`) 및 총 페이지 수(`$P`). 결과적으로 텍스트가 "페이지: 1/5"와 비슷하게 읽히게 됩니다.

## 7단계: 페이지에 플로팅 상자 추가

새로 만든 페이지에 페이지 번호 텍스트와 함께 플로팅 박스를 추가할 차례입니다.

```csharp
// 페이지에 floatingBox를 추가합니다
page.Paragraphs.Add(box1);
```
이 줄은 기본적으로 Floating Box를 페이지에 내장하여 문서 레이아웃의 일부로 만듭니다. 

## 8단계: 문서 저장

마지막으로, 작업 내용을 저장하는 것을 잊지 마세요! 마지막 단계는 PDF 문서를 적절한 파일 이름으로 저장하는 것입니다.

```csharp
// 문서를 저장하세요
pdf.Save(dataDir + "PageNumberinHeaderFooterUsingFloatingBox_out.pdf");
```
지정한 경로에 원하는 파일 이름이 포함되어 있는지 확인하세요. 이제 페이지 번호가 포함된 멋진 PDF가 완성되었습니다! 

## 결론

자, 이제 여러분! Aspose.PDF for .NET을 사용하여 PDF의 머리글과 바닥글에 페이지 번호를 추가하는 것은 정말 간단합니다. 몇 줄의 코드만으로 애플리케이션에서 문서 처리 기술을 마스터하는 여정을 시작할 수 있습니다. 다양한 레이아웃과 서식을 시도해 보세요. 창의력에는 한계가 없으니까요! 전문적인 문서를 만들 준비가 되셨나요? 코딩 실력을 발휘하여 실험을 시작해 보세요.

## 자주 묻는 질문

### 페이지 번호 텍스트의 모양을 사용자 지정할 수 있나요?  
예, 글꼴 크기, 색상, 스타일 등의 텍스트 속성을 조정하여 사용자 정의할 수 있습니다. `TextFragment` 속성.

### Aspose.PDF는 무료로 사용할 수 있나요?  
Aspose.PDF는 무료 평가판을 제공하지만, 실제 업무용으로는 유료 제품입니다. [여기서 사세요](https://purchase.aspose.com/buy).

### 더 자세한 문서는 어디에서 찾을 수 있나요?  
포괄적인 문서는 다음에서 찾을 수 있습니다. [Aspose.PDF 문서 사이트](https://reference.aspose.com/pdf/net/).

### 여러 페이지에 머리글과 바닥글을 적용하려면 어떻게 해야 하나요?  
문서의 모든 페이지를 반복하고 각 페이지에도 마찬가지로 플로팅 상자를 적용할 수 있습니다.

### 추가 기능에 대한 지원이 필요하면 어떻게 해야 하나요?  
추가 질문이나 지원이 필요하면 다음을 방문하세요. [Aspose 포럼](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}