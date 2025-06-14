---
"description": "Aspose.PDF for .NET을 사용하여 PDF 문서에서 이미지 배치를 추출하고 조작하는 방법을 알아보세요. 예제와 코드 조각이 포함된 단계별 가이드입니다."
"linktitle": "이미지 배치"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "이미지 배치"
"url": "/ko/net/programming-with-images/image-placements/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 이미지 배치

## 소개

PDF 파일에서 이미지 작업은 까다로울 수 있지만, Aspose.PDF for .NET을 사용하면 힘들이지 않고도 이미지 속성을 쉽게 조작하고 추출할 수 있습니다. 이미지 크기를 가져오거나, 추출하거나, 해상도와 같은 다른 속성을 가져오는 등 어떤 작업을 하든 Aspose.PDF에는 필요한 도구가 있습니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF 문서에서 이미지 배치를 추출하는 방법을 단계별로 안내합니다. 패키지 가져오기부터 너비, 높이, 해상도와 같은 이미지 속성 가져오기까지 모든 것을 다룹니다.

## 필수 조건

튜토리얼을 시작하기 전에 몇 가지 준비해야 할 사항이 있습니다. 간단한 체크리스트는 다음과 같습니다.

1. Aspose.PDF for .NET: Aspose.PDF for .NET 라이브러리가 설치되어 있는지 확인하세요. 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/net/).
2. 개발 환경: 컴퓨터에 Visual Studio나 기타 .NET 지원 IDE가 설치되어 있어야 합니다.
3. PDF 문서: 이미지가 포함된 샘플 PDF 문서를 준비하세요. 이 예시에서는 다음 이름의 파일을 사용하겠습니다. `ImagePlacement.pdf`.
4. C# 기본 지식: 이 가이드는 초보자에게 친화적이지만, C#에 대한 기본 지식이 있으면 코드 조각을 더 잘 이해하는 데 도움이 됩니다.

## 패키지 가져오기

코드의 세부적인 내용을 살펴보기 전에 먼저 필요한 네임스페이스를 임포트해야 합니다. 이 패키지들은 Aspose.PDF for .NET에서 PDF 문서 작업과 이미지 조작에 필수적입니다.

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using System.Drawing;
```

이 패키지를 사용하면 PDF 작업이 가능합니다.`Aspose.Pdf`), 이미지 배치를 조작합니다(`Aspose.Pdf.ImagePlacement`), 이미지 스트림과 그래픽을 처리합니다.`System.Drawing` 그리고 `System.IO`).

이제 필수 구성 요소와 패키지가 준비되었으니, 튜토리얼의 각 부분을 간단하고 따라하기 쉬운 가이드로 나누어 보겠습니다.

## 1단계: PDF 문서 로드

첫 번째 단계는 PDF 문서를 프로젝트에 로드하는 것입니다. 이는 PDF 파일 내의 이미지 작업을 위한 기반이 됩니다.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; 
Aspose.Pdf.Document doc = new Aspose.Pdf.Document(dataDir + "ImagePlacement.pdf");
```

이 단계에서는 다음을 사용하여 PDF 문서의 파일 경로를 정의합니다. `dataDir` 그리고 새로운 인스턴스를 생성합니다. `Aspose.Pdf.Document` 클래스입니다. 이렇게 하면 PDF 파일을 프로그램에 불러올 수 있습니다. 간단하죠? 책을 펼쳐서 읽기 시작하는 것처럼, 이제 안에 있는 내용을 살펴볼 준비가 되었습니다.

## 2단계: 이미지 배치 흡수기 초기화

이미지를 추출하려면 "이미지 배치 흡수기"라는 것이 필요합니다. 특정 페이지의 모든 이미지 정보를 흡수하는 도구라고 생각하면 됩니다.

```csharp
ImagePlacementAbsorber abs = new ImagePlacementAbsorber();
```

여기서 우리는 인스턴스를 생성하고 있습니다 `ImagePlacementAbsorber`이 객체는 특정 PDF 페이지의 모든 이미지 배치에 대한 정보를 수집하고 저장합니다. 마치 돋보기로 페이지를 스캔하여 모든 이미지를 식별하는 것과 같습니다!

## 3단계: 첫 번째 페이지에서 흡수체 수락

다음으로, 흡수체에 PDF의 어느 페이지를 스캔할지 알려줘야 합니다. 이 예시에서는 첫 번째 페이지에 집중하겠습니다.

```csharp
doc.Pages[1].Accept(abs);
```

그만큼 `Accept` 이 방법은 PDF 문서의 첫 페이지를 스캔하여 이미지를 확인하고 결과를 내부에 저장합니다. `ImagePlacementAbsorber`. 이는 돋보기에게 이미지를 어디에서 찾아야 할지 알려주는 것과 같습니다.

## 4단계: 각 이미지 배치 반복

이제 페이지를 스캔했으므로 페이지에서 찾은 각 이미지를 반복하여 속성을 검색해야 합니다.

```csharp
foreach (ImagePlacement imagePlacement in abs.ImagePlacements)
{
    Console.Out.WriteLine("image width:" + imagePlacement.Rectangle.Width);
    Console.Out.WriteLine("image height:" + imagePlacement.Rectangle.Height);
    Console.Out.WriteLine("image LLX:" + imagePlacement.Rectangle.LLX);
    Console.Out.WriteLine("image LLY:" + imagePlacement.Rectangle.LLY);
    Console.Out.WriteLine("image horizontal resolution:" + imagePlacement.Resolution.X);
    Console.Out.WriteLine("image vertical resolution:" + imagePlacement.Resolution.Y);
}
```

이 루프는 페이지에서 찾은 각 이미지를 살펴봅니다. 이미지의 너비, 높이, 왼쪽 하단 x 좌표(LLX), 왼쪽 하단 y 좌표(LLY), 그리고 해상도(가로 및 세로)를 출력합니다. 이러한 정보는 PDF 내에서 각 이미지의 크기와 위치를 이해하는 데 도움이 됩니다.

## 5단계: 눈에 보이는 크기로 이미지 추출

이미지 정보를 수집한 후, 실제 이미지와 크기를 추출하고 싶을 수 있습니다. 방법은 다음과 같습니다.

```csharp
Bitmap scaledImage;
using (MemoryStream imageStream = new MemoryStream())
{
    imagePlacement.Image.Save(imageStream, System.Drawing.Imaging.ImageFormat.Png);
    Bitmap resourceImage = (Bitmap)Bitmap.FromStream(imageStream);
    scaledImage = new Bitmap(resourceImage, (int)imagePlacement.Rectangle.Width, (int)imagePlacement.Rectangle.Height);
}
```

이 코드 조각은 PDF에서 이미지를 검색하고 정의된 실제 크기에 맞게 크기를 조정합니다. `ImagePlacement` 객체입니다. 이미지를 메모리 스트림에 저장하고 크기를 조정하면 추출한 이미지가 PDF에 표시되었던 정확한 크기를 유지하도록 할 수 있습니다.

## 결론

Aspose.PDF for .NET을 사용하여 PDF 문서에서 이미지 배치를 추출하는 것은 단계별로 살펴보면 매우 간단합니다. PDF 로딩부터 이미지 속성 가져오기, 실제 크기로 이미지 추출까지 모든 과정을 다루었습니다. Aspose.PDF는 PDF 작업과 콘텐츠 조작을 매우 간편하게 만들어 이미지, 텍스트 등을 효율적으로 작업할 수 있도록 지원합니다.

## 자주 묻는 질문

### PDF의 특정 페이지에서 이미지를 추출할 수 있나요?  
네, 사용할 때 페이지 번호를 지정하면 됩니다. `Accept` 이 방법을 사용하면 특정 페이지에 집중할 수 있습니다.

### 추출에 지원되는 이미지 형식은 무엇입니까?  
Aspose.PDF는 PNG, JPEG, BMP 등 다양한 형식을 지원합니다.

### 추출된 이미지를 조작하는 것이 가능합니까?  
물론입니다! 추출한 후에는 다음을 사용할 수 있습니다. `System.Drawing` 이미지를 조작하기 위한 네임스페이스.

### 비밀번호로 보호된 PDF에서 이미지를 추출할 수 있나요?  
네, 가능합니다. 하지만 이미지를 추출하기 전에 적절한 자격 증명을 사용하여 PDF의 잠금을 해제해야 합니다.

### Aspose.PDF for .NET은 모든 .NET 프레임워크에서 작동합니까?  
네, .NET Framework, .NET Core, .NET 5 이상을 지원합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}