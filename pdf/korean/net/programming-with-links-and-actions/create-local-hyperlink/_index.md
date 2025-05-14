---
"description": "단계별 가이드를 통해 Aspose.PDF for .NET을 사용하여 PDF 파일에 로컬 하이퍼링크를 쉽게 만드는 방법을 알아보세요."
"linktitle": "PDF 파일에 로컬 하이퍼링크 만들기"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에 로컬 하이퍼링크 만들기"
"url": "/ko/net/programming-with-links-and-actions/create-local-hyperlink/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에 로컬 하이퍼링크 만들기

## 소개

이 가이드에서는 Aspose.PDF for .NET을 사용하여 PDF 파일에 로컬 하이퍼링크를 만드는 과정을 안내합니다. 각 단계를 명확하게 설명하여 PDF 조작에 익숙하지 않은 사용자도 쉽게 따라갈 수 있도록 돕습니다.

## 필수 조건

코드를 자세히 살펴보기 전에 먼저 필요한 모든 것이 있는지 확인해 보겠습니다.

1. Visual Studio: .NET 애플리케이션을 개발하는 데 필요합니다. 다음에서 다운로드하세요. [웹사이트](https://visualstudio.microsoft.com/).
2. .NET용 Aspose.PDF: 이 라이브러리는 다음을 통해 다운로드할 수 있습니다. [다운로드 링크 여기](https://releases.aspose.com/pdf/net/)PDF 조작을 위한 다양한 기능이 포함되어 있습니다.
3. C#에 대한 기본 지식: C# 프로그래밍에 대한 약간의 지식이 도움이 되겠지만 걱정하지 마세요. 코드를 줄별로 살펴보겠습니다.
4. .NET Framework: 컴퓨터에 .NET Framework가 설치되어 있는지 확인하세요. Aspose.PDF에서 요구 사항을 확인할 수 있습니다. [선적 서류 비치](https://reference.aspose.com/pdf/net/).

이러한 전제 조건을 충족하면 PDF 문서에서 로컬 하이퍼링크를 만드는 방법을 알아볼 준비가 된 것입니다!

## 패키지 가져오기

이제 모든 준비가 끝났으니 C# 프로젝트에 필요한 패키지를 가져올 차례입니다. Aspose.PDF 라이브러리에는 필요한 모든 클래스가 포함되어 있습니다. 방법은 다음과 같습니다.

### 프로젝트 열기

기존 .NET 프로젝트를 열거나 Visual Studio에서 새 프로젝트를 만드세요. 새로 시작하는 경우 시작 화면에서 "새 프로젝트 만들기"를 선택하세요.

### Aspose.PDF에 참조 추가

솔루션 탐색기에서 프로젝트 폴더의 "종속성"을 마우스 오른쪽 버튼으로 클릭합니다. "NuGet 패키지 관리"를 선택한 후 다음을 검색합니다. `Aspose.PDF`. 최신 버전을 설치하세요. PDF 생성 및 편집에 필요한 모든 도구가 제공됩니다.

### 네임스페이스 가져오기

.cs 파일 맨 위에 다음과 같이 Aspose.PDF 라이브러리에 대한 using 지시문을 추가합니다.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

이렇게 하면 라이브러리의 기능에 접근할 수 있습니다.

로컬 하이퍼링크 생성 과정을 간단한 단계로 나누어 살펴보겠습니다. 각 단계의 원리를 이해하는 데 도움이 되도록 자세히 설명하겠습니다.

## 1단계: 문서 인스턴스 설정

이 단계에서는 작업할 PDF 파일을 나타내는 Document 클래스의 새 인스턴스를 만듭니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 문서 디렉토리 설정
Document doc = new Document(); // 문서 인스턴스 생성
```
그만큼 `dataDir` 변수는 새로 만든 PDF가 저장될 위치입니다. 다음을 바꿔야 합니다. `"YOUR DOCUMENT DIRECTORY"` 시스템의 실제 경로와 함께. `Document` 클래스는 페이지와 링크를 추가할 수 있는 새로운 PDF 문서를 만듭니다.

## 2단계: 문서에 페이지 추가

다음으로, PDF 문서에 페이지를 추가합니다. 

```csharp
Page page = doc.Pages.Add(); // 페이지 컬렉션에 페이지 추가
```
그만큼 `Pages.Add()` 이 메서드는 문서에 새 페이지를 추가합니다. 여기에 모든 콘텐츠가 저장됩니다.

## 3단계: 텍스트 조각 만들기

이제 클릭 가능한 링크 역할을 하는 텍스트를 만들어 보겠습니다.

```csharp
Aspose.Pdf.Text.TextFragment text = new Aspose.Pdf.Text.TextFragment("link page number test to page 7");
```
그만큼 `TextFragment` PDF의 텍스트 세그먼트를 나타냅니다. 여기서는 사용자에게 7페이지로 이동한다는 것을 알려주는 링크를 만들고 있습니다.

## 4단계: 로컬 하이퍼링크 만들기

바로 여기서 마법이 일어납니다! 텍스트 조각이 가리킬 위치를 알려주는 로컬 하이퍼링크를 만들어야 합니다.

```csharp
Aspose.Pdf.LocalHyperlink link = new Aspose.Pdf.LocalHyperlink(); // 로컬 하이퍼링크 생성
link.TargetPageNumber = 7; // 링크 인스턴스에 대한 대상 페이지 설정
text.Hyperlink = link; // TextFragment 하이퍼링크 설정
```
그만큼 `LocalHyperlink` 클래스는 같은 문서의 다른 페이지를 가리킬 수 있게 해줍니다. `TargetPageNumber` 7번에서 하이퍼링크를 클릭하면 해당 특정 페이지로 이동하도록 지정합니다.

## 5단계: 페이지에 텍스트 조각 추가

하이퍼링크를 설정한 후에는 우리가 만든 페이지에 텍스트 조각을 추가할 차례입니다.

```csharp
page.Paragraphs.Add(text); // 페이지의 문단 모음에 텍스트 추가
```
이 줄은 클릭 가능한 텍스트를 페이지의 문단 모음에 추가합니다.

## 6단계: 다른 텍스트 조각 만들기(선택 사항)

1페이지로 돌아갈 수 있는 하이퍼링크를 하나 더 추가해 보겠습니다.

```csharp
text = new TextFragment("link page number test to page 1"); // 새로운 TextFragment를 만듭니다
text.IsInNewPage = true; // 새 페이지에 추가
```
새로운 것을 만드는 중 `TextFragment` 두 번째 링크의 경우 다음을 설정합니다. `IsInNewPage` true로 설정하면 이 텍스트가 새 페이지에 표시됩니다.

## 7단계: 두 번째 로컬 하이퍼링크 설정

이전과 마찬가지로 1페이지에 대한 또 다른 로컬 하이퍼링크를 만듭니다.

```csharp
link = new LocalHyperlink(); // 다른 로컬 하이퍼링크 인스턴스를 만듭니다.
link.TargetPageNumber = 1; // 두 번째 하이퍼링크에 대한 대상 페이지 설정
text.Hyperlink = link; // 두 번째 TextFragment에 대한 링크 설정
```
이 하이퍼링크는 1페이지를 대상으로 하며, 사용자는 2페이지에 도달하면 뒤로 돌아갈 수 있습니다.

## 8단계: 새 페이지에 두 번째 텍스트 조각 추가

이제 이 텍스트를 해당 페이지에 추가해 보겠습니다.

```csharp
page.Paragraphs.Add(text); // 페이지 객체의 문단 컬렉션에 텍스트 추가
```
5단계와 마찬가지로 이 줄은 새로 만든 페이지에 새로운 하이퍼링크 텍스트를 추가합니다.

## 9단계: 문서 저장

마침내, 여러분의 노고를 저장할 시간입니다! 

```csharp
dataDir = dataDir + "CreateLocalHyperlink_out.pdf"; // 출력 파일 이름 지정
doc.Save(dataDir); // 업데이트된 문서 저장
Console.WriteLine("\nLocal hyperlink created successfully.\nFile saved at " + dataDir);
```
이것은 디렉토리 경로와 파일 이름을 결합합니다. `Save()` 이 방법을 사용하면 문서가 저장되고, 확인 메시지가 나타나 모든 것이 원활하게 진행되었음을 알려줍니다!

## 결론

Aspose.PDF for .NET을 사용하여 PDF 파일에 로컬 하이퍼링크를 만드는 것은 단순히 멋진 기술이 아니라, 탐색 기능과 사용자 경험을 향상시키는 실용적인 기능입니다. 이제 독자에게 필요한 정보를 바로 제공할 수 있는 지식을 갖추게 되었습니다. 앞서 언급했던 비유를 다시 생각해 보세요. 더 이상 끝없는 페이지를 헤매는 길 잃은 영혼은 없을 것입니다.

## 자주 묻는 질문

### .NET용 Aspose.PDF란 무엇인가요?
.NET용 Aspose.PDF는 개발자가 .NET 프레임워크를 사용하여 PDF 문서를 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있는 라이브러리입니다.

### 외부 웹페이지에 하이퍼링크를 만들 수 있나요?
네, Aspose.PDF는 PDF 내의 로컬 하이퍼링크 외에도 외부 URL에 대한 하이퍼링크 생성을 지원합니다.

### Aspose.PDF 무료 체험판이 있나요?
물론입니다! 무료 체험판을 다음에서 이용하실 수 있습니다. [대지](https://releases.aspose.com/).

### Aspose는 어떤 프로그래밍 언어를 지원하나요?
Aspose는 Java, C++, Python 등 다양한 프로그래밍 언어에 대한 라이브러리를 제공합니다.

### Aspose 제품에 대한 지원은 어떻게 받을 수 있나요?
지원을 요청할 수 있습니다. [Aspose 포럼](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}