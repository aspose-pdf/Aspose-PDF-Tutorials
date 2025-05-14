---
"date": "2025-04-11"
"description": "Aspose.PDF for .NET을 사용하여 PDF 문서에 날짜 및 시간 스탬프나 주석을 효율적으로 추가하는 방법을 알아보세요. 따라 하기 쉬운 단계를 통해 문서 관리를 더욱 효율적으로 개선해 보세요."
"title": "Aspose.PDF for .NET을 사용하여 PDF에 날짜 및 시간 스탬프 추가"
"url": "/ko/net/document-manipulation/aspose-pdf-net-date-time-stamps-annotations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.PDF for .NET을 사용하여 PDF에 날짜 및 시간 스탬프 추가

## 소개

오늘날의 디지털 시대에 효과적인 문서 관리는 기업과 개인 모두에게 매우 중요합니다. PDF에 날짜 및 시간 스탬프나 주석을 추가하면 데이터 무결성과 정리 기능을 강화할 수 있습니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 이러한 기능을 통합하는 방법을 보여줍니다.

**주요 내용:**
- 지정된 PDF 페이지에 현재 날짜와 시간을 텍스트 스탬프로 추가합니다.
- 문서의 원하는 위치에 자유 텍스트 주석을 만듭니다.
- Aspose.PDF for .NET을 사용하여 최적의 성능을 얻으려면 모범 사례를 따르세요.

## 필수 조건
시작하기 전에 다음 사항을 확인하세요.

### 필수 라이브러리 및 버전
- **.NET용 Aspose.PDF**: Adobe Acrobat 없이 PDF를 조작할 수 있는 강력한 라이브러리입니다. 21.x 버전 이상을 사용하세요.

### 환경 설정 요구 사항
- .NET Framework 4.5 이상 또는 .NET Core 2.0 이상을 갖춘 개발 환경
- C# 프로그래밍을 지원하는 Visual Studio 또는 다른 IDE

### 지식 전제 조건
- C# 및 .NET 프로젝트 구조에 대한 기본 이해
- 디렉토리 구조에서 파일을 처리하는 방법에 대한 지식

## .NET용 Aspose.PDF 설정
다음 방법 중 하나를 사용하여 Aspose.PDF를 설치하세요.

**.NET CLI 사용:**
```bash
dotnet add package Aspose.PDF
```

**패키지 관리자 사용:**
```powershell
Install-Package Aspose.PDF
```

**NuGet 패키지 관리자 UI를 통해:**
- IDE에서 NuGet 패키지 관리자를 엽니다.
- "Aspose.PDF"를 검색하여 최신 버전을 설치하세요.

### 라이센스 취득 단계
Aspose.PDF를 최대한 활용하려면:
1. **무료 체험:** 모든 기능을 탐색하려면 임시 라이센스를 다운로드하세요.
2. **임시 면허:** 필요한 경우 확장된 평가 라이선스를 요청하세요.
3. **구입:** Aspose 웹사이트에서 장기 사용 라이선스를 구매하세요.

코드에서 라이센스를 초기화하세요:
```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to License File");
```

## 구현 가이드
PDF에 날짜와 시간 스탬프를 추가해 보겠습니다.

### 기능 1: PDF에 날짜/시간 스탬프 추가
이 기능은 지정된 PDF 문서의 첫 페이지에 현재 날짜와 시간을 텍스트 스탬프로 추가합니다.

#### 단계별 구현

##### 1. 기존 PDF 문서 열기
대상 문서를 로드하세요:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/AddTextStamp.pdf");
```

##### 2. 현재 날짜 및 시간을 문자열로 가져오기
현재 날짜와 시간을 형식화합니다.
```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

##### 3. 현재 날짜와 시간을 포함하는 텍스트 스탬프 만들기
생성하다 `TextStamp` 형식화된 문자열을 사용하는 인스턴스:
```csharp
TextStamp textStamp = new TextStamp(annotationText);
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

##### 4. 첫 페이지에 텍스트 스탬프 추가
문서의 첫 페이지에 스탬프를 추가하세요.
```csharp
document.Pages[1].AddStamp(textStamp);
```

##### 5. FreeTextAnnotation 생성 및 추가(선택 사항)
더 복잡한 주석의 경우 다음을 생성하세요. `FreeTextAnnotation`:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(document.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance)
{
    Name = "Stamp",
    Contents = textStamp.Value
};
textAnnotation.Border = new Border(textAnnotation) { Width = 0 };
document.Pages[1].Annotations.Add(textAnnotation);
```

##### 6. 수정된 문서 저장
변경 사항을 저장하세요:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/AddDateTimeStamp_out.pdf";
document.Save(outputDir);
```

### 기능 2: PDF에 자유 텍스트 주석 추가
PDF 문서 내에서 원하는 위치에 자유 텍스트 주석을 추가할 수 있습니다.

#### 단계별 구현

##### 1. 기존 PDF 문서 열기
대상 문서를 로드하세요:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/Sample.pdf");
```

##### 2. 주석을 위한 사각형 영역 정의
페이지에 주석을 배치할 위치를 지정하세요.
```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(100, 400, 200, 450);
```

##### 3. 지정된 모양과 위치로 FreeTextAnnotation 만들기
원하는 텍스트와 모양 설정으로 주석을 초기화하세요.
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 12, System.Drawing.Color.Blue);
FreeTextAnnotation freeTextAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], rect, default_appearance)
{
    Contents = "This is a sample annotation",
    Title = "Sample Annotation"
};
```

##### 4. 테두리 스타일 설정 및 주석 추가
테두리 스타일이 귀하의 요구 사항과 일치하는지 확인하세요(이 경우에는 보이지 않음):
```csharp
freeTextAnnotation.Border = new Border(freeTextAnnotation) { Width = 0 };
pdfDocument.Pages[1].Annotations.Add(freeTextAnnotation);
```

##### 5. 수정된 문서 저장
새로 추가한 주석과 함께 문서를 저장하세요.
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/FreeTextAnnotation_out.pdf";
document.Save(outputDir);
```

## 실제 응용 프로그램
PDF에 날짜 스탬프와 주석을 추가하는 기능은 다양한 산업 분야에서 유용합니다.
- **법률 문서**: 변경 사항에 타임스탬프를 적용하여 규정 준수를 보장합니다.
- **학술 논문**: 주석을 통해 공동 편집이 용이해집니다.
- **재무 기록**: 타임스탬프가 포함된 보고서로 정확한 감사 추적을 유지합니다.
- **기술 문서**: 매뉴얼의 업데이트나 중요한 참고 사항을 강조 표시합니다.

## 성능 고려 사항
.NET에서 Aspose.PDF를 사용할 때 최적의 성능을 얻으려면:
- **일괄 처리**: 오버헤드를 줄이기 위해 여러 PDF를 일괄적으로 처리합니다.
- **메모리 관리**: 사용 `Dispose` 각 문서를 처리한 후 메모리 리소스를 해제하는 방법.
- **최적화된 글꼴 및 이미지**: 파일 크기를 줄이려면 글꼴 유형과 이미지 해상도를 제한하세요.

## 결론
Aspose.PDF for .NET을 통합하면 PDF 문서에 날짜 표시 및 주석 기능을 추가하여 기능을 향상시킬 수 있습니다. 이러한 도구는 데이터 무결성을 개선하고 문서 관리를 간소화합니다.

다양한 구성을 실험하고 Aspose.PDF가 제공하는 추가 기능을 살펴보아 특정 요구 사항을 충족하세요.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}