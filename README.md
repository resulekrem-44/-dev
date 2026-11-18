# Araç Kiralama Yönetim Sistemi (Vehicle Rental Management System)

Bu proje, **BGY203 / YBS223 Nesne Tabanlı Programlama** dersi kapsamında **Dr. Öğr. Üyesi Tohid YOUSEFİ** tarafından verilen dönem sonu teknik şartnamesine tam uyumlu olarak geliştirilmiş, katmanlı mimariye sahip modern bir Windows Forms masaüstü uygulamasıdır.

---

## 👨‍💻 Geliştirici ve Proje Bilgileri
- **Ders Adı:** Nesne Tabanlı Programlama (BGY203 / YBS223)
- **Öğretim Elemanı:** Dr. Öğr. Üyesi Tohid YOUSEFİ
- **Öğrenci Adı Soyadı:** Resul Ekrem ÖZCAN
- **Öğrenci Numarası:** 25902009
- **Teslim Formatı:** ALMS Tek ZIP Paketi (`25902009_ResulEkremOzcan_VehicleRentalSystem.zip`)
- **GitHub Repository:** Private (Gizli) Repository, Collaborator: `tohid.yousefi`

---

## 🎯 Projenin Amacı ve Kapsamı
Projenin temel amacı, C# programlama dili ve Windows Forms teknolojisi kullanılarak araç kiralama süreçlerini (filo yönetimi, müşteri kayıtları, sözleşme oluşturma, ücret hesaplama ve araç iade) güvenilir, hataya dayanıklı ve modüler bir yapıda yürütmektir. 

Sistem; sadece basit bir CRUD (ekle/çıkar/güncelle) uygulaması değil, nesne tabanlı programlamanın (OOP) 4 ana direğini somut iş akışlarında kullanan bir mimariye sahiptir:
1. **Kapsülleme (Encapsulation)**
2. **Kalıtım (Inheritance)**
3. **Çok Biçimlilik (Polymorphism)**
4. **Soyutlama (Abstraction)**

---

## 🛠️ Kullanılan Teknolojiler ve Geliştirme Ortamı
- **Programlama Dili:** C# 12.0
- **Çalışma Zamanı (Framework):** .NET 8.0 Windows Desktop SDK (`net8.0-windows`)
- **Arayüz (GUI):** Windows Forms (WinForms)
- **Geliştirme Ortamı (IDE):** Visual Studio 2022 / Visual Studio Code
- **Veri Yapıları:** Generic Koleksiyonlar (`List<T>`, `IReadOnlyList<T>`, LINQ)
- **Sürüm Kontrolü:** Git & GitHub

---

## 🏛️ Sınıf Mimarisi ve OOP Prensiplerinin Uygulanışı

### 1. Soyutlama (Abstraction) ve Arayüz (Interface)
- **`IRentable` (Arayüz):** Kiralanabilir nesneler için sözleşme görevi görür (`Id`, `Plate`, `DailyRate`, `CalculateRentalPrice()`, `Rent()`, `ReturnVehicle()`).
- **`Vehicle` (Abstract Base Class):** Doğrudan nesnesi türetilemeyen soyut temel sınıftır. Tüm araçlar için ortak özellikleri ve `abstract decimal CalculateRentalPrice(int days)` metodunu tanımlar.

### 2. Kalıtım (Inheritance)
- **`Car : Vehicle`**: Otomobil sınıfı. Temel sınıftan kalıtım alarak `SeatingCapacity` (koltuk) ve `TransmissionType` (vites) ek özelliklerini kazanır. `base(...)` yapıcısını çağırır.
- **`Suv : Vehicle`**: SUV/Arazi aracı sınıfı. Temel sınıftan türer ve `FourWheelDrive` (4x4) özelliğini barındırır.

### 3. Çok Biçimlilik (Polymorphism)
- Temel sınıftaki `CalculateRentalPrice(int days)` soyut metodu alt sınıflarda iş mantığına göre özelleştirilmiştir:
  - **Otomobillerde (`Car`):** 7 gün ve üzeri kiralamalarda kampanya kapsamında **%10 indirim** uygulanır.
  - **SUV Araçlarda (`Suv`):** Zorlu arazi şartları kasko koruması için kiralama bedeline **%15 arazi güvence primi** eklenir.

### 4. Kapsülleme (Encapsulation)
- Tüm veri alanları (`_id`, `_plate`, `_brand`, `_dailyRate`, `_phoneNumber` vb.) `private` olarak gizlenmiştir.
- Değer atamaları public property'lerin `set` bloklarında katı doğrulama (validation) kurallarına tabidir:
  - Günlük ücret $\le 0$ olamaz.
  - Plaka, marka, model, ad-soyad boş veya whitespace olamaz.
  - Plaka tekrarları ve aynı ehliyet numarasıyla çift kayıt engellenir.
  - Kiralama başlangıç ve bitiş tarihi kontrol edilir (Bitiş tarihi başlangıçtan önce olamaz).

---

## 📂 Proje Klasör Yapısı
Teknik şartnamenin 8. maddesinde belirtilen yapıya %100 uyumludur:

```text
25902009_ResulEkremOzcan_VehicleRentalSystem/
│
├── 01_SourceCode/                               # Visual Studio Solution ve Tüm Kaynak Kodlar
│   ├── VehicleRentalSystem.sln                  # Solution Dosyası
│   └── VehicleRentalSystem/
│       ├── Forms/                               # Arayüz Formları
│       │   ├── MainForm.cs                      # Dashboard ve Ana Menü
│       │   ├── VehiclesForm.cs                  # Araç Yönetimi (Ekle, Güncelle, Sil, Listele)
│       │   ├── CustomersForm.cs                 # Müşteri Yönetimi
│       │   ├── RentalForm.cs                    # Kiralama İşlemi & Hesaplama
│       │   └── ReturnForm.cs                    # Araç İade İşlemi & Müsait Yapma
│       ├── Models/                              # OOP Model ve Varlık Sınıfları
│       │   ├── Enums.cs                         # VehicleStatus & RentalStatus
│       │   ├── IRentable.cs                     # Arayüz Sözleşmesi
│       │   ├── Vehicle.cs                       # Soyut Temel Araç Sınıfı
│       │   ├── Car.cs                           # Otomobil Sınıfı
│       │   ├── Suv.cs                           # SUV Sınıfı
│       │   ├── Customer.cs                      # Müşteri Sınıfı
│       │   └── Rental.cs                        # Kiralama Sözleşme Sınıfı
│       ├── Services/                            # İş Mantığı Katmanı
│       │   └── RentalManager.cs                 # Generic List<T>, CRUD ve İstatistikler
│       ├── Program.cs                           # Uygulama Giriş Noktası
│       └── VehicleRentalSystem.csproj
│
├── 02_Application/
│   └── Release/                                 # Derlenmiş Çalıştırılabilir Masaüstü Uygulaması
│       ├── VehicleRentalSystem.exe              # Doğrudan Tıklayıp Çalıştırılacak Dosya
│       ├── VehicleRentalSystem.dll
│       └── VehicleRentalSystem.runtimeconfig.json
│
├── 03_Report/
│   └── Proje_Raporu.pdf                         # Detaylı 10 Bölümlük Teknik Rapor
│
├── 04_GitHub/
│   ├── README.md                                # GitHub Bilgilendirme Dosyası
│   └── GITHUB_INFO.txt                          # Repository Bağlantısı ve Collaborator Bilgisi
│
└── README.md                                    # Kök Dizin Bilgilendirme Dosyası
```

---

## 🚀 Projeyi Çalıştırma Yönergeleri

### Yöntem 1: Doğrudan Çalıştırılabilir Dosya İle (En Hızlı)
1. `02_Application/Release/` klasörüne girin.
2. `VehicleRentalSystem.exe` dosyasına çift tıklayarak uygulamayı anında başlatabilirsiniz.

### Yöntem 2: Visual Studio İle Kaynak Koddan Çalıştırma
1. `01_SourceCode/VehicleRentalSystem.sln` dosyasını Visual Studio 2022 veya üzeri ile açın.
2. Üst menüden derleme yapılandırmasını `Debug` veya `Release` olarak seçin.
3. Klavyeden `F5` tuşuna basın veya `Başlat (Start)` butonuna tıklayın.

### Yöntem 3: .NET CLI ile Terminalden Çalıştırma
Proje dizininde PowerShell veya komut satırını açıp şu komutları uygulayabilirsiniz:
```bash
cd 01_SourceCode/VehicleRentalSystem
dotnet run
```

---

## 🧪 Şartnamede Belirtilen 5 Zorunlu Test Senaryosu

1. **Müsait Araç Kiralama:** Müsait durumdaki bir araç seçilip geçerli tarihler girildiğinde toplam kira tutarı gün ve indirim/kasko hesabı yapılarak oluşturulur, araç durumu anında "Kirada"ya döner.
2. **Kiradaki Aracı Tekrar Kiralamayı Engelleme:** Kiralama ekranındaki araç listesinde yalnızca `Status == Available` olan müsait araçlar listelenir. Böylece kiradaki bir aracın mükerrer kiralanması engellenir.
3. **Geçersiz Tarih Girişi Kontrolü:** Kiralama bitiş tarihi başlangıç tarihinden geriye seçildiğinde sistem hata verir ve kiralama oluşturulamaz.
4. **Eksik veya Hatalı Bilgi Kontrolü:** Zorunlu alanlar (plaka, ad-soyad, telefon, ehliyet) boş bırakıldığında veya günlük ücret 0 veya negatif girildiğinde kullanıcıya uyarı kutusu gösterilir.
5. **İade İşlemi:** İade ekranından aktif kiralama seçilip onaylandığında kiralama durumu "Tamamlandı" yapılır ve araç tekrar sistemde "Müsait" durumuna geçirilir.
