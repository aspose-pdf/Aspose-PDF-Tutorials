---
category: general
date: 2026-03-03
description: Aspose.PDF kullanarak C#'de sayfalı PDF oluşturun ve metin kutusu PDF
  form alanları ekleyin. Metin kutusu eklemeyi, PDF form alanı oluşturmayı ve birden
  fazla sayfalı PDF'yi hızlıca eklemeyi öğrenin.
draft: false
keywords:
- create pdf with pages
- add text box pdf
- how to add textbox
- create pdf form field
- add multiple pages pdf
language: tr
og_description: Aspose.PDF kullanarak sayfalı PDF oluşturun. Bu kılavuz, metin kutusu
  PDF alanları eklemeyi, PDF form alanı oluşturmayı ve C#'ta çok sayfalı PDF eklemeyi
  gösterir.
og_title: Sayfalarla PDF Oluştur – Tam C# Öğreticisi
tags:
- pdf
- csharp
- aspose
title: Sayfalar ve Metin Kutusu Alanlarıyla PDF Oluşturma – Tam C# Rehberi
url: /tr/net/programming-with-forms/create-pdf-with-pages-and-text-box-fields-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sayfalar ve Metin Kutusu Alanlarıyla PDF Oluşturma – Tam C# Rehberi

Kullanıcıların not almasını sağlayan **sayfalarla pdf oluşturma** oluşturmanız gerektiğinde hiç oldu mu? Belki bir sözleşme portalı, bir geri bildirim formu ya da basit bir anket oluşturuyorsunuzdur. Bu durumda, yalnızca birkaç sayfaya sahip olmakla kalmayıp aynı zamanda yeniden kullanılabilir bir metin kutusu içeren bir PDF istemek isteyeceksiniz. İyi haber: Aspose.PDF for .NET ile tüm bunları birkaç satırda yapabilirsiniz.

Bu öğreticide **textbox ekleme** kontrollerini, bir **pdf form alanı oluşturma** kaydedecek ve son olarak **çok sayfalı pdf ekleme** ekleyerek cilalı, etkileşimli bir belge oluşturacağız. Gereksiz ayrıntı yok—sadece kopyala‑yapıştır yapabileceğiniz kod ve her kararın “neden”i. Sonunda `TextBoxTwoWidgets.pdf` adlı bir PDF'niz olacak ve aynı metin kutusunu iki ayrı sayfada içerecek.

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.6+ ile de çalışır)  
- Aspose.PDF for .NET NuGet paketi (`Install-Package Aspose.PDF`)  
- C# sınıfları ve nesne temizleme hakkında temel bir anlayış (bir `using` bloğu kullanacağız)  

> **Pro tip:** Visual Studio kullanıyorsanız, daha temiz bir deneyim için *nullable reference types* özelliğini etkinleştirin, ancak bu örnek için gerekli değildir.

## Adım 1: Sayfalarla PDF Oluşturma – Belgeyi Ayarlama

İlk yapmanız gereken boş bir PDF belgesi oluşturmaktır. `Document` sınıfını yeni bir not defteri gibi düşünün; sayfaları daha sonra ona ekleyeceksiniz.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

using (var pdfDocument = new Document())
{
    // The document is now ready for pages and form fields.
```

*Neden bir `using` bloğu?* İşimiz bittiğinde tüm yönetilmeyen kaynakların (dosya tutamaçları, bellek tamponları) serbest bırakılmasını garanti eder, sızıntıları önler—özellikle bir web hizmetinde çok sayıda PDF oluştururken önemlidir.

## Adım 2: İlk Sayfaya Metin Kutusu PDF Alanı Ekleme

Belge artık mevcut olduğuna göre, bir form alanı barındırmak için en az bir sayfaya ihtiyacımız var. Aynı textbox'ın her iki sayfada da görünmesini istediğimiz için **iki sayfa** ekleyeceğiz.

```csharp
    // Add the first page
    var firstPage = pdfDocument.Pages.Add();

    // Add the second page (will host the widget copy)
    var secondPage = pdfDocument.Pages.Add();

    // Create a TextBoxField on the first page
    var notesField = new TextBoxField(
        firstPage,
        new Rectangle(50, 700, 300, 750))   // left, bottom, right, top
    {
        Name = "Notes",
        Value = "Type here..."
    };
```

Dikdörtgen koordinatları PDF koordinat sistemine (köşe alt‑sol) göre belirlenir. `Name` özelliği iç kimliktir; kullanıcı formu doldurduktan sonra değeri alırken daha sonra kullanacaksınız.

## Adım 3: İkinci Sayfada Textbox Widget'ı Nasıl Eklenir

*Widget*, bir form alanının görsel temsilidir. Varsayılan olarak bir alan, oluşturulduğu sayfada tek bir widget alır. Aynı textbox'ı başka bir sayfada da istiyorsanız, başka bir widget açıklaması eklemeniz gerekir.

```csharp
    // Place a second widget of the same field on the second page
    notesField.AddWidgetAnnotation(
        secondPage,
        new Rectangle(50, 500, 300, 550));
```

Farklı Y‑koordinatlarına dikkat edin—bu, ikinci textbox'ı sayfada daha aşağı konumlandırır. Elbette aynı dikdörtgeni kullanarak aynı yerleşimi de elde edebilirsiniz.

## Adım 4: PDF Form Alanı Oluşturma ve Kaydetme

`notesField`'i zaten örneklediğimiz halde, belge'nin `Form` koleksiyonuna kaydetmemiz gerekir. Bu adım, alanı etkileşimli form yapısının bir parçası haline getirir.

```csharp
    // Register the field with the PDF form
    pdfDocument.Form.Add(notesField, notesField.Name);
```

Bu satırı atlayarsanız, textbox görsel olarak görünecek ancak form alanı olarak kaydedilmeyecek, yani PDF işlendiğinde içeriği gönderilmeyecek.

## Adım 5: PDF'yi Kaydetme ve Çok Sayfalı PDF'yi Doğrulama

Son olarak belgeyi diske yazıyoruz. Dosya adı isteğe bağlıdır; sadece klasörün var olduğundan ve uygulamanızın yazma iznine sahip olduğundan emin olun.

```csharp
    // Save the resulting PDF
    pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
}
```

`TextBoxTwoWidgets.pdf` dosyasını Adobe Acrobat Reader'da açtığınızda, aynı “Notes” textbox'ını içeren iki sayfa göreceksiniz. İlk sayfada bir şeyler yazın, ikinciye geçin—her iki alan da aynı temel veri nesnesini paylaştığı için bağımsız kalır.

### Beklenen Çıktı

- **Sayfa 1:** (50, 700) koordinatlarında “Type here…” yer tutucusuna sahip textbox.  
- **Sayfa 2:** Daha düşük konumda (50, 500) aynı textbox.  
- Her iki sayfa da “Notes” adlı **tek bir PDF formuna** aittir.  

Formu, verileri dışa aktararak test edebilirsiniz (Acrobat → Tools → Prepare Form → Export Data) ve `Notes` için tek bir giriş göreceksiniz.

## Yaygın Varyasyonlar ve Kenar Durumları

| Senaryo | Ne Değiştirilmeli | Neden |
|----------|-------------------|-------|
| **Sayfa başına farklı varsayılan metin** | Farklı `Name` değerlerine sahip iki ayrı `TextBoxField` nesnesi oluşturun. | Her widget, bağımsız değerler tutabilmesi için kendi alanına ait olmalıdır. |
| **Salt okunur textbox** | `notesField.ReadOnly = true;` satırını widget eklemeden önce ayarlayın. | Kullanıcıların alanı düzenlemesini engellerken bilgiyi göstermeye devam eder. |
| **Çok satırlı textbox** | `notesField.Multiline = true;` olarak ayarlayın ve dikdörtgen yüksekliğini artırın. | Kaydırma yapmadan daha uzun notlar almayı sağlar. |
| **Şifre korumalı PDF** | Kaydetmeden sonra `pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AESx128);` metodunu çağırın. | Form alanlarını korurken belgeyi güvence altına alır. |

## Aspose.PDF Formlarıyla Çalışmak İçin Pro İpuçları

- **Toplu oluşturma:** Eğer onlarca aynı widget'a ihtiyacınız varsa, `pdfDocument.Pages` üzerinde döngü yapın ve döngü içinde `AddWidgetAnnotation` metodunu çağırın.  
- **Alan adlandırma kuralları:** Daha sonra PDF'leri birleştirirken çakışmaları önlemek için `txt_` veya `fld_` gibi bir ön ek kullanın.  
- **Performans:** Mümkün olduğunda tek bir `Rectangle` örneğini yeniden kullanın; kütüphane değerleri dahili olarak kopyalar, böylece bellek darboğazına takılmazsınız.  

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // 2️⃣ Add two pages – we’ll place a widget on each
            var firstPage = pdfDocument.Pages.Add();
            var secondPage = pdfDocument.Pages.Add();

            // 3️⃣ Define the textbox field (add text box pdf)
            var notesField = new TextBoxField(
                firstPage,
                new Rectangle(50, 700, 300, 750))
            {
                Name = "Notes",
                Value = "Type here..."
            };

            // 4️⃣ Add a second widget on the second page (how to add textbox)
            notesField.AddWidgetAnnotation(
                secondPage,
                new Rectangle(50, 500, 300, 550));

            // 5️⃣ Register the field (create pdf form field)
            pdfDocument.Form.Add(notesField, notesField.Name);

            // 6️⃣ Save the file (add multiple pages pdf)
            pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
        }

        System.Console.WriteLine("PDF created successfully!");
    }
}
```

Programı çalıştırın, oluşan dosyayı açın ve öğreticide anlatılanı tam olarak göreceksiniz.

## Sonuç

Az önce **sayfalarla pdf oluşturduk** ve içinde yeniden kullanılabilir bir **add text box pdf** form öğesi ekledik, birden çok sayfada **textbox ekleme** widget'larını gösterdik ve uygun bir **pdf form alanı oluşturma** kaydettik. Son belge, formu etkileşimli ve hafif tutarken **çok sayfalı pdf ekleyebileceğinizi** kanıtlıyor.

Sırada ne var? PDF'i gerçekten dinamik hâle getirmek için onay kutuları, radyo düğmeleri veya hatta JavaScript eylemleri eklemeyi deneyin. Ayrıca bu tür PDF'leri tek bir raporda birleştirmeyi keşfedebilirsiniz—Aspose.PDF bunu çok kolay bir hale getirir.

Sorularınız veya paylaşmak istediğiniz ilginç bir kullanım senaryonuz mu var? Aşağıya bir yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}