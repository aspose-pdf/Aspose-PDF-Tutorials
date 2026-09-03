---
category: general
date: 2026-02-20
description: Tanulja meg, hogyan telepítsen NuGet csomagokat PowerShell segítségével,
  hogyan futtassa a PowerShellt rendszergazdaként, hogyan listázza a telepített csomagokat,
  és hogyan ellenőrizze a telepített csomagot percek alatt.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: hu
og_description: hogyan telepítsünk NuGet csomagokat PowerShell segítségével, futtassuk
  a PowerShellt rendszergazdaként, listázzuk a telepített csomagokat és ellenőrizzük
  a telepített csomagot – teljes útmutató.
og_title: Hogyan telepítsünk NuGet csomagokat PowerShell segítségével – gyors útmutató
tags:
- PowerShell
- NuGet
- Package Management
title: Hogyan telepítsünk NuGet csomagokat PowerShell segítségével – lépésről lépésre
url: /hu/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hogyan telepítsünk nuget csomagokat PowerShell segítségével – lépésről lépésre

Gondolkodtál már azon, **hogyan telepítsünk nuget** csomagokat anélkül, hogy megnyitnád a Visual Studio‑t? Nem vagy egyedül. Sok CI pipeline‑ban vagy friss gépeken a leggyorsabb megoldás, ha PowerShell‑be lépsz – lehetőleg *run powershell as admin* – és hagyod, hogy a csomagkezelő elvégezze a dolgát.

Ebben az útmutatóban végigvezetünk a teljes folyamaton: a megfelelő konzol megnyitása, egy adott könyvtár verziójának letöltése, és végül annak megerősítése, hogy a csomag valóban megérkezett a rendszeredre. A végére képes leszel **list installed packages** megjeleníteni, tudni **how to verify package** integritását, és magabiztosan tudni, hogy a **verify installed package** lépés minden alkalommal sikeres volt.

## Mit fogsz megtanulni

- Hogyan indítsd el a PowerShell‑t a megfelelő jogosultságokkal.  
- A `Install-Package` parancs pontos szintaxisa a NuGet‑hez.  
- Módszerek a **list installed packages** megjelenítésére és a verziószámok ellenőrzésére.  
- Gyakori buktatók (hiányzó admin jogosultság, verzióeltérések) és hogyan kerüld el őket.  

Nem szükséges előzetes NuGet tapasztalat, csak egy működő Windows gép és egy kis kíváncsiság.

---

## NuGet csomagok telepítése PowerShell segítségével

> **Pro tip:** Ha gyakran adsz hozzá ugyanazokat a csomagokat, fontold meg, hogy egy script‑fájlba helyezed őket, és `-File` kapcsolóval futtatod. Ez megspórolja, hogy ugyanazt a sort újra és újra be kelljen gépelned.

### 1. lépés: PowerShell megnyitása a szükséges jogosultságokkal

Az első dolog, amit meg kell tenned, hogy **run powershell as admin**. Emelt jogok nélkül a `Install-Package` cmdlet csendben meghiúsulhat, vagy olyan megerősítést kérhet, amivel nem szeretnél foglalkozni.

1. Kattints a Start gombra.  
2. Írd be a **PowerShell** szót.  
3. Kattints jobb gombbal a *Windows PowerShell*‑re, és válaszd a **Run as administrator** lehetőséget.  

Megjelenik egy UAC felugró ablak; kattints a **Yes** gombra. Most már van egy jogosultságokkal rendelkező munkameneted a csomagtelepítéshez.

> *Miért admin?*  
> A NuGet a globális csomagok mappájába (`C:\Program Files\PackageManagement\NuGet\Packages` alapértelmezés szerint) ír fájlokat. Ez a hely védett, ezért csak emelt jogosultságú folyamat tud oda írni.

### 2. lépés: A kívánt NuGet csomag és verzió telepítése

A konzol megnyitása után a fő parancs egyszerű:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` a PowerShell burkoló a NuGet kliens körül.  
- `-Version` rögzíti a pontos buildet, amelyre szükséged van, megakadályozva a véletlen frissítéseket.  

Ha kihagyod a `-Version` kapcsolót, a PowerShell a legújabb stabil kiadást tölti le – néha ez megfelelő, néha viszont a pontos verzióra van szükséged, amelyet teszteltél.

#### Mi történik a háttérben?

A PowerShell felkeresi a beállított csomagforrást (alapértelmezés szerint `https://www.nuget.org/api/v2`), és letölti a `.nupkg` fájlt. Ezután kicsomagolja a DLL‑eket a globális csomagok mappájába, és regisztrálja a csomagot a helyi csomagszolgáltatóval. A teljes folyamat általában néhány másodperc alatt befejeződik, hacsak nem lassú a hálózat.

### 3. lépés: Ellenőrizd, hogy a csomag sikeresen települt-e

Most, hogy a csomag a lemezen van, valószínűleg azt kérdezed, **„Hogyan ellenőrizhetem a csomagot?”** A válasz egy egyszerű lekérdezésben rejlik:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

A futtatás eredménye valami ilyesmi:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Ez a kimenet két dolgot erősít meg:

1. A **Aspose.PDF** csomag jelen van.  
2. A verziója megegyezik a kért verzióval, teljesítve a **verify installed package** követelményt.

Ha *minden* csomagot szeretnél látni a gépen, hagyd el a `-Name` szűrőt:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Ez a **list installed packages** nézet hasznos auditokhoz vagy amikor régi könyvtárakat kell tisztítani.

### 4. lépés: Opcionális – szélsőséges esetek kezelése

#### a) Csomag nem található vagy verzióeltérés

Ha a PowerShell *„Package not found”* vagy *„Version not available”* üzenettel válaszol, ellenőrizd a helyesírást és a verziószámot. A NuGet nem különbözteti meg a kis‑ és nagybetűket, de egy felesleges szóköz megtörheti a parancsot.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Futtatás admin jogok nélkül

Ha elfelejted **run powershell as admin**, a cmdlet jogosultsági hibát dob. A megoldás egyszerű: zárd be az ablakot, és nyisd meg újra emelt jogokkal – nincs szükség semmi újratelepítésre.

#### c) Egyedi forrás használata

Vállalati környezetben lehet egy belső NuGet tároló:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

Az ellenőrzési lépés változatlan marad; csak ne felejtsd el a `-Source` kapcsolót megadni a telepítéskor.

---

## Gyors referencia tábla

| Művelet                              | PowerShell command                                          | Miért fontos |
|--------------------------------------|-------------------------------------------------------------|--------------|
| Emelt jogú konzol megnyitása          | *Run PowerShell as Administrator*                           | Szükséges a globális telepítéshez |
| Adott verzió telepítése              | `Install-Package <pkg> -Version <x.y.z>`                    | Biztosítja az ismételhető buildeket |
| Egyetlen csomag listázása            | `Get-Package -Name <pkg>`                                    | Megerősíti a **how to verify package** |
| Minden NuGet csomag listázása        | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| **list installed packages** számára hasznos |
| Elérhető verziók keresése            | `Find-Package <pkg> -AllVersions`                           | Segít, ha a verzió ismeretlen |

## Összegzés

Áttekintettük, **hogyan telepítsünk nuget** csomagokat PowerShell segítségével a kezdetektől a végéig – a konzol megnyitását **run powershell as admin**, egy adott verzió letöltését, és végül a **list installed packages** használatát a **verify installed package** ellenőrzéséhez. Ezekkel a parancsokkal a szerszámosládádban automatizálhatod a könyvtárkezelést bármely Windows gépen, legyen szó CI pipeline‑ról vagy csak egy hiányzó DLL javításáról a fejlesztői gépeden.

Következő lépések? Próbálj meg több csomagot egyetlen scriptbe felvenni, fedezd fel a `-Scope` paramétert a projekt helyi telepítéséhez, vagy kombináld ezeket a parancsokat a `Invoke-Expression`‑nel, hogy egy könnyűsúlyú telepítőt építs a csapatod számára. És ha elakadsz, ne feledd a **how to verify package** lépést – a verzió megtekintése a `Get-Package`‑ben gyakran a leggyorsabb módja a probléma felderítésének.

Boldog PowerShell‑ozást! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}