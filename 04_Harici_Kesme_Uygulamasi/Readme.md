# 04. Harici Kesme Uygulaması (External Interrupt)

Bu proje, **STM32F303RE** mikrodenetleyicisinde buton kontrolünün **Harici Kesme (EXTI)** mekanizması ile nasıl yönetildiğini gösterir.

Önceki uygulamaların aksine, işlemci (CPU) ana döngüde butonu sürekli kontrol etmez (Polling yapmaz). Bunun yerine, butona basıldığı anda donanımsal bir sinyal (Interrupt) oluşur ve işlemci o anki işini bırakıp LED'in durumunu değiştirir.

![Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)
![Peripheral](https://img.shields.io/badge/Peripheral-GPIO_EXTI-blue)
![Mechanism](https://img.shields.io/badge/Mechanism-Interrupt-orange)

## ⚙️ Donanım ve Pin Ayarları

| Pin | Etiket | Mod | Donanım | Açıklama |
| :--- | :--- | :--- | :--- | :--- |
| **PC13** | `B1_Pin` | **External Interrupt (Falling Edge)** | User Button (Mavi) | Basıldığında (Düşen Kenar) kesme üretir. |
| **PA5** | `LD2_Pin` | **Output** | User LED (Yeşil) | Durumu (Yan/Sön) değiştirilir. |

## 📝 Yazılımın Çalışma Mantığı

1. **Konfigürasyon (`MX_GPIO_Init`):**
   * **PC13** pini, `GPIO_MODE_IT_FALLING` modunda ayarlanmıştır. Yani voltaj 3.3V'tan 0V'a düştüğü anda (butona basıldığında) tetiklenir.
   * **NVIC (Nested Vectored Interrupt Controller):** `EXTI15_10_IRQn` hattı önceliklendirilmiş ve aktif edilmiştir.

2. **Ana Döngü (`main.c` -> `while(1)`):**
   * Sonsuz döngü **tamamen boştur**. İşlemci burada hiçbir şey yapmadan bekler (Idle). Bu, işlemcinin başka işlerle meşgul olabileceğini simüle eder.

3. **Kesme Rutini (`stm32f3xx_it.c` -> `EXTI15_10_IRQHandler`):**
   * Butona basıldığında donanım otomatik olarak `main` dosyasından çıkar ve bu fonksiyona atlar.
   * Fonksiyon içinde **PC13** pininin `RESET` (Basılı) olup olmadığı kontrol edilir.
   * Eğer basılıysa, **PA5** pininin durumu `HAL_GPIO_TogglePin` ile terslenir (Yansıya söner, sönükse yanar).

```c
/* stm32f3xx_it.c dosyasındaki Kesme Servis Rutini (ISR) */
void EXTI15_10_IRQHandler(void)
{
  // Butona basıldığını teyit et
  if(HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13) == RESET){
      // LED durumunu değiştir (Toggle)
      HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
  }
  // Kesme bayrağını temizle (Bir sonraki kesme için hazırla)
  HAL_GPIO_EXTI_IRQHandler(B1_Pin);
}