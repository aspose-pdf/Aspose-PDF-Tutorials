---
category: general
date: 2026-03-03
description: วิธีตรวจสอบการติดตั้งแพ็กเกจ NuGet ใน PowerShell เรียนรู้การเรียกใช้
  PowerShell ด้วยสิทธิผู้ดูแลระบบ การติดตั้งเวอร์ชันเฉพาะ และการจัดการแพ็กเกจอย่างมีประสิทธิภาพ.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: th
og_description: วิธีตรวจสอบการติดตั้งแพ็กเกจ NuGet ใน PowerShell คู่มือขั้นตอนนี้จะแสดงวิธีการเรียกใช้
  PowerShell ด้วยสิทธิผู้ดูแลระบบ, ติดตั้งเวอร์ชันที่ต้องการ, และยืนยันว่าแพ็กเกจมีอยู่
og_title: วิธีตรวจสอบการติดตั้งแพคเกจ NuGet ด้วย PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: วิธีตรวจสอบการติดตั้งแพ็กเกจ NuGet ด้วย PowerShell
url: /th/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตรวจสอบการติดตั้งแพคเกจ NuGet ด้วย PowerShell

การตรวจสอบการติดตั้งแพคเกจ NuGet ใน PowerShell เป็นงานทั่วไปสำหรับผู้ดูแลระบบ Windows หากคุณเคยสงสัยว่าแพคเกจนั้นได้ติดตั้งลงในระบบของคุณจริงหรือไม่ คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนการตรวจสอบการติดตั้งอย่างแม่นยำ—ไม่มีการคาดเดา  

ในไม่กี่นาทีต่อไป เราจะพาคุณผ่านการเรียกใช้ PowerShell ด้วยสิทธิ์ผู้ดูแลระบบ การดึงเวอร์ชันเฉพาะของแพคเกจ และสุดท้ายการยืนยันว่าแพคเกจมีอยู่ในเครื่องของคุณ คุณยังจะได้เรียนรู้เคล็ดลับเล็กน้อยสำหรับ **PowerShell package management** ประจำวันที่ช่วยให้สภาพแวดล้อมของคุณเป็นระเบียบ  

ก่อนที่เราจะเริ่มลงลึก ตรวจสอบให้แน่ใจว่าคุณมีเครื่อง Windows ที่ติดตั้ง PowerShell 7 (หรือ Windows PowerShell 5.1) และมีการเชื่อมต่ออินเทอร์เน็ต ไม่จำเป็นต้องใช้เครื่องมือเพิ่มเติม; ทุกอย่างทำงานโดยตรงจากผู้ให้บริการ PackageManagement ที่มาพร้อมในระบบ  

---

![ภาพหน้าต่าง PowerShell ที่ยกระดับพร้อมคำสั่ง Get-Package](/images/verify-installation.png "ภาพหน้าจอแสดงวิธีตรวจสอบการติดตั้งในหน้าต่าง PowerShell ที่ยกระดับ")

## ขั้นตอนที่ 1: เรียกใช้ PowerShell ด้วยสิทธิ์ผู้ดูแลระบบ  

การเรียกใช้ PowerShell ด้วยสิทธิ์ผู้ดูแลระบบเป็นแนวป้องกันแรกสุดต่อปัญหาที่เกี่ยวข้องกับสิทธิ์ เมื่อคุณ **run PowerShell as admin** คำสั่ง `Install-Package` จะสามารถเขียนไปยังโฟลเดอร์ Program Files และลงทะเบียนแพคเกจในแคตาล็อกระดับระบบได้  

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **เคล็ดลับ:** ปักหมุดทางลัด “Windows PowerShell (Admin)” ไว้บนทาสก์บาร์ เพียงคลิกเดียวคุณก็พร้อมใช้งาน  

### ทำไมการยกระดับจึงสำคัญ  

หากไม่มีการยกระดับ `Install-Package` อาจย้อนกลับไปยังตำแหน่งที่กำหนดให้ผู้ใช้โดยเงียบ ๆ ซึ่งอาจทำให้ `Get-Package` สับสนในภายหลังเนื่องจากโดยค่าเริ่มต้นมันมองหาในระดับระบบ การยกระดับรับประกันว่าแพคเกจจะปรากฏในตำแหน่งที่สคริปต์ส่วนใหญ่คาดหวัง  

---

## ขั้นตอนที่ 2: ติดตั้งเวอร์ชันเฉพาะของแพคเกจ NuGet  

บ่อยครั้งคุณอาจไม่ต้องการเวอร์ชันล่าสุด แต่ต้องการเวอร์ชันที่ตรวจสอบแล้วว่าดีและโครงการของคุณได้ทดสอบกับมันแล้ว รูปแบบ **install specific version** ทำได้ง่ายด้วยฟลัก `-Version`  

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### แยกส่วนคำสั่ง  

| Parameter | ทำหน้าที่อะไร | ทำไมคุณถึงต้องใช้ |
|-----------|--------------|-----------------|
| `-Version 25.3` | กำหนดหมายเลขบิลด์ที่แน่นอน | รับประกันการสร้างที่ทำซ้ำได้ |
| `-ProviderName NuGet` | บอก PowerShell ว่าจะใช้ผู้ให้บริการใด | ป้องกันความสับสนหากมีผู้ให้บริการหลายตัวลงทะเบียน |
| `-Scope AllUsers` | ติดตั้งสำหรับทุกบัญชีบนเครื่อง | ทำงานร่วมกับการค้นหา `Get-Package` ระดับระบบ |
| `-Force` | ปิดการแสดงพรอมต์ (มีประโยชน์ในสคริปต์) | ทำให้การอัตโนมัตินุ่มนวล |

> **ระวัง:** หากคุณละเว้น `-Version` PowerShell จะดึงแพคเกจรุ่นล่าสุด ซึ่งอาจทำให้เกิดการเปลี่ยนแปลงที่ทำให้โค้ดเสียหาย  

---

## ขั้นตอนที่ 3: ตรวจสอบการติดตั้ง  

ตอนนี้มาถึงช่วงเวลาที่สำคัญ: **how to verify installation** วิธีที่ตรงที่สุดคือให้ PowerShell แสดงแพคเกจที่คุณเพิ่งติดตั้ง  

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

คุณควรเห็นผลลัพธ์ที่คล้ายกับ:  

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

หากคำสั่งไม่คืนค่าใด ๆ ให้ลองใช้การค้นหาแบบผู้ใช้:  

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### วิธีการตรวจสอบทางเลือก  

1. **ตรวจสอบโฟลเดอร์โมดูล** – แพคเกจจะถูกเก็บไว้ที่ `C:\Program Files\PackageManagement\Packages\`. มองหาโฟลเดอร์ที่ชื่อ `Aspose.PDF.25.3`.  
2. **ใช้ `Find-Package`** – คำสั่งนี้จะค้นหาในรีโพซิทอรีและยืนยันว่าเวอร์ชันนั้นพร้อมใช้งาน:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **ตรวจสอบด้วย .NET** – โหลดแอสเซมบลีใน PowerShell เพื่อให้แน่ใจว่า DLL สามารถโหลดได้:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

หากการตรวจสอบใด ๆ เหล่านี้สำเร็จ คุณได้ **verified installation** อย่างสำเร็จแล้ว  

---

## ปัญหาที่พบบ่อยและวิธีหลีกเลี่ยง  

- **Missing NuGet provider** – เริ่มต้นด้วยการรัน `Install-PackageProvider -Name NuGet -Force` ก่อน.  
- **ExecutionPolicy blocks** – ตั้งค่าแบบชั่วคราว `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` สำหรับเซสชัน.  
- **Network proxy issues** – ใช้พารามิเตอร์ `-Proxy` และ `-ProxyCredential` หากสภาพแวดล้อมของคุณอยู่หลังพร็อกซีขององค์กร.  
- **Version conflicts** – เมื่อมีหลายเวอร์ชันอยู่ ให้ระบุ `-RequiredVersion` ใน `Get-Package` เพื่อแยกความแตกต่าง.  

---

## รวมทุกอย่างเข้าด้วยกัน – สคริปต์เต็มรูปแบบ  

ด้านล่างเป็นสคริปต์พร้อมรันที่รวมสามขั้นตอนเข้าด้วยกัน มีการจัดการข้อผิดพลาดและพิมพ์ข้อความยืนยันความสำเร็จที่เป็นมิตร  

```powershell
<# 
.SYNOPSIS
    Installs a specific version of a NuGet package and verifies the installation.
.DESCRIPTION
    Demonstrates how to run PowerShell as admin, install a specific version, 
    and confirm that the package is present using Get-Package.
#>

# Ensure we are running elevated
if (-not ([Security.Principal.WindowsPrincipal] `
        [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
        [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Warning "Please run this script in an elevated PowerShell session."
    exit 1
}

$packageName = 'Aspose.PDF'
$packageVersion = '25.3'

try {
    Write-Host "Installing $packageName version $packageVersion..."
    Install-Package $packageName -Version $packageVersion `
        -ProviderName NuGet -Scope AllUsers -Force -ErrorAction Stop

    Write-Host "Installation completed. Verifying..."
    $pkg = Get-Package -Name $packageName -ProviderName NuGet -ErrorAction Stop

    if ($pkg.Version -eq $packageVersion) {
        Write-Host "`n✅ Successfully verified installation of $packageName $packageVersion."
    } else {
        Write-Error "Version mismatch: Expected $packageVersion but got $($pkg.Version)."
    }
}
catch {
    Write-Error "An error occurred: $_"
}
```

การรันสคริปต์จะได้บรรทัดที่ชัดเจนว่า “✅ Successfully verified installation…” ซึ่งยืนยันว่า **how to verify installation** ทำงานจากต้นจนจบ  

---

## สรุป  

ตอนนี้คุณรู้ **how to verify installation** ของแพคเกจ NuGet ใด ๆ ด้วย PowerShell ตั้งแต่การเปิดเซสชันที่ยกระดับ การติดตั้งเวอร์ชันที่ต้องการ ไปจนถึงการยืนยันการมีอยู่ของแพคเกจ การเชี่ยวชาญขั้นตอนเหล่านี้ทำให้คุณมั่นใจในกระบวนการ **PowerShell package management** ของคุณและป้องกันอาการ “ดูเหมือนติดตั้งแล้วแต่จริง ๆ ไม่ได้” ที่มักทำให้ผู้พัฒนา Windows ปวดหัว  

ต่อไปคุณจะทำอะไร? ลองเปลี่ยน `Aspose.PDF` เป็นไลบรารีอื่น ทดลองใช้ `-Scope CurrentUser` หรือเขียนสคริปต์ติดตั้งหลายแพคเกจพร้อมกันสำหรับเครื่องทำงานใหม่ และหากเจอปัญหา ให้จำเคล็ดลับการแก้ไขปัญหาข้างต้น—โดยเฉพาะการตรวจสอบผู้ให้บริการและนโยบายการดำเนินการ  

สคริปต์ให้สนุกและขอให้การติดตั้งของคุณตรวจสอบได้เสมอ!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}