# 🏦 Mobil Bankacılık Veritabanı Uygulaması

Bu proje; müşteri işlemleri, kredi başvurusu değerlendirme süreçleri, kart ve ürün yönetimi ile borç/taksit takibini içeren nesne tabanlı ve veritabanı odaklı bir mobil bankacılık simülasyonudur. İş mantığının önemli bir kısmı MS SQL Server üzerinde saklı yordamlar (Stored Procedures) ve transaction yapılarıyla yönetilerek veri bütünlüğü ve işlem güvenliği ön planda tutulmuştur.

---

## 🛠️ Teknolojiler & Araçlar

- **Uygulama Katmanı:** Java (JDBC / `CallableStatement`)
- **Veritabanı Management System (DBMS):** Microsoft SQL Server
- **Veritabanı Nesneleri:** T-SQL, Stored Procedures, Transactions (`BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK`)
- **Mimari:** Katmanlı Mimari (Uygulama Arayüzü & Veritabanı Mantığı Ayrımı)

---

## ✨ Öne Çıkan Özellikler

### 1. Kredi Başvuru & Onay Mekanizması
- Kullanıcıların dinamik tutar ve vade tercihleriyle kredi başvurusunda bulunması.
- Başvuru ID bilgisi üzerinden çalışan merkezi onay mekanizması.
- Eşit taksit hesaplama algoritmaları ile kullanıcı bazlı borç ve ödeme planı oluşturma.

### 2. Müşteri Ürün & Kart Yönetimi (`MusteriUrun`)
- Onaylanan kredi, kart ve hesapların `MusteriUrun` tablosuna benzersiz ürün tipleriyle otomatik kaydedilmesi.
- Kart numaralarının standartlara uygun formatlanması ve güvenli gösterimi.

### 3. Taksit & Borç Takip Sistemi
- Kredi taksit ödemelerinin doğrudan `KalanBorc` ve ilgili hesap bakiyeleri üzerinden anlık güncellenmesi.
- Ödeme geçmişi ve kalan anapara/faiz takibi.

### 4. İşlem Güvenliği & Veri Bütünlüğü (ACID)
- Kritik finansal işlemlerde `BEGIN TRANSACTION`, `COMMIT` ve `ROLLBACK` blokları kullanılarak veri tutarsızlıklarının önüne geçilmesi.
- Veritabanı seviyesinde dinamik veri ayrıştırma (parsing) ve hata yönetimi.

---

## 📐 Veritabanı & Saklı Yordam (Stored Procedure) Mimarisi

Uygulama, veritabanı çağrılarını Java tarafında `CallableStatement` kullanarak gerçekleştirir. 

Örnek Kritik Saklı Yordamlar:
- **`OnayVeUrunEkle`**: Başvuruyu onaylayarak `MusteriUrun` ve borç detay tablolarını atomik bir transaction içerisinde eşzamanlı olarak günceller.
- **Taksit ve Bakiye Güncelleme Yordamları**: Ödeme esnasında müşteri bakiyesini düşüp borç tablosunu güncelleyen güvenli prosedürler.

---

## 🚀 Kurulum & Çalıştırma

### 1. Veritabanı Kurulumu
1. MS SQL Server Management Studio (SSMS) uygulamasını açın.
2. Proje içerisinde yer alan `.sql` veritabanı betiğini (şema, tablolar ve Stored Procedure'leri) çalıştırarak veritabanını oluşturun.

### 2. Uygulama Bağlantısı
1. Java projesindeki veritabanı bağlantı sınıfında (`DatabaseConnection.java`) `connectionString`, `username` ve `password` bilgilerini kendi yerel SQL Server ayarlarınıza göre düzenleyin.
2. MS SQL JDBC sürücüsünün (`mssql-jdbc`) projenize eklendiğinden emin olun.
3. Projeyi derleyip çalıştırın.

---

## 📄 Lisans
Bu proje eğitim ve kişisel gelişim amacıyla hazırlanmıştır.
