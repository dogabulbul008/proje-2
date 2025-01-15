# proje-2
# Tiva C Timer + LCD Projesi

Bu proje, Tiva C serisi mikrokontrolcü kullanarak zamanı güncelleyip bir LCD ekranda görüntüleyen bir uygulamayı ele almaktadır. Visual Studio kullanılarak geliştirilen kod, Timer modülü, GPIO ve kesmelerin nasıl kullanılabileceğini detaylı bir şekilde açıklamaktadır.

## Projenin Amaçları

1. Tiva C platformunda Timer ve kesme mekanizmasını kullanarak zamanı takip etmek.
2. Zaman bilgilerini formatlayıp bir 16x2 LCD ekranda görüntülemek.
3. GPIO kullanarak LED durumu ile zamanın ilerleyişini görselleştirmek.

## İçerik ve İşlevler

### 1. Donanım Gereksinimleri

- Tiva C LaunchPad (TM4C123GXL)
- 16x2 LCD ekran
- GPIO pinleri (LCD için RS, E, D4-D7)
- Timer modülü (1 saniye periyodik kesme için)
- GPIO LED'ler (test ve görsel geribildirim için)

### 2. Yazılım Bileşenleri

- **Driver Library**: TivaWare’in GPIO, Timer, Interrupt ve SysCtl modülleri kullanılmıştır.
- **Kesme Mekanizması**: Timer 0, 1 saniye periyodik kesme tetikler.
- **LCD Kontrolü**: 4-bit modunda veri ve komut iletimi gerçekleştirilir.
- **Zaman Formatlama**: Saat, dakika ve saniye bilgisi bir string olarak formatlanır ve LCD'de gösterilir.

### 3. Kod Yapısı

#### Ana Bileşenler

1. **main()**

   - LCD'yi başlatır (`lcd_init`).
   - Timer ve kesmeleri ayarlayan `SetInitSettings` fonksiyonunu çağırır.
   - Zamanı güncelleyip LCD'ye yazdırma işlemleri kesme mekanizmasında gerçekleştirildiği için ana döngüyö boş bırakır.

2. **SetInitSettings()**

   - Timer0 modülü 1 saniyelik periyodik kesme üretecek şekilde ayarlanır.
   - Timer kesmeleri için `timerkesmefonksiyonu` atanır.

3. **timerkesmefonksiyonu()**

   - Timer0 kesme bayrağı temizlenir.
   - Saat, dakika ve saniye bilgisi güncellenir.
   - Formatlanmış zaman bilgisi LCD'ye yazdırılır.
   - GPIO PF2 pinindeki LED durumu her kesmede değiştirilerek zaman ilerleyişi görselleştirilir.

4. **LCD Fonksiyonları**

   - `lcd_init()`: LCD'yi 4-bit modunda çalışacak şekilde başlatır.
   - `lcd_command()`: LCD'ye komut gönderir.
   - `lcd_data()`: LCD'ye veri gönderir (karakter).
   - `lcd_print()`: Bir stringi LCD'de yazdırır.

5. **Zaman Formatlama**

   - `format_time()`: Saat, dakika ve saniye bilgilerini “HH\:MM\:SS” formatında bir string olarak oluşturur.

### 4. LCD ve GPIO Ayarları

- LCD’nin GPIO portu: **Port B**

  - RS: PB0
  - E: PB1
  - D4-D7: PB4-PB7

- LED GPIO portu: **Port F**

  - PF1, PF2, PF3: LED kontrolü için çıkış olarak ayarlanmıştır.

### 5. Periyodik Kesme

- Timer0, 40 MHz sistem saatini kullanarak 1 saniyelik kesmeler üretir.
- Bu kesmelerde zaman bilgisi güncellenir ve LCD’ye yazılır.

### 6. Görsel Geri Bildirim

- GPIO PF2 LED durumu her kesmede değiştirilerek zamanın ilerleyişi görselleştirilmiştir.

---

## Projeyi Çalıştırma Adımları

### 1. Donanım Bağlantısı

- LCD’yi Port B pinlerine bağlayın.
- LED için Port F pinlerini kullanın.
- Timer modülü ve kesmelerin doğru bir şekilde çalışması için Tiva C kartının 40 MHz frekansında çalıştığından emin olun.

### 2. Yazılım Yükleme

- Proje dosyasını Visual Studio veya Tiva IDE'ye aktarın.
- Kodu derleyin ve Tiva C LaunchPad'e yükleyin.

### 3. Sonuçları Gözlemleme

- LCD ekranda zaman bilgisi formatında (HH\:MM\:SS) görüntülenir.
- GPIO PF2 LED’in yanıp söndüğünü gözlemleyerek kesme mekanizmasının çalıştığından emin olun.

---

## Geliştirme Fırsatları

1. **Alarm Sistemi**: Belirli bir zamanda alarm vererek LED veya buzzer kullanılabilir.
2. **Zaman Ayarı**: Kullanıcının zamanı ayarlayabilmesi için bir tuştakımı entegre edilebilir.
3. **Daha Karmaşık LCD Kullanımı**: Tarih bilgisi veya mesajlar eklenebilir.

---

## Lisans

Bu proje MIT Lisansı altında sunulmuştur.


