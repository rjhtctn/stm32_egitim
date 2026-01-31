# 08. ADC ile Voltaj Hesaplama

Bu proje, **STM32F303RE** mikrodenetleyicisinde ADC üzerinden okunan ham dijital verinin (Raw Data), yazılımsal olarak **Volt (V)** birimine dönüştürülmesini gösterir.

Uygulamada, Polling (Sorgulama) yöntemiyle okunan 12-bitlik ADC değeri, referans voltajı (3.3V) baz alınarak işlenir.

![Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)
![Peripheral](https://img.shields.io/badge/Peripheral-ADC-blue)
![Operation](https://img.shields.io/badge/Operation-Voltage_Calculation-orange)

## ⚙️ Donanım ve Pin Ayarları

| Pin | Donanım | Kanal | Açıklama |
| :--- | :--- | :--- | :--- |
| **PA0** | Potansiyometre | **ADC1_IN1** | Analog giriş (0V - 3.3V). |

## 📝 Yazılımın Çalışma Mantığı

1.  **ADC Konfigürasyonu:**
    * **Çözünürlük:** 12-Bit (0 ile 4095 arası).
    * **Referans Voltajı:** 3.3V (STM32 Nucleo kartlarında varsayılan).

2.  **Okuma ve Hesaplama (`main.c` -> `while(1)`):**
    * **Adım 1:** `ReadAdcValue()` fonksiyonu ile ham veri (0-4095) okunur.
    * **Adım 2:** Okunan değer aşağıdaki formül ile Volt cinsine çevrilir ve `float` (ondalıklı) türündeki değişkene yazılır.

### Voltaj Hesaplama Formülü

Mikrodenetleyici 3.3V referans gerilimi ve 12-bit (2^12 - 1 = 4095) çözünürlük kullandığı için formül şu şekildedir:

```c
/*
 * Formül: Voltaj = Referans_Voltajı * (Okunan_ADC / Maks_ADC_Değeri)
 * Örnek:  1.65V  = 3.3 * (2048 / 4095)
 */
analogVoltaj = 3.3 * (float)(analogVeriler / 4095.0);