---
"description": "Aspose.PDF for .NET을 사용하여 PDF 파일의 텍스트 문단과 빌더를 사용하여 텍스트를 회전하는 방법을 알아보세요."
"linktitle": "PDF 파일에서 텍스트 단락 및 빌더를 사용하여 텍스트 회전"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에서 텍스트 단락 및 빌더를 사용하여 텍스트 회전"
"url": "/ko/net/programming-with-text/rotate-text-using-text-paragraph-and-builder/"
"weight": 410
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에서 텍스트 단락 및 빌더를 사용하여 텍스트 회전

## 소개

동적 PDF 문서를 만드는 것은 데이터, 보고서, 아이디어를 시각적으로 표현하는 흥미로운 방법이 될 수 있습니다. 이를 체계적으로 구현하는 데 도움이 되는 강력한 도구 중 하나는 .NET용 Aspose.PDF입니다. 이 가이드에서는 Aspose.PDF를 사용하여 PDF 파일 내의 텍스트를 회전하는 방법을 살펴보겠습니다. `TextParagraph` 그리고 `TextBuilder` 수업. 주석이 달린 보고서든 시각적으로 매력적인 문서든, PDF 텍스트 편집을 완벽하게 익히는 것은 필수입니다. 텍스트를 문자 그대로 뒤집을 준비가 되셨나요? 자, 시작해 볼까요!

## 필수 조건

텍스트 회전 모험을 시작하기 전에 꼭 준비해야 할 몇 가지 필수 사항이 있습니다.

- C#에 대한 기본 지식: C# 프로그래밍에 익숙하면 코드를 탐색하기가 더 쉬워집니다.
- Visual Studio 설정: 코드를 작성하고 실행하려면 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요.
- Aspose.PDF 라이브러리: 프로젝트에서 Aspose.PDF 라이브러리를 참조해야 합니다. 아직 설치하지 않으셨다면 다음에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/).
- .NET Framework: 사용자 환경이 .NET을 지원하는지 확인하세요. 필요에 따라 .NET Framework나 .NET Core를 사용할 수 있습니다.

이제 기초가 마련되었으니 PDF 작업을 시작하는 데 필요한 패키지를 가져와 보겠습니다.

## 패키지 가져오기

Aspose.PDF for .NET을 사용하려면 올바른 네임스페이스를 가져와야 합니다. C# 파일 맨 위에 다음 using 지시문을 추가하세요.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
```

이러한 패키지는 텍스트와 기타 문서 측면을 효과적으로 조작하는 데 필요한 모든 클래스를 제공합니다.

이제 설정이 완료되었으니, PDF 문서 내에서 텍스트를 회전하는 실제 단계를 살펴보겠습니다. 먼저 문서 초기화부터 저장까지 살펴보겠습니다. 안전띠 매세요!

## 1단계: 문서 개체 초기화

첫 번째 단계는 생성하고 초기화하는 것입니다. `Document` 객체입니다. 이 객체는 텍스트를 추가할 캔버스 역할을 합니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
// 문서 객체 초기화
Document pdfDocument = new Document();
```

그만큼 `Document` 클래스는 PDF의 핵심입니다. PDF 내의 페이지와 콘텐츠를 관리하는 데 도움이 됩니다.

## 2단계: 페이지 추가

다음으로, 텍스트를 배치할 새 페이지를 문서에 추가해 보겠습니다.

```csharp
// 특정 페이지 가져오기
Page pdfPage = (Page)pdfDocument.Pages.Add();
```

여기서 PDF에 새 페이지를 추가합니다. 이 페이지에 텍스트 단락이 들어갈 것입니다.

## 3단계: 텍스트 단락 만들기 및 구성

이제 재미있는 일이 시작됩니다! 여러 개의 `TextParagraph` 객체를 구성하고 위치 및 회전 각도를 포함한 속성을 구성합니다.

```csharp
for (int i = 0; i < 4; i++)
{
    TextParagraph paragraph = new TextParagraph();
    paragraph.Position = new Position(200, 600);
    // 회전 지정
    paragraph.Rotation = i * 90 + 45;
}
```

이 루프에서는 네 개의 문단을 생성하고, 각 문단은 90도씩 회전합니다. 각 문단은 처음에 좌표 (200, 600)에 위치합니다.

## 4단계: 텍스트 조각 만들기

문단을 설정한 후 이제 텍스트를 추가할 차례입니다! `TextFragment` 표시하려는 실제 텍스트를 보관하는 객체입니다.

```csharp
TextFragment textFragment1 = new TextFragment("Paragraph Text");
textFragment1.TextState.FontSize = 12;
textFragment1.TextState.Font = FontRepository.FindFont("TimesNewRoman");
textFragment1.TextState.BackgroundColor = Aspose.Pdf.Color.LightGray;
textFragment1.TextState.ForegroundColor = Aspose.Pdf.Color.Blue;
```

각 조각은 글꼴 크기, 글꼴 유형, 배경색, 전경색 등의 속성을 사용자 지정할 수 있습니다. 여러 텍스트 조각에 대해 이 과정을 반복합니다.

```csharp
TextFragment textFragment2 = new TextFragment("Second line of text");
textFragment2.TextState = ConfigureText("Second line of text");
TextFragment textFragment3 = new TextFragment("And some more text...");
textFragment3.TextState = ConfigureText("And some more text...", true);
```

방법 `ConfigureText` 텍스트 스타일 속성을 캡슐화하여 코드 재사용성과 명확성을 개선하기 위해 만드는 유틸리티 메서드일 수 있습니다.

## 5단계: 문단에 텍스트 조각 추가

다음으로, 문단에 텍스트 조각을 추가합니다. 이렇게 하면 문단에 구조화된 텍스트 흐름이 생성됩니다.

```csharp
paragraph.AppendLine(textFragment1);
paragraph.AppendLine(textFragment2);
paragraph.AppendLine(textFragment3);
```

사용 중 `AppendLine`, 각 텍스트가 문단 내에서 별도의 줄로 수직으로 추가되었는지 확인하세요.

## 6단계: PDF 페이지에 문단 추가

이제 문단이 텍스트로 가득 찼으므로 PDF 페이지에 배치해야 합니다. `TextBuilder` 물체.

```csharp
TextBuilder textBuilder = new TextBuilder(pdfPage);
textBuilder.AppendParagraph(paragraph);
```

마법이 일어나는 곳이 바로 여기입니다! 준비된 문단을 가져와서 `TextBuilder` 이전에 만든 캔버스(PDF 페이지)에 놓습니다.

## 7단계: 문서 저장

마지막으로, 열심히 작업한 결과물을 저장할 시간입니다! 출력 PDF 파일의 디렉터리와 이름을 지정해 주세요.

```csharp
pdfDocument.Save(dataDir + "TextFragmentTests_Rotated4_out.pdf");
```

이 줄에서 다음을 바꾸세요 `dataDir` 원하는 출력 디렉터리 경로를 입력하세요. PDF 파일은 "TextFragmentTests_Rotated4_out.pdf"라는 이름으로 저장됩니다.

## 결론

Aspose.PDF for .NET을 사용하여 PDF에서 텍스트를 회전하는 방법에 대한 자세한 안내가 있습니다! 작업을 관리하기 쉬운 단계로 나누면 어느새 PDF가 여러분의 스타일과 창의성을 보여주는 역동적인 문서로 변신합니다. 보고서 작성, 초대장 제작, 텍스트 배열 실험 등 어떤 작업을 하든 Aspose.PDF는 여러분의 필요에 맞는 유연한 도구를 제공합니다. 더 이상 기다릴 필요 없이 지금 바로 실험해 보고 PDF 문서로 얼마나 창의적인 작업을 할 수 있는지 직접 확인해 보세요!

## 자주 묻는 질문

### 텍스트를 어떤 방향으로든 회전할 수 있나요?
네, 다양한 방향을 구현하기 위해 원하는 회전 각도(90도의 배수)를 지정할 수 있습니다.

### 텍스트 대신 이미지를 추가하려면 어떻게 해야 하나요?
Aspose.PDF를 사용하면 이미지도 조작할 수 있습니다! 다음을 사용하여 이미지를 추가할 수 있습니다. `Image` 비슷한 방식으로 수업을 진행합니다.

### Aspose.PDF for .NET은 무료인가요?
무료 체험판을 제공하지만 계속 사용하려면 라이선스를 구매해야 합니다. [구입](https://purchase.aspose.com/buy) 자세한 내용은 페이지를 참조하세요!

### Aspose.PDF 사용에 대한 지원을 받을 수 있나요?
네, 지원을 받고 질문을 게시할 수 있습니다. [Aspose 포럼](https://forum.aspose.com/c/pdf/10).

### Aspose.PDF에 대한 임시 라이선스를 받으려면 어떻게 해야 하나요?
테스트 목적으로 임시 라이센스를 얻을 수 있습니다. [임시 면허 페이지](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}