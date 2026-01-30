# 01. GPIO Dijital Çıkış Uygulaması (Digital Output)

Bu proje, **STM32F303RE** mikrodenetleyicisinde bir GPIO pininin "Output" (Çıkış) olarak ayarlanmasını ve lojik seviyesinin kontrol edilmesini gösterir.

Uygulamada, Nucleo geliştirme kartı üzerindeki kullanıcı LED'i (LD2) yazılımsal olarak yakılmıştır.

![Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)
![Peripheral](https://img.shields.io/badge/Peripheral-GPIO-blue)

## ⚙️ Donanım ve Pin Yapılandırması

Proje, STM32F303RE (Nucleo-64) donanımına göre aşağıdaki pin ayarlarını kullanır:

| Pin | Etiket | Mod | Durum | Açıklama |
|---|---|---|---|---|
| **PA5** | `LD2_Pin` | **Output Push-Pull** | **High (1)** | Kart üzerindeki Yeşil LED |

## 📝 Yazılım Mantığı

Kodun çalışma adımları şöyledir:

1. **Sistem Saati Ayarı:**  
   İşlemci, dahili osilatör (HSI) ve PLL kullanılarak **72 MHz** hızında çalışacak şekilde yapılandırıldı.

2. **GPIO Başlatma (`MX_GPIO_Init`):**
   - `GPIOA` portunun saati aktif edildi.
   - `PA5` pini çıkış (Output) moduna alındı.

3. **Ana Döngü (`while(1)`):**
   - Sonsuz döngü içerisinde `PA5` pinine 3.3V (Lojik 1) verilerek LED'in sürekli yanması sağlandı.

### Kullanılan Temel Fonksiyon

```c
/*
 * GPIOA Portunun 5. Pinini (PA5) Lojik-1 (High) yapar.
 * Sonuç: LED Yanar.
 */
HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);
