\# 03. GPIO Giriş-Çıkış Uygulaması: Buton ile LED Kontrolü



Bu proje, \*\*STM32F303RE\*\* mikrodenetleyicisinde Dijital Giriş (Input) ve Dijital Çıkış (Output) işlemlerinin birlikte kullanımını gösterir.



Uygulamada, "Polling" (Sorgulama) yöntemi kullanılarak butonun durumu sürekli kontrol edilir. Butona basıldığında LED yanar, bırakıldığında söner.



!\[Platform](https://img.shields.io/badge/Donanım-NUCLEO--F303RE-green)

!\[Peripheral](https://img.shields.io/badge/Peripheral-GPIO-blue)



\## ⚙️ Donanım ve Pin Ayarları



Kod içerisinde aşağıdaki pinler aktif olarak kullanılmaktadır:



| Pin | Etiket | Mod | Donanım | Açıklama |

| :--- | :--- | :--- | :--- | :--- |

| \*\*PC13\*\* | `GPIO\_PIN\_13` | \*\*Input\*\* | User Button (Mavi) | Giriş pini (Pull-up/down yok). |

| \*\*PA5\*\* | `LD2\_Pin` | \*\*Output\*\* | User LED (Yeşil) | Çıkış pini. |



\## 📝 Yazılımın Çalışma Mantığı



Kodun akışı şu şekildedir:



1\.  \*\*Başlangıç:\*\* Sistem saati 72 MHz'e ayarlanır, GPIO portları (A ve C) aktif edilir.

2\.  \*\*Sonsuz Döngü (`while(1)`):\*\*

&nbsp;   \* İşlemci sürekli olarak \*\*PC13\*\* pinini okur.

&nbsp;   \* \*\*Koşul:\*\* Eğer okunan değer `RESET` (Lojik 0) ise —yani butona basılmışsa— \*\*PA5\*\* pinini `SET` (Lojik 1) yapar ve LED'i yakar.

&nbsp;   \* \*\*Değilse:\*\* Butona basılmıyorsa (`SET` / Lojik 1 ise), \*\*PA5\*\* pinini `RESET` yapar ve LED'i söndürür.



```c

/\* Ana döngü içerisindeki kontrol bloğu \*/

while (1)

{

&nbsp; // Butona basıldı mı? (Nucleo kartlarında butona basınca şaseye çeker -> RESET)

&nbsp; if(HAL\_GPIO\_ReadPin(GPIOC, GPIO\_PIN\_13) == RESET)

&nbsp; {

&nbsp;     // LED'i Yak

&nbsp;     HAL\_GPIO\_WritePin(GPIOA, GPIO\_PIN\_5, SET);

&nbsp; }

&nbsp; else

&nbsp; {

&nbsp;     // LED'i Söndür

&nbsp;     HAL\_GPIO\_WritePin(GPIOA, GPIO\_PIN\_5, RESET);

&nbsp; }

}

