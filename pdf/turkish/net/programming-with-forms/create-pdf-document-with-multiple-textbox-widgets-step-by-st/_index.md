---
category: general
date: 2026-02-12
description: PDF belgesi oluşturun ve bir form alanı oluştururken boş bir PDF sayfası
  ekleyin – C#'ta metin kutusu PDF widget'larını hızlıca eklemeyi öğrenin.
draft: false
keywords:
- create pdf document
- add blank page pdf
- create pdf form field
- how to create pdf form
- how to add textbox pdf
language: tr
og_description: Boş bir sayfa ve birden fazla metin kutusu widget'ı içeren PDF belgesi
  oluşturun. Aspose.Pdf kullanarak metin kutusu PDF alanları eklemeyi öğrenmek için
  bu kılavuzu izleyin.
og_title: PDF Belgesi Oluştur – C#'ta Metin Kutusu Widget'ları Ekle
tags:
- pdf
- csharp
- aspose
- form-fields
title: Birden Çok Metin Kutusu Widget'ı ile PDF Belgesi Oluşturma – Adım Adım Rehber
url: /tr/net/programming-with-forms/create-pdf-document-with-multiple-textbox-widgets-step-by-st/
---

! If you hit any snags, drop a comment below or explore the Aspose.Pdf documentation for deeper dives. Remember, the best way to master PDF generation is to experiment—so tweak the coordinates, add more widgets, and watch your form come to life.*"

Translate.

Then closing shortcodes.

Now produce final output with all markdown.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Birden Çok Metin Kutusu Widget'ı ile PDF Belgesi Oluşturma – Tam Kılavuz

Hiç **pdf belgesi oluşturma** ihtiyacı duydunuz mu ve içinde birden fazla metin kutusu widget'ı bulunan bir form barındırıyor? Tek başınıza değilsiniz—geliştiriciler sık sık, *“iki yerde görünen metin kutusu pdf alanlarını nasıl eklerim?”* sorusunu sorar. İyi haber, Aspose.Pdf bunu çocuk oyuncağı haline getiriyor. Bu rehberde bir PDF oluşturmayı, boş bir sayfa pdf eklemeyi, bir form alanı oluşturmayı ve sonunda **metin kutusu pdf** widget'larını programlı olarak nasıl ekleyeceğimizi adım adım göstereceğiz.

Belgeyi başlatmaktan son dosyayı kaydetmeye kadar bilmeniz gereken her şeyi ele alacağız. Sonunda, birden çok widget içeren **pdf formu oluşturma** öğelerini gösteren, kullanıma hazır bir PDF elde edeceksiniz ve formun PDF görüntüleyicileri arasında güvenilir kalmasını sağlayan küçük nüansları anlayacaksınız.

## Gereksinimler

- **Aspose.Pdf for .NET** (herhangi bir yeni sürüm; burada kullanılan API 23.x ve sonrası ile çalışır).  
- Bir .NET geliştirme ortamı (Visual Studio, Rider veya hatta C# uzantılı VS Code).  
- C# sözdizimine temel aşinalık—derin PDF bilgisi gerekmez.

Bu maddeleri işaretlediyseniz, başlayalım.

## Adım 1: PDF Belgesi Oluştur – Başlat ve Boş Sayfa Ekle

İlk yaptığımız şey **pdf belgesi oluşturma** nesnesi yaratmak ve ona temiz bir tuval vermektir. Boş bir sayfa pdf eklemek, `Pages.Add()` çağrısı kadar basittir.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

public class MultiWidgetExample
{
    public static void Main()
    {
        // Step 1: Create a new PDF document (the canvas)
        using (var pdfDocument = new Document())
        {
            // Step 2: Add a blank page pdf to the document
            var pdfPage = pdfDocument.Pages.Add();

            // The rest of the steps follow...
```

*Neden önemli:* `Document` sınıfı tüm dosyayı temsil eder. Sayfa olmadan form alanlarını yerleştirecek bir yer yoktur, bu yüzden boş sayfa pdf, oluşturacağınız herhangi bir formun temelini oluşturur.

## Adım 2: PDF Form Alanı Oluştur – Birden Çok Widget Barındırabilen Metin Kutusu Tanımla

Şimdi gerçek **pdf form alanı oluşturma** işlemini yapıyoruz. Aspose buna `TextBoxField` diyor. `MultipleWidgets = true` ayarı, motorun bu alanın birden fazla kez görünebileceğini belirtir.

```csharp
            // Step 3: Create a TextBox field that supports multiple widgets
            var multiWidgetTextBox = new TextBoxField(
                pdfPage,
                new Rectangle(50, 700, 250, 730)); // position on the first page
            multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
            multiWidgetTextBox.Value = "First widget";
```

*İpucu:* Dikdörtgen koordinatları puan cinsinden ifade edilir (1 pt = 1/72 in). Düzeninize uyması için ayarlayın; örnek kutuyu sol‑üst köşeye yakın bir konuma yerleştirir.

## Adım 3: Formun İlk Widget'ını Ekleyin

Alan tanımlandıktan sonra, belge form koleksiyonuna ekliyoruz. Bu, birincil widget için **metin kutusu pdf ekleme** adımıdır.

```csharp
            // Step 4: Add the TextBox field to the form (first widget)
            pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);
```

Üçüncü argüman (`1`) widget indeksidir—önceki adımda oluşturduğumuz sayfada zaten bir widget olduğu için 1’den başlar.

## Adım 4: İkinci Widget'ı Programlı Olarak Ekleyin – Çoklu Widget'ların Gerçek Gücü

Bir kez **pdf formu oluşturma** öğelerinin tekrarlanması gerektiğini merak ettiyseniz, işte sihir burada gerçekleşir. Bir `WidgetAnnotation` örneği oluşturur ve alanın `Widgets` koleksiyonuna ekleriz.

```csharp
            // Step 5: Create and attach a second widget programmatically
            var secondWidget = new WidgetAnnotation(
                new Rectangle(300, 700, 500, 730)); // position on the same page
            multiWidgetTextBox.Widgets.Add(secondWidget);
```

*Neden ikinci bir widget ekleyelim?* Kullanıcıların aynı değeri iki farklı yerde doldurması gerekebilir—örneğin bir formun üst kısmında ve imza bloğunda görünen “Müşteri Adı” alanı. Aynı alan adı (`MultiTB`) paylaşılırsa, bir konumdaki değişiklik diğerini otomatik olarak günceller.

## Adım 5: PDF'yi Kaydet – Her İki Widget'ın da Göründüğünü Doğrulayın

Son olarak belgeyi diske yazıyoruz. Dosya iki senkronize metin kutusu widget'ı içerecek.

```csharp
            // Step 6: Save the PDF with both widgets
            pdfDocument.Save("multiWidget.pdf");
        }
    }
}
```

`multiWidget.pdf` dosyasını Adobe Acrobat, Foxit veya hatta bir tarayıcı PDF görüntüleyicisinde açtığınızda iki metin kutusunu yan yana göreceksiniz. Birine yazdığınızda diğeri anında güncellenir—bu, **metin kutusu pdf ekleme** işlemini çoklu widget'larla başarıyla yaptığımızın kanıtıdır.

### Beklenen Sonuç

- `multiWidget.pdf` adlı tek sayfalık bir PDF.  
- “First widget” etiketiyle iki metin kutusu widget'ı.  
- Her iki kutu da aynı alan adını paylaştığı için içerikleri birbirini yansıtır.

![Birden Çok Metin Kutusu Widget'ı ile PDF Belgesi Oluşturma](https://example.com/images/multi-widget.png "PDF Belgesi Oluşturma örneği")

*Resim alt metni:* iki metin kutusu widget'ı gösteren pdf belgesi

## Yaygın Sorular & Kenar Durumları

### Widget'ları farklı sayfalara yerleştirebilir miyim?

Kesinlikle. İkinci widget için yeni bir `Page` nesnesi oluşturup koordinatlarını kullanın. Alan adı (`"MultiTB"`) aynı kaldığı sürece bağlantı korunur.

```csharp
var secondPage = pdfDocument.Pages.Add();
var thirdWidget = new WidgetAnnotation(new Rectangle(50, 700, 250, 730));
multiWidgetTextBox.Widgets.Add(thirdWidget);
```

### Her widget için farklı bir varsayılan değer gerekirse ne olur?

`Value` özelliği tüm alan için geçerlidir, bireysel widget'lar için değil. Ayrı varsayılanlar istiyorsanız `MultipleWidgets` yerine ayrı alanlar oluşturmanız gerekir.

### PDF/A veya PDF/UA uyumluluğu ile çalışır mı?

Evet, ancak form alanlarını ekledikten sonra ek belge özellikleri (ör. `pdfDocument.ConvertToPdfA()`) ayarlamanız gerekebilir. Widget bağlantısı değişmeden kalır.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda tamamen çalışır bir program örneği bulacaksınız. Sadece bir konsol projesine yapıştırın, Aspose.Pdf NuGet paketine referans ekleyin ve **F5** tuşuna basın.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

namespace AsposePdfMultiWidget
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Add a blank page pdf
                var pdfPage = pdfDocument.Pages.Add();

                // Create a TextBox field that can contain multiple widgets
                var multiWidgetTextBox = new TextBoxField(
                    pdfPage,
                    new Rectangle(50, 700, 250, 730));
                multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
                multiWidgetTextBox.Value = "First widget";

                // Add the TextBox field to the form (first widget)
                pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);

                // Create and attach a second widget programmatically
                var secondWidget = new WidgetAnnotation(
                    new Rectangle(300, 700, 500, 730));
                multiWidgetTextBox.Widgets.Add(secondWidget);

                // Save the PDF with both widgets
                pdfDocument.Save("multiWidget.pdf");
            }
        }
    }
}
```

Programı çalıştırın ve `multiWidget.pdf` dosyasını açın. İki senkronize metin kutusu göreceksiniz—tam da **pdf formu oluşturma** sorusunu birden çok girişle sorduğunuzda istediğiniz şey.

## Özet & Sonraki Adımlar

**pdf belgesi oluşturma**, **boş sayfa pdf** ekleme, **pdf form alanı oluşturma** ve sonunda **metin kutusu pdf ekleme** widget'larını veri paylaşımıyla nasıl yapacağınızı adım adım inceledik. Temel fikir, tek bir alan adının birden çok kez render edilebilmesi ve ekstra kod yazmadan esnek form düzenleri sunmasıdır.

Daha ileri gitmek ister misiniz? Şu fikirleri deneyin:

- **Metin kutusunu stilize edin** – kenar rengi, arka plan veya yazı tipini `TextBoxField` özellikleriyle değiştirin.  
- **Doğrulama ekleyin** – JavaScript eylemlerini (`TextBoxField.Actions.OnValidate`) kullanarak formatları zorlayın.  
- **Diğer alanlarla birleştirin** – onay kutuları, radyo düğmeleri veya dijital imzalar ekleyerek tam özellikli bir form oluşturun.  
- **Form verilerini dışa aktarın** – `pdfDocument.Form.ExportFields()` çağrısıyla kullanıcı girdilerini JSON veya XML olarak alın.

Bu adımlar, ele aldığımız temelin üzerine inşa edildiği için faturalar, sözleşmeler, anketler veya herhangi bir iş ihtiyacı için gelişmiş PDF formları oluşturmanız artık çok daha kolay.

---

*Kodlamanın tadını çıkarın! Herhangi bir sorunla karşılaşırsanız aşağıya yorum bırakın ya da daha derinlemesine bilgi için Aspose.Pdf dokümantasyonuna göz atın. PDF üretimini ustalaşmanın en iyi yolu deneme‑yanılma yoluyla öğrenmektir—koordinatları ayarlayın, daha fazla widget ekleyin ve formunuzun canlanmasını izleyin.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}