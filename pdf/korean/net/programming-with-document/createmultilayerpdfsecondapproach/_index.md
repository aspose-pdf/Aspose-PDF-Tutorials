---
"description": "Aspose.PDF for .NET을 사용하여 다층 PDF를 만드는 방법을 알아보세요. 단계별 가이드를 따라 PDF 파일에 텍스트, 이미지, 레이어를 손쉽게 추가하세요."
"linktitle": "다층 PDF 파일 두 번째 방법 만들기"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "다층 PDF 파일 두 번째 방법 만들기"
"url": "/ko/net/programming-with-document/createmultilayerpdfsecondapproach/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 다층 PDF 파일 두 번째 방법 만들기

## 소개

오늘날 디지털 문서 시대에는 전문적이고 레이어가 적용된 PDF를 제작하는 능력이 매우 중요합니다. 워터마크를 추가하거나, 이미지 위에 텍스트를 삽입하거나, 복잡한 레이아웃을 만들 때 PDF 레이어를 완벽하게 제어할 수 있는 강력한 솔루션이 필요합니다. Aspose.PDF for .NET은 이러한 과정을 원활하고 간편하게 만들어 주는 강력한 도구입니다.

## 필수 조건

시작하기에 앞서 다음 사항이 있는지 확인하세요.

- .NET 라이브러리용 Aspose.PDF: 아직 설치하지 않았다면 다운로드하세요. [최신 버전은 여기](https://releases.aspose.com/pdf/net/).
- .NET 개발 환경: Visual Studio나 .NET을 지원하는 다른 IDE를 사용할 수 있습니다.
- C#에 대한 기본적인 이해: 이 내용을 따라가려면 C# 프로그래밍에 익숙해야 합니다.
- 테스트 이미지 파일: 이 튜토리얼에서 사용하려면 이미지 파일(예: "test_image.png")이 필요합니다.

아직 .NET용 Aspose.PDF 라이선스가 없으면 다음을 요청할 수 있습니다. [임시 면허](https://purchase.aspose.com/temporary-license/)추가 리소스는 다음을 확인하세요. [선적 서류 비치](https://reference.aspose.com/pdf/net/) 또는 연락하세요 [지원하다](https://forum.aspose.com/c/pdf/10).

## 필요한 패키지 가져오기

다중 레이어 PDF 생성을 시작하려면 적절한 네임스페이스를 가져와야 합니다. 이러한 패키지는 다음과 같은 모든 필수 클래스를 사용할 수 있도록 합니다. `Document`, `Page`, `TextFragment`, 그리고 `FloatingBox`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Drawing;
```

이제 전제 조건이 해결되었으므로 주요 부분인 다층 PDF 파일을 만드는 단계로 넘어가겠습니다.

이 가이드는 각 단계를 자세하고 초보자 친화적으로 안내해 드립니다. 자, 이제 팔을 걷어붙이고 시작해 볼까요!

## 1단계: 문서 초기화 및 경로 설정

가장 먼저 필요한 것은 PDF 문서 객체와 최종 PDF를 저장할 위치를 참조하는 방법입니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

이 스니펫에서 우리는 다음을 생성했습니다. `Document` PDF를 나타내는 객체입니다. `dataDir` 변수는 생성된 PDF 파일을 저장할 디렉토리로 설정해야 합니다.

## 2단계: PDF 문서에 페이지 추가

모든 PDF 문서는 하나 이상의 페이지로 구성됩니다. 문서에 페이지를 추가해 보겠습니다.

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

이 코드는 문서에 빈 페이지를 추가합니다. 꽤 간단하죠? 이제 이 페이지에 레이어를 추가하는 단계로 넘어가 보겠습니다.

## 3단계: 텍스트 조각 만들기 및 사용자 지정

다음으로, 텍스트 조각을 만들어 보겠습니다. 이는 색상, 크기, 위치를 조정할 수 있는 텍스트 블록입니다.

```csharp
Aspose.Pdf.Text.TextFragment t1 = new Aspose.Pdf.Text.TextFragment("paragraph 3 segment");
t1.TextState.ForegroundColor = Color.Red;
t1.IsInLineParagraph = true;
t1.TextState.FontSize = 12;
```

무슨 일이 일어나고 있는지 알려드리겠습니다.
- 그만큼 `TextFragment` 물체 `t1` "문단 3 세그먼트"라는 텍스트로 초기화됩니다.
- 우리는 다음을 사용하여 텍스트 색상을 빨간색으로 변경합니다. `ForegroundColor` 재산.
- 텍스트 크기는 12포인트로 설정되고 문단 내에서 인라인으로 배치됩니다. `IsInLineParagraph`.

## 4단계: FloatingBox에 텍스트 조각 추가

이제 텍스트 조각이 생겼으니 PDF에 넣어야 합니다. 페이지에 직접 추가하는 대신, `FloatingBox` 구체적인 위치를 지정하기 위해서입니다.

```csharp
Aspose.Pdf.FloatingBox TextFloatingBox1 = new Aspose.Pdf.FloatingBox(117, 21);
TextFloatingBox1.ZIndex = 1;
TextFloatingBox1.Left = -4;
TextFloatingBox1.Top = -4;
page.Paragraphs.Add(TextFloatingBox1);
TextFloatingBox1.Paragraphs.Add(t1);
```

이것을 자세히 살펴보겠습니다.
- 우리는 만듭니다 `FloatingBox` 그리고 크기(117x21)를 정의합니다.
- 그만큼 `ZIndex` 속성이 1로 설정되어 있으므로 맨 아래 레이어에 배치됩니다.
- 그만큼 `Left` 그리고 `Top` 속성은 페이지에서 상자의 정확한 위치를 정의합니다.
- 마지막으로 텍스트 조각 `t1` 떠 있는 상자 안에 추가된 후, 이 상자가 페이지에 추가됩니다.

## 5단계: 다른 FloatingBox에 이미지 삽입

다음으로 PDF에 이미지를 추가하겠습니다. 텍스트와 마찬가지로 이미지를 PDF 파일 안에 배치합니다. `FloatingBox`.

```csharp
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
image1.File = dataDir + "test_image.png";
Aspose.Pdf.FloatingBox ImageFloatingBox = new Aspose.Pdf.FloatingBox(117, 21);
ImageFloatingBox.Left = -4;
ImageFloatingBox.Top = -4;
ImageFloatingBox.ZIndex = 2;
ImageFloatingBox.Paragraphs.Add(image1);
page.Paragraphs.Add(ImageFloatingBox);
```

세부 내용은 다음과 같습니다.
- 우리는 만듭니다 `Image` 객체를 만들고 이미지 파일의 경로를 지정합니다.
- 새로운 `FloatingBox` 텍스트가 떠 있는 상자와 동일한 크기로 이미지에 맞게 만들어졌습니다.
- 이미지 플로팅 상자는 텍스트 플로팅 상자 위에 겹쳐서 배치됩니다. `ZIndex` 2까지.
- 그만큼 `Left` 그리고 `Top` 속성은 이미지를 원하는 위치에 정확하게 배치합니다.
- 이미지는 떠 있는 상자에 추가되고, 그 상자는 페이지에 추가됩니다.

## 6단계: PDF 문서 저장

마지막으로 새로 만든 다층 PDF를 지정된 디렉토리에 저장합니다.

```csharp
doc.Save(dataDir + @"Multilayer-2ndApproach_out.pdf");
```

이 줄은 지정한 디렉터리에 "Multilayer-2ndApproach_out.pdf"라는 이름의 PDF 파일을 저장합니다. 축하합니다! Aspose.PDF for .NET을 사용하여 다층 PDF를 성공적으로 생성했습니다!

## 결론

Aspose.PDF for .NET을 사용하면 다층 PDF 파일을 유연하면서도 강력하게 만들 수 있습니다. 텍스트, 이미지 또는 기타 요소를 오버레이하려는 경우 이 방법을 사용하면 문서의 구조와 표현 방식을 완벽하게 제어할 수 있습니다.

## 자주 묻는 질문

### Aspose.PDF for .NET을 사용하여 여러 페이지로 구성된 PDF를 만들 수 있나요?  
네, 전화로 원하는 만큼 페이지를 추가할 수 있습니다. `doc.Pages.Add()` 각 페이지마다.

### PDF에 도형이나 주석과 같은 요소를 더 많이 추가하려면 어떻게 해야 하나요?  
사용할 수 있습니다 `FloatingBox` 모양, 주석, 표 등 모든 유형의 콘텐츠에 사용할 수 있습니다.

### Aspose.PDF for .NET에서는 어떤 이미지 형식을 지원합니까?  
Aspose.PDF는 PNG, JPEG, GIF, BMP 등 다양한 이미지 형식을 지원합니다.

### PDF에서 요소의 불투명도를 변경할 수 있나요?  
예, 불투명도를 조정하여 수정할 수 있습니다. `Alpha` 의 구성 요소 `Color` 물체.

### PDF에서 요소를 다른 위치로 이동하려면 어떻게 해야 하나요?  
조정할 수 있습니다 `Left` 그리고 `Top` 의 속성 `FloatingBox` 모든 요소의 위치를 변경합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}