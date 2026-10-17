---
category: general
date: 2026-02-14
description: Bates numaralandırması PDF'yi belgelerinize zahmetsizce ekleyin. Altbilgi
  sayfa numaralarını nasıl ekleyeceğinizi ve Aspose.Pdf ile dakikalar içinde PDF'ye
  sıralı numaralar eklemeyi öğrenin.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: tr
og_description: Bates numaralandırmasını PDF'e hızlıca ekleyin. Bu rehber, Aspose.Pdf
  kullanarak altbilgi sayfa numaraları ve sıralı numaraları PDF'e nasıl ekleyeceğinizi,
  tam kod ve ipuçlarıyla gösterir.
og_title: Bates Numaralandırması PDF Ekle – Adım Adım C# Öğreticisi
tags:
- Aspose.Pdf
- C#
- PDF automation
title: PDF'ye Bates Numaralandırması Ekle – Tam C# Rehberi
url: /tr/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'e Bates Numaralandırma Ekle – Tam C# Rehberi

PDF dosyalarına **Bates numaralandırma ekleme** ihtiyacı hiç duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz. Hukuk ekipleri, denetçiler ve büyük belge setleriyle çalışan herkes sürekli olarak “Bates numaralarını düzeni bozmadan nasıl eklerim?” sorusunu sorar. İyi haber şu ki, Aspose.Pdf for .NET ile bu numaraları basit bir alt bilgi (footer) olarak enjekte edebilirsiniz—manuel düzenleme gerekmez.

Bu öğreticide, yalnızca **alt bilgi sayfa numaraları eklemek**le kalmayıp, aynı zamanda **PDF dosyalarına sıralı numaralar eklemek** için özel bir ön ek, yazı tipi boyutu ve hizalama ayarlamanıza olanak tanıyan pratik, uçtan uca bir çözümü adım adım inceleyeceğiz. Sonunda çalıştırmaya hazır bir C# programına, her ayarın neden önemli olduğuna dair net bir anlayışa ve yaygın hatalardan kaçınmak için birkaç uzman ipucuna sahip olacaksınız.

## What You’ll Learn

- Mevcut bir PDF'yi yükleyip Bates numaralandırma için hazırlama.  
- Görünüm ve konumu kontrol eden **BatesNumberingOptions** özellikleri.  
- Numaralandırmayı tek bir çağrı ile tüm sayfalara uygulama.  
- Farklı yasal formatlar için ön ek, başlangıç numarası ve kenar boşluklarını özelleştirme yolları.  
- Kenar durumları yönetimi—şifreli PDF'lerle veya zaten alt bilgi içeren belgelerle ne yapılır.

**Prerequisites**: .NET 6+ (veya .NET Framework 4.7+), güncel bir Aspose.Pdf sürümü (örnek 23.10 kullanıyor), ve değiştirme hakkına sahip olduğunuz bir giriş PDF'i. Başka üçüncü‑taraf kütüphane gerekmez.

---

## Step 1 – Load the PDF You Want to Number

İlk olarak, kaynak dosyayı işaret eden bir `Document` örneği oluşturuyoruz. `using var` deseni, dosya tutamacının otomatik olarak serbest bırakılmasını sağlar.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Why this matters:** Aspose.Pdf, tüm PDF yapısını belleğe okuyarak sayfaları, ek açıklamaları ve meta verileri orijinal dosyaya dokunmadan manipüle etmemize olanak tanır. PDF şifre korumalıysa, şifreyi yapıcıya geçirebilirsiniz—sondaki “Encrypted PDFs” notuna bakın.

---

## Step 2 – Define Your Bates Numbering Options

Bates numaraları, yapılandırılabilir bir ön ek ve sıralı bir sayaç içeren sayfa alt bilgileri gibidir. `BatesNumberingOptions` sınıfı, görsel her yönü ince ayar yapmanıza izin verir.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Quick tip

- **Prefix**: Alt bilginin okunabilir kalması için kısa, benzersiz bir tanımlayıcı (ör. dava numarası) kullanın.  
- **StartNumber**: Hukuk firmaları genellikle `1` veya özel bir offset ile başlar; dosyalama sisteminize uyanı seçin.  
- **Margins**: `20` puanlık alt kenar boşluğu, metnin sayfa kenarına yakın olabilecek dipnotlar veya imzalarla çakışmasını önler.

---

## Step 3 – Apply the Numbering to All Pages

Seçenekler ayarlandıktan sonra, gerçek ekleme tek satırda gerçekleşir. Aspose.Pdf sayfalama işlemini yönetir, mevcut içerik akışlarını günceller ve sayfa dönüşünü otomatik olarak dikkate alır.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **What’s happening under the hood?** Kütüphane, her `Page` nesnesi üzerinde döner, ön ek ve mevcut sayaçla bir `TextFragment` oluşturur ve ardından sayfanın koordinat sistemini kullanarak çizer. `HorizontalAlignment.Right` ve `VerticalAlignment.Bottom` ayarlandığı için metin, sayfa boyutundan bağımsız olarak alt‑sağ köşeye sabitlenir.

---

## Step 4 – Save the Modified PDF

Son olarak, sonucu yeni bir dosyaya yazın. Orijinali üzerine yazmak mümkün olsa da, bir kopya tutmak sürüm kontrolü açısından faydalıdır.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Orijinal meta verileri (yazar, oluşturma tarihi vb.) korumak isterseniz, Aspose.Pdf varsayılan olarak bunları kopyalar. PDF/A uyumluluğu veya sıkıştırma için bir `SaveOptions` nesnesi de belirtebilirsiniz.

---

## Full Working Example

Aşağıda, çalıştırmaya hazır tam program yer alıyor. Bir console uygulaması projesine yapıştırın, dosya yollarını ayarlayın ve **F5** tuşuna basın.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Expected result:** `output.pdf`'in her sayfası artık `ABC-1000`, `ABC-1001`, … gibi alt bilgiye sahip ve bu metin alt‑sağ köşeye sabitlenmiş olur. Doğrulamak için dosyayı herhangi bir PDF okuyucusunda açın.

---

## Handling Common Variations

### Adding Footer Page Numbers Only

Sadece ön ek olmadan basit sayfa numaraları istiyorsanız, `Prefix = ""` olarak ayarlayın ve mevcut alt bilgilerle çakışmayı önlemek için kenar boşluğunu gerektiği gibi ayarlayın.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Using a Different Alignment

Bazı yasal belgeler numaranın sayfanın alt ortasında olmasını ister. Hizalamayı şu şekilde değiştirin:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Dealing with Encrypted PDFs

Kaynak PDF şifre korumalıysa, şifreyi aşağıdaki gibi sağlayın:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

İş akışının geri kalanı aynı kalır.

### Skipping Existing Footers

Bir belgede zaten bir alt bilgi varsa ve üzerine yazmak istemiyorsanız, yeni sayıyı ayırt edebilecek özel bir dize ekleyebilir ya da sayfaları manuel olarak dönerken alt bilgi bulunmayan sayfalara sadece bir `TextFragment` ekleyebilirsiniz. Kütüphanenin `Page` sınıfı, ince ayar kontrolü için `Annotations` ve `Contents` koleksiyonlarını sunar.

---

## Pro Tips & Pitfalls

- **Avoid clipping**: Çok küçük alt kenar boşlukları, metnin yazıcıda kesilmesine neden olabilir. Fiziksel kopya dağıtacaksanız mutlaka bir baskı testi yapın.  
- **Performance**: 500 sayfalık bir PDF'e Bates numarası eklemek modern bir dizüstü bilgisayarda bir saniyenin altında sürer, ancak büyük toplu işlemler paralel işleme fayda sağlar—`Document` nesnesi thread‑safe değildir, bu yüzden her iş parçacığı kendi örneğine sahip olmalıdır.  
- **Version compatibility**: Kod, Aspose.Pdf 23.10 ve üzeri sürümlerle çalışır. Daha eski bir sürüm kullanıyorsanız, özellik adları aynı kalır ancak `MarginInfo` yapıcısı `float` argümanlar isteyebilir.  
- **Legal compliance**: Bazı yargı bölgeleri Bates numarasının belirli bir konumda (ör. alt‑sol) bulunmasını zorunlu kılar. `HorizontalAlignment` değerini buna göre ayarlayın.  

---

## Conclusion

Aspose.Pdf for .NET kullanarak **PDF'e Bates numaralandırma ekleme** sürecini, belgeyi yüklemekten temiz bir alt bilgiyle son sürümü kaydetmeye kadar adım adım gösterdik. Birkaç özelliği ayarlayarak **alt bilgi sayfa numaraları ekleyebilir**, **PDF dosyalarına sıralı numaralar ekleyebilir** veya görünümü herhangi bir yasal standarda göre özelleştirebilirsiniz.

Bir sonraki adım için hazır mısınız? Bu tekniği OCR metin çıkarımıyla birleştirerek Bates numaralarınızın yanına aranabilir anahtar kelimeler ekleyebilir veya `Directory.GetFiles` kullanarak tüm klasörler için otomatikleştirebilirsiniz. Olanaklar sınırsızdır ve şimdi sahip olduğunuz temel, bu genişletmeleri sorunsuz yapmanızı sağlayacak.

İyi kodlamalar, ve PDF'leriniz her zaman mükemmel numaralandırılmış olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}