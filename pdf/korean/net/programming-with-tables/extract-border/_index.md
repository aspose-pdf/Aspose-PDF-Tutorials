---
"description": "Aspose.PDF for .NET을 사용하여 PDF 파일에서 테두리를 추출하고 이미지로 저장하는 방법을 알아보세요. 코드 샘플과 성공 팁을 담은 단계별 가이드입니다."
"linktitle": "PDF 파일에서 테두리 추출"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에서 테두리 추출"
"url": "/ko/net/programming-with-tables/extract-border/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에서 테두리 추출

## 소개

PDF 작업 시 테두리나 그래픽 경로와 같은 특정 요소를 추출하는 것은 어려울 수 있습니다. 하지만 Aspose.PDF for .NET을 사용하면 PDF 파일에서 테두리나 도형을 쉽게 추출하여 이미지로 저장할 수 있습니다. 이 튜토리얼에서는 PDF에서 테두리를 추출하여 PNG 이미지로 저장하는 과정을 자세히 살펴보겠습니다. PDF의 그래픽 콘텐츠를 직접 관리할 준비를 하세요!

## 필수 조건

코드를 살펴보기 전에 모든 것이 설정되어 있는지 확인하세요.

1. .NET용 Aspose.PDF: 아직 Aspose.PDF 라이브러리를 설치하지 않은 경우 다음을 수행할 수 있습니다. [여기서 다운로드하세요](https://releases.aspose.com/pdf/net/). 무료 평가판이나 구매한 라이선스를 통해 라이선스를 적용해야 합니다.
2. IDE 설정: Visual Studio 또는 다른 .NET IDE에서 C# 프로젝트를 설정합니다. Aspose.PDF 라이브러리에 필요한 참조를 추가했는지 확인하세요.
3. PDF 파일 입력: 테두리를 추출할 PDF 파일을 준비하세요. 이 튜토리얼에서는 다음 이름의 파일을 참조합니다. `input.pdf`.

## 필수 패키지 가져오기

필요한 네임스페이스를 가져오는 것부터 시작해 보겠습니다. 이 패키지는 PDF 콘텐츠를 조작하는 데 필요한 도구를 제공합니다.

```csharp
using System.IO;
using System;
using System.Drawing.Drawing2D;
using System.Drawing.Imaging;
using System.Collections;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
```

이제 기본 사항을 다루었으니, 각 코드 부분을 분석하여 자세히 설명하는 단계별 가이드로 넘어가겠습니다.


## 1단계: PDF 문서 로드

첫 번째 단계는 추출하려는 테두리가 포함된 PDF 문서를 불러오는 것입니다. 마치 책을 읽기 전에 책을 펼치는 것과 같습니다. 즉, 내용에 접근해야 합니다!

PDF 파일이 저장된 디렉토리를 지정하고 다음을 사용하여 문서를 로드하는 것으로 시작합니다. `Aspose.Pdf.Document` 수업.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

이 코드는 다음을 로드합니다. `input.pdf` 지정한 디렉터리에서 파일을 가져오세요. 파일 경로가 올바른지 확인하세요. 그렇지 않으면 "파일을 찾을 수 없습니다" 오류가 발생할 수 있습니다.

## 2단계: 그래픽 및 비트맵 설정

추출을 시작하기 전에 그림을 그릴 캔버스를 만들어야 합니다. .NET 환경에서는 Bitmap 객체와 Graphics 객체를 설정하는 것을 의미합니다. Bitmap 객체는 이미지를 나타내고, Graphics 객체는 PDF에서 추출한 테두리와 같은 도형을 그릴 수 있도록 해줍니다.

```csharp
System.Drawing.Bitmap bitmap = new System.Drawing.Bitmap((int)doc.Pages[1].PageInfo.Width, (int)doc.Pages[1].PageInfo.Height);
System.Drawing.Drawing2D.GraphicsPath graphicsPath = new System.Drawing.Drawing2D.GraphicsPath();
System.Drawing.Drawing2D.Matrix lastCTM = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, 0);
System.Drawing.Drawing2D.Matrix inversionMatrix = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, (float)doc.Pages[1].PageInfo.Height);
System.Drawing.PointF lastPoint = new System.Drawing.PointF(0, 0);
System.Drawing.Color fillColor = System.Drawing.Color.FromArgb(0, 0, 0);
System.Drawing.Color strokeColor = System.Drawing.Color.FromArgb(0, 0, 0);
```

세부 내용은 다음과 같습니다.
- PDF의 첫 페이지 크기의 비트맵 이미지를 만듭니다.
- GraphicsPath는 모양(이 경우 테두리)을 정의하는 데 사용됩니다.
- 행렬은 그래픽이 어떻게 변환될지 정의합니다. PDF와 .NET은 서로 다른 좌표계를 사용하기 때문에 역행렬이 필요합니다.

## 3단계: PDF 콘텐츠 처리


PDF 파일은 일련의 그리기 명령이며, 각 명령을 처리하여 테두리 정보를 식별하고 추출해야 합니다.

```csharp
foreach (Operator op in doc.Pages[1].Contents)
{
    // 상태 저장/복원, 선 그리기, 모양 채우기 등의 명령 처리
}
```

이 코드는 PDF 콘텐츠 스트림의 모든 그리기 연산자를 순회합니다. 각 연산자는 선, 사각형 또는 기타 그래픽 명령을 나타낼 수 있습니다.

## 4단계: PDF 연산자 처리

PDF 파일의 각 연산자는 동작을 제어합니다. 테두리를 추출하려면 "이동", "선", "사각형 그리기"와 같은 명령을 식별해야 합니다. 다음 연산자들이 이러한 동작을 처리합니다.

- MoveTo: 커서를 시작점으로 이동합니다.
- LineTo: 현재 지점에서 새 지점까지 선을 그립니다.
- Re: 사각형을 그립니다(이것은 테두리의 일부가 될 수 있습니다).

```csharp
Aspose.Pdf.Operators.MoveTo opMoveTo = op as Aspose.Pdf.Operators.MoveTo;
Aspose.Pdf.Operators.LineTo opLineTo = op as Aspose.Pdf.Operators.LineTo;
Aspose.Pdf.Operators.Re opRe = op as Aspose.Pdf.Operators.Re;

if (opMoveTo != null)
{
    lastPoint = new System.Drawing.PointF((float)opMoveTo.X, (float)opMoveTo.Y);
}
else if (opLineTo != null)
{
    System.Drawing.PointF linePoint = new System.Drawing.PointF((float)opLineTo.X, (float)opLineTo.Y);
    graphicsPath.AddLine(lastPoint, linePoint);
    lastPoint = linePoint;
}
else if (opRe != null)
{
    System.Drawing.RectangleF re = new System.Drawing.RectangleF((float)opRe.X, (float)opRe.Y, (float)opRe.Width, (float)opRe.Height);
    graphicsPath.AddRectangle(re);
}
```

이 단계에서는:
- 우리는 그려진 각 선이나 모양의 점을 포착합니다.
- 직사각형의 경우 (`opRe`), 우리는 그것들을 직접 추가합니다 `graphicsPath`, 나중에 테두리를 그리는 데 사용합니다.

## 5단계: 테두리 그리기

테두리를 형성하는 선과 사각형을 파악했으면 이제 실제로 Bitmap 객체에 그려야 합니다. 이때 Graphics 객체가 필요합니다.

```csharp
using (System.Drawing.Graphics gr = System.Drawing.Graphics.FromImage(bitmap))
{
    gr.SmoothingMode = SmoothingMode.HighQuality;
    gr.DrawPath(new System.Drawing.Pen(strokeColor), graphicsPath);
}
```

- 비트맵을 기반으로 Graphics 객체를 생성합니다.
- SmoothingMode.HighQuality를 사용하면 매끄러운 이미지를 얻을 수 있습니다.
- 마지막으로 DrawPath를 사용하여 테두리를 그립니다.

## 6단계: 추출된 테두리 저장

테두리를 추출했으니 이제 이미지 파일로 저장할 차례입니다. 그러면 테두리가 PNG 파일로 저장됩니다.

```csharp
dataDir = dataDir + "ExtractBorder_out.png";
bitmap.Save(dataDir, ImageFormat.Png);
```

- 비트맵은 PNG 이미지로 저장됩니다.
- 이제 이 이미지를 열어 추출된 테두리를 볼 수 있습니다.

## 결론

Aspose.PDF for .NET을 사용하여 PDF 파일에서 테두리를 추출하는 것은 처음에는 까다로울 수 있지만, 자세히 살펴보면 간단해집니다. PDF의 그리기 연산자를 이해하고 강력한 .NET 라이브러리를 활용하면 그래픽 콘텐츠를 효율적으로 조작하고 추출할 수 있습니다. 이 가이드는 PDF 조작을 시작하는 데 필요한 탄탄한 기반을 제공합니다!

## 자주 묻는 질문

### PDF에서 여러 페이지를 처리하려면 어떻게 해야 하나요?  
문서의 각 페이지를 반복하여 순환할 수 있습니다. `doc.Pages` 하드코딩 대신 `doc.Pages[1]`.

### 동일한 방법을 사용하여 텍스트와 같은 다른 요소를 추출할 수 있습니까?  
네, Aspose.PDF는 PDF 파일에서 텍스트, 이미지 및 기타 콘텐츠를 추출하는 풍부한 API를 제공합니다.

### 제한을 피하기 위해 라이선스를 적용하려면 어떻게 해야 합니까?  
당신은 할 수 있습니다 [라이센스를 적용하다](https://purchase.aspose.com/temporary-license/) 그것을 통해 로드하여 `License` Aspose가 제공하는 클래스입니다.

### PDF에 테두리가 없으면 어떻게 해야 하나요?  
PDF에 눈에 보이는 테두리가 없으면 그래픽 추출 과정에서 결과가 나오지 않을 수 있습니다. PDF 콘텐츠에 그리기 가능한 테두리가 포함되어 있는지 확인하세요.

### PNG 이외의 다른 형식으로 출력물을 저장할 수 있나요?  
네, 간단히 변경하세요 `ImageFormat.Png` 다른 지원 형식(예: `ImageFormat.Jpeg`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}