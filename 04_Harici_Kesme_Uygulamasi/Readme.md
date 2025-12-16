\# 04. Harici Kesme Uygulaması (External Interrupt)



Bu proje, \*\*STM32F303RE\*\* mikrodenetleyicisinde buton kontrolünün \*\*Harici Kesme (EXTI)\*\* mekanizması ile nasıl yönetildiğini gösterir.



Önceki uygulamaların aksine, işlemci (CPU) ana döngüde butonu sürekli kontrol etmez (Polling yapmaz). Bunun yerine, butona basıldığı anda donanımsal bir sinyal (Interrupt) oluşur ve işlemci o anki işini bırakıp LED'in durumunu değiştirir.



!\[Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)

!\[Peripheral](https://img.shields.io/badge/Peripheral-GPIO\_EXTI-blue)

!\[Mechanism](https://img.shields.io/badge/Mechanism-Interrupt-orange)



\## ⚙️ Donanım ve Pin Ayarları



| Pin | Etiket | Mod | Donanım | Açıklama |

| :--- | :--- | :--- | :--- | :--- |

| \*\*PC13\*\* | `B1\_Pin` | \*\*External Interrupt (Falling Edge)\*\* | User Button (Mavi) | Basıldığında (Düşen Kenar) kesme üretir. |

| \*\*PA5\*\* | `LD2\_Pin` | \*\*Output\*\* | User LED (Yeşil) | Durumu (Yan/Sön) değiştirilir. |



\## 📝 Yazılımın Çalışma Mantığı



1\.  \*\*Konfigürasyon (`MX\_GPIO\_Init`):\*\*

&nbsp;   \* \*\*PC13\*\* pini, `GPIO\_MODE\_IT\_FALLING` modunda ayarlanmıştır. Yani voltaj 3.3V'tan 0V'a düştüğü anda (butona basıldığında) tetiklenir.

&nbsp;   \* \*\*NVIC (Nested Vectored Interrupt Controller):\*\* `EXTI15\_10\_IRQn` hattı önceliklendirilmiş ve aktif edilmiştir.



2\.  \*\*Ana Döngü (`main.c` -> `while(1)`):\*\*

&nbsp;   \* Sonsuz döngü \*\*tamamen boştur\*\*. İşlemci burada hiçbir şey yapmadan bekler (Idle). Bu, işlemcinin başka işlerle meşgul olabileceğini simüle eder.



3\.  \*\*Kesme Rutini (`stm32f3xx\_it.c` -> `EXTI15\_10\_IRQHandler`):\*\*

&nbsp;   \* Butona basıldığında donanım otomatik olarak `main` dosyasından çıkar ve bu fonksiyona atlar.

&nbsp;   \* Fonksiyon içinde \*\*PC13\*\* pininin `RESET` (Basılı) olup olmadığı kontrol edilir.

&nbsp;   \* Eğer basılıysa, \*\*PA5\*\* pininin durumu `HAL\_GPIO\_TogglePin` ile terslenir (Yansıya söner, sönükse yanar).



```c

/\* stm32f3xx\_it.c dosyasındaki Kesme Servis Rutini (ISR) \*/

void EXTI15\_10\_IRQHandler(void)

{

&nbsp; // Butona basıldığını teyit et

&nbsp; if(HAL\_GPIO\_ReadPin(GPIOC, GPIO\_PIN\_13) == RESET){

&nbsp;     // LED durumunu değiştir (Toggle)

&nbsp;     HAL\_GPIO\_TogglePin(GPIOA, GPIO\_PIN\_5);

&nbsp; }

&nbsp; // Kesme bayrağını temizle (Bir sonraki kesme için hazırla)

&nbsp; HAL\_GPIO\_EXTI\_IRQHandler(B1\_Pin);

}

