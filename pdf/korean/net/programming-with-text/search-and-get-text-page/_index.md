---
"description": "Aspose.PDF for .NET을 사용하여 PDF 파일의 특정 페이지에서 텍스트를 검색하고 가져오는 방법을 알아보세요."
"linktitle": "PDF 파일에서 텍스트 페이지 검색 및 가져오기"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에서 텍스트 페이지 검색 및 가져오기"
"url": "/ko/net/programming-with-text/search-and-get-text-page/"
"weight": 430
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에서 텍스트 페이지 검색 및 가져오기

## 소개

PDF 문서에서 특정 텍스트를 검색하여 나중에 사용하기 위해 추출해야 했던 경험이 있으신가요? 문서를 처리하고 정밀한 데이터 추출이 필요한 앱을 개발 중이거나, PDF를 효율적으로 분석해야 하는 경우 등 어떤 경우든, 바로 여기가 정답입니다! 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF 파일의 특정 페이지에서 텍스트를 검색하고 가져오는 방법을 자세히 알아보겠습니다. 초보자든 숙련된 개발자든, 이 가이드는 각 단계를 쉽고 재미있게 안내해 드립니다. 시작할 준비가 되셨나요? 시작해 볼까요!

## 필수 조건

코딩에 들어가기 전에 필요한 모든 것이 있는지 확인해 보겠습니다.

1. .NET 라이브러리용 Aspose.PDF: 여기에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/) 또는 같은 링크에서 무료 체험판을 받으세요. 구매하려면 [애스포즈 매장](https://purchase.aspose.com/buy).
2. .NET Framework: Visual Studio와 같은 .NET 개발 환경이 필요합니다.
3. PDF 파일: 텍스트를 검색하고 추출할 수 있는 샘플 PDF 파일이 필요합니다. 이 튜토리얼에서는 파일 이름이 다음과 같다고 가정하겠습니다. `SearchAndGetTextPage.pdf`.

## 패키지 가져오기

먼저 Aspose.PDF for .NET을 사용하는 데 필요한 네임스페이스를 가져와야 합니다. 이 네임스페이스가 코드 상단에 포함되어 있는지 확인하세요.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System
```

이제 전제 조건을 살펴보았으니 코드를 단계별로 자세히 살펴보겠습니다. 각 단계는 명확하게 설명되어 있어 따라하기 쉽습니다.

## 1단계: 문서 디렉터리 경로 설정

PDF 파일을 사용하기 전에 PDF 문서가 저장된 경로를 정의해야 합니다. 이렇게 하면 프로그램이 해당 파일에 접근할 수 있습니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- dataDir: PDF 파일이 저장된 폴더의 경로입니다. 바꾸기 `"YOUR DOCUMENT DIRECTORY"` PDF가 위치한 실제 경로를 사용합니다.

## 2단계: PDF 문서 로드

다음 단계는 PDF 문서를 메모리에 불러와서 작업하는 것입니다. 방법은 다음과 같습니다.

```csharp
Document pdfDocument = new Document(dataDir + "SearchAndGetTextPage.pdf");
```

- 문서: PDF 파일을 로드하는 Aspose.PDF 클래스입니다.
- pdfDocument: PDF 파일이 로드된 후 저장되는 변수입니다.

## 3단계: 텍스트 흡수기 개체 만들기

그만큼 `TextFragmentAbsorber` 클래스를 사용하면 PDF에서 특정 텍스트를 검색할 수 있습니다. 주어진 검색어의 모든 인스턴스를 찾는 이 클래스의 인스턴스를 만들어 보겠습니다.

```csharp
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Figure");
```

- TextFragmentAbsorber: 이 클래스는 PDF에서 텍스트를 찾아 추출하는 역할을 합니다.
- "그림": PDF 내에서 검색하려는 텍스트로 바꾸세요.

## 4단계: 전체 PDF에 텍스트 흡수기 적용

텍스트 흡수기를 설정한 후에는 프로그램에서 PDF의 모든 페이지를 검색하도록 설정해야 합니다.

```csharp
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- Accept(): 이 메서드는 PDF에 텍스트 흡수기를 적용하여 모든 페이지에서 지정한 텍스트를 스캔합니다.

## 5단계: 추출된 텍스트 검색 및 반복

PDF를 스캔했으니 이제 결과를 가져와서 표시할 차례입니다. 추출된 텍스트 조각을 반복해서 살펴보겠습니다.

```csharp
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- TextFragmentCollection: 이 컬렉션은 텍스트 흡수기에서 찾은 모든 텍스트 조각 인스턴스를 보관합니다.

## 6단계: 각 조각을 반복하고 데이터 추출

이제 우리는 다음을 반복합니다. `textFragmentCollection` 각 텍스트 세그먼트의 위치, 글꼴 세부 정보, 색상 등 다양한 속성을 추출합니다.

```csharp
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

- TextFragment: 각 조각에는 발견된 텍스트의 일부가 포함되어 있습니다.
- TextSegment: 각 조각은 텍스트의 여러 부분을 나타내는 여러 개의 세그먼트를 가질 수 있습니다.
- TextState: 텍스트의 글꼴, 크기, 색상에 대한 자세한 정보를 제공합니다.

이 루프에서는 실제 텍스트, 위치(X 및 Y 좌표), 글꼴, 글꼴이 PDF에 포함되어 있는지 여부, 텍스트의 전경색과 같은 세부 정보를 인쇄합니다.

## 결론

자, 이제 끝났습니다! Aspose.PDF for .NET을 사용하여 PDF 파일에서 텍스트를 성공적으로 검색하고 추출했습니다. 이 라이브러리의 유연성은 정말 놀랍습니다. 대용량 문서에서 특정 텍스트를 검색하거나, 추출하거나, 속성을 분석해야 할 때 Aspose.PDF를 사용하면 매우 간편하게 작업할 수 있습니다. 또한, 앞서 설명한 코드를 통해 필요에 맞게 쉽게 조정할 수 있습니다. 

## 자주 묻는 질문

### 여러 구문을 동시에 검색할 수 있나요?  
예, 여러 개의 구문을 생성하여 여러 구문을 검색하도록 코드를 수정할 수 있습니다. `TextFragmentAbsorber` 사물.

### 특정 페이지에서 텍스트를 추출하려면 어떻게 해야 하나요?  
특정 페이지를 타겟으로 삼을 수 있습니다. `TextFragmentAbsorber` 전체 문서 대신 한 페이지로만 표시됩니다. 예: `pdfDocument.Pages[1].Accept(textFragmentAbsorber);`.

### Aspose.PDF for .NET은 무료인가요?  
Aspose.PDF는 상업용 제품이지만 다음과 함께 사용할 수 있습니다. [무료 체험](https://releases.aspose.com/).

### Aspose.PDF를 사용하여 PDF에서 이미지를 추출할 수 있나요?  
네, Aspose.PDF를 사용하면 텍스트뿐만 아니라 이미지도 추출할 수 있습니다. [선적 서류 비치](https://reference.aspose.com/pdf/net/) 자세한 내용은.

### 더 많은 도움이나 지원이 필요하면 어떻게 해야 하나요?  
당신은 항상 도움을 받을 수 있습니다 [Aspose 지원 포럼](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}