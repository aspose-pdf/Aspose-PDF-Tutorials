---
"description": "Aspose.PDF for .NET을 사용하여 스마트 카드를 사용하여 PDF 파일에 서명하는 방법을 알아보세요. 안전한 디지털 서명을 위한 단계별 가이드를 따라해 보세요."
"linktitle": "PDF 파일 서명을 사용하여 스마트 카드로 서명"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일 서명을 사용하여 스마트 카드로 서명"
"url": "/ko/net/programming-with-security-and-signatures/sign-with-smart-card-using-pdf-file-signature/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일 서명을 사용하여 스마트 카드로 서명

## 소개

디지털 시대에 문서 보안은 그 어느 때보다 중요합니다. 계약서, 합의서, 또는 민감한 정보 등 어떤 문서든 문서의 진위 여부와 변조 여부를 확인하는 것이 무엇보다 중요합니다. 바로 디지털 서명입니다! 오늘은 Aspose.PDF for .NET을 사용하여 스마트 카드를 사용하여 PDF 파일에 서명하는 방법을 자세히 알아보겠습니다. 이 강력한 라이브러리를 통해 개발자는 PDF 문서를 효율적으로 조작하고 생성할 수 있으며, 보안 디지털 서명도 추가할 수 있습니다. 자, 스마트 카드를 준비하고 시작해 보세요!

## 필수 조건

PDF 파일 서명의 세부적인 내용을 살펴보기 전에, 필요한 모든 것이 있는지 확인해 보겠습니다. 준비에 도움이 될 체크리스트를 소개합니다.

1. .NET용 Aspose.PDF: Aspose.PDF 라이브러리가 설치되어 있는지 확인하세요. 다음에서 다운로드할 수 있습니다. [대지](https://releases.aspose.com/pdf/net/).
2. Visual Studio: .NET 코드를 작성하고 실행할 수 있는 개발 환경입니다.
3. 스마트 카드: 유효한 디지털 인증서가 설치된 스마트 카드가 필요합니다.
4. C#에 대한 기본적인 이해: C# 프로그래밍에 익숙하면 이 언어로 코드 조각을 작성할 수 있으므로 유익합니다.
5. PDF 문서: 샘플 PDF 파일(예: `blank.pdf`) 서명 과정을 테스트해 보세요.

이러한 전제 조건을 갖추면 이제 코드를 살펴볼 준비가 되었습니다!

## 패키지 가져오기

먼저 필요한 패키지를 가져오겠습니다. 프로젝트에 Aspose.PDF 라이브러리에 대한 참조를 추가해야 합니다. 방법은 다음과 같습니다.

1. Visual Studio를 엽니다.
2. 새로운 프로젝트를 만들거나 기존 프로젝트를 엽니다.
3. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 다음을 선택합니다. `Manage NuGet Packages`.
4. 검색 `Aspose.PDF` 최신 버전을 설치하세요.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

이제 필요한 패키지를 가져왔으니 코드를 단계별로 나누어 보겠습니다.

## 1단계: 문서 설정

첫 번째 단계는 서명할 PDF 문서를 설정하는 것입니다. 방법은 다음과 같습니다.

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
Document doc = new Document(dataDir + "blank.pdf");
```
이 스니펫에서는 문서 디렉토리 경로를 정의하고 인스턴스를 생성합니다. `Document` 샘플 PDF 파일을 사용하는 클래스 `blank.pdf`. 교체를 꼭 하세요 `"YOUR DOCUMENTS DIRECTORY"` PDF가 위치한 실제 경로를 사용합니다.

## 2단계: PdfFileSignature 초기화

다음으로, 우리는 초기화할 것입니다 `PdfFileSignature` 서명 과정을 처리하는 클래스입니다.

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature())
{
    pdfSign.BindPdf(doc);
```
여기서 우리는 인스턴스를 생성합니다 `PdfFileSignature` PDF 문서에 바인딩합니다. 이렇게 하면 서명을 위한 문서 준비가 완료됩니다.

## 3단계: 스마트 카드 인증서에 액세스

이제 중요한 단계, 스마트 카드에 저장된 디지털 인증서에 접근하는 단계입니다. 방법은 다음과 같습니다.

### 인증서 저장소 열기

```csharp
System.Security.Cryptography.X509Certificates.X509Store store = new System.Security.Cryptography.X509Certificates.X509Store(System.Security.Cryptography.X509Certificates.StoreLocation.CurrentUser);
store.Open(System.Security.Cryptography.X509Certificates.OpenFlags.ReadOnly);
```
현재 사용자 프로필에 있는 인증서 저장소를 엽니다. 이를 통해 스마트 카드에 있는 인증서를 포함하여 사용자 기기에 설치된 인증서에 접근할 수 있습니다.

### 인증서를 선택하세요

```csharp
System.Security.Cryptography.X509Certificates.X509Certificate2Collection sel =
    System.Security.Cryptography.X509Certificates.X509Certificate2UI.SelectFromCollection(
        store.Certificates, null, null, System.Security.Cryptography.X509Certificates.X509SelectionFlag.SingleSelection);
```
이 코드는 사용자에게 컬렉션에서 인증서를 선택하도록 요청합니다. 사용자 인터페이스에 사용 가능한 모든 인증서가 표시되어 스마트 카드와 연결된 인증서를 선택할 수 있습니다.

## 4단계: 외부 서명 만들기

인증서를 선택한 후 다음 단계는 선택한 인증서를 사용하여 외부 서명을 만드는 것입니다.

```csharp
Aspose.Pdf.Forms.ExternalSignature externalSignature = new Aspose.Pdf.Forms.ExternalSignature(sel[0]);
```
여기서 우리는 인스턴스를 생성합니다 `ExternalSignature` 선택한 인증서를 사용합니다. 이 개체는 PDF 문서에 서명하는 데 사용됩니다.

## 5단계: 서명 모양 설정

이제 서명 모양을 설정해 보겠습니다. 여기에서 문서에 서명이 어떻게 표시되는지 사용자 지정할 수 있습니다.

```csharp
pdfSign.SignatureAppearance = dataDir + "demo.png";
```
이 스니펫에서는 이미지 파일(로고나 서명 그래픽 등) 경로를 제공하여 서명의 모양을 지정합니다. `"demo.png"` 실제로 사용하고자 하는 이미지와 함께.

## 6단계: PDF에 서명하기

모든 것이 설정되었으니 이제 PDF 문서에 서명할 시간입니다!

```csharp
pdfSign.Sign(1, "Reason", "Contact", "Location", true, new System.Drawing.Rectangle(100, 100, 200, 200), externalSignature);
pdfSign.Save(dataDir + "externalSignature2.pdf");
```
이 단계에서는 다음을 호출합니다. `Sign` 우리의 방법 `pdfSign` 객체입니다. 각 매개변수의 의미는 다음과 같습니다.
- `1`: 서명이 나타날 페이지 번호입니다.
- `"Reason"`: 문서에 서명하는 이유.
- `"Contact"`: 서명자의 연락처 정보.
- `"Location"`: 서명자의 위치.
- `true`: 표시되는 서명을 만들지 여부를 나타냅니다.
- `new System.Drawing.Rectangle(100, 100, 200, 200)`: PDF에서 서명의 위치와 크기.
- `externalSignature`: 이전에 생성한 서명 객체입니다.

마지막으로 서명된 문서를 다음과 같이 저장합니다. `externalSignature2.pdf`.

## 7단계: 서명 확인

문서에 서명한 후에는 서명이 유효한지 확인하는 것이 중요합니다. 방법은 다음과 같습니다.

### 확인 프로세스 초기화

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature(new Document(dataDir + "externalSignature2.pdf")))
{
    IList<string> sigNames = pdfSign.GetSignNames();
```
우리는 새로운 인스턴스를 생성합니다 `PdfFileSignature` 서명된 문서에 대해. 그런 다음 문서에 있는 모든 서명의 이름을 검색합니다.

### 서명 유효성 확인

```csharp
for (int index = 0; index <= sigNames.Count - 1; index++)
{
    if (!pdfSign.VerifySigned(sigNames[index]) || !pdfSign.VerifySignature(sigNames[index]))
    {
        throw new ApplicationException("Not verified");
    }
}
```
각 서명 이름을 순회하며 유효성을 검증합니다. 서명 중 검증에 실패하는 서명이 있으면 해당 서명이 유효하지 않음을 나타내는 예외가 발생합니다.

## 결론

자, 이제 완료되었습니다! Aspose.PDF for .NET을 사용하여 스마트 카드를 사용하여 PDF 문서에 성공적으로 서명했습니다. 이 과정은 문서의 보안을 강화할 뿐만 아니라 오늘날 디지털 세상에서 매우 중요한 신뢰성을 더해줍니다. 계약서, 법률 문서 또는 기타 민감한 정보를 다룰 때 디지털 서명 구현 방법을 아는 것은 매우 중요한 기술입니다. 

## 자주 묻는 질문

### .NET용 Aspose.PDF란 무엇인가요?
.NET용 Aspose.PDF는 개발자가 .NET 애플리케이션 내에서 PDF 문서를 만들고, 조작하고, 변환할 수 있는 강력한 라이브러리입니다.

### PDF에 서명하려면 스마트 카드가 필요한가요?
스마트 카드는 필수는 아니지만, 보안을 강화하는 디지털 서명에 사용하는 것이 좋습니다.

### 모든 PDF 파일을 서명에 사용할 수 있나요?
네, 모든 PDF 파일을 사용하실 수 있지만, 암호로 보호되어 있지 않은지 확인하세요. 암호로 보호되어 있다면 먼저 잠금을 해제해야 합니다.

### 디지털 인증서가 없으면 어떻게 하나요?
신뢰할 수 있는 인증 기관(CA)에서 디지털 인증서를 얻거나 테스트 목적으로 자체 서명된 인증서를 사용할 수 있습니다.

### Aspose.PDF의 평가판이 있나요?
네, 무료 평가판을 다운로드할 수 있습니다. [Aspose 웹사이트](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}