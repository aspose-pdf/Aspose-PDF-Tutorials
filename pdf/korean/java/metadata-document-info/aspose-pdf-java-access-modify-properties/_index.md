---
"date": "2025-04-14"
"description": "Aspose.PDF for Java를 사용하여 PDF 속성에 접근하고 수정하는 방법을 알아보세요. 이 가이드에서는 문서 메타데이터, 창 설정, 읽기 순서 등에 대해 다룹니다."
"title": "Aspose.PDF for Java를 사용하여 PDF 속성에 액세스하고 수정하는 방법&#58; 포괄적인 가이드"
"url": "/ko/java/metadata-document-info/aspose-pdf-java-access-modify-properties/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Java용 Aspose.PDF를 사용하여 PDF 속성에 액세스하고 수정하는 방법

## 소개

PDF 파일의 속성에 쉽게 액세스하고 수정하여 PDF 파일과의 애플리케이션 상호 작용을 향상시키세요. **Java용 Aspose.PDF**이 포괄적인 가이드에서는 Aspose.PDF를 사용하여 창 위치, 읽기 순서, 표시 제목 설정 등 다양한 문서 속성을 관리하는 방법을 안내합니다.

**배울 내용:**
- 프로젝트에서 Java용 Aspose.PDF를 설정합니다.
- Aspose.PDF 메서드를 사용하여 다양한 문서 속성에 액세스합니다.
- 창 표시 설정 및 읽기 순서 구성.
- PDF 작업 시 흔히 발생하는 문제를 해결합니다.

시작하는 데 필요한 전제 조건을 살펴보겠습니다!

## 필수 조건

시작하기 전에 설정에 다음이 포함되어 있는지 확인하세요.

### 필수 라이브러리
- **Java용 Aspose.PDF**: 25.3 이상 버전을 권장합니다. 이 튜토리얼에 설명된 대로 Maven이나 Gradle을 통해 추가하세요.

### 환경 설정
- 컴퓨터에 Java 개발 키트(JDK)가 설치되어 있어야 합니다.
- IntelliJ IDEA, Eclipse 또는 NetBeans와 같은 통합 개발 환경(IDE).

### 지식 전제 조건
- Java 프로그래밍에 대한 기본적인 이해.
- 종속성 관리를 위한 Maven이나 Gradle과 같은 프로젝트 관리 도구에 익숙합니다.

필수 구성 요소를 갖추었으니 Java용 Aspose.PDF를 설정해 보겠습니다.

## Java용 Aspose.PDF 설정

사용을 시작하려면 **Java용 Aspose.PDF**프로젝트에 포함해야 합니다. 방법은 다음과 같습니다.

### 메이븐
다음 종속성을 추가하세요. `pom.xml` 파일:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

### 그래들
이 줄을 포함하세요 `build.gradle` 파일:
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### 라이센스 취득

당신은 얻을 수 있습니다 **무료 체험** Aspose.PDF를 다음에서 다운로드하여 [출시 페이지](https://releases.aspose.com/pdf/java/). 지속적으로 사용하려면 라이센스를 구매하거나 다음을 통해 임시 라이센스를 신청해야 할 수 있습니다. [구매 페이지](https://purchase.aspose.com/buy).

### 기본 초기화

Aspose.PDF로 프로젝트를 설정한 후 다음과 같이 초기화합니다.
```java
import com.aspose.pdf.Document;

public class PdfPropertiesExample {
    public static void main(String[] args) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        
        // 문서 객체를 초기화합니다
        Document pdfDocument = new Document(dataDir + "/Original.pdf");
        
        // 문서 속성에 액세스하려면 계속하세요.
    }
}
```

Aspose.PDF가 구성되었으므로 이제 PDF 문서 속성에 액세스하고 구성하는 방법을 살펴보겠습니다.

## 구현 가이드

이 섹션에서는 Aspose.PDF를 사용하여 PDF 문서의 다양한 속성에 액세스하는 방법을 안내합니다.

### 중앙 창 속성

**개요**: 이 속성은 PDF 창을 열 때 가운데에 배치할지 여부를 결정합니다. 기본적으로 다음과 같이 설정되어 있습니다. `false`.

#### 단계
1. **부동산 접근**
   ```java
   boolean centerWindow = pdfDocument.isCenterWindow();
   System.out.println("Is center window enabled? " + centerWindow);
   ```

2. **속성 설정**
   중앙 정렬을 활성화하려면:
   ```java
   pdfDocument.setCenterWindow(true);
   ```

### 읽기 순서

**개요**: 그 `Direction` 속성은 왼쪽에서 오른쪽(L2R) 또는 오른쪽에서 왼쪽(R2L)과 같이 읽기 순서를 지정합니다.

#### 단계
1. **부동산 접근**
   ```java
   String direction = pdfDocument.getDirection();
   System.out.println("Reading direction: " + direction);
   ```

2. **읽기 순서 설정**
   오른쪽에서 왼쪽으로 변경합니다.
   ```java
   pdfDocument.setDirection(com.aspose.pdf.Document.DirectionType.R2L);
   ```

### 문서 제목 표시

**개요**: 창의 제목 표시줄에 문서 제목이나 파일 이름을 표시할지 여부를 제어합니다.

#### 단계
1. **부동산 접근**
   ```java
   boolean displayDocTitle = pdfDocument.isDisplayDocTitle();
   System.out.println("Is document title displayed? " + displayDocTitle);
   ```

2. **설정 수정**
   문서 제목 표시를 활성화하려면:
   ```java
   pdfDocument.setDisplayDocTitle(true);
   ```

### 창 맞춤

**개요**: 이 속성은 창을 열 때 첫 번째 페이지에 맞게 창 크기를 조절합니다.

#### 단계
1. **부동산 접근**
   ```java
   boolean fitWindow = pdfDocument.isFitWindow();
   System.out.println("Is fit window enabled? " + fitWindow);
   ```

2. **설정 조정**
   크기 조절 활성화:
   ```java
   pdfDocument.setFitWindow(true);
   ```

### 메뉴 모음 및 도구 모음 숨기기

**개요**: 이러한 속성은 메뉴 표시줄 및 도구 모음과 같은 UI 요소의 가시성을 제어합니다.

#### 단계
1. **속성 액세스**
   ```java
   boolean hideMenuBar = pdfDocument.isHideMenubar();
   System.out.println("Is menu bar hidden? " + hideMenuBar);

   boolean hideToolBar = pdfDocument.isHideToolBar();
   System.out.println("Is tool bar hidden? " + hideToolBar);
   ```

2. **가시성 구성**
   둘 다 숨기려면:
   ```java
   pdfDocument.setHideMenubar(true);
   pdfDocument.setHideToolBar(true);
   ```

### 창 UI 숨기기

**개요**: 이 속성을 true로 설정하면 페이지 내용을 제외한 모든 UI 요소가 숨겨집니다.

#### 단계
1. **부동산 접근**
   ```java
   boolean hideWindowUI = pdfDocument.isHideWindowUI();
   System.out.println("Is window UI hidden? " + hideWindowUI);
   ```

2. **설정 활성화**
   ```java
   pdfDocument.setHideWindowUI(true);
   ```

### 전체 화면이 아닌 페이지 모드

**개요**: 전체 화면 표시를 종료할 때 페이지 모드를 결정합니다.

#### 단계
1. **부동산 접근**
   ```java
   String nonFullScreenPageMode = pdfDocument.getNonFullScreenPageMode();
   System.out.println("Non-full screen page mode: " + nonFullScreenPageMode);
   ```

2. **페이지 모드 설정**
   썸네일로 변경:
   ```java
   pdfDocument.setNonFullScreenPageMode(com.aspose.pdf.Document.PageModeType.Thumbnails);
   ```

### 페이지 레이아웃

**개요**: 페이지가 한 페이지인지, 두 열인지 등 어떻게 배치되는지 정의합니다.

#### 단계
1. **부동산 접근**
   ```java
   String pageLayout = pdfDocument.getPageLayout();
   System.out.println("Page layout: " + pageLayout);
   ```

2. **레이아웃 구성**
   두 개의 열로 설정:
   ```java
   pdfDocument.setPageLayout(com.aspose.pdf.Document.PageLayoutType.TwoColumnLeft);
   ```

### 페이지 모드

**개요**축소판 그림, 윤곽선 등의 옵션을 사용하여 문서를 열 때 표시되는 방식을 제어합니다.

#### 단계
1. **부동산 접근**
   ```java
   String pageMode = pdfDocument.getPageMode();
   System.out.println("Page mode: " + pageMode);
   ```

2. **페이지 모드 설정**
   북마크로 표시:
   ```java
   pdfDocument.setPageMode(com.aspose.pdf.Document.PageModeType.Outlines);
   ```

## 실제 응용 프로그램

PDF 속성을 이해하고 조작하는 것은 다양한 시나리오에서 매우 유용할 수 있습니다.

1. **자동 보고서 생성**: 클라이언트 프레젠테이션에 맞게 창 설정을 사용자 지정합니다.
2. **디지털 출판**: 다국어 문서의 읽기 순서를 제어합니다.
3. **사용자 인터페이스 사용자 정의**: 도구 모음과 같은 UI 요소를 조정하여 사용자 경험을 향상시킵니다.
4. **프레젠테이션 모드**: 더 나은 시청 환경을 위해 전체 화면이 아닌 페이지 모드와 레이아웃 조정을 활용하세요.

## 결론

이 가이드에서는 Aspose.PDF for Java를 사용하여 PDF 속성에 접근하고 수정하는 과정을 안내했습니다. 이러한 기능을 활용하면 애플리케이션과 PDF 파일의 상호 작용을 향상시켜 사용자에게 더욱 맞춤화된 경험을 제공할 수 있습니다.

더 자세히 알아보려면 Aspose.PDF의 광범위한 문서를 살펴보고 프로젝트에 도움이 될 수 있는 추가 기능을 살펴보세요.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}