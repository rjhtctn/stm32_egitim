# 06. ADC Uygulaması: Analog Değer ile LED Kontrolü

Bu proje, **STM32F303RE** mikrodenetleyicisinde ADC (Analog-Dijital Çevirici) kullanılarak okunan voltaj seviyesine göre farklı LED gruplarının kontrol edilmesini gösterir.

Uygulamada, bir potansiyometre üzerinden okunan analog veri dijital bir eşik değeriyle (Threshold) karşılaştırılır ve buna göre çıkışlar anahtarlanır.

![Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)
![Peripheral](https://img.shields.io/badge/Peripheral-ADC-blue)

## ⚙️ Donanım ve Pin Ayarları

Bu projede 1 Analog Giriş ve 4 Dijital Çıkış kullanılmıştır:

| Pin | Donanım | İşlev | Açıklama |
| :--- | :--- | :--- | :--- |
| **PA0** | Potansiyometre | **ADC_IN1** | Analog giriş (0V - 3.3V). |
| **PA1** | LED 1 | Output | 1. Grup LED |
| **PA4** | LED 2 | Output | 2. Grup LED |
| **PB0** | LED 3 | Output | 1. Grup LED |
| **PC1** | LED 4 | Output | 2. Grup LED |

## 📝 Yazılımın Çalışma Mantığı

1.  **ADC Konfigürasyonu:**
    * **Çözünürlük:** **8-Bit** olarak ayarlanmıştır. Bu, okunan değerin **0 ile 255** arasında olacağı anlamına gelir.
    * **Örnekleme:** Continuous Mode (Sürekli Mod) aktif edilmiştir.

2.  **Karar Mekanizması (`LedOn` Fonksiyonu):**
    * Okunan ADC değeri orta nokta olan **128** ile kıyaslanır.
    * **Durum 1 (< 128):** Potansiyometre 0V - 1.65V arasındaysa -> **LED1 ve LED3 Yanar.**
    * **Durum 2 (>= 128):** Potansiyometre 1.65V - 3.3V arasındaysa -> **LED2 ve LED4 Yanar.**

```c
/* LED Kontrol Mantığı */
if(adcValue < 128)
{
    // Düşük Voltaj Aralığı
    HAL_GPIO_WritePin(LED1_PORT, LED1_PIN, GPIO_PIN_SET); // LED1 Yak
    HAL_GPIO_WritePin(LED3_PORT, LED3_PIN, GPIO_PIN_SET); // LED3 Yak
}
else
{
    // Yüksek Voltaj Aralığı
    HAL_GPIO_WritePin(LED2_PORT, LED2_PIN, GPIO_PIN_SET); // LED2 Yak
    HAL_GPIO_WritePin(LED4_PORT, LED4_PIN, GPIO_PIN_SET); // LED4 Yak
}