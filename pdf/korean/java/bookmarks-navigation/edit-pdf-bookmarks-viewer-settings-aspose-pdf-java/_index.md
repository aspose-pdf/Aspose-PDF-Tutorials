---
date: '2025-12-19'
description: Aspose.PDF for Java를 사용하여 PDF 페이지 레이아웃을 변경하고, PDF 북마크를 편집하며, 뷰어 설정을 사용자
  정의하는 방법을 배우세요. 원활한 사용자 경험을 위해 탐색 및 레이아웃 기본 설정을 마스터하세요.
keywords:
- edit PDF bookmarks Java
- Aspose.PDF viewer settings
- configure PDF navigation Java
title: 'Java에서 PDF 페이지 레이아웃 변경: 북마크 및 설정 편집'
url: /ko/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Java에서 PDF 페이지 레이아웃 변경: 북마크 및 설정 편집

## 소개
복잡한 PDF 문서를 탐색하는 것은 번거로울 수 있습니다. 특히 **PDF 페이지 레이아웃 변경** 설정이 올바르게 구성되지 않았거나 북마크가 잘못된 위치를 가리킬 때 더욱 그렇습니다. 이 튜토리얼에서는 Aspose.PDF for Java를 사용하여 **PDF 페이지 레이아웃을 변경**, **PDF 북마크를 편집**, **PDF 뷰어 설정을 구성**하는 방법을 배웁니다. 끝까지 따라오면 탐색, 북마크 목적지 및 문서가 독자에게 표시되는 방식을 완벽히 제어할 수 있게 됩니다.

**배우게 될 내용**
- 기존 PDF 북마크를 페이지 시작 지점으로 지정하는 방법.  
- PDF를 생성하면서 북마크 목적지를 설정하는 방법.  
- 페이지 레이아웃과 같은 뷰어 기본 설정을 변경하는 방법.  
- Java에서 PDF 문서를 로드하고 성능을 최적화하는 실용적인 팁.

### 빠른 답변
- **PDF 페이지 레이아웃을 변경하는 기본 방법은?** `PdfContentEditor.changeViewerPreference()`에 `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`를 사용합니다.  
- **PDF 생성 후에 북마크 목적지를 편집할 수 있나요?** 예 – 문서를 로드하고, 아웃라인에 접근한 뒤 새로운 `ExplicitDestination`을 설정합니다.  
- **이 기능들을 사용하려면 라이선스가 필요합니까?** 평가용 무료 체험판으로도 사용 가능하며, 정식 라이선스를 구매하면 모든 제한이 해제됩니다.  
- **필요한 Maven 의존성은?** `com.aspose:aspose-pdf:25.3` (또는 이후 버전).  
- **Java 11 이상과 호환되나요?** 물론입니다 – Aspose.PDF는 Java 8 이상을 지원합니다.

## “PDF 페이지 레이아웃 변경”이란?
PDF 페이지 레이아웃을 변경하면 뷰어에서 페이지가 표시되는 방식—단일 페이지, 연속, 양면 보기 등—을 제어합니다. 이 설정을 조정하면 특히 긴 보고서나 카탈로그의 가독성이 크게 향상됩니다.

## 왜 PDF 북마크를 편집하고 북마크 목적지를 설정해야 할까요?
북마크는 목차와 같은 역할을 합니다. 정확한 목적지를 지정하면 독자가 원하는 섹션으로 바로 이동할 수 있어 불편함을 줄이고 전반적인 사용자 경험을 개선합니다.

## 사전 요구 사항
- **라이브러리 및 의존성**: Aspose.PDF for Java v25.3 이상.  
- **환경**: JDK 8 이상, Maven 또는 Gradle 빌드 도구.  
- **지식**: 기본 Java 프로그래밍 및 PDF 개념에 대한 이해.

## Aspose.PDF for Java 설정
### Maven 설치
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Gradle 설치
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**라이선스 획득**: 무료 체험판으로 시작하거나 전체 기능 접근을 위한 임시 라이선스를 요청하세요. 운영 환경에서는 정식 라이선스 구매를 권장합니다.

### 기본 초기화
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## 구현 가이드
### Java에서 PDF 페이지 레이아웃 변경 방법
**개요**: 뷰어 기본 설정을 조정하여 페이지를 원하는 방식으로 표시합니다.

#### PdfContentEditor 초기화
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### 뷰어 기본 설정 변경
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### 업데이트된 문서 저장
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

### PDF 북마크 편집 방법
**개요**: 기존 북마크가 특정 페이지 시작을 정확히 가리키도록 조정합니다.

#### 북마크 접근
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### 새로운 목적지 설정
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### 변경 사항 저장
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

### PDF 생성 시 북마크 목적지 설정 방법
**개요**: 새로 생성된 PDF에서 사용자를 원하는 위치로 직접 안내하는 북마크를 만듭니다.

#### 북마크 생성 및 구성
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### 북마크 목적지 정의
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### PDF 추가 및 저장
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## 실용적인 적용 사례
1. **디지털 도서** – 각 장의 북마크가 페이지 상단에 위치하도록 하여 매끄러운 독서 경험 제공.  
2. **기술 매뉴얼** – 정확한 탐색으로 엔지니어가 대용량 PDF에서도 섹션을 빠르게 찾을 수 있음.  
3. **제품 카탈로그** – 단일 페이지 레이아웃으로 태블릿에서 카탈로그 탐색이 직관적임.

## 성능 고려 사항
- **리소스 최적화**: 대용량 PDF를 처리할 때 `Document.optimizeResources()`를 사용해 메모리 사용량을 감소시킵니다.  
- **Java 메모리 관리**: 스트림을 명시적으로 닫고, 처리 후 가비지 컬렉터가 객체를 회수하도록 합니다.

## 일반적인 문제 및 해결책
- **북마크가 업데이트되지 않음**: 올바른 아웃라인 인덱스(`get_Item(1)`은 최상위 북마크 첫 번째 항목)를 수정하고 있는지 확인하세요.  
- **뷰어 기본 설정이 적용되지 않음**: 기본 설정을 변경한 뒤 `editor.save()`를 호출해야 합니다; 호출하지 않으면 메모리 상에만 변경됩니다.  
- **라이선스 예외**: 체험판 라이선스는 워터마크가 추가될 수 있으니, 운영 환경에서는 정식 라이선스를 확보하세요.

## 자주 묻는 질문
**Q: Java에서 PDF 문서를 가장 쉽게 로드하는 방법은?**  
A: `new Document("path/to/file.pdf")`를 사용합니다; Aspose.PDF가 파일 형식을 자동으로 감지합니다.

**Q: PdfContentEditor 없이 페이지 레이아웃을 변경할 수 있나요?**  
A: 예, `Document` 객체의 `getViewerPreferences().setPageLayout(...)`를 직접 호출하면 됩니다.

**Q: 뷰어 레이아웃을 변경하면 인쇄에 영향을 줍니까?**  
A: 뷰어 레이아웃은 화면 표시에만 영향을 미치며 인쇄 결과에는 영향을 주지 않습니다.

**Q: 만들 수 있는 북마크 수에 제한이 있나요?**  
A: 명시적인 제한은 없지만, 매우 큰 아웃라인 트리는 성능에 영향을 줄 수 있으니 구조를 정리해 두세요.

**Q: 페이지를 추가하거나 삭제한 후 북마크 목적지를 정확히 맞추려면?**  
A: 구조 변경 후 현재 페이지 인덱스를 기준으로 목적지를 다시 계산합니다.

## 리소스
- **문서**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)  
- **다운로드**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)  
- **구매**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)  
- **무료 체험**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)  
- **임시 라이선스**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**마지막 업데이트:** 2025-12-19  
**테스트 환경:** Aspose.PDF for Java v25.3  
**작성자:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}