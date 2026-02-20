---
category: general
date: 2026-02-20
description: PowerShell을 사용해 NuGet 패키지를 설치하고, PowerShell을 관리자 권한으로 실행하며, 설치된 패키지를
  나열하고, 몇 분 안에 설치된 패키지를 확인하는 방법을 배워보세요.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: ko
og_description: PowerShell를 사용하여 NuGet 패키지를 설치하는 방법, PowerShell를 관리자 권한으로 실행하기, 설치된
  패키지 목록 확인 및 설치된 패키지 검증—전체 단계별 안내.
og_title: PowerShell을 사용하여 NuGet 패키지 설치 방법 – 빠른 가이드
tags:
- PowerShell
- NuGet
- Package Management
title: PowerShell을 사용하여 NuGet 패키지를 설치하는 방법 – 단계별
url: /ko/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerShell를 사용하여 NuGet 패키지를 설치하는 방법 – 단계별

Visual Studio를 열지 않고 **how to install nuget** 패키지를 설치하는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 많은 CI 파이프라인이나 새 머신에서는 가장 빠른 방법이 PowerShell에 들어가는 것입니다—가능하면 *run powershell as admin*—하고 패키지 관리자가 작업을 수행하도록 합니다.

이 튜토리얼에서는 전체 과정을 단계별로 살펴보겠습니다: 올바른 콘솔을 열고, 라이브러리의 특정 버전을 다운로드하고, 마지막으로 패키지가 시스템에 제대로 설치되었는지 확인합니다. 끝까지 하면 **list installed packages**를 수행하고, **how to verify package** 무결성을 확인하는 방법을 알게 되며, **verify installed package** 단계가 매번 성공했는지 확신할 수 있습니다.

## 배울 내용

- 올바른 권한으로 PowerShell을 실행하는 방법.  
- `Install-Package` 명령 구문을 정확히 사용하는 방법 (NuGet용).  
- **list installed packages**를 확인하고 버전 번호를 확인하는 방법.  
- 일반적인 함정(관리자 권한 누락, 버전 불일치) 및 이를 피하는 방법.  

NuGet에 대한 사전 경험은 필요 없으며, 작동하는 Windows 머신과 약간의 호기심만 있으면 됩니다.

---

## PowerShell를 사용하여 NuGet 패키지를 설치하는 방법

> **Pro tip:** 동일한 패키지를 자주 추가한다면 스크립트 파일에 넣고 `-File` 옵션으로 실행하는 것을 고려하세요. 같은 줄을 반복해서 입력하는 수고를 덜어줍니다.

### 단계 1: 필요한 권한으로 PowerShell 열기

가장 먼저 해야 할 일은 **run powershell as admin** 하는 것입니다. 권한이 상승되지 않으면 `Install-Package` cmdlet이 조용히 실패하거나 원하지 않는 확인을 요구할 수 있습니다.

1. 시작 버튼을 클릭합니다.  
2. **PowerShell**을 입력합니다.  
3. *Windows PowerShell*을 오른쪽 클릭하고 **Run as administrator**를 선택합니다.  

UAC 프롬프트가 표시되면 **Yes**를 클릭합니다. 이제 패키지 설치를 위한 권한이 부여된 세션이 준비되었습니다.

> *왜 관리자 권한인가?*  
> NuGet은 전역 패키지 폴더(`C:\Program Files\PackageManagement\NuGet\Packages`)에 파일을 씁니다(기본값). 이 위치는 보호되어 있어 상승된 프로세스만 쓸 수 있습니다.

### 단계 2: 원하는 NuGet 패키지와 버전 설치

With the console open, the core command is straightforward:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package`는 NuGet 클라이언트의 PowerShell 래퍼입니다.  
- `-Version`은 필요한 정확한 빌드를 지정하여 실수로 업그레이드되는 것을 방지합니다.  

If you omit `-Version`, PowerShell will pull the latest stable release—sometimes that’s fine, sometimes you want the exact version you tested against.

#### 내부에서 무슨 일이 일어나나요?

PowerShell은 구성된 패키지 소스에 연결합니다(기본값은 `https://www.nuget.org/api/v2`) 그리고 `.nupkg` 파일을 다운로드합니다. 그런 다음 DLL을 전역 패키지 폴더에 추출하고 로컬 패키지 제공자에 패키지를 등록합니다. 전체 과정은 일반적으로 몇 초 안에 완료되며, 네트워크가 느린 경우를 제외합니다.

### 단계 3: 패키지가 성공적으로 설치되었는지 확인

Now that the package is on disk, you’ll probably ask, **“How do I verify the package?”** The answer lives in a simple query:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Running this returns something like:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

That output confirms two things:

1. The package **Aspose.PDF**가 존재합니다.  
2. Its version matches the one you asked for, satisfying the **verify installed package** requirement.  

If you want to see *every* package on the machine, drop the `-Name` filter:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

This **list installed packages** view is handy for audits or when you need to clean up old libraries.

### 단계 4: 선택 사항 – 예외 상황 처리

#### a) 패키지를 찾을 수 없거나 버전 불일치

PowerShell가 *“Package not found”* 또는 *“Version not available”* 라고 응답하면 철자와 버전 번호를 다시 확인하세요. NuGet은 대소문자를 구분하지 않지만, 불필요한 공백이 명령을 깨뜨릴 수 있습니다.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) 관리자 권한 없이 실행

**run powershell as admin**를 잊어버리면 cmdlet이 권한 오류를 발생시킵니다. 해결 방법은 창을 닫고 권한이 상승된 상태로 다시 여는 것이며, 재설치할 필요는 없습니다.

#### c) 사용자 지정 소스 사용

In corporate environments you might have an internal NuGet feed:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

The verification step stays the same; just remember to include `-Source` when you install.

---

## 빠른 참고 표

| Action                              | PowerShell command                                          | Why it matters |
|-------------------------------------|-------------------------------------------------------------|----------------|
| 권한 상승 콘솔 열기               | *Run PowerShell as Administrator*                           | 전역 설치에 필요 |
| 특정 버전 설치                     | `Install-Package <pkg> -Version <x.y.z>`                    | 재현 가능한 빌드 보장 |
| 단일 패키지 목록                   | `Get-Package -Name <pkg>`                                    | **how to verify package** 확인 |
| 전체 NuGet 패키지 목록             | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| **list installed packages**에 유용 |
| 사용 가능한 버전 검색               | `Find-Package <pkg> -AllVersions`                           | 버전이 알려지지 않았을 때 도움 |

---

## 결론

우리는 **how to install nuget** 패키지를 PowerShell로 시작부터 끝까지 다루었습니다—콘솔을 **run powershell as admin**로 열고, 특정 버전을 가져오며, 마지막으로 **list installed packages**를 사용해 **verify installed package**를 수행합니다. 이러한 명령을 도구 상자에 넣으면 CI 파이프라인을 스크립팅하든 개발 환경에서 누락된 DLL을 수정하든 모든 Windows 머신에서 라이브러리 관리를 자동화할 수 있습니다.

다음 단계는? 여러 패키지를 하나의 스크립트에 추가해 보고, 프로젝트에 로컬로 설치하기 위해 `-Scope` 매개변수를 탐색하거나, `Invoke-Expression`과 결합해 팀을 위한 경량 설치 프로그램을 만들어 보세요. 문제가 발생하면 **how to verify package** 단계를 기억하세요—`Get-Package`에서 버전을 확인하는 것이 문제를 가장 빠르게 찾는 방법입니다.

PowerShell 즐겁게 사용하세요! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}