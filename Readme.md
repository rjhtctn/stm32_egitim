# STM32F303RE ile Gömülü Sistemler Eğitim

![Language](https://img.shields.io/badge/Language-C-red)
![Platform](https://img.shields.io/badge/Platform-STM32F303RE-orange)
![IDE](https://img.shields.io/badge/IDE-STM32CubeIDE-brown)

---

### Bölüm 1: Genel Amaçlı Giriş Çıkış İşlemleri (GPIO)
Mikrodenetleyicinin dış dünya ile en temel iletişim yolu olan pin kontrollerinin öğrenilmesi.
* **1.1.** GPIO Çevresel Birimini Tanıma ve Blok Şeması
* **1.2.** Pull-Up ve Pull-Down Direnç Yapısı
* **1.3.** GPIO Konfigürasyonu (Mode, Speed, ODR, IDR)
* **1.4.** Çıkış Kontrolü Uygulaması: LED Yakma
* **1.5.** Giriş Kontrolü Uygulaması: Buton Durumu Okuma
* **1.6.** Bit Maskeleme ve Register İşlemleri ile LED Kontrolü

### Bölüm 2: Harici Kesme Birimi (External Interrupt)
İşlemciyi sürekli meşgul etmeden (polling yapmadan), bir olay gerçekleştiğinde tepki verme mekanizması.
* **2.1.** Kesme (Interrupt) Nedir, Nasıl Kullanılır?
* **2.2.** NVIC (Nested Vectored Interrupt Controller) ve Öncelik Ayarları
* **2.3.** Harici Kesme Konfigürasyonu (EXTI Line)
* **2.4.** Kesme ile Asenkron Buton Okuma ve LED Kontrolü

### Bölüm 3: Analog - Dijital Çevirici (ADC)
Analog sensör sinyallerinin dijital verilere dönüştürülmesi ve işlenmesi.
* **3.1.** Analog ve Dijital Sinyal Kavramları
* **3.2.** ADC Çevresel Biriminin Çalışma Mantığı (SAR Yapısı)
* **3.3.** ADC Konfigürasyonu (Resolution, Alignment, Sampling Time)
* **3.4.** Potansiyometre ile Voltaj Okuma Uygulaması
* **3.5.** ADC Kesmesi (Interrupt) ile Veri Okuma
* **3.6.** ADC Değerinden Gerçek Voltaj Hesaplama (Formülizasyon)
* **3.7.** Dahili Sıcaklık Sensörü ile Sıcaklık Ölçümü

### Bölüm 4: Zamanlayıcılar (Timers)
Zamanlama, sayma ve periyodik görevlerin yönetimi.
* **4.1.** Zamanlayıcı Nedir? Up-Counter ve Down-Counter Mantığı
* **4.2.** Genel Amaçlı Zamanlayıcılar (TIMx) ve Kurulumu
* **4.3.** Prescaler ve Period (Auto-Reload) Hesaplamaları
* **4.4.** Zamanlayıcı Kesmesi ile Periyodik LED Kontrolü
* **4.5.** SysTick Timer İncelemesi ve Gecikme Fonksiyonları
* **4.6.** Zamanlayıcı ile Saat (Clock) Uygulaması

### Bölüm 5: Doğrudan Bellek Erişimi (DMA)
İşlemciyi (CPU) kullanmadan çevresel birimler ve bellek arasında hızlı veri transferi.
* **5.1.** DMA (Direct Memory Access) Nedir?
* **5.2.** DMA Çalışma Modları (Circular, Normal) ve Kanal Seçimi
* **5.3.** DMA ile ADC Verisi Okuma Konfigürasyonu
* **5.4.** DMA Kesmeleri (Transfer Complete, Half Transfer)

### Bölüm 6: Seri Haberleşme Protokolleri: UART/USART
Bilgisayar ve diğer cihazlarla asenkron veri iletişimi.
* **6.1.** Haberleşme Protokollerine Giriş (Seri vs Paralel)
* **6.2.** UART ve USART Farkları, Baud Rate Kavramı
* **6.3.** USART Konfigürasyonu
* **6.4.** Bilgisayara Veri Gönderme (Transmit - Tx)
* **6.5.** Bilgisayardan Veri Alma (Receive - Rx)
* **6.6.** Interrupt (Kesme) Kullanarak Veri İletişimi

### Bölüm 7: I2C Haberleşme Protokolü
İki telli (SDA, SCL) senkron haberleşme arayüzü.
* **7.1.** I2C Nedir, Nasıl Çalışır? (Master/Slave Yapısı)
* **7.2.** Harici Modül Tanıtımı (DS3231 RTC)
* **7.3.** I2C Adresleme ve Register Okuma/Yazma Mantığı
* **7.4.** I2C Hattına Bağlı Cihazları Bulan Tarayıcı (Scanner) Yazılımı
* **7.5.** Gerçek Zamanlı Saat (RTC) Uygulaması

### Bölüm 8: SPI Haberleşme Protokolü
Yüksek hızlı, tam çift yönlü (Full-Duplex) senkron haberleşme.
* **8.1.** SPI Nedir? (MISO, MOSI, SCK, CS Pinleri)
* **8.2.** SPI Konfigürasyonu (CPOL, CPHA Modları)
* **8.3.** Sensör Veri Sayfasını (Datasheet) İnceleme
* **8.4.** Sensörden (Örn: İvmeölçer) Register Okuma ve Yazma
* **8.5.** X, Y, Z Eksen Verilerinin Anlık Takibi

### Bölüm 9: Hafıza Birimi Yönetimi
Mikrodenetleyicinin dahili hafızasına erişim.
* **9.1.** STM32 Hafıza Haritası (Memory Map) İncelemesi
* **9.2.** Flash Bellek Yapısı (Sektörler ve Sayfalar)
* **9.3.** Dahili Flash Birimine Veri Yazma
* **9.4.** Dahili Flash Biriminden Veri Okuma

### Bölüm 10: Rastgele Numara Üretici (RNG)
* **10.1.** Donanımsal RNG Birimi ve Entropi Kaynakları
* **10.2.** Rastgele Sayı Üretimi ve Olasılık Uygulamaları

---

## 💻 Teknik Altyapı
Bu müfredat aşağıdaki araçlar kullanılarak uygulanmıştır:
* **Geliştirme Ortamı:** STM32CubeIDE
* **Donanım:** NUCLEO-F303RE (STM32F303RET6)
* **Kütüphane:** STM32 HAL (Hardware Abstraction Layer)