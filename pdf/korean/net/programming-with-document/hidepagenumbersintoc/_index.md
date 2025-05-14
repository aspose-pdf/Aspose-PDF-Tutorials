---
"description": "Aspose.PDF for .NET을 사용하여 목차에서 페이지 번호를 숨기는 방법을 알아보세요. 코드 예제와 함께 제공되는 이 자세한 가이드를 따라 전문가 수준의 PDF를 만들어 보세요."
"linktitle": "TOC에서 페이지 번호 숨기기"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "TOC에서 페이지 번호 숨기기"
"url": "/ko/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# TOC에서 페이지 번호 숨기기

## 소개

PDF 작업을 하다 보면 목차(TOC)를 만들면서도 페이지 번호를 숨겨 깔끔한 느낌을 유지하고 싶을 때가 있습니다. 페이지 번호가 없으면 문서 흐름이 더 좋아질 수도 있고, 미적인 측면을 고려한 선택일 수도 있습니다. 어떤 이유든 Aspose.PDF for .NET을 사용한다면 이 튜토리얼을 통해 목차에서 페이지 번호를 숨기는 방법을 자세히 알아보세요.

## 필수 조건

시작하기 전에 몇 가지 준비해야 할 사항이 있습니다. 간단한 체크리스트는 다음과 같습니다.

- Visual Studio 설치: 코딩을 하려면 Visual Studio의 작동 버전이 필요합니다.
- .NET 라이브러리용 Aspose.PDF: .NET 라이브러리용 Aspose.PDF를 설치했는지 확인하세요.
  - 다운로드 링크: [.NET용 Aspose.PDF](https://releases.aspose.com/pdf/net/)
- 임시 라이센스: 기능을 테스트해 볼 경우 임시 라이센스가 있으면 유용합니다.
  - 임시 면허: [여기서 구매하세요](https://purchase.aspose.com/temporary-license/)

## 패키지 가져오기

코드 작업을 시작하기 전에 C# 프로젝트에서 다음 네임스페이스를 가져오세요. 이 네임스페이스는 PDF 문서 작업 및 목차(TOC) 생성에 필요한 클래스와 메서드를 제공합니다.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

이제 환경이 준비되고 패키지도 가져왔으니, 프로세스의 각 단계를 자세히 살펴보겠습니다. 코드의 모든 부분을 자세히 설명하여 이해하기 쉽게 설명해 드리겠습니다.

## 1단계: PDF 문서 초기화

가장 먼저 해야 할 일은 새 PDF 문서를 만들고 목차(TOC) 페이지를 추가하는 것입니다.


```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir: 출력 파일이 저장되는 디렉토리입니다.
- Document(): 새로운 PDF 문서를 초기화합니다.
- Pages.Add(): 나중에 TOC를 보관할 새 빈 페이지를 문서에 추가합니다.

## 2단계: TOC 정보 및 제목 설정

다음으로 TOC 정보를 정의하고 TOC 상단에 표시될 제목을 설정합니다.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo: 이 객체는 TOC에 대한 모든 정보를 보관합니다.
- TextFragment: TOC 제목의 텍스트를 나타냅니다. 여기서는 "목차"로 설정합니다.
- 글꼴 스타일: TOC 제목의 크기를 20으로 설정하고 굵게 표시하여 스타일을 지정합니다.
- tocPage.TocInfo: TOC를 표시할 페이지에 TOC 정보를 할당합니다.

## 3단계: TOC에서 페이지 번호 숨기기

이제 재밌는 부분입니다! 여기서는 목차에서 페이지 번호를 숨기도록 설정합니다.

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers: 페이지 번호를 숨기는 마법의 스위치입니다. 설정하세요. `false`그리고 TOC에 페이지 번호가 나타나지 않습니다.
- FormatArrayLength: 이 값을 4로 설정하면 TOC 제목의 4가지 수준에 대한 서식을 정의한다는 것을 나타냅니다.

## 4단계: TOC 형식 사용자 지정

TOC에 더 많은 스타일을 추가하기 위해 이제 다양한 수준의 제목에 대한 서식을 정의하겠습니다.

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray: 이 배열은 TOC 항목의 서식을 제어합니다. 각 인덱스는 다른 제목 수준을 나타냅니다.
- 여백 및 텍스트 스타일: 여백을 설정하고 각 제목 수준에 굵게, 기울임꼴, 밑줄 등의 글꼴 스타일을 적용합니다.

## 5단계: 문서에 제목 추가

마지막으로 TOC에 포함될 실제 제목을 추가해 보겠습니다.

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- 제목 및 텍스트 세그먼트: 목차에 나타날 제목을 나타냅니다. 각 레벨에는 고유한 제목이 있습니다.
- IsAutoSequence: 제목에 자동으로 번호를 매깁니다.
- IsInList: 각 제목이 TOC에 나타나는지 확인합니다.

## 6단계: 문서 저장

모든 것이 설정되면 PDF 문서를 지정된 출력 파일로 저장합니다.

```csharp
doc.Save(outFile);
```

이제 끝입니다! 목차가 포함된 PDF가 성공적으로 생성되었고, 페이지 번호는 숨겨졌습니다!

## 결론

PDF에 목차를 만들고 페이지 번호를 숨기는 것은 까다로울 수 있지만, Aspose.PDF for .NET을 사용하면 아주 간단합니다. 이 단계별 가이드를 따라 목차 형식을 사용자 지정하고, 페이지 번호를 숨기고, 제목에 다양한 스타일을 적용하는 방법을 익혔습니다. 이제 필요에 딱 맞는 전문적인 PDF를 제작할 수 있습니다.

## 자주 묻는 질문

### TOC에서 특정 제목의 페이지 번호를 표시할 수 있나요?
아니요, Aspose.PDF는 전체 목차의 페이지 번호를 숨기거나 표시합니다. 특정 항목의 페이지 번호를 선택적으로 숨길 수는 없습니다.

### TOC에 더 많은 레벨을 추가할 수 있나요?
네, 늘릴 수 있습니다. `FormatArrayLength` TOC 제목의 더 많은 수준을 정의합니다.

### 모든 TOC 항목의 글꼴을 어떻게 변경할 수 있나요?
글꼴을 수정하여 변경할 수 있습니다. `TextState.Font` 각 레벨의 속성 `FormatArray`.

### TOC에 하이퍼링크를 삽입할 수 있나요?
예, 다음을 사용하여 각 TOC 항목을 문서의 특정 섹션에 연결할 수 있습니다. `Heading.TocPage` 재산.

### Aspose.PDF를 사용하려면 라이선스가 필요합니까?
네, 프로덕션 용도로는 유효한 라이선스가 필요합니다. 임시 라이선스를 받으실 수 있습니다. [여기](https://purchase.aspose.com/temporary-license/) 기능을 테스트하려면.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}