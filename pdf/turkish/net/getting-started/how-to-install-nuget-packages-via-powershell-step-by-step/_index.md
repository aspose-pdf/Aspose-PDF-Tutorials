---
category: general
date: 2026-02-20
description: PowerShell kullanarak NuGet paketlerini nasıl kuracağınızı, PowerShell'i
  yönetici olarak çalıştırmayı, kurulu paketleri listelemeyi ve kurulan paketi dakikalar
  içinde doğrulamayı öğrenin.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: tr
og_description: PowerShell kullanarak NuGet paketlerini nasıl kurulur, PowerShell'i
  yönetici olarak çalıştırma, kurulu paketleri listeleme ve kurulan paketi doğrulama—tam
  bir rehber.
og_title: PowerShell ile NuGet paketlerini nasıl kurulur – hızlı rehber
tags:
- PowerShell
- NuGet
- Package Management
title: PowerShell ile NuGet paketlerini nasıl kurulur – adım adım
url: /tr/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerShell ile NuGet paketlerini nasıl kurulur – adım adım

Visual Studio'yu açmadan **nuget paketlerini nasıl kuracağınızı** hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok CI boru hattında ya da yeni makinelerde en hızlı yol PowerShell'e geçmek—tercihen *run powershell as admin*—ve paket yöneticisinin işini yapmasına izin vermektir.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: doğru konsolu açmak, bir kütüphanenin belirli bir sürümünü indirmek ve sonunda paketin gerçekten sisteminize yüklendiğini doğrulamak. Sonunda **list installed packages** komutunu kullanabilecek, **how to verify package** bütünlüğünü nasıl kontrol edeceğinizi öğrenecek ve **verify installed package** adımının her seferinde başarılı olduğunu göreceksiniz.

## Öğrenecekleriniz

- PowerShell'i doğru yetkilerle nasıl başlatacağınız.  
- NuGet için tam `Install-Package` komut sözdizimi.  
- **list installed packages** komutuyla paketleri listeleme ve sürüm numaralarını doğrulama.  
- Yaygın tuzaklar (yönetici hakları eksikliği, sürüm uyumsuzlukları) ve bunlardan nasıl kaçınılacağı.  

NuGet ile ilgili önceden bir deneyime sahip olmanız gerekmez, sadece çalışan bir Windows makinesi ve biraz merak yeterli.

---

## PowerShell Kullanarak NuGet Paketlerini Nasıl Kurulur

> **Pro tip:** Aynı paketleri sık sık ekliyorsanız, bir script dosyasına ekleyip `-File` ile çalıştırmayı düşünün. Aynı satırı tekrar tekrar yazmaktan kurtulursunuz.

### Adım 1: Gerekli izinlerle PowerShell'i açın

İlk yapmanız gereken **run powershell as admin**. Yetkilendirilmemiş bir oturumda `Install-Package` cmdlet'i sessizce başarısız olabilir veya istemediğiniz onayları sorabilir.

1. Başlat düğmesine tıklayın.  
2. **PowerShell** yazın.  
3. *Windows PowerShell* üzerine sağ‑tıklayın ve **Run as administrator** seçeneğini seçin.  

UAC penceresi görünecek; **Yes**'e tıklayın. Artık paket kurulumuna hazır yetkili bir oturumunuz var.

> *Neden yönetici?*  
> NuGet, varsayılan olarak global paket klasörüne (`C:\Program Files\PackageManagement\NuGet\Packages`) dosyalar yazar. Bu konum korumalıdır, bu yüzden yalnızca yükseltilmiş bir süreç yazabilir.

### Adım 2: İstenen NuGet paketini ve sürümünü kurun

Konsol açıkken temel komut oldukça basittir:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package`, NuGet istemcisinin PowerShell sarmalayıcısıdır.  
- `-Version`, ihtiyacınız olan tam yapıyı sabitleyerek istenmeyen yükseltmeleri önler.  

`-Version` parametresini atladığınızda PowerShell en son kararlı sürümü çeker—bazen bu yeterli olur, bazen ise test ettiğiniz tam sürümü istiyorsunuz.

#### Bu işlem arka planda ne yapar?

PowerShell, yapılandırılmış paket kaynağına (varsayılan olarak `https://www.nuget.org/api/v2`) bağlanır ve `.nupkg` dosyasını indirir. Ardından DLL'leri global paket klasörüne çıkarır ve paketi yerel paket sağlayıcısına kaydeder. Bu süreç genellikle birkaç saniye içinde tamamlanır, yavaş bir ağda daha uzun sürebilir.

### Adım 3: Paketin başarılı bir şekilde kurulduğunu doğrulayın

Paket artık diskte olduğuna göre muhtemelen **“Paketi nasıl doğrularım?”** diye soracaksınız. Cevap basit bir sorguda saklı:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Bu komutu çalıştırdığınızda aşağıdakine benzer bir çıktı alırsınız:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Bu çıktı iki şeyi onaylar:

1. **Aspose.PDF** paketinin mevcut olduğu.  
2. Sürümünün istediğiniz sürümle eşleştiği, **verify installed package** gereksinimini karşıladığı.

Makinedeki *tüm* paketleri görmek isterseniz `-Name` filtresini kaldırın:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Bu **list installed packages** görünümü denetimler için ya da eski kütüphaneleri temizlemeniz gerektiğinde çok kullanışlıdır.

### Adım 4: Opsiyonel – Kenar durumlarını ele alma

#### a) Paket bulunamadı veya sürüm uyuşmazlığı

PowerShell *“Package not found”* ya da *“Version not available”* mesajı verirse, paket adını ve sürüm numarasını tekrar kontrol edin. NuGet büyük/küçük harfe duyarsızdır, ancak fazladan bir boşluk komutu bozabilir.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Yönetici hakları olmadan çalıştırma

**run powershell as admin** unutursanız, cmdlet bir izin hatası verir. Çözüm, pencereyi kapatıp yükseltilmiş haklarla yeniden açmak; hiçbir şeyi yeniden kurmanıza gerek yok.

#### c) Özel bir kaynak kullanma

Kurumsal ortamlarda iç bir NuGet beslemeniz olabilir:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

Doğrulama adımı aynı kalır; sadece kurarken `-Source` eklemeyi unutmayın.

---

## Hızlı referans tablosu

| İşlem                               | PowerShell komutu                                            | Neden önemli |
|-------------------------------------|-------------------------------------------------------------|--------------|
| Yükseltilmiş konsolu aç              | *PowerShell'i Yönetici olarak Çalıştır*                     | Global kurulum için gerekli |
| Belirli bir sürümü kur              | `Install-Package <pkg> -Version <x.y.z>`                    | Tekrarlanabilir derlemeler sağlar |
| Tek bir paketi listele              | `Get-Package -Name <pkg>`                                    | **how to verify package** doğrulamasını sağlar |
| Tüm NuGet paketlerini listele       | `Get-Package \| Where-Object {$_.ProviderName -eq 'NuGet'}`| **list installed packages** için kullanışlı |
| Mevcut sürümleri ara                | `Find-Package <pkg> -AllVersions`                           | Sürüm bilinmediğinde yardımcı olur |

---

## Sonuç

PowerShell'i **run powershell as admin** olarak açıp, belirli bir sürümü indirerek **list installed packages** komutuyla **verify installed package** adımını tamamlayarak **how to install nuget** paketlerini baştan sona nasıl kuracağınızı öğrendik. Bu komutlar sayesinde herhangi bir Windows makinesinde kütüphane yönetimini otomatikleştirebilir, CI boru hattı script'leri yazabilir ya da geliştirme ortamınızdaki eksik DLL'leri hızlıca düzeltebilirsiniz.

Sonraki adımlar? Birden fazla paketi tek bir script'e ekleyin, bir proje için yerel kurulum yapmayı sağlayan `-Scope` parametresini keşfedin veya bu komutları `Invoke-Expression` ile birleştirerek ekibiniz için hafif bir kurucu oluşturun. Bir sorunla karşılaşırsanız, **how to verify package** adımını hatırlayın—`Get-Package` çıktısında sürümü görmek genellikle problemi en hızlı tespit etmenizi sağlar.

PowerShell ile mutlu kodlamalar! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}