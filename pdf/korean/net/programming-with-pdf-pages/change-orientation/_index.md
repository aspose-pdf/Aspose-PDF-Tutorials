---
"description": "Aspose.PDF for .NET을 사용하여 PDF의 페이지 방향을 변경하는 단계별 가이드입니다. 쉽게 따라 하고 프로젝트에 구현할 수 있습니다."
"linktitle": "방향 전환"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "방향 전환"
"url": "/ko/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 방향 전환

## 소개

PDF 파일의 페이지 방향이 어긋나서 곤란했던 적이 있으신가요? 스캔하거나 잘못 만든 문서 때문에 페이지를 회전해야 하는 경우가 있을 수 있습니다. 다행히 Aspose.PDF for .NET은 페이지 방향 변경을 포함하여 상상할 수 있는 거의 모든 방식으로 PDF 파일을 조작할 수 있는 쉽고 강력한 방법을 제공합니다. 세로 모드에서 가로 모드로, 또는 그 반대로 전환하려는 경우, 이 가이드가 단계별로 안내해 드립니다.

이제 PDF 페이지를 쉽게 회전할 준비가 되셨나요? 시작해볼까요!

## 필수 조건

PDF에서 페이지 방향을 변경하는 방법에 대한 자세한 내용을 살펴보기 전에 먼저 필요한 사항을 간략히 살펴보겠습니다.

- .NET용 Aspose.PDF: .NET용 Aspose.PDF 라이브러리가 설치되어 있는지 확인하세요. 설치되어 있지 않은 경우 [여기서 다운로드하세요](https://releases.aspose.com/pdf/net/).
- .NET 개발 환경: Visual Studio, JetBrains Rider 또는 선호하는 IDE를 사용하여 .NET 작업을 수행할 수 있습니다.
- C#에 대한 기본 지식: 이 가이드는 간단하지만, C#에 대한 기본적인 이해가 있다면 더 쉽게 따라갈 수 있습니다.
- PDF 파일: 아래 예시에서는 여러 페이지로 구성된 PDF 파일이 있다고 가정합니다. PDF 파일이 없다면 샘플 PDF 파일을 만들거나 다운로드하여 작업하세요.

또한, 방금 시작했다면 Aspose.PDF를 사용해 볼 수 있습니다. [무료 임시 면허](https://purchase.aspose.com/temporary-license/) 결정하기 전에 [정식 버전을 구매하세요](https://purchase.aspose.com/buy).

## 네임스페이스 가져오기

PDF의 페이지 방향을 조정하려면 먼저 C# 프로젝트에 필요한 네임스페이스를 가져와야 합니다. 다음 사항이 있는지 확인하세요.

```csharp
using System.IO;
using Aspose.Pdf;
```

이제 가져온 내용을 바탕으로 튜토리얼의 주요 부분으로 넘어가겠습니다.

## 1단계: PDF 문서 로드

가장 먼저 해야 할 일은 수정하려는 PDF 파일을 불러오는 것입니다. `Document` Aspose.PDF 네임스페이스의 클래스를 사용하여 PDF를 엽니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

이 줄은 지정한 디렉터리에서 PDF를 로드합니다. 다음을 반드시 바꾸세요. `"YOUR DOCUMENT DIRECTORY"` 파일의 실제 경로와 함께 `"input.pdf"` 방향을 변경하려는 PDF입니다.

## 2단계: 각 페이지 반복

이제 문서가 로드되었으므로 PDF의 각 페이지를 반복해 보겠습니다. `foreach` 각 페이지를 반복해서 살펴보면서 모든 페이지에 방향 변경을 적용할 수 있습니다.

```csharp
foreach (Page page in doc.Pages)
{
    // 각 페이지를 조작하세요
}
```

이 루프는 문서 내의 모든 페이지를 반복합니다.

## 3단계: 페이지의 미디어박스 가져오기

PDF의 각 페이지에는 다음이 있습니다. `MediaBox` 페이지의 경계를 정의합니다. 현재 방향을 확인하고 수정하려면 이 경계에 접근해야 합니다.

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

그만큼 `MediaBox` 페이지의 너비, 높이, 위치 등 크기를 알려줍니다.

## 4단계: 너비와 높이 바꾸기

페이지 방향을 세로에서 가로로 또는 가로에서 세로로 변경하려면 너비와 높이 값을 바꾸기만 하면 됩니다. 이 단계를 통해 페이지의 크기가 조정됩니다.

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

이 코드는 높이와 너비를 바꾸고 왼쪽 하단 모서리를 다시 배치합니다.`LLY`) 회전 후 내용이 깔끔하게 맞춰지도록 합니다.

## 5단계: MediaBox 및 CropBox 업데이트

이제 새로운 높이와 너비가 있으므로 페이지에 변경 사항을 적용해 보겠습니다. `MediaBox` 그리고 `CropBox`. 그 `CropBox` 원본 문서에 세트가 하나 있는 경우 전체 페이지가 올바르게 표시되는지 확인하는 것이 필수적입니다.

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

이 단계에서는 방금 계산한 새로운 치수를 기준으로 페이지 크기를 조정합니다.

## 6단계: 페이지 회전

마지막으로, 페이지의 회전 각도를 설정합니다. Aspose.PDF를 사용하면 이 과정이 매우 간단합니다. 세로 모드에서 가로 모드로, 또는 가로 모드에서 세로 모드로 전환하려면 페이지를 90도 회전할 수 있습니다.

```csharp
page.Rotate = Rotation.on90;
```

이 코드는 페이지를 90도 회전시켜 원하는 방향으로 뒤집습니다.

## 7단계: 출력 PDF 저장

모든 페이지에 방향 변경을 적용한 후, 수정된 문서를 새 파일에 저장합니다. 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

새 파일 이름을 제공해야 합니다(이 경우, `ChangeOrientation_out.pdf`)을 눌러 출력을 저장합니다. 이렇게 하면 원본 파일을 덮어쓰지 않습니다.

### 결론

자, 이제 끝났습니다! Aspose.PDF for .NET을 사용하여 PDF 파일의 페이지 방향을 변경하는 것은 문서를 로드하고, 페이지를 순환하며, MediaBox를 조정하고, 업데이트된 파일을 저장하는 것만큼 간단합니다. 스캔 품질이 좋지 않은 문서를 다루거나 서식에 맞게 페이지를 회전해야 하는 경우, 이 단계별 가이드가 도움이 될 것입니다.

## 자주 묻는 질문

### PDF의 모든 페이지 대신 특정 페이지만 회전할 수 있나요?  
네, 모든 페이지를 반복하는 대신 인덱스를 사용하여 특정 페이지를 대상으로 루프를 수정할 수 있습니다.

### 무엇입니까? `MediaBox`?  
그만큼 `MediaBox` PDF 파일에서 페이지의 크기와 모양을 정의합니다. 페이지 내용이 배치되는 위치입니다.

### .NET용 Aspose.PDF는 다른 파일 형식에서도 작동합니까?  
네, Aspose.PDF는 HTML, XML, XPS 등 다양한 파일 형식을 처리할 수 있습니다.

### .NET용 Aspose.PDF의 무료 버전이 있나요?  
네, 시작할 수 있습니다. [무료 체험](https://releases.aspose.com/) 또는 요청 [임시 면허](https://purchase.aspose.com/temporary-license/).

### 변경 사항을 저장한 후 취소할 수 있나요?  
문서를 저장하면 변경 사항이 영구적으로 적용됩니다. 사본을 만들거나 원본 파일을 백업해 두세요.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}