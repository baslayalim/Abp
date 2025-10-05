\# Baslayalim Abp



Buradaki bilgiler \[github.com/baslayalim](https://github.com/baslayalim) hesabına aittir.

Kişisel notlar ve denemeler içerir; \*\*eksik, yanlış veya hatalı bilgiler olabilir.\*\*

Lütfen anlamadığınız ya da farklı durumlar için resmi dokümantasyona göz atın: \[https://abp.io](https://abp.io)



---



\## 📘 Ön Bilgi



Yaklaşık 2 yıl önce oluşturduğum projeyi incelemeniz, ABP Framework'ü daha iyi anlamanıza yardımcı olacaktır:

🔗 \[ https://github.com/baslayalim/CaseStudy ]( https://github.com/baslayalim/CaseStudy )



Bu projede \*\*Onion Architecture\*\* kullanarak katmanlı bir yapı oluşturdum ve ABP'nin sunduğu bazı özellikleri uyguladım.

ABP Framework, bu süreci büyük ölçüde kolaylaştırır, işlem adımlarını hızlandırır ve geliştirme sürecine esneklik katar.



> 💡 Bu projeyi incelemenizi önermemin nedeni:

> 100'den fazla commit ile adım adım işlemleri ve proje gelişimini takip edebilirsiniz.

> Ayrıca ABP'nin kendi dokümantasyonunda da örnek projeler mevcuttur.





Komutları kullanabilmek için \*\*Volo\*\* firmasına ait \*\*ABP CLI\*\* aracını kurmamız gerekiyor.

(Eski bir CLI sürümü yüklüyse, kaldırmanız veya güncellemeniz gerekebilir.)




\## 🧱 1. Commit Başlangıç


```bash

dotnet tool install -g Volo.Abp.Studio.Cli

\# veya mevcut ise güncelleme:

dotnet tool update -g Volo.Abp.Studio.Cli



Cli Create -> dotnet tool install -g Volo.Abp.Studio.Cli

Cli Update -> dotnet tool update -g Volo.Abp.Studio.Cli


Kurarken ben hata aldım çünkü .net9 güncel degildi


Tool 'volo.abp.studio.cli' failed to update due to the following:

The settings file in the tool's NuGet package is invalid: Settings file 'DotnetToolSettings.xml' was not found in the package.

Tool 'volo.abp.studio.cli' failed to install. Contact the tool author for assistance.


Benzeri bir hata alırsanız aşağıdaki linki kullanabilirsiniz


https://dotnet.microsoft.com/en-us/download/dotnet/9.0

Güncellemeden Sonra Kurulum Başarılı

You can invoke the tool using the following command: abp

Tool 'volo.abp.studio.cli' was successfully installed.


Proje Oluştururken

Birden fazla template ve veritabanı seçenekleri var

Örnek : Angular, Razor, Blazor vs. Database de ise Entity , Mongo

(zaten entity framework içinde neredeyse tüm dbleri destekleyen bir yapı mevcut)


Örnek Proje Kodu : abp new Acme.BookStore -t app

Katmanlı mimariye bakmamız bizim için iyi olacaktır Abpyi daha derinlemesine inceleme fırsatımız olabilir




\## 🧱 2. Commit Proje Detayları


```bash

Cli üzerinde proje başlangıç komutu çalıştırıldığında migration işlemlerini yapıyor, yapılmadığı durumlarda DbMigrator Çalıştırılarak Tablolar Oluşturuluyor iki Connection gördüm birincisi Uygulama projesinde ikincisi DbMigrator içerisinde istediğimiz Connection ile degiştirebiliyoruz

Tabloları user tabloları standart yetki ve rol tabloları, loglama olarak serilog kullanılıyor migration içerisinde serilog kendi tablolarınıda oluşturuyor
Settings tabloları ve diğer uygulamaya erişim için kullanılacak tablolar mevcut

Solution içerisindeki projeler sistemli oluşturulmuş ilgimi çeken Domain ve Domain.Shared olması Domain kapsayıcı entityleri içerdiği için diğer
projelere taşınması yerine diğer projelerde kullanılacak entity modellerini Domain.Shared içerisinde konumlandırılmış .

Login 
email : admin@abp.io
pass  : 1q2w3E*

Not : Lütfen eski migration dosyalarını silip kendi migration işlemlerinizi başlatın sonra benim gibi zaman kaybetmeyin


Dikkatimi çeken güzel özellikler

Entity oluşturulduğunda abp nin kendi tablolarının açılması silinme özelliğinin aktif gelmesi, loglama özellikleri, Entity üzerinde en son kim işlem yapmış gibi bilgilerin tutulması, tabloların consol ile haberleşip javascript ile işlemlerin yapılabilmesi, kendisine ait arayüz componentlerinin olması ve daha bir çok özellik kullandıkça daha çok hoşunuza gidiyor, Icrud servisiyle oluşturulan entity için swaggerdan işlem yapılması 

Abp servisleriyle sadece Entity oluşturduktan sonra javascript ile erişim sağlayıyoruz, swagger dan erişim sağlıyoruz tabloları oluşturuyoruz aslında tüm hazır sistemler Abp ye eklenmiş ve hepsi birbirine bağlanmış şekilde hizmet ediyor


örnek javascript list sorgusu

acme.bookStore.books.book.getList({})
    .done(function (result) { console.log(result); });


örnek javascript kayıt sorgusu

acme.bookStore.books.book.create({
        name: 'Foundation',
        type: 7,
        publishDate: '1951-05-24',
        price: 21.5
    }).then(function (result) {
        console.log('successfully created the book with id: ' + result.id);
    });







