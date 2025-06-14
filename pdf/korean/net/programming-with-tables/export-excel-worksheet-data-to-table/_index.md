---
"description": "Aspose.PDF for .NET을 사용하여 Excel 워크시트 데이터를 PDF 표로 내보내는 방법을 알아보세요. 코드 예제, 필수 구성 요소, 유용한 팁이 포함된 단계별 튜토리얼입니다."
"linktitle": "Excel 워크시트 데이터를 테이블로 내보내기"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "Excel 워크시트 데이터를 테이블로 내보내기"
"url": "/ko/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel 워크시트 데이터를 테이블로 내보내기

## 소개

Excel 워크시트의 데이터를 깔끔하게 표 형식으로 정리된 PDF 파일로 내보내야 했던 적이 있으신가요? Excel에 데이터가 산더미처럼 쌓여 있는데, 전문가 수준의 PDF 파일로 공유해야 한다고 상상해 보세요. 복잡하게 들릴 수 있죠? 하지만 Aspose.PDF for .NET을 사용하면 이 작업을 아주 쉽게 처리할 수 있습니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 Excel 워크시트 데이터를 PDF 문서 내의 표로 내보내는 과정을 안내해 드립니다. 모든 과정을 단계별로 자세히 설명해 드리기 때문에 처음 접하는 사용자라도 마치 전문가처럼 능숙하게 다룰 수 있을 것입니다.

## 필수 조건

코딩에 들어가기 전에 몇 가지를 설정해 보겠습니다.

1. Aspose.PDF for .NET 라이브러리 – 최신 버전이 설치되어 있는지 확인하세요. [여기서 다운로드하세요](https://releases.aspose.com/pdf/net/).
2. Aspose.Cells for .NET 라이브러리 - Excel 작업을 처리하는 데 필요합니다. 에서 다운로드하세요. [여기](https://releases.aspose.com/cells/net/).
3. .NET 개발 환경 – Visual Studio와 같은 도구는 코딩에 완벽하게 적합합니다.
4. Excel 파일 – 내보내고자 하는 데이터가 담긴 Excel 파일을 준비하세요.

Aspose.PDF 및 Aspose.Cells 라이브러리가 없으면 다음으로 시작할 수 있습니다. [무료 체험](https://releases.aspose.com/).

## 패키지 가져오기

먼저, 프로젝트에 Aspose.PDF와 Aspose.Cells 라이브러리가 모두 설치되어 있는지 확인하세요. Visual Studio의 NuGet 패키지 관리자를 사용하여 설치할 수 있습니다.

C# 코드에서 필요한 패키지를 가져오는 방법은 다음과 같습니다.

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

이제 필수 조건이 설정되었으므로 Excel 시트의 데이터를 PDF 문서의 표로 내보내는 과정을 살펴보겠습니다.

## 1단계: Excel 통합 문서 로드

시작하려면 Excel 통합 문서를 프로그램에 불러와야 합니다. 이 단계에서는 Aspose.Cells를 사용하여 Excel 파일을 엽니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Excel 통합 문서 로드
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

설명: 여기서 Excel 파일이 있는 디렉토리 경로를 지정하고 다음을 사용하여 통합 문서를 로드합니다. `Aspose.Cells.Workbook`. 조정을 꼭 하세요 `"YOUR DOCUMENT DIRECTORY"` 파일의 위치를 가리키도록 합니다.

## 2단계: 첫 번째 워크시트에 액세스

통합 문서를 로드한 후에는 데이터가 저장된 첫 번째 워크시트에 액세스해야 합니다.

```csharp
// Excel 파일의 첫 번째 워크시트에 액세스하기
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

설명: 이 단계는 간단합니다. 내보낼 데이터가 들어 있는 통합 문서에서 첫 번째 워크시트를 가져오면 됩니다.

## 3단계: DataTable로 데이터 내보내기

이제 Excel 시트의 데이터를 DataTable 개체로 내보내 보겠습니다. 이 개체는 데이터를 PDF로 전송하는 중개자 역할을 합니다.

```csharp
// 1번째 셀부터 시작하여 7행 2열의 내용을 DataTable로 내보내기
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

설명: `ExportDataTable` 이 메서드는 워크시트의 첫 번째 셀부터 시작하여 모든 행과 열에 걸쳐 데이터를 추출합니다. 이 데이터는 다음 위치에 저장됩니다. `DataTable` 추후 사용을 위해.

## 4단계: 새 PDF 문서 만들기

다음으로, Aspose.PDF를 사용하여 새로운 PDF 문서를 만들어야 합니다.

```csharp
// 문서 인스턴스를 인스턴스화합니다
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// 문서 인스턴스에 페이지를 만듭니다.
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

설명: 여기서 우리는 새로운 것을 초기화합니다. `Aspose.Pdf.Document` 페이지를 추가합니다. 이 페이지에는 나중에 Excel 데이터로 만드는 표가 포함됩니다.

## 5단계: PDF에서 표 개체 만들기

이제 PDF 문서 내부에 표를 만들어 보겠습니다.

```csharp
// Table 객체를 생성합니다
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// 페이지의 문단 컬렉션에 Table 객체를 추가합니다.
page.Paragraphs.Add(table);
```

설명: 우리는 다음을 생성합니다. `Aspose.Pdf.Table` 객체를 만들어 페이지의 문단 컬렉션에 추가하면 페이지에 표가 표시됩니다.

## 6단계: 열 너비 및 테두리 설정

PDF 표에는 열 너비를 정의해야 합니다. 또한 표의 가독성을 높이기 위해 테두리를 추가할 예정입니다.

```csharp
// 표의 열 너비 설정
table.ColumnWidths = "40 100 100";

// 기본 셀 테두리 설정
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

설명: 세 개의 열 너비를 설정하고 모든 셀에 두께가 있는 기본 테두리를 지정합니다. `0.1F`.

## 7단계: DataTable에서 PDF 테이블로 데이터 가져오기

이제 DataTable에서 PDF 테이블로 데이터를 가져올 차례입니다.

```csharp
// DataTable에서 Table 개체로 데이터 가져오기
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

설명: `ImportDataTable` 이 방법은 모든 데이터를 전송합니다. `DataTable` PDF 표로. 그러면 Excel 시트의 데이터가 표에 채워집니다.

## 8단계: 헤더 행 스타일 지정

배경색, 글꼴, 정렬을 변경하여 표의 헤더 행의 스타일을 지정해 보겠습니다.

```csharp
// 테이블에서 첫 번째 행을 가져옵니다
Aspose.Pdf.Row headerRow = table.Rows[0];

// 헤더 행에 대한 스타일 설정
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

설명: 첫 번째 행(헤더)의 모든 셀을 반복하여 배경색을 파란색으로, 텍스트 색상을 노란색으로 설정하고 텍스트를 가운데에 맞춥니다.

## 9단계: 나머지 행 스타일 지정

헤더와 나머지 행을 구분하기 위해 나머지 행에 다른 스타일을 추가해 보겠습니다.

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

설명: 헤더를 제외한 모든 행에 대해 회색 배경과 흰색 텍스트 색상을 설정했습니다.

## 10단계: PDF 문서 저장

마지막으로 표가 포함된 PDF 문서를 저장합니다.

```csharp
// PDF 저장
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

설명: PDF를 지정된 디렉터리에 저장합니다. 짜잔! 이제 Excel 데이터가 보기 좋게 포맷된 PDF 표에 저장되었습니다.

## 결론

자, 이제 완성되었습니다! Aspose.PDF for .NET을 사용하여 몇 단계만 거치면 Excel 워크시트의 데이터를 PDF 내부의 표로 내보낼 수 있습니다. 프로세스를 세분화하고 스타일을 적용하면 출력 결과를 사용자 지정하고 데이터가 깔끔하고 전문적으로 보이도록 할 수 있습니다. 다음에 누군가 Excel 파일을 건네주며 PDF 보고서를 요청하면 어떻게 해야 할지 정확히 알 수 있습니다.

## 자주 묻는 질문

### 표를 더욱 맞춤설정할 수 있나요?
물론입니다! 색상, 글꼴, 정렬을 수정하고 특정 셀에 테두리를 추가할 수도 있습니다.

### Aspose.PDF for .NET은 무료인가요?
무료 체험판을 제공하지만, 장기간 사용하려면 라이선스가 필요합니다. [여기서 사세요](https://purchase.aspose.com/buy).

### 특정 행과 열만 내보낼 수 있나요?
네, 매개변수를 수정할 수 있습니다. `ExportDataTable` 특정 범위를 내보내는 방법.

### 이 기능이 대용량 Excel 파일에도 적용되나요?
네, Aspose.Cells는 대용량 Excel 파일을 효율적으로 처리하도록 설계되었습니다.

### PDF에 페이지를 더 추가하려면 어떻게 해야 하나요?
사용할 수 있습니다 `pdfDocument.Pages.Add()` 필요한 만큼 페이지를 추가할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}