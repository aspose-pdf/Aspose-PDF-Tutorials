---
"description": "Aspose.PDF for .NET을 사용하여 타임스탬프를 포함한 PDF에 디지털 서명하는 방법을 알아보세요. 이 단계별 가이드에서는 필수 구성 요소, 인증서 설정, 타임스탬프 사용 방법 등을 다룹니다."
"linktitle": "PDF 파일에 타임스탬프를 포함한 디지털 서명"
"second_title": ".NET API 참조용 Aspose.PDF"
"title": "PDF 파일에 타임스탬프를 포함한 디지털 서명"
"url": "/ko/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 파일에 타임스탬프를 포함한 디지털 서명

## 소개

보안 강화를 위해 PDF에 디지털 서명을 하고 타임스탬프를 추가해야 했던 적이 있으신가요? 법률 문서, 계약서 등 보안 인증이 필요한 모든 작업을 할 때 타임스탬프가 포함된 디지털 서명은 신뢰도를 한층 높여줍니다. 이 튜토리얼에서는 Aspose.PDF for .NET을 사용하여 PDF 문서에 타임스탬프와 함께 디지털 서명을 추가하는 방법을 자세히 알아보겠습니다. 걱정하지 마세요. 단계별로 설명해 드리겠습니다!

## 필수 조건

코드를 자세히 살펴보기 전에, 따라 하기 위해 설정해야 할 몇 가지 사항이 있습니다. 시작하기 위한 필수 조건은 다음과 같습니다.

- Aspose.PDF for .NET 라이브러리: 프로젝트에 Aspose.PDF for .NET 라이브러리가 설치되어 있어야 합니다. [여기에서 최신 버전을 다운로드하세요](https://releases.aspose.com/pdf/net/) 또는 NuGet을 통해 프로젝트에 추가하세요.
- PDF 문서: 작업할 샘플 PDF 파일이 필요합니다. 프로젝트 디렉터리에 서명할 파일이 있는지 확인하세요.
- 디지털 인증서(PFX 파일): 디지털 인증서(PFX 파일)가 있는지 확인하십시오. `.pfx` 파일)을 사용하여 문서에 디지털 서명합니다.
- 타임스탬프 URL: 이것은 디지털 서명에 타임스탬프를 첨부하는 데 사용되는 온라인 타임스탬프 서비스입니다. 
- 기본 C# 지식: 전문가가 될 필요는 없지만 C#의 기본 사항을 알면 코드를 이해하고 사용자 정의하는 데 도움이 됩니다.

이 모든 사항을 체크하고 나면 코딩을 시작할 준비가 된 것입니다!

## 패키지 가져오기

시작하려면 다음 네임스페이스를 C# 프로젝트로 가져와야 합니다. 이렇게 하면 관련 Aspose.PDF 클래스와 함수에 액세스할 수 있습니다.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## 1단계: PDF 문서 로드

가장 먼저 해야 할 일은 서명할 PDF 문서를 불러오는 것입니다. 방법은 다음과 같습니다.

```csharp
// 문서 디렉토리 경로를 정의하세요
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// PDF 문서를 로드합니다
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

이 단계는 매우 간단합니다. 서명하려는 문서의 경로를 정의하기만 하면 됩니다. `Document` Aspose.PDF의 클래스가 파일 로딩을 처리합니다.

## 2단계: 디지털 서명 설정

다음으로, PKCS7 클래스를 사용하여 디지털 서명을 생성하고 PFX 파일을 로드합니다. 이 PFX 파일에는 문서 서명에 필요한 인증서와 개인 키가 포함되어 있습니다.

```csharp
// .pfx 파일 경로
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// 서명 객체를 초기화합니다
PdfFileSignature signature = new PdfFileSignature(document);

// 비밀번호로 PFX 파일을 로드합니다
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

이 시점에서 Aspose가 문서 서명에 디지털 인증서를 사용하도록 지시합니다. `PKCS7` 객체가 모든 암호화 작업을 처리하므로, 세세한 사항에 대해 걱정할 필요가 없습니다.

## 3단계: 타임스탬프 설정 추가

강력한 디지털 서명의 핵심 구성 요소 중 하나는 타임스탬프입니다. 타임스탬프는 인증서가 만료된 후에도 문서 서명을 검증할 수 있도록 보장합니다. 온라인 타임스탬프 인증 기관을 사용하여 타임스탬프를 설정해 보겠습니다.

```csharp
// 타임스탬프 설정 정의
TimestampSettings timestampSettings = new TimestampSettings("https://"your_timestamp_url", "user:password");

// PKCS7 개체에 타임스탬프 설정 추가
pkcs.TimestampSettings = timestampSettings;
```

여기서는 서명에 시간과 날짜를 자동으로 추가하는 타임스탬프 서비스의 URL을 지정합니다. 이 작업은 인증 여부와 관계없이 수행할 수 있습니다.

## 4단계: 서명 위치 및 모양 정의

이제 PDF에서 서명이 표시될 위치와 크기를 정의하겠습니다. 페이지에서 서명 상자의 위치와 크기를 사용자 지정할 수 있습니다.

```csharp
// 서명 모양과 위치 정의(지정된 사각형이 있는 페이지 1)
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

여기서는 PDF의 첫 번째 페이지에서 좌표 (100, 100)에 서명을 배치하는 사각형을 정의합니다. 사각형의 너비는 200이고 높이는 100입니다. 디자인에 맞게 이 값을 변경할 수 있습니다.

## 5단계: PDF 문서에 서명하기

모든 설정이 완료되면 이제 PDF에 디지털 서명을 실제로 적용할 차례입니다. 이 단계에서는 인증서, 타임스탬프, 위치 지정을 하나의 간단한 명령으로 통합합니다.

```csharp
// 첫 페이지에 문서에 서명하세요
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

무슨 일이 일어나고 있는지 알려드리겠습니다.
- 1: 이는 서명이 첫 번째 페이지에 적용되어야 함을 나타냅니다.
- "서명 사유": 여기에서 문서에 서명하는 이유를 지정할 수 있습니다.
- "연락처": 서명자의 연락처 정보를 입력하세요.
- "위치": 서명자의 위치를 지정합니다.
- true: 이 부울 값은 서명이 문서에 표시되는지 여부를 나타냅니다.
- rect: 앞서 정의한 사각형은 서명의 크기와 위치를 지정합니다.
- pkcs: PKCS7 개체에는 디지털 인증서와 타임스탬프 설정이 포함되어 있습니다.

## 6단계: 서명된 PDF 저장

문서에 서명한 후에는 저장하기만 하면 됩니다. 원본과 서명된 버전을 모두 보관하려면 새 파일 이름을 선택하세요.

```csharp
// 서명된 PDF 문서를 저장합니다.
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

새로 서명하고 타임스탬프를 찍은 PDF가 지정된 디렉토리에 저장되었습니다!

## 결론

자, 이제 완료되었습니다! Aspose.PDF for .NET을 사용하여 타임스탬프가 포함된 PDF에 디지털 서명을 성공적으로 완료했습니다. 이 과정은 문서의 신뢰성과 무결성을 보장하여 작성자와 수신자 모두에게 안심을 제공합니다. 오늘날 디지털 세상에서 디지털 서명은 점점 더 중요해지고 있으므로, 이 과정을 숙달하는 것은 분명 가치 있는 기술입니다.

## 자주 묻는 질문

### 인증서에 다른 파일 형식을 사용할 수 있나요?  
네, 하지만 튜토리얼에서는 디지털 인증서의 가장 일반적인 형식인 PFX 파일을 사용하는 데 중점을 두고 있습니다.

### 타임스탬프를 적용하려면 인터넷 연결이 필요합니까?  
네, 타임스탬프는 온라인 타임스탬프 기관에서 가져오므로 인터넷 접속이 필요합니다.

### PDF의 여러 페이지에 서명할 수 있나요?  
물론입니다! 수정할 수 있습니다. `signature.Sign()` 여러 페이지를 타겟으로 삼거나 모든 페이지를 반복하는 방법.

### PFX 파일 비밀번호가 올바르지 않으면 어떻게 되나요?  
비밀번호가 틀리면 예외가 발생하므로 비밀번호를 정확하게 입력했는지 확인하세요.

### 서명을 보이지 않게 할 수 있나요?  
네, 통과할 수 있습니다 `false` 에게 `Sign` 서명을 보이지 않게 하려면 메서드의 가시성 매개변수를 변경합니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}