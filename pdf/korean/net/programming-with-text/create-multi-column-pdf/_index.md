---
"description": "Aspose.PDF for .NET을 사용하여 여러 열로 구성된 PDF를 만드는 방법을 알아보세요. 코드 예제와 자세한 설명이 포함된 단계별 가이드입니다. 전문가에게 적합합니다."
"linktitle": "다중 열 PDF 만들기"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "다중 열 PDF 만들기"
"url": "/ko/net/programming-with-text/create-multi-column-pdf/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 다중 열 PDF 만들기

## 소개

여러 열로 구성된 PDF를 만들면 텍스트를 더욱 체계적이고 읽기 쉬운 형식으로 표현할 수 있습니다. 보고서, 기사 또는 출판물 레이아웃을 제작할 때 여러 열 구조는 콘텐츠를 더욱 매력적으로 만들 수 있습니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 여러 열로 구성된 PDF를 만드는 방법을 살펴보겠습니다. 걱정하지 마세요. 모든 과정을 간단한 단계로 나누어 설명해 드리므로 Aspose.PDF를 처음 사용하는 분도 쉽게 따라 할 수 있습니다.

## 필수 조건

코드로 들어가기 전에, 원활하게 따라가기 위해 꼭 필요한 몇 가지 사항이 있습니다.

1. Aspose.PDF for .NET: 이 라이브러리가 설치되어 있어야 합니다. 다음에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/).
2. 개발 환경: C# 코드를 작성하고 실행하기 위해 Visual Studio와 같은 원하는 IDE를 설정합니다.
3. .NET Framework: 호환되는 버전의 .NET이 설치되어 있는지 확인하세요.
4. C#에 대한 기본적인 이해: C# 구문에 익숙하면 도움이 되지만, 각 단계를 자세히 설명하겠습니다.
5. 임시 라이선스: Aspose.PDF는 워터마크나 제한을 피하기 위해 라이선스가 필요합니다. [임시 면허](https://purchase.aspose.com/temporary-license/) 필요한 경우.

## 패키지 가져오기

코딩을 시작하기 전에 Aspose.PDF와 상호 작용하는 데 필요한 네임스페이스를 가져와야 합니다. 가져와야 할 항목은 다음과 같습니다.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

이러한 네임스페이스는 PDF 생성, 도형 그리기, 텍스트 서식 처리에 필요한 클래스에 대한 액세스를 제공합니다.

여러 열로 구성된 PDF를 만드는 과정을 간단하고 관리하기 쉬운 단계로 나누어 보겠습니다.

## 1단계: 문서 설정

시작하려면 새 PDF 문서를 만들어야 합니다. 여기에는 여백을 정의하고 콘텐츠를 넣을 페이지를 추가하는 작업이 포함됩니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 새 PDF 문서 만들기
Document doc = new Document();

// PDF 파일의 여백을 설정합니다
doc.PageInfo.Margin.Left = 40;
doc.PageInfo.Margin.Right = 40;

// 문서에 페이지 추가
Page page = doc.Pages.Add();
```

여기서 우리는 다음을 생성했습니다. `Document` 객체를 만들고 왼쪽과 오른쪽 여백을 40단위로 설정했습니다. 그런 다음 이 문서에 다중 열 레이아웃을 포함할 새 페이지를 추가했습니다.

## 2단계: 섹션을 구분하기 위한 선 추가

다음으로, 시각적 구분을 위해 페이지에 수평선을 추가해 보겠습니다. 이렇게 하면 깔끔하고 전문적인 느낌을 줄 수 있습니다.

```csharp
// 선을 유지하기 위한 그래프 객체를 생성합니다.
Aspose.Pdf.Drawing.Graph graph1 = new Aspose.Pdf.Drawing.Graph(500.0, 2.0);

// 페이지의 문단 컬렉션에 줄을 추가합니다.
page.Paragraphs.Add(graph1);

// 선의 좌표를 정의합니다
float[] posArr = new float[] { 1, 2, 500, 2 };

// 선을 만들어 그래프에 추가하세요
Aspose.Pdf.Drawing.Line l1 = new Aspose.Pdf.Drawing.Line(posArr);
graph1.Shapes.Add(l1);
```

여기서 우리는 다음을 사용하여 수평선을 만들고 있습니다. `Graph` 그리고 `Line` 클래스. 이 줄은 페이지에 추가됩니다. `Paragraphs` 모든 시각적 요소를 담고 있는 컬렉션입니다.

## 3단계: 서식이 적용된 HTML 텍스트 추가

다음으로, PDF에서 텍스트를 동적으로 서식 지정하는 방법을 보여주기 위해 HTML 태그가 포함된 텍스트를 삽입해 보겠습니다.

```csharp
// HTML 콘텐츠로 문자열을 만듭니다.
string s = "<font face=\"Times New Roman\" size=4>" +
           "<strong> How to Steer Clear of Money Scams </strong>" +
           "</font>";

// 서식이 지정된 텍스트로 새 HtmlFragment를 만듭니다.
HtmlFragment heading_text = new HtmlFragment(s);

// 페이지에 HTML 텍스트를 추가합니다
page.Paragraphs.Add(heading_text);
```

를 사용하여 `HtmlFragment` 클래스에서는 글꼴 크기, 스타일, 굵은 글씨 등의 HTML 태그가 포함된 서식 있는 텍스트를 추가할 수 있습니다. 이는 PDF 콘텐츠의 모양을 개선하는 데 유용합니다.

## 4단계: 다중 열 레이아웃 만들기

이제 다중 열 레이아웃을 만들어 보겠습니다. 마법 같은 일이 바로 여기서 일어납니다. 원하는 열의 개수와 너비를 지정할 수 있습니다.

```csharp
// 기둥을 고정할 떠 있는 상자를 만듭니다.
Aspose.Pdf.FloatingBox box = new Aspose.Pdf.FloatingBox();

// 열의 개수와 열 사이의 간격을 설정합니다.
box.ColumnInfo.ColumnCount = 2;
box.ColumnInfo.ColumnSpacing = "5";
box.ColumnInfo.ColumnWidths = "105 105";

// 페이지에 상자 추가
page.Paragraphs.Add(box);
```

여기서는 두 개의 열을 포함하는 떠다니는 상자를 만듭니다. 열 사이의 간격을 설정하고 각 열의 너비를 105 단위로 지정합니다. 이렇게 하면 PDF 내에서 원하는 열 레이아웃을 만들 수 있습니다.

## 5단계: 열에 텍스트 추가

이제 열에 텍스트 콘텐츠를 채워 보겠습니다. 다양한 텍스트를 추가할 수 있습니다. `TextFragment` 각 열에 객체를 추가합니다.

```csharp
// 첫 번째 텍스트 조각을 만들고 서식을 지정합니다.
TextFragment text1 = new TextFragment("By A Googler (The Official Google Blog)");
text1.TextState.FontSize = 8;
text1.TextState.FontStyle = FontStyles.Italic;
box.Paragraphs.Add(text1);

// 구분을 위해 또 다른 줄을 추가합니다.
Aspose.Pdf.Drawing.Graph graph2 = new Aspose.Pdf.Drawing.Graph(50.0, 10.0);
float[] posArr2 = new float[] { 1, 10, 100, 10 };
Aspose.Pdf.Drawing.Line l2 = new Aspose.Pdf.Drawing.Line(posArr2);
graph2.Shapes.Add(l2);
box.Paragraphs.Add(graph2);

// 두 번째 텍스트 조각을 만들고 추가합니다.
TextFragment text2 = new TextFragment("Lorem ipsum dolor sit amet, consectetur adipiscing elit...");
box.Paragraphs.Add(text2);
```

우리는 추가합니다 `TextFragment` 떠 있는 상자로 이어지고, 그 뒤에 또 다른 수평선이 이어진다. 두 번째 `TextFragment` 두 번째 열을 채울 더 많은 텍스트가 포함되어 있습니다. 이러한 조각을 사용하면 다양한 서식 옵션을 사용하여 PDF에 다양한 텍스트 요소를 추가할 수 있습니다.

## 6단계: PDF 저장

모든 콘텐츠를 추가한 후 마지막 단계는 문서를 PDF 파일로 저장하는 것입니다.

```csharp
// PDF의 출력 경로를 정의합니다.
dataDir = dataDir + "CreateMultiColumnPdf_out.pdf";

// PDF 문서를 저장합니다
doc.Save(dataDir);

// 출력 성공 메시지
Console.WriteLine("\nMulti-column PDF file created successfully.\nFile saved at " + dataDir);
```

이 블록은 PDF 파일을 지정된 디렉터리에 저장하고 콘솔에 성공 메시지를 출력합니다. 이제 PDF 파일을 볼 준비가 되었습니다!

## 결론

간단한 단계를 따라 Aspose.PDF for .NET을 사용하여 전문가 수준의 여러 열로 구성된 PDF를 쉽게 만들 수 있습니다. 보고서, 기사, 뉴스레터 등 어떤 문서든 이 기술을 사용하면 콘텐츠를 시각적으로 매력적인 형식으로 정리할 수 있습니다. Aspose.PDF는 여백, 레이아웃, 텍스트 서식, 도형 그리기 등 PDF를 사용자 정의할 수 있는 강력한 도구를 제공합니다. 이제 직접 사용해 보고 PDF 제작 실력을 한 단계 높여 보세요!

## 자주 묻는 질문

### PDF에 두 개 이상의 열을 만들 수 있나요?
네, 필요한 만큼 많은 열을 만들 수 있습니다. 간단히 조정하세요. `ColumnCount` 원하는 열 수에 맞게 속성을 변경합니다.

### 각 열의 너비를 어떻게 변경합니까?
수정할 수 있습니다 `ColumnWidths` 각 열에 다른 너비를 지정하는 속성입니다. 이 속성은 공백으로 구분된 문자열 값을 허용합니다.

### 열에 이미지를 추가할 수 있나요?
물론입니다! 다음을 사용하여 이미지를 추가할 수 있습니다. `Image` 클래스를 만들고 PDF의 플로팅 상자나 다른 레이아웃 요소에 포함시킵니다.

### HTML 태그를 사용하여 열의 텍스트 스타일을 지정할 수 있나요?
네, HTML 태그를 사용할 수 있습니다. `HtmlFragment` 텍스트 스타일을 지정할 수 있는 개체입니다. 여기에는 글꼴, 크기, 색상 등이 포함됩니다.

### 동일한 열 레이아웃으로 페이지를 더 추가하려면 어떻게 해야 하나요?
추가 페이지를 사용하여 추가할 수 있습니다. `doc.Pages.Add()` 그리고 각 페이지에 열과 내용을 추가하는 과정을 반복합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}