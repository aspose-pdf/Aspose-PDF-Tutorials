---
"description": "Aspose.PDF for .NET을 사용하여 PDF 파일에서 텍스트 세그먼트를 검색하는 방법을 단계별로 자세히 알아보세요. 텍스트 추출, 세그먼트 분석 등의 기능을 제공합니다."
"linktitle": "PDF 파일에서 텍스트 세그먼트 페이지 검색"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에서 텍스트 세그먼트 페이지 검색"
"url": "/ko/net/programming-with-text/search-text-segments-page/"
"weight": 470
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에서 텍스트 세그먼트 페이지 검색

## 소개

Aspose.PDF for .NET을 사용하여 PDF 문서에서 특정 텍스트 세그먼트를 찾는 방법을 궁금해하신 적 있으신가요? 잘 오셨습니다! 이 가이드에서는 간단한 단계별 설명으로 그 과정을 안내해 드리겠습니다. 정보 추출, 텍스트 분석, 또는 PDF 조작의 복잡한 과정 등 어떤 작업을 하든 Aspose.PDF for .NET이 도와드리겠습니다. 자, 시작해 볼까요!

## 필수 조건

시작하기에 앞서, 필요한 모든 것이 있는지 확인해 보겠습니다.

- Aspose.PDF for .NET: 라이브러리가 설치되어 있는지 확인하세요. 다음에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/).
- .NET Framework: 컴퓨터에 .NET이 설치되어 있는지 확인하세요.
- 개발 환경: Visual Studio 또는 .NET을 지원하는 IDE를 권장합니다.
- PDF 문서: 텍스트 세그먼트를 검색할 수 있는 PDF 파일입니다.

아직 Aspose.PDF for .NET을 사용하지 않으셨다면 걱정하지 마세요! 다음에서 무료 평가판을 받으실 수 있습니다. [여기](https://releases.aspose.com/) 또는 구매하세요 [여기](https://purchase.aspose.com/buy).

## 패키지 가져오기

코딩을 시작하기 전에 필요한 패키지를 프로젝트에 가져오는 것이 중요합니다. 이렇게 하면 PDF 조작 작업에 필요한 모든 클래스와 메서드를 사용할 수 있습니다.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

기본적인 사항을 파악했으니, 바로 단계별 가이드로 들어가 보겠습니다.


## 1단계: PDF 문서 로드

첫 번째 단계는 PDF 파일을 프로그램에 불러오는 것입니다. 문서가 불러와지지 않으면 검색할 게 없잖아요? 방법은 다음과 같습니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// 문서 열기
Document pdfDocument = new Document(dataDir + "SearchTextSegmentsPage.pdf");
```

- `dataDir`: 이 변수는 PDF 파일의 경로를 저장합니다. `"YOUR DOCUMENT DIRECTORY"` 파일이 저장된 실제 디렉토리와 함께.
- `pdfDocument`: 사용 `Document` 클래스에서 PDF를 메모리에 로드합니다.

## 2단계: 텍스트 검색 설정

이제 문서가 로드되었으므로 다음 단계는 다음을 만드는 것입니다. `TextFragmentAbsorber` 문서 내에서 특정 텍스트를 검색할 수 있는 객체입니다.

```csharp
// 입력 검색어의 모든 인스턴스를 찾기 위해 TextAbsorber 객체를 생성합니다.
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- `TextFragmentAbsorber`: 이 객체는 검색하는 텍스트의 모든 항목을 캡처하는 데 사용됩니다. 바꾸기 `"text"` 검색하려는 실제 텍스트와 함께.

## 3단계: 특정 페이지에 대한 흡수 장치 수락

PDF 문서 전체를 검색하고 싶지 않을 수도 있습니다. 이 예시에서는 특정 페이지로 검색 범위를 좁혀 보겠습니다.

```csharp
// 모든 페이지에 대한 흡수체를 수용합니다.
pdfDocument.Pages[2].Accept(textFragmentAbsorber);
```

- `pdfDocument.Pages[2]`: 이는 문서의 두 번째 페이지만 검색하고 있음을 나타냅니다. 다른 페이지를 대상으로 색인을 수정할 수 있습니다.
- `Accept()`: 이 방법을 사용하면 `TextFragmentAbsorber` 지정된 페이지 내의 텍스트를 처리합니다.

## 4단계: 텍스트 조각 추출

페이지를 검색한 후, 발견된 텍스트 조각을 컬렉션으로 추출합니다.

```csharp
// 추출된 텍스트 조각을 가져옵니다
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`: 이 컬렉션은 검색 과정에서 발견된 모든 텍스트 조각 인스턴스를 보관합니다.

## 5단계: 텍스트 조각을 반복하고 데이터 추출

이제 각 텍스트 조각을 반복하여 위치, 글꼴, 색상 등의 세부 정보를 추출해 보겠습니다.

```csharp
// 조각을 반복합니다
foreach (TextFragment textFragment in textFragmentCollection)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        Console.WriteLine("Text : {0} ", textSegment.Text);
        Console.WriteLine("Position : {0} ", textSegment.Position);
        Console.WriteLine("XIndent : {0} ", textSegment.Position.XIndent);
        Console.WriteLine("YIndent : {0} ", textSegment.Position.YIndent);
        Console.WriteLine("Font - Name : {0}", textSegment.TextState.Font.FontName);
        Console.WriteLine("Font - IsAccessible : {0} ", textSegment.TextState.Font.IsAccessible);
        Console.WriteLine("Font - IsEmbedded : {0} ", textSegment.TextState.Font.IsEmbedded);
        Console.WriteLine("Font - IsSubset : {0} ", textSegment.TextState.Font.IsSubset);
        Console.WriteLine("Font Size : {0} ", textSegment.TextState.FontSize);
        Console.WriteLine("Foreground Color : {0} ", textSegment.TextState.ForegroundColor);
    }
}
```

- `foreach (TextFragment textFragment in textFragmentCollection)`: 우리는 각각을 반복합니다 `TextFragment` 컬렉션에서.
- `foreach (TextSegment textSegment in textFragment.Segments)`: 각 조각 안에는 여러 개의 세그먼트가 있습니다. 이 세그먼트들을 반복하여 모든 관련 정보를 수집합니다.
- 다양한 속성 `textSegment`이러한 정보는 텍스트의 위치(X 및 Y), 글꼴 세부 정보, 크기, 색상 등 텍스트에 대한 자세한 정보를 제공합니다.

## 6단계: 결과 출력

마지막으로 모든 정보를 추출한 후 결과가 콘솔에 출력됩니다. 이를 통해 텍스트의 정확한 위치와 서식 정보를 확인할 수 있습니다.

명확성을 위해 샘플 출력을 보여드리겠습니다.

```
Text : text
Position : X: 45.0, Y: 75.0
XIndent : 45.0
YIndent : 75.0
Font - Name : Arial
Font - IsAccessible : True
Font - IsEmbedded : False
Font - IsSubset : False
Font Size : 12.0
Foreground Color : System.Drawing.Color [Black]
```

- 이 출력은 지정된 페이지에서 "text"라는 텍스트의 정확한 위치와 서식 정보를 제공합니다.

## 결론

자, 이제 끝났습니다! Aspose.PDF for .NET을 사용하여 PDF 문서에서 특정 텍스트 세그먼트를 검색하는 방법을 알아보았습니다. 이 기능은 대용량 PDF를 다룰 때 매우 유용하며, 핵심 텍스트를 효율적으로 찾아 추출할 수 있습니다. 데이터 분석, 정보 추출, 또는 문서 탐색 등 어떤 작업이든 Aspose.PDF는 작업을 완료하는 데 필요한 강력한 도구를 제공합니다.

## 자주 묻는 질문

### 여러 단어나 구문을 검색할 수 있나요?
네, 수정할 수 있습니다. `TextFragmentAbsorber` 입력 문자열을 변경하여 다른 텍스트를 검색합니다.

### 여러 페이지에서 검색하는 것이 가능합니까?
물론입니다! PDF의 모든 페이지를 반복하여 탐색할 수 있습니다. `pdfDocument.Pages`.

### 대소문자를 구분하지 않는 텍스트를 검색하려면 어떻게 해야 하나요?
사용할 수 있습니다 `TextSearchOptions` 대소문자를 구분하지 않고 검색이 가능하도록 합니다.

### 텍스트를 찾은 후에 수정할 수 있나요?
네, 당신이 찾은 후에 `TextFragment`, 텍스트 속성을 수정할 수 있습니다.

### 이 방법을 암호화된 PDF에도 적용할 수 있나요?
네, 올바른 비밀번호를 사용하여 PDF 잠금을 해제하면 됩니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}