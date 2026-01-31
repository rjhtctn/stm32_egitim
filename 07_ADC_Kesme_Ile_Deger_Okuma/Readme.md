# 07. ADC Uygulaması: Kesme (Interrupt) ile Okuma

Bu proje, **STM32F303RE** mikrodenetleyicisinde analog verinin **Interrupt (Kesme)** yöntemi kullanılarak okunmasını gösterir.

Polling yönteminin aksine, bu yöntemde işlemci ADC çevrimini bekleyerek vakit kaybetmez. ADC modülü arka planda çevrim işlemini yapar ve işlem bittiğinde işlemciye haber verir (Kesme üretir).

![Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)
![Peripheral](https://img.shields.io/badge/Peripheral-ADC_Interrupt-blue)

## ⚙️ Donanım ve Pin Ayarları

| Pin | Donanım | Kanal | Açıklama |
| :--- | :--- | :--- | :--- |
| **PA0** | Potansiyometre | **ADC1_IN1** | Analog giriş pini. |

## 📝 Yazılımın Çalışma Mantığı

1.  **ADC Konfigürasyonu (`MX_ADC1_Init`):**
    * **Çözünürlük:** 12-Bit (0 - 4095 arası değer).
    * **Mod:** Continuous Conversion (Sürekli Çevrim) -> `ENABLE`.
    * **Kesme:** NVIC üzerinden ADC global kesmesi aktif edilmiştir.

2.  **Başlatma (`main.c`):**
    * `HAL_ADC_Start_IT(&hadc1)` komutu ile ADC hem başlatılır hem de kesmeleri açılır.
    * Ana döngü (`while(1)`) **tamamen boştur**.

3.  **Kesme Rutini (`stm32f3xx_it.c` -> `ADC1_2_IRQHandler`):**
    * ADC her çevrimi tamamladığında (Continuous mod olduğu için sürekli tamamlar), program otomatik olarak bu fonksiyona atlar.
    * Fonksiyon içerisinde `HAL_ADC_GetValue` ile değer okunur ve `adcValue` global değişkenine yazılır.

```c
/* Interrupt Service Routine (ISR) - stm32f3xx_it.c */
void ADC1_2_IRQHandler(void)
{
    // ADC çevrimi bitti, değeri oku ve değişkene yaz
    adcValue = HAL_ADC_GetValue(&hadc1);
    
    // Kesme bayrağını temizle
    HAL_ADC_IRQHandler(&hadc1);
}