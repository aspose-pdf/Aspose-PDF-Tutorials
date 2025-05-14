---
"description": "Aspose.PDF for .NET을 사용하여 PDF 문서의 모든 페이지에서 텍스트를 검색하고 가져오는 방법을 알아보세요."
"linktitle": "모든 텍스트 검색 및 가져오기"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "모든 텍스트 검색 및 가져오기"
"url": "/ko/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 모든 텍스트 검색 및 가져오기

## 소개

PDF에서 특정 텍스트를 추출해야 했지만 까다로웠던 경험이 있으신가요? PDF는 마치 잠긴 컨테이너처럼 느껴져 필요한 정보를 얻기 어려울 수 있습니다. 하지만 좋은 소식이 있습니다. Aspose.PDF for .NET을 사용하면 모든 PDF에서 텍스트를 쉽게 검색하고 가져올 수 있습니다. 이 강력한 라이브러리는 .NET 애플리케이션에서 PDF 작업에 필요한 모든 기능을 제공하여 텍스트 추출을 간편하게 해줍니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF 파일에서 텍스트를 검색하고 추출하는 과정을 안내합니다. 텍스트 분석 도구를 개발하든 PDF 보고서에서 데이터 추출을 자동화해야 하든, 바로 여기가 정답입니다!

## 필수 조건

코드로 넘어가기 전에 모든 것이 설정되어 있는지 확인해 보겠습니다.

1. Aspose.PDF for .NET: Aspose.PDF for .NET을 다운로드하여 설치해야 합니다. 다운로드 페이지에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/).
2. .NET 환경: 개발용 컴퓨터에 .NET Framework 또는 .NET Core가 설치되어 있는지 확인하세요.
3. 기본 C## 지식: C#에 대한 지식과 .NET 프로젝트 작업에 대한 지식이 권장됩니다.
4. PDF 문서: 텍스트를 추출할 샘플 PDF 파일입니다. 이 예시에서는 `SearchAndGetTextFromAll.pdf`.

## 패키지 가져오기

코드를 작성하기 전에 Aspose.PDF에서 작업하는 데 필요한 네임스페이스를 프로젝트에 가져와야 합니다.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

이러한 네임스페이스는 PDF의 문서 객체 모델에 대한 액세스를 제공하고 파일 내의 텍스트를 조작할 수 있게 해줍니다.

쉽게 따라할 수 있도록 과정을 간단한 단계로 나누어 보겠습니다.

## 1단계: 문서 디렉터리 설정

먼저 PDF 파일이 있는 디렉터리 경로를 지정해야 합니다. 이렇게 하면 애플리케이션이 텍스트를 추출할 파일을 찾는 데 도움이 됩니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- 그만큼 `dataDir` 변수는 디렉토리를 가리켜야 합니다. `SearchAndGetTextFromAll.pdf` 파일이 저장되었습니다.
- 바꾸다 `"YOUR DOCUMENT DIRECTORY"` 컴퓨터의 실제 경로와 함께.

## 2단계: PDF 문서 열기

다음으로 Aspose.PDF를 사용하여 PDF 문서를 엽니다. `Document` 물체.

```csharp
// 문서 열기
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- 우리는 새로운 인스턴스를 생성합니다 `Document` PDF의 전체 파일 경로를 전달하여 클래스를 만듭니다.
- 이렇게 하면 PDF가 메모리에 로드되어 처리할 준비가 됩니다.

## 3단계: 텍스트 흡수기 만들기

그만큼 `TextFragmentAbsorber` object는 PDF 파일 내에서 특정 텍스트를 검색하는 데 사용됩니다. 이 경우 "text"라는 단어를 검색하겠습니다.

```csharp
// 입력 검색어의 모든 인스턴스를 찾기 위해 TextAbsorber 객체를 생성합니다.
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- 그만큼 `TextFragmentAbsorber` 문자열로 초기화됩니다 `"text"`즉, PDF 문서 내에서 "텍스트"라는 단어가 나타나는 부분을 찾습니다.

## 4단계: 모든 페이지에 대한 흡수체 수락

이제 PDF 문서에 흡수체를 허용하고 모든 페이지에서 텍스트를 검색하도록 지시하겠습니다.

```csharp
// 모든 페이지에 대한 흡수체를 수용합니다.
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- 그만큼 `Accept` 메서드가 문서의 페이지에 적용됩니다. 이 메서드는 지정된 텍스트를 모든 페이지에서 검색합니다.

## 5단계: 텍스트 조각 추출

흡수체가 문서를 스캔하면 추출된 텍스트 조각을 검색할 수 있습니다.

```csharp
// 추출된 텍스트 조각을 가져옵니다
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- 그만큼 `TextFragments` 의 재산 `TextFragmentAbsorber` 검색어와 일치하는 모든 텍스트 조각의 컬렉션을 반환합니다.

## 6단계: 텍스트 조각 반복

이제 텍스트 조각 컬렉션이 있으므로 이를 반복하여 세부 정보를 추출하겠습니다.

```csharp
// 조각을 반복합니다
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- 그만큼 `foreach` 루프는 각각을 반복합니다 `TextFragment` 컬렉션에서.
- 각 조각의 실제 텍스트, 페이지에서의 위치, 글꼴 세부 정보, 글꼴 크기 등 다양한 속성을 인쇄합니다.
- 그만큼 `XIndent` 그리고 `YIndent` 속성은 PDF 내 텍스트 조각의 정확한 좌표를 제공합니다.

## 결론

자, 이제 완성했습니다! 몇 줄의 코드만으로 Aspose.PDF for .NET을 사용하여 PDF에서 텍스트를 검색하고 추출하는 데 성공했습니다. Aspose.PDF는 유연하게 PDF를 다양한 방식으로 조작할 수 있어 .NET 환경에서 강력한 PDF 솔루션을 필요로 하는 개발자에게 탁월한 선택입니다. 이 예제를 확장하여 다른 단어를 검색하거나, 더 자세한 정보를 추출하거나, 필요에 따라 PDF 콘텐츠를 조작할 수도 있습니다. 이 가이드가 PDF 작업에 대한 명확하고 직관적인 접근 방식을 제공해 주었기를 바랍니다. 직접 PDF를 만들어 보세요!

## 자주 묻는 질문

### 여러 단어를 동시에 검색할 수 있나요?  
네, 수정할 수 있습니다. `TextFragmentAbsorber` 검색 문자열을 적절히 조정하여 여러 구문을 검색합니다.

### 텍스트가 여러 줄에 걸쳐 있으면 어떻게 되나요?  
Aspose.PDF는 텍스트가 여러 줄에 걸쳐 있어도 인식하고 추출합니다. 각 조각을 개별적으로 처리할 수 있습니다.

### 추출된 텍스트를 파일로 저장하려면 어떻게 해야 하나요?  
다음과 같은 표준 C# 파일 I/O 작업을 사용하여 추출된 텍스트를 파일에 쓸 수 있습니다. `StreamWriter`.

### Aspose.PDF는 스캔한 PDF에서 텍스트를 추출하는 기능을 지원합니까?  
Aspose.PDF는 OCR을 지원하지 않습니다. 스캔한 PDF의 경우, 텍스트를 인식하려면 OCR 도구가 필요합니다.

### 암호화된 PDF를 어떻게 처리하나요?  
PDF가 암호로 보호된 경우 Aspose.PDF에서 문서를 로드할 때 암호를 입력하여 잠금을 해제할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}