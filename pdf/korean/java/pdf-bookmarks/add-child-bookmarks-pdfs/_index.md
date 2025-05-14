---
"description": "Aspose.PDF for Java를 사용하여 하위 북마크를 포함한 PDF 문서를 개선하는 방법을 알아보세요. 코드 예제를 포함한 단계별 가이드를 통해 탐색 및 정리 기능을 개선하세요."
"linktitle": "PDF에 자식 북마크 추가"
"second_title": "Aspose.PDF Java PDF 처리 API"
"title": "PDF에 자식 북마크 추가"
"url": "/ko/java/pdf-bookmarks/add-child-bookmarks-pdfs/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF에 자식 북마크 추가


## PDF에 자식 북마크 추가 소개

이 글에서는 Aspose.PDF for Java를 사용하여 PDF 문서에 하위 북마크를 추가하는 방법을 살펴보겠습니다. 하위 북마크는 PDF 문서의 내용을 편리하게 구성하고 탐색할 수 있는 방법으로, 사용자가 문서 내 특정 섹션이나 주제를 더 쉽게 찾을 수 있도록 해줍니다.

## 필수 조건

구현에 들어가기 전에 다음과 같은 전제 조건이 충족되었는지 확인하세요.

- 시스템에 Java 개발 환경이 설치되어 있습니다.
- Java 라이브러리용 Aspose.PDF입니다. 다음에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/java/).

## 환경 설정

1. 제공된 링크에서 Java 라이브러리용 Aspose.PDF를 다운로드하세요.
2. Java 프로젝트에 라이브러리를 추가합니다.

이제 새 PDF 문서를 만들고 자식 책갈피를 단계별로 추가하는 것부터 시작해 보겠습니다.

## 새 PDF 문서 만들기

먼저 PDF 문서를 초기화하고 페이지를 추가해야 합니다. 시작하는 데 필요한 코드는 다음과 같습니다.

```java
// PDF 문서 초기화
Document pdfDocument = new Document();

// PDF에 페이지 추가
pdfDocument.getPages().add();
pdfDocument.getPages().add();
```

이 예에서는 새로운 PDF 문서를 만들고 두 페이지를 추가했습니다.

## 부모 북마크 추가

상위 북마크는 PDF 문서의 주요 섹션이나 카테고리 역할을 합니다. 상위 북마크를 만들어 보겠습니다.

```java
// 부모 북마크 만들기
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);
```

"부모 북마크 1"과 "부모 북마크 2"라는 두 개의 부모 북마크를 추가했습니다.

## 자식 북마크 추가

이제 앞서 만든 부모 북마크에 자식 북마크를 추가할 차례입니다. 자식 북마크는 각 부모 북마크 내의 특정 주제나 하위 섹션을 나타냅니다. 방법은 다음과 같습니다.

```java
// 부모 북마크 1에 자식 북마크 추가
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// 부모 북마크 2에 자식 북마크 추가
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);
```

"부모 북마크 1"과 "부모 북마크 2"에 모두 자식 북마크를 추가했습니다.

## 북마크 모양 사용자 지정

북마크의 텍스트와 스타일을 변경하여 모양을 원하는 대로 설정할 수 있습니다. 또한, 북마크에 아이콘을 추가하여 시각적으로 더욱 보기 좋게 표현할 수 있습니다. 다음은 사용 예시입니다.

```java
// 북마크 모양 사용자 지정
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());
```

이 예에서는 부모 책갈피를 기울임체로 만들고, 자식 책갈피의 텍스트 색상을 녹색으로 변경하고, 자식 책갈피에 기울임체 아이콘을 추가했습니다.

## 이벤트 처리

북마크에는 관련 동작도 지정할 수 있습니다. 예를 들어, 사용자가 북마크를 클릭하면 실행되는 동작을 추가할 수 있습니다. 북마크 클릭 이벤트를 처리하는 방법은 다음과 같습니다.

```java
// 북마크에 작업 추가
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);
```

이 코드에서는 자식 북마크에 "이동" 동작을 추가했는데, 이를 클릭하면 사용자가 PDF의 두 번째 페이지로 이동합니다.

## PDF 저장

필요한 모든 북마크를 추가하고 모양과 동작을 사용자 지정한 후 수정된 PDF 문서를 저장할 수 있습니다.

```java
// PDF 문서를 저장합니다
pdfDocument.save("output.pdf");
```

이제 자식 북마크가 포함된 PDF 문서가 준비되었습니다.

## 완전한 소스 코드

다음은 Java용 Aspose.PDF를 사용하여 PDF 문서에 자식 북마크를 추가하는 전체 소스 코드입니다.

```java
// PDF 문서 초기화
Document pdfDocument = new Document();

// PDF에 페이지 추가
pdfDocument.getPages().add();
pdfDocument.getPages().add();

// 부모 북마크 만들기
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);

// 부모 북마크 1에 자식 북마크 추가
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// 부모 북마크 2에 자식 북마크 추가
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);

// 북마크 모양 사용자 지정
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());

// 북마크에 작업 추가
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);

// PDF 문서를 저장합니다
pdfDocument.save("output.pdf");
```

## 결론

Aspose.PDF for Java를 사용하여 PDF에 하위 북마크를 추가하는 기능은 문서 탐색 및 정리 기능을 향상시키는 강력한 기능입니다. 이 문서에 설명된 단계를 따라 상위 및 하위 북마크를 사용하여 잘 구성된 PDF를 만들고, 모양을 사용자 정의하고, 사용자 경험을 향상시키는 동작을 추가할 수도 있습니다.

## 자주 묻는 질문

### Java용 Aspose.PDF를 어떻게 다운로드할 수 있나요?

Java용 Aspose.PDF는 웹사이트에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/pdf/java/).

### 모든 PDF 뷰어에서 자식 북마크가 지원됩니까?

네, 자식 북마크는 대부분의 최신 PDF 뷰어에서 지원되며 PDF 문서를 탐색하는 데 향상된 사용자 환경을 제공합니다.

### 북마크의 모양을 추가로 사용자 지정할 수 있나요?

네, 문서 디자인에 맞게 텍스트 스타일, 색상, 아이콘을 조정하여 북마크의 모양을 사용자 지정할 수 있습니다.

### 북마크에 어떤 다른 작업을 추가할 수 있나요?

"이동" 동작 외에도 웹 링크를 여는 "URI" 동작이나 북마크를 클릭하면 사용자 정의 스크립트를 실행하는 "JavaScript" 동작과 같은 동작을 추가할 수 있습니다.

### Aspose.PDF for Java는 상업 프로젝트에 적합합니까?

네, Aspose.PDF for Java는 개인 및 상업 프로젝트 모두에 적합하며, PDF 조작 및 생성을 위한 광범위한 기능을 제공합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}