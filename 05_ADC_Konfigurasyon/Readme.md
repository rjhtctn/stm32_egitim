# 05. ADC Konfigürasyonu ve Analog Okuma (Polling)

Bu proje, **STM32F303RE** mikrodenetleyicisinin ADC (Analog-Dijital Çevirici) birimini kullanarak analog bir sinyalin nasıl okunacağını gösterir.

Uygulamada, en temel yöntem olan **Polling (Sorgulama)** yöntemi kullanılmıştır. İşlemci, ADC çevrimini başlatır, bitmesini bekler ve sonucu bir değişkene yazar.

![Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)
![Peripheral](https://img.shields.io/badge/Peripheral-ADC-blue)

## ⚙️ Donanım ve Pin Ayarları

Kod içerisinde ADC1 birimi tek kanal üzerinden okuma yapacak şekilde ayarlanmıştır:

| Pin | Donanım | Kanal | Açıklama |
| :--- | :--- | :--- | :--- |
| **PA0** | Potansiyometre / Sensör | **ADC1_IN1** | Analog giriş pini. |

## 📝 Yazılımın Çalışma Mantığı

1.  **Sistem Ayarları:** İşlemci 72 MHz hızında çalıştırılmıştır.
2.  **ADC Ayarları (`MX_ADC1_Init`):**
    * **Çözünürlük:** 12-Bit (0 - 4095 arası değer).
    * **Mod:** Tekli Çevrim (Single Conversion).
    * **Hız:** Async Clock / 1 Cycle Sampling.
3.  **Okuma Fonksiyonu (`ReadAdcValue`):**
    * `HAL_ADC_Start`: Çevrimi başlatır.
    * `HAL_ADC_PollForConversion`: Çevrim bitene kadar (max 1000ms) işlemciyi bekletir.
    * `HAL_ADC_GetValue`: Dönüştürülen dijital veriyi okur.
    * `HAL_ADC_Stop`: ADC'yi durdurur.

```c
/* Polling yöntemiyle ADC okuma fonksiyonu */
uint32_t ReadAdcValue(void)
{
    uint32_t adcValue = 0;
    HAL_ADC_Start(&hadc1);                 // 1. Başlat
    HAL_ADC_PollForConversion(&hadc1, 1000); // 2. Bekle
    adcValue = HAL_ADC_GetValue(&hadc1);   // 3. Oku
    HAL_ADC_Stop(&hadc1);                  // 4. Durdur
    return adcValue;
}