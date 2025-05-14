---
"description": "이 포괄적인 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF 문서에 목차를 추가하는 동시에 페이지 번호를 사용자 지정하는 방법을 알아봅니다."
"linktitle": "TOC를 추가하는 동안 페이지 번호 사용자 지정"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "TOC를 추가하는 동안 페이지 번호 사용자 지정"
"url": "/ko/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# TOC를 추가하는 동안 페이지 번호 사용자 지정

## 소개

문서 관리 분야에서 PDF는 최고의 자리를 차지하고 있습니다. 다양한 플랫폼에서 문서를 공유하고 보존하는 데 필수적인 형식입니다. 하지만 목차(TOC)와 같은 기능으로 PDF 문서를 더욱 돋보이게 하고 싶다면 어떻게 해야 할까요? 바로 Aspose.PDF for .NET이 그 해답입니다! 이 강력한 라이브러리를 통해 개발자는 PDF 파일을 손쉽게 조작하고 콘텐츠를 추가, 수정 및 사용자 지정할 수 있습니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF 문서에 목차를 추가하면서 페이지 번호를 사용자 지정하는 방법을 자세히 알아보겠습니다. 자, 코딩 실력을 키우고 시작해 볼까요!

## 필수 조건

코드로 넘어가기 전에 몇 가지 준비해야 할 사항이 있습니다.

1. Visual Studio: 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요. 이것이 개발 환경이 될 것입니다.
2. Aspose.PDF for .NET: Aspose.PDF 라이브러리를 다운로드하여 설치해야 합니다. [여기](https://releases.aspose.com/pdf/net/).
3. C#에 대한 기본 지식: C# 프로그래밍에 대한 지식은 코드 조각을 더 잘 이해하는 데 도움이 됩니다.
4. 샘플 PDF 파일: 작업할 수 있는 샘플 PDF 파일을 준비해 주세요. 간단한 파일을 만들거나 기존 PDF 파일을 다운로드할 수 있습니다.

## 패키지 가져오기

시작하려면 필요한 패키지를 가져와야 합니다. Visual Studio 프로젝트를 열고 Aspose.PDF 라이브러리에 대한 참조를 추가하세요. NuGet 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭합니다.
2. "NuGet 패키지 관리"를 선택하세요.
3. "Aspose.PDF"를 검색하여 설치하세요.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

라이브러리를 설치하면 코딩을 시작할 수 있습니다!

## 1단계: 문서 디렉터리 설정

먼저, 문서 디렉터리를 설정해야 합니다. 여기에 입력 및 출력 PDF 파일을 저장할 것입니다. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

이 스니펫에서 다음을 교체하세요. `YOUR DOCUMENT DIRECTORY` PDF 파일이 있는 실제 경로를 입력하세요. 이렇게 하면 기존 PDF를 로드하고 수정된 버전을 저장하는 데 도움이 됩니다.

## 2단계: 기존 PDF 파일 로드

이제 문서 디렉토리를 설정했으니 기존 PDF 파일을 로드해 보겠습니다. 

```csharp
Document doc = new Document(inFile);
```

여기서 우리는 새로운 것을 만듭니다 `Document` 입력 파일 경로를 전달하여 객체를 생성합니다. 이를 통해 PDF 콘텐츠를 프로그래밍 방식으로 조작할 수 있습니다.

## 3단계: TOC에 대한 새 페이지 삽입

다음으로, 목차가 들어갈 PDF에 새 페이지를 만들어야 합니다.

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

이 줄은 문서 시작 부분에 새 페이지를 삽입합니다. 이 페이지에 목차가 표시됩니다.

## 4단계: TOC 정보 생성

이제 TOC 정보를 나타내는 객체를 만들어 보겠습니다.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

이 단계에서는 다음을 생성합니다. `TocInfo` 객체를 만들고 제목을 "목차"로 설정합니다. 또한 글꼴 크기와 스타일도 사용자 지정합니다. `PageNumbersPrefix` "P"로 설정하면 TOC에 페이지 번호가 접두사로 추가됩니다.

## 5단계: TOC에 제목 추가

이제 재미있는 부분입니다! 문서의 페이지를 순회하며 목차에 제목을 추가해 보겠습니다.

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

이 루프에서 우리는 새로운 것을 만듭니다. `Heading` 각 페이지에 대한 객체를 생성합니다. 각 제목의 대상 페이지를 설정하고 표시할 텍스트를 지정합니다. 텍스트는 "페이지 X"이며, 여기서 X는 페이지 번호입니다. 마지막으로 목차 페이지에 제목을 추가합니다.

## 6단계: 업데이트된 문서 저장

필요한 제목을 모두 추가한 후에는 업데이트된 문서를 저장할 차례입니다.

```csharp
doc.Save(outFile);
```

이 줄은 목차를 포함한 수정된 PDF를 저장합니다. 이제 출력 파일을 열어 사용자 지정 목차를 확인할 수 있습니다!

## 결론

자, 이제 완성했습니다! Aspose.PDF for .NET을 사용하여 PDF 문서에 목차를 추가하면서 페이지 번호를 성공적으로 사용자 지정했습니다. 이 강력한 라이브러리를 사용하면 PDF 파일을 쉽게 조작할 수 있으며, 몇 줄의 코드만으로 문서를 크게 개선할 수 있습니다. 보고서, 전자책 또는 기타 유형의 PDF를 만들 때 목차를 사용하면 독자의 탐색 기능을 크게 향상시킬 수 있습니다. 자, 이제 무엇을 기다리시나요? Aspose.PDF를 사용하여 지금 바로 멋진 PDF를 만들어 보세요!

## 자주 묻는 질문

### .NET용 Aspose.PDF란 무엇인가요?
.NET용 Aspose.PDF는 개발자가 PDF 문서를 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있는 라이브러리입니다.

### Aspose.PDF를 무료로 사용할 수 있나요?
네, Aspose는 라이브러리 기능을 체험해 볼 수 있는 무료 체험판을 제공합니다. 다운로드하실 수 있습니다. [여기](https://releases.aspose.com/).

### Aspose.PDF에 대한 지원은 어떻게 받을 수 있나요?
Aspose 포럼을 방문하면 지원을 받을 수 있습니다. [여기](https://forum.aspose.com/c/pdf/10).

### 임시면허가 있나요?
네, Aspose.PDF에 대한 임시 라이선스를 요청할 수 있습니다. [여기](https://purchase.aspose.com/temporary-license/).

### .NET용 Aspose.PDF는 어디서 구매할 수 있나요?
.NET용 Aspose.PDF를 구매할 수 있습니다. [여기](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}