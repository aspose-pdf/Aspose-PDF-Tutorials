---
"description": "이 튜토리얼을 통해 Aspose.PDF for .NET을 사용하여 PDF 파일에서 강조 표시된 텍스트를 효율적으로 추출하는 방법을 알아보세요. 데이터 분석 및 콘텐츠 검토에 적합합니다."
"linktitle": "PDF 파일에서 강조된 텍스트 추출"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에서 강조된 텍스트 추출"
"url": "/ko/net/annotations/extracthighlightedtext/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에서 강조된 텍스트 추출

## 소개

PDF 파일 작업 시, 데이터 분석, 콘텐츠 검토, 또는 간단한 노트 정리 등 강조 표시된 텍스트를 추출하는 것은 매우 중요한 작업입니다. Aspose.PDF for .NET을 사용하는 경우, 이 과정은 간단하고 효율적입니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF 문서에서 강조 표시된 텍스트를 추출하는 방법을 안내합니다. 필수 조건부터 단계별 안내까지 모든 내용을 다루어 학습을 완료할 때까지 포괄적으로 이해할 수 있도록 도와드립니다.

## 필수 조건

코드를 살펴보기 전에 꼭 준비해야 할 몇 가지 사항이 있습니다.

- Aspose.PDF for .NET 라이브러리: Aspose.PDF 라이브러리가 설치되어 있는지 확인하세요. 설치되어 있지 않으면 다음에서 다운로드할 수 있습니다. [출시 페이지](https://releases.aspose.com/pdf/net/).
- 개발 환경: Visual Studio와 같은 작동하는 개발 환경을 설정해야 합니다.
- C#에 대한 기본 지식: C# 프로그래밍 언어와 객체 지향 프로그래밍에 대한 지식이 필수입니다.
- 유효한 Aspose 라이센스: 무료 평가판으로 시작할 수 있지만 다음을 고려하십시오. [임시 면허](https://purchase.aspose.com/temporary-license/) 또는 다음에서 구매 [여기](https://purchase.aspose.com/buy) 제한 없이 사용 가능.

## 패키지 가져오기

시작하려면 C# 프로젝트에 필요한 네임스페이스를 가져와야 합니다. 이는 Aspose.PDF for .NET에서 제공하는 클래스와 메서드에 액세스하는 데 필수적입니다.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

이제 Aspose.PDF for .NET을 사용하여 PDF 파일에서 강조 표시된 텍스트를 추출하는 과정을 자세히 살펴보겠습니다. 각 단계를 자세히 설명하여 기본 개념과 구현 방식을 이해하는 데 도움을 드립니다.

## 1단계: 프로젝트 디렉토리 설정

가장 먼저, PDF 파일이 있는 프로젝트 디렉터리를 설정해야 합니다. 바로 여기서 마법이 일어납니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

바꾸다 `"YOUR DOCUMENT DIRECTORY"` PDF 파일이 있는 디렉토리의 실제 경로를 입력합니다. 이 디렉토리는 애플리케이션이 처리할 PDF 파일을 가져오는 곳입니다.

## 2단계: PDF 문서 로드

다음으로, 강조 표시된 텍스트를 추출할 PDF 문서를 로드해야 합니다. 이 작업은 다음을 사용하여 수행됩니다. `Document` Aspose.PDF에서 제공하는 클래스입니다.

```csharp
Document doc = new Document(dataDir + "ExtractHighlightedText.pdf");
```

그만큼 `Document` 클래스는 PDF 파일 경로로 인스턴스화됩니다. 여기서는 `"ExtractHighlightedText.pdf"` 강조 표시된 텍스트가 포함된 PDF 파일의 이름입니다. 이 파일이 지정된 디렉터리에 있는지 확인하세요.

## 3단계: 주석 컬렉션에 액세스

PDF 문서가 로드되면 다음 단계는 문서 첫 페이지의 주석에 접근하는 것입니다. 주석은 PDF에서 강조 표시, 주석 등과 같은 추가 정보를 추가하는 데 사용됩니다.

```csharp
foreach (Annotation annotation in doc.Pages[1].Annotations)
{
```

그만큼 `Annotations` 의 재산 `Page` 객체는 PDF의 특정 페이지에 있는 모든 주석에 대한 액세스를 제공합니다. 여기서는 첫 페이지의 각 주석을 반복합니다.

## 4단계: 강조 표시된 텍스트 주석 필터링

이제 모든 주석에 접근할 수 있게 되었으므로, 강조 표시된 텍스트 주석만 필터링해야 합니다. 이는 각 주석의 유형을 확인하여 수행됩니다.

```csharp
if (annotation is TextMarkupAnnotation)
{
    TextMarkupAnnotation highlightedAnnotation = annotation as TextMarkupAnnotation;
```

그만큼 `TextMarkupAnnotation` 클래스는 강조 표시를 포함한 텍스트 마크업 주석을 나타내는 데 사용됩니다. `is` 키워드는 주석이 유형인지 확인합니다. `TextMarkupAnnotation`, 그렇다면 주석을 다음으로 캐스팅합니다. `TextMarkupAnnotation`.

## 5단계: 강조 표시된 텍스트 추출

강조된 주석을 식별한 후 다음 단계는 강조 표시와 관련된 텍스트를 추출하는 것입니다.

```csharp
TextFragmentCollection collection = highlightedAnnotation.GetMarkedTextFragments();
foreach (TextFragment tf in collection)
{
    Console.WriteLine(tf.Text);
}
```

그만큼 `GetMarkedTextFragments()` 메서드는 컬렉션을 반환합니다. `TextFragment` 각 객체는 강조 표시된 텍스트의 일부를 나타냅니다. 이 컬렉션을 반복하여 각 조각의 텍스트를 콘솔에 출력합니다.

## 결론

Aspose.PDF for .NET을 사용하여 PDF에서 강조 표시된 텍스트를 추출하는 기능은 특히 대용량 문서를 다룰 때 워크플로우를 간소화하는 강력한 기능입니다. 이 튜토리얼에 설명된 단계를 따르면 자신의 프로젝트에 이 기능을 쉽게 구현할 수 있습니다. 메모 정리, 보고서 작성, 데이터 분석 등 어떤 작업을 하든 이 방법은 강조 표시된 텍스트를 추출하고 활용하는 완벽한 솔루션을 제공합니다.

## 자주 묻는 질문

### 이 방법을 사용하여 다른 유형의 주석을 추출할 수 있나요?  
예, 다음을 수정하여 다른 유형의 주석을 추출할 수 있습니다. `if` 다양한 주석 유형을 확인하기 위한 조건(예: `TextAnnotation`, `StampAnnotation`, 등.

### PDF의 모든 페이지에서 강조된 텍스트를 추출하는 것이 가능합니까?  
물론입니다! PDF 문서의 각 페이지를 반복해서 살펴보고 동일한 추출 로직을 적용하여 모든 페이지에서 강조 표시된 텍스트를 수집할 수 있습니다.

### Aspose.PDF for .NET을 사용하려면 라이선스가 필요합니까?  
무료 체험판으로 시작할 수 있지만, [임시 면허](https://purchase.aspose.com/temporary-license/) 또는 모든 기능에 대한 제한 없는 액세스를 위해 전체 라이선스를 구매하세요.

### 콘솔에 인쇄하는 대신 추출된 텍스트를 파일에 저장할 수 있나요?  
네, 코드를 쉽게 수정하여 추출된 텍스트를 텍스트 파일이나 다른 원하는 형식으로 저장할 수 있습니다.

### Aspose.PDF는 .NET 이외의 다른 플랫폼을 지원합니까?  
네, Aspose.PDF는 Java와 다른 플랫폼도 지원하여 다양한 환경에서 비슷한 기능을 제공합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}