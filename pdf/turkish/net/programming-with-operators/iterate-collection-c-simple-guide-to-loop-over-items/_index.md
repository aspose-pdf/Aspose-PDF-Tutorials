---
category: general
date: 2026-04-25
description: C# koleksiyonunu hızlıca dolaşın, net bir foreach döngüsü örneğiyle.
  Nesne adlarını nasıl alacağınızı ve sadece birkaç adımda string listesini nasıl
  görüntüleyeceğinizi öğrenin.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: tr
og_description: C#'ta bir foreach döngüsü örneğiyle koleksiyonu yineleyin. Nesne adlarını
  nasıl alacağınızı ve bir string listesini verimli bir şekilde nasıl görüntüleyeceğinizi
  keşfedin.
og_title: C# Koleksiyonunu Yinele – Öğeler Üzerinde Adım Adım Döngü
tags:
- C#
- collections
- loops
title: C# Koleksiyonunu Döndür – Öğeler Üzerinde Döngü Yapmanın Basit Kılavuzu
url: /tr/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Koleksiyonları Dolaşma C# – Foreach Döngüsü Örneğiyle Öğeleri Döngüleme

Hiç **koleksiyonları dolaşma C#** ihtiyacı duydunuz mu, ama hangi yapının en temiz kodu verdiğinden emin değildiniz mi? Yalnız değilsiniz. Birçok projede sadece birkaç dizeyi yazdırmak için uzun `for` döngüleri yazıyoruz—zaman ve okunabilirlik kaybına yol açıyor. İyi haber? Tek bir `foreach` döngüsü, bir nesneden tüm adları çekip **dize listesini görüntüleme** işlemini saniyeler içinde yapabilir.

Bu öğreticide, **nesne adlarını alma**, öğeler üzerinde döngü kurma ve bunları konsola yazdırma adımlarını gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, .NET 6+ konsol uygulamasına doğrudan ekleyebileceğiniz bağımsız bir kod parçacığı ve kenar durumları ile performans ipuçları elde edeceksiniz.

> **Pro ipucu:** Büyük koleksiyonlarla çalışıyorsanız `Parallel.ForEach` kullanmayı düşünün—ama bu başka bir günün konusu.

---

## Öğrenecekleriniz

- Bir nesneden ad koleksiyonunu nasıl alırsınız (`GetSignatureNames` örneğimizde)
- C#’ta bir **foreach döngüsü örneği**nin sözdizimi ve incelikleri
- Konsolda **dize listesini görüntüleme** yolları, biçimlendirme püf noktaları dahil
- Öğeler üzerinde döngü kurarken sıkça karşılaşılan tuzaklar (null koleksiyonlar, boş sonuçlar)
- Anında çalıştırabileceğiniz tam bir program örneği

Harici bir kütüphane gerekmez; sadece .NET ile gelen temel sınıf kitaplığı yeterlidir. .NET SDK’nız kuruluysa, hazırsınız demektir.

---

![Iterate collection C# diyagramı, bir listenin foreach döngüsüne ve ardından konsola akışı](/images/iterate-collection-csharp.png "iterate collection c# diyagramı")

---

## Adım 1: Örnek Nesneyi Oluşturma

İlk olarak, bir ad koleksiyonu döndürebilen bir nesneye ihtiyacımız var. `Signature` adında, içinde birkaç imza tutan bir sınıfınız olduğunu hayal edin; her imzanın bir `Name` özelliği var. `GetSignatureNames` metodu, bu adları bir `IEnumerable<string>` olarak çıkartıyor.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace IterateCollectionDemo
{
    // A minimal representation of the object you might be working with
    public class Signature
    {
        private readonly List<string> _names = new()
        {
            "Alice Johnson",
            "Bob Smith",
            "Charlie Davis"
        };

        // This method mimics the real‑world API that returns a collection of names
        public IEnumerable<string> GetSignatureNames()
        {
            // Using LINQ to return a read‑only IEnumerable<string>
            return _names.AsReadOnly();
        }
    }
}
```

**Neden önemli:** `IEnumerable<string>` döndürerek yöntemi esnek tutuyoruz—çağıranlar sonucu yineleyebilir, sorgulayabilir veya kopyalamadan dönüştürebilir. Ayrıca daha sonra **öğeler üzerinde döngü** kurmayı da kolaylaştırıyor.

---

## Adım 2: Foreach Döngüsüyle Dize Listesini Görüntüleme

Şimdi bir ad kaynağımız olduğuna göre **koleksiyonları dolaşma C#** işlemini gerçekleştirelim. `foreach` yapısı, enumerable’daki her öğeyi otomatik olarak çeker; indeks değişkeni yönetmemize gerek kalmaz.

```csharp
using System;

namespace IterateCollectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Instantiate the object that holds our signatures
            var signature = new Signature();

            // Step 2: Retrieve the collection of signature names from the signature object
            var signatureNames = signature.GetSignatureNames();

            // Step 3: Loop over items and output each name to the console
            foreach (var name in signatureNames)
            {
                Console.WriteLine(name);
            }

            // Keep the console window open when debugging locally
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Kodun açıklaması:**

1. **Instantiate** `Signature` – artık kendi adlarını bilen bir nesneniz var.
2. **Retrieve** koleksiyonu `GetSignatureNames()` ile – bu **nesne adlarını alma** adımı.
3. **Foreach döngüsü örneği** – `foreach (var name in signatureNames)` her dizeyi otomatik olarak iterasyon eder.
4. **Display** her `name`i `Console.WriteLine` ile – konsol uygulamasında **dize listesini görüntüleme**nin klasik yolu.

`signatureNames` `IEnumerable<string>` uyguladığı için `foreach` döngüsü kutudan çıkar çıkmaz çalışır, arka planda enumerator’u yönetir. Artık off‑by‑one hataları ya da manuel sınır kontrolleriyle uğraşmazsınız.

---

## Adım 3: Programı Çalıştırma ve Çıktıyı Doğrulama

Programı derleyip çalıştırın (ör. proje klasöründen `dotnet run`). Şu çıktıyı görmelisiniz:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

Eğer hiçbir şey yazdırılmadıysa, `GetSignatureNames` metodunun `null` döndürmediğini kontrol edin. Hızlı bir savunma kontrolü baş ağrılarınızı önleyebilir:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Böylece döngü eksik bir koleksiyonla karşılaştığında zarifçe hiçbir şey yazdırmaz, `NullReferenceException` fırlatmaz.

---

## Adım 4: Yaygın Varyasyonlar ve Kenar Durumları

### 4.1 Karmaşık Nesneler Listesi Üzerinde Döngü

Çoğu zaman sadece düz stringlerle değil, birden fazla özelliği olan nesnelerle çalışırsınız. Bu durumda hâlâ **öğeler üzerinde döngü** kurabilir ve ne göstereceğinize karar verebilirsiniz:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Burada string interpolasyonu ile alanları birleştiriyoruz—hala bir `foreach` döngüsü, sadece daha zengin bir çıktı.

### 4.2 `break` ile Erken Çıkış

Sadece ilk eşleşen adı istiyorsanız, döngüden `break` ile çıkabilirsiniz:

```csharp
foreach (var name in signatureNames)
{
    if (name.StartsWith("B"))
    {
        Console.WriteLine(name);
        break; // stops after the first B‑name
    }
}
```

### 4.3 Paralel İterasyon (İleri Düzey)

Koleksiyon çok büyük ve her iterasyon CPU‑ağır ise, `Parallel.ForEach` işleri hızlandırabilir:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Unutmayın, `Console.WriteLine` kendisi thread‑safe olsa da çıktı sırası deterministik olmayacaktır.

---

## Adım 5: Temiz ve Bakımı Kolay Döngüler İçin İpuçları

- **İndeks gerekmiyorsa `foreach` tercih edin**; off‑by‑one hatalarını azaltır.
- **Metot imzalarında `IEnumerable<T>` kullanın**; API’leri esnek tutar.
- **Null koleksiyonlara karşı null‑coalescing operatörü (`??`) ile koruma ekleyin**.
- **Döngü gövdesini küçük tutun**; çok satır yazıyorsanız bir metoda çıkarın.
- **İterasyon sırasında koleksiyonu değiştirmeyin**; aksi takdirde `InvalidOperationException` fırlatır.

---

## Sonuç

Temiz bir **foreach döngüsü örneği**yle **koleksiyonları dolaşma C#**i, **nesne adlarını alma** ve konsolda **dize listesini görüntüleme**i nasıl yapacağınızı gösterdik. Nesne tanımı, veri çekme ve iterasyonun tamamı çalıştırılabilir bir program olarak sunuldu; böylece öğeler üzerinde döngü kurmanız gereken her senaryo için sağlam bir temeliniz oldu.

Bundan sonra keşfedebilecekleriniz:

- Döngüden önce LINQ ile filtreleme (`signatureNames.Where(n => n.Contains("a"))`)
- Çıktıyı konsol yerine bir dosyaya yazma
- Asenkron akışlar için `IAsyncEnumerable<T>` kullanma

Deneyin, `foreach` yapısının ne kadar çok yönlü olduğunu göreceksiniz. Kenar durumları ya da performans hakkında sorularınız varsa aşağıya yorum bırakın, mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}