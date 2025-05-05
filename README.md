# AgriculturePresentation

Bu depo, ASP.NET Core MVC kullanılarak geliştirilmiş, tarım odaklı bir web uygulaması olan "AgriculturePresentation" projesinin kaynak kodlarını barındırmaktadır. Proje, tarımsal hizmetlerin, duyuruların, ekip üyelerinin ve diğer ilgili bilgilerin sunulduğu ve yönetildiği bir platform sunmayı amaçlamaktadır.

## Projeye Genel Bakış

AgriculturePresentation, modern .NET uygulamalarında yaygın olarak tercih edilen N-Katmanlı Mimari prensiplerine uygun olarak geliştirilmiştir:

*   **EntityLayer:** Uygulamanın veri tabanı nesnelerini temsil eden POCO (Plain Old CLR Object) sınıflarını içerir (Örn: `About`, `Announcement`, `Contact`, `Image`, `Service`, `Team`, `Admin`, `Address`, `SocialMedia`).
*   **DataAccessLayer:** Veri erişim operasyonlarından sorumludur. Entity Framework Core ORM aracı kullanılmıştır.
    *   `Abstract`: Veri erişim katmanı için soyutlama (arayüzler - `IRepository`, `IAboutDal` vb.) içerir. Repository Deseni kullanılmıştır.
    *   `Concrete`: `DbContext` (`Context`) ve Generic Repository (`GenericRepository`) gibi somut sınıfları barındırır.
    *   `EntityFramework`: Entity Framework Core'a özgü somut Repository implementasyonlarını (`EfAboutDal`, `EfAnnouncementDal` vb.) içerir.
    *   `Migrations`: Entity Framework Core veritabanı geçişlerini (schema değişiklikleri) içerir.
*   **BusinessLayer:** İş mantığı kurallarını, servisleri ve doğrulamaları içerir.
    *   `Abstract`: İş katmanı servisleri için arayüzleri (`IAboutService`, `IAnnouncementService` vb.) tanımlar.
    *   `Concrete`: Servis arayüzlerinin somut implementasyonlarını (`AboutManager`, `AnnouncementManager` vb.) içerir. Yöneticiler (Manager'lar) DataAccess katmanı ile iletişim kurar.
    *   `ValidationRules`: Veri doğrulama kurallarını (FluentValidation kullanılarak) içerir (`AddressValidator`, `TeamValidator` vb.).
    *   `Container`: Bağımlılık Enjeksiyonu (Dependency Injection) yapılandırmalarını içerir (`Extensions.cs`).
*   **AgriculturePresentation (UI):** Kullanıcı arayüzünü oluşturan ana ASP.NET Core MVC projesidir.
    *   `Areas/Admin`: Yönetim paneli için Controller, View ve Model'ları içerir.
    *   `Controllers`: Genel kullanıcı arayüzü ve kimlik doğrulama (Login, Register) için Controller'ları içerir.
    *   `Models`: View'ler için özel olarak tasarlanmış ViewModel'ları içerir (`LoginViewModel`, `RegisterViewModel`, `ServiceAddViewModel` vb.).
    *   `ViewComponents`: Tekrar kullanılabilir UI bileşenlerini içerir (`_DashboardChartPartial`, `_TeamPartial`, `_MapPartial` vb.).
    *   `Views`: Kullanıcıya gösterilecek HTML sayfalarını (Razor View) içerir.
    *   `wwwroot`: Statik dosyaları (CSS, JavaScript, Kütüphaneler (Bootstrap, jQuery, matrix-admin teması), Resimler) içerir.

## Özellikler

*   **Genel Kullanıcı Arayüzü:**
    *   Hakkımızda, Hizmetler, Ekibimiz, İletişim gibi bilgilendirme sayfaları.
    *   Duyuruların listelenmesi.
*   **Yönetim Paneli (`/Admin` alanı):**
    *   Güvenli giriş (Login).
    *   Gösterge Paneli (Dashboard) - İstatistikler ve genel bakış.
    *   CRUD (Oluşturma, Okuma, Güncelleme, Silme) İşlemleri:
        *   Duyurular
        *   Hizmetler
        *   Ekip Üyeleri
        *   Resim Galerisi
        *   İletişim Mesajları (Okuma/Silme)
        *   Sosyal Medya Hesapları
        *   Adres Bilgileri
        *   Yöneticiler (Admin Kullanıcıları)
    *   Profil Düzenleme.
    *   Raporlama 
*   **Kullanıcı Yönetimi:**
    *   Kullanıcı Kaydı (`RegisterController`).
    *   Kullanıcı Girişi (`LoginController`).
*   **Veri Doğrulama:** FluentValidation kütüphanesi ile gelen verilerin sunucu tarafında doğrulanması.
*   **Mimari Desenler:** N-Katmanlı Mimari, Repository Deseni, Dependency Injection.

## Kullanılan Teknolojiler

*   **Backend:** C#, ASP.NET Core MVC (.NET 6 veya üstü muhtemel)
*   **Veri Erişimi:** Entity Framework Core
*   **Veritabanı:** SQL Server (EF Core Migrations kullanıldığı için varsayılan)
*   **Ön Yüz (Frontend):** HTML, CSS, JavaScript, jQuery, Bootstrap
*   **Admin Teması:** Matrix Admin
*   **Doğrulama:** FluentValidation
*   **Mimari:** N-Katmanlı Mimari, Repository Pattern, Dependency Injection
