# 02. GPIO Giriş Uygulaması: Buton Okuma

Bu proje, **STM32F303RE** mikrodenetleyicisinde bir GPIO pininin **Giriş (Input)** olarak yapılandırılmasını ve buton durumunun okunmasını gösterir.

Uygulamada, Nucleo kartı üzerindeki kullanıcı butonu (B1) sürekli taranarak (polling yöntemiyle) durumu bir değişkene aktarılır.

![Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)
![Peripheral](https://img.shields.io/badge/Peripheral-GPIO_Input-blue)

## ⚙️ Donanım ve Pin Ayarları

Bu proje için Nucleo-F303RE kartındaki şu bağlantılar kullanılmıştır:

| Pin | Etiket | Donanım | Açıklama |
| :--- | :--- | :--- | :--- |
| **PC13** | `B1_Pin` | **User Button (Mavi)** | Giriş (Input) olarak ayarlandı. |
| **PA5** | `LD2_Pin` | **User LED (Yeşil)** | Çıkış (Output) - *Bu uygulamada kullanılmadı.* |

## 📝 Yazılımın Çalışma Mantığı

Kodun işleyişi şu adımlardan oluşur:

1.  **Sistem Saati:** İşlemci hızı 72 MHz olarak ayarlanmıştır.
2.  **GPIO Başlatma:** `PC13` pini giriş modunda aktif edilmiştir.
3.  **Ana Döngü (`while(1)`):**
    * Kod sürekli olarak `GPIOC` portunun 13. pinini kontrol eder.
    * Okunan değer (0 veya 1), `butonDurumu` adlı değişkene yazılır.

```c
/* Ana döngü içerisindeki okuma komutu */
while (1)
{
  // Butonun anlık durumunu oku ve değişkene kaydet
  butonDurumu = HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13);
}