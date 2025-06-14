---
"description": "Aspose.PDF for .NET을 사용하여 PDF 파일에 JavaScript를 추가하는 방법을 알아보세요. 문서 및 페이지 수준 스크립팅을 위한 코드 튜토리얼이 포함된 단계별 가이드입니다."
"linktitle": "Java Script PDF 파일 추가"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에 자바 스크립트 추가"
"url": "/ko/net/programming-with-document/addjavascripttopage/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에 자바 스크립트 추가

## 소개

팝업 알림이나 자동 인쇄 기능과 같은 인터랙티브 요소를 PDF에 추가하는 방법을 궁금해하신 적 있으신가요? 다행히 가능합니다! Aspose.PDF for .NET을 사용하면 PDF 문서에 JavaScript를 손쉽게 추가할 수 있습니다. 작업을 자동화하든 동적인 사용자 경험을 구축하든, PDF에 JavaScript를 임베드하면 파일에 더욱 향상된 기능을 제공할 수 있습니다.

## 필수 조건

코딩 부분으로 넘어가기 전에 먼저 설정해야 할 몇 가지 사항이 있습니다.

- .NET용 Aspose.PDF: 라이브러리를 다운로드하세요 [Aspose 릴리스](https://releases.aspose.com/pdf/net/) 또는 얻을 [무료 체험](https://releases.aspose.com/).
- 개발 환경: Visual Studio와 같은 .NET 호환 IDE.
- 기본 C# 지식: 이 가이드에서는 독자가 기본 C# 구문에 익숙하다고 가정합니다.
- 임시 면허(선택 사항): 다음을 얻을 수 있습니다. [임시 면허](https://purchase.aspose.com/temporary-license/) 개발 중에 제한을 피하고 싶다면.

## 패키지 가져오기

코드 작성을 시작하기 전에 Aspose.PDF 라이브러리에서 필요한 네임스페이스를 가져와야 합니다. 이 네임스페이스를 사용하면 PDF를 쉽게 조작하고 JavaScript 작업을 추가할 수 있습니다.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

이제 올바른 네임스페이스를 가져왔으므로 코딩을 시작할 준비가 되었습니다.

## 1단계: 기존 PDF 로드

가장 먼저 해야 할 일은 JavaScript를 추가할 PDF 문서를 로드하는 것입니다. 이 단계는 모든 추가 수정 작업을 위한 토대를 마련하는 것입니다. 예를 들어, PDF 문서를 열면 자동으로 인쇄되는 것처럼 동적 기능을 추가하고 싶은 경우를 생각해 보세요.

PDF 파일을 로드하는 방법은 다음과 같습니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 기존 PDF 파일 로드
Document doc = new Document(dataDir + "input.pdf");
```

이 코드 조각에서는 다음을 사용합니다. `Document` 지정된 디렉터리에서 기존 PDF 파일을 로드하는 클래스입니다. `"YOUR DOCUMENT DIRECTORY"` PDF 파일의 실제 경로를 포함합니다.

## 2단계: 문서 수준에서 JavaScript 추가

이제 문서가 열릴 때 실행되는 JavaScript를 추가해 보겠습니다. 이 예제에서는 사용자가 PDF 파일을 열자마자 인쇄 대화 상자를 여는 스크립트를 작성해 보겠습니다.

문서 수준 JavaScript는 전체 PDF에 적용하려는 작업에 적합합니다. 문서에 대한 전역 규칙을 설정하는 것과 같습니다.

코드는 다음과 같습니다.

```csharp
// 문서 수준에서 JavaScript 추가
// 원하는 JavaScript 문장으로 JavascriptAction을 인스턴스화합니다.
JavascriptAction javaScript = new JavascriptAction("this.print({bUI:true,bSilent:false,bShrinkToFit:true});");

// Document의 OpenAction에 JavascriptAction 객체를 할당합니다.
doc.OpenAction = javaScript;
```

이 단계에서는 다음을 생성합니다. `JavascriptAction` 문서가 열릴 때 인쇄 대화 상자를 여는 JavaScript 함수를 정의하는 객체입니다. `doc.OpenAction` 그러면 속성에 이 JavaScript 작업이 할당됩니다.

## 3단계: 페이지 수준에서 JavaScript 추가

모든 동작이 문서 전체에 영향을 미칠 필요는 없습니다. 특정 페이지를 열거나 닫을 때 특정 동작이 발생하도록 설정해야 할 때가 있습니다. 여기서는 특정 페이지(예: 2페이지)를 열거나 닫을 때 실행되는 JavaScript 동작을 설정해 보겠습니다.

페이지 수준 JavaScript는 특정 대상과의 상호작용에 유용합니다. 사용자가 페이지로 이동할 때 메시지를 표시하는 것부터 양식 필드 자동 채우기와 같은 사용자 지정 작업까지 다양합니다.

방법은 다음과 같습니다.

```csharp
// 페이지 수준에서 JavaScript 추가
doc.Pages[2].Actions.OnOpen = new JavascriptAction("app.alert('Page 2 opened')");
doc.Pages[2].Actions.OnClose = new JavascriptAction("app.alert('Page 2 closed')");
```

이 코드 조각에서는 두 가지 JavaScript 동작을 추가합니다.
1. OnOpen 작업: 사용자가 2페이지를 열면 "2페이지가 열렸습니다"라는 경고를 표시합니다.
2. OnClose 작업: 사용자가 2페이지에서 벗어나면 "2페이지가 닫혔습니다"라는 경고를 표시합니다.

이렇게 하면 PDF에 상호작용 기능이 추가됩니다. 사용자가 여러 페이지에서 일련의 단계를 거치도록 안내하고, 페이지에 들어가거나 나갈 때 알림이 표시되는 것을 상상해 보세요.

## 4단계: PDF 문서 저장

이제 문서와 특정 페이지 모두에 JavaScript를 추가했습니다. 마지막 단계는 수정된 PDF를 원하는 위치에 저장하는 것입니다. 이 단계는 간단하지만 매우 중요합니다. 작업 내용을 저장하는 것을 잊지 마세요!

코드는 다음과 같습니다.

```csharp
// 출력 파일 경로를 지정하세요
dataDir = dataDir + "JavaScript-Added_out.pdf";

// 업데이트된 PDF 문서를 저장합니다.
doc.Save(dataDir);

Console.WriteLine("\nJavaScript added successfully to the PDF.\nFile saved at " + dataDir);
```

이 스니펫에서는 추가된 JavaScript를 사용하여 업데이트된 문서를 새 파일 이름으로 저장합니다. `"JavaScript-Added_out.pdf"`이렇게 하면 원본 파일을 덮어쓰지 않고 작업할 수 있는 백업을 얻을 수 있습니다.

## 결론

Aspose.PDF for .NET을 사용하여 PDF 파일에 JavaScript를 추가하면 인터랙티브하고 동적인 PDF를 만들 수 있는 강력한 방법이 됩니다. 인쇄와 같은 작업을 자동화하거나 사용자 지정 알림을 만들 때, PDF에 JavaScript를 삽입하면 문서의 흥미와 기능이 더욱 향상됩니다.

## 자주 묻는 질문

### PDF의 여러 페이지에 여러 개의 JavaScript 동작을 추가할 수 있나요?
네, 개별 페이지나 전체 문서에 다른 JavaScript 동작을 할당할 수 있습니다.

### PDF를 추가한 후 JavaScript를 제거할 수 있나요?
예, 기존 JavaScript 작업을 지우면 제거하거나 수정할 수 있습니다. `Actions` 문서나 페이지의 속성.

### PDF에서 어떤 종류의 JavaScript 함수를 사용할 수 있나요?
인쇄, 알림, 양식 조작 등 Adobe Acrobat의 JavaScript 엔진이 지원하는 모든 JavaScript를 사용할 수 있습니다.

### JavaScript는 모든 PDF 뷰어에서 작동합니까?
대부분의 JavaScript 동작은 Adobe Acrobat처럼 대화형 PDF를 지원하는 PDF 뷰어에서 작동합니다. 하지만 일부 기본 PDF 리더는 JavaScript를 지원하지 않을 수 있습니다.

### PDF에서 사용자 입력을 기반으로 JavaScript 작업을 트리거할 수 있나요?
네, JavaScript를 양식 필드에 바인딩하여 사용자 입력에 따라 작업을 트리거할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}